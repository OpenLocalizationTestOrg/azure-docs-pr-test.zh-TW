---
title: "使用 Azure Site Recovery 複寫多層式 Dynamics AX 部署 | Microsoft Docs"
description: "本文說明如何使用 Azure Site Recovery 複寫和保護 Dynamics AX"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="81b0f-103">使用 Azure Site Recovery 複寫多層式 Dynamics AX 應用程式</span><span class="sxs-lookup"><span data-stu-id="81b0f-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="81b0f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="81b0f-104">Overview</span></span>


<span data-ttu-id="81b0f-105">Microsoft Dynamics AX 是企業間受歡迎的 ERP 解決方案之一，可橫跨位置將程序標準化、管理資源及簡化合規性。</span><span class="sxs-lookup"><span data-stu-id="81b0f-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="81b0f-106">考量應用程式攸關組織的業務運作，請務必確定在發生任何災害時，應用程式都能在最短的時間內啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="81b0f-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="81b0f-107">現今，Microsoft Dynamics AX 並未提供任何現成的災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="81b0f-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="81b0f-108">Microsoft Dynamics AX 包含許多伺服器元件，例如 Application Object Server、Active Directory (AD)、SQL Database Server、SharePoint Server、Reporting Server 等。手動管理上述每個元件的災害復原，不僅代價昂貴，而且也容易發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="81b0f-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="81b0f-109">本文詳細說明有關如何使用 [Azure Site Recovery](site-recovery-overview.md) 為 Dynamics AX 應用程式建立災害復原解決方案。</span><span class="sxs-lookup"><span data-stu-id="81b0f-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="81b0f-110">也會探討使用單鍵復原方案、支援的組態和必要條件的計劃性/非計劃性/測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="81b0f-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="81b0f-111">以 Azure Site Recovery 為基礎的災害復原解決方案已經過完整測試、認證並由 Microsoft Dynamics AX 建議。</span><span class="sxs-lookup"><span data-stu-id="81b0f-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="81b0f-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="81b0f-112">Prerequisites</span></span>

<span data-ttu-id="81b0f-113">您需要完成下列必要條件，才能使用 Azure Site Recovery 實作 Dynamics AX 應用程式的災害復原。</span><span class="sxs-lookup"><span data-stu-id="81b0f-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="81b0f-114">•   已設定內部部署 Dynamics AX 部署</span><span class="sxs-lookup"><span data-stu-id="81b0f-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="81b0f-115">•   已在 Microsoft Azure 訂用帳戶中建立 Azure Site Recovery 服務保存庫</span><span class="sxs-lookup"><span data-stu-id="81b0f-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="81b0f-116">•   如果 Azure 是您的復原網站，請在 VM 上執行 Azure 虛擬機器整備評估工具，以確保相容於 Azure VM 與 Azure Site Recovery 服務</span><span class="sxs-lookup"><span data-stu-id="81b0f-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="81b0f-117">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="81b0f-117">Site Recovery support</span></span>

<span data-ttu-id="81b0f-118">為建立這篇文章，會使用 Windows Server 2012 R2 Enterprise 上的 VMware 虛擬機器與 Dynamics AX 2012R3。</span><span class="sxs-lookup"><span data-stu-id="81b0f-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="81b0f-119">因為站台復原複寫應用程式無從驗證，此處提供的建議也都必須保留下列案例。</span><span class="sxs-lookup"><span data-stu-id="81b0f-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="81b0f-120">來源與目標</span><span class="sxs-lookup"><span data-stu-id="81b0f-120">Source and target</span></span>

