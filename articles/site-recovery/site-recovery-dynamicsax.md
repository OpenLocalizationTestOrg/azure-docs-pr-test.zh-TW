---
title: "使用 Azure Site Recovery 的多層式 Dynamics AX 部署 aaaReplicate |Microsoft 文件"
description: "本文說明如何 tooreplicate 及保護 Dynamics AX 使用 Azure Site Recovery"
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="4520a-103">使用 Azure Site Recovery 複寫多層式 Dynamics AX 應用程式</span><span class="sxs-lookup"><span data-stu-id="4520a-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="4520a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4520a-104">Overview</span></span>


<span data-ttu-id="4520a-105">Microsoft Dynamics AX hello 熱門 ERP 方案之間的企業 toostandardized 程序的其中一個位置，管理資源和簡化相容性。</span><span class="sxs-lookup"><span data-stu-id="4520a-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="4520a-106">Hello 應用程式是商務關鍵 tooan 組織考量是確定非常重要 toobe，如果任何損毀時，應用程式應該啟動且正在執行中的最小時間。</span><span class="sxs-lookup"><span data-stu-id="4520a-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="4520a-107">現今，Microsoft Dynamics AX 並未提供任何現成的災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="4520a-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="4520a-108">Microsoft Dynamics AX 包含許多伺服器元件，例如應用程式物件的伺服器、 Active Directory (AD)、 SQL 資料庫伺服器，SharePoint 伺服器，以手動方式是 Reporting Server 等 toomanage hello 嚴重損壞修復的每個元件不只若高度耗費資源，但也容易發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="4520a-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="4520a-109">本文詳細說明有關如何使用 [Azure Site Recovery](site-recovery-overview.md) 為 Dynamics AX 應用程式建立災害復原解決方案。</span><span class="sxs-lookup"><span data-stu-id="4520a-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="4520a-110">也會探討使用單鍵復原方案、支援的組態和必要條件的計劃性/非計劃性/測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4520a-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="4520a-111">以 Azure Site Recovery 為基礎的災害復原解決方案已經過完整測試、認證並由 Microsoft Dynamics AX 建議。</span><span class="sxs-lookup"><span data-stu-id="4520a-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="4520a-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="4520a-112">Prerequisites</span></span>

<span data-ttu-id="4520a-113">實作災害復原使用 Azure Site Recovery 的 Dynamics AX 應用程式需要 hello 之後完成的必要元件。</span><span class="sxs-lookup"><span data-stu-id="4520a-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="4520a-114">•   已設定內部部署 Dynamics AX 部署</span><span class="sxs-lookup"><span data-stu-id="4520a-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="4520a-115">•   已在 Microsoft Azure 訂用帳戶中建立 Azure Site Recovery 服務保存庫</span><span class="sxs-lookup"><span data-stu-id="4520a-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="4520a-116">• 如果 Azure 為您的復原網站 hello Azure 虛擬機器整備評估工具上執行的 Vm tooensure 它們相容的 Azure Vm 與 Azure Site Recovery Services</span><span class="sxs-lookup"><span data-stu-id="4520a-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="4520a-117">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="4520a-117">Site Recovery support</span></span>

<span data-ttu-id="4520a-118">Hello 目的是要建立此發行項時，會使用與 Windows Server 2012 R2 Enterprise 上 Dynamics AX 2012R3 VMware 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4520a-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="4520a-119">站台復原複寫與應用程式無關，hello 建議提供以下是預期的 toohold 以及下列案例。</span><span class="sxs-lookup"><span data-stu-id="4520a-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="4520a-120">來源與目標</span><span class="sxs-lookup"><span data-stu-id="4520a-120">Source and target</span></span>

