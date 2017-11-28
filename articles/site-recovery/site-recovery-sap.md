---
title: "aaaProtect 使用 Azure Site Recovery 的多層式 SAP NetWeaver 應用程式部署 |Microsoft 文件"
description: "本文說明如何 tooprotect SAP NetWeaver 應用程式部署使用 Azure Site Recovery"
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
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a><span data-ttu-id="a5f21-103">使用 Azure Site Recovery 保護多層式 SAP NetWeaver 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="a5f21-103">Protect a multi-tier SAP NetWeaver application deployment using Azure Site Recovery</span></span>

<span data-ttu-id="a5f21-104">大部分的大型與中型 SAP 部署都有某種形式的災害復原方案。</span><span class="sxs-lookup"><span data-stu-id="a5f21-104">Most large and medium-sized SAP deployments have some form of Disaster Recovery solution.</span></span>  <span data-ttu-id="a5f21-105">更多的核心商務處理程序是移動 （如 SAP) tooapplications 增加 hello 重要性強固和可測試的災害復原解決方案。</span><span class="sxs-lookup"><span data-stu-id="a5f21-105">hello importance of robust and testable Disaster Recovery solutions has increased as more core business processes are moved tooapplications such as SAP.</span></span>  <span data-ttu-id="a5f21-106">Azure Site Recovery 已完善測試而且整合的 SAP 應用程式，而且超過 hello 功能大部分在內部部署災害復原方案，在降低擁有權總成本 (TCO) 比競爭解決方案。</span><span class="sxs-lookup"><span data-stu-id="a5f21-106">Azure Site Recovery has been tested and integrated with SAP applications, and exceeds hello capabilities of most on-premises Disaster Recovery solutions, at a lower total cost of ownership (TCO) than competing solutions.</span></span>
<span data-ttu-id="a5f21-107">使用 Azure Site Recovery，您可以：</span><span class="sxs-lookup"><span data-stu-id="a5f21-107">With Azure Site Recovery you can:</span></span>
* <span data-ttu-id="a5f21-108">啟用 SAP NetWeaver 和非 NetWeaver 實際執行應用程式內部，藉由複寫元件 tooAzure 的保護。</span><span class="sxs-lookup"><span data-stu-id="a5f21-108">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running on-premises, by replicating components tooAzure.</span></span>
* <span data-ttu-id="a5f21-109">啟用保護，藉由複寫元件 tooanother Azure 資料中心內執行 Azure 的 SAP NetWeaver 和非 NetWeaver 生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5f21-109">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running Azure, by replicating components tooanother Azure datacenter.</span></span>
* <span data-ttu-id="a5f21-110">使用站台復原 toomigrate 您 SAP 部署 tooAzure 簡化雲端移轉。</span><span class="sxs-lookup"><span data-stu-id="a5f21-110">Simplify cloud migration, by using Site Recovery toomigrate your SAP deployment tooAzure.</span></span>
* <span data-ttu-id="a5f21-111">藉由建立隨選生產複本來測試 SAP 應用程式，簡化 SAP 專案升級、測試和原型設計。</span><span class="sxs-lookup"><span data-stu-id="a5f21-111">Simplify SAP project upgrades, testing, and prototyping, by creating a production clone on-demand for testing SAP applications.</span></span>

