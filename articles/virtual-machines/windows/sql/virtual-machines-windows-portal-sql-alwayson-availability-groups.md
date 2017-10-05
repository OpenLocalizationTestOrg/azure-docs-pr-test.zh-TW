---
title: "設定 Azure Resource Manager VM 的高可用性 | Microsoft Docs"
description: "本教學課程將說明如何使用 Azure Resource Manager 模式下的 Azure 虛擬機器來建立 Always On 可用性群組。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d430febee23081b26eee0a68d4beb43228549f52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a><span data-ttu-id="92666-103">在 Azure 虛擬機器中自動設定 Always On 可用性群組：Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92666-103">Configure Always On availability groups in Azure Virtual Machines automatically: Resource Manager</span></span>

<span data-ttu-id="92666-104">本教學課程示範如何使用 Azure Resource Manager 虛擬機器來建立 SQL Server 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="92666-104">This tutorial shows you how to create a SQL Server availability group that uses Azure Resource Manager virtual machines.</span></span> <span data-ttu-id="92666-105">本教學課程使用 Azure 刀鋒視窗來設定範本。</span><span class="sxs-lookup"><span data-stu-id="92666-105">The tutorial uses Azure blades to configure a template.</span></span> <span data-ttu-id="92666-106">逐步執行本教學課程時，您可以在入口網站中檢閱預設設定、輸入必要的設定，以及更新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="92666-106">You can review the default settings, type required settings, and update the blades in the portal as you walk through this tutorial.</span></span>

<span data-ttu-id="92666-107">完成本教學課程，即會在 Azure 虛擬機器上建立 SQL Server 可用性群組，包括下列項目：</span><span class="sxs-lookup"><span data-stu-id="92666-107">The complete tutorial creates a SQL Server availability group on Azure Virtual Machines that include the following elements:</span></span>

* <span data-ttu-id="92666-108">包含多個子網路 (前端和後端子網路) 的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="92666-108">A virtual network that has multiple subnets, including a frontend and a backend subnet</span></span>
* <span data-ttu-id="92666-109">具有 Active Directory 網域的兩個網域控制站</span><span class="sxs-lookup"><span data-stu-id="92666-109">Two domain controllers that have an Active Directory domain</span></span>
* <span data-ttu-id="92666-110">執行 SQL Server VM 的兩部虛擬機器已部署至後端子網路並加入 Active Directory 網域</span><span class="sxs-lookup"><span data-stu-id="92666-110">Two virtual machines that run SQL Server and are deployed to the backend subnet and joined to the Active Directory domain</span></span>
* <span data-ttu-id="92666-111">具有節點多數仲裁模型的 3 節點容錯移轉叢集</span><span class="sxs-lookup"><span data-stu-id="92666-111">A three-node failover cluster with the Node Majority quorum model</span></span>
* <span data-ttu-id="92666-112">具有兩份可用性資料庫同步認可複本的可用性群組</span><span class="sxs-lookup"><span data-stu-id="92666-112">An availability group that has two synchronous-commit replicas of an availability database</span></span>

<span data-ttu-id="92666-113">下圖呈現完整的解決方案。</span><span class="sxs-lookup"><span data-stu-id="92666-113">The following illustration represents the complete solution.</span></span>