<span data-ttu-id="81b0f-121">**案例**</span><span class="sxs-lookup"><span data-stu-id="81b0f-121">**Scenario**</span></span> | <span data-ttu-id="81b0f-122">**至次要網站**</span><span class="sxs-lookup"><span data-stu-id="81b0f-122">**To a secondary site**</span></span> | <span data-ttu-id="81b0f-123">**至 Azure**</span><span class="sxs-lookup"><span data-stu-id="81b0f-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="81b0f-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="81b0f-124">**Hyper-V**</span></span> | <span data-ttu-id="81b0f-125">是</span><span class="sxs-lookup"><span data-stu-id="81b0f-125">Yes</span></span> | <span data-ttu-id="81b0f-126">是</span><span class="sxs-lookup"><span data-stu-id="81b0f-126">Yes</span></span>
<span data-ttu-id="81b0f-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="81b0f-127">**VMware**</span></span> | <span data-ttu-id="81b0f-128">是</span><span class="sxs-lookup"><span data-stu-id="81b0f-128">Yes</span></span> | <span data-ttu-id="81b0f-129">是</span><span class="sxs-lookup"><span data-stu-id="81b0f-129">Yes</span></span>
<span data-ttu-id="81b0f-130">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="81b0f-130">**Physical server**</span></span> | <span data-ttu-id="81b0f-131">是</span><span class="sxs-lookup"><span data-stu-id="81b0f-131">Yes</span></span> | <span data-ttu-id="81b0f-132">是</span><span class="sxs-lookup"><span data-stu-id="81b0f-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="81b0f-133">使用 Azure Site Recovery 啟用 Dynamics AX 應用程式的 DR</span><span class="sxs-lookup"><span data-stu-id="81b0f-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="81b0f-134">保護 Dynamics AX 應用程式</span><span class="sxs-lookup"><span data-stu-id="81b0f-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="81b0f-135">Dynamics AX 的每個元件都需要受到保護，才能做到完整的應用程式複寫與復原。</span><span class="sxs-lookup"><span data-stu-id="81b0f-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="81b0f-136">本節涵蓋︰</span><span class="sxs-lookup"><span data-stu-id="81b0f-136">This section covers:</span></span>

<span data-ttu-id="81b0f-137">**1.Active Directory 的保護**</span><span class="sxs-lookup"><span data-stu-id="81b0f-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="81b0f-138">**2.SQL 層的保護**</span><span class="sxs-lookup"><span data-stu-id="81b0f-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="81b0f-139">**3.應用程式和 Web 層的保護**</span><span class="sxs-lookup"><span data-stu-id="81b0f-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="81b0f-140">**4.網路設定**</span><span class="sxs-lookup"><span data-stu-id="81b0f-140">**4. Networking configuration**</span></span>

<span data-ttu-id="81b0f-141">**5.復原方案**</span><span class="sxs-lookup"><span data-stu-id="81b0f-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="81b0f-142">1.安裝 AD 和 DNS 複寫</span><span class="sxs-lookup"><span data-stu-id="81b0f-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="81b0f-143">DR 網站上需要有 Active Directory，Dynamics AX 應用程式才能運作。</span><span class="sxs-lookup"><span data-stu-id="81b0f-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="81b0f-144">根據客戶內部部署環境的複雜度而定，有兩個建議的選擇。</span><span class="sxs-lookup"><span data-stu-id="81b0f-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="81b0f-145">**選項 1**</span><span class="sxs-lookup"><span data-stu-id="81b0f-145">**Option 1**</span></span>

<span data-ttu-id="81b0f-146">如果客戶的整個內部部署網站有少數的應用程式和單一網域控制站，而且將會一起容錯移轉整個網站，則我們建議使用 ASR 複寫將 DC 電腦複寫至次要網站 (適用於網站對網站和網站對 Azure)。</span><span class="sxs-lookup"><span data-stu-id="81b0f-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="81b0f-147">**選項 2**</span><span class="sxs-lookup"><span data-stu-id="81b0f-147">**Option 2**</span></span>

