---
title: "使用 Azure Site Recovery 保護多層式 SAP NetWeaver 應用程式部署 | Microsoft Docs"
description: "本文說明如何使用 Azure Site Recovery 保護 SAP NetWeaver 應用程式部署"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 951980eeba61e53c983d5b23c301c81eee9528bd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a><span data-ttu-id="70732-103">使用 Azure Site Recovery 保護多層式 SAP NetWeaver 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="70732-103">Protect a multi-tier SAP NetWeaver application deployment using Azure Site Recovery</span></span>

<span data-ttu-id="70732-104">大部分的大型與中型 SAP 部署都有某種形式的災害復原方案。</span><span class="sxs-lookup"><span data-stu-id="70732-104">Most large and medium-sized SAP deployments have some form of Disaster Recovery solution.</span></span>  <span data-ttu-id="70732-105">隨著移至應用程式 (如 SAP) 的核心商務程序愈來愈多，強固且可測試的災害復原解決方案愈形重要。</span><span class="sxs-lookup"><span data-stu-id="70732-105">The importance of robust and testable Disaster Recovery solutions has increased as more core business processes are moved to applications such as SAP.</span></span>  <span data-ttu-id="70732-106">Azure Site Recovery 已經過測試並與 SAP 應用程式整合，以比競爭解決方案低的總體擁有成本 (TCO)，超越大部分的內部部署災害復原解決方案。</span><span class="sxs-lookup"><span data-stu-id="70732-106">Azure Site Recovery has been tested and integrated with SAP applications, and exceeds the capabilities of most on-premises Disaster Recovery solutions, at a lower total cost of ownership (TCO) than competing solutions.</span></span>
<span data-ttu-id="70732-107">使用 Azure Site Recovery，您可以：</span><span class="sxs-lookup"><span data-stu-id="70732-107">With Azure Site Recovery you can:</span></span>
* <span data-ttu-id="70732-108">藉由將元件複寫到 Azure，啟用在內部部署環境執行之 SAP NetWeaver 和非 NetWeaver 生產應用程式的保護功能。</span><span class="sxs-lookup"><span data-stu-id="70732-108">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running on-premises, by replicating components to Azure.</span></span>
* <span data-ttu-id="70732-109">藉由將元件複寫到另一個 Azure 資料中心，啟用執行 Azure 之 SAP NetWeaver 和非 NetWeaver 生產應用程式的保護功能。</span><span class="sxs-lookup"><span data-stu-id="70732-109">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running Azure, by replicating components to another Azure datacenter.</span></span>
* <span data-ttu-id="70732-110">使用 Site Recovery 將您的 SAP 部署移轉至 Azure，來簡化雲端移轉。</span><span class="sxs-lookup"><span data-stu-id="70732-110">Simplify cloud migration, by using Site Recovery to migrate your SAP deployment to Azure.</span></span>
* <span data-ttu-id="70732-111">藉由建立隨選生產複本來測試 SAP 應用程式，簡化 SAP 專案升級、測試和原型設計。</span><span class="sxs-lookup"><span data-stu-id="70732-111">Simplify SAP project upgrades, testing, and prototyping, by creating a production clone on-demand for testing SAP applications.</span></span>