<span data-ttu-id="4520a-121">**案例**</span><span class="sxs-lookup"><span data-stu-id="4520a-121">**Scenario**</span></span> | <span data-ttu-id="4520a-122">**tooa 次要站台**</span><span class="sxs-lookup"><span data-stu-id="4520a-122">**tooa secondary site**</span></span> | <span data-ttu-id="4520a-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="4520a-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="4520a-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="4520a-124">**Hyper-V**</span></span> | <span data-ttu-id="4520a-125">是</span><span class="sxs-lookup"><span data-stu-id="4520a-125">Yes</span></span> | <span data-ttu-id="4520a-126">是</span><span class="sxs-lookup"><span data-stu-id="4520a-126">Yes</span></span>
<span data-ttu-id="4520a-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="4520a-127">**VMware**</span></span> | <span data-ttu-id="4520a-128">是</span><span class="sxs-lookup"><span data-stu-id="4520a-128">Yes</span></span> | <span data-ttu-id="4520a-129">是</span><span class="sxs-lookup"><span data-stu-id="4520a-129">Yes</span></span>
<span data-ttu-id="4520a-130">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="4520a-130">**Physical server**</span></span> | <span data-ttu-id="4520a-131">是</span><span class="sxs-lookup"><span data-stu-id="4520a-131">Yes</span></span> | <span data-ttu-id="4520a-132">是</span><span class="sxs-lookup"><span data-stu-id="4520a-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="4520a-133">使用 Azure Site Recovery 啟用 Dynamics AX 應用程式的 DR</span><span class="sxs-lookup"><span data-stu-id="4520a-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="4520a-134">保護 Dynamics AX 應用程式</span><span class="sxs-lookup"><span data-stu-id="4520a-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="4520a-135">每個元件的 hello Dynamics AX 需求 toobe 保護 tooenable hello 完整的應用程式的複寫和復原。</span><span class="sxs-lookup"><span data-stu-id="4520a-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="4520a-136">本節涵蓋︰</span><span class="sxs-lookup"><span data-stu-id="4520a-136">This section covers:</span></span>

<span data-ttu-id="4520a-137">**1.Active Directory 的保護**</span><span class="sxs-lookup"><span data-stu-id="4520a-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="4520a-138">**2.SQL 層的保護**</span><span class="sxs-lookup"><span data-stu-id="4520a-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="4520a-139">**3.應用程式和 Web 層的保護**</span><span class="sxs-lookup"><span data-stu-id="4520a-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="4520a-140">**4.網路設定**</span><span class="sxs-lookup"><span data-stu-id="4520a-140">**4. Networking configuration**</span></span>

<span data-ttu-id="4520a-141">**5.復原方案**</span><span class="sxs-lookup"><span data-stu-id="4520a-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="4520a-142">1.安裝 AD 和 DNS 複寫</span><span class="sxs-lookup"><span data-stu-id="4520a-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="4520a-143">Active Directory 需要 Dynamics AX 應用程式 toofunction 的 hello DR 網站。</span><span class="sxs-lookup"><span data-stu-id="4520a-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="4520a-144">有兩個建議的選擇依據 hello 客戶的內部部署環境的 hello 複雜性。</span><span class="sxs-lookup"><span data-stu-id="4520a-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="4520a-145">**選項 1**</span><span class="sxs-lookup"><span data-stu-id="4520a-145">**Option 1**</span></span>

<span data-ttu-id="4520a-146">如果 hello 客戶都有少量應用程式和其整個的單一網域控制站在內部部署站台和將會容錯移轉 hello 整個站台在一起，則我們建議使用 ASR 複寫 tooreplicate hello DC 機器 toosecondary 站台 （適用於站台 tooSite 和站台 tooAzure）。</span><span class="sxs-lookup"><span data-stu-id="4520a-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="4520a-147">**選項 2**</span><span class="sxs-lookup"><span data-stu-id="4520a-147">**Option 2**</span></span>

