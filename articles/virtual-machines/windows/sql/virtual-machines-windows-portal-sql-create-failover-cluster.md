---
title: "aaaSQL Server FCI 的 Azure 虛擬機器 |Microsoft 文件"
description: "這篇文章說明如何 toocreate SQL Server 容錯移轉叢集執行個體的 Azure 虛擬機器上。"
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
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="f3bf4-103">在 Azure 虛擬機器上設定 SQL Server 容錯移轉叢集執行個體</span><span class="sxs-lookup"><span data-stu-id="f3bf4-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="f3bf4-104">這篇文章說明如何 toocreate SQL Server 容錯移轉叢集執行個體 (FCI) 資源管理員模型中的 Azure 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="f3bf4-105">這個解決方案會使用[儲存空間直接存取 Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)以軟體為基礎的虛擬 SAN，同步處理之間 hello 節點 (Azure Vm) 中的 hello 儲存體 （資料磁碟）Windows 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="f3bf4-106">S2D 是 Windows Server 2016 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="f3bf4-107">hello 下圖顯示 hello 完整解決方案 Azure 虛擬機器上：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![可用性群組](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="f3bf4-109">上述圖表會顯示 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="f3bf4-110">兩部位於 Windows 容錯移轉叢集中的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="f3bf4-111">位於容錯移轉叢集中的虛擬機器也稱為「叢集節點」或「節點」。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="f3bf4-112">每部虛擬機器有兩個以上的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="f3bf4-113">S2D hello hello 資料磁碟上的資料同步處理，並顯示 hello 同步處理儲存體與儲存體集區。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="f3bf4-114">hello 存放集區提供叢集共用磁碟區 (CSV) toohello 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="f3bf4-115">hello SQL Server FCI 的叢集角色會使用 hello CSV hello 資料磁碟機。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="f3bf4-116">Azure 負載平衡器 toohold hello IP 位址 hello SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="f3bf4-117">Azure 可用性設定組保存 hello 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f3bf4-118">所有的 Azure 資源都在 hello 圖表 hello 中相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="f3bf4-119">如需有關 S2D 的詳細資料，請參閱 [Windows Server 2016 Datacenter 版本儲存空間直接存取 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="f3bf4-120">S2D 支援兩種類型的架構 - 交集和超交集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="f3bf4-121">本文件中的 hello 架構是超聚合。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="f3bf4-122">上的超聚合式基礎結構上的芳鄰 hello 儲存體 hello 該主機叢集的 hello 應用程式的相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="f3bf4-123">在這種架構，hello 儲存體是每個 SQL Server FCI 節點上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="f3bf4-124">Azure 範本範例</span><span class="sxs-lookup"><span data-stu-id="f3bf4-124">Example Azure template</span></span>

<span data-ttu-id="f3bf4-125">從範本，您可以在 Azure 中建立 hello 整個方案。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="f3bf4-126">範本的範例可用於 hello GitHub [Azure 快速入門範本](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="f3bf4-127">此範例並非為任何特定工作負載而設計或測試。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="f3bf4-128">您可以使用 S2D 儲存體連接的 tooyour 網域執行 hello 範本 toocreate SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="f3bf4-129">您可以評估 hello 範本，並修改您的目的。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f3bf4-130">開始之前</span><span class="sxs-lookup"><span data-stu-id="f3bf4-130">Before you begin</span></span>

<span data-ttu-id="f3bf4-131">有幾件事，您需要 tooknow 和幾個事項您備妥後再繼續。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="f3bf4-132">哪些 tooknow</span><span class="sxs-lookup"><span data-stu-id="f3bf4-132">What tooknow</span></span>
<span data-ttu-id="f3bf4-133">您應該了解 operational hello 下列技術：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="f3bf4-134">Windows 叢集技術</span><span class="sxs-lookup"><span data-stu-id="f3bf4-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="f3bf4-135">[SQL Server 容錯移轉叢集執行個體](http://msdn.microsoft.com/library/ms189134.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="f3bf4-136">此外，您應該有基本認識的 hello 下列技術：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="f3bf4-137">在 Windows Server 2016 中使用儲存空間直接存取的超交集解決方案</span><span class="sxs-lookup"><span data-stu-id="f3bf4-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="f3bf4-138">Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="f3bf4-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="f3bf4-139">哪些 toohave</span><span class="sxs-lookup"><span data-stu-id="f3bf4-139">What toohave</span></span>

<span data-ttu-id="f3bf4-140">這篇文章中的 hello 指示之前，您應該已經有：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="f3bf4-141">Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="f3bf4-142">Azure 虛擬機器上的 Windows 網域。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="f3bf4-143">具有權限 toocreate 物件 hello Azure 虛擬機器中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="f3bf4-144">Azure 虛擬網路和子網路具有足夠的 IP 位址空間，來 hello 下列元件：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="f3bf4-145">兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-145">Both virtual machines.</span></span>
   - <span data-ttu-id="f3bf4-146">hello 容錯移轉叢集 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="f3bf4-147">每個 FCI 上一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="f3bf4-148">Hello Azure 網路，指向 toohello 網域控制站上設定的 DNS。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="f3bf4-149">備妥這些先決條件後，便可繼續建置您的容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="f3bf4-150">hello 第一個步驟是 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="f3bf4-151">步驟 1：建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f3bf4-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="f3bf4-152">登入 toohello [Azure 入口網站](http://portal.azure.com)與您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="f3bf4-153">[建立 Azure 可用性設定組](../tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="f3bf4-154">hello 可用性設定虛擬機器群組橫跨容錯網域和更新網域。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="f3bf4-155">hello 可用性設定組可確保您的應用程式不受到單一失敗點，像是 hello 網路交換器或是伺服器機架的 hello 電源裝置。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="f3bf4-156">如果您尚未建立虛擬機器 hello 資源群組，請在您建立 Azure 可用性設定組時執行動作。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="f3bf4-157">如果您使用 hello Azure 入口網站 toocreate hello 可用性設定組，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="f3bf4-158">在 hello Azure 入口網站，按一下   **+**  tooopen hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="f3bf4-159">搜尋 [可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="f3bf4-160">按一下 [可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="f3bf4-161">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-161">Click **Create**.</span></span>
   - <span data-ttu-id="f3bf4-162">在 hello**建立可用性設定組**刀鋒視窗中，設定下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="f3bf4-163">**名稱**: hello 可用性設定組的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="f3bf4-164">**訂用帳戶**：您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="f3bf4-165">**資源群組**： 如果您想 toouse 現有的群組，請按一下**使用現有**和從 hello 下拉式清單選取 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="f3bf4-166">否則選擇**新建**輸入 hello 群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="f3bf4-167">**位置**： 將您計劃 toocreate hello 位置設定您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="f3bf4-168">**故障網域**： 使用 hello 預設 (3)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="f3bf4-169">**更新網域**： 使用 hello 預設 (5)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="f3bf4-170">按一下**建立**toocreate hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="f3bf4-171">Hello 中建立虛擬機器 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="f3bf4-172">佈建 hello Azure 可用性設定組中的兩個 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="f3bf4-173">如需指示，請參閱[hello Azure 入口網站中的 SQL Server 虛擬機器佈建](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="f3bf4-174">將兩部虛擬機器放置於：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="f3bf4-175">在 hello 您的可用性設定組的相同 Azure 資源群組內。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="f3bf4-176">在 hello 相同網路為您的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="f3bf4-177">有足夠 IP 位址空間存放兩部虛擬機器，與最終會用於此叢集的所有 FCI 的子網路上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="f3bf4-178">在 hello Azure 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="f3bf4-179">建立虛擬機器後，您無法設定或變更可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="f3bf4-180">選擇從 hello Azure Marketplace 的映像。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="f3bf4-181">您可以使用 Marketplace 映像，包括 Windows Server 和 SQL Server 或只是 hello Windows 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="f3bf4-182">如需詳細資料，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f3bf4-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="f3bf4-183">hello 官方 SQL Server 映像 hello Azure 圖庫中的包含已安裝的 SQL Server 執行個體，再加上 hello SQL Server 安裝軟體和 hello 必要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="f3bf4-184">選擇 hello 右側的影像，根據您想要的 toohow toopay hello 的 SQL Server 授權：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="f3bf4-185">**支付每使用量授權**: hello 每分鐘費用這些映像包括 hello SQL Server 授權：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="f3bf4-186">**Windows Server Datacenter 2016 上的 SQL Server 2016 Enterprise 版本**</span><span class="sxs-lookup"><span data-stu-id="f3bf4-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="f3bf4-187">**Windows Server Datacenter 2016 上的 SQL Server 2016 Standard 版本**</span><span class="sxs-lookup"><span data-stu-id="f3bf4-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="f3bf4-188">**Windows Server Datacenter 2016 上的 SQL Server 2016 Developer 版本**</span><span class="sxs-lookup"><span data-stu-id="f3bf4-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="f3bf4-189">**自備授權 (BYOL)**</span><span class="sxs-lookup"><span data-stu-id="f3bf4-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="f3bf4-190">**{BYOL} Windows Server Datacenter 2016 上的 SQL Server 2016 Enterprise 版本**</span><span class="sxs-lookup"><span data-stu-id="f3bf4-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="f3bf4-191">**{BYOL} Windows Server Datacenter 2016 上的 SQL Server 2016 Standard 版本**</span><span class="sxs-lookup"><span data-stu-id="f3bf4-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="f3bf4-192">建立 hello 虛擬機器之後，移除 hello 單獨預先安裝的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="f3bf4-193">設定 hello 容錯移轉叢集和 S2D 之後，您將使用 hello 預先安裝的 SQL Server 媒體 toocreate hello SQL Server FCI。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="f3bf4-194">或者，您可以使用 Azure Marketplace 映像只 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="f3bf4-195">選擇**Windows Server 2016 Datacenter**映像和安裝 SQL Server FCI hello 設定 hello 容錯移轉叢集和 S2D 之後。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="f3bf4-196">此映像不包含 SQL Server 安裝媒體。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="f3bf4-197">將 hello 安裝媒體放在您可以在其中執行 hello SQL Server 安裝的每一部伺服器的位置。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="f3bf4-198">Azure 建立虛擬機器之後，請使用 RDP 連線 tooeach 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="f3bf4-199">當您第一次使用 RDP 連線 tooa 虛擬機器時，hello 電腦詢問您是否 tooallow 此 PC toobe hello 網路上可探索。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="f3bf4-200">按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-200">Click **Yes**.</span></span>

1. <span data-ttu-id="f3bf4-201">如果您使用其中一個 hello SQL Server 為基礎的虛擬機器映像，移除 hello SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="f3bf4-202">在 [程式和功能] 中，以滑鼠右鍵按一下 [Microsoft SQL Server 2016 (64 位元)] 然後按一下 [解除安裝/變更]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="f3bf4-203">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-203">Click **Remove**.</span></span>
   - <span data-ttu-id="f3bf4-204">選取 hello 預設執行個體。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-204">Select hello default instance.</span></span>
   - <span data-ttu-id="f3bf4-205">移除所有在 [Database Engine 服務] 下的功能。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="f3bf4-206">請勿移除 [共用功能]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="f3bf4-207">請參閱下列圖片的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-207">See hello following picture:</span></span>

      ![移除功能](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="f3bf4-209">按一下 下一步，然後按一下移除。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="f3bf4-210"><a name="ports"></a>開啟 hello 防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="f3bf4-211">每個虛擬機器上，開啟下列連接埠上的 Windows 防火牆 hello hello。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="f3bf4-212">目的</span><span class="sxs-lookup"><span data-stu-id="f3bf4-212">Purpose</span></span> | <span data-ttu-id="f3bf4-213">TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="f3bf4-213">TCP Port</span></span> | <span data-ttu-id="f3bf4-214">注意事項</span><span class="sxs-lookup"><span data-stu-id="f3bf4-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="f3bf4-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="f3bf4-215">SQL Server</span></span> | <span data-ttu-id="f3bf4-216">1433</span><span class="sxs-lookup"><span data-stu-id="f3bf4-216">1433</span></span> | <span data-ttu-id="f3bf4-217">適用於 SDL Server 預設執行個體的一般連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="f3bf4-218">如果您使用映像從 hello 組件庫時，會自動開啟此連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="f3bf4-219">健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="f3bf4-219">Health probe</span></span> | <span data-ttu-id="f3bf4-220">59999</span><span class="sxs-lookup"><span data-stu-id="f3bf4-220">59999</span></span> | <span data-ttu-id="f3bf4-221">任何開啟的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-221">Any open TCP port.</span></span> <span data-ttu-id="f3bf4-222">在稍後步驟中，設定 hello 負載平衡器[健全狀況探查](#probe)和 hello 叢集 toouse 此連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="f3bf4-223">新增儲存體 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="f3bf4-224">如需詳細資訊，請參閱[新增儲存區](../../../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="f3bf4-225">每部虛擬機器需要至少兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="f3bf4-226">連接原始磁碟 - 非 NTFS 格式的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="f3bf4-227">若您連接 NTFS 格式的磁碟，您只能啟用 S2D 而無法進行磁碟適用性檢查。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="f3bf4-228">將附加兩個 Premium 儲存體 （SSD 磁碟） tooeach VM 的最小值。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="f3bf4-229">建議使用 P30 (1 TB) 或以上的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="f3bf4-230">設定主機快取太**唯讀**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="f3bf4-231">您在實際執行環境中使用的 hello 儲存容量取決於您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="f3bf4-232">本文中所述的 hello 值是展示和測試。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="f3bf4-233">[新增 hello 虛擬機器 tooyour 預先存在的網域](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="f3bf4-234">Hello 虛擬機器所建立及設定之後，您可以設定 hello 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="f3bf4-235">步驟 2： 設定 S2D hello Windows 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="f3bf4-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="f3bf4-236">hello 下一個步驟是與 S2D tooconfigure hello 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="f3bf4-237">在此步驟中，您要執行 hello 下列子步驟：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="f3bf4-238">新增 Windows 容錯移轉叢集功能</span><span class="sxs-lookup"><span data-stu-id="f3bf4-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="f3bf4-239">驗證 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="f3bf4-239">Validate hello cluster</span></span>
1. <span data-ttu-id="f3bf4-240">建立 hello 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="f3bf4-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="f3bf4-241">建立 hello 雲端見證</span><span class="sxs-lookup"><span data-stu-id="f3bf4-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="f3bf4-242">新增儲存體</span><span class="sxs-lookup"><span data-stu-id="f3bf4-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="f3bf4-243">新增 Windows 容錯移轉叢集功能</span><span class="sxs-lookup"><span data-stu-id="f3bf4-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="f3bf4-244">toobegin，與使用網域帳戶屬於本機系統管理員，且具有權限 toocreate 物件在 Active Directory 中的 RDP 連接 toohello 第一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="f3bf4-245">此帳戶用於 hello 其他 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="f3bf4-246">[將容錯移轉叢集功能 tooeach 虛擬機器加入](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="f3bf4-247">hello tooinstall hello UI 中，從容錯移轉叢集功能，下列步驟在兩部虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="f3bf4-248">在 伺服器管理員 中，按一下 管理，然後按一下新增角色及功能。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="f3bf4-249">在**新增角色及功能精靈**，按一下 **下一步**直到太**選取功能**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="f3bf4-250">在 [選取功能] 中，按一下 [容錯移轉叢集]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="f3bf4-251">包含所有必要的功能和 hello 管理工具。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="f3bf4-252">按一下 [新增功能]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="f3bf4-253">按一下**下一步**，然後按一下**完成**tooinstall hello 功能。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="f3bf4-254">tooinstall hello 容錯移轉叢集功能使用 PowerShell，執行下列其中一個 hello 虛擬機器上從系統管理員 PowerShell 工作階段的指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="f3bf4-255">供參考，hello 接下來的步驟會遵循底下的步驟 3 的 hello 指示[使用儲存空間直接存取 Windows Server 2016 中的超聚合式方案](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="f3bf4-256">驗證 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="f3bf4-256">Validate hello cluster</span></span>

<span data-ttu-id="f3bf4-257">本指南是指在 tooinstructions[驗證叢集](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="f3bf4-258">驗證 hello 叢集在 hello UI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="f3bf4-259">toovalidate hello 叢集以 hello UI，請勿 hello 其中 hello 虛擬機器中的下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="f3bf4-260">在 [伺服器管理員] 中，按一下 [工具]，然後按一下 [容錯移轉叢集管理員]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="f3bf4-261">在 [容錯移轉叢集管理員] 中，按一下 [動作]，然後按一下 [驗證設定...]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="f3bf4-262">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-262">Click **Next**.</span></span>
1. <span data-ttu-id="f3bf4-263">在**選取伺服器或叢集**，型別 hello 兩部虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="f3bf4-264">在 [測試選項] 中，選擇 [僅執行我選取的測試]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="f3bf4-265">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-265">Click **Next**.</span></span>
1. <span data-ttu-id="f3bf4-266">在 [測試選取範圍] 中，選取**儲存體**以外的所有測試。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="f3bf4-267">請參閱下列圖片的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-267">See hello following picture:</span></span>

   ![驗證測試](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="f3bf4-269">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-269">Click **Next**.</span></span>
1. <span data-ttu-id="f3bf4-270">在 [確認] 中，，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="f3bf4-271">hello**驗證設定精靈**執行 hello 驗證測試。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="f3bf4-272">使用 PowerShell，執行下列其中一個 hello 虛擬機器上從系統管理員 PowerShell 工作階段的指令碼的 hello toovalidate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="f3bf4-273">驗證 hello 叢集後，請建立 hello 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="f3bf4-274">建立 hello 容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="f3bf4-274">Create hello failover cluster</span></span>

<span data-ttu-id="f3bf4-275">本指南是指太[建立 hello 容錯移轉叢集](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="f3bf4-276">toocreate hello 容錯移轉叢集，您必須：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="f3bf4-277">hello hello 變成 hello 叢集節點的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="f3bf4-278">Hello 容錯移轉叢集的名稱</span><span class="sxs-lookup"><span data-stu-id="f3bf4-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="f3bf4-279">Hello 容錯移轉叢集的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="f3bf4-280">您可以使用 hello 未使用的 IP 位址相同 Azure 虛擬網路和子網路為 hello 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="f3bf4-281">hello 遵循 PowerShell 建立容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="f3bf4-282">更新 hello hello 名稱 hello 節點 （hello 虛擬機器名稱） 的指令碼和 hello Azure VNET 中可用的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="f3bf4-283">建立雲端見證</span><span class="sxs-lookup"><span data-stu-id="f3bf4-283">Create a cloud witness</span></span>

<span data-ttu-id="f3bf4-284">雲端見證儲存在 Azure 儲存體 Blob 中，是一種新型的叢集仲裁見證。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="f3bf4-285">這會移除 hello 需要個別的虛擬機器裝載見證共用。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="f3bf4-286">[建立雲端 hello 容錯移轉叢集的見證](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="f3bf4-287">建立 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-287">Create a blob container.</span></span>

1. <span data-ttu-id="f3bf4-288">儲存 hello 存取金鑰，然後 hello 容器 URL。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="f3bf4-289">設定 hello 容錯移轉叢集的叢集仲裁見證。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="f3bf4-290">請參閱，[設定 hello 仲裁見證 hello 使用者介面中的]。(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) hello UI 中。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="f3bf4-291">新增儲存體</span><span class="sxs-lookup"><span data-stu-id="f3bf4-291">Add storage</span></span>

<span data-ttu-id="f3bf4-292">S2D hello 磁碟需要 toobe 空白，且不含資料分割或其他資料。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="f3bf4-293">請依照下列 tooclean 磁碟[本指南中步驟的 hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="f3bf4-294">[啟用儲存空間直接存取 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="f3bf4-295">下列 PowerShell hello 可讓儲存空間 direct。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="f3bf4-296">在**容錯移轉叢集管理員**，您現在可以看到 hello 存放集區。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="f3bf4-297">[建立磁碟區](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="f3bf4-298">S2D hello 功能之一是它會自動建立儲存集區，當您啟用它。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="f3bf4-299">現在您已經準備就緒 toocreate 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="f3bf4-300">hello PowerShell commandlet`New-Volume`自動化 hello 磁碟區建立程序，包括格式、 新增 toohello 叢集和建立叢集共用磁碟區 (CSV)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="f3bf4-301">下列範例中的 hello 建立 800 gb CSV。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="f3bf4-302">完成此命令後，系統會將 800 GB 的磁碟區掛接為叢集資源。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="f3bf4-303">hello 磁碟區位於`C:\ClusterStorage\Volume1\`。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="f3bf4-304">hello 下列圖表顯示 S2D 的叢集共用磁碟區：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="f3bf4-306">步驟 3︰測試容錯移轉叢集的容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f3bf4-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="f3bf4-307">在 [容錯移轉叢集管理員] 中，確認您可以移動 hello 儲存體資源 toohello 其他叢集節點。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="f3bf4-308">如果您可以連接 toohello 容錯移轉叢集與**容錯移轉叢集管理員**並且從一個節點 toohello 其他移動 hello 存放裝置，您就準備好 tooconfigure hello FCI。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="f3bf4-309">步驟 4：建立 SDL Server FCI</span><span class="sxs-lookup"><span data-stu-id="f3bf4-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="f3bf4-310">設定 hello 容錯移轉叢集與所有叢集元件包括儲存體之後，您可以建立 SQL Server FCI hello。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="f3bf4-311">使用 RDP 連線 toohello 第一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="f3bf4-312">在**容錯移轉叢集管理員**，請確定所有叢集核心資源在 hello 第一部虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="f3bf4-313">如果有必要，請移動所有資源 toothis 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="f3bf4-314">找出 hello 安裝媒體。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-314">Locate hello installation media.</span></span> <span data-ttu-id="f3bf4-315">如果 hello 虛擬機器可使用其中一個 hello Azure Marketplace 映像，是位於 hello 媒體`C:\SQLServer_<version number>_Full`。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="f3bf4-316">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-316">Click **Setup**.</span></span>

1. <span data-ttu-id="f3bf4-317">在 hello **SQL Server 安裝中心**，按一下 **安裝**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="f3bf4-318">按一下 [安裝新的 SQL Server 容錯移轉叢集]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="f3bf4-319">請遵循 hello hello 精靈 tooinstall hello SQL Server FCI 中的指示。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="f3bf4-320">hello FCI 資料目錄需要 toobe 叢集存放裝置上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="f3bf4-321">S2D，它不共用的磁碟，而每個伺服器上的掛接點 tooa 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="f3bf4-322">S2D 同步處理兩個節點之間的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="f3bf4-323">hello 磁碟區會顯示 toohello 叢集與叢集共用磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="f3bf4-324">用於 hello 資料目錄中的 hello CSV 掛接點。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="f3bf4-326">Hello 精靈完成之後，安裝程式會安裝 SQL Server FCI hello 第一個節點上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="f3bf4-327">安裝程式已成功安裝 hello FCI hello 第一個節點上之後，請使用 RDP 連線 toohello 第二個節點。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="f3bf4-328">開啟 hello **SQL Server 安裝中心**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="f3bf4-329">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-329">Click **Installation**.</span></span>

1. <span data-ttu-id="f3bf4-330">按一下**新增節點 tooa SQL Server 容錯移轉叢集**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="f3bf4-331">遵循 hello hello 精靈 tooinstall SQL server 中的指示，並將此伺服器 toohello FCI。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f3bf4-332">如果您使用 Azure Marketplace 的資源庫映像與 SQL Server，SQL Server 工具已隨附 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="f3bf4-333">如果您未使用此映像，請個別安裝 hello SQL Server 工具。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="f3bf4-334">請參閱[下載 Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="f3bf4-335">步驟 5：建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="f3bf4-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="f3bf4-336">Azure 虛擬機器，在叢集上使用負載平衡器 toohold 一次需要 toobe 一個叢集節點上的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="f3bf4-337">在此解決方案中，hello 負載平衡器會保存 hello hello SQL Server FCI 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="f3bf4-338">[建立並設定 Azure Load Balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="f3bf4-339">在 hello Azure 入口網站中建立 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="f3bf4-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="f3bf4-340">toocreate hello 負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="f3bf4-341">在 hello Azure 入口網站，移 toohello 資源群組與 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="f3bf4-342">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-342">Click **+ Add**.</span></span> <span data-ttu-id="f3bf4-343">搜尋 hello Marketplace 的**負載平衡器**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="f3bf4-344">按一下 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="f3bf4-345">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-345">Click **Create**.</span></span>

1. <span data-ttu-id="f3bf4-346">設定具有 hello 負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="f3bf4-347">**名稱**： 可識別 hello 負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="f3bf4-348">**型別**: hello 負載平衡器可以是公用或私用。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="f3bf4-349">私用的負載平衡器可從 hello 相同的 VNET。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="f3bf4-350">大部分的 Azure 應用程式都能使用私人負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="f3bf4-351">如果您的應用程式需要存取 tooSQL 伺服器直接透過網際網路 hello，請使用公用負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="f3bf4-352">**虛擬網路**: hello 做為 hello 虛擬機器相同網路。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="f3bf4-353">**子網路**: hello hello 虛擬機器相同的子網路。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="f3bf4-354">**私用 IP 位址**: hello 相同的 IP 位址指派給 toohello SQL Server FCI 的叢集網路資源。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="f3bf4-355">**訂用帳戶**：您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="f3bf4-356">**資源群組**： 使用 hello 相同資源群組，做為虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="f3bf4-357">**位置**： 使用 hello 相同做為虛擬機器的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="f3bf4-358">請參閱下列圖片的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="f3bf4-360">Hello 負載平衡器後端集區設定</span><span class="sxs-lookup"><span data-stu-id="f3bf4-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="f3bf4-361">傳回與 hello 虛擬機器 toohello Azure 資源群組，並找出 hello 新增負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="f3bf4-362">您可能必須 toorefresh hello 檢視 hello 資源群組上。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="f3bf4-363">按一下 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="f3bf4-364">在 hello 負載平衡器刀鋒視窗中，按一下 **後端集區**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="f3bf4-365">按一下**+ 加**tooadd 後端集區。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="f3bf4-366">輸入 hello 後端集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="f3bf4-367">按一下 [+ 新增虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="f3bf4-368">在 hello**選擇虛擬機器**刀鋒視窗中，按一下 **選擇可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="f3bf4-369">選擇 hello 可用性設定組放置於 hello SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="f3bf4-370">在 hello**選擇虛擬機器**刀鋒視窗中，按一下 **選擇 hello 虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="f3bf4-371">在 Azure 入口網站看起來應該類似下列圖片的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="f3bf4-373">按一下**選取**上 hello**選擇虛擬機器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="f3bf4-374">按兩次 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="f3bf4-375">設定負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="f3bf4-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="f3bf4-376">在 hello 負載平衡器刀鋒視窗中，按一下 **健全狀況探查**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="f3bf4-377">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="f3bf4-378">在 hello**新增健全狀況探查**刀鋒視窗中， <a name="probe"></a>設定 hello 健全狀況探查參數：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="f3bf4-379">**名稱**: hello 健全狀況探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="f3bf4-380">**通訊協定**：TCP。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="f3bf4-381">**連接埠**： 設定 tooan 可用的 TCP 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="f3bf4-382">此連接埠需要開啟防火牆的連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-382">This port requires an open firewall port.</span></span> <span data-ttu-id="f3bf4-383">使用 hello[相同的連接埠](#ports)您在 hello 防火牆設定 hello 健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="f3bf4-384">**間隔**：5 秒。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="f3bf4-385">**狀況不良臨界值**：2 次連續失敗。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="f3bf4-386">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="f3bf4-387">設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="f3bf4-387">Set load balancing rules</span></span>

1. <span data-ttu-id="f3bf4-388">在 hello 負載平衡器刀鋒視窗中，按一下 **負載平衡規則**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="f3bf4-389">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="f3bf4-390">設定 hello 負載平衡規則參數：</span><span class="sxs-lookup"><span data-stu-id="f3bf4-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="f3bf4-391">**名稱**: hello 負載平衡規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="f3bf4-392">**前端 IP 位址**: hello IP 位址用於 hello SQL Server FCI 的叢集網路資源。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="f3bf4-393">**連接埠**: hello SQL Server FCI TCP 通訊埠設定。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="f3bf4-394">hello 預設執行個體的連接埠為 1433年。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="f3bf4-395">**後端連接埠**： 這個值一律使用相同連接埠的 hello 與 hello**連接埠**值，當您啟用**浮動 IP （伺服器直接回傳）**。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="f3bf4-396">**後端集區**： 使用 hello 後端集區名稱，您先前設定。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="f3bf4-397">**健全狀況探查**： 您先前設定的使用 hello 健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="f3bf4-398">**工作階段持續性**：無。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="f3bf4-399">**閒置逾時 (分鐘)**：4。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="f3bf4-400">**浮動 IP (伺服器直接回傳)**：已啟用。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="f3bf4-401">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="f3bf4-402">步驟 6：設定探查叢集</span><span class="sxs-lookup"><span data-stu-id="f3bf4-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="f3bf4-403">在 PowerShell 中設定 hello 叢集探查連接埠參數。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="f3bf4-404">tooset hello 叢集探查連接埠參數，請更新您的環境中的下列指令碼的 hello 中的變數。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="f3bf4-405">步驟 7：測試 FCI 容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f3bf4-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="f3bf4-406">測試容錯移轉的 hello FCI toovalidate 叢集功能。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="f3bf4-407">下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="f3bf4-407">Do hello following steps:</span></span>

1. <span data-ttu-id="f3bf4-408">使用 RDP 連線 tooone hello SQL Server FCI 的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="f3bf4-409">開啟 [容錯移轉叢集管理員]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="f3bf4-410">按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-410">Click **Roles**.</span></span> <span data-ttu-id="f3bf4-411">請注意哪個節點擁有 hello SQL Server FCI 角色中。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="f3bf4-412">以滑鼠右鍵按一下 hello SQL Server FCI 角色。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="f3bf4-413">按一下 [移動]，然後按一下 [最佳可行節點]。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="f3bf4-414">**容錯移轉叢集管理員**顯示 hello 角色和其資源變成離線狀態。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="f3bf4-415">hello 資源移動，然後上線在 hello 另一個節點。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="f3bf4-416">測試連線能力</span><span class="sxs-lookup"><span data-stu-id="f3bf4-416">Test connectivity</span></span>

<span data-ttu-id="f3bf4-417">tootest 連線，hello tooanother 虛擬機器中的記錄檔相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="f3bf4-418">開啟**SQL Server Management Studio**並連接 toohello SQL Server FCI 的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="f3bf4-419">如有需要，您可以[下載 SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="f3bf4-420">限制</span><span class="sxs-lookup"><span data-stu-id="f3bf4-420">Limitations</span></span>
<span data-ttu-id="f3bf4-421">Azure 虛擬機器，在 Microsoft Distributed Transaction Coordinator (DTC) 不支援在 Fci 上因為 hello 負載平衡器不支援 hello RPC 連接埠。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="f3bf4-422">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f3bf4-422">See Also</span></span>

[<span data-ttu-id="f3bf4-423">透過遠端桌面 (Azure) 設定 S2D</span><span class="sxs-lookup"><span data-stu-id="f3bf4-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="f3bf4-424">[具有儲存空間直接存取的超交集解決方案](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)。</span><span class="sxs-lookup"><span data-stu-id="f3bf4-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="f3bf4-425">儲存空間直接存取概觀</span><span class="sxs-lookup"><span data-stu-id="f3bf4-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="f3bf4-426">適用於 S2D 的 SQL Server 支援</span><span class="sxs-lookup"><span data-stu-id="f3bf4-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