![Azure 中可用性群組的測試實驗室架構](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

<span data-ttu-id="92666-115">此解決方案中的資源全都屬於單一資源群組。</span><span class="sxs-lookup"><span data-stu-id="92666-115">All resources in this solution belong to a single resource group.</span></span>

<span data-ttu-id="92666-116">在開始本教學課程之前，請確認下列項目︰</span><span class="sxs-lookup"><span data-stu-id="92666-116">Before you start this tutorial, confirm the following:</span></span>

* <span data-ttu-id="92666-117">您已經有 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="92666-117">You already have an Azure account.</span></span> <span data-ttu-id="92666-118">如果您沒有帳戶，請 [註冊一個試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="92666-118">If you don't have one, [sign up for a trial account](http://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="92666-119">您已經知道如何使用 GUI 佈建來自虛擬機器資源庫的 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="92666-119">You already know how to use the GUI to provision a SQL Server virtual machine from the virtual machine gallery.</span></span> <span data-ttu-id="92666-120">如需詳細資訊，請參閱[在 Azure 上佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="92666-120">For more information, see [Provisioning a SQL Server virtual machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>
* <span data-ttu-id="92666-121">您已非常熟悉可用性群組的功能。</span><span class="sxs-lookup"><span data-stu-id="92666-121">You already have a solid understanding of availability groups.</span></span> <span data-ttu-id="92666-122">如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)。</span><span class="sxs-lookup"><span data-stu-id="92666-122">For more information, see [Always On availability groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="92666-123">如果您對搭配 SharePoint 使用可用性群組感興趣，另請參閱 [為 SharePoint 2013 設定 SQL Server 2012 Always On 可用性群組](http://technet.microsoft.com/library/jj715261.aspx)。</span><span class="sxs-lookup"><span data-stu-id="92666-123">If you are interested in using availability groups with SharePoint, also see [Configure SQL Server 2012 Always On availability groups for SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx).</span></span>
>
>

<span data-ttu-id="92666-124">在本教學課程中，使用 Azure 入口網站執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="92666-124">In this tutorial, use the Azure portal to:</span></span>

* <span data-ttu-id="92666-125">從入口網站選擇 Always On 範本。</span><span class="sxs-lookup"><span data-stu-id="92666-125">Choose the Always On template from the portal.</span></span>
* <span data-ttu-id="92666-126">檢閱範本設定，並針對您的環境更新一些組態設定。</span><span class="sxs-lookup"><span data-stu-id="92666-126">Review the template settings and update a few configuration settings for your environment.</span></span>
* <span data-ttu-id="92666-127">監視 Azure 建立整個環境的情形。</span><span class="sxs-lookup"><span data-stu-id="92666-127">Monitor Azure as it creates the entire environment.</span></span>
* <span data-ttu-id="92666-128">連線到網域控制站，然後連線到執行 SQL Server 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="92666-128">Connect to a domain controller and then to a server that runs SQL Server.</span></span>

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-the-cluster-from-the-gallery"></a><span data-ttu-id="92666-129">從資源庫佈建叢集</span><span class="sxs-lookup"><span data-stu-id="92666-129">Provision the cluster from the gallery</span></span>
<span data-ttu-id="92666-130">Azure 提供整個解決方案的資源庫映像。</span><span class="sxs-lookup"><span data-stu-id="92666-130">Azure provides a gallery image for the entire solution.</span></span> <span data-ttu-id="92666-131">若要找出範本，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="92666-131">To locate the template:</span></span>

1. <span data-ttu-id="92666-132">使用您的帳戶登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="92666-132">Sign in to the Azure portal by using your account.</span></span>
2. <span data-ttu-id="92666-133">在 Azure 入口網站中，按一下 [+新增] 以開啟 [新增] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="92666-133">In the Azure portal, click **+New** to open the **New** blade.</span></span>
3. <span data-ttu-id="92666-134">在 [新增] 刀鋒視窗上，搜尋 **AlwaysOn**。</span><span class="sxs-lookup"><span data-stu-id="92666-134">On the **New** blade, search for **AlwaysOn**.</span></span>
   <span data-ttu-id="92666-135">![尋找 AlwaysOn 範本](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)</span><span class="sxs-lookup"><span data-stu-id="92666-135">![Find AlwaysOn Template](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)</span></span>
4. <span data-ttu-id="92666-136">在搜尋結果中，找出「SQL Server AlwaysOn 叢集」。</span><span class="sxs-lookup"><span data-stu-id="92666-136">In the search results, locate **SQL Server AlwaysOn Cluster**.</span></span>
   <span data-ttu-id="92666-137">![AlwaysOn 範本](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)</span><span class="sxs-lookup"><span data-stu-id="92666-137">![AlwaysOn Template](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)</span></span>
5. <span data-ttu-id="92666-138">在 [選取部署模型] 中，選擇 [Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="92666-138">On **Select a deployment model**, choose **Resource Manager**.</span></span>

### <a name="basics"></a><span data-ttu-id="92666-139">基本概念</span><span class="sxs-lookup"><span data-stu-id="92666-139">Basics</span></span>
<span data-ttu-id="92666-140">按一下 [基本] 並設定下列設定：</span><span class="sxs-lookup"><span data-stu-id="92666-140">Click **Basics** and configure the following settings:</span></span>

* <span data-ttu-id="92666-141">[系統管理員使用者名稱] 是具有網域系統管理員權限，且在兩個 SQL Server 執行個體上皆具備 SQL Server sysadmin 固定伺服器角色成員身分的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="92666-141">**Administrator user name** is a user account that has domain administrator permissions and is a member of the SQL Server sysadmin fixed server role on both instances of SQL Server.</span></span> <span data-ttu-id="92666-142">本教學課程使用 **DomainAdmin**。</span><span class="sxs-lookup"><span data-stu-id="92666-142">For this tutorial, use **DomainAdmin**.</span></span>
* <span data-ttu-id="92666-143"> 是網域系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="92666-143">**Password** is the password for the domain administrator account.</span></span> <span data-ttu-id="92666-144">使用複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="92666-144">Use a complex password.</span></span> <span data-ttu-id="92666-145">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="92666-145">Confirm the password.</span></span>
* <span data-ttu-id="92666-146">[訂用帳戶] 是在執行針對可用性群組部署的所有資源時，Azure 將收費的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="92666-146">**Subscription** is the subscription that Azure bills to run all deployed resources for the availability group.</span></span> <span data-ttu-id="92666-147">如果您的帳戶有多個訂用帳戶，您可以指定不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="92666-147">If your account has multiple subscriptions, you can specify a different subscription.</span></span>
* <span data-ttu-id="92666-148">[資源群組] 是此範本建立之所有 Azure 資源所屬群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-148">**Resource group** is the name for the group to which all Azure resources that are created by this template belong.</span></span> <span data-ttu-id="92666-149">本教學課程使用 **SQL-HA-RG**。</span><span class="sxs-lookup"><span data-stu-id="92666-149">For this tutorial, use **SQL-HA-RG**.</span></span> <span data-ttu-id="92666-150">如需詳細資訊，請參閱 [Azure Resource Manager 概觀](../../../azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="92666-150">For more information, see [Azure Resource Manager overview](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
* <span data-ttu-id="92666-151">[位置] 是本教學課程要在其中建立資源的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="92666-151">**Location** is the Azure region where the tutorial creates the resources.</span></span> <span data-ttu-id="92666-152">選擇 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="92666-152">Choose an Azure region.</span></span>

<span data-ttu-id="92666-153">以下螢幕擷取畫面是已完成的 [基本] 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="92666-153">The following screenshot is a completed **Basics** blade:</span></span>

![基本概念](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

<span data-ttu-id="92666-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="92666-155">Click **OK**.</span></span>

### <a name="domain-and-network-settings"></a><span data-ttu-id="92666-156">網域和網路設定</span><span class="sxs-lookup"><span data-stu-id="92666-156">Domain and network settings</span></span>
<span data-ttu-id="92666-157">此 Azure 資源庫範本會建立網域與網域控制站。</span><span class="sxs-lookup"><span data-stu-id="92666-157">This Azure gallery template creates a domain and domain controllers.</span></span> <span data-ttu-id="92666-158">它也會建立一個網路和兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="92666-158">It also creates a network and two subnets.</span></span> <span data-ttu-id="92666-159">此範本無法在現有的網域或虛擬網路中建立伺服器。</span><span class="sxs-lookup"><span data-stu-id="92666-159">The template cannot create servers in an existing domain or virtual network.</span></span> <span data-ttu-id="92666-160">下一步是設定網域和網路設定。</span><span class="sxs-lookup"><span data-stu-id="92666-160">The next step configures the domain and network settings.</span></span>

<span data-ttu-id="92666-161">在 [網域和網路設定] 刀鋒視窗上，檢閱網域和網路設定的預設值：</span><span class="sxs-lookup"><span data-stu-id="92666-161">On the **Domain and network settings** blade, review the preset values for the domain and network settings:</span></span>

* <span data-ttu-id="92666-162">[樹系根網域名稱] 是用於要裝載叢集之 Active Directory 網域的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-162">**Forest root domain name** is the domain name for the Active Directory domain that hosts the cluster.</span></span> <span data-ttu-id="92666-163">本教學課程使用 **contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="92666-163">For the tutorial, use **contoso.com**.</span></span>
* <span data-ttu-id="92666-164">[虛擬網路名稱] 是 Azure 虛擬網路的網路名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-164">**Virtual Network name** is the network name for the Azure virtual network.</span></span> <span data-ttu-id="92666-165">本教學課程使用 **autohaVNET**。</span><span class="sxs-lookup"><span data-stu-id="92666-165">For the tutorial, use **autohaVNET**.</span></span>
* <span data-ttu-id="92666-166">[網域控制站子網路名稱] 是裝載網域控制站之虛擬網路中某個部分的名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-166">**Domain Controller subnet name** is the name of a portion of the virtual network that hosts the domain controller.</span></span> <span data-ttu-id="92666-167">請使用 **subnet-1**。</span><span class="sxs-lookup"><span data-stu-id="92666-167">Use **subnet-1**.</span></span> <span data-ttu-id="92666-168">這個子網路會使用位址首碼 **10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="92666-168">This subnet uses address prefix **10.0.0.0/24**.</span></span>
* <span data-ttu-id="92666-169">[SQL Server 子網路名稱] 是裝載伺服器 (執行 SQL Server) 和檔案共用見證之虛擬網路中某個部分的名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-169">**SQL Server subnet name** is the name of a portion of the virtual network that hosts the servers that run SQL Server and the file share witness.</span></span> <span data-ttu-id="92666-170">請使用 **subnet-2**。</span><span class="sxs-lookup"><span data-stu-id="92666-170">Use **subnet-2**.</span></span> <span data-ttu-id="92666-171">這個子網路會使用位址首碼 **10.0.1.0/26**。</span><span class="sxs-lookup"><span data-stu-id="92666-171">This subnet uses address prefix **10.0.1.0/26**.</span></span>

<span data-ttu-id="92666-172">若要深入了解 Azure 中的虛擬網路，請參閱[虛擬網路概觀](../../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92666-172">To learn more about virtual networks in Azure, see [Virtual network overview](../../../virtual-network/virtual-networks-overview.md).</span></span>  

<span data-ttu-id="92666-173">**網域和網路設定**看起來應該類似以下螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="92666-173">The **Domain and network settings** should look like the following screenshot:</span></span>

![網域和網路設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

<span data-ttu-id="92666-175">如有必要，您可以變更這些值。</span><span class="sxs-lookup"><span data-stu-id="92666-175">If necessary, you can change these values.</span></span> <span data-ttu-id="92666-176">本教學課程使用預設值。</span><span class="sxs-lookup"><span data-stu-id="92666-176">For this tutorial, use the preset values.</span></span>

<span data-ttu-id="92666-177">檢閱設定，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="92666-177">Review the settings, and then click **OK**.</span></span>

### <a name="availability-group-settings"></a><span data-ttu-id="92666-178">可用性群組設定</span><span class="sxs-lookup"><span data-stu-id="92666-178">Availability group settings</span></span>
<span data-ttu-id="92666-179">在 [可用性群組設定] 上，檢閱可用性群組和接聽程式的預設值。</span><span class="sxs-lookup"><span data-stu-id="92666-179">On **Availability group settings**, review the preset values for the availability group and the listener.</span></span>

* <span data-ttu-id="92666-180">[可用性群組名稱] 是可用性群組的叢集資源名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-180">**Availability group name** is the clustered resource name for the availability group.</span></span> <span data-ttu-id="92666-181">本教學課程使用 **Contoso-ag**。</span><span class="sxs-lookup"><span data-stu-id="92666-181">For this tutorial, use **Contoso-ag**.</span></span>
* <span data-ttu-id="92666-182">[可用性群組接聽程式名稱] 是供叢集和內部負載平衡器使用。</span><span class="sxs-lookup"><span data-stu-id="92666-182">**Availability group listener name** is used by the cluster and the internal load balancer.</span></span> <span data-ttu-id="92666-183">連線到 SQL Server 的用戶端可以使用這個名稱來連線到資料庫的適當複本。</span><span class="sxs-lookup"><span data-stu-id="92666-183">Clients that connect to SQL Server can use this name to connect to the appropriate replica of the database.</span></span> <span data-ttu-id="92666-184">本教學課程使用 **Contoso-listener**。</span><span class="sxs-lookup"><span data-stu-id="92666-184">For this tutorial, use **Contoso-listener**.</span></span>
* <span data-ttu-id="92666-185">**可用性群組接聽程式連接埠**會指定 SQL Server 接聽程式的 TCP 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="92666-185">**Availability group listener port** specifies the TCP port of the SQL Server listener.</span></span> <span data-ttu-id="92666-186">本教學課程使用預設連接埠 **1433**。</span><span class="sxs-lookup"><span data-stu-id="92666-186">For this tutorial, use the default port, **1433**.</span></span>

<span data-ttu-id="92666-187">如有必要，您可以變更這些值。</span><span class="sxs-lookup"><span data-stu-id="92666-187">If necessary, you can change these values.</span></span> <span data-ttu-id="92666-188">本教學課程使用預設值。</span><span class="sxs-lookup"><span data-stu-id="92666-188">For this tutorial, use the preset values.</span></span>  

![可用性群組設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

<span data-ttu-id="92666-190">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="92666-190">Click **OK**.</span></span>

### <a name="virtual-machine-size-storage-settings"></a><span data-ttu-id="92666-191">虛擬機器大小，儲存體設定</span><span class="sxs-lookup"><span data-stu-id="92666-191">Virtual machine size, storage settings</span></span>
<span data-ttu-id="92666-192">在 [VM 大小，儲存體設定] 上，選擇 SQL Server 虛擬機器大小，並檢閱其他設定。</span><span class="sxs-lookup"><span data-stu-id="92666-192">On **VM size, storage settings**, choose a SQL Server virtual machine size, and review the other settings.</span></span>

* <span data-ttu-id="92666-193">**SQL Server 虛擬機器大小**是執行 SQL Server 之兩個虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="92666-193">**SQL Server virtual machine size** is the size for both virtual machines that run SQL Server.</span></span> <span data-ttu-id="92666-194">選擇適合工作負載的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="92666-194">Choose an appropriate virtual machine size for your workload.</span></span> <span data-ttu-id="92666-195">如果您要為教學課程建置此環境，請使用 **DS2**。</span><span class="sxs-lookup"><span data-stu-id="92666-195">If you are building this environment for the tutorial, use **DS2**.</span></span> <span data-ttu-id="92666-196">針對生產工作負載，選擇可支援工作負載的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="92666-196">For production workloads, choose a virtual machine size that can support the workload.</span></span> <span data-ttu-id="92666-197">許多生產環境工作負載需要 **DS4** 或更大。</span><span class="sxs-lookup"><span data-stu-id="92666-197">Many production workloads require **DS4** or larger.</span></span> <span data-ttu-id="92666-198">此範本會建置兩個此大小的虛擬機器，並在每個虛擬機器上安裝 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="92666-198">The template builds two virtual machines of this size and installs SQL Server on each one.</span></span> <span data-ttu-id="92666-199">如需相關資訊，請參閱[虛擬機器的大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="92666-199">For more information, see [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="92666-200">Azure 會安裝 SQL Server Enterprise 版。</span><span class="sxs-lookup"><span data-stu-id="92666-200">Azure installs the Enterprise Edition of SQL Server.</span></span> <span data-ttu-id="92666-201">成本根據版本和虛擬機器大小而定。</span><span class="sxs-lookup"><span data-stu-id="92666-201">The cost depends on the edition and the virtual machine size.</span></span> <span data-ttu-id="92666-202">如需目前成本的詳細資訊，請參閱[虛擬機器定價](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql)。</span><span class="sxs-lookup"><span data-stu-id="92666-202">For detailed information about current costs, see [virtual machines pricing](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).</span></span>
>
>

* <span data-ttu-id="92666-203">[網域控制站虛擬機器大小] 是網域控制站的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="92666-203">**Domain controller virtual machine size** is the virtual machine size for the domain controllers.</span></span> <span data-ttu-id="92666-204">本教學課程使用 **D2**。</span><span class="sxs-lookup"><span data-stu-id="92666-204">For this tutorial use **D2**.</span></span>
* <span data-ttu-id="92666-205">[檔案共用見證虛擬機器大小] 是檔案共用見證的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="92666-205">**File Share Witness virtual machine size** is the virtual machine size for the file share witness.</span></span> <span data-ttu-id="92666-206">本教學課程使用 **A1**。</span><span class="sxs-lookup"><span data-stu-id="92666-206">For this tutorial, use **A1**.</span></span>
* <span data-ttu-id="92666-207">**SQL 儲存體帳戶**是存放 SQL Server 資料和作業系統磁碟的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-207">**SQL Storage account** is the name of the storage account that holds the SQL Server data and operating system disks.</span></span> <span data-ttu-id="92666-208">本教學課程使用 **alwaysonsql01**。</span><span class="sxs-lookup"><span data-stu-id="92666-208">For this tutorial, use **alwaysonsql01**.</span></span>
* <span data-ttu-id="92666-209">[DC 儲存體帳戶] 是網域控制站的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-209">**DC Storage account** is the name of the storage account for the domain controllers.</span></span> <span data-ttu-id="92666-210">本教學課程使用 **alwaysondc01**。</span><span class="sxs-lookup"><span data-stu-id="92666-210">For this tutorial, use **alwaysondc01**.</span></span>
* <span data-ttu-id="92666-211">[SQL Server 資料磁碟大小 (TB)] 是 SQL Server 資料磁碟的大小，以 TB 為單位。</span><span class="sxs-lookup"><span data-stu-id="92666-211">**SQL Server data disk size** in TB is the size of the SQL Server data disk in TB.</span></span> <span data-ttu-id="92666-212">指定從 1 到 4 的數字。</span><span class="sxs-lookup"><span data-stu-id="92666-212">Specify a number from 1 through 4.</span></span> <span data-ttu-id="92666-213">本教學課程使用 **1**。</span><span class="sxs-lookup"><span data-stu-id="92666-213">For this tutorial, use **1**.</span></span>
* <span data-ttu-id="92666-214"> 會根據工作負載類型，設定 SQL Server 虛擬機器的特定儲存體組態設定。</span><span class="sxs-lookup"><span data-stu-id="92666-214">**Storage optimization** sets specific storage configuration settings for the SQL Server virtual machines based on the workload type.</span></span> <span data-ttu-id="92666-215">在此案例中，所有 SQL Server 虛擬機器都使用進階儲存體，且 Azure 磁碟主機快取設為唯讀。</span><span class="sxs-lookup"><span data-stu-id="92666-215">All SQL Server virtual machines in this scenario use premium storage with Azure disk host cache set to read-only.</span></span> <span data-ttu-id="92666-216">此外，有下列三種設定供您選擇，以最佳化 SQL Server 的工作負載設定：</span><span class="sxs-lookup"><span data-stu-id="92666-216">In addition, you can optimize SQL Server settings for the workload by choosing one of these three settings:</span></span>

  * <span data-ttu-id="92666-217">**一般工作負載**不會設定任何特定的組態設定。</span><span class="sxs-lookup"><span data-stu-id="92666-217">**General workload** sets no specific configuration settings.</span></span>
  * <span data-ttu-id="92666-218">**交易式處理**會設定追蹤旗標 1117 和 1118。</span><span class="sxs-lookup"><span data-stu-id="92666-218">**Transactional processing** sets trace flag 1117 and 1118.</span></span>
  * <span data-ttu-id="92666-219">**資料倉儲**會設定追蹤旗標 1117 和 610。</span><span class="sxs-lookup"><span data-stu-id="92666-219">**Data warehousing** sets trace flag 1117 and 610.</span></span>

<span data-ttu-id="92666-220">本教學課程使用 [一般工作負載]。</span><span class="sxs-lookup"><span data-stu-id="92666-220">For this tutorial, use **General workload**.</span></span>

![VM 大小儲存體設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

<span data-ttu-id="92666-222">檢閱設定，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="92666-222">Review the settings, and then click **OK**.</span></span>

#### <a name="a-note-about-storage"></a><span data-ttu-id="92666-223">儲存體注意事項</span><span class="sxs-lookup"><span data-stu-id="92666-223">A note about storage</span></span>
<span data-ttu-id="92666-224">其他最佳化視 SQL Server 資料磁碟大小而定。</span><span class="sxs-lookup"><span data-stu-id="92666-224">Additional optimizations depend on the size of the SQL Server data disks.</span></span> <span data-ttu-id="92666-225">Azure 會針對資料磁碟的每一 TB，額外新增 1 TB 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="92666-225">For each terabyte of data disk, Azure adds an additional 1 TB premium storage.</span></span> <span data-ttu-id="92666-226">當伺服器需要 2 TB 以上的空間時，該範本會在每個 SQL Server 虛擬機器上建立儲存體集區。</span><span class="sxs-lookup"><span data-stu-id="92666-226">When a server requires 2 TB or more, the template creates a storage pool on each SQL Server virtual machine.</span></span> <span data-ttu-id="92666-227">存放集區是一種儲存虛擬化，經由設定多張光碟來提供更高的容量、備援及效能。</span><span class="sxs-lookup"><span data-stu-id="92666-227">A storage pool is a form of storage virtualization where multiple discs are configured to provide higher capacity, resiliency, and performance.</span></span>  <span data-ttu-id="92666-228">然後，此範本會在儲存體集區上建立儲存空間，然後向作業系統顯示單一資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="92666-228">The template then creates a storage space on the storage pool and presents a single data disk to the operating system.</span></span> <span data-ttu-id="92666-229">此範本會將此磁碟指定為 SQL Server 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="92666-229">The template designates this disk as the data disk for SQL Server.</span></span> <span data-ttu-id="92666-230">此範本會使用下列設定來調整 SQL Server 的儲存體集區：</span><span class="sxs-lookup"><span data-stu-id="92666-230">The template tunes the storage pool for SQL Server by using the following settings:</span></span>

* <span data-ttu-id="92666-231">等量磁碟區大小為虛擬磁碟的交錯設定。</span><span class="sxs-lookup"><span data-stu-id="92666-231">Stripe size is the interleave setting for the virtual disk.</span></span> <span data-ttu-id="92666-232">交易式工作負載使用 64 KB。</span><span class="sxs-lookup"><span data-stu-id="92666-232">Transactional workloads use 64 KB.</span></span> <span data-ttu-id="92666-233">資料倉儲工作負載使用 256 KB。</span><span class="sxs-lookup"><span data-stu-id="92666-233">Data warehousing workloads use 256 KB.</span></span>
* <span data-ttu-id="92666-234">備援為簡單 (無備援)。</span><span class="sxs-lookup"><span data-stu-id="92666-234">Resiliency is simple (no resiliency).</span></span>

> [!NOTE]
> <span data-ttu-id="92666-235">Premium 進階儲存體為本機備援，在單一區域內會保留三份資料，所以存放集區上不需要額外備援。</span><span class="sxs-lookup"><span data-stu-id="92666-235">Azure premium storage is locally redundant and keeps three copies of the data within a single region, so additional resiliency at the storage pool is not required.</span></span>
>
>

* <span data-ttu-id="92666-236">資料行計數等於存放集區內的磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="92666-236">Column count equals the number of disks in the storage pool.</span></span>

<span data-ttu-id="92666-237">如需儲存空間和儲存體集區的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="92666-237">For additional information about storage space and storage pools, see:</span></span>

* [<span data-ttu-id="92666-238">儲存空間概觀</span><span class="sxs-lookup"><span data-stu-id="92666-238">Storage Spaces Overview</span></span>](http://technet.microsoft.com/library/hh831739.aspx)
* [<span data-ttu-id="92666-239">Windows Server 備份和存放集區</span><span class="sxs-lookup"><span data-stu-id="92666-239">Windows Server Backup and Storage Pools</span></span>](http://technet.microsoft.com/library/dn390929.aspx)

<span data-ttu-id="92666-240">如需有關 SQL Server 組態最佳做法的詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 效能最佳做法](virtual-machines-windows-sql-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="92666-240">For more information about SQL Server configuration best practices, see [Performance best practices for SQL Server in Azure virtual machines](virtual-machines-windows-sql-performance.md).</span></span>

### <a name="sql-server-settings"></a><span data-ttu-id="92666-241">SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="92666-241">SQL Server settings</span></span>
<span data-ttu-id="92666-242">在 [SQL Server 設定] 上，檢閱及修改 SQL Server 虛擬機器名稱前置詞、SQL Server 版本、SQL Server 服務帳戶和密碼，以及 SQL 自動修補維護排程。</span><span class="sxs-lookup"><span data-stu-id="92666-242">On **SQL Server settings**, review and modify the SQL Server virtual machine name prefix, SQL Server version, SQL Server service account and password, and the SQL auto-patching maintenance schedule.</span></span>

* <span data-ttu-id="92666-243">[SQL Server 名稱前置詞] 是用來建立每個 SQL Server 虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-243">**SQL Server Name Prefix** is used to create a name for each SQL Server virtual machine.</span></span> <span data-ttu-id="92666-244">本教學課程使用 **sqlserver**。</span><span class="sxs-lookup"><span data-stu-id="92666-244">For this tutorial, use **sqlserver**.</span></span> <span data-ttu-id="92666-245">範本會將 SQL Server 虛擬機器命名為 *sqlserver-0* 和 *sqlserver-1*。</span><span class="sxs-lookup"><span data-stu-id="92666-245">The template names the SQL Server virtual machines *sqlserver-0* and *sqlserver-1*.</span></span>
* <span data-ttu-id="92666-246">[SQL Server 版本] 是 SQL Server 的版本。</span><span class="sxs-lookup"><span data-stu-id="92666-246">**SQL Server version** is the version of SQL Server.</span></span> <span data-ttu-id="92666-247">本教學課程使用 **SQL Server 2014**。</span><span class="sxs-lookup"><span data-stu-id="92666-247">For this tutorial use **SQL Server 2014**.</span></span> <span data-ttu-id="92666-248">您也可以選擇 **SQL Server 2012** 或 **SQL Server 2016**。</span><span class="sxs-lookup"><span data-stu-id="92666-248">You can also choose **SQL Server 2012** or **SQL Server 2016**.</span></span>
* <span data-ttu-id="92666-249">[SQL Server 服務帳戶使用者名稱] 是 SQL Server 服務的網域帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-249">**SQL Server service account user name** is the domain account name for the SQL Server service.</span></span> <span data-ttu-id="92666-250">本教學課程使用 **sqlservice**。</span><span class="sxs-lookup"><span data-stu-id="92666-250">For this tutorial, use **sqlservice**.</span></span>
* <span data-ttu-id="92666-251"> 是 SQL Server 服務帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="92666-251">**Password** is the password for the SQL Server service account.</span></span>  <span data-ttu-id="92666-252">使用複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="92666-252">Use a complex password.</span></span> <span data-ttu-id="92666-253">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="92666-253">Confirm the password.</span></span>
* <span data-ttu-id="92666-254">[SQL 自動修補維護排程] 會識別 Azure 自動修補 SQL Server 的工作日。</span><span class="sxs-lookup"><span data-stu-id="92666-254">**SQL Auto Patching maintenance schedule** identifies the day of the week that Azure automatically patches the SQL Servers.</span></span> <span data-ttu-id="92666-255">在本教學課程中，請輸入**星期日**。</span><span class="sxs-lookup"><span data-stu-id="92666-255">For this tutorial, type **Sunday**.</span></span>
* <span data-ttu-id="92666-256">[SQL 自動修補維護開始時間] 是開始進行自動修補的 Azure 區域當天時間。</span><span class="sxs-lookup"><span data-stu-id="92666-256">**SQL Auto Patching maintenance start hour** is the time of day for the Azure region when automatic patching begins.</span></span>

> [!NOTE]
> <span data-ttu-id="92666-257">每個虛擬機器的修補時段會錯開一小時。</span><span class="sxs-lookup"><span data-stu-id="92666-257">The patching window for each virtual machine is staggered by one hour.</span></span> <span data-ttu-id="92666-258">一次只會修補一部虛擬機器，以避免服務中斷。</span><span class="sxs-lookup"><span data-stu-id="92666-258">Only one virtual machine is patched at a time to prevent disruption of services.</span></span>
>
>

![SQL Server 設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

<span data-ttu-id="92666-260">檢閱設定，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="92666-260">Review the settings, and then click **OK**.</span></span>

### <a name="summary"></a><span data-ttu-id="92666-261">摘要</span><span class="sxs-lookup"><span data-stu-id="92666-261">Summary</span></span>
<span data-ttu-id="92666-262">在 [摘要] 頁面上，Azure 會驗證設定。</span><span class="sxs-lookup"><span data-stu-id="92666-262">On the summary page, Azure validates the settings.</span></span> <span data-ttu-id="92666-263">您也可以下載此範本。</span><span class="sxs-lookup"><span data-stu-id="92666-263">You can also download the template.</span></span> <span data-ttu-id="92666-264">檢閱摘要。</span><span class="sxs-lookup"><span data-stu-id="92666-264">Review the summary.</span></span> <span data-ttu-id="92666-265">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="92666-265">Click **OK**.</span></span>

### <a name="buy"></a><span data-ttu-id="92666-266">購買</span><span class="sxs-lookup"><span data-stu-id="92666-266">Buy</span></span>
<span data-ttu-id="92666-267">這個最終的刀鋒視窗包含 [使用條款] 和 [隱私權原則]。</span><span class="sxs-lookup"><span data-stu-id="92666-267">This final blade contains **terms of use**, and **privacy policy**.</span></span> <span data-ttu-id="92666-268">檢閱此資訊。</span><span class="sxs-lookup"><span data-stu-id="92666-268">Review this information.</span></span> <span data-ttu-id="92666-269">當您準備好讓 Azure 開始建立虛擬機器及可用性群組的所有其他必要資源時，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="92666-269">When you are ready for Azure to start to create the virtual machines and all the other required resources for the availability group, click **Create**.</span></span>

<span data-ttu-id="92666-270">Azure 入口網站會建立資源群組和所有資源。</span><span class="sxs-lookup"><span data-stu-id="92666-270">The Azure portal creates the resource group and all the resources.</span></span>

## <a name="monitor-deployment"></a><span data-ttu-id="92666-271">監視部署</span><span class="sxs-lookup"><span data-stu-id="92666-271">Monitor deployment</span></span>
<span data-ttu-id="92666-272">從 Azure 入口網站監視部署進度。</span><span class="sxs-lookup"><span data-stu-id="92666-272">Monitor the deployment progress from the Azure portal.</span></span> <span data-ttu-id="92666-273">部署圖示會自動釘選到 Azure 入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="92666-273">An icon that represents the deployment is automatically pinned to the Azure portal dashboard.</span></span>

![Azure 儀表板](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-to-sql-server"></a><span data-ttu-id="92666-275">連接到 SQL Server</span><span class="sxs-lookup"><span data-stu-id="92666-275">Connect to SQL Server</span></span>
<span data-ttu-id="92666-276">SQL Server 的新執行個體會在具有已連線網際網路之 IP 位址的虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="92666-276">The new instances of SQL Server are running on virtual machines that have internet-connected IP addresses.</span></span> <span data-ttu-id="92666-277">您可以直接遠端桌面 (RDP) 連線至每部 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="92666-277">You can remote desktop (RDP) directly to each SQL Server virtual machine.</span></span>

<span data-ttu-id="92666-278">若要以 RDP 連接至 SQL Server，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="92666-278">To RDP to a SQL Server, follow these steps:</span></span>

1. <span data-ttu-id="92666-279">從 Azure 入口網站儀表板中，確認已成功部署。</span><span class="sxs-lookup"><span data-stu-id="92666-279">From the Azure portal dashboard, verify that the deployment has succeeded.</span></span>
2. <span data-ttu-id="92666-280">按一下 [資源] 。</span><span class="sxs-lookup"><span data-stu-id="92666-280">Click **Resources**.</span></span>
3. <span data-ttu-id="92666-281">在 [資源] 刀鋒視窗中，按一下 [sqlserver-0]，這是執行 SQL Server 之其中一部虛擬機器的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-281">In the **Resources** blade, click **sqlserver-0**, which is the computer name of one of the virtual machines that's running SQL Server.</span></span>
4. <span data-ttu-id="92666-282">在 [sqlserver-0] 的刀鋒視窗上，按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="92666-282">On the blade for **sqlserver-0**, click **Connect**.</span></span> <span data-ttu-id="92666-283">瀏覽器會詢問您是否要開啟或儲存遠端連接物件。</span><span class="sxs-lookup"><span data-stu-id="92666-283">Your browser asks if you want to open or save the remote connection object.</span></span> <span data-ttu-id="92666-284">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="92666-284">Click **Open**.</span></span>
5. <span data-ttu-id="92666-285">[遠端桌面連線] 可能會警告您無法識別這個遠端連線的發行者。</span><span class="sxs-lookup"><span data-stu-id="92666-285">**Remote desktop connection** might warn you that the publisher of this remote connection can’t be identified.</span></span> <span data-ttu-id="92666-286">按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="92666-286">Click **Connect**.</span></span>
6. <span data-ttu-id="92666-287">Windows 安全性會提示您輸入認證，以連接到主要網域控制站的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="92666-287">Windows security prompts you to enter your credentials to connect to the IP address of the primary domain controller.</span></span> <span data-ttu-id="92666-288">按一下 [使用其他帳戶]。</span><span class="sxs-lookup"><span data-stu-id="92666-288">Click **Use another account**.</span></span> <span data-ttu-id="92666-289">在 [使用者名稱] 中，輸入 **contoso\DomainAdmin**。</span><span class="sxs-lookup"><span data-stu-id="92666-289">For **User name**, type **contoso\DomainAdmin**.</span></span> <span data-ttu-id="92666-290">當您在範本中設定系統管理員使用者名稱時，您可以設定此帳戶。</span><span class="sxs-lookup"><span data-stu-id="92666-290">You configured this account when you set the administrator user name in the template.</span></span> <span data-ttu-id="92666-291">使用您設定範本時選擇的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="92666-291">Use the complex password that you chose when you configured the template.</span></span>
7. <span data-ttu-id="92666-292">[遠端桌面] 可能會警告您因為安全性憑證有問題，無法驗證遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="92666-292">**Remote desktop** might warn you that the remote computer could not be authenticated due to problems with its security certificate.</span></span> <span data-ttu-id="92666-293">它會顯示安全性憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="92666-293">It shows you the security certificate name.</span></span> <span data-ttu-id="92666-294">如果您依照本教學課程進行，此名稱會是 **sqlserver-0.contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="92666-294">If you followed the tutorial, the name is **sqlserver-0.contoso.com**.</span></span> <span data-ttu-id="92666-295">按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="92666-295">Click **Yes**.</span></span>

<span data-ttu-id="92666-296">您現在已使用 RDP 連線至 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="92666-296">You are now connected with RDP to the SQL Server virtual machine.</span></span> <span data-ttu-id="92666-297">您可以開啟 SQL Server Management Studio、連線到 SQL Server 的預設執行個體，並確認已設定可用性群組。</span><span class="sxs-lookup"><span data-stu-id="92666-297">You can open SQL Server Management Studio, connect to the default instance of SQL Server, and verify that the availability group is configured.</span></span>
