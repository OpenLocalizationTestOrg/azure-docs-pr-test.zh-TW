---
title: "SQL Server FCI - Azure 虛擬機器 | Microsoft Docs"
description: "本文說明如何在 Azure 虛擬機器上建立 SQL Server 容錯移轉叢集執行個體。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 439353b7d22fb7376049ea8e1433a8d5840d3e0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="841e1-103">在 Azure 虛擬機器上設定 SQL Server 容錯移轉叢集執行個體</span><span class="sxs-lookup"><span data-stu-id="841e1-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="841e1-104">本文說明如何在 Resource Manager 模型內的 Azure 虛擬機器中，建立 SQL Server 容錯移轉叢集執行個體 (FCI)。</span><span class="sxs-lookup"><span data-stu-id="841e1-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="841e1-105">此解決方案會使用 [Windows Server 2016 Datacenter 版本儲存空間直接存取 \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) 做為軟體型虛擬 SAN，以同步 Windows 叢集中各節點 (Azure VM) 間的儲存體 (資料磁碟)。</span><span class="sxs-lookup"><span data-stu-id="841e1-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="841e1-106">S2D 是 Windows Server 2016 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="841e1-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="841e1-107">下圖顯示 Azure 虛擬機器中的完整解決方案：</span><span class="sxs-lookup"><span data-stu-id="841e1-107">The following diagram shows the complete solution on Azure virtual machines:</span></span>

