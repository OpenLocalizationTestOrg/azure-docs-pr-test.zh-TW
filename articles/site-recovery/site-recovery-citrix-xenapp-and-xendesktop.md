---
title: "使用 Azure Site Recovery 複寫多層式 Citrix XenDesktop 和 XenApp 部署 | Microsoft Docs"
description: "本文說明如何使用 Azure Site Recovery 保護和復原 Citrix XenDesktop 和 XenApp 部署。"
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
ms.openlocfilehash: dc064352b1841ff346b705dc63186b12d79350b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="7278e-103">使用 Azure Site Recovery 複寫多層式 Citrix XenApp 和 XenDesktop 部署</span><span class="sxs-lookup"><span data-stu-id="7278e-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="7278e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7278e-104">Overview</span></span>

<span data-ttu-id="7278e-105">Citrix XenDesktop 是桌面虛擬化解決方案，能夠為任何地方的任何使用者提供桌面與應用程式的隨需服務。</span><span class="sxs-lookup"><span data-stu-id="7278e-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service to any user, anywhere.</span></span> <span data-ttu-id="7278e-106">藉由 FlexCast 傳遞技術，XenDesktop 能夠以快速且安全的方式為使用者傳遞應用程式和桌面。</span><span class="sxs-lookup"><span data-stu-id="7278e-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops to users.</span></span>
<span data-ttu-id="7278e-107">現在，Citrix XenApp 不提供任何災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="7278e-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="7278e-108">理想的災害復原解決方案應該允許上述複雜應用程式架構的相關復原計劃模型化，並且也能夠新增自訂步驟以處理各層之間的應用程式對應，因此在導致較低 RTO 的災難發生時能提供單鍵擷取方案。</span><span class="sxs-lookup"><span data-stu-id="7278e-108">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>

<span data-ttu-id="7278e-109">對於為 Hyper-V 和 VMware vSphere 平台上的內部部署 Citrix XenApp 部署建置災害復原方案，本文提供逐步指引。</span><span class="sxs-lookup"><span data-stu-id="7278e-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="7278e-110">本文同時也會說明如何使用復原計劃、支援的組態和必要條件，執行測試容錯移轉 (災害復原訓練) 和未計劃的 Azure 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="7278e-110">This document also describes how to perform a test failover(disaster recovery drill) and unplanned failover to Azure using recovery plans, the supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7278e-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="7278e-111">Prerequisites</span></span>