<span data-ttu-id="4520a-148">如果 hello 客戶具有大量的應用程式和執行 Active Directory 樹系，而且將容錯移轉少數應用程式一次，則我們建議您設定 hello DR 網站上的其他網域控制站 (次要站台或 Azure 中)。</span><span class="sxs-lookup"><span data-stu-id="4520a-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="4520a-149">請參閱太[上提供可用的網域控制站在 DR 網站上的附屬指南](site-recovery-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="4520a-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="4520a-150">對於本文件的其餘部分，我們會假設 DR 網站上有 DC 可用。</span><span class="sxs-lookup"><span data-stu-id="4520a-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="4520a-151">2.設定 SQL Server 複寫</span><span class="sxs-lookup"><span data-stu-id="4520a-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="4520a-152">如需詳細指引技術 hello 建議保護選項，請參閱 toocompanion 指南[SQL 層](site-recovery-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="4520a-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="4520a-153">3.啟用 Dynamics AX 用戶端和 AOS VM 的保護</span><span class="sxs-lookup"><span data-stu-id="4520a-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="4520a-154">執行相關的 Azure Site Recovery 設定，根據 hello Vm 是否部署於[HYPER-V](site-recovery-hyper-v-site-to-azure.md)或在[VMware](site-recovery-vmware-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="4520a-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="4520a-155">建議的損毀一致的頻率 tooconfigure 是 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4520a-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="4520a-156">hello 快照下方會顯示 'VMware 站台 tooAzure' 保護案例中的 hello 的 Dynamics 元件 Vm 的保護狀態。</span><span class="sxs-lookup"><span data-stu-id="4520a-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="4520a-157">![受保護的項目](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="4520a-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="4520a-158">4.設定網路功能</span><span class="sxs-lookup"><span data-stu-id="4520a-158">4. Configure Networking</span></span>
<span data-ttu-id="4520a-159">設定 VM 計算和網路設定</span><span class="sxs-lookup"><span data-stu-id="4520a-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="4520a-160">Hello AX 用戶端和 AOS Vm，讓 hello VM 網路中取得附加的 toohello 正確 DR 網路容錯移轉之後，Azure Site Recovery 中設定網路設定。</span><span class="sxs-lookup"><span data-stu-id="4520a-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="4520a-161">請確定這些層的 hello DR 網路路由傳送 toohello SQL 層。</span><span class="sxs-lookup"><span data-stu-id="4520a-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="4520a-162">您可以選取在 hello hello VM 複寫項目 tooconfigure hello 網路設定，下列 hello 快照中所示。</span><span class="sxs-lookup"><span data-stu-id="4520a-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="4520a-163">AOS 伺服器選取 hello 正確的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="4520a-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="4520a-164">如果您使用靜態 ip 位址，則指定您想 hello hello 中的虛擬機器 tootake hello IP**目標 IP**欄位![網路設定](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="4520a-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="4520a-165">5.建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="4520a-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="4520a-166">您可以在 Azure Site Recovery tooautomate hello 容錯移轉程序中建立的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="4520a-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="4520a-167">Hello 復原計劃中加入應用程式層和 web 層。</span><span class="sxs-lookup"><span data-stu-id="4520a-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="4520a-168">排列這些資料行中不同的群組讓的 hello 前端應用程式層之前關閉。</span><span class="sxs-lookup"><span data-stu-id="4520a-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="4520a-169">選取您的訂用帳戶中的 hello Azure Site Recovery 保存庫，並按一下 '復原計畫' 的磚。</span><span class="sxs-lookup"><span data-stu-id="4520a-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="4520a-170">按一下 [+ 復原方案] 並指定名稱。</span><span class="sxs-lookup"><span data-stu-id="4520a-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="4520a-171">選取 hello 'Source' 和 'Target'。</span><span class="sxs-lookup"><span data-stu-id="4520a-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="4520a-172">hello 目標可以是 Azure 或次要站台。</span><span class="sxs-lookup"><span data-stu-id="4520a-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="4520a-173">如果您選擇 Azure，您必須指定 hello 部署模型</span><span class="sxs-lookup"><span data-stu-id="4520a-173">In case you choose Azure, you must specify hello deployment model</span></span>

![建立復原方案](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="4520a-175">選取 hello AOS 與用戶端 Vm toohello 復原計劃，然後按一下 ✓。</span><span class="sxs-lookup"><span data-stu-id="4520a-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="4520a-176">![建立復原方案](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="4520a-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![復原方案](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="4520a-178">您可以藉由新增不同的步驟如下所述自訂 hello Dynamics AX 應用程式的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="4520a-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="4520a-179">hello 快照集上方顯示 hello 完整的復原方案之後加入所有 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="4520a-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="4520a-180">*步驟：*</span><span class="sxs-lookup"><span data-stu-id="4520a-180">*Steps:*</span></span>

<span data-ttu-id="4520a-181">*1.SQL Server 容錯移轉步驟*</span><span class="sxs-lookup"><span data-stu-id="4520a-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="4520a-182">參照太['SQL Server DR 解決方案'](site-recovery-sql.md)附屬指南，如需復原步驟特定 tooSQL 伺服器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4520a-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="4520a-183">*2.容錯移轉群組 1： 容錯移轉 hello AOS Vm*</span><span class="sxs-lookup"><span data-stu-id="4520a-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="4520a-184">請確定選取的復原點 hello 做為可能 toohello 資料庫 PIT 關閉但不是會繼續。</span><span class="sxs-lookup"><span data-stu-id="4520a-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="4520a-185">*3.指令碼： 新增負載平衡器 (僅 E-A)*出現 tooadd 負載平衡器 tooit AOS VM 群組之後加入指令碼 （透過 Azure 自動化）。</span><span class="sxs-lookup"><span data-stu-id="4520a-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="4520a-186">您可以使用指令碼 toodo 這項工作。</span><span class="sxs-lookup"><span data-stu-id="4520a-186">You can use a script toodo this task.</span></span> <span data-ttu-id="4520a-187">發行項，請參閱[如何 tooadd 用於負載平衡器多層式應用程式 DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="4520a-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="4520a-188">*4.容錯移轉群組 2： 容錯移轉 hello AX 用戶端 Vm。*</span><span class="sxs-lookup"><span data-stu-id="4520a-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="4520a-189">容錯移轉的 hello 復原方案一部分的 hello web 層 Vm。</span><span class="sxs-lookup"><span data-stu-id="4520a-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="4520a-190">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="4520a-190">Doing a test failover</span></span>

<span data-ttu-id="4520a-191">Too'AD DR 解決方案，請參閱 ' 與 'SQL Server DR 解決方案' 附屬指南考量特定 tooAD 和分別測試容錯移轉期間的 SQL server。</span><span class="sxs-lookup"><span data-stu-id="4520a-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="4520a-192">移 tooAzure 入口網站，然後選取您的站台復原保存庫。</span><span class="sxs-lookup"><span data-stu-id="4520a-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="4520a-193">按一下建立的 Dynamics AX hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="4520a-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="4520a-194">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="4520a-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="4520a-195">選取 hello 虛擬網路 toostart hello 測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="4520a-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="4520a-196">一旦 hello 次要環境已啟動，您可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="4520a-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="4520a-197">Hello 驗證完成後，您可以選取 '完成驗證'，並將清除 hello 測試容錯移轉環境。</span><span class="sxs-lookup"><span data-stu-id="4520a-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="4520a-198">請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4520a-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="4520a-199">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="4520a-199">Doing a failover</span></span>

1.  <span data-ttu-id="4520a-200">移 tooAzure 入口網站，然後選取您的站台復原保存庫。</span><span class="sxs-lookup"><span data-stu-id="4520a-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="4520a-201">按一下建立的 Dynamics AX hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="4520a-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="4520a-202">按一下 [容錯移轉]，然後選取 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="4520a-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="4520a-203">選取 hello 目標網路，然後按一下 ✓ toostart hello 容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="4520a-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="4520a-204">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="4520a-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="4520a-205">執行容錯回復</span><span class="sxs-lookup"><span data-stu-id="4520a-205">Perform a Failback</span></span>

<span data-ttu-id="4520a-206">Too'SQL 伺服器 DR 解決方案，請參閱 ' 考量特定 tooSQL 伺服器在容錯回復期間的附屬指南。</span><span class="sxs-lookup"><span data-stu-id="4520a-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="4520a-207">移 tooAzure 入口網站，然後選取您的站台復原保存庫。</span><span class="sxs-lookup"><span data-stu-id="4520a-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="4520a-208">按一下建立的 Dynamics AX hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="4520a-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="4520a-209">按一下 [容錯移轉]，然後選取 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="4520a-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="4520a-210">按一下 [變更方向]。</span><span class="sxs-lookup"><span data-stu-id="4520a-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="4520a-211">選取 hello 適當的選項為 VM 建立選項與資料同步處理</span><span class="sxs-lookup"><span data-stu-id="4520a-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="4520a-212">按一下 ✓ toostart hello '容錯回復' 處理序。</span><span class="sxs-lookup"><span data-stu-id="4520a-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="4520a-213">當您在進行容錯回復時，請依照[本指引](site-recovery-failback-azure-to-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="4520a-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="4520a-214">摘要</span><span class="sxs-lookup"><span data-stu-id="4520a-214">Summary</span></span>
<span data-ttu-id="4520a-215">使用 Azure Site Recovery，您可以為 Dynamics AX 應用程式建立一個完整的自動化災害復原方案。</span><span class="sxs-lookup"><span data-stu-id="4520a-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="4520a-216">您可以從任何地方秒內起始 hello 容錯移轉在 hello 中斷的事件，並取得 hello 應用程式啟動並執行以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="4520a-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4520a-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4520a-217">Next steps</span></span>
<span data-ttu-id="4520a-218">讀取[可以保護哪些工作負載？](site-recovery-workload.md) toolearn 深入了解保護與 Azure Site Recovery 的企業工作負載。</span><span class="sxs-lookup"><span data-stu-id="4520a-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
