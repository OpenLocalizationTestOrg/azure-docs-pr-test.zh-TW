---
title: "使用 Azure Site Recovery 的多層式 Citrix XenDesktop 和 XenApp 部署 aaaReplicate |Microsoft 文件"
description: "本文說明如何 tooprotect 和復原 Citrix XenDesktop 和 XenApp 部署使用 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="2e937-103">使用 Azure Site Recovery 複寫多層式 Citrix XenApp 和 XenDesktop 部署</span><span class="sxs-lookup"><span data-stu-id="2e937-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="2e937-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2e937-104">Overview</span></span>

<span data-ttu-id="2e937-105">Citrix XenDesktop 是身為 ondemand 服務 tooany 使用者，任何位置提供桌面與應用程式的桌面虛擬化解決方案。</span><span class="sxs-lookup"><span data-stu-id="2e937-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="2e937-106">FlexCast 傳遞技術，XenDesktop 可以快速且安全的方式傳遞應用程式和桌面 toousers。</span><span class="sxs-lookup"><span data-stu-id="2e937-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="2e937-107">現在，Citrix XenApp 不提供任何災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="2e937-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="2e937-108">理想的災害復原解決方案，應該上方複雜的應用程式架構允許 hello 周圍的復原方案的模型，而且也具有 hello 能力 tooadd 自訂步驟 toohandle 應用程式之間的對應因此提供的各層單鍵確定 hello 開頭 tooa 災害事件中擷取畫面方案降低 RTO。</span><span class="sxs-lookup"><span data-stu-id="2e937-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="2e937-109">對於為 Hyper-V 和 VMware vSphere 平台上的內部部署 Citrix XenApp 部署建置災害復原方案，本文提供逐步指引。</span><span class="sxs-lookup"><span data-stu-id="2e937-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="2e937-110">本文也說明如何 tooperform 測試容錯移轉 （災害復原訓練） 和非計劃的容錯移轉 tooAzure 使用復原計劃、 支援的 hello 組態和必要條件。</span><span class="sxs-lookup"><span data-stu-id="2e937-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2e937-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="2e937-111">Prerequisites</span></span>

