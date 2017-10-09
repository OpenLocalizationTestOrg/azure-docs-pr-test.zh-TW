---
title: "aaaReplicate 多層式 SharePoint 應用程式使用 Azure Site Recovery |Microsoft 文件"
description: "本文說明如何 tooreplicate 多層式 SharePoint 應用程式使用 Azure Site Recovery 功能。"
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
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a><span data-ttu-id="4d102-103">使用 Azure Site Recovery 複寫多層式 SharePoint 應用程式以便進行災害復原</span><span class="sxs-lookup"><span data-stu-id="4d102-103">Replicate a multi-tier SharePoint application for disaster recovery using Azure Site Recovery</span></span>

<span data-ttu-id="4d102-104">本文詳細說明如何使用 SharePoint 應用程式的 tooprotect [Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4d102-104">This article describes in detail how tooprotect a SharePoint application using  [Azure Site Recovery](site-recovery-overview.md).</span></span>


## <a name="overview"></a><span data-ttu-id="4d102-105">概觀</span><span class="sxs-lookup"><span data-stu-id="4d102-105">Overview</span></span>

<span data-ttu-id="4d102-106">Microsoft SharePoint 是功能強大的應用程式，可協助群組或部門組織、共同作業及共用資訊。</span><span class="sxs-lookup"><span data-stu-id="4d102-106">Microsoft SharePoint is a powerful application that can help a group or department organize, collaborate, and share information.</span></span> <span data-ttu-id="4d102-107">SharePoint 可提供內部網路入口網站、文件和檔案管理、共同作業、社交網路、外部網路、網站、企業搜尋與商業智慧。</span><span class="sxs-lookup"><span data-stu-id="4d102-107">SharePoint can provide intranet portals, document and file management, collaboration, social networks, extranets, websites, enterprise search, and business intelligence.</span></span> <span data-ttu-id="4d102-108">它也具有系統整合、程序整合和工作流程自動化功能。</span><span class="sxs-lookup"><span data-stu-id="4d102-108">It also has system integration, process integration, and workflow automation capabilities.</span></span> <span data-ttu-id="4d102-109">通常，組織將其視為第 1 層應用程式機密 toodowntime 和資料遺失。</span><span class="sxs-lookup"><span data-stu-id="4d102-109">Typically, organizations consider it as a Tier-1 application sensitive toodowntime and data loss.</span></span>

<span data-ttu-id="4d102-110">現今，Microsoft SharePoint 並未提供任何現成的災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="4d102-110">Today, Microsoft SharePoint  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="4d102-111">不論 hello 型別和小數位數的災害，復原會涉及 hello 的待命資料庫的資料中心，您可以 hello 伺服器陣列復原到使用。</span><span class="sxs-lookup"><span data-stu-id="4d102-111">Regardless of hello type and scale of a disaster, recovery involves hello use of a standby data center that you can recover hello farm to.</span></span> <span data-ttu-id="4d102-112">待命資料庫的資料中心案例所需的位置本機備援系統和備份無法從復原在 hello 主要資料中心的 hello 中斷。</span><span class="sxs-lookup"><span data-stu-id="4d102-112">Standby data centers are required for scenarios where local redundant systems and backups cannot recover from hello outage at hello primary data center.</span></span>

<span data-ttu-id="4d102-113">理想的災害復原解決方案應該 hello 複雜的應用程式架構，例如 SharePoint 周圍允許復原方案的模型。</span><span class="sxs-lookup"><span data-stu-id="4d102-113">A good disaster recovery solution should allow modeling of recovery plans around hello  complex application architectures such as SharePoint.</span></span> <span data-ttu-id="4d102-114">它也應該擁有 hello 能力 tooadd 自訂步驟 toohandle 應用程式之間的對應各層，因此具有較低 RTO hello 災害事件中提供單鍵容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4d102-114">It should also have hello ability tooadd customized steps toohandle application mappings between various tiers and hence providing a single-click failover with a lower RTO in hello event of a disaster.</span></span>

<span data-ttu-id="4d102-115">本文詳細說明如何使用 SharePoint 應用程式的 tooprotect [Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4d102-115">This article describes in detail how tooprotect a SharePoint application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="4d102-116">本文將討論複寫三層 SharePoint 應用程式 tooAzure、 告訴您如何進行災害復原訓練，及如何容錯移轉 hello 應用程式 tooAzure 最佳的作法。</span><span class="sxs-lookup"><span data-stu-id="4d102-116">This article will cover best practices for replicating a three tier SharePoint application tooAzure, how you can do a disaster recovery drill, and how you can failover hello application tooAzure.</span></span>

<span data-ttu-id="4d102-117">您可以觀賞復原多層應用程式 tooAzure 相關的影片下方的 hello。</span><span class="sxs-lookup"><span data-stu-id="4d102-117">You can watch hello below video about recovering a multi tier application tooAzure.</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a><span data-ttu-id="4d102-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="4d102-118">Prerequisites</span></span>

<span data-ttu-id="4d102-119">開始之前，請確定您了解 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4d102-119">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="4d102-120">複寫虛擬機器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4d102-120">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
2. <span data-ttu-id="4d102-121">如何太[設計與復原網路](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="4d102-121">How too[design a recovery network](site-recovery-network-design.md)</span></span>
3. [<span data-ttu-id="4d102-122">執行測試容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4d102-122">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
4. [<span data-ttu-id="4d102-123">執行容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4d102-123">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="4d102-124">如何太[複寫的網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="4d102-124">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="4d102-125">如何太[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="4d102-125">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="sharepoint-architecture"></a><span data-ttu-id="4d102-126">SharePoint 架構</span><span class="sxs-lookup"><span data-stu-id="4d102-126">SharePoint architecture</span></span>

<span data-ttu-id="4d102-127">可以使用階層的拓撲和伺服器角色 tooimplement 符合特定目標的伺服器陣列設計的一或多個伺服器上部署 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="4d102-127">SharePoint can be deployed on one or more servers using tiered topologies and server roles tooimplement a farm design that meets specific goals and objectives.</span></span> <span data-ttu-id="4d102-128">支援大量並行使用者和大量內容項目的典型大型、高需求 SharePoint 伺服器陣列，會使用服務群組作為其延展性策略的一部分。</span><span class="sxs-lookup"><span data-stu-id="4d102-128">A typical large, high-demand SharePoint server farm that supports a high number of concurrent users and a large number of content items use service grouping as part of their scalability strategy.</span></span> <span data-ttu-id="4d102-129">這種方法牽涉到將這些服務群組在一起，且再向外擴充 hello 伺服器做為群組的專用伺服器上執行服務。</span><span class="sxs-lookup"><span data-stu-id="4d102-129">This approach involves running services on dedicated servers, grouping these services together, and then scaling out hello servers as a group.</span></span> <span data-ttu-id="4d102-130">hello 下列拓撲描述在 hello 服務和伺服器群組的三層 SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="4d102-130">hello following topology illustrates hello service and server grouping for a three tier SharePoint server farm.</span></span> <span data-ttu-id="4d102-131">請參閱 tooSharePoint 文件和產品線架構的不同 SharePoint 拓撲的詳細指引。</span><span class="sxs-lookup"><span data-stu-id="4d102-131">Please refer tooSharePoint documentation and product line architectures for detailed guidance on different SharePoint topologies.</span></span> <span data-ttu-id="4d102-132">您可以在[這份文件](https://technet.microsoft.com/en-us/library/cc303422.aspx)中找到有關 SharePoint 2013 部署的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4d102-132">You can find more details about SharePoint 2013 deployment in [this document](https://technet.microsoft.com/en-us/library/cc303422.aspx).</span></span>



![部署模式 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a><span data-ttu-id="4d102-134">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="4d102-134">Site Recovery support</span></span>

<span data-ttu-id="4d102-135">為了建立這篇文章，使用了 VMware 虛擬機器搭配 Windows Server 2012 R2 Enterprise。</span><span class="sxs-lookup"><span data-stu-id="4d102-135">For creating this article, VMware virtual machines with Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="4d102-136">還使用 SharePoint 2013 Enterprise 版本和 SQL Server 2014 Enterprise 版本。</span><span class="sxs-lookup"><span data-stu-id="4d102-136">SharePoint 2013 Enterprise edition and SQL server 2014 Enterprise edition were used.</span></span> <span data-ttu-id="4d102-137">站台復原複寫與應用程式無關，因為 hello 建議這裡提供預期的 toohold 上也有下列情況。</span><span class="sxs-lookup"><span data-stu-id="4d102-137">As Site Recovery replication is application agnostic, hello recommendations provided here are expected toohold on for following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="4d102-138">來源與目標</span><span class="sxs-lookup"><span data-stu-id="4d102-138">Source and target</span></span>

<span data-ttu-id="4d102-139">**案例**</span><span class="sxs-lookup"><span data-stu-id="4d102-139">**Scenario**</span></span> | <span data-ttu-id="4d102-140">**tooa 次要站台**</span><span class="sxs-lookup"><span data-stu-id="4d102-140">**tooa secondary site**</span></span> | <span data-ttu-id="4d102-141">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="4d102-141">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="4d102-142">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="4d102-142">**Hyper-V**</span></span> | <span data-ttu-id="4d102-143">是</span><span class="sxs-lookup"><span data-stu-id="4d102-143">Yes</span></span> | <span data-ttu-id="4d102-144">是</span><span class="sxs-lookup"><span data-stu-id="4d102-144">Yes</span></span>
<span data-ttu-id="4d102-145">**VMware**</span><span class="sxs-lookup"><span data-stu-id="4d102-145">**VMware**</span></span> | <span data-ttu-id="4d102-146">是</span><span class="sxs-lookup"><span data-stu-id="4d102-146">Yes</span></span> | <span data-ttu-id="4d102-147">是</span><span class="sxs-lookup"><span data-stu-id="4d102-147">Yes</span></span>
<span data-ttu-id="4d102-148">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="4d102-148">**Physical server**</span></span> | <span data-ttu-id="4d102-149">是</span><span class="sxs-lookup"><span data-stu-id="4d102-149">Yes</span></span> | <span data-ttu-id="4d102-150">是</span><span class="sxs-lookup"><span data-stu-id="4d102-150">Yes</span></span>

### <a name="sharepoint-versions"></a><span data-ttu-id="4d102-151">SharePoint 版本</span><span class="sxs-lookup"><span data-stu-id="4d102-151">SharePoint Versions</span></span>
<span data-ttu-id="4d102-152">支援下列 SharePoint server 版本的 hello。</span><span class="sxs-lookup"><span data-stu-id="4d102-152">hello following SharePoint server versions are supported.</span></span>

* <span data-ttu-id="4d102-153">SharePoint Server 2013 Standard</span><span class="sxs-lookup"><span data-stu-id="4d102-153">SharePoint server 2013 Standard</span></span>
* <span data-ttu-id="4d102-154">SharePoint Server 2013 Enterprise</span><span class="sxs-lookup"><span data-stu-id="4d102-154">SharePoint server 2013 Enterprise</span></span>
* <span data-ttu-id="4d102-155">SharePoint Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="4d102-155">SharePoint server 2016 Standard</span></span>
* <span data-ttu-id="4d102-156">SharePoint Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="4d102-156">SharePoint server 2016 Enterprise</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="4d102-157">請注意的事項 tookeep</span><span class="sxs-lookup"><span data-stu-id="4d102-157">Things tookeep in mind</span></span>

<span data-ttu-id="4d102-158">如果您使用的共用磁碟叢集做為任何層應用程式中，則您不會是能 toouse 站台復原複寫 tooreplicate 這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4d102-158">If you are using a shared disk-based cluster as any tier in your application then you will not be able toouse Site Recovery replication tooreplicate those virtual machines.</span></span> <span data-ttu-id="4d102-159">您可以使用原生 hello 應用程式所提供的複寫，然後使用[復原計劃](site-recovery-create-recovery-plans.md)toofailover 所有層。</span><span class="sxs-lookup"><span data-stu-id="4d102-159">You can use native replication provided by hello application and then use a [recovery plan](site-recovery-create-recovery-plans.md) toofailover all tiers.</span></span>

## <a name="replicating-virtual-machines"></a><span data-ttu-id="4d102-160">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4d102-160">Replicating virtual machines</span></span>

<span data-ttu-id="4d102-161">請遵循[本指南](site-recovery-vmware-to-azure.md)toostart 複寫 hello 虛擬機器 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4d102-161">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello virtual machine tooAzure.</span></span>

* <span data-ttu-id="4d102-162">Hello 複寫完成之後，請確定您移 tooeach 每一層的虛擬機器，然後選取相同的可用性設定組 ' 複寫項目 > 設定 > 內容 > 計算與網路 '。</span><span class="sxs-lookup"><span data-stu-id="4d102-162">Once hello replication is complete, make sure you go tooeach virtual machine of each tier and select same availability set in 'Replicated item > Settings > Properties > Compute and Network'.</span></span> <span data-ttu-id="4d102-163">例如，如果您的 web 層有 3 個 Vm，確定所有 hello 3 的 vm 都設定 toobe 一部分在 Azure 中設定的同一個可用性。</span><span class="sxs-lookup"><span data-stu-id="4d102-163">For example, if your web tier has 3 VMs, ensure all hello 3 VMs are configured toobe part of same availability set in Azure.</span></span>

    ![Set-Availability-Set](./media/site-recovery-sharepoint/select-av-set.png)

* <span data-ttu-id="4d102-165">如需保護 Active Directory 和 DNS 的指引，請參閱太[保護 Active Directory 和 DNS](site-recovery-active-directory.md)文件。</span><span class="sxs-lookup"><span data-stu-id="4d102-165">For guidance on protecting Active Directory and DNS, refer too[Protect Active Directory and DNS](site-recovery-active-directory.md) document.</span></span>

* <span data-ttu-id="4d102-166">如需保護 SQL server 上執行的資料庫層的指引，請參閱太[保護 SQL Server](site-recovery-active-directory.md)文件。</span><span class="sxs-lookup"><span data-stu-id="4d102-166">For guidance on protecting database tier running on SQL server, refer too[Protect SQL Server](site-recovery-active-directory.md) document.</span></span>

## <a name="networking-configuration"></a><span data-ttu-id="4d102-167">網路設定</span><span class="sxs-lookup"><span data-stu-id="4d102-167">Networking configuration</span></span>

### <a name="network-properties"></a><span data-ttu-id="4d102-168">網路屬性</span><span class="sxs-lookup"><span data-stu-id="4d102-168">Network properties</span></span>

* <span data-ttu-id="4d102-169">Hello 應用程式與 Web 層的 Vm，以便讓 hello Vm 取得附加的 toohello 正確 DR 網路容錯移轉之後，Azure 入口網站中設定網路設定。</span><span class="sxs-lookup"><span data-stu-id="4d102-169">For hello App and Web tier VMs, configure network settings in Azure portal so that hello VMs get attached toohello right DR network after failover.</span></span>

    ![選取網路](./media/site-recovery-sharepoint/select-network.png)


* <span data-ttu-id="4d102-171">如果您使用靜態 ip 位址，然後指定您想 hello hello 中的虛擬機器 tootake hello IP**目標 IP**欄位</span><span class="sxs-lookup"><span data-stu-id="4d102-171">If you are using a static IP, then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field</span></span>

    ![設定靜態 IP](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a><span data-ttu-id="4d102-173">DNS 和流量路由</span><span class="sxs-lookup"><span data-stu-id="4d102-173">DNS and Traffic Routing</span></span>

<span data-ttu-id="4d102-174">為網際網路對向站台，[建立 Traffic Manager 設定檔 'Priority' 型別的](../traffic-manager/traffic-manager-create-profile.md)hello Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="4d102-174">For internet facing sites, [create a Traffic Manager profile of 'Priority' type](../traffic-manager/traffic-manager-create-profile.md) in hello Azure subscription.</span></span> <span data-ttu-id="4d102-175">然後在 hello 下列方式設定您的 DNS 和 Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="4d102-175">And then configure your DNS and Traffic Manager profile in hello following manner.</span></span>


| <span data-ttu-id="4d102-176">**其中**</span><span class="sxs-lookup"><span data-stu-id="4d102-176">**Where**</span></span> | <span data-ttu-id="4d102-177">**來源**</span><span class="sxs-lookup"><span data-stu-id="4d102-177">**Source**</span></span> | <span data-ttu-id="4d102-178">**目標**</span><span class="sxs-lookup"><span data-stu-id="4d102-178">**Target**</span></span>|
| --- | --- | --- |
| <span data-ttu-id="4d102-179">公用 DNS</span><span class="sxs-lookup"><span data-stu-id="4d102-179">Public DNS</span></span> | <span data-ttu-id="4d102-180">SharePoint 網站的 公用 DNS</span><span class="sxs-lookup"><span data-stu-id="4d102-180">Public DNS for SharePoint sites</span></span> <br/><br/> <span data-ttu-id="4d102-181">例如︰sharepoint.contoso.com</span><span class="sxs-lookup"><span data-stu-id="4d102-181">Ex: sharepoint.contoso.com</span></span> | <span data-ttu-id="4d102-182">流量管理員</span><span class="sxs-lookup"><span data-stu-id="4d102-182">Traffic Manager</span></span> <br/><br/> <span data-ttu-id="4d102-183">contososharepoint.trafficmanager.net</span><span class="sxs-lookup"><span data-stu-id="4d102-183">contososharepoint.trafficmanager.net</span></span> |
| <span data-ttu-id="4d102-184">內部部署 DNS</span><span class="sxs-lookup"><span data-stu-id="4d102-184">On-premises DNS</span></span> | <span data-ttu-id="4d102-185">sharepointonprem.contoso.com</span><span class="sxs-lookup"><span data-stu-id="4d102-185">sharepointonprem.contoso.com</span></span> | <span data-ttu-id="4d102-186">Hello 在內部部署伺服器陣列上的公用 IP</span><span class="sxs-lookup"><span data-stu-id="4d102-186">Public IP on hello on-premises farm</span></span> |


<span data-ttu-id="4d102-187">在 hello Traffic Manager 設定檔，[主要和復原的端點建立 hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md)。</span><span class="sxs-lookup"><span data-stu-id="4d102-187">In hello Traffic Manager profile, [create hello primary and recovery endpoints](../traffic-manager/traffic-manager-configure-priority-routing-method.md).</span></span> <span data-ttu-id="4d102-188">使用 hello 外部端點的內部端點與 Azure 端點的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="4d102-188">Use hello external endpoint for on-premises endpoint and public IP for Azure endpoint.</span></span> <span data-ttu-id="4d102-189">請確定 hello 優先權會設定較高的 tooon 內部端點。</span><span class="sxs-lookup"><span data-stu-id="4d102-189">Ensure that hello priority is set higher tooon-premises endpoint.</span></span>

<span data-ttu-id="4d102-190">主機測試頁上為了讓 Traffic Manager tooautomatically hello SharePoint web 層中的特定連接埠 (例如 800) 會偵測容錯移轉後的可用性。</span><span class="sxs-lookup"><span data-stu-id="4d102-190">Host a test page on a specific port (for example, 800) in hello SharePoint web tier in order for Traffic Manager tooautomatically detect availability post failover.</span></span> <span data-ttu-id="4d102-191">如果您無法在任何 SharePoint 網站上啟用匿名驗證，這是個解決辦法。</span><span class="sxs-lookup"><span data-stu-id="4d102-191">This is a workaround in case you cannot enable anonymous authentication on any of your SharePoint sites.</span></span>

<span data-ttu-id="4d102-192">[設定 hello Traffic Manager 設定檔](../traffic-manager/traffic-manager-configure-priority-routing-method.md)以 hello 以下設定。</span><span class="sxs-lookup"><span data-stu-id="4d102-192">[Configure hello Traffic Manager profile](../traffic-manager/traffic-manager-configure-priority-routing-method.md) with hello below settings.</span></span>

* <span data-ttu-id="4d102-193">路由方法 -「優先順序」</span><span class="sxs-lookup"><span data-stu-id="4d102-193">Routing method - 'Priority'</span></span>
* <span data-ttu-id="4d102-194">DNS 時間 toolive (TTL)-' 30 秒'</span><span class="sxs-lookup"><span data-stu-id="4d102-194">DNS time toolive (TTL) - '30 seconds'</span></span>
* <span data-ttu-id="4d102-195">端點監視器設定 - 如果您可以啟用匿名驗證，即可提供特定的網站端點。</span><span class="sxs-lookup"><span data-stu-id="4d102-195">Endpoint monitor settings - If you can enable anonymous authentication, you can give a specific website endpoint.</span></span> <span data-ttu-id="4d102-196">或者，您可以在特定連接埠 (例如 800) 上使用測試頁。</span><span class="sxs-lookup"><span data-stu-id="4d102-196">Or, you can use a test page on a specific port (for example, 800).</span></span>

## <a name="creating-a-recovery-plan"></a><span data-ttu-id="4d102-197">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="4d102-197">Creating a recovery plan</span></span>

<span data-ttu-id="4d102-198">復原計劃可讓您排序 hello 容錯移轉維護應用程式一致性是多層式應用程式，因此，在各層。</span><span class="sxs-lookup"><span data-stu-id="4d102-198">A recovery plan allows sequencing hello failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="4d102-199">建立多層式 web 應用程式的復原計劃時，請遵循下面的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="4d102-199">Follow hello below steps while creating a recovery plan for a multi-tier web application.</span></span> <span data-ttu-id="4d102-200">[深入了解如何建立復原計劃](site-recovery-runbook-automation.md#customize-the-recovery-plan)。</span><span class="sxs-lookup"><span data-stu-id="4d102-200">[Learn more about creating a recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="4d102-201">新增虛擬機器 toofailover 群組</span><span class="sxs-lookup"><span data-stu-id="4d102-201">Adding virtual machines toofailover groups</span></span>

1. <span data-ttu-id="4d102-202">建立復原方案所加入的 hello 應用程式和 Web 層 Vm。</span><span class="sxs-lookup"><span data-stu-id="4d102-202">Create a recovery plan by adding hello App and Web tier VMs.</span></span>
2. <span data-ttu-id="4d102-203">按一下 自訂' toogroup hello Vm。</span><span class="sxs-lookup"><span data-stu-id="4d102-203">Click on 'Customize' toogroup hello VMs.</span></span> <span data-ttu-id="4d102-204">根據預設，所有 VM 都是「群組 1」的一部分。</span><span class="sxs-lookup"><span data-stu-id="4d102-204">By default, all VMs are part of 'Group 1'.</span></span>

    ![自訂 RP](./media/site-recovery-sharepoint/rp-groups.png)

3. <span data-ttu-id="4d102-206">建立另一個群組 (群組 2)，並將 hello Web 層 Vm 移到 hello 新群組。</span><span class="sxs-lookup"><span data-stu-id="4d102-206">Create another Group (Group 2) and move hello Web tier VMs into hello new group.</span></span> <span data-ttu-id="4d102-207">您的應用程式層 VM 應該是「群組 1」的一部分，而 Web 層 VM 應該是「群組 2」的一部分。</span><span class="sxs-lookup"><span data-stu-id="4d102-207">Your App tier VMs should be part of 'Group 1' and Web tier VMs should be part of 'Group 2'.</span></span> <span data-ttu-id="4d102-208">這是 hello 應用程式層 Vm 開機第一次後面接著 Web 層 Vm 的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="4d102-208">This is tooensure that hello App tier VMs boot up first followed by Web tier VMs.</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="4d102-209">加入指令碼 toohello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="4d102-209">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="4d102-210">您可以將最常用的 hello Azure 站台復原指令碼部署到您的自動化帳戶按一下下面的 hello '部署 tooAzure' 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4d102-210">You can deploy hello most commonly used Azure Site Recovery scripts into your Automation account clicking hello 'Deploy tooAzure' button below.</span></span> <span data-ttu-id="4d102-211">當您使用任何已發行的指令碼時，請確定您遵循 hello 指令碼中的 hello 指導方針。</span><span class="sxs-lookup"><span data-stu-id="4d102-211">When you are using any published script, ensure you follow hello guidance in hello script.</span></span>

<span data-ttu-id="4d102-212">[![部署 tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="4d102-212">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

1. <span data-ttu-id="4d102-213">新增動作前指令碼 too'Group 1' toofailover SQL 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="4d102-213">Add a pre-action script too'Group 1' toofailover SQL Availability group.</span></span> <span data-ttu-id="4d102-214">使用發行 hello 範例指令碼中的 hello ' ASR-SQL-FailoverAG' 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4d102-214">Use hello 'ASR-SQL-FailoverAG' script published in hello sample scripts.</span></span> <span data-ttu-id="4d102-215">請確定您遵循 hello 指令碼中的 hello 指導方針，變更所需的 hello hello 指令碼中適當地。</span><span class="sxs-lookup"><span data-stu-id="4d102-215">Ensure you follow hello guidance in hello script and make hello required changes in hello script appropriately.</span></span>

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. <span data-ttu-id="4d102-218">新增網頁階層 (群組 2) 的虛擬機器容錯移轉負載平衡器上 hello 後動作指令碼 tooattach。</span><span class="sxs-lookup"><span data-stu-id="4d102-218">Add a post action script tooattach a load balancer on hello failed over virtual machines of Web tier (Group 2).</span></span> <span data-ttu-id="4d102-219">使用發行 hello 範例指令碼中的 hello ' ASR AddSingleLoadBalancer' 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4d102-219">Use hello 'ASR-AddSingleLoadBalancer' script published in hello sample scripts.</span></span> <span data-ttu-id="4d102-220">請確定您遵循 hello 指令碼中的 hello 指導方針，變更所需的 hello hello 指令碼中適當地。</span><span class="sxs-lookup"><span data-stu-id="4d102-220">Ensure you follow hello guidance in hello script and make hello required changes in hello script appropriately.</span></span>

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. <span data-ttu-id="4d102-223">在 Azure 中新增的手動步驟 tooupdate hello DNS 記錄 toopoint toohello 新伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="4d102-223">Add a manual step tooupdate hello DNS records toopoint toohello new farm in Azure.</span></span>

    * <span data-ttu-id="4d102-224">若為網際網路面向網站，容錯移轉後不需要更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="4d102-224">For internet facing sites, no DNS updates are required post failover.</span></span> <span data-ttu-id="4d102-225">請遵循 hello hello '網路指引' 區段 tooconfigure Traffic Manager 中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="4d102-225">Follow hello steps described in hello 'Networking guidance' section tooconfigure Traffic Manager.</span></span> <span data-ttu-id="4d102-226">如果 hello Traffic Manager 設定檔已設定 hello 上一節中所述，，新增指令碼 tooopen 虛擬連接埠 (在 hello 範例 800) hello Azure VM 上。</span><span class="sxs-lookup"><span data-stu-id="4d102-226">If hello Traffic Manager profile has been set up as described in hello previous section, add a script tooopen dummy port (800 in hello example) on hello Azure VM.</span></span>

    * <span data-ttu-id="4d102-227">內部對向的網站，加入手動步驟 tooupdate hello DNS 記錄 toopoint toohello 新 Web 層的 VM 的負載平衡器 IP。</span><span class="sxs-lookup"><span data-stu-id="4d102-227">For internal facing sites, add a manual step tooupdate hello DNS record toopoint toohello new Web tier VM’s load balancer IP.</span></span>

4. <span data-ttu-id="4d102-228">從備份中新增的手動步驟 toorestore 搜尋應用程式或啟動新的搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="4d102-228">Add a manual step toorestore search application from a backup or start a new search service.</span></span>

5. <span data-ttu-id="4d102-229">如需從備份還原搜尋服務應用程式，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4d102-229">For restoring Search service application from a backup, follow below steps.</span></span>

    * <span data-ttu-id="4d102-230">這個方法會假設 hello 搜尋服務應用程式的備份執行之前 hello 重大事件，而且該 hello 備份可以使用在 hello DR 網站。</span><span class="sxs-lookup"><span data-stu-id="4d102-230">This method assumes that a backup of hello Search Service Application was performed before hello catastrophic event and that hello backup is available at hello DR site.</span></span>
    * <span data-ttu-id="4d102-231">這可以輕易地達成排程 hello 備份 （例如每天一次），並在 hello DR 網站使用複製程序 tooplace hello 備份。</span><span class="sxs-lookup"><span data-stu-id="4d102-231">This can easily be achieved by scheduling hello backup (for example, once daily) and using a copy procedure tooplace hello backup at hello DR site.</span></span> <span data-ttu-id="4d102-232">複製程序可能包含指令碼程式，例如 AzCopy (Azure 複製) 或設定 DFSR (分散式檔案服務複寫)。</span><span class="sxs-lookup"><span data-stu-id="4d102-232">Copy procedures could include scripted programs such as AzCopy (Azure Copy) or setting up DFSR (Distributed File Services Replication).</span></span>
    * <span data-ttu-id="4d102-233">現在該 hello SharePoint 伺服器陣列執行時，瀏覽 hello 管理中心] 中，[備份及還原]，然後選取 [還原。</span><span class="sxs-lookup"><span data-stu-id="4d102-233">Now that hello SharePoint farm is running, navigate hello Central Administration, 'Backup and Restore' and select Restore.</span></span> <span data-ttu-id="4d102-234">hello 還原質詢 hello 所指定的備份位置 （您可能需要 tooupdate hello 值）。</span><span class="sxs-lookup"><span data-stu-id="4d102-234">hello restore interrogates hello backup location specified (you may need tooupdate hello value).</span></span> <span data-ttu-id="4d102-235">選取您想要 toorestore hello 搜尋服務應用程式備份。</span><span class="sxs-lookup"><span data-stu-id="4d102-235">Select hello Search Service Application backup you would like toorestore.</span></span>
    * <span data-ttu-id="4d102-236">已還原搜尋。</span><span class="sxs-lookup"><span data-stu-id="4d102-236">Search is restored.</span></span> <span data-ttu-id="4d102-237">請記住，hello 還原預期 toofind hello 相同拓撲 （相同的伺服器數目），和相同硬碟磁碟機代號指派 toothose 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d102-237">Keep in mind that hello restore expects toofind hello same topology (same number of servers) and same hard drive letters assigned toothose servers.</span></span> <span data-ttu-id="4d102-238">如需詳細資訊，請參閱[在 SharePoint 2013 中還原搜尋服務應用程式](https://technet.microsoft.com/library/ee748654.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="4d102-238">For more information, see ['Restore Search service application in SharePoint 2013'](https://technet.microsoft.com/library/ee748654.aspx) document.</span></span>


6. <span data-ttu-id="4d102-239">如需從新的搜尋服務應用程式著手，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4d102-239">For starting with a new Search service application, follow below steps.</span></span>

    * <span data-ttu-id="4d102-240">這個方法會假設 hello 「 搜尋系統管理 」 資料庫的備份可以使用在 hello DR 網站。</span><span class="sxs-lookup"><span data-stu-id="4d102-240">This method assumes that a backup of hello “Search Administration” database is available at hello DR site.</span></span>
    * <span data-ttu-id="4d102-241">Hello 其他搜尋服務應用程式資料庫不會複寫，因為它們會需要 toobe 重新建立。</span><span class="sxs-lookup"><span data-stu-id="4d102-241">Since hello other Search Service Application databases are not replicated, they need toobe re-created.</span></span> <span data-ttu-id="4d102-242">toodo，瀏覽 tooCentral 管理，然後刪除 hello 搜尋服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d102-242">toodo so, navigate tooCentral Administration and delete hello Search Service Application.</span></span> <span data-ttu-id="4d102-243">在任何伺服器上的主機 hello 搜尋索引會刪除 hello 索引檔案。</span><span class="sxs-lookup"><span data-stu-id="4d102-243">On any servers which host hello Search Index, delete hello index files.</span></span>
    * <span data-ttu-id="4d102-244">重新建立 hello 搜尋服務應用程式與這個重新建立 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d102-244">Re-create hello Search Service Application and this re-creates hello databases.</span></span> <span data-ttu-id="4d102-245">建議 toohave 備妥的指令碼重新建立此服務應用程式因為它不可能 tooperform 透過 hello GUI 的所有動作。</span><span class="sxs-lookup"><span data-stu-id="4d102-245">It is recommended toohave a prepared script that re-creates this service application since it is not possible tooperform all actions via hello GUI.</span></span> <span data-ttu-id="4d102-246">例如，設定 hello 索引的磁碟機位置和設定 hello 搜尋拓樸都僅能使用 SharePoint PowerShell 指令程式。</span><span class="sxs-lookup"><span data-stu-id="4d102-246">For example, setting hello index drive location and configuring hello search topology are only possible by using SharePoint PowerShell cmdlets.</span></span> <span data-ttu-id="4d102-247">使用 hello 還原 SPEnterpriseSearchServiceApplication 的 Windows PowerShell cmdlet 並指定 hello 記錄傳送和複寫 Search_Service__DB 搜尋管理資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d102-247">Use hello Windows PowerShell cmdlet Restore-SPEnterpriseSearchServiceApplication and specify hello log-shipped and replicated Search Administration database, Search_Service__DB.</span></span> <span data-ttu-id="4d102-248">此 cmdlet 提供 hello 搜尋設定、 結構描述、 managed 的屬性、 規則和來源並建立一組預設的 hello 其他元件。</span><span class="sxs-lookup"><span data-stu-id="4d102-248">This cmdlet gives hello search configuration, schema, managed properties, rules, and sources and creates a default set of hello other components.</span></span>
    * <span data-ttu-id="4d102-249">一旦搜尋服務應用程式的 hello 加以重新建立，您必須啟動完整搜耙的每個內容來源 toorestore hello 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="4d102-249">Once hello Search Service Application has be re-created, you must start a full crawl for each content source toorestore hello Search Service.</span></span> <span data-ttu-id="4d102-250">您會遺失一些從 hello 在內部部署伺服器陣列，例如搜尋建議的分析資訊。</span><span class="sxs-lookup"><span data-stu-id="4d102-250">You lose some analytics information from hello on-premises farm, such as search recommendations.</span></span>

7. <span data-ttu-id="4d102-251">一旦 hello 的所有步驟都完成都之後，儲存 hello 復原計劃並 hello 最終的復原計劃看起來像下列。</span><span class="sxs-lookup"><span data-stu-id="4d102-251">Once all hello steps are completed, save hello recovery plan and hello final recovery plan will look like following.</span></span>

    ![已儲存的 RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="4d102-253">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="4d102-253">Doing a test failover</span></span>
<span data-ttu-id="4d102-254">請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4d102-254">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

1.  <span data-ttu-id="4d102-255">移 tooAzure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="4d102-255">Go tooAzure portal and select your Recovery Service vault.</span></span>
2.  <span data-ttu-id="4d102-256">按一下 hello 復原計劃建立 SharePoint 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d102-256">Click on hello recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="4d102-257">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="4d102-257">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="4d102-258">選取的復原點和 Azure 虛擬網路 toostart hello 測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="4d102-258">Select recovery point and Azure virtual network toostart hello test failover process.</span></span>
5.  <span data-ttu-id="4d102-259">一旦 hello 次要環境已啟動，您可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="4d102-259">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="4d102-260">Hello 驗證完成後，您可以按一下 清除測試容錯移轉' hello 復原計劃，並會清除 hello 測試容錯移轉環境。</span><span class="sxs-lookup"><span data-stu-id="4d102-260">Once hello validations are complete, you can click 'Cleanup test failover' on hello recovery plan and hello test failover environment is cleaned.</span></span>

<span data-ttu-id="4d102-261">如需 ad 執行測試容錯移轉的指引和 DNS，請參閱太[測試容錯移轉考量 AD 和 DNS](site-recovery-active-directory.md#test-failover-considerations)文件。</span><span class="sxs-lookup"><span data-stu-id="4d102-261">For guidance on doing test failover for AD and DNS, refer too[Test failover considerations for AD and DNS](site-recovery-active-directory.md#test-failover-considerations) document.</span></span>

<span data-ttu-id="4d102-262">如需執行測試容錯移轉的 SQL Alwayson 可用性群組的指引，請參閱太[執行測試容錯移轉 SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover)文件。</span><span class="sxs-lookup"><span data-stu-id="4d102-262">For guidance on doing test failover for SQL Always ON availability groups, refer too[Doing Test failover for SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) document.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="4d102-263">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="4d102-263">Doing a failover</span></span>
<span data-ttu-id="4d102-264">請依照[本指引](site-recovery-failover.md)來進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4d102-264">Follow [this guidance](site-recovery-failover.md) for doing a failover.</span></span>

1.  <span data-ttu-id="4d102-265">移 tooAzure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="4d102-265">Go tooAzure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="4d102-266">按一下 hello 復原計劃建立 SharePoint 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d102-266">Click on hello recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="4d102-267">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="4d102-267">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="4d102-268">選取的復原點 toostart hello 容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="4d102-268">Select recovery point toostart hello failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d102-269">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d102-269">Next steps</span></span>
<span data-ttu-id="4d102-270">您可以深入了解如何使用 Site Recovery [複寫其他應用程式](site-recovery-workload.md)。</span><span class="sxs-lookup"><span data-stu-id="4d102-270">You can learn more about [replicating other applications](site-recovery-workload.md) using Site Recovery.</span></span>