<span data-ttu-id="81b0f-148">如果客戶有大量應用程式、正在執行 Active Directory 樹系，並將一次容錯移轉少數應用程式，則我們建議在 DR 網站 (次要網站或 Azure 中) 另外設定一個網域控制站。</span><span class="sxs-lookup"><span data-stu-id="81b0f-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="81b0f-149">請參閱[在 DR 網站上提供網域控制站的附屬指南](site-recovery-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="81b0f-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="81b0f-150">對於本文件的其餘部分，我們會假設 DR 網站上有 DC 可用。</span><span class="sxs-lookup"><span data-stu-id="81b0f-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="81b0f-151">2.設定 SQL Server 複寫</span><span class="sxs-lookup"><span data-stu-id="81b0f-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="81b0f-152">請參閱附屬指南，以取得建議用於保護 [SQL 層](site-recovery-sql.md)之選項的詳細技術指引。</span><span class="sxs-lookup"><span data-stu-id="81b0f-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="81b0f-153">3.啟用 Dynamics AX 用戶端和 AOS VM 的保護</span><span class="sxs-lookup"><span data-stu-id="81b0f-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="81b0f-154">根據 VM 是部署於 [Hyper-V](site-recovery-hyper-v-site-to-azure.md) 還是 [VMware](site-recovery-vmware-to-azure.md)，執行相關的 Azure Site Recovery 設定。</span><span class="sxs-lookup"><span data-stu-id="81b0f-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="81b0f-155">要設定為 15 分鐘的建議損毀一致頻率。</span><span class="sxs-lookup"><span data-stu-id="81b0f-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="81b0f-156">下列快照集顯示 Dynamics 元件 VM 在「從 VMware 站台到 Azure」保護案例中的保護狀態。</span><span class="sxs-lookup"><span data-stu-id="81b0f-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="81b0f-157">![受保護的項目](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="81b0f-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="81b0f-158">4.設定網路功能</span><span class="sxs-lookup"><span data-stu-id="81b0f-158">4. Configure Networking</span></span>
<span data-ttu-id="81b0f-159">設定 VM 計算和網路設定</span><span class="sxs-lookup"><span data-stu-id="81b0f-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="81b0f-160">對於 AX 用戶端和 AOS VM，設定 Azure Site Recovery 中的網路設定，讓 VM 網路能在容錯移轉之後連結到正確的 DR 網路。</span><span class="sxs-lookup"><span data-stu-id="81b0f-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="81b0f-161">確保這些層的 DR 網路可路由傳送到 SQL 層。</span><span class="sxs-lookup"><span data-stu-id="81b0f-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="81b0f-162">您可以在複寫的項目中選取 VM 來進行網路設定，如以下快照集所示。</span><span class="sxs-lookup"><span data-stu-id="81b0f-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="81b0f-163">對於 AOS 伺服器，選取正確的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="81b0f-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="81b0f-164">如果您是使用靜態 IP 位址，請在![網路設定](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)的 [目標 IP] 欄位中指定您想要虛擬機器採用的 IP。</span><span class="sxs-lookup"><span data-stu-id="81b0f-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="81b0f-165">5.建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="81b0f-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="81b0f-166">您可以在 Azure Site Recovery 中建立復原方案，將容錯移轉程序自動化。</span><span class="sxs-lookup"><span data-stu-id="81b0f-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="81b0f-167">在復原方案中新增應用程式層和 Web 層。</span><span class="sxs-lookup"><span data-stu-id="81b0f-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="81b0f-168">在不同群組中將它們排序，讓前端關機出現在應用程式層之前。</span><span class="sxs-lookup"><span data-stu-id="81b0f-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="81b0f-169">在您的訂用帳戶中選取 Azure Site Recovery 保存庫，然後按一下 [復原方案] 圖格。</span><span class="sxs-lookup"><span data-stu-id="81b0f-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="81b0f-170">按一下 [+ 復原方案] 並指定名稱。</span><span class="sxs-lookup"><span data-stu-id="81b0f-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="81b0f-171">選取 [來源] 和 [目標]。</span><span class="sxs-lookup"><span data-stu-id="81b0f-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="81b0f-172">目標可以是 Azure 或次要網站。</span><span class="sxs-lookup"><span data-stu-id="81b0f-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="81b0f-173">如果您選擇 Azure，則必須指定部署模型</span><span class="sxs-lookup"><span data-stu-id="81b0f-173">In case you choose Azure, you must specify the deployment model</span></span>

