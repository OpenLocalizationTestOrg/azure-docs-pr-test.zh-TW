---
title: "使用 Azure Site Recovery 複寫多層式 SharePoint 應用程式 | Microsoft Docs"
description: "本文說明如何使用 Azure Site Recovery 功能複寫多層式 SharePoint 應用程式。"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: 9c0570b9da661a8ffb0041e5c24905480f55f6e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a><span data-ttu-id="549b6-103">使用 Azure Site Recovery 複寫多層式 SharePoint 應用程式以便進行災害復原</span><span class="sxs-lookup"><span data-stu-id="549b6-103">Replicate a multi-tier SharePoint application for disaster recovery using Azure Site Recovery</span></span>

<span data-ttu-id="549b6-104">本文詳細說明如何使用 [Azure Site Recovery](site-recovery-overview.md) 保護 SharePoint 應用程式。</span><span class="sxs-lookup"><span data-stu-id="549b6-104">This article describes in detail how to protect a SharePoint application using  [Azure Site Recovery](site-recovery-overview.md).</span></span>


## <a name="overview"></a><span data-ttu-id="549b6-105">概觀</span><span class="sxs-lookup"><span data-stu-id="549b6-105">Overview</span></span>

<span data-ttu-id="549b6-106">Microsoft SharePoint 是功能強大的應用程式，可協助群組或部門組織、共同作業及共用資訊。</span><span class="sxs-lookup"><span data-stu-id="549b6-106">Microsoft SharePoint is a powerful application that can help a group or department organize, collaborate, and share information.</span></span> <span data-ttu-id="549b6-107">SharePoint 可提供內部網路入口網站、文件和檔案管理、共同作業、社交網路、外部網路、網站、企業搜尋與商業智慧。</span><span class="sxs-lookup"><span data-stu-id="549b6-107">SharePoint can provide intranet portals, document and file management, collaboration, social networks, extranets, websites, enterprise search, and business intelligence.</span></span> <span data-ttu-id="549b6-108">它也具有系統整合、程序整合和工作流程自動化功能。</span><span class="sxs-lookup"><span data-stu-id="549b6-108">It also has system integration, process integration, and workflow automation capabilities.</span></span> <span data-ttu-id="549b6-109">一般而言，組織會將其視為對停機時間和資料遺失很敏感的第 1 層應用程式。</span><span class="sxs-lookup"><span data-stu-id="549b6-109">Typically, organizations consider it as a Tier-1 application sensitive to downtime and data loss.</span></span>

<span data-ttu-id="549b6-110">現今，Microsoft SharePoint 並未提供任何現成的災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="549b6-110">Today, Microsoft SharePoint  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="549b6-111">不論災害的類型和規模為何，復原都會涉及使用您可以將伺服器陣列復原至的待命資料中心。</span><span class="sxs-lookup"><span data-stu-id="549b6-111">Regardless of the type and scale of a disaster, recovery involves the use of a standby data center that you can recover the farm to.</span></span> <span data-ttu-id="549b6-112">在本機備援系統和備份無法自主要資料中心中斷修復的情況下，需要待命資料中心。</span><span class="sxs-lookup"><span data-stu-id="549b6-112">Standby data centers are required for scenarios where local redundant systems and backups cannot recover from the outage at the primary data center.</span></span>

<span data-ttu-id="549b6-113">理想的災害復原解決方案應允許以複雜應用程式架構 (例如 SharePoint) 為主的復原方案模型。</span><span class="sxs-lookup"><span data-stu-id="549b6-113">A good disaster recovery solution should allow modeling of recovery plans around the  complex application architectures such as SharePoint.</span></span> <span data-ttu-id="549b6-114">它也應該能夠新增自訂步驟，以處理各層之間的應用程式對應，因而提供在發生災害時具有較低 RTO 的單鍵容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="549b6-114">It should also have the ability to add customized steps to handle application mappings between various tiers and hence providing a single-click failover with a lower RTO in the event of a disaster.</span></span>

<span data-ttu-id="549b6-115">本文詳細說明如何使用 [Azure Site Recovery](site-recovery-overview.md) 保護 SharePoint 應用程式。</span><span class="sxs-lookup"><span data-stu-id="549b6-115">This article describes in detail how to protect a SharePoint application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="549b6-116">本文將介紹最佳做法來將三層 SharePoint 應用程式複寫至 Azure、如何進行災害復原訓練，以及如何將應用程式容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="549b6-116">This article will cover best practices for replicating a three tier SharePoint application to Azure, how you can do a disaster recovery drill, and how you can failover the application to Azure.</span></span>