<span data-ttu-id="2e937-112">開始之前，請確定您了解 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2e937-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="2e937-113">複寫虛擬機器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="2e937-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="2e937-114">如何太[設計與復原網路](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="2e937-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="2e937-115">執行測試容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="2e937-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="2e937-116">執行容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="2e937-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="2e937-117">如何太[複寫的網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="2e937-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="2e937-118">如何太[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="2e937-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="2e937-119">部署模式</span><span class="sxs-lookup"><span data-stu-id="2e937-119">Deployment patterns</span></span>

<span data-ttu-id="2e937-120">Citrix XenApp 和 XenDesktop 的伺服器陣列通常具有下列部署模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e937-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="2e937-121">**部署模式**</span><span class="sxs-lookup"><span data-stu-id="2e937-121">**Deployment pattern**</span></span>

<span data-ttu-id="2e937-122">AD DNS 伺服器、SQL 資料庫伺服器、Citrix 傳遞控制站、StoreFront 伺服器，XenApp Master (VDA)、Citrix XenApp 授權伺服器的 Citrix XenApp 和 XenDesktop 部署</span><span class="sxs-lookup"><span data-stu-id="2e937-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![部署模式 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="2e937-124">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="2e937-124">Site Recovery support</span></span>

<span data-ttu-id="2e937-125">Hello 本文的目的，在 VMware 虛擬機器的 Citrix 部署管理的 vSphere 6.0/System Center VMM 2012 R2 已使用的 toosetup DR。</span><span class="sxs-lookup"><span data-stu-id="2e937-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="2e937-126">來源與目標</span><span class="sxs-lookup"><span data-stu-id="2e937-126">Source and target</span></span>

<span data-ttu-id="2e937-127">**案例**</span><span class="sxs-lookup"><span data-stu-id="2e937-127">**Scenario**</span></span> | <span data-ttu-id="2e937-128">**tooa 次要站台**</span><span class="sxs-lookup"><span data-stu-id="2e937-128">**tooa secondary site**</span></span> | <span data-ttu-id="2e937-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="2e937-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="2e937-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="2e937-130">**Hyper-V**</span></span> | <span data-ttu-id="2e937-131">不在範圍中</span><span class="sxs-lookup"><span data-stu-id="2e937-131">Not in scope</span></span> | <span data-ttu-id="2e937-132">是</span><span class="sxs-lookup"><span data-stu-id="2e937-132">Yes</span></span>
<span data-ttu-id="2e937-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="2e937-133">**VMware**</span></span> | <span data-ttu-id="2e937-134">不在範圍中</span><span class="sxs-lookup"><span data-stu-id="2e937-134">Not in scope</span></span> | <span data-ttu-id="2e937-135">是</span><span class="sxs-lookup"><span data-stu-id="2e937-135">Yes</span></span>
<span data-ttu-id="2e937-136">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="2e937-136">**Physical server**</span></span> | <span data-ttu-id="2e937-137">不在範圍中</span><span class="sxs-lookup"><span data-stu-id="2e937-137">Not in scope</span></span> | <span data-ttu-id="2e937-138">是</span><span class="sxs-lookup"><span data-stu-id="2e937-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="2e937-139">版本</span><span class="sxs-lookup"><span data-stu-id="2e937-139">Versions</span></span>
<span data-ttu-id="2e937-140">客戶可以部署 XenApp 元件成為 Hyper-V 或 VMware 上執行的虛擬機器，或成為實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="2e937-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="2e937-141">Azure Site Recovery 保護這兩個實體和虛擬部署 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="2e937-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="2e937-142">因為 XenApp 7.7 或更新版本支援在 Azure 中，只使用這些版本部署可以容錯移轉 tooAzure 嚴重損壞修復或移轉。</span><span class="sxs-lookup"><span data-stu-id="2e937-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="2e937-143">請注意的事項 tookeep</span><span class="sxs-lookup"><span data-stu-id="2e937-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="2e937-144">保護與復原支援內部部署使用 Server OS 機器 toodeliver XenApp 已發佈應用程式和 XenApp 發佈的桌面。</span><span class="sxs-lookup"><span data-stu-id="2e937-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="2e937-145">不支援保護和復原的內部部署用戶端虛擬桌面，包括 Windows 10 中，使用桌面 OS 機器 toodeliver 桌面 VDI。</span><span class="sxs-lookup"><span data-stu-id="2e937-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="2e937-146">這是因為 ASR 並不支援的電腦桌面 OS'es hello 復原。</span><span class="sxs-lookup"><span data-stu-id="2e937-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="2e937-147">此外，某些用戶端虛擬桌面 (例如</span><span class="sxs-lookup"><span data-stu-id="2e937-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="2e937-148">Windows 7) 在 Azure 中尚不支援授權。</span><span class="sxs-lookup"><span data-stu-id="2e937-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="2e937-149">[深入了解](https://azure.microsoft.com/pricing/licensing-faq/)如何在 Azure 中進行用戶端/伺服器桌面的授權。</span><span class="sxs-lookup"><span data-stu-id="2e937-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="2e937-150">Azure Site Recovery 無法複寫和保護現有的內部部署 MCS 或 PV 複製品。</span><span class="sxs-lookup"><span data-stu-id="2e937-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="2e937-151">您需要 toorecreate 使用從傳遞控制站的 Azure RM 佈建這些複製品。</span><span class="sxs-lookup"><span data-stu-id="2e937-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="2e937-152">無法使用 Azure Site Recovery 保護 NetScaler，因為 NetScaler 是以 FreeBSD 為基礎，而且 Azure Site Recovery 不支援 FreeBSD 作業系統的保護。</span><span class="sxs-lookup"><span data-stu-id="2e937-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="2e937-153">您會需要 toodeploy，並在容錯移轉 tooAzure 之後設定新 NetScaler 裝置從 Azure 市場的位置。</span><span class="sxs-lookup"><span data-stu-id="2e937-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="2e937-154">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2e937-154">Replicating virtual machines</span></span>

<span data-ttu-id="2e937-155">下列元件的 hello Citrix XenApp 部署的 hello 需要受保護的 toobe tooenable 複寫和復原。</span><span class="sxs-lookup"><span data-stu-id="2e937-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="2e937-156">AD DNS 伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="2e937-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="2e937-157">SQL 資料庫伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="2e937-157">Protection of SQL database server</span></span>
* <span data-ttu-id="2e937-158">Citrix 傳遞控制站的保護</span><span class="sxs-lookup"><span data-stu-id="2e937-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="2e937-159">StoreFront 伺服器的保護。</span><span class="sxs-lookup"><span data-stu-id="2e937-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="2e937-160">XenApp Master (VDA) 的保護</span><span class="sxs-lookup"><span data-stu-id="2e937-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="2e937-161">Citrix XenApp 授權伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="2e937-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="2e937-162">**AD DNS 伺服器複寫**</span><span class="sxs-lookup"><span data-stu-id="2e937-162">**AD DNS server replication**</span></span>

<span data-ttu-id="2e937-163">請參閱太[保護 Active Directory 和 DNS 與 Azure Site Recovery](site-recovery-active-directory.md)上複寫，以及在 Azure 中設定的網域控制站的指引。</span><span class="sxs-lookup"><span data-stu-id="2e937-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="2e937-164">**SQL Database 伺服器複寫**</span><span class="sxs-lookup"><span data-stu-id="2e937-164">**SQL database Server replication**</span></span>

<span data-ttu-id="2e937-165">請參閱太[以 SQL Server 嚴重損壞修復及 Azure Site Recovery 保護 SQL Server](site-recovery-sql.md)如需詳細指引技術 hello 建議的選項，來保護 SQL server。</span><span class="sxs-lookup"><span data-stu-id="2e937-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="2e937-166">請遵循[本指南](site-recovery-vmware-to-azure.md)toostart 複寫 hello 其他元件的虛擬機器 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="2e937-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![XenApp 元件的保護](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="2e937-168">**計算和網路設定**</span><span class="sxs-lookup"><span data-stu-id="2e937-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="2e937-169">Hello 機器受到保護之後 （狀態顯示為 「 受保護 」 複寫的項目 下，） hello 運算和網路設定需要 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="2e937-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="2e937-170">在計算與網路 > 計算屬性，您可以指定 hello Azure VM 的名稱和目標大小。</span><span class="sxs-lookup"><span data-stu-id="2e937-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="2e937-171">如果您需要，修改 hello 名稱 toocomply Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="2e937-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="2e937-172">您也可以檢視和新增 hello 目標網路、 子網路及指派 toohello Azure VM 的 IP 位址資訊。</span><span class="sxs-lookup"><span data-stu-id="2e937-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="2e937-173">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2e937-173">Note hello following:</span></span>

* <span data-ttu-id="2e937-174">您可以設定 hello 目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2e937-174">You can set hello target IP address.</span></span> <span data-ttu-id="2e937-175">如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="2e937-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="2e937-176">如果您將無法使用在容錯移轉的位址，將無法運作 hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="2e937-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="2e937-177">相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。</span><span class="sxs-lookup"><span data-stu-id="2e937-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="2e937-178">Hello AD/DNS 伺服器，保留 hello 內部位址可讓您指定的 hello 相同位址做為 hello hello Azure 虛擬網路的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2e937-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="2e937-179">hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：</span><span class="sxs-lookup"><span data-stu-id="2e937-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="2e937-180">如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。</span><span class="sxs-lookup"><span data-stu-id="2e937-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="2e937-181">如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="2e937-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="2e937-182">例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="2e937-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="2e937-183">如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。</span><span class="sxs-lookup"><span data-stu-id="2e937-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="2e937-184">如果 hello 虛擬機器具有多張網路介面卡將所有連線 toohello 相同的網路。</span><span class="sxs-lookup"><span data-stu-id="2e937-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="2e937-185">如果 hello 虛擬機器有多張網路介面卡，然後 hello hello 清單所示的第一個會變成 hello Azure 虛擬機器中的 hello 預設網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="2e937-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="2e937-186">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="2e937-186">Creating a recovery plan</span></span>

<span data-ttu-id="2e937-187">啟用 hello XenApp 元件 Vm 複寫之後，hello 下一個步驟是 toocreate 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="2e937-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="2e937-188">復原計畫群組會將有類似需求的虛擬機器分組，以便進行容錯移轉和復原。</span><span class="sxs-lookup"><span data-stu-id="2e937-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="2e937-189">**步驟 toocreate 復原計劃**</span><span class="sxs-lookup"><span data-stu-id="2e937-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="2e937-190">Hello XenApp 元件中加入虛擬機器復原計劃的 hello。</span><span class="sxs-lookup"><span data-stu-id="2e937-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="2e937-191">按一下 [復原計畫] -> [+ 復原計畫]。</span><span class="sxs-lookup"><span data-stu-id="2e937-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="2e937-192">提供直覺式 hello 復原計劃的名稱。</span><span class="sxs-lookup"><span data-stu-id="2e937-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="2e937-193">對於 VMware 虛擬機器：選取 VMware 處理序伺服器做為來源，選取 Microsoft Azure 做為目標，並選取資源管理員做為部署模型，然後按一下 [選取項目]。</span><span class="sxs-lookup"><span data-stu-id="2e937-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="2e937-194">HYPER-V 虛擬機器： 選取來源 VMM 伺服器，以目標為 Microsoft Azure，以及部署模型與資源管理員和按一下選取的項目，然後選取 hello XenApp 部署 Vm。</span><span class="sxs-lookup"><span data-stu-id="2e937-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="2e937-195">新增虛擬機器 toofailover 群組</span><span class="sxs-lookup"><span data-stu-id="2e937-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="2e937-196">復原計劃可以是特定的啟動順序、 指令碼或手動動作的自訂的 tooadd 容錯移轉群組。</span><span class="sxs-lookup"><span data-stu-id="2e937-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="2e937-197">下列群組的 hello 需要 toobe 加入的 toohello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="2e937-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="2e937-198">容錯移轉群組 1：AD DNS</span><span class="sxs-lookup"><span data-stu-id="2e937-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="2e937-199">容錯移轉群組 2：SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="2e937-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="2e937-200">容錯移轉群組 3：VDA Master Image VM</span><span class="sxs-lookup"><span data-stu-id="2e937-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="2e937-201">容錯移轉群組 4：傳遞控制站和 StoreFront 伺服器 VM</span><span class="sxs-lookup"><span data-stu-id="2e937-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="2e937-202">加入指令碼 toohello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="2e937-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="2e937-203">可以在復原計畫中的特定群組之前或之後執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="2e937-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="2e937-204">也可以在容錯移轉期間加入並執行手動動作。</span><span class="sxs-lookup"><span data-stu-id="2e937-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="2e937-205">hello 自訂的復原計劃看起來類似下面的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e937-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="2e937-206">容錯移轉群組 1：AD DNS</span><span class="sxs-lookup"><span data-stu-id="2e937-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="2e937-207">容錯移轉群組 2：SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="2e937-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="2e937-208">容錯移轉群組 3：VDA Master Image VM</span><span class="sxs-lookup"><span data-stu-id="2e937-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="2e937-209">步驟 4、 6 和 7 包含手動 」 或 「 指令碼動作都適用 tooonly 內部 XenApp > MCS/PV 目錄的環境。</span><span class="sxs-lookup"><span data-stu-id="2e937-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="2e937-210">手動或指令碼動作的群組 3： 關閉主要 VDA VM hello Master VDA VM 容錯移轉 tooAzure 時將會處於執行中狀態。</span><span class="sxs-lookup"><span data-stu-id="2e937-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="2e937-211">toocreate 新 MCS 的目錄，使用 Azure ARM 裝載，hello 主機 VDA VM 是處於 已停止 (de 配置) 的必要的 toobe 狀態。</span><span class="sxs-lookup"><span data-stu-id="2e937-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="2e937-212">關機 hello VM 從 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2e937-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="2e937-213">容錯移轉群組 4：傳遞控制站和 StoreFront 伺服器 VM</span><span class="sxs-lookup"><span data-stu-id="2e937-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="2e937-214">群組 3 手動或指令碼動作 1：</span><span class="sxs-lookup"><span data-stu-id="2e937-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="2e937-215">***新增 Azure RM 主機連線***</span><span class="sxs-lookup"><span data-stu-id="2e937-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="2e937-216">在傳遞控制站機器 tooprovision 中新 MCS 類別目錄，在 Azure 中的建立 Azure ARM 主機連接。</span><span class="sxs-lookup"><span data-stu-id="2e937-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="2e937-217">在此說明，請遵循 hello 步驟[文章](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/)。</span><span class="sxs-lookup"><span data-stu-id="2e937-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="2e937-218">群組 3 手動或指令碼動作 2：</span><span class="sxs-lookup"><span data-stu-id="2e937-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="2e937-219">***在 Azure 中重新建立 MCS 目錄***</span><span class="sxs-lookup"><span data-stu-id="2e937-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="2e937-220">hello 現有 MCS 或 PV 複製品 hello 主要站台上的將不會複寫的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="2e937-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="2e937-221">您必須使用 hello 這些複製品會在從傳遞控制站複寫 「 主要 VDA 和佈建的 Azure ARM toorecreate。在此說明，請遵循 hello 步驟[文章](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/)toocreate MCS 目錄在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="2e937-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![XenApp 元件的復原計畫](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="2e937-223">您可以使用指令碼，於[位置](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts)tooupdate hello DNS 以容錯移轉的 hello 的新 Ip hello > 視虛擬機器或 tooattach hello 上的負載平衡器無法容錯移轉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2e937-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="2e937-224">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="2e937-224">Doing a test failover</span></span>

<span data-ttu-id="2e937-225">請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="2e937-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![復原方案](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="2e937-227">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="2e937-227">Doing a failover</span></span>

<span data-ttu-id="2e937-228">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="2e937-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e937-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e937-229">Next steps</span></span>

<span data-ttu-id="2e937-230">您可以在這份白皮書中[深入了解](https://aka.ms/citrix-xenapp-xendesktop-with-asr)複寫 Citrix XenApp 和 XenDesktop 部署。</span><span class="sxs-lookup"><span data-stu-id="2e937-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="2e937-231">查看 hello 指引太[複寫其他應用程式](site-recovery-workload.md)使用站台復原。</span><span class="sxs-lookup"><span data-stu-id="2e937-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