<span data-ttu-id="70732-112">本文說明如何使用 [Azure Site Recovery](site-recovery-overview.md) 保護 SAP NetWeaver 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="70732-112">This article describes how to protect SAP NetWeaver application deployments using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="70732-113">本文涵蓋下列最佳做法︰使用 Azure Site Recovery 複寫到另一個 Azure 資料中心，以保護 Azure 上的三層式 SAP NetWeaver 部署，支援的案例和組態，以及如何執行容錯移轉 (包括測試容錯移轉 (災害復原演練) 和實際容錯移轉)。</span><span class="sxs-lookup"><span data-stu-id="70732-113">This article covers the best practices for protecting a three-tier SAP NetWeaver deployment on Azure by replicating to another Azure datacenter using Azure Site Recovery, the supported scenarios and configurations, and how to perform failovers, both test failovers (disaster recovery drills) and actual failovers.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="70732-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="70732-114">Prerequisites</span></span>
<span data-ttu-id="70732-115">開始之前，請確定您瞭解下列項目︰</span><span class="sxs-lookup"><span data-stu-id="70732-115">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="70732-116">將虛擬機器複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="70732-116">Replicating a virtual machine to Azure</span></span>](azure-to-azure-walkthrough-enable-replication.md)
2. <span data-ttu-id="70732-117">如何[設計修復網路](site-recovery-azure-to-azure-networking-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="70732-117">How to [design a recovery network](site-recovery-azure-to-azure-networking-guidance.md)</span></span>
3. [<span data-ttu-id="70732-118">執行測試容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="70732-118">Doing a test failover to Azure</span></span>](azure-to-azure-walkthrough-test-failover.md)
4. [<span data-ttu-id="70732-119">執行容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="70732-119">Doing a failover to Azure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="70732-120">如何[複寫網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="70732-120">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="70732-121">如何[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="70732-121">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="70732-122">支援的案例</span><span class="sxs-lookup"><span data-stu-id="70732-122">Supported scenarios</span></span>
<span data-ttu-id="70732-123">使用 Azure Site Recovery，您可以針對下列案例實作災害復原解決方案：</span><span class="sxs-lookup"><span data-stu-id="70732-123">With Azure Site Recovery you can implement a disaster recovery solution for the following scenarios:</span></span>
* <span data-ttu-id="70732-124">在一個 Azure 資料中心執行並複寫至另一個 Azure 資料中心 (Azure 對 Azure DR) 的 SAP 系統，其架構[在此](https://aka.ms/asr-a2a-architecture)。</span><span class="sxs-lookup"><span data-stu-id="70732-124">SAP systems running in one Azure datacenter replicating to another Azure datacenter (Azure-to-Azure DR), as architected [here](https://aka.ms/asr-a2a-architecture).</span></span>
* <span data-ttu-id="70732-125">在內部部署 VMWare (或實體) 伺服器上執行並複寫至 Azure 資料中心 DR 網站 (VMware-to-Azure DR) 的 SAP 系統，這需要一些額外的元件，其架構[在此](https://aka.ms/asr-v2a-architecture)。</span><span class="sxs-lookup"><span data-stu-id="70732-125">SAP systems running on VMWare (or Physical) servers on-premises replicating to a DR site in an Azure datacenter (VMware-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-v2a-architecture).</span></span>
* <span data-ttu-id="70732-126">在內部部署 Hyper-V 上執行並複寫至 Azure 資料中心 DR 網站 (Hyper-V-to-Azure DR) 的 SAP 系統，這需要一些額外的元件，其架構[在此](https://aka.ms/asr-h2a-architecture)。</span><span class="sxs-lookup"><span data-stu-id="70732-126">SAP systems running on Hyper-V on-premises replicating to a DR site in an Azure datacenter (Hyper-V-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-h2a-architecture).</span></span>

<span data-ttu-id="70732-127">本文件使用第一個案例 (Azure 對 Azure DR) 來示範 Azure Site Recovery 的 SAP 災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="70732-127">This document uses the first case - Azure-to-Azure DR - to demonstrate Azure Site Recovery's SAP disaster recovery capabilities.</span></span> <span data-ttu-id="70732-128">因為 Azure Site Recovery 複寫無從驗證應用程式，所以此處描述的程序應針對其他案例保留。</span><span class="sxs-lookup"><span data-stu-id="70732-128">As Azure Site Recovery replication is application agnostic, the process described is expected to hold for other scenarios as well.</span></span>

### <a name="required-foundation-services"></a><span data-ttu-id="70732-129">必要的基礎服務</span><span class="sxs-lookup"><span data-stu-id="70732-129">Required foundation services</span></span>
<span data-ttu-id="70732-130">此文件案例已部署下列基礎服務：</span><span class="sxs-lookup"><span data-stu-id="70732-130">This documentation scenario all been deployed with the following foundation services deployed:</span></span>
* <span data-ttu-id="70732-131">ExpressRoute 或站對站虛擬私人網路 (VPN)</span><span class="sxs-lookup"><span data-stu-id="70732-131">ExpressRoute or Site-to-Site Virtual Private Network (VPN)</span></span>
* <span data-ttu-id="70732-132">至少有一個 Active Directory 網域控制站和 DNS 伺服器在 Azure 中執行</span><span class="sxs-lookup"><span data-stu-id="70732-132">At least one Active Directory Domain Controller and DNS server running in Azure</span></span>

<span data-ttu-id="70732-133">建議在部署 Azure Site Recovery 之前建立上述基礎結構。</span><span class="sxs-lookup"><span data-stu-id="70732-133">It is recommended that the infrastructure above is established prior to deploying Azure Site Recovery.</span></span>


## <a name="typical-sap-application-deployment"></a><span data-ttu-id="70732-134">典型 SAP 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="70732-134">Typical SAP application deployment</span></span>
<span data-ttu-id="70732-135">大型 SAP 客戶通常部署 6 到 20 個個別的 SAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70732-135">Large SAP customers usually deploy between 6 to 20 individual SAP applications.</span></span>  <span data-ttu-id="70732-136">這些應用程式大部分是以 SAP NetWeaver ABAP 或 Java 引擎為基礎。</span><span class="sxs-lookup"><span data-stu-id="70732-136">Most of these applications are based on the SAP NetWeaver ABAP or Java engines.</span></span>  <span data-ttu-id="70732-137">這些核心 NetWeaver 應用程式 (有些通常是非 SAP 應用程式) 是由許多小型特定非 NetWeaver SAP 獨立引擎支援。</span><span class="sxs-lookup"><span data-stu-id="70732-137">Supporting these core NetWeaver applications are many smaller specific non-NetWeaver SAP standalone engines and typically some non-SAP applications.</span></span>  

<span data-ttu-id="70732-138">務必清查在環境中執行的所有 SAP 應用程式，並判斷部署模式 (2 層或 3 層)、版本、修補程式、大小、變換率，以及磁碟持續性需求。</span><span class="sxs-lookup"><span data-stu-id="70732-138">It is critical to inventory all the SAP applications running in a landscape and to determine the deployment mode (either 2-tier or 3-tier), versions, patches, sizes, churn rates, and disk persistence requirements.</span></span>

![部署模式](./media/site-recovery-sap/sap-typical-deployment.png)

<span data-ttu-id="70732-140">SAP 資料庫持續層應透過原生 DBMS 工具保護，例如 SQL Server AlwaysOn、Oracle DataGuard 或 HANA System Replication。</span><span class="sxs-lookup"><span data-stu-id="70732-140">The SAP Database persistence layer should be protected via the native DBMS tools such as SQL Server AlwaysOn, Oracle DataGuard, or HANA System Replication.</span></span> <span data-ttu-id="70732-141">用戶端層也不受 Azure Site Recovery 保護，但務必考量會影響此層級的主題，例如 DNS 傳播延遲、安全性和 DR 資料中心的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="70732-141">The client layer is also not protected by Azure Site Recovery, but it is important to consider topics that impact this layer such as DNS Propagation delay, security and remote access to the DR datacenter.</span></span>

<span data-ttu-id="70732-142">Azure Site Recovery 是應用程式層的建議解決方案 (包括 (A)SCS)。</span><span class="sxs-lookup"><span data-stu-id="70732-142">Azure Site Recovery is the recommended solution for the application layer, including (A)SCS.</span></span> <span data-ttu-id="70732-143">其他應用程式 (例如非 NetWeaver SAP 應用程式和非 SAP 應用程式) 形成整體 SAP 部署環境的一部分，也應該使用 Azure Site Recovery 保護。</span><span class="sxs-lookup"><span data-stu-id="70732-143">Other applications such as non-NetWeaver SAP applications and non-SAP applications form part of the overall SAP deployment environment and should also be protected with Azure Site Recovery.</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="70732-144">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="70732-144">Replicate virtual machines</span></span>
<span data-ttu-id="70732-145">請依照[本指引](azure-to-azure-walkthrough-enable-replication.md)，開始將所有 SAP 應用程式虛擬機器複寫至 Azure DR 資料中心。</span><span class="sxs-lookup"><span data-stu-id="70732-145">Follow [this guidance](azure-to-azure-walkthrough-enable-replication.md) to start replicating all the SAP application virtual machines to the Azure DR datacenter.</span></span>

<span data-ttu-id="70732-146">如果您使用靜態 IP，您可以在 [計算和網路] 設定的 [網路介面卡] 區段中指定您希望虛擬機器採用的 IP。</span><span class="sxs-lookup"><span data-stu-id="70732-146">If you are using a static IP, you can specify the IP that you want the virtual machine to take in the Network interface cards section in Compute and Network settings.</span></span>

![目標 IP](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="70732-148">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="70732-148">Creating a recovery plan</span></span>
<span data-ttu-id="70732-149">復原計劃可讓您在多層式應用程式中排序各層的容錯移轉，因此可維護應用程式一致性。</span><span class="sxs-lookup"><span data-stu-id="70732-149">A recovery plan allows sequencing the failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="70732-150">建立多層式 web 應用程式的復原計畫時，請遵循[此處](site-recovery-create-recovery-plans.md)描述的步驟。</span><span class="sxs-lookup"><span data-stu-id="70732-150">Follow the steps described [here](site-recovery-create-recovery-plans.md) while creating a recovery plan for a multi-tier web application.</span></span>

### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="70732-151">將指令碼新增至復原計畫</span><span class="sxs-lookup"><span data-stu-id="70732-151">Adding scripts to the recovery plan</span></span>
<span data-ttu-id="70732-152">您可能需要在容錯移轉/測試容錯移轉後，於 Azure 虛擬機器上執行某些作業，讓您的應用程式正常運作。</span><span class="sxs-lookup"><span data-stu-id="70732-152">You may need to do some operations on the Azure virtual machines post failover/test failover for your applications to function correctly.</span></span> <span data-ttu-id="70732-153">您可以自動執行容錯移轉後置作業，例如更新 DNS 項目，以及變更網站繫結和連線 (如[本文](site-recovery-create-recovery-plans.md#add-scripts)所述在復原方案中新增對應的指令碼)。</span><span class="sxs-lookup"><span data-stu-id="70732-153">You can automate the post failover operation such as updating DNS entry, and changing bindings and connections, by adding corresponding scripts in the recovery plan as described in [this article](site-recovery-create-recovery-plans.md#add-scripts).</span></span>

### <a name="dns-update"></a><span data-ttu-id="70732-154">DNS 更新</span><span class="sxs-lookup"><span data-stu-id="70732-154">DNS update</span></span>
<span data-ttu-id="70732-155">如果已設定動態 DNS 更新的 DNS，則虛擬機器通常會在啟動之後使用新的 IP 更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="70732-155">If the DNS is configured for dynamic DNS update, then virtual machines usually update the DNS with the new IP once they start.</span></span> <span data-ttu-id="70732-156">如果您想要使用虛擬機器的新 IP 新增更新 DNS 的明確步驟，則請新增此[指令碼來更新 DNS 中的 IP](https://aka.ms/asr-dns-update) 做為復原方案群組上的後置動作。</span><span class="sxs-lookup"><span data-stu-id="70732-156">If you want to add an explicit step to update DNS with the new IPs of the virtual machines then add this [script to update IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

## <a name="example-azure-to-azure-deployment"></a><span data-ttu-id="70732-157">Azure 對 Azure 部署範例</span><span class="sxs-lookup"><span data-stu-id="70732-157">Example Azure-to-Azure deployment</span></span>
<span data-ttu-id="70732-158">下圖說明 Azure Site Recovery Azure 對 Azure DR 案例：</span><span class="sxs-lookup"><span data-stu-id="70732-158">In the diagram below the Azure Site Recovery Azure-to-Azure DR scenario is depicted:</span></span>
* <span data-ttu-id="70732-159">主要資料中心位於新加坡 (Azure 南東亞洲)，而在 DR 資料中心位於香港特別行政區 (Azure 東亞)。</span><span class="sxs-lookup"><span data-stu-id="70732-159">The Primary Datacenter is in Singapore (Azure South-East Asia) and the DR datacenter is Hong Kong (Azure East Asia).</span></span>  <span data-ttu-id="70732-160">在此案例中，擁有兩部在新加坡以同步模式執行 SQL Server AlwaysOn 的 VM，即可提供本機高可用性。</span><span class="sxs-lookup"><span data-stu-id="70732-160">In this scenario, local High Availability is provided by having two VMs running SQL Server AlwaysOn in Synchronous mode in Singapore.</span></span>
* <span data-ttu-id="70732-161">檔案共用 ASCS 可用來為 SAP 單一失敗點提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="70732-161">The File Share ASCS can be used to provide HA for the SAP single points of failure.</span></span> <span data-ttu-id="70732-162">檔案共用 ASCS 不需要叢集共用磁碟，而且不需要 SIOS 等應用程式。</span><span class="sxs-lookup"><span data-stu-id="70732-162">File Share ASCS does not require a cluster shared disk, and applications such as SIOS are not required.</span></span>
* <span data-ttu-id="70732-163">DBMS 層的 DR 保護是利用非同步複寫達成。</span><span class="sxs-lookup"><span data-stu-id="70732-163">DR protection for the DBMS layer is achieved using Asynchronous replication.</span></span>
* <span data-ttu-id="70732-164">此案例顯示「對稱式 DR」，該詞彙用來描述屬於確切生產複本的 DR 解決方案，因此 DR SQL Server 解決方案可擁有本機高可用性。</span><span class="sxs-lookup"><span data-stu-id="70732-164">This scenario shows “symmetrical DR” – a term used to describe a DR solution that is an exact replica of production, therefore the DR SQL Server solution has local High Availability.</span></span> <span data-ttu-id="70732-165">資料庫層不強制使用對稱式 DR，而且許多客戶會利用雲端部署的彈性，在 DR 事件之後快速建置本機高可用性節點。</span><span class="sxs-lookup"><span data-stu-id="70732-165">The use of symmetrical DR is not mandatory for the Database layer, and many customers leverage the flexibility of cloud deployments to build a local High Availability Node quickly after a DR event.</span></span>
* <span data-ttu-id="70732-166">本圖說明 Azure Site Recovery 所複寫的 SAP NetWeaver ASCS 和應用程式伺服器層。</span><span class="sxs-lookup"><span data-stu-id="70732-166">The diagram depicts the SAP NetWeaver ASCS and Application server layer replicated by Azure Site Recovery.</span></span>

![複寫案例](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="70732-168">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="70732-168">Doing a test failover</span></span>
<span data-ttu-id="70732-169">請依照[本指引](azure-to-azure-walkthrough-test-failover.md)來執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="70732-169">Follow [this guidance](azure-to-azure-walkthrough-test-failover.md) to do a test failover.</span></span>

1.  <span data-ttu-id="70732-170">請移至 Azure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="70732-170">Go to Azure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="70732-171">按一下為 SAP 應用程式建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="70732-171">Click on the recovery plan created for SAP applications(s).</span></span>
3.  <span data-ttu-id="70732-172">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="70732-172">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="70732-173">選取復原點和 Azure 虛擬網路來開始測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="70732-173">Select recovery point and Azure virtual network to start the test failover process.</span></span>
5.  <span data-ttu-id="70732-174">次要環境啟動後，您就可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="70732-174">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="70732-175">完成驗證後，按一下 [清除測試容錯移轉] 以清除容錯移轉環境。</span><span class="sxs-lookup"><span data-stu-id="70732-175">Once the validations are complete, click on ‘Cleanup test failover’ and to clean the failover environment.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="70732-176">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="70732-176">Doing a failover</span></span>
<span data-ttu-id="70732-177">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="70732-177">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="70732-178">請移至 Azure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="70732-178">Go to Azure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="70732-179">按一下為 SAP 應用程式建立的復原方案。</span><span class="sxs-lookup"><span data-stu-id="70732-179">Click on the recovery plan created for SAP application(s).</span></span>
3.  <span data-ttu-id="70732-180">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="70732-180">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="70732-181">選取復原點以啟動容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="70732-181">Select recovery point to start the failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70732-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70732-182">Next steps</span></span>
<span data-ttu-id="70732-183">請參閱[本白皮書](http://aka.ms/asr-sap)，了解如何使用 Azure Site Recovery 為 SAP NetWeaver 部署建置災害復原解決方案。</span><span class="sxs-lookup"><span data-stu-id="70732-183">Learn more about building a disaster recovery solution for SAP NetWeaver deployments using Azure Site Recovery in [this whitepaper](http://aka.ms/asr-sap).</span></span> <span data-ttu-id="70732-184">本白皮書也會討論不同 SAP 架構的建議，列出支援 Azure 上的 SAP 的應用程式和 VM 類型，並說明災害復原解決方案可行的測試方案。</span><span class="sxs-lookup"><span data-stu-id="70732-184">The whitepaper also discusses recommendations for different SAP architectures, lists supported applications and VM types for SAP on Azure, and describes possible testing plans for your disaster recovery solution.</span></span>

<span data-ttu-id="70732-185">深入了解如何使用 Site Recovery [複寫其他工作負載](site-recovery-workload.md)。</span><span class="sxs-lookup"><span data-stu-id="70732-185">Learn more about [replicating other workloads](site-recovery-workload.md) using Site Recovery.</span></span>