<span data-ttu-id="a5f21-112">本文說明如何 tooprotect SAP NetWeaver 應用程式部署使用[Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a5f21-112">This article describes how tooprotect SAP NetWeaver application deployments using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="a5f21-113">本文章涵蓋 hello 保護藉由複寫 tooanother 使用 Azure Site Recovery，hello 支援案例和組態，Azure 資料中心的三層式 SAP NetWeaver 部署在 Azure 上的最佳作法和如何 tooperform 容錯移轉，同時測試實際的容錯移轉和容錯移轉 （災害復原演練）。</span><span class="sxs-lookup"><span data-stu-id="a5f21-113">This article covers hello best practices for protecting a three-tier SAP NetWeaver deployment on Azure by replicating tooanother Azure datacenter using Azure Site Recovery, hello supported scenarios and configurations, and how tooperform failovers, both test failovers (disaster recovery drills) and actual failovers.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a5f21-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="a5f21-114">Prerequisites</span></span>
<span data-ttu-id="a5f21-115">開始之前，請確定您了解 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="a5f21-115">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="a5f21-116">複寫虛擬機器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a5f21-116">Replicating a virtual machine tooAzure</span></span>](azure-to-azure-walkthrough-enable-replication.md)
2. <span data-ttu-id="a5f21-117">如何太[設計與復原網路](site-recovery-azure-to-azure-networking-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="a5f21-117">How too[design a recovery network](site-recovery-azure-to-azure-networking-guidance.md)</span></span>
3. [<span data-ttu-id="a5f21-118">執行測試容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a5f21-118">Doing a test failover tooAzure</span></span>](azure-to-azure-walkthrough-test-failover.md)
4. [<span data-ttu-id="a5f21-119">執行容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a5f21-119">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="a5f21-120">如何太[複寫的網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="a5f21-120">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="a5f21-121">如何太[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="a5f21-121">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="a5f21-122">支援的案例</span><span class="sxs-lookup"><span data-stu-id="a5f21-122">Supported scenarios</span></span>
<span data-ttu-id="a5f21-123">使用 Azure Site Recovery 中，您可以實作下列案例的 hello 災害復原解決方案：</span><span class="sxs-lookup"><span data-stu-id="a5f21-123">With Azure Site Recovery you can implement a disaster recovery solution for hello following scenarios:</span></span>
* <span data-ttu-id="a5f21-124">架構在一個 Azure 資料中心複寫 tooanother (Azure-Azure DR) 的 Azure 資料中心執行的 SAP 系統[這裡](https://aka.ms/asr-a2a-architecture)。</span><span class="sxs-lookup"><span data-stu-id="a5f21-124">SAP systems running in one Azure datacenter replicating tooanother Azure datacenter (Azure-to-Azure DR), as architected [here](https://aka.ms/asr-a2a-architecture).</span></span>
* <span data-ttu-id="a5f21-125">執行 VMWare （或實體） 的伺服器上的 SAP 系統的內部複寫 tooa DR 網站，在 Azure 資料中心 (VMware-Azure DR)，這需要一些額外的元件，因為架構[這裡](https://aka.ms/asr-v2a-architecture)。</span><span class="sxs-lookup"><span data-stu-id="a5f21-125">SAP systems running on VMWare (or Physical) servers on-premises replicating tooa DR site in an Azure datacenter (VMware-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-v2a-architecture).</span></span>
* <span data-ttu-id="a5f21-126">在 HYPER-V 上執行的 SAP 系統的內部複寫 tooa DR 網站，在 Azure 資料中心 (Hyper-v-V-至 Azure DR)，這需要一些額外的元件，因為架構[這裡](https://aka.ms/asr-h2a-architecture)。</span><span class="sxs-lookup"><span data-stu-id="a5f21-126">SAP systems running on Hyper-V on-premises replicating tooa DR site in an Azure datacenter (Hyper-V-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-h2a-architecture).</span></span>

<span data-ttu-id="a5f21-127">這份文件會使用 hello 第一個案例-Azure-Azure DR-toodemonstrate Azure Site Recovery 的 SAP 災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="a5f21-127">This document uses hello first case - Azure-to-Azure DR - toodemonstrate Azure Site Recovery's SAP disaster recovery capabilities.</span></span> <span data-ttu-id="a5f21-128">Azure Site Recovery 的複寫與應用程式無關，是針對其他情況下的預期的 toohold hello 所述的程序。</span><span class="sxs-lookup"><span data-stu-id="a5f21-128">As Azure Site Recovery replication is application agnostic, hello process described is expected toohold for other scenarios as well.</span></span>

### <a name="required-foundation-services"></a><span data-ttu-id="a5f21-129">必要的基礎服務</span><span class="sxs-lookup"><span data-stu-id="a5f21-129">Required foundation services</span></span>
<span data-ttu-id="a5f21-130">此文件案例中所有已部署以下列 foundation 服務部署的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5f21-130">This documentation scenario all been deployed with hello following foundation services deployed:</span></span>
* <span data-ttu-id="a5f21-131">ExpressRoute 或站對站虛擬私人網路 (VPN)</span><span class="sxs-lookup"><span data-stu-id="a5f21-131">ExpressRoute or Site-to-Site Virtual Private Network (VPN)</span></span>
* <span data-ttu-id="a5f21-132">至少有一個 Active Directory 網域控制站和 DNS 伺服器在 Azure 中執行</span><span class="sxs-lookup"><span data-stu-id="a5f21-132">At least one Active Directory Domain Controller and DNS server running in Azure</span></span>

<span data-ttu-id="a5f21-133">建議您使用上述 hello 基礎結構會建立先前 toodeploying Azure Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="a5f21-133">It is recommended that hello infrastructure above is established prior toodeploying Azure Site Recovery.</span></span>


## <a name="typical-sap-application-deployment"></a><span data-ttu-id="a5f21-134">典型 SAP 應用程式部署</span><span class="sxs-lookup"><span data-stu-id="a5f21-134">Typical SAP application deployment</span></span>
<span data-ttu-id="a5f21-135">大型的 SAP 客戶通常部署之間 6 too20 個別的 SAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5f21-135">Large SAP customers usually deploy between 6 too20 individual SAP applications.</span></span>  <span data-ttu-id="a5f21-136">這些應用程式的大部分取決於 hello SAP NetWeaver ABAP 或 Java 引擎。</span><span class="sxs-lookup"><span data-stu-id="a5f21-136">Most of these applications are based on hello SAP NetWeaver ABAP or Java engines.</span></span>  <span data-ttu-id="a5f21-137">這些核心 NetWeaver 應用程式 (有些通常是非 SAP 應用程式) 是由許多小型特定非 NetWeaver SAP 獨立引擎支援。</span><span class="sxs-lookup"><span data-stu-id="a5f21-137">Supporting these core NetWeaver applications are many smaller specific non-NetWeaver SAP standalone engines and typically some non-SAP applications.</span></span>  

<span data-ttu-id="a5f21-138">它是關鍵 tooinventory hello SAP 執行所有應用程式中的橫向與 toodetermine hello 部署模式 （2 層或 3 層）、 版本、 修補程式，大小、 變換率，以及磁碟持續性需求。</span><span class="sxs-lookup"><span data-stu-id="a5f21-138">It is critical tooinventory all hello SAP applications running in a landscape and toodetermine hello deployment mode (either 2-tier or 3-tier), versions, patches, sizes, churn rates, and disk persistence requirements.</span></span>

![部署模式](./media/site-recovery-sap/sap-typical-deployment.png)

<span data-ttu-id="a5f21-140">hello SAP 資料庫保存層應該保護透過 hello 原生 DBMS 工具，例如 SQL Server AlwaysOn、 Oracle DataGuard 或 HANA 系統複寫。</span><span class="sxs-lookup"><span data-stu-id="a5f21-140">hello SAP Database persistence layer should be protected via hello native DBMS tools such as SQL Server AlwaysOn, Oracle DataGuard, or HANA System Replication.</span></span> <span data-ttu-id="a5f21-141">hello 用戶端層也不受 Azure Site Recovery 中，但會影響此圖層，例如 DNS 傳播延遲、 安全性和遠端存取 toohello DR 資料中心的重要 tooconsider 主題。</span><span class="sxs-lookup"><span data-stu-id="a5f21-141">hello client layer is also not protected by Azure Site Recovery, but it is important tooconsider topics that impact this layer such as DNS Propagation delay, security and remote access toohello DR datacenter.</span></span>

<span data-ttu-id="a5f21-142">Azure Site Recovery 會為 hello 建議 hello 應用程式層，其中包括 (A) SCS 的方案。</span><span class="sxs-lookup"><span data-stu-id="a5f21-142">Azure Site Recovery is hello recommended solution for hello application layer, including (A)SCS.</span></span> <span data-ttu-id="a5f21-143">其他應用程式等非 NetWeaver SAP 應用程式和非 SAP 應用程式組成 hello 整體 SAP 部署環境，也應該與 Azure Site Recovery 保護。</span><span class="sxs-lookup"><span data-stu-id="a5f21-143">Other applications such as non-NetWeaver SAP applications and non-SAP applications form part of hello overall SAP deployment environment and should also be protected with Azure Site Recovery.</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="a5f21-144">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a5f21-144">Replicate virtual machines</span></span>
<span data-ttu-id="a5f21-145">請遵循[本指南](azure-to-azure-walkthrough-enable-replication.md)toostart 複寫所有 hello SAP 應用程式的虛擬機器 toohello Azure DR 資料中心。</span><span class="sxs-lookup"><span data-stu-id="a5f21-145">Follow [this guidance](azure-to-azure-walkthrough-enable-replication.md) toostart replicating all hello SAP application virtual machines toohello Azure DR datacenter.</span></span>

<span data-ttu-id="a5f21-146">如果您使用靜態 ip 位址，您可以指定您想 hello hello 運算和網路設定中網路介面卡區段中的虛擬機器 tootake hello IP。</span><span class="sxs-lookup"><span data-stu-id="a5f21-146">If you are using a static IP, you can specify hello IP that you want hello virtual machine tootake in hello Network interface cards section in Compute and Network settings.</span></span>

![目標 IP](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="a5f21-148">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="a5f21-148">Creating a recovery plan</span></span>
<span data-ttu-id="a5f21-149">復原計劃可讓您排序 hello 容錯移轉維護應用程式一致性是多層式應用程式，因此，在各層。</span><span class="sxs-lookup"><span data-stu-id="a5f21-149">A recovery plan allows sequencing hello failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="a5f21-150">請依照下列所述的 hello 步驟[這裡](site-recovery-create-recovery-plans.md)時建立多層式 web 應用程式的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="a5f21-150">Follow hello steps described [here](site-recovery-create-recovery-plans.md) while creating a recovery plan for a multi-tier web application.</span></span>

### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="a5f21-151">加入指令碼 toohello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="a5f21-151">Adding scripts toohello recovery plan</span></span>
<span data-ttu-id="a5f21-152">您可能需要 toodo hello Azure 虛擬機器後測試容錯移轉/容錯移轉的某些作業的應用程式 toofunction 正確。</span><span class="sxs-lookup"><span data-stu-id="a5f21-152">You may need toodo some operations on hello Azure virtual machines post failover/test failover for your applications toofunction correctly.</span></span> <span data-ttu-id="a5f21-153">您可以自動化 hello post 容錯移轉作業，例如更新 DNS 項目，以及變更繫結和連接，藉由新增 hello 復原計劃中的對應的指令碼中所述[本文](site-recovery-create-recovery-plans.md#add-scripts)。</span><span class="sxs-lookup"><span data-stu-id="a5f21-153">You can automate hello post failover operation such as updating DNS entry, and changing bindings and connections, by adding corresponding scripts in hello recovery plan as described in [this article](site-recovery-create-recovery-plans.md#add-scripts).</span></span>

### <a name="dns-update"></a><span data-ttu-id="a5f21-154">DNS 更新</span><span class="sxs-lookup"><span data-stu-id="a5f21-154">DNS update</span></span>
<span data-ttu-id="a5f21-155">如果通常 hello DNS 設定為動態 DNS 更新時，則虛擬機器更新 hello DNS hello 新 ip 之後啟動。</span><span class="sxs-lookup"><span data-stu-id="a5f21-155">If hello DNS is configured for dynamic DNS update, then virtual machines usually update hello DNS with hello new IP once they start.</span></span> <span data-ttu-id="a5f21-156">如果您想 tooadd 以 hello 明確步驟 tooupdate DNS 新 hello 虛擬機器的 Ip 再新增這[指令碼在 DNS 中的 tooupdate IP](https://aka.ms/asr-dns-update)作為復原計畫群組後動作。</span><span class="sxs-lookup"><span data-stu-id="a5f21-156">If you want tooadd an explicit step tooupdate DNS with hello new IPs of hello virtual machines then add this [script tooupdate IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

## <a name="example-azure-to-azure-deployment"></a><span data-ttu-id="a5f21-157">Azure 對 Azure 部署範例</span><span class="sxs-lookup"><span data-stu-id="a5f21-157">Example Azure-to-Azure deployment</span></span>
<span data-ttu-id="a5f21-158">Hello 圖 hello Azure Site Recovery Azure-Azure DR 案例中會說明：</span><span class="sxs-lookup"><span data-stu-id="a5f21-158">In hello diagram below hello Azure Site Recovery Azure-to-Azure DR scenario is depicted:</span></span>
* <span data-ttu-id="a5f21-159">主要資料中心是新加坡 （Azure 南東亞洲） 中的 hello 與 hello DR 資料中心是香港特別行政區 （Azure 東亞）。</span><span class="sxs-lookup"><span data-stu-id="a5f21-159">hello Primary Datacenter is in Singapore (Azure South-East Asia) and hello DR datacenter is Hong Kong (Azure East Asia).</span></span>  <span data-ttu-id="a5f21-160">在此案例中，擁有兩部在新加坡以同步模式執行 SQL Server AlwaysOn 的 VM，即可提供本機高可用性。</span><span class="sxs-lookup"><span data-stu-id="a5f21-160">In this scenario, local High Availability is provided by having two VMs running SQL Server AlwaysOn in Synchronous mode in Singapore.</span></span>
* <span data-ttu-id="a5f21-161">檔案共用 ASCS hello 可以是使用的 tooprovide HA hello SAP 單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="a5f21-161">hello File Share ASCS can be used tooprovide HA for hello SAP single points of failure.</span></span> <span data-ttu-id="a5f21-162">檔案共用 ASCS 不需要叢集共用磁碟，而且不需要 SIOS 等應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5f21-162">File Share ASCS does not require a cluster shared disk, and applications such as SIOS are not required.</span></span>
* <span data-ttu-id="a5f21-163">Hello DBMS 層的 DR 保護是利用非同步複寫來達成。</span><span class="sxs-lookup"><span data-stu-id="a5f21-163">DR protection for hello DBMS layer is achieved using Asynchronous replication.</span></span>
* <span data-ttu-id="a5f21-164">這個案例顯示 「 對稱 DR"– 使用的詞彙 toodescribe DR 方案中的實際執行的相同複本，因此 hello DR SQL Server 方案的本機高可用性。</span><span class="sxs-lookup"><span data-stu-id="a5f21-164">This scenario shows “symmetrical DR” – a term used toodescribe a DR solution that is an exact replica of production, therefore hello DR SQL Server solution has local High Availability.</span></span> <span data-ttu-id="a5f21-165">hello 對稱 DR 使用並非強制性的 hello 資料庫層級，而且許多客戶利用 hello 彈性的雲端部署 toobuild 本機的高可用性節點快速 DR 事件之後。</span><span class="sxs-lookup"><span data-stu-id="a5f21-165">hello use of symmetrical DR is not mandatory for hello Database layer, and many customers leverage hello flexibility of cloud deployments toobuild a local High Availability Node quickly after a DR event.</span></span>
* <span data-ttu-id="a5f21-166">hello 圖表描述 SAP NetWeaver ASCS hello 和複寫的 Azure Site Recovery 的應用程式伺服器層。</span><span class="sxs-lookup"><span data-stu-id="a5f21-166">hello diagram depicts hello SAP NetWeaver ASCS and Application server layer replicated by Azure Site Recovery.</span></span>

![複寫案例](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="a5f21-168">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="a5f21-168">Doing a test failover</span></span>
<span data-ttu-id="a5f21-169">請遵循[本指南](azure-to-azure-walkthrough-test-failover.md)toodo 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="a5f21-169">Follow [this guidance](azure-to-azure-walkthrough-test-failover.md) toodo a test failover.</span></span>

1.  <span data-ttu-id="a5f21-170">移 tooAzure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a5f21-170">Go tooAzure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="a5f21-171">按一下 hello 針對 SAP 應用程式 (s) 建立的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="a5f21-171">Click on hello recovery plan created for SAP applications(s).</span></span>
3.  <span data-ttu-id="a5f21-172">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="a5f21-172">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="a5f21-173">選取的復原點和 Azure 虛擬網路 toostart hello 測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="a5f21-173">Select recovery point and Azure virtual network toostart hello test failover process.</span></span>
5.  <span data-ttu-id="a5f21-174">一旦 hello 次要環境已啟動，您可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="a5f21-174">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="a5f21-175">Hello 驗證完成後，按一下 [清除測試容錯移轉]，並 tooclean hello 容錯移轉環境。</span><span class="sxs-lookup"><span data-stu-id="a5f21-175">Once hello validations are complete, click on ‘Cleanup test failover’ and tooclean hello failover environment.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="a5f21-176">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="a5f21-176">Doing a failover</span></span>
<span data-ttu-id="a5f21-177">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="a5f21-177">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="a5f21-178">移 tooAzure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a5f21-178">Go tooAzure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="a5f21-179">按一下 hello SAP 應用程式所建立的復原計畫。</span><span class="sxs-lookup"><span data-stu-id="a5f21-179">Click on hello recovery plan created for SAP application(s).</span></span>
3.  <span data-ttu-id="a5f21-180">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="a5f21-180">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="a5f21-181">選取的復原點 toostart hello 容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="a5f21-181">Select recovery point toostart hello failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5f21-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5f21-182">Next steps</span></span>
<span data-ttu-id="a5f21-183">請參閱[本白皮書](http://aka.ms/asr-sap)，了解如何使用 Azure Site Recovery 為 SAP NetWeaver 部署建置災害復原解決方案。</span><span class="sxs-lookup"><span data-stu-id="a5f21-183">Learn more about building a disaster recovery solution for SAP NetWeaver deployments using Azure Site Recovery in [this whitepaper](http://aka.ms/asr-sap).</span></span> <span data-ttu-id="a5f21-184">hello 技術白皮書也會討論不同 SAP 架構的建議，列出在 Azure 上 SAP 支援的應用程式和 VM 類型並描述可能的災害復原方案的測試計劃。</span><span class="sxs-lookup"><span data-stu-id="a5f21-184">hello whitepaper also discusses recommendations for different SAP architectures, lists supported applications and VM types for SAP on Azure, and describes possible testing plans for your disaster recovery solution.</span></span>

<span data-ttu-id="a5f21-185">深入了解如何使用 Site Recovery [複寫其他工作負載](site-recovery-workload.md)。</span><span class="sxs-lookup"><span data-stu-id="a5f21-185">Learn more about [replicating other workloads](site-recovery-workload.md) using Site Recovery.</span></span>