<span data-ttu-id="549b6-117">您可以觀賞以下有關將多層式應用程式復原至 Azure 的影片。</span><span class="sxs-lookup"><span data-stu-id="549b6-117">You can watch the below video about recovering a multi tier application to Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a><span data-ttu-id="549b6-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="549b6-118">Prerequisites</span></span>

<span data-ttu-id="549b6-119">開始之前，請確定您瞭解下列項目︰</span><span class="sxs-lookup"><span data-stu-id="549b6-119">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="549b6-120">將虛擬機器複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="549b6-120">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
2. <span data-ttu-id="549b6-121">如何[設計修復網路](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="549b6-121">How to [design a recovery network](site-recovery-network-design.md)</span></span>
3. [<span data-ttu-id="549b6-122">執行測試容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="549b6-122">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
4. [<span data-ttu-id="549b6-123">執行容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="549b6-123">Doing a failover to Azure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="549b6-124">如何[複寫網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="549b6-124">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="549b6-125">如何[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="549b6-125">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="sharepoint-architecture"></a><span data-ttu-id="549b6-126">SharePoint 架構</span><span class="sxs-lookup"><span data-stu-id="549b6-126">SharePoint architecture</span></span>

<span data-ttu-id="549b6-127">可以使用分層式拓撲和伺服器角色在一或多部伺服器上部署 SharePoint，以實作符合特定目標的伺服器陣列設計。</span><span class="sxs-lookup"><span data-stu-id="549b6-127">SharePoint can be deployed on one or more servers using tiered topologies and server roles to implement a farm design that meets specific goals and objectives.</span></span> <span data-ttu-id="549b6-128">支援大量並行使用者和大量內容項目的典型大型、高需求 SharePoint 伺服器陣列，會使用服務群組作為其延展性策略的一部分。</span><span class="sxs-lookup"><span data-stu-id="549b6-128">A typical large, high-demand SharePoint server farm that supports a high number of concurrent users and a large number of content items use service grouping as part of their scalability strategy.</span></span> <span data-ttu-id="549b6-129">這種方法涉及在專用伺服器上執行服務、將這些服務群組在一起，然後將伺服器相應放大為群組。</span><span class="sxs-lookup"><span data-stu-id="549b6-129">This approach involves running services on dedicated servers, grouping these services together, and then scaling out the servers as a group.</span></span> <span data-ttu-id="549b6-130">下列拓撲說明三層式 SharePoint 伺服器陣列的服務與伺服器群組。</span><span class="sxs-lookup"><span data-stu-id="549b6-130">The following topology illustrates the service and server grouping for a three tier SharePoint server farm.</span></span> <span data-ttu-id="549b6-131">如需不同 SharePoint 拓撲的詳細指引，請參閱 SharePoint 文件集和產品線架構。</span><span class="sxs-lookup"><span data-stu-id="549b6-131">Please refer to SharePoint documentation and product line architectures for detailed guidance on different SharePoint topologies.</span></span> <span data-ttu-id="549b6-132">您可以在[這份文件](https://technet.microsoft.com/en-us/library/cc303422.aspx)中找到有關 SharePoint 2013 部署的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="549b6-132">You can find more details about SharePoint 2013 deployment in [this document](https://technet.microsoft.com/en-us/library/cc303422.aspx).</span></span>



![部署模式 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a><span data-ttu-id="549b6-134">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="549b6-134">Site Recovery support</span></span>

<span data-ttu-id="549b6-135">為了建立這篇文章，使用了 VMware 虛擬機器搭配 Windows Server 2012 R2 Enterprise。</span><span class="sxs-lookup"><span data-stu-id="549b6-135">For creating this article, VMware virtual machines with Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="549b6-136">還使用 SharePoint 2013 Enterprise 版本和 SQL Server 2014 Enterprise 版本。</span><span class="sxs-lookup"><span data-stu-id="549b6-136">SharePoint 2013 Enterprise edition and SQL server 2014 Enterprise edition were used.</span></span> <span data-ttu-id="549b6-137">因為站台復原複寫應用程式無從驗證，此處提供的建議也都必須對下列案例保留。</span><span class="sxs-lookup"><span data-stu-id="549b6-137">As Site Recovery replication is application agnostic, the recommendations provided here are expected to hold on for following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="549b6-138">來源與目標</span><span class="sxs-lookup"><span data-stu-id="549b6-138">Source and target</span></span>

<span data-ttu-id="549b6-139">**案例**</span><span class="sxs-lookup"><span data-stu-id="549b6-139">**Scenario**</span></span> | <span data-ttu-id="549b6-140">**至次要網站**</span><span class="sxs-lookup"><span data-stu-id="549b6-140">**To a secondary site**</span></span> | <span data-ttu-id="549b6-141">**至 Azure**</span><span class="sxs-lookup"><span data-stu-id="549b6-141">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="549b6-142">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="549b6-142">**Hyper-V**</span></span> | <span data-ttu-id="549b6-143">是</span><span class="sxs-lookup"><span data-stu-id="549b6-143">Yes</span></span> | <span data-ttu-id="549b6-144">是</span><span class="sxs-lookup"><span data-stu-id="549b6-144">Yes</span></span>
<span data-ttu-id="549b6-145">**VMware**</span><span class="sxs-lookup"><span data-stu-id="549b6-145">**VMware**</span></span> | <span data-ttu-id="549b6-146">是</span><span class="sxs-lookup"><span data-stu-id="549b6-146">Yes</span></span> | <span data-ttu-id="549b6-147">是</span><span class="sxs-lookup"><span data-stu-id="549b6-147">Yes</span></span>
<span data-ttu-id="549b6-148">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="549b6-148">**Physical server**</span></span> | <span data-ttu-id="549b6-149">是</span><span class="sxs-lookup"><span data-stu-id="549b6-149">Yes</span></span> | <span data-ttu-id="549b6-150">是</span><span class="sxs-lookup"><span data-stu-id="549b6-150">Yes</span></span>

### <a name="sharepoint-versions"></a><span data-ttu-id="549b6-151">SharePoint 版本</span><span class="sxs-lookup"><span data-stu-id="549b6-151">SharePoint Versions</span></span>
<span data-ttu-id="549b6-152">支援下列 SharePoint Server 版本。</span><span class="sxs-lookup"><span data-stu-id="549b6-152">The following SharePoint server versions are supported.</span></span>

* <span data-ttu-id="549b6-153">SharePoint Server 2013 Standard</span><span class="sxs-lookup"><span data-stu-id="549b6-153">SharePoint server 2013 Standard</span></span>
* <span data-ttu-id="549b6-154">SharePoint Server 2013 Enterprise</span><span class="sxs-lookup"><span data-stu-id="549b6-154">SharePoint server 2013 Enterprise</span></span>
* <span data-ttu-id="549b6-155">SharePoint Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="549b6-155">SharePoint server 2016 Standard</span></span>
* <span data-ttu-id="549b6-156">SharePoint Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="549b6-156">SharePoint server 2016 Enterprise</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="549b6-157">要牢記在心的事項</span><span class="sxs-lookup"><span data-stu-id="549b6-157">Things to keep in mind</span></span>

<span data-ttu-id="549b6-158">如果您使用以磁碟為基礎的共用叢集作為您應用程式中的任何層，然後您將無法使用 Site Recovery 複寫來複寫這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="549b6-158">If you are using a shared disk-based cluster as any tier in your application then you will not be able to use Site Recovery replication to replicate those virtual machines.</span></span> <span data-ttu-id="549b6-159">您可以使用應用程式所提供的原生複寫，然後使用[復原方案](site-recovery-create-recovery-plans.md)來容錯移轉所有層。</span><span class="sxs-lookup"><span data-stu-id="549b6-159">You can use native replication provided by the application and then use a [recovery plan](site-recovery-create-recovery-plans.md) to failover all tiers.</span></span>

## <a name="replicating-virtual-machines"></a><span data-ttu-id="549b6-160">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="549b6-160">Replicating virtual machines</span></span>

<span data-ttu-id="549b6-161">請依照[本指引](site-recovery-vmware-to-azure.md)開始將虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="549b6-161">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the virtual machine to Azure.</span></span>

* <span data-ttu-id="549b6-162">複寫完成後，請務必移至每層的每部虛擬機器，然後在 [複寫項目 > 設定 > 屬性 > 計算和網路] 中選取相同的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="549b6-162">Once the replication is complete, make sure you go to each virtual machine of each tier and select same availability set in 'Replicated item > Settings > Properties > Compute and Network'.</span></span> <span data-ttu-id="549b6-163">例如，如果您的 Web 層有 3 部 VM，請確定這 3 部 VM 全會設定為 Azure 中相同可用性設定組的一部分。</span><span class="sxs-lookup"><span data-stu-id="549b6-163">For example, if your web tier has 3 VMs, ensure all the 3 VMs are configured to be part of same availability set in Azure.</span></span>

    ![Set-Availability-Set](./media/site-recovery-sharepoint/select-av-set.png)

* <span data-ttu-id="549b6-165">如需保護 Active Directory 和 DNS 的指引，請參閱[保護 Active Directory 和 DNS](site-recovery-active-directory.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="549b6-165">For guidance on protecting Active Directory and DNS, refer to [Protect Active Directory and DNS](site-recovery-active-directory.md) document.</span></span>

* <span data-ttu-id="549b6-166">如需保護在 SQL Server 上執行之資料庫層的指引，請參閱[保護 SQL Server](site-recovery-active-directory.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="549b6-166">For guidance on protecting database tier running on SQL server, refer to [Protect SQL Server](site-recovery-active-directory.md) document.</span></span>

## <a name="networking-configuration"></a><span data-ttu-id="549b6-167">網路設定</span><span class="sxs-lookup"><span data-stu-id="549b6-167">Networking configuration</span></span>

### <a name="network-properties"></a><span data-ttu-id="549b6-168">網路屬性</span><span class="sxs-lookup"><span data-stu-id="549b6-168">Network properties</span></span>

* <span data-ttu-id="549b6-169">對於應用程式和 Web 層 VM，在 Azure 入口網站中設定網路設定，讓 VM 能在容錯移轉之後連結到正確的 DR 網路。</span><span class="sxs-lookup"><span data-stu-id="549b6-169">For the App and Web tier VMs, configure network settings in Azure portal so that the VMs get attached to the right DR network after failover.</span></span>

    ![選取網路](./media/site-recovery-sharepoint/select-network.png)


* <span data-ttu-id="549b6-171">如果您是使用靜態 IP 位址，然後在 [目標 IP] 欄位中指定您希望虛擬機器採用的 IP</span><span class="sxs-lookup"><span data-stu-id="549b6-171">If you are using a static IP, then specify the IP that you want the virtual machine to take in the **Target IP** field</span></span>

    ![設定靜態 IP](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a><span data-ttu-id="549b6-173">DNS 和流量路由</span><span class="sxs-lookup"><span data-stu-id="549b6-173">DNS and Traffic Routing</span></span>

<span data-ttu-id="549b6-174">針對網際網路面向網站，在 Azure 訂用帳戶中[建立「優先順序」類型的流量管理員設定檔](../traffic-manager/traffic-manager-create-profile.md)。</span><span class="sxs-lookup"><span data-stu-id="549b6-174">For internet facing sites, [create a Traffic Manager profile of 'Priority' type](../traffic-manager/traffic-manager-create-profile.md) in the Azure subscription.</span></span> <span data-ttu-id="549b6-175">然後以下列方式設定您的 DNS 和流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="549b6-175">And then configure your DNS and Traffic Manager profile in the following manner.</span></span>


| <span data-ttu-id="549b6-176">**其中**</span><span class="sxs-lookup"><span data-stu-id="549b6-176">**Where**</span></span> | <span data-ttu-id="549b6-177">**來源**</span><span class="sxs-lookup"><span data-stu-id="549b6-177">**Source**</span></span> | <span data-ttu-id="549b6-178">**目標**</span><span class="sxs-lookup"><span data-stu-id="549b6-178">**Target**</span></span>|
| --- | --- | --- |
| <span data-ttu-id="549b6-179">公用 DNS</span><span class="sxs-lookup"><span data-stu-id="549b6-179">Public DNS</span></span> | <span data-ttu-id="549b6-180">SharePoint 網站的 公用 DNS</span><span class="sxs-lookup"><span data-stu-id="549b6-180">Public DNS for SharePoint sites</span></span> <br/><br/> <span data-ttu-id="549b6-181">例如︰sharepoint.contoso.com</span><span class="sxs-lookup"><span data-stu-id="549b6-181">Ex: sharepoint.contoso.com</span></span> | <span data-ttu-id="549b6-182">流量管理員</span><span class="sxs-lookup"><span data-stu-id="549b6-182">Traffic Manager</span></span> <br/><br/> <span data-ttu-id="549b6-183">contososharepoint.trafficmanager.net</span><span class="sxs-lookup"><span data-stu-id="549b6-183">contososharepoint.trafficmanager.net</span></span> |
| <span data-ttu-id="549b6-184">內部部署 DNS</span><span class="sxs-lookup"><span data-stu-id="549b6-184">On-premises DNS</span></span> | <span data-ttu-id="549b6-185">sharepointonprem.contoso.com</span><span class="sxs-lookup"><span data-stu-id="549b6-185">sharepointonprem.contoso.com</span></span> | <span data-ttu-id="549b6-186">內部部署伺服器陣列上的公用 IP</span><span class="sxs-lookup"><span data-stu-id="549b6-186">Public IP on the on-premises farm</span></span> |


<span data-ttu-id="549b6-187">在流量管理員設定檔中，[建立主要和復原端點](../traffic-manager/traffic-manager-configure-priority-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="549b6-187">In the Traffic Manager profile, [create the primary and recovery endpoints](../traffic-manager/traffic-manager-configure-priority-routing-method.md).</span></span> <span data-ttu-id="549b6-188">使用內部部署端點的外部端點和 Azure 端點的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="549b6-188">Use the external endpoint for on-premises endpoint and public IP for Azure endpoint.</span></span> <span data-ttu-id="549b6-189">確保內部部署端點的優先順序設定為較高。</span><span class="sxs-lookup"><span data-stu-id="549b6-189">Ensure that the priority is set higher to on-premises endpoint.</span></span>

<span data-ttu-id="549b6-190">在 SharePoint Web 層中的特定通訊埠 (例如 800) 上裝載測試頁，以便流量管理員自動偵測容錯移轉後的可用性。</span><span class="sxs-lookup"><span data-stu-id="549b6-190">Host a test page on a specific port (for example, 800) in the SharePoint web tier in order for Traffic Manager to automatically detect availability post failover.</span></span> <span data-ttu-id="549b6-191">如果您無法在任何 SharePoint 網站上啟用匿名驗證，這是個解決辦法。</span><span class="sxs-lookup"><span data-stu-id="549b6-191">This is a workaround in case you cannot enable anonymous authentication on any of your SharePoint sites.</span></span>

<span data-ttu-id="549b6-192">使用下列設定來[設定流量管理員設定檔](../traffic-manager/traffic-manager-configure-priority-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="549b6-192">[Configure the Traffic Manager profile](../traffic-manager/traffic-manager-configure-priority-routing-method.md) with the below settings.</span></span>

* <span data-ttu-id="549b6-193">路由方法 -「優先順序」</span><span class="sxs-lookup"><span data-stu-id="549b6-193">Routing method - 'Priority'</span></span>
* <span data-ttu-id="549b6-194">DNS 存留時間 (TTL) -「30 秒」</span><span class="sxs-lookup"><span data-stu-id="549b6-194">DNS time to live (TTL) - '30 seconds'</span></span>
* <span data-ttu-id="549b6-195">端點監視器設定 - 如果您可以啟用匿名驗證，即可提供特定的網站端點。</span><span class="sxs-lookup"><span data-stu-id="549b6-195">Endpoint monitor settings - If you can enable anonymous authentication, you can give a specific website endpoint.</span></span> <span data-ttu-id="549b6-196">或者，您可以在特定連接埠 (例如 800) 上使用測試頁。</span><span class="sxs-lookup"><span data-stu-id="549b6-196">Or, you can use a test page on a specific port (for example, 800).</span></span>

## <a name="creating-a-recovery-plan"></a><span data-ttu-id="549b6-197">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="549b6-197">Creating a recovery plan</span></span>

<span data-ttu-id="549b6-198">復原計劃可讓您在多層式應用程式中排序各層的容錯移轉，因此可維護應用程式一致性。</span><span class="sxs-lookup"><span data-stu-id="549b6-198">A recovery plan allows sequencing the failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="549b6-199">建立多層式 web 應用程式的復原計畫時請，遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="549b6-199">Follow the below steps while creating a recovery plan for a multi-tier web application.</span></span> <span data-ttu-id="549b6-200">[深入了解如何建立復原計劃](site-recovery-runbook-automation.md#customize-the-recovery-plan)。</span><span class="sxs-lookup"><span data-stu-id="549b6-200">[Learn more about creating a recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="549b6-201">將虛擬機器新增至容錯移轉群組</span><span class="sxs-lookup"><span data-stu-id="549b6-201">Adding virtual machines to failover groups</span></span>

1. <span data-ttu-id="549b6-202">新增應用程式和 Web 層 VM，以建立復原方案。</span><span class="sxs-lookup"><span data-stu-id="549b6-202">Create a recovery plan by adding the App and Web tier VMs.</span></span>
2. <span data-ttu-id="549b6-203">按一下 [自訂] 將 VM 分組。</span><span class="sxs-lookup"><span data-stu-id="549b6-203">Click on 'Customize' to group the VMs.</span></span> <span data-ttu-id="549b6-204">根據預設，所有 VM 都是「群組 1」的一部分。</span><span class="sxs-lookup"><span data-stu-id="549b6-204">By default, all VMs are part of 'Group 1'.</span></span>

    ![自訂 RP](./media/site-recovery-sharepoint/rp-groups.png)

3. <span data-ttu-id="549b6-206">建立另一個群組 (群組 2)，並將 Web 層 VM 移到新群組中。</span><span class="sxs-lookup"><span data-stu-id="549b6-206">Create another Group (Group 2) and move the Web tier VMs into the new group.</span></span> <span data-ttu-id="549b6-207">您的應用程式層 VM 應該是「群組 1」的一部分，而 Web 層 VM 應該是「群組 2」的一部分。</span><span class="sxs-lookup"><span data-stu-id="549b6-207">Your App tier VMs should be part of 'Group 1' and Web tier VMs should be part of 'Group 2'.</span></span> <span data-ttu-id="549b6-208">這是為了確保應用程式層 VM 先啟動，Web 層 VM 再接著啟動。</span><span class="sxs-lookup"><span data-stu-id="549b6-208">This is to ensure that the App tier VMs boot up first followed by Web tier VMs.</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="549b6-209">將指令碼新增至復原計畫</span><span class="sxs-lookup"><span data-stu-id="549b6-209">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="549b6-210">您可以按一下底下的 [部署至 Azure] 按鈕，將最常用的 Azure Site Recovery 指令碼部署至您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="549b6-210">You can deploy the most commonly used Azure Site Recovery scripts into your Automation account clicking the 'Deploy to Azure' button below.</span></span> <span data-ttu-id="549b6-211">當您使用任何已發佈的指令碼時，請務必遵循指令碼中的指引。</span><span class="sxs-lookup"><span data-stu-id="549b6-211">When you are using any published script, ensure you follow the guidance in the script.</span></span>

<span data-ttu-id="549b6-212">[![部署至 Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="549b6-212">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

1. <span data-ttu-id="549b6-213">將動作前指令碼新增至「群組 1」，以容錯移轉 SQL 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="549b6-213">Add a pre-action script to 'Group 1' to failover SQL Availability group.</span></span> <span data-ttu-id="549b6-214">使用在範例指令碼中發佈的 'ASR-SQL-FailoverAG' 指令碼。</span><span class="sxs-lookup"><span data-stu-id="549b6-214">Use the 'ASR-SQL-FailoverAG' script published in the sample scripts.</span></span> <span data-ttu-id="549b6-215">請務必遵循指令碼中的指引，並在指令碼中適當地進行必要的變更。</span><span class="sxs-lookup"><span data-stu-id="549b6-215">Ensure you follow the guidance in the script and make the required changes in the script appropriately.</span></span>

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. <span data-ttu-id="549b6-218">新增動作後指令碼，以連結 Web 層 (群組 2) 之已容錯移轉虛擬機器上的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="549b6-218">Add a post action script to attach a load balancer on the failed over virtual machines of Web tier (Group 2).</span></span> <span data-ttu-id="549b6-219">使用在範例指令碼中發佈的 'ASR-AddSingleLoadBalancer' 指令碼。</span><span class="sxs-lookup"><span data-stu-id="549b6-219">Use the 'ASR-AddSingleLoadBalancer' script published in the sample scripts.</span></span> <span data-ttu-id="549b6-220">請務必遵循指令碼中的指引，並在指令碼中適當地進行必要的變更。</span><span class="sxs-lookup"><span data-stu-id="549b6-220">Ensure you follow the guidance in the script and make the required changes in the script appropriately.</span></span>

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. <span data-ttu-id="549b6-223">新增手動步驟來更新 DNS 記錄，以指向 Azure 中新的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="549b6-223">Add a manual step to update the DNS records to point to the new farm in Azure.</span></span>

    * <span data-ttu-id="549b6-224">若為網際網路面向網站，容錯移轉後不需要更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="549b6-224">For internet facing sites, no DNS updates are required post failover.</span></span> <span data-ttu-id="549b6-225">遵循「網路指引」一節所述的步驟來設定流量管理員。</span><span class="sxs-lookup"><span data-stu-id="549b6-225">Follow the steps described in the 'Networking guidance' section to configure Traffic Manager.</span></span> <span data-ttu-id="549b6-226">如果已如上一節所述設定流量管理員設定檔，請新增一個指令碼，以開啟 Azure VM 上的虛擬連接埠 (在此範例中為 800)。</span><span class="sxs-lookup"><span data-stu-id="549b6-226">If the Traffic Manager profile has been set up as described in the previous section, add a script to open dummy port (800 in the example) on the Azure VM.</span></span>

    * <span data-ttu-id="549b6-227">針對內部面向網站，新增一個手動步驟來更新 DNS 記錄，以指向新 Web 層 VM 的負載平衡器 IP。</span><span class="sxs-lookup"><span data-stu-id="549b6-227">For internal facing sites, add a manual step to update the DNS record to point to the new Web tier VM’s load balancer IP.</span></span>

4. <span data-ttu-id="549b6-228">新增一個手動步驟，以從備份還原搜尋應用程式或啟動新的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="549b6-228">Add a manual step to restore search application from a backup or start a new search service.</span></span>

5. <span data-ttu-id="549b6-229">如需從備份還原搜尋服務應用程式，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="549b6-229">For restoring Search service application from a backup, follow below steps.</span></span>

    * <span data-ttu-id="549b6-230">此方法假設搜尋服務應用程式的備份已在災難性事件之前執行，而且可在 DR 網站上取得該備份。</span><span class="sxs-lookup"><span data-stu-id="549b6-230">This method assumes that a backup of the Search Service Application was performed before the catastrophic event and that the backup is available at the DR site.</span></span>
    * <span data-ttu-id="549b6-231">排定備份 (例如，每天一次) 並使用複製程序將備份置於 DR 網站上，即可輕鬆達成。</span><span class="sxs-lookup"><span data-stu-id="549b6-231">This can easily be achieved by scheduling the backup (for example, once daily) and using a copy procedure to place the backup at the DR site.</span></span> <span data-ttu-id="549b6-232">複製程序可能包含指令碼程式，例如 AzCopy (Azure 複製) 或設定 DFSR (分散式檔案服務複寫)。</span><span class="sxs-lookup"><span data-stu-id="549b6-232">Copy procedures could include scripted programs such as AzCopy (Azure Copy) or setting up DFSR (Distributed File Services Replication).</span></span>
    * <span data-ttu-id="549b6-233">既然 SharePoint 伺服器陣列正在執行中，請瀏覽 [管理中心]、[備份及還原]，然後選取 [還原]。</span><span class="sxs-lookup"><span data-stu-id="549b6-233">Now that the SharePoint farm is running, navigate the Central Administration, 'Backup and Restore' and select Restore.</span></span> <span data-ttu-id="549b6-234">還原會質詢所指定的備份位置 (您可能需要更新此值)。</span><span class="sxs-lookup"><span data-stu-id="549b6-234">The restore interrogates the backup location specified (you may need to update the value).</span></span> <span data-ttu-id="549b6-235">選取您想要還原的搜尋服務應用程式備份。</span><span class="sxs-lookup"><span data-stu-id="549b6-235">Select the Search Service Application backup you would like to restore.</span></span>
    * <span data-ttu-id="549b6-236">已還原搜尋。</span><span class="sxs-lookup"><span data-stu-id="549b6-236">Search is restored.</span></span> <span data-ttu-id="549b6-237">請記住，還原應會發現相同的拓撲 (相同的伺服器數目) 以及指派給這些伺服器的相同硬碟磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="549b6-237">Keep in mind that the restore expects to find the same topology (same number of servers) and same hard drive letters assigned to those servers.</span></span> <span data-ttu-id="549b6-238">如需詳細資訊，請參閱[在 SharePoint 2013 中還原搜尋服務應用程式](https://technet.microsoft.com/library/ee748654.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="549b6-238">For more information, see ['Restore Search service application in SharePoint 2013'](https://technet.microsoft.com/library/ee748654.aspx) document.</span></span>


6. <span data-ttu-id="549b6-239">如需從新的搜尋服務應用程式著手，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="549b6-239">For starting with a new Search service application, follow below steps.</span></span>

    * <span data-ttu-id="549b6-240">此方法假設可在 DR 網站上取得「搜尋管理」資料庫的備份。</span><span class="sxs-lookup"><span data-stu-id="549b6-240">This method assumes that a backup of the “Search Administration” database is available at the DR site.</span></span>
    * <span data-ttu-id="549b6-241">由於不會複寫其他搜尋服務應用程式資料庫，因此必須加以重建。</span><span class="sxs-lookup"><span data-stu-id="549b6-241">Since the other Search Service Application databases are not replicated, they need to be re-created.</span></span> <span data-ttu-id="549b6-242">若要這麼做，請瀏覽至管理中心並刪除搜尋服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="549b6-242">To do so, navigate to Central Administration and delete the Search Service Application.</span></span> <span data-ttu-id="549b6-243">在任何裝載搜尋索引的伺服器上，刪除索引檔案。</span><span class="sxs-lookup"><span data-stu-id="549b6-243">On any servers which host the Search Index, delete the index files.</span></span>
    * <span data-ttu-id="549b6-244">重建搜尋服務應用程式，而這會重建資料庫。</span><span class="sxs-lookup"><span data-stu-id="549b6-244">Re-create the Search Service Application and this re-creates the databases.</span></span> <span data-ttu-id="549b6-245">建議備妥一個指令碼來重建此服務應用程式，因為不可能透過 GUI 執行所有動作。</span><span class="sxs-lookup"><span data-stu-id="549b6-245">It is recommended to have a prepared script that re-creates this service application since it is not possible to perform all actions via the GUI.</span></span> <span data-ttu-id="549b6-246">例如，唯有使用 SharePoint PowerShell cmdlet，才可能設定索引磁碟機位置及設定搜尋拓撲。</span><span class="sxs-lookup"><span data-stu-id="549b6-246">For example, setting the index drive location and configuring the search topology are only possible by using SharePoint PowerShell cmdlets.</span></span> <span data-ttu-id="549b6-247">使用 Windows PowerShell Cmdlet Restore-SPEnterpriseSearchServiceApplication 並指定記錄隨附和複寫的搜尋管理資料庫 Search_Service__DB。</span><span class="sxs-lookup"><span data-stu-id="549b6-247">Use the Windows PowerShell cmdlet Restore-SPEnterpriseSearchServiceApplication and specify the log-shipped and replicated Search Administration database, Search_Service__DB.</span></span> <span data-ttu-id="549b6-248">此 Cmdlet 可提供搜尋組態、結構描述、受管理的屬性、規則和來源，並建立一組預設的其他元件。</span><span class="sxs-lookup"><span data-stu-id="549b6-248">This cmdlet gives the search configuration, schema, managed properties, rules, and sources and creates a default set of the other components.</span></span>
    * <span data-ttu-id="549b6-249">一旦重建搜尋服務應用程式，您就必須為每個內容來源啟動完整編目，以還原搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="549b6-249">Once the Search Service Application has be re-created, you must start a full crawl for each content source to restore the Search Service.</span></span> <span data-ttu-id="549b6-250">您會從內部部署伺服器陣列遺失一些分析資訊，例如搜尋建議。</span><span class="sxs-lookup"><span data-stu-id="549b6-250">You lose some analytics information from the on-premises farm, such as search recommendations.</span></span>

7. <span data-ttu-id="549b6-251">完成所有步驟後，儲存復原方案，而最終的復原方案如下所示。</span><span class="sxs-lookup"><span data-stu-id="549b6-251">Once all the steps are completed, save the recovery plan and the final recovery plan will look like following.</span></span>

    ![已儲存的 RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="549b6-253">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="549b6-253">Doing a test failover</span></span>
<span data-ttu-id="549b6-254">請依照[本指引](site-recovery-test-failover-to-azure.md)來執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="549b6-254">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

1.  <span data-ttu-id="549b6-255">請移至 Azure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="549b6-255">Go to Azure portal and select your Recovery Service vault.</span></span>
2.  <span data-ttu-id="549b6-256">按一下為 SharePoint 應用程式建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="549b6-256">Click on the recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="549b6-257">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="549b6-257">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="549b6-258">選取復原點和 Azure 虛擬網路來開始測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="549b6-258">Select recovery point and Azure virtual network to start the test failover process.</span></span>
5.  <span data-ttu-id="549b6-259">次要環境啟動後，您就可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="549b6-259">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="549b6-260">完成驗證後，您可以按一下復原方案上的 [清除測試容錯移轉]，而測試容錯移轉環境會清除。</span><span class="sxs-lookup"><span data-stu-id="549b6-260">Once the validations are complete, you can click 'Cleanup test failover' on the recovery plan and the test failover environment is cleaned.</span></span>

<span data-ttu-id="549b6-261">如需有關進行 AD 和 DNS 之測試容錯移轉的指引，請參閱 [AD 和 DNS 的測試容錯移轉考量](site-recovery-active-directory.md#test-failover-considerations)文件。</span><span class="sxs-lookup"><span data-stu-id="549b6-261">For guidance on doing test failover for AD and DNS, refer to [Test failover considerations for AD and DNS](site-recovery-active-directory.md#test-failover-considerations) document.</span></span>

<span data-ttu-id="549b6-262">如需有關進行 SQL Always ON 可用性群組之測試容錯移轉的指引，請參閱[進行 SQL Server Always On 的測試容錯移轉](site-recovery-sql.md#steps-to-do-a-test-failover)文件。</span><span class="sxs-lookup"><span data-stu-id="549b6-262">For guidance on doing test failover for SQL Always ON availability groups, refer to [Doing Test failover for SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) document.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="549b6-263">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="549b6-263">Doing a failover</span></span>
<span data-ttu-id="549b6-264">請依照[本指引](site-recovery-failover.md)來進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="549b6-264">Follow [this guidance](site-recovery-failover.md) for doing a failover.</span></span>

1.  <span data-ttu-id="549b6-265">請移至 Azure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="549b6-265">Go to Azure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="549b6-266">按一下為 SharePoint 應用程式建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="549b6-266">Click on the recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="549b6-267">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="549b6-267">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="549b6-268">選取復原點以啟動容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="549b6-268">Select recovery point to start the failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="549b6-269">後續步驟</span><span class="sxs-lookup"><span data-stu-id="549b6-269">Next steps</span></span>
<span data-ttu-id="549b6-270">您可以深入了解如何使用 Site Recovery [複寫其他應用程式](site-recovery-workload.md)。</span><span class="sxs-lookup"><span data-stu-id="549b6-270">You can learn more about [replicating other applications](site-recovery-workload.md) using Site Recovery.</span></span>