![可用性群組](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="841e1-109">上圖顯示︰</span><span class="sxs-lookup"><span data-stu-id="841e1-109">The preceding diagram shows:</span></span>

- <span data-ttu-id="841e1-110">兩部位於 Windows 容錯移轉叢集中的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="841e1-111">位於容錯移轉叢集中的虛擬機器也稱為「叢集節點」或「節點」。</span><span class="sxs-lookup"><span data-stu-id="841e1-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="841e1-112">每部虛擬機器有兩個以上的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="841e1-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="841e1-113">S2D 會同步處理資料磁碟上的資料，並將已同步處理的儲存體當做儲存體集區使用。</span><span class="sxs-lookup"><span data-stu-id="841e1-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="841e1-114">儲存體集區會向容錯移轉提供叢集共用磁碟區 (CSV)。</span><span class="sxs-lookup"><span data-stu-id="841e1-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span></span>
- <span data-ttu-id="841e1-115">SQL Server FCI 叢集角色會針對資料硬碟使用 CSV。</span><span class="sxs-lookup"><span data-stu-id="841e1-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span></span>
- <span data-ttu-id="841e1-116">保留 SQL Server FCI IP 位址的 Azure Load Balancer。</span><span class="sxs-lookup"><span data-stu-id="841e1-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span></span>
- <span data-ttu-id="841e1-117">保留所有資源的 Azure 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="841e1-117">An Azure availability set holds all the resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="841e1-118">圖表內的所有 Azure 資源都位於相同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="841e1-118">All Azure resources are in the diagram are in the same resource group.</span></span>

<span data-ttu-id="841e1-119">如需有關 S2D 的詳細資料，請參閱 [Windows Server 2016 Datacenter 版本儲存空間直接存取 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)。</span><span class="sxs-lookup"><span data-stu-id="841e1-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="841e1-120">S2D 支援兩種類型的架構 - 交集和超交集。</span><span class="sxs-lookup"><span data-stu-id="841e1-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="841e1-121">本文件中的架構為超交集。</span><span class="sxs-lookup"><span data-stu-id="841e1-121">The architecture in this document is hyper-converged.</span></span> <span data-ttu-id="841e1-122">超交集基礎結構會將儲存體放置於與裝載叢集應用程式相同的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="841e1-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span></span> <span data-ttu-id="841e1-123">在此架構中，儲存體會放置在每個 SQL Server FCI 節點上。</span><span class="sxs-lookup"><span data-stu-id="841e1-123">In this architecture, the storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="841e1-124">Azure 範本範例</span><span class="sxs-lookup"><span data-stu-id="841e1-124">Example Azure template</span></span>

<span data-ttu-id="841e1-125">您可以在 Azure 中，從範本開始建立整個解決方案。</span><span class="sxs-lookup"><span data-stu-id="841e1-125">You can create the entire solution in Azure from a template.</span></span> <span data-ttu-id="841e1-126">GitHub [Azure 快速入門範本](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad) 內有提供範本範例。</span><span class="sxs-lookup"><span data-stu-id="841e1-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="841e1-127">此範例並非為任何特定工作負載而設計或測試。</span><span class="sxs-lookup"><span data-stu-id="841e1-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="841e1-128">您可以執行範本來建立 SQL Server FCI，並將 S2D 儲存區連接至您的網域。</span><span class="sxs-lookup"><span data-stu-id="841e1-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span></span> <span data-ttu-id="841e1-129">您可以評估此範本，並依需要進行修改。</span><span class="sxs-lookup"><span data-stu-id="841e1-129">You can evaluate the template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="841e1-130">開始之前</span><span class="sxs-lookup"><span data-stu-id="841e1-130">Before you begin</span></span>

<span data-ttu-id="841e1-131">開始之前，您必須先了解一些需要注意的事項，並先備妥幾個項目。</span><span class="sxs-lookup"><span data-stu-id="841e1-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-to-know"></a><span data-ttu-id="841e1-132">注意事項</span><span class="sxs-lookup"><span data-stu-id="841e1-132">What to know</span></span>
<span data-ttu-id="841e1-133">您應了解下列技術的操作方式：</span><span class="sxs-lookup"><span data-stu-id="841e1-133">You should have an operational understanding of the following technologies:</span></span>

- [<span data-ttu-id="841e1-134">Windows 叢集技術</span><span class="sxs-lookup"><span data-stu-id="841e1-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="841e1-135">[SQL Server 容錯移轉叢集執行個體](http://msdn.microsoft.com/library/ms189134.aspx)。</span><span class="sxs-lookup"><span data-stu-id="841e1-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="841e1-136">此外，您也應對下列技術有大概了解：</span><span class="sxs-lookup"><span data-stu-id="841e1-136">Also, you should have a general understanding of the following technologies:</span></span>

- [<span data-ttu-id="841e1-137">在 Windows Server 2016 中使用儲存空間直接存取的超交集解決方案</span><span class="sxs-lookup"><span data-stu-id="841e1-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="841e1-138">Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="841e1-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-to-have"></a><span data-ttu-id="841e1-139">應備項目</span><span class="sxs-lookup"><span data-stu-id="841e1-139">What to have</span></span>

<span data-ttu-id="841e1-140">在依照本文中的指示進行之前，您應先備妥下列項目：</span><span class="sxs-lookup"><span data-stu-id="841e1-140">Before following the instructions in this article, you should already have:</span></span>

- <span data-ttu-id="841e1-141">Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="841e1-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="841e1-142">Azure 虛擬機器上的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="841e1-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="841e1-143">擁有在 Azure 虛擬機器中建立物件之權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="841e1-143">An account with permission to create objects in the Azure virtual machine.</span></span>
- <span data-ttu-id="841e1-144">Azure 虛擬網路和子網路，且具有足夠 IP 位址空間以容納下列元件：</span><span class="sxs-lookup"><span data-stu-id="841e1-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span></span>
   - <span data-ttu-id="841e1-145">兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-145">Both virtual machines.</span></span>
   - <span data-ttu-id="841e1-146">容錯移轉叢集的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-146">The failover cluster IP address.</span></span>
   - <span data-ttu-id="841e1-147">每個 FCI 上一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="841e1-148">設定 Azure 網路上的 DNS，並指向網域控制站。</span><span class="sxs-lookup"><span data-stu-id="841e1-148">DNS configured on the Azure Network, pointing to the domain controllers.</span></span>

<span data-ttu-id="841e1-149">備妥這些先決條件後，便可繼續建置您的容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="841e1-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="841e1-150">第一步是建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-150">The first step is to create the virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="841e1-151">步驟 1：建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="841e1-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="841e1-152">使用您的訂用帳戶登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="841e1-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="841e1-153">[建立 Azure 可用性設定組](../tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="841e1-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="841e1-154">可用性設定組群組虛擬機器遍佈在容錯網域與更新網域中，</span><span class="sxs-lookup"><span data-stu-id="841e1-154">The availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="841e1-155">可用性設定組可確保應用程式不受單一失敗點 (如網路交換器或伺服器機架的電源裝置) 所影響。</span><span class="sxs-lookup"><span data-stu-id="841e1-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span></span>

   <span data-ttu-id="841e1-156">若您尚未建立虛擬機器的資源群組，請在建立 Azure 可用性設定組時建立。</span><span class="sxs-lookup"><span data-stu-id="841e1-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="841e1-157">若您正在使用 Azure 入口網站建立可用性設定組，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="841e1-157">If you're using the Azure portal to create the availability set, do the following steps:</span></span>

   - <span data-ttu-id="841e1-158">在 Azure 入口網站中，按一下 **+** 以開啟 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="841e1-158">In the Azure portal, click **+** to open the Azure Marketplace.</span></span> <span data-ttu-id="841e1-159">搜尋 [可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="841e1-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="841e1-160">按一下 [可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="841e1-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="841e1-161">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-161">Click **Create**.</span></span>
   - <span data-ttu-id="841e1-162">在 [建立可用性設定組] 刀鋒視窗中，設定下列值︰</span><span class="sxs-lookup"><span data-stu-id="841e1-162">On the **Create availability set** blade, set the following values:</span></span>
      - <span data-ttu-id="841e1-163">**名稱**：可用性設定組的名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-163">**Name**: A name for the availability set.</span></span>
      - <span data-ttu-id="841e1-164">**訂用帳戶**：您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="841e1-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="841e1-165">**資源群組**︰若您想要使用現有的群組，請按一下 [使用現有的群組] 並從下拉式清單中選取群組。</span><span class="sxs-lookup"><span data-stu-id="841e1-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span></span> <span data-ttu-id="841e1-166">否則，選擇 [建立新的] 並輸入群組名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-166">Otherwise choose **Create New** and type a name for the group.</span></span>
      - <span data-ttu-id="841e1-167">**位置**︰設定您計劃建立虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="841e1-167">**Location**: Set the location where you plan to create your virtual machines.</span></span>
      - <span data-ttu-id="841e1-168">**容錯網域**︰使用預設值 (3)。</span><span class="sxs-lookup"><span data-stu-id="841e1-168">**Fault domains**: Use the default (3).</span></span>
      - <span data-ttu-id="841e1-169">**更新網域**︰使用預設值 (5)。</span><span class="sxs-lookup"><span data-stu-id="841e1-169">**Update domains**: Use the default (5).</span></span>
   - <span data-ttu-id="841e1-170">按一下 [建立] 來建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="841e1-170">Click **Create** to create the availability set.</span></span>

1. <span data-ttu-id="841e1-171">在可用性設定組中建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-171">Create the virtual machines in the availability set.</span></span>

   <span data-ttu-id="841e1-172">在 Azure 可用性設定組中佈建兩部 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-172">Provision two SQL Server virtual machines in the Azure availability set.</span></span> <span data-ttu-id="841e1-173">如需指示，請參閱[在 Azure 入口網站中佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="841e1-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="841e1-174">將兩部虛擬機器放置於：</span><span class="sxs-lookup"><span data-stu-id="841e1-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="841e1-175">與可用性設定組相同的 Azure 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="841e1-175">In the same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="841e1-176">您網域控制站的相同網路上。</span><span class="sxs-lookup"><span data-stu-id="841e1-176">On the same network as your domain controller.</span></span>
   - <span data-ttu-id="841e1-177">有足夠 IP 位址空間存放兩部虛擬機器，與最終會用於此叢集的所有 FCI 的子網路上。</span><span class="sxs-lookup"><span data-stu-id="841e1-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="841e1-178">Azure 可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="841e1-178">In the Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="841e1-179">建立虛擬機器後，您無法設定或變更可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="841e1-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="841e1-180">從 Azure Marketplace 中選擇映像。</span><span class="sxs-lookup"><span data-stu-id="841e1-180">Choose an image from the Azure Marketplace.</span></span> <span data-ttu-id="841e1-181">您可以使用包含 Windows Server 與 SQL Server，或只包含 Windows Server 的 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="841e1-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span></span> <span data-ttu-id="841e1-182">如需詳細資料，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="841e1-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="841e1-183">Azure 資源庫中的官方 SQL Server 映像包含已安裝的 SQL Server 執行個體、SQL Server 安裝軟體與所需金鑰。</span><span class="sxs-lookup"><span data-stu-id="841e1-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span></span>

   <span data-ttu-id="841e1-184">按照您喜好的付款方式購買 SDL Server 授權，並選擇合適的映像：</span><span class="sxs-lookup"><span data-stu-id="841e1-184">Choose the right image according to how you want to pay for the SQL Server license:</span></span>

   - <span data-ttu-id="841e1-185">**每次使用授權時付款**：費用會以分鐘計算，且會包含下列 SQL Server 授權：</span><span class="sxs-lookup"><span data-stu-id="841e1-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span></span>
      - <span data-ttu-id="841e1-186">**Windows Server Datacenter 2016 上的 SQL Server 2016 Enterprise 版本**</span><span class="sxs-lookup"><span data-stu-id="841e1-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="841e1-187">**Windows Server Datacenter 2016 上的 SQL Server 2016 Standard 版本**</span><span class="sxs-lookup"><span data-stu-id="841e1-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="841e1-188">**Windows Server Datacenter 2016 上的 SQL Server 2016 Developer 版本**</span><span class="sxs-lookup"><span data-stu-id="841e1-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="841e1-189">**自備授權 (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="841e1-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="841e1-190">**{BYOL} Windows Server Datacenter 2016 上的 SQL Server 2016 Enterprise 版本**</span><span class="sxs-lookup"><span data-stu-id="841e1-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="841e1-191">**{BYOL} Windows Server Datacenter 2016 上的 SQL Server 2016 Standard 版本**</span><span class="sxs-lookup"><span data-stu-id="841e1-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="841e1-192">建立虛擬機器後，請移除預先安裝的獨立 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="841e1-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="841e1-193">設定容錯移轉叢集與 S2D 後，您將使用預先安裝的 SQL Server 媒體來建立 SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="841e1-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span></span>

   <span data-ttu-id="841e1-194">或者，您也可以只將 Azure Marketplace 映像與作業系統搭配使用。</span><span class="sxs-lookup"><span data-stu-id="841e1-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span></span> <span data-ttu-id="841e1-195">設定容錯移轉叢集與 S2D 後，請選擇 **Windows Server 2016 Datacenter** 映像並安裝 SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="841e1-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span></span> <span data-ttu-id="841e1-196">此映像不包含 SQL Server 安裝媒體。</span><span class="sxs-lookup"><span data-stu-id="841e1-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="841e1-197">將安裝媒體放置於可在每個伺服器上執行 SQL Server 安裝的位置。</span><span class="sxs-lookup"><span data-stu-id="841e1-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span></span>

1. <span data-ttu-id="841e1-198">Azure 建立虛擬機器後，請透過 RDP 連接至每部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span></span>

   <span data-ttu-id="841e1-199">首次透過 RDP 連接至虛擬機器時，電腦會詢問您是否允許此電腦在網路上可供搜尋。</span><span class="sxs-lookup"><span data-stu-id="841e1-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span></span> <span data-ttu-id="841e1-200">按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-200">Click **Yes**.</span></span>

1. <span data-ttu-id="841e1-201">若您正在使用其中一個 SQL Server 型虛擬機器映像，請移除 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="841e1-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span></span>

   - <span data-ttu-id="841e1-202">在 [程式和功能] 中，以滑鼠右鍵按一下 [Microsoft SQL Server 2016 (64 位元)] 然後按一下 [解除安裝/變更]。</span><span class="sxs-lookup"><span data-stu-id="841e1-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="841e1-203">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-203">Click **Remove**.</span></span>
   - <span data-ttu-id="841e1-204">選取預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="841e1-204">Select the default instance.</span></span>
   - <span data-ttu-id="841e1-205">移除所有在 [Database Engine 服務] 下的功能。</span><span class="sxs-lookup"><span data-stu-id="841e1-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="841e1-206">請勿移除 [共用功能]。</span><span class="sxs-lookup"><span data-stu-id="841e1-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="841e1-207">請參閱下圖︰</span><span class="sxs-lookup"><span data-stu-id="841e1-207">See the following picture:</span></span>

      ![移除功能](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="841e1-209">按一下 [下一步]，然後按一下 [移除]。</span><span class="sxs-lookup"><span data-stu-id="841e1-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="841e1-210"><a name="ports"></a>開啟防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="841e1-210"><a name="ports"></a>Open the firewall ports.</span></span>

   <span data-ttu-id="841e1-211">在每部虛擬機器上，開啟 Windows 防火牆上的下列連接埠。</span><span class="sxs-lookup"><span data-stu-id="841e1-211">On each virtual machine, open the following ports on the Windows Firewall.</span></span>

   | <span data-ttu-id="841e1-212">目的</span><span class="sxs-lookup"><span data-stu-id="841e1-212">Purpose</span></span> | <span data-ttu-id="841e1-213">TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="841e1-213">TCP Port</span></span> | <span data-ttu-id="841e1-214">注意事項</span><span class="sxs-lookup"><span data-stu-id="841e1-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="841e1-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="841e1-215">SQL Server</span></span> | <span data-ttu-id="841e1-216">1433</span><span class="sxs-lookup"><span data-stu-id="841e1-216">1433</span></span> | <span data-ttu-id="841e1-217">適用於 SDL Server 預設執行個體的一般連接埠。</span><span class="sxs-lookup"><span data-stu-id="841e1-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="841e1-218">若您曾使用來自資源庫的映像，此連接埠會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="841e1-218">If you used an image from the gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="841e1-219">健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="841e1-219">Health probe</span></span> | <span data-ttu-id="841e1-220">59999</span><span class="sxs-lookup"><span data-stu-id="841e1-220">59999</span></span> | <span data-ttu-id="841e1-221">任何開啟的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="841e1-221">Any open TCP port.</span></span> <span data-ttu-id="841e1-222">在接下來的步驟中，設定負載平衝器[健全狀況探查](#probe)和要使用此連接埠的叢集。</span><span class="sxs-lookup"><span data-stu-id="841e1-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span></span>  

1. <span data-ttu-id="841e1-223">將儲存體新增至虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="841e1-223">Add storage to the virtual machine.</span></span> <span data-ttu-id="841e1-224">如需詳細資訊，請參閱[新增儲存區](../../../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="841e1-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="841e1-225">每部虛擬機器需要至少兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="841e1-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="841e1-226">連接原始磁碟 - 非 NTFS 格式的磁碟。</span><span class="sxs-lookup"><span data-stu-id="841e1-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="841e1-227">若您連接 NTFS 格式的磁碟，您只能啟用 S2D 而無法進行磁碟適用性檢查。</span><span class="sxs-lookup"><span data-stu-id="841e1-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="841e1-228">每部 VM 至少可連接兩個進階儲存體 (SSD 磁碟)。</span><span class="sxs-lookup"><span data-stu-id="841e1-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span></span> <span data-ttu-id="841e1-229">建議使用 P30 (1 TB) 或以上的磁碟。</span><span class="sxs-lookup"><span data-stu-id="841e1-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="841e1-230">將主機快取設為**唯讀**。</span><span class="sxs-lookup"><span data-stu-id="841e1-230">Set host caching to **Read-only**.</span></span>

   <span data-ttu-id="841e1-231">在生產環境中使用的儲存體容量是依您的工作負載而定。</span><span class="sxs-lookup"><span data-stu-id="841e1-231">The storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="841e1-232">本文所描述的值僅供示範與測試之用。</span><span class="sxs-lookup"><span data-stu-id="841e1-232">The values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="841e1-233">[將虛擬機器新增至既存的網域](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)。</span><span class="sxs-lookup"><span data-stu-id="841e1-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="841e1-234">建立並設定虛擬機器後，您便可設定容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="841e1-234">After the virtual machines are created and configured, you can configure the failover cluster.</span></span>

## <a name="step-2-configure-the-windows-failover-cluster-with-s2d"></a><span data-ttu-id="841e1-235">步驟 2：透過 S2D 設定 Windows 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="841e1-235">Step 2: Configure the Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="841e1-236">下一步是透過 S2D 設定容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="841e1-236">The next step is to configure the failover cluster with S2D.</span></span> <span data-ttu-id="841e1-237">在此步驟中，您將執行下列子步驟：</span><span class="sxs-lookup"><span data-stu-id="841e1-237">In this step, you will do the following substeps:</span></span>

1. <span data-ttu-id="841e1-238">新增 Windows 容錯移轉叢集功能</span><span class="sxs-lookup"><span data-stu-id="841e1-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="841e1-239">驗證叢集</span><span class="sxs-lookup"><span data-stu-id="841e1-239">Validate the cluster</span></span>
1. <span data-ttu-id="841e1-240">建立容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="841e1-240">Create the failover cluster</span></span>
1. <span data-ttu-id="841e1-241">建立雲端見證</span><span class="sxs-lookup"><span data-stu-id="841e1-241">Create the cloud witness</span></span>
1. <span data-ttu-id="841e1-242">新增儲存體</span><span class="sxs-lookup"><span data-stu-id="841e1-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="841e1-243">新增 Windows 容錯移轉叢集功能</span><span class="sxs-lookup"><span data-stu-id="841e1-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="841e1-244">若要開始，請使用本機系統管理員成員，且具有在 Active Directory 中建立物件之權限的網域帳戶，透過 RDP 連接至第一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span></span> <span data-ttu-id="841e1-245">在之後的設定程序中繼續使用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="841e1-245">Use this account for the rest of the configuration.</span></span>

1. <span data-ttu-id="841e1-246">[將容錯移轉叢集功能新增至每部虛擬機器](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)。</span><span class="sxs-lookup"><span data-stu-id="841e1-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="841e1-247">若要從 UI 安裝容錯移轉叢集功能，請於兩部虛擬機器上執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="841e1-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span></span>
   - <span data-ttu-id="841e1-248">在 [伺服器管理員] 中，按一下 [管理]，然後按一下 [新增角色及功能]。</span><span class="sxs-lookup"><span data-stu-id="841e1-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="841e1-249">在 [新增角色及功能精靈] 中，連續按 [下一步] 直到到達 [選取功能]。</span><span class="sxs-lookup"><span data-stu-id="841e1-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span></span>
   - <span data-ttu-id="841e1-250">在 [選取功能] 中，按一下 [容錯移轉叢集]。</span><span class="sxs-lookup"><span data-stu-id="841e1-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="841e1-251">選取所有所需功能與管理工具。</span><span class="sxs-lookup"><span data-stu-id="841e1-251">Include all required features and the management tools.</span></span> <span data-ttu-id="841e1-252">按一下 [新增功能]。</span><span class="sxs-lookup"><span data-stu-id="841e1-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="841e1-253">按一下 [下一步]，然後按一下 [完成] 以安裝功能。</span><span class="sxs-lookup"><span data-stu-id="841e1-253">Click **Next** and then click **Finish** to install the features.</span></span>

   <span data-ttu-id="841e1-254">若要透過 PowerShell 安裝容錯移轉叢集功能，請在其中一部虛擬機器上執行下列來自系統管理員 PowerShell 工作階段的指令碼。</span><span class="sxs-lookup"><span data-stu-id="841e1-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="841e1-255">如需參考，請在接下來的步驟依照[在 Windows Server 2016 中使用儲存空間直接存取的超交集解決方案](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct) 步驟 3 的指示操作。</span><span class="sxs-lookup"><span data-stu-id="841e1-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-the-cluster"></a><span data-ttu-id="841e1-256">驗證叢集</span><span class="sxs-lookup"><span data-stu-id="841e1-256">Validate the cluster</span></span>

<span data-ttu-id="841e1-257">本指南參考[驗證叢集](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation)下的指示。</span><span class="sxs-lookup"><span data-stu-id="841e1-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="841e1-258">在 UI 中或透過 PowerShell 驗證叢集。</span><span class="sxs-lookup"><span data-stu-id="841e1-258">Validate the cluster in the UI or with PowerShell.</span></span>

<span data-ttu-id="841e1-259">若要透過 UI 驗證叢集，請在其中一部虛擬機器上執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="841e1-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span></span>

1. <span data-ttu-id="841e1-260">在 [伺服器管理員] 中，按一下 [工具]，然後按一下 [容錯移轉叢集管理員]。</span><span class="sxs-lookup"><span data-stu-id="841e1-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="841e1-261">在 [容錯移轉叢集管理員] 中，按一下 [動作]，然後按一下 [驗證設定...]。</span><span class="sxs-lookup"><span data-stu-id="841e1-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="841e1-262">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-262">Click **Next**.</span></span>
1. <span data-ttu-id="841e1-263">在 [選取伺服器或叢集] 中，輸入這兩部虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span></span>
1. <span data-ttu-id="841e1-264">在 [測試選項] 中，選擇 [僅執行我選取的測試]。</span><span class="sxs-lookup"><span data-stu-id="841e1-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="841e1-265">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-265">Click **Next**.</span></span>
1. <span data-ttu-id="841e1-266">在 [測試選取範圍] 中，選取**儲存體**以外的所有測試。</span><span class="sxs-lookup"><span data-stu-id="841e1-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="841e1-267">請參閱下圖︰</span><span class="sxs-lookup"><span data-stu-id="841e1-267">See the following picture:</span></span>

   ![驗證測試](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="841e1-269">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-269">Click **Next**.</span></span>
1. <span data-ttu-id="841e1-270">在 [確認] 中，，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="841e1-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="841e1-271">[驗證設定精靈] 會執行驗證測試。</span><span class="sxs-lookup"><span data-stu-id="841e1-271">The **Validate a Configuration Wizard** runs the validation tests.</span></span>

<span data-ttu-id="841e1-272">若要透過 PowerShell 驗證叢集，請在其中一部虛擬機器上，執行下列來自系統管理員 PowerShell 工作階段的指令碼。</span><span class="sxs-lookup"><span data-stu-id="841e1-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="841e1-273">驗證叢集後，請建立容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="841e1-273">After you validate the cluster, create the failover cluster.</span></span>

### <a name="create-the-failover-cluster"></a><span data-ttu-id="841e1-274">建立容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="841e1-274">Create the failover cluster</span></span>

<span data-ttu-id="841e1-275">本指南會參考[建立容錯移轉叢集](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster)。</span><span class="sxs-lookup"><span data-stu-id="841e1-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="841e1-276">若要建立容錯移轉叢集，您需要：</span><span class="sxs-lookup"><span data-stu-id="841e1-276">To create the failover cluster, you need:</span></span>
- <span data-ttu-id="841e1-277">成為叢集節點的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-277">The names of the virtual machines that become the cluster nodes.</span></span>
- <span data-ttu-id="841e1-278">容錯移轉叢集的名稱</span><span class="sxs-lookup"><span data-stu-id="841e1-278">A name for the failover cluster</span></span>
- <span data-ttu-id="841e1-279">容錯移轉叢集的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-279">An IP address for the failover cluster.</span></span> <span data-ttu-id="841e1-280">您可以使用與叢集節點一樣，沒有在 Azure 虛擬網路和子網路上用過的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span></span>

<span data-ttu-id="841e1-281">下列 PowerShell 會建立容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="841e1-281">The following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="841e1-282">使用節點名稱 (虛擬機器名稱) 和 Azure VNET 中可用的 IP 位址來更新指令碼：</span><span class="sxs-lookup"><span data-stu-id="841e1-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="841e1-283">建立雲端見證</span><span class="sxs-lookup"><span data-stu-id="841e1-283">Create a cloud witness</span></span>

<span data-ttu-id="841e1-284">雲端見證儲存在 Azure 儲存體 Blob 中，是一種新型的叢集仲裁見證。</span><span class="sxs-lookup"><span data-stu-id="841e1-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="841e1-285">如有雲端見證，便不再需要使用獨立的 VM 來裝載見證共用。</span><span class="sxs-lookup"><span data-stu-id="841e1-285">This removes the need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="841e1-286">[建立容錯移轉叢集的雲端見證](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)。</span><span class="sxs-lookup"><span data-stu-id="841e1-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="841e1-287">建立 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="841e1-287">Create a blob container.</span></span>

1. <span data-ttu-id="841e1-288">儲存存取金鑰和容器 URL。</span><span class="sxs-lookup"><span data-stu-id="841e1-288">Save the access keys and the container URL.</span></span>

1. <span data-ttu-id="841e1-289">設定容錯移轉叢集的叢集仲裁見證。</span><span class="sxs-lookup"><span data-stu-id="841e1-289">Configure the failover cluster cluster quorum witness.</span></span> <span data-ttu-id="841e1-290">請在 UI 中參閱 [在使用者介面中設定 WSFC 叢集仲裁見證] (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness)。</span><span class="sxs-lookup"><span data-stu-id="841e1-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="841e1-291">新增儲存體</span><span class="sxs-lookup"><span data-stu-id="841e1-291">Add storage</span></span>

<span data-ttu-id="841e1-292">S2D 的磁碟需為空白且不含分割區或其他資料。</span><span class="sxs-lookup"><span data-stu-id="841e1-292">The disks for S2D need to be empty and without partitions or other data.</span></span> <span data-ttu-id="841e1-293">若要清理磁碟，請遵循[本指南內的步驟](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks)。</span><span class="sxs-lookup"><span data-stu-id="841e1-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="841e1-294">[啟用儲存空間直接存取 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct)。</span><span class="sxs-lookup"><span data-stu-id="841e1-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="841e1-295">下列 PowerShell 會啟用儲存空間直接存取。</span><span class="sxs-lookup"><span data-stu-id="841e1-295">The following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="841e1-296">現在，您可以在**容錯移轉管理員**中看到儲存集區。</span><span class="sxs-lookup"><span data-stu-id="841e1-296">In **Failover Cluster Manager**, you can now see the storage pool.</span></span>

1. <span data-ttu-id="841e1-297">[建立磁碟區](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes)。</span><span class="sxs-lookup"><span data-stu-id="841e1-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="841e1-298">S2D 的其中一項功能，是會在您啟用時自動建立儲存集區。</span><span class="sxs-lookup"><span data-stu-id="841e1-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="841e1-299">您現在可以開始建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="841e1-299">You are now ready to create a volume.</span></span> <span data-ttu-id="841e1-300">PowerShell commandlet `New-Volume` 會自動執行磁碟區建立程序，包括格式化、新增至叢集、和建立叢集共用磁碟區 (CSV)。</span><span class="sxs-lookup"><span data-stu-id="841e1-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="841e1-301">下列範列會建立 800 GB 的 CSV。</span><span class="sxs-lookup"><span data-stu-id="841e1-301">The following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="841e1-302">完成此命令後，系統會將 800 GB 的磁碟區掛接為叢集資源。</span><span class="sxs-lookup"><span data-stu-id="841e1-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="841e1-303">磁碟區會位於 `C:\ClusterStorage\Volume1\`。</span><span class="sxs-lookup"><span data-stu-id="841e1-303">The volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="841e1-304">下圖顯示具有 S2D 的叢集共用磁碟區︰</span><span class="sxs-lookup"><span data-stu-id="841e1-304">The following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="841e1-306">步驟 3︰測試容錯移轉叢集的容錯移轉</span><span class="sxs-lookup"><span data-stu-id="841e1-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="841e1-307">在容錯移轉叢集管理員中，請確認您可以將儲存體資源移至其他叢集節點。</span><span class="sxs-lookup"><span data-stu-id="841e1-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span></span> <span data-ttu-id="841e1-308">如果您可以透過**容錯移轉叢集管理員**連接至容錯移轉叢集，並且能將儲存體從一個節點移到另一個，則您可以設定 FCI。</span><span class="sxs-lookup"><span data-stu-id="841e1-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="841e1-309">步驟 4：建立 SDL Server FCI</span><span class="sxs-lookup"><span data-stu-id="841e1-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="841e1-310">設定容錯移轉叢集與所有叢集元件 (包括儲存體) 後，您可以建立 SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="841e1-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span></span>

1. <span data-ttu-id="841e1-311">透過 RDP 連接至第一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-311">Connect to the first virtual machine with RDP.</span></span>

1. <span data-ttu-id="841e1-312">在**容錯移轉叢集管理員**中，請確認所有叢集核心資源皆位於第一部虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="841e1-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span></span> <span data-ttu-id="841e1-313">如有必要，請將所有資源移至此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-313">If necessary, move all resources to this virtual machine.</span></span>

1. <span data-ttu-id="841e1-314">找出安裝媒體。</span><span class="sxs-lookup"><span data-stu-id="841e1-314">Locate the installation media.</span></span> <span data-ttu-id="841e1-315">若虛擬機器是使用其中一個 Azure Marketplace 映像，則媒體會位於 `C:\SQLServer_<version number>_Full`。</span><span class="sxs-lookup"><span data-stu-id="841e1-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="841e1-316">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-316">Click **Setup**.</span></span>

1. <span data-ttu-id="841e1-317">在 [SQL Server 安裝中心] 中，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="841e1-317">In the **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="841e1-318">按一下 [安裝新的 SQL Server 容錯移轉叢集]。</span><span class="sxs-lookup"><span data-stu-id="841e1-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="841e1-319">請遵循精靈內的指示安裝 SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="841e1-319">Follow the instructions in the wizard to install the SQL Server FCI.</span></span>

   <span data-ttu-id="841e1-320">FCI 資料目錄必須位於叢集儲存體中。</span><span class="sxs-lookup"><span data-stu-id="841e1-320">The FCI data directories need to be on clustered storage.</span></span> <span data-ttu-id="841e1-321">與 S2D 搭配使用時，FCI 會做為每個伺服器上的磁碟區掛接點，而非共用磁碟。</span><span class="sxs-lookup"><span data-stu-id="841e1-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span></span> <span data-ttu-id="841e1-322">S2D 會在節點之間同步處理磁碟區。</span><span class="sxs-lookup"><span data-stu-id="841e1-322">S2D synchronizes the volume between both nodes.</span></span> <span data-ttu-id="841e1-323">叢集會將磁碟區當做叢集共用磁碟區使用。</span><span class="sxs-lookup"><span data-stu-id="841e1-323">The volume is presented to the cluster as a cluster shared volume.</span></span> <span data-ttu-id="841e1-324">在資料目錄上使用 CSV 掛接點。</span><span class="sxs-lookup"><span data-stu-id="841e1-324">Use the CSV mount point for the data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="841e1-326">完成精靈中的指示後，安裝程式會在第一個節點上安裝 SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="841e1-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span></span>

1. <span data-ttu-id="841e1-327">安裝程式在第一個節點上成功安裝 FCI 後，請透過 RDP 連接至第二個節點。</span><span class="sxs-lookup"><span data-stu-id="841e1-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span></span>

1. <span data-ttu-id="841e1-328">開啟 [SQL Server 安裝中心]。</span><span class="sxs-lookup"><span data-stu-id="841e1-328">Open the **SQL Server Installation Center**.</span></span> <span data-ttu-id="841e1-329">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="841e1-329">Click **Installation**.</span></span>

1. <span data-ttu-id="841e1-330">按一下 [將節點新增到 SQL Server 容錯移轉叢集]。</span><span class="sxs-lookup"><span data-stu-id="841e1-330">Click **Add node to a SQL Server failover cluster**.</span></span> <span data-ttu-id="841e1-331">請遵循精靈中的指示安裝 SQL Server FCI，並將此伺服器新增至 FCI。</span><span class="sxs-lookup"><span data-stu-id="841e1-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="841e1-332">若您曾透過 SQL Server 使用 Azure Marketplace 資源庫映像，映像會包含 SQL Server 工具。</span><span class="sxs-lookup"><span data-stu-id="841e1-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span></span> <span data-ttu-id="841e1-333">若您沒有用過此映像，請另外安裝 SQL Server 工具。</span><span class="sxs-lookup"><span data-stu-id="841e1-333">If you did not use this image, install the SQL Server tools separately.</span></span> <span data-ttu-id="841e1-334">請參閱[下載 Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="841e1-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="841e1-335">步驟 5：建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="841e1-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="841e1-336">在 Azure 虛擬機器上，叢集會使用負載平衡器來保留每次均需在一個節點上的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span></span> <span data-ttu-id="841e1-337">在此解決方案中，負載平衡器會保留 SQL Server FCI 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span></span>

<span data-ttu-id="841e1-338">[建立並設定 Azure Load Balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="841e1-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="841e1-339">在 Azure 入口網站中建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="841e1-339">Create the load balancer in the Azure portal</span></span>

<span data-ttu-id="841e1-340">若要建立負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="841e1-340">To create the load balancer:</span></span>

1. <span data-ttu-id="841e1-341">在 Azure 入口網站中，請透過虛擬機器移至資源群組。</span><span class="sxs-lookup"><span data-stu-id="841e1-341">In the Azure portal, go to the Resource Group with the virtual machines.</span></span>

1. <span data-ttu-id="841e1-342">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="841e1-342">Click **+ Add**.</span></span> <span data-ttu-id="841e1-343">在 Marketplace 內搜尋 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="841e1-343">Search the Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="841e1-344">按一下 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="841e1-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="841e1-345">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-345">Click **Create**.</span></span>

1. <span data-ttu-id="841e1-346">使用下列項目設定負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="841e1-346">Configure the load balancer with:</span></span>

   - <span data-ttu-id="841e1-347">**名稱**︰用以識別負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-347">**Name**: A name that identifies the load balancer.</span></span>
   - <span data-ttu-id="841e1-348">**類型**︰負載平衡器分為公開或私人兩種類型。</span><span class="sxs-lookup"><span data-stu-id="841e1-348">**Type**: The load balancer can be either public or private.</span></span> <span data-ttu-id="841e1-349">私人負載平衡器可從相同的 VNET 內存取。</span><span class="sxs-lookup"><span data-stu-id="841e1-349">A private load balancer can be accessed from within the same VNET.</span></span> <span data-ttu-id="841e1-350">大部分的 Azure 應用程式都能使用私人負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="841e1-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="841e1-351">若您的應用程式需要直接透過網際網路存取 SQL Server，請使用公開負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="841e1-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="841e1-352">**虛擬網路**︰與虛擬機器相同的網路。</span><span class="sxs-lookup"><span data-stu-id="841e1-352">**Virtual Network**: The same network as the virtual machines.</span></span>
   - <span data-ttu-id="841e1-353">**子網路**︰與虛擬機器相同的子網路。</span><span class="sxs-lookup"><span data-stu-id="841e1-353">**Subnet**: The same subnet as the virtual machines.</span></span>
   - <span data-ttu-id="841e1-354">**私人 IP 位址**︰與您指派至 SQL Server FCI 叢集網路資源相同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="841e1-355">**訂用帳戶**：您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="841e1-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="841e1-356">**資源群組**︰使用與虛擬機器相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="841e1-356">**Resource Group**: Use the same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="841e1-357">**位置**︰使用與虛擬機器相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="841e1-357">**Location**: Use the same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="841e1-358">請參閱下圖︰</span><span class="sxs-lookup"><span data-stu-id="841e1-358">See the following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-the-load-balancer-backend-pool"></a><span data-ttu-id="841e1-360">設定負載平衡器後端集區</span><span class="sxs-lookup"><span data-stu-id="841e1-360">Configure the load balancer backend pool</span></span>

1. <span data-ttu-id="841e1-361">透過虛擬機器返回 Azure 資源群組，並尋找新的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="841e1-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span></span> <span data-ttu-id="841e1-362">您可能需要重新整理資源群組的畫面。</span><span class="sxs-lookup"><span data-stu-id="841e1-362">You may have to refresh the view on the Resource Group.</span></span> <span data-ttu-id="841e1-363">按一下 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="841e1-363">Click the load balancer.</span></span>

1. <span data-ttu-id="841e1-364">在 [負載平衡器] 刀鋒視窗中，按一下 [後端集區]。</span><span class="sxs-lookup"><span data-stu-id="841e1-364">On the load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="841e1-365">按一下 [+ 新增] 以新增後端集區。</span><span class="sxs-lookup"><span data-stu-id="841e1-365">Click **+ Add** to add a backend pool.</span></span>

1. <span data-ttu-id="841e1-366">輸入後端集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-366">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="841e1-367">按一下 [+ 新增虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="841e1-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="841e1-368">在 [選擇虛擬機器] 刀鋒視窗中，按一下 [選擇可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="841e1-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="841e1-369">選擇您放置 SQL Server 虛擬機器的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="841e1-369">Choose the availability set that you placed the SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="841e1-370">在 [選擇虛擬機器] 刀鋒視窗中，按一下 [選擇虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="841e1-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span></span>

   <span data-ttu-id="841e1-371">您的 Azure 入口網站看起來應如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="841e1-371">Your Azure portal should look like the following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="841e1-373">在 [選擇虛擬機器] 刀鋒視窗中，按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="841e1-373">Click **Select** on the **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="841e1-374">按兩次 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="841e1-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="841e1-375">設定負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="841e1-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="841e1-376">在 [負載平衡器] 刀鋒視窗中，按一下 [健全狀況探查]。</span><span class="sxs-lookup"><span data-stu-id="841e1-376">On the load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="841e1-377">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="841e1-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="841e1-378">在 [新增健全狀況探查] 刀鋒視窗中，<a name="probe"></a>設定健全狀況探查參數︰</span><span class="sxs-lookup"><span data-stu-id="841e1-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span></span>

   - <span data-ttu-id="841e1-379">**名稱**：健全狀況探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-379">**Name**: A name for the health probe.</span></span>
   - <span data-ttu-id="841e1-380">**通訊協定**：TCP。</span><span class="sxs-lookup"><span data-stu-id="841e1-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="841e1-381">**連接埠**︰設為可用的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="841e1-381">**Port**: Set to an available TCP port.</span></span> <span data-ttu-id="841e1-382">此連接埠需要開啟防火牆的連接埠。</span><span class="sxs-lookup"><span data-stu-id="841e1-382">This port requires an open firewall port.</span></span> <span data-ttu-id="841e1-383">使用與您在防火牆設定健全狀況探查[相同的連接埠](#ports)。</span><span class="sxs-lookup"><span data-stu-id="841e1-383">Use the [same port](#ports) you set for the health probe at the firewall.</span></span>
   - <span data-ttu-id="841e1-384">**間隔**：5 秒。</span><span class="sxs-lookup"><span data-stu-id="841e1-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="841e1-385">**狀況不良臨界值**：2 次連續失敗。</span><span class="sxs-lookup"><span data-stu-id="841e1-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="841e1-386">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="841e1-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="841e1-387">設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="841e1-387">Set load balancing rules</span></span>

1. <span data-ttu-id="841e1-388">在 [負載平衡器] 刀鋒視窗中，按一下 [負載平衡規則]。</span><span class="sxs-lookup"><span data-stu-id="841e1-388">On the load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="841e1-389">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="841e1-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="841e1-390">設定負載平衡規則參數：</span><span class="sxs-lookup"><span data-stu-id="841e1-390">Set the load balancing rules parameters:</span></span>

   - <span data-ttu-id="841e1-391">**名稱**︰負載平衡規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-391">**Name**: A name for the load balancing rules.</span></span>
   - <span data-ttu-id="841e1-392">**前端 IP 位址**︰使用 SQL Server FCI 叢集網路資源的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="841e1-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="841e1-393">**連接埠**：設定為 SQL Server FCI TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="841e1-393">**Port**: Set for the SQL Server FCI TCP port.</span></span> <span data-ttu-id="841e1-394">預設執行個體連接埠為 1433。</span><span class="sxs-lookup"><span data-stu-id="841e1-394">The default instance port is 1433.</span></span>
   - <span data-ttu-id="841e1-395">**後端連接埠**：此值使用的連接埠與您啟用**浮動 IP (伺服器直接回傳)** 時的**連接埠**值相同。</span><span class="sxs-lookup"><span data-stu-id="841e1-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="841e1-396">**後端集區**︰使用您稍早設定的後端集區名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-396">**Backend pool**: Use the backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="841e1-397">**健全狀況探查**：使用您稍早設定的健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="841e1-397">**Health probe**: Use the health probe that you configured earlier.</span></span>
   - <span data-ttu-id="841e1-398">**工作階段持續性**：無。</span><span class="sxs-lookup"><span data-stu-id="841e1-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="841e1-399">**閒置逾時 (分鐘)**：4。</span><span class="sxs-lookup"><span data-stu-id="841e1-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="841e1-400">**浮動 IP (伺服器直接回傳)**：已啟用。</span><span class="sxs-lookup"><span data-stu-id="841e1-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="841e1-401">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="841e1-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="841e1-402">步驟 6：設定探查叢集</span><span class="sxs-lookup"><span data-stu-id="841e1-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="841e1-403">設定 PowerShell 中的叢集探查連接埠參數。</span><span class="sxs-lookup"><span data-stu-id="841e1-403">Set the cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="841e1-404">若要設定叢集探查連接埠參數，請從您環境的下列指令碼中更新變數。</span><span class="sxs-lookup"><span data-stu-id="841e1-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "IP Address Resource Name" # the IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="841e1-405">步驟 7：測試 FCI 容錯移轉</span><span class="sxs-lookup"><span data-stu-id="841e1-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="841e1-406">測試 FCI 的容錯移轉來驗證叢集功能。</span><span class="sxs-lookup"><span data-stu-id="841e1-406">Test failover of the FCI to validate cluster functionality.</span></span> <span data-ttu-id="841e1-407">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="841e1-407">Do the following steps:</span></span>

1. <span data-ttu-id="841e1-408">透過 RDP 連接至其中一個 SQL Server FCI 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="841e1-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="841e1-409">開啟 [容錯移轉叢集管理員]。</span><span class="sxs-lookup"><span data-stu-id="841e1-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="841e1-410">按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="841e1-410">Click **Roles**.</span></span> <span data-ttu-id="841e1-411">請注意哪個節點擁有 SQL Server FCI 角色。</span><span class="sxs-lookup"><span data-stu-id="841e1-411">Notice which node owns the SQL Server FCI role.</span></span>

1. <span data-ttu-id="841e1-412">以滑鼠右鍵按一下 SQL Server FCI 角色。</span><span class="sxs-lookup"><span data-stu-id="841e1-412">Right-click the SQL Server FCI role.</span></span>

1. <span data-ttu-id="841e1-413">按一下 [移動]，然後按一下 [最佳可行節點]。</span><span class="sxs-lookup"><span data-stu-id="841e1-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="841e1-414">**容錯移轉叢集管理員**會顯示角色，其資源則會變成離線狀態。</span><span class="sxs-lookup"><span data-stu-id="841e1-414">**Failover Cluster Manager** shows the role and its resources go offline.</span></span> <span data-ttu-id="841e1-415">接著資源會移動，並在另一個節點上線。</span><span class="sxs-lookup"><span data-stu-id="841e1-415">The resources then move and come online on the other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="841e1-416">測試連線能力</span><span class="sxs-lookup"><span data-stu-id="841e1-416">Test connectivity</span></span>

<span data-ttu-id="841e1-417">若要測試連線能力，請在相同的虛擬網路內登入至另一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="841e1-417">To test connectivity, log in to another virtual machine in the same virtual network.</span></span> <span data-ttu-id="841e1-418">開啟 [SQL Server Management Studio]，然後連接到 SQL Server FCI 名稱。</span><span class="sxs-lookup"><span data-stu-id="841e1-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="841e1-419">如有需要，您可以[下載 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="841e1-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="841e1-420">限制</span><span class="sxs-lookup"><span data-stu-id="841e1-420">Limitations</span></span>
<span data-ttu-id="841e1-421">在 Azure 虛擬機器中，由於負載平衡器不支援 RPC 連接埠，因此 FCI 不支援 Microsoft Distributed Transaction Coordinator (DTC)。</span><span class="sxs-lookup"><span data-stu-id="841e1-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="841e1-422">另請參閱</span><span class="sxs-lookup"><span data-stu-id="841e1-422">See Also</span></span>

[<span data-ttu-id="841e1-423">透過遠端桌面 (Azure) 設定 S2D</span><span class="sxs-lookup"><span data-stu-id="841e1-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="841e1-424">[具有儲存空間直接存取的超交集解決方案](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)。</span><span class="sxs-lookup"><span data-stu-id="841e1-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="841e1-425">儲存空間直接存取概觀</span><span class="sxs-lookup"><span data-stu-id="841e1-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="841e1-426">適用於 S2D 的 SQL Server 支援</span><span class="sxs-lookup"><span data-stu-id="841e1-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