![建立復原方案](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="81b0f-175">選取復原方案的 AOS 和用戶端 VM，然後按一下 ✓。</span><span class="sxs-lookup"><span data-stu-id="81b0f-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="81b0f-176">![建立復原方案](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="81b0f-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![復原方案](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="81b0f-178">新增如下所述的各種步驟，即可自訂 Dynamics AX 應用程式的復原方案。</span><span class="sxs-lookup"><span data-stu-id="81b0f-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="81b0f-179">以上的快照集顯示新增所有步驟之後的完整復原方案。</span><span class="sxs-lookup"><span data-stu-id="81b0f-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="81b0f-180">*步驟：*</span><span class="sxs-lookup"><span data-stu-id="81b0f-180">*Steps:*</span></span>

<span data-ttu-id="81b0f-181">*1.SQL Server 容錯移轉步驟*</span><span class="sxs-lookup"><span data-stu-id="81b0f-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="81b0f-182">請參閱 [SQL Server DR 解決方案](site-recovery-sql.md)附屬指南，以了解 SQL Server 在容錯回復期間的特定考量。</span><span class="sxs-lookup"><span data-stu-id="81b0f-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="81b0f-183">*2.容錯移轉群組 1︰容錯移轉 AOS VM*</span><span class="sxs-lookup"><span data-stu-id="81b0f-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="81b0f-184">確定所選取的復原點儘可能接近資料庫 PIT，但不為繼續進行。</span><span class="sxs-lookup"><span data-stu-id="81b0f-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="81b0f-185">*3.指令碼︰新增負載平衡器 (僅限E-A)* 在 AOS VM 群組開始新增負載平衡器之後，新增指令碼 (透過 Azure 自動化)。</span><span class="sxs-lookup"><span data-stu-id="81b0f-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="81b0f-186">您可以使用指令碼來執行此工作。</span><span class="sxs-lookup"><span data-stu-id="81b0f-186">You can use a script to do this task.</span></span> <span data-ttu-id="81b0f-187">請參閱[如何為多層式應用程式 DR 新增負載平衡器](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="81b0f-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="81b0f-188">*4.容錯移轉群組 2︰容錯移轉 AX 用戶端 VM。*</span><span class="sxs-lookup"><span data-stu-id="81b0f-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="81b0f-189">容錯移轉 Web 層 VM 作為復原方案的一部份。</span><span class="sxs-lookup"><span data-stu-id="81b0f-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="81b0f-190">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="81b0f-190">Doing a test failover</span></span>

<span data-ttu-id="81b0f-191">請參閱「AD DR 解決方案」和「SQL Server DR 解決方案」附屬指南，以了解 AD 和 SQL Server 在容錯回復期間各自的特定考量。</span><span class="sxs-lookup"><span data-stu-id="81b0f-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="81b0f-192">移至 Azure 入口網站並選取您的 Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="81b0f-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="81b0f-193">按一下為 Dynamics AX 建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="81b0f-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="81b0f-194">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="81b0f-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="81b0f-195">選取虛擬網路來開始測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="81b0f-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="81b0f-196">次要環境啟動後，您就可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="81b0f-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="81b0f-197">驗證完成後，您可以選取 [完成驗證]，並會清除測試容錯移轉環境。</span><span class="sxs-lookup"><span data-stu-id="81b0f-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="81b0f-198">請依照[本指引](site-recovery-test-failover-to-azure.md)來執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="81b0f-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="81b0f-199">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="81b0f-199">Doing a failover</span></span>

1.  <span data-ttu-id="81b0f-200">移至 Azure 入口網站並選取您的 Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="81b0f-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="81b0f-201">按一下為 Dynamics AX 建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="81b0f-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="81b0f-202">按一下 [容錯移轉]，然後選取 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="81b0f-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="81b0f-203">選取目標網路，然後按一下 ✓ 啟動容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="81b0f-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="81b0f-204">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="81b0f-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="81b0f-205">執行容錯回復</span><span class="sxs-lookup"><span data-stu-id="81b0f-205">Perform a Failback</span></span>

<span data-ttu-id="81b0f-206">請參閱「SQL Server DR 解決方案」附屬指南，以了解 SQL Server 在容錯回復期間的特定考量。</span><span class="sxs-lookup"><span data-stu-id="81b0f-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="81b0f-207">移至 Azure 入口網站並選取您的 Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="81b0f-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="81b0f-208">按一下為 Dynamics AX 建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="81b0f-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="81b0f-209">按一下 [容錯移轉]，然後選取 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="81b0f-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="81b0f-210">按一下 [變更方向]。</span><span class="sxs-lookup"><span data-stu-id="81b0f-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="81b0f-211">選取適當的選項 - 資料同步處理和 VM 建立選項</span><span class="sxs-lookup"><span data-stu-id="81b0f-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="81b0f-212">按一下 ✓ 啟動 [容錯回復] 程序。</span><span class="sxs-lookup"><span data-stu-id="81b0f-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="81b0f-213">當您在進行容錯回復時，請依照[本指引](site-recovery-failback-azure-to-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="81b0f-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="81b0f-214">摘要</span><span class="sxs-lookup"><span data-stu-id="81b0f-214">Summary</span></span>
<span data-ttu-id="81b0f-215">使用 Azure Site Recovery，您可以為 Dynamics AX 應用程式建立一個完整的自動化災害復原方案。</span><span class="sxs-lookup"><span data-stu-id="81b0f-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="81b0f-216">當發生中斷時，您可以在幾秒鐘內從任何地方起始容錯移轉，並且在數分鐘內啟動並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="81b0f-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81b0f-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81b0f-217">Next steps</span></span>
<span data-ttu-id="81b0f-218">閱讀[我可以保護哪些工作負載?](site-recovery-workload.md)，深入了解如何以 Azure Site Recovery 保護企業工作負載。</span><span class="sxs-lookup"><span data-stu-id="81b0f-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