<span data-ttu-id="7278e-112">開始之前，請確定您瞭解下列項目︰</span><span class="sxs-lookup"><span data-stu-id="7278e-112">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="7278e-113">將虛擬機器複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="7278e-113">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="7278e-114">如何[設計修復網路](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="7278e-114">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="7278e-115">執行測試容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="7278e-115">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="7278e-116">執行容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="7278e-116">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="7278e-117">如何[複寫網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="7278e-117">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="7278e-118">如何[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="7278e-118">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="7278e-119">部署模式</span><span class="sxs-lookup"><span data-stu-id="7278e-119">Deployment patterns</span></span>

<span data-ttu-id="7278e-120">Citrix XenApp 和 XenDesktop 伺服器陣列通常有下列部署模式：</span><span class="sxs-lookup"><span data-stu-id="7278e-120">A Citrix XenApp and XenDesktop farm typically has the following deployment pattern:</span></span>

<span data-ttu-id="7278e-121">**部署模式**</span><span class="sxs-lookup"><span data-stu-id="7278e-121">**Deployment pattern**</span></span>

<span data-ttu-id="7278e-122">AD DNS 伺服器、SQL 資料庫伺服器、Citrix 傳遞控制站、StoreFront 伺服器，XenApp Master (VDA)、Citrix XenApp 授權伺服器的 Citrix XenApp 和 XenDesktop 部署</span><span class="sxs-lookup"><span data-stu-id="7278e-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![部署模式 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="7278e-124">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="7278e-124">Site Recovery support</span></span>

<span data-ttu-id="7278e-125">在本文中，vSphere 6.0 / System Center VMM 2012 R2 所管理 VMware 虛擬機器上的 Citrix 部署是用來安裝 DR。</span><span class="sxs-lookup"><span data-stu-id="7278e-125">For the purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used to setup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="7278e-126">來源與目標</span><span class="sxs-lookup"><span data-stu-id="7278e-126">Source and target</span></span>

<span data-ttu-id="7278e-127">**案例**</span><span class="sxs-lookup"><span data-stu-id="7278e-127">**Scenario**</span></span> | <span data-ttu-id="7278e-128">**至次要網站**</span><span class="sxs-lookup"><span data-stu-id="7278e-128">**To a secondary site**</span></span> | <span data-ttu-id="7278e-129">**至 Azure**</span><span class="sxs-lookup"><span data-stu-id="7278e-129">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="7278e-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="7278e-130">**Hyper-V**</span></span> | <span data-ttu-id="7278e-131">不在範圍中</span><span class="sxs-lookup"><span data-stu-id="7278e-131">Not in scope</span></span> | <span data-ttu-id="7278e-132">是</span><span class="sxs-lookup"><span data-stu-id="7278e-132">Yes</span></span>
<span data-ttu-id="7278e-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="7278e-133">**VMware**</span></span> | <span data-ttu-id="7278e-134">不在範圍中</span><span class="sxs-lookup"><span data-stu-id="7278e-134">Not in scope</span></span> | <span data-ttu-id="7278e-135">是</span><span class="sxs-lookup"><span data-stu-id="7278e-135">Yes</span></span>
<span data-ttu-id="7278e-136">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="7278e-136">**Physical server**</span></span> | <span data-ttu-id="7278e-137">不在範圍中</span><span class="sxs-lookup"><span data-stu-id="7278e-137">Not in scope</span></span> | <span data-ttu-id="7278e-138">是</span><span class="sxs-lookup"><span data-stu-id="7278e-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="7278e-139">版本</span><span class="sxs-lookup"><span data-stu-id="7278e-139">Versions</span></span>
<span data-ttu-id="7278e-140">客戶可以部署 XenApp 元件成為 Hyper-V 或 VMware 上執行的虛擬機器，或成為實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="7278e-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="7278e-141">Azure Site Recovery 可以保護 Azure 的實體與虛擬部署。</span><span class="sxs-lookup"><span data-stu-id="7278e-141">Azure Site Recovery can protect both physical and virtual deployments to Azure.</span></span>
<span data-ttu-id="7278e-142">由於 Azure 支援 XenApp 7.7 或更新版本，因此只有這些版本的部署才能容錯移轉到 Azure 進行災害復原或移轉。</span><span class="sxs-lookup"><span data-stu-id="7278e-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over to Azure for Disaster Recovery or migration.</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="7278e-143">要牢記在心的事項</span><span class="sxs-lookup"><span data-stu-id="7278e-143">Things to keep in mind</span></span>

1. <span data-ttu-id="7278e-144">支援使用伺服器作業系統機器保護和復原內部部署來傳遞 XenApp 發佈的應用程式和 XenApp 發佈的桌面。</span><span class="sxs-lookup"><span data-stu-id="7278e-144">Protection and recovery of on-premises deployments using Server OS machines to deliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="7278e-145">不支援使用桌面作業系統機器保護和復原內部部署來傳遞虛擬桌面的桌面 VDI，包括 Windows 10 用戶端。</span><span class="sxs-lookup"><span data-stu-id="7278e-145">Protection and recovery of on-premises deployments using desktop OS machines to deliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="7278e-146">這是因為 ASR 不支援使用復原使用桌面作業系統的機器。</span><span class="sxs-lookup"><span data-stu-id="7278e-146">This is because ASR does not support the recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="7278e-147">此外，某些用戶端虛擬桌面 (例如</span><span class="sxs-lookup"><span data-stu-id="7278e-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="7278e-148">Windows 7) 在 Azure 中尚不支援授權。</span><span class="sxs-lookup"><span data-stu-id="7278e-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="7278e-149">[深入了解](https://azure.microsoft.com/pricing/licensing-faq/)如何在 Azure 中進行用戶端/伺服器桌面的授權。</span><span class="sxs-lookup"><span data-stu-id="7278e-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="7278e-150">Azure Site Recovery 無法複寫和保護現有的內部部署 MCS 或 PV 複製品。</span><span class="sxs-lookup"><span data-stu-id="7278e-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="7278e-151">您需要使用傳遞控制站的 Azure RM 佈建重新建立這些複製品。</span><span class="sxs-lookup"><span data-stu-id="7278e-151">You need to recreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="7278e-152">無法使用 Azure Site Recovery 保護 NetScaler，因為 NetScaler 是以 FreeBSD 為基礎，而且 Azure Site Recovery 不支援 FreeBSD 作業系統的保護。</span><span class="sxs-lookup"><span data-stu-id="7278e-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="7278e-153">容錯移轉到 Azure 之後，您需要從 Azure Market Place 部署和設定新的 NetScaler 裝置。</span><span class="sxs-lookup"><span data-stu-id="7278e-153">You would need to deploy and configure a new NetScaler appliance from Azure Market place after failover to Azure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="7278e-154">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7278e-154">Replicating virtual machines</span></span>

<span data-ttu-id="7278e-155">需要保護 Citrix XenApp 部署的下列元件，才能啟用複寫和復原。</span><span class="sxs-lookup"><span data-stu-id="7278e-155">The following components of the Citrix XenApp deployment need to be protected to enable replication and recovery.</span></span>

* <span data-ttu-id="7278e-156">AD DNS 伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="7278e-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="7278e-157">SQL 資料庫伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="7278e-157">Protection of SQL database server</span></span>
* <span data-ttu-id="7278e-158">Citrix 傳遞控制站的保護</span><span class="sxs-lookup"><span data-stu-id="7278e-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="7278e-159">StoreFront 伺服器的保護。</span><span class="sxs-lookup"><span data-stu-id="7278e-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="7278e-160">XenApp Master (VDA) 的保護</span><span class="sxs-lookup"><span data-stu-id="7278e-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="7278e-161">Citrix XenApp 授權伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="7278e-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="7278e-162">**AD DNS 伺服器複寫**</span><span class="sxs-lookup"><span data-stu-id="7278e-162">**AD DNS server replication**</span></span>

<span data-ttu-id="7278e-163">關於複寫和設定 Azure 中的網域控制站所需的指引，請參閱[以 Azure Site Recovery 保護 Active Directory 和 DNS](site-recovery-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="7278e-163">Please refer to [Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="7278e-164">**SQL Database 伺服器複寫**</span><span class="sxs-lookup"><span data-stu-id="7278e-164">**SQL database Server replication**</span></span>

<span data-ttu-id="7278e-165">如需保護 SQL Server 的建議選項有關的詳細技術指引，請參閱[使用 SQL Server 災害復原與 Azure Site Recovery 保護 SQL Server](site-recovery-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="7278e-165">Please refer to [Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on the recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="7278e-166">請依照[本指引](site-recovery-vmware-to-azure.md)開始將其他元件虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7278e-166">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the other component virtual machines to Azure.</span></span>

![XenApp 元件的保護](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="7278e-168">**計算和網路設定**</span><span class="sxs-lookup"><span data-stu-id="7278e-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="7278e-169">機器受到保護之後 (在 [複寫項目] 下顯示為「受保護」狀態)，需要設定計算和網路設定。</span><span class="sxs-lookup"><span data-stu-id="7278e-169">After the machines are protected (status shows as “Protected” under Replicated Items), the Compute and Network settings need to be configured.</span></span>
<span data-ttu-id="7278e-170">在 [計算和網路] > [計算屬性] 中，您可以指定 Azure VM 名稱和目標大小。</span><span class="sxs-lookup"><span data-stu-id="7278e-170">In Compute and Network > Compute properties, you can specify the Azure VM name and target size.</span></span>
<span data-ttu-id="7278e-171">視需要修改名稱以符合 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="7278e-171">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="7278e-172">您也可以檢視和加入目標網路、子網路的相關資訊，以及將指派給 Azure VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7278e-172">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span>

<span data-ttu-id="7278e-173">請注意：</span><span class="sxs-lookup"><span data-stu-id="7278e-173">Note the following:</span></span>

* <span data-ttu-id="7278e-174">您可以設定目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7278e-174">You can set the target IP address.</span></span> <span data-ttu-id="7278e-175">如果您未提供地址，則容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="7278e-175">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="7278e-176">如果您設定的位址在容錯移轉時無法使用，則容錯移轉會失敗。</span><span class="sxs-lookup"><span data-stu-id="7278e-176">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="7278e-177">如果位址可用於測試容錯移轉網路，則相同的目標 IP 位址可用於測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="7278e-177">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

* <span data-ttu-id="7278e-178">對於 AD/DNS 伺服器，保留內部部署位址可讓您為 Azure 虛擬網路指定與 DNS 伺服器相同的位址。</span><span class="sxs-lookup"><span data-stu-id="7278e-178">For the AD/DNS server, retaining the on-premises address lets you specify the same address as the DNS server for the Azure Virtual network.</span></span>

<span data-ttu-id="7278e-179">網路介面卡的數目會視您指定給目標虛擬機器的大小而有所不同，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7278e-179">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

*   <span data-ttu-id="7278e-180">如果來源電腦上的網路介面卡數目小於或等於針對目標機器大小所允許的介面卡數目，則目標將具備與來源相同的介面卡數目。</span><span class="sxs-lookup"><span data-stu-id="7278e-180">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
*   <span data-ttu-id="7278e-181">如果來源虛擬機器的介面卡數目超過針對目標大小所允許的數目，則將使用目標大小的最大值。</span><span class="sxs-lookup"><span data-stu-id="7278e-181">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
* <span data-ttu-id="7278e-182">例如，如果來源機器具有兩張網路介面卡，而目標機器大小支援四張，則目標機器將會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="7278e-182">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="7278e-183">如果來源機器具有兩張介面卡，但支援的目標大小僅支援一張，則目標機器將只會有一張介面卡。</span><span class="sxs-lookup"><span data-stu-id="7278e-183">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>
*   <span data-ttu-id="7278e-184">如果虛擬機器有多張網路介面卡，則全部會連接至相同的網路。</span><span class="sxs-lookup"><span data-stu-id="7278e-184">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
*   <span data-ttu-id="7278e-185">如果虛擬機器具有多個網路介面卡，則清單中顯示的第一個介面卡會變成 Azure 虛擬機器中的「預設」網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="7278e-185">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the Default network adapter in the Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="7278e-186">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="7278e-186">Creating a recovery plan</span></span>

<span data-ttu-id="7278e-187">啟用 XenApp 元件 VM 的複寫之後，下一個步驟是建立復原計畫。</span><span class="sxs-lookup"><span data-stu-id="7278e-187">After replication is enabled for the XenApp component VMs, the next step is to create a recovery plan.</span></span>
<span data-ttu-id="7278e-188">復原計畫群組會將有類似需求的虛擬機器分組，以便進行容錯移轉和復原。</span><span class="sxs-lookup"><span data-stu-id="7278e-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="7278e-189">**建立復原計畫的步驟**</span><span class="sxs-lookup"><span data-stu-id="7278e-189">**Steps to create a recovery plan**</span></span>

1. <span data-ttu-id="7278e-190">在復原計畫中加入 XenApp 元件虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7278e-190">Add the XenApp component virtual machines in the Recovery Plan.</span></span>
2. <span data-ttu-id="7278e-191">按一下 [復原計畫] -> [+ 復原計畫]。</span><span class="sxs-lookup"><span data-stu-id="7278e-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="7278e-192">為復原計畫取個直覺式名稱。</span><span class="sxs-lookup"><span data-stu-id="7278e-192">Provide an intuitive name for the recovery plan.</span></span>
3. <span data-ttu-id="7278e-193">對於 VMware 虛擬機器：選取 VMware 處理序伺服器做為來源，選取 Microsoft Azure 做為目標，並選取資源管理員做為部署模型，然後按一下 [選取項目]。</span><span class="sxs-lookup"><span data-stu-id="7278e-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="7278e-194">對於 Hyper-V 虛擬機器：選取 VMM 伺服器做為來源，選取 Microsoft Azure 做為目標，選取資源管理員做為部署模型，並按一下 [選取項目]，然後選取 XenApp 部署 VM。</span><span class="sxs-lookup"><span data-stu-id="7278e-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select the XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="7278e-195">將虛擬機器新增至容錯移轉群組</span><span class="sxs-lookup"><span data-stu-id="7278e-195">Adding virtual machines to failover groups</span></span>

<span data-ttu-id="7278e-196">可以自訂復原計畫，以新增特定啟動順序、指令碼或手動動作的容錯移轉群組。</span><span class="sxs-lookup"><span data-stu-id="7278e-196">Recovery plans can be customized to add failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="7278e-197">您必須將下列群組加入至復原計畫。</span><span class="sxs-lookup"><span data-stu-id="7278e-197">The following groups need to be added to the recovery plan.</span></span>

1. <span data-ttu-id="7278e-198">容錯移轉群組 1：AD DNS</span><span class="sxs-lookup"><span data-stu-id="7278e-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="7278e-199">容錯移轉群組 2：SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="7278e-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="7278e-200">容錯移轉群組 3：VDA Master Image VM</span><span class="sxs-lookup"><span data-stu-id="7278e-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="7278e-201">容錯移轉群組 4：傳遞控制站和 StoreFront 伺服器 VM</span><span class="sxs-lookup"><span data-stu-id="7278e-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="7278e-202">將指令碼新增至復原計畫</span><span class="sxs-lookup"><span data-stu-id="7278e-202">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="7278e-203">可以在復原計畫中的特定群組之前或之後執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="7278e-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="7278e-204">也可以在容錯移轉期間加入並執行手動動作。</span><span class="sxs-lookup"><span data-stu-id="7278e-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="7278e-205">自訂的復原計畫如下所示：</span><span class="sxs-lookup"><span data-stu-id="7278e-205">The customized recovery plan looks like the below:</span></span>

1. <span data-ttu-id="7278e-206">容錯移轉群組 1：AD DNS</span><span class="sxs-lookup"><span data-stu-id="7278e-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="7278e-207">容錯移轉群組 2：SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="7278e-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="7278e-208">容錯移轉群組 3：VDA Master Image VM</span><span class="sxs-lookup"><span data-stu-id="7278e-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="7278e-209">包含手動或指令碼動作的步驟 4、6 和 7 僅適用於有 MCS/PV 目錄的內部部署 XenApp 環境。</span><span class="sxs-lookup"><span data-stu-id="7278e-209">Steps 4, 6 and 7 containing manual or script actions are applicable to only an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="7278e-210">群組 3 手動或指令碼動作：關閉主要 VDA VM。主要 VDA VM 在容錯移轉至 Azure 時將處於執行中狀態。</span><span class="sxs-lookup"><span data-stu-id="7278e-210">Group 3 Manual or script action: Shutdown master VDA VM The Master VDA VM when failed over to Azure will be in a running state.</span></span> <span data-ttu-id="7278e-211">若要使用 Azure ARM 裝載建立新的 MCS 目錄，主要 VDA VM 需要處於已停止 (已解除配置) 狀態。</span><span class="sxs-lookup"><span data-stu-id="7278e-211">To create new MCS catalogs using Azure ARM hosting, the master VDA VM is required to be in Stopped (de allocated) state.</span></span> <span data-ttu-id="7278e-212">從 Azure 入口網站關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="7278e-212">Shutdown the VM from Azure Portal.</span></span>

5. <span data-ttu-id="7278e-213">容錯移轉群組 4：傳遞控制站和 StoreFront 伺服器 VM</span><span class="sxs-lookup"><span data-stu-id="7278e-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="7278e-214">群組 3 手動或指令碼動作 1：</span><span class="sxs-lookup"><span data-stu-id="7278e-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="7278e-215">***新增 Azure RM 主機連線***</span><span class="sxs-lookup"><span data-stu-id="7278e-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="7278e-216">在傳遞控制站機器中建立 Azure ARM 主機連線，以便在 Azure 中佈建新的 MCS 目錄。</span><span class="sxs-lookup"><span data-stu-id="7278e-216">Create Azure ARM host connection in Delivery Controller machine to provision new MCS catalogs in Azure.</span></span> <span data-ttu-id="7278e-217">請遵循本[文章](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/)中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="7278e-217">Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="7278e-218">群組 3 手動或指令碼動作 2：</span><span class="sxs-lookup"><span data-stu-id="7278e-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="7278e-219">***在 Azure 中重新建立 MCS 目錄***</span><span class="sxs-lookup"><span data-stu-id="7278e-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="7278e-220">主要網站上的現有 MCS 或 PVS 複製品不會複寫到 Azure。</span><span class="sxs-lookup"><span data-stu-id="7278e-220">The existing MCS or PVS clones on the primary site will not be replicated to Azure.</span></span> <span data-ttu-id="7278e-221">您需要使用複寫的主要 VDA 和 Azure ARM 佈建，從傳遞控制站重新建立這些複製品。請遵循本[文章](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/)中所述的步驟在 Azure 中建立 MCS 目錄。</span><span class="sxs-lookup"><span data-stu-id="7278e-221">You need to recreate these clones using the replicated master VDA and Azure ARM provisioning from Delivery controller.Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) to create MCS catalogs in Azure.</span></span>

![XenApp 元件的復原計畫](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="7278e-223">您可以在[位置](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts)使用指令碼，以容錯移轉虛擬機器的新 IP 更新 DNS，或在有需要時連接容錯移轉機器上的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7278e-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) to update the DNS with the new IPs of the failed over >virtual machines or to attach a load balancer on the failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="7278e-224">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="7278e-224">Doing a test failover</span></span>

<span data-ttu-id="7278e-225">請依照[本指引](site-recovery-test-failover-to-azure.md)來執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="7278e-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

![復原方案](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="7278e-227">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="7278e-227">Doing a failover</span></span>

<span data-ttu-id="7278e-228">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="7278e-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7278e-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7278e-229">Next steps</span></span>

<span data-ttu-id="7278e-230">您可以在這份白皮書中[深入了解](https://aka.ms/citrix-xenapp-xendesktop-with-asr)複寫 Citrix XenApp 和 XenDesktop 部署。</span><span class="sxs-lookup"><span data-stu-id="7278e-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="7278e-231">參閱使用 Site Recovery [複寫其他應用程式](site-recovery-workload.md)的指引。</span><span class="sxs-lookup"><span data-stu-id="7278e-231">Look at the guidance to [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
