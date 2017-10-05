---
title: "在 Azure Site Recovery 中將內部部署機器複寫至次要內部部署網站如何運作？ | Microsoft Docs"
description: "本文提供使用 Azure Site Recovery 服務將內部部署 VM 和實體伺服器複寫至次要網站時所用元件和架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: fca95c63964b955db7ddfbe53250702cc8af122e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-on-premises-machine-replication-to-a-secondary-site-work-in-site-recovery"></a><span data-ttu-id="0fd01-104">在 Site Recovery 中將內部部署機器複寫至次要網站如何運作？</span><span class="sxs-lookup"><span data-stu-id="0fd01-104">How does on-premises machine replication to a secondary site work in Site Recovery?</span></span>

<span data-ttu-id="0fd01-105">本文說明使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署虛擬機器和實體伺服器複寫至 Azure 時的相關元件和程序。</span><span class="sxs-lookup"><span data-stu-id="0fd01-105">This article describes the components and processes involved when replicating on-premises virtual machines and physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="0fd01-106">您可以將下列項目複寫至次要內部部署網站：</span><span class="sxs-lookup"><span data-stu-id="0fd01-106">You can replicate the following to a secondary on-premises site:</span></span>
- <span data-ttu-id="0fd01-107">Hyper-V 叢集和獨立主機上在 System Center Virtual Machine Manager (VMM) 雲端中管理的內部部署 Hyper-V VM。</span><span class="sxs-lookup"><span data-stu-id="0fd01-107">On-premises Hyper-V VMs Hyper-V VMs on Hyper-V clusters and standalone hosts that are managed in System Center Virtual Machine Manager (VMM) clouds.</span></span>
- <span data-ttu-id="0fd01-108">內部部署 VMware VM 和 Windows/Linux 實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fd01-108">On-premises VMware VMs and Windows/Linux physical servers.</span></span> <span data-ttu-id="0fd01-109">在此案例中，複寫是由 Scout 管理。</span><span class="sxs-lookup"><span data-stu-id="0fd01-109">In this scenario replication is managed by Scout.</span></span>

<span data-ttu-id="0fd01-110">如有任何意見，請張貼於這篇文章下方或 [Azure 復原服務論壇 (英文)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 中。</span><span class="sxs-lookup"><span data-stu-id="0fd01-110">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="replicate-hyper-v-vms-to-a-secondary-on-premises-site"></a><span data-ttu-id="0fd01-111">將 Hyper-V VM 複寫至次要內部部署網站</span><span class="sxs-lookup"><span data-stu-id="0fd01-111">Replicate Hyper-V VMs to a secondary on-premises site</span></span>


### <a name="architectural-components"></a><span data-ttu-id="0fd01-112">架構元件</span><span class="sxs-lookup"><span data-stu-id="0fd01-112">Architectural components</span></span>

<span data-ttu-id="0fd01-113">以下是要將 Hyper-V VM 複寫到次要網站的所需項目。</span><span class="sxs-lookup"><span data-stu-id="0fd01-113">Here's what you need for replicating Hyper-V VMs to a secondary site.</span></span>

<span data-ttu-id="0fd01-114">**元件**</span><span class="sxs-lookup"><span data-stu-id="0fd01-114">**Component**</span></span> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <span data-ttu-id="0fd01-116">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="0fd01-116">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="0fd01-117">**Azure**</span><span class="sxs-lookup"><span data-stu-id="0fd01-117">**Azure**</span></span> | <span data-ttu-id="0fd01-118">您需要 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fd01-118">You need an account in Microsoft.</span></span> |
<span data-ttu-id="0fd01-119">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-119">**VMM server**</span></span> | <span data-ttu-id="0fd01-120">我們建議主要網站與次要網站中各要有一部 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="0fd01-120">We recommend a VMM server in the primary site, and one in the secondary site</span></span> | <span data-ttu-id="0fd01-121">每部 VMM 伺服器應連線至網際網路。</span><span class="sxs-lookup"><span data-stu-id="0fd01-121">Each VMM server should be connected to the internet.</span></span><br/><br/> <span data-ttu-id="0fd01-122">每一部伺服器都應該有至少一個 VMM 私人雲端，並設定好 Hyper-V 功能設定檔。</span><span class="sxs-lookup"><span data-stu-id="0fd01-122">Each server should have at least one VMM private cloud, with the Hyper-V capability profile set.</span></span><br/><br/> <span data-ttu-id="0fd01-123">您會在 VMM 伺服器上安裝 Azure Site Recovery Provider。</span><span class="sxs-lookup"><span data-stu-id="0fd01-123">You install the Azure Site Recovery Provider on the VMM server.</span></span> <span data-ttu-id="0fd01-124">此提供者會透過網際網路與 Site Recovery 服務協調進行複寫。</span><span class="sxs-lookup"><span data-stu-id="0fd01-124">The Provider coordinates and orchestrates replication with the Site Recovery service over the internet.</span></span> <span data-ttu-id="0fd01-125">Provider 和 Azure 之間的通訊都是安全且加密的。</span><span class="sxs-lookup"><span data-stu-id="0fd01-125">Communications between the Provider and Azure are secure and encrypted.</span></span>
<span data-ttu-id="0fd01-126">**Hyper-V 伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-126">**Hyper-V server**</span></span> |  <span data-ttu-id="0fd01-127">在主要和次要 VMM 雲端中，有一或多部 Hyper-V 主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fd01-127">One or more Hyper-V host servers in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="0fd01-128">伺服器應連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="0fd01-128">Servers should be connected to the internet.</span></span><br/><br/> <span data-ttu-id="0fd01-129">在主要和次要 Hyper-V 主機伺服器之間，使用 Kerberos 或憑證驗證透過 LAN 或 VPN 來複寫資料。</span><span class="sxs-lookup"><span data-stu-id="0fd01-129">Data is replicated between the primary and secondary Hyper-V host servers over the LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="0fd01-130">**Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="0fd01-130">**Hyper-V VMs**</span></span> | <span data-ttu-id="0fd01-131">位於來源 Hyper-V 主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fd01-131">Located on the source Hyper-V host server.</span></span> | <span data-ttu-id="0fd01-132">來源主機伺服器應該至少有一個您想要複寫的 VM。</span><span class="sxs-lookup"><span data-stu-id="0fd01-132">The source host server should have at least one VM that you want to replicate.</span></span>

### <a name="replication-process"></a><span data-ttu-id="0fd01-133">複寫程序</span><span class="sxs-lookup"><span data-stu-id="0fd01-133">Replication process</span></span>

1. <span data-ttu-id="0fd01-134">您要設定 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fd01-134">You set up the Azure account.</span></span>
2. <span data-ttu-id="0fd01-135">您要建立用於 Site Recovery 的複寫服務保存庫，並設定保存庫設定，包括︰</span><span class="sxs-lookup"><span data-stu-id="0fd01-135">You create a Replication Services vault for Site Recovery, and configure vault settings, including:</span></span>

    - <span data-ttu-id="0fd01-136">複寫來源和目標 (主要和次要網站)。</span><span class="sxs-lookup"><span data-stu-id="0fd01-136">The replication source and target (primary and secondary sites).</span></span>
    - <span data-ttu-id="0fd01-137">安裝 Azure Site Recovery 提供者和 Microsoft Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="0fd01-137">Installation of the Azure Site Recovery Provider and the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="0fd01-138">提供者安裝在 VMM 伺服器上，代理程式則安裝在每一部 Hyper-V 主機上。</span><span class="sxs-lookup"><span data-stu-id="0fd01-138">The Provider is installed on VMM servers, and the agent on each Hyper-V host.</span></span>
    - <span data-ttu-id="0fd01-139">您要建立來源 VMM 雲端的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="0fd01-139">You create a replication policy for source VMM cloud.</span></span> <span data-ttu-id="0fd01-140">此原則會套用至位於雲端主機上的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="0fd01-140">The policy is applied to all VMs located on hosts in the cloud.</span></span>
    - <span data-ttu-id="0fd01-141">您要啟用 Hyper-V VM 的複寫。</span><span class="sxs-lookup"><span data-stu-id="0fd01-141">You enable replication for Hyper-V VMs.</span></span> <span data-ttu-id="0fd01-142">初始複寫會根據複寫原則設定來進行。</span><span class="sxs-lookup"><span data-stu-id="0fd01-142">Initial replication occurs in accordance with the replication policy settings.</span></span>
4. <span data-ttu-id="0fd01-143">資料變更會受到追蹤，而在初始複寫完成之後，就會開始複寫差異變更。</span><span class="sxs-lookup"><span data-stu-id="0fd01-143">Data changes are tracked, and replication of delta changes to begins after the initial replication finishes.</span></span> <span data-ttu-id="0fd01-144">項目的追蹤變更會保存在 .hrl 檔案中。</span><span class="sxs-lookup"><span data-stu-id="0fd01-144">Tracked changes for an item are held in a .hrl file.</span></span>
5. <span data-ttu-id="0fd01-145">您要執行測試容錯移轉，以確定一切都沒問題。</span><span class="sxs-lookup"><span data-stu-id="0fd01-145">You run a test failover to make sure everything's working.</span></span>

<span data-ttu-id="0fd01-146">**圖 1：VMM 至 VMM 的複寫**</span><span class="sxs-lookup"><span data-stu-id="0fd01-146">**Figure 1: VMM to VMM replication**</span></span>

![內部部署至內部部署](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a><span data-ttu-id="0fd01-148">容錯移轉和容錯回復程序</span><span class="sxs-lookup"><span data-stu-id="0fd01-148">Failover and failback process</span></span>

1. <span data-ttu-id="0fd01-149">您可以在內部部署網站間執行計劃性或非計劃性的[容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="0fd01-149">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="0fd01-150">如果您執行計劃性容錯移轉，則來源 VM 會關閉以確保不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="0fd01-150">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="0fd01-151">您可以容錯移轉單一機器，或建立[復原計劃](site-recovery-create-recovery-plans.md)來協調多部機器的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="0fd01-151">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="0fd01-152">如果您執行非計劃性容錯移轉到次要網站，則在容錯移轉之後，次要位置中的容錯移轉機器不會啟用保護或複寫。</span><span class="sxs-lookup"><span data-stu-id="0fd01-152">If you perform an unplanned failover to a secondary site, after the failover machines in the secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="0fd01-153">如果您執行了計劃性容錯移轉，則在容錯移轉之後，次要位置中的容錯移轉機器會受到保護。</span><span class="sxs-lookup"><span data-stu-id="0fd01-153">If you ran a planned failover, after the failover, machines in the secondary location are protected.</span></span>
5. <span data-ttu-id="0fd01-154">然後，您要認可讓容錯移轉開始存取來自複本 VM 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0fd01-154">Then, you commit the failover to start accessing the workload from the replica VM.</span></span>
6. <span data-ttu-id="0fd01-155">當主要網站恢復可用狀態時，您就可以起始從次要網站到主要網站的反向複寫作業。</span><span class="sxs-lookup"><span data-stu-id="0fd01-155">When your primary site is available again, you initiate reverse replication to replicate from the secondary site to the primary.</span></span> <span data-ttu-id="0fd01-156">反向複寫會讓虛擬機器進入受保護的狀態，但是次要資料中心仍是使用中位置。</span><span class="sxs-lookup"><span data-stu-id="0fd01-156">Reverse replication brings the virtual machines into a protected state, but the secondary datacenter is still the active location.</span></span>
7. <span data-ttu-id="0fd01-157">若要讓主要網站再次成為使用中位置，您需要起始從次要網站到主要網站的計劃性容錯移轉，然後再進行另一個反向複寫。</span><span class="sxs-lookup"><span data-stu-id="0fd01-157">To make the primary site into the active location again, you initiate a planned failover from secondary to primary, followed by another reverse replication.</span></span>




## <a name="replicate-vmware-vmsphysical-servers-to-a-secondary-site"></a><span data-ttu-id="0fd01-158">將 VMware VM/實體伺服器複寫至次要網站</span><span class="sxs-lookup"><span data-stu-id="0fd01-158">Replicate VMware VMs/physical servers to a secondary site</span></span>

<span data-ttu-id="0fd01-159">您可以使用 InMage Scout 及下列架構元件，將 VMware VM 或實體伺服器複寫至次要網站：</span><span class="sxs-lookup"><span data-stu-id="0fd01-159">You replicate VMware VMs or physical servers to a secondary site using InMage Scout, using these architectural components:</span></span>


### <a name="architectural-components"></a><span data-ttu-id="0fd01-160">架構元件</span><span class="sxs-lookup"><span data-stu-id="0fd01-160">Architectural components</span></span>

<span data-ttu-id="0fd01-161">**元件**</span><span class="sxs-lookup"><span data-stu-id="0fd01-161">**Component**</span></span> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <span data-ttu-id="0fd01-163">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="0fd01-163">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="0fd01-164">**Azure**</span><span class="sxs-lookup"><span data-stu-id="0fd01-164">**Azure**</span></span> | <span data-ttu-id="0fd01-165">InMage Scout。</span><span class="sxs-lookup"><span data-stu-id="0fd01-165">InMage Scout.</span></span> | <span data-ttu-id="0fd01-166">若要取得 InMage Scout，您必須要有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fd01-166">To obtain InMage Scout you need an Azure subscription.</span></span><br/><br/> <span data-ttu-id="0fd01-167">建立復原服務保存庫之後，您可下載 InMage Scout 並安裝最新的更新，以設定部署。</span><span class="sxs-lookup"><span data-stu-id="0fd01-167">After you create a Recovery Services vault, you download InMage Scout and install the latest updates to set up the deployment.</span></span>
<span data-ttu-id="0fd01-168">**處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-168">**Process server**</span></span> | <span data-ttu-id="0fd01-169">位於主要網站</span><span class="sxs-lookup"><span data-stu-id="0fd01-169">Located in primary site</span></span> | <span data-ttu-id="0fd01-170">您部署處理序伺服器來處理快取、壓縮和資料最佳化。</span><span class="sxs-lookup"><span data-stu-id="0fd01-170">You deploy the process server to handle caching, compression, and data optimization.</span></span><br/><br/> <span data-ttu-id="0fd01-171">它也會處理您想要保護的機器的整合代理程式推入安裝。</span><span class="sxs-lookup"><span data-stu-id="0fd01-171">It also handles push installation of the Unified Agent to machines you want to protect.</span></span>
<span data-ttu-id="0fd01-172">**組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-172">**Configuration server**</span></span> | <span data-ttu-id="0fd01-173">位於次要網站</span><span class="sxs-lookup"><span data-stu-id="0fd01-173">Located in secondary site</span></span> | <span data-ttu-id="0fd01-174">組態伺服器會使用管理網站或 vContinuum 主控台來管理、設定和監視您的部署。</span><span class="sxs-lookup"><span data-stu-id="0fd01-174">The configuration server manages, configure, and monitor your deployment, either using the management website or the vContinuum console.</span></span>
<span data-ttu-id="0fd01-175">**vContinuum 伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-175">**vContinuum server**</span></span> | <span data-ttu-id="0fd01-176">選用。</span><span class="sxs-lookup"><span data-stu-id="0fd01-176">Optional.</span></span> <span data-ttu-id="0fd01-177">與組態伺服器安裝在相同的位置。</span><span class="sxs-lookup"><span data-stu-id="0fd01-177">Installed in the same location as the configuration server.</span></span> | <span data-ttu-id="0fd01-178">它會提供主控台來管理及監視您的受保護的環境。</span><span class="sxs-lookup"><span data-stu-id="0fd01-178">It provides a console for managing and monitoring your protected environment.</span></span>
<span data-ttu-id="0fd01-179">**主要目標伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-179">**Master target server**</span></span> | <span data-ttu-id="0fd01-180">位於次要網站</span><span class="sxs-lookup"><span data-stu-id="0fd01-180">Located in the secondary site</span></span> | <span data-ttu-id="0fd01-181">主要目標伺服器保留複製的資料。</span><span class="sxs-lookup"><span data-stu-id="0fd01-181">The master target server holds replicated data.</span></span> <span data-ttu-id="0fd01-182">它會從處理序伺服器接收資料，在次要網站中建立複本機器，並且保存資料保留點。</span><span class="sxs-lookup"><span data-stu-id="0fd01-182">It receives data from the process server, creates a replica machine in the secondary site, and holds the data retention points.</span></span><br/><br/> <span data-ttu-id="0fd01-183">您需要的主要目標伺服器的數目取決於您要保護的機器數目。</span><span class="sxs-lookup"><span data-stu-id="0fd01-183">The number of master target servers you need depends on the number of machines you're protecting.</span></span><br/><br/> <span data-ttu-id="0fd01-184">如果您想要容錯回復到主要網站，您也需要主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fd01-184">If you want to fail back to the primary site, you need a master target server there too.</span></span> <span data-ttu-id="0fd01-185">此伺服器上會安裝整合代理程式。</span><span class="sxs-lookup"><span data-stu-id="0fd01-185">The Unified Agent is installed on this server.</span></span>
<span data-ttu-id="0fd01-186">**VMware ESX/ESXi 和 vCenter 伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-186">**VMware ESX/ESXi and vCenter server**</span></span> |  <span data-ttu-id="0fd01-187">VM 裝載於 ESX/ESXi 主機。</span><span class="sxs-lookup"><span data-stu-id="0fd01-187">VMs are hosted on ESX/ESXi hosts.</span></span> <span data-ttu-id="0fd01-188">主機是使用 vCenter 伺服器進行管理</span><span class="sxs-lookup"><span data-stu-id="0fd01-188">Hosts are managed with a vCenter server</span></span> | <span data-ttu-id="0fd01-189">您需要 VMware 基礎結構以便複寫 VMware VM。</span><span class="sxs-lookup"><span data-stu-id="0fd01-189">You need a VMware infrastructure to replicate VMware VMs.</span></span>
<span data-ttu-id="0fd01-190">**VM/實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="0fd01-190">**VMs/physical servers**</span></span> |  <span data-ttu-id="0fd01-191">安裝於 VMware VM 上的整合代理程式和您想要複寫的實體伺服器</span><span class="sxs-lookup"><span data-stu-id="0fd01-191">Unified Agent installed on VMware VMs and physical servers you want to replicate.</span></span> | <span data-ttu-id="0fd01-192">此代理程式會做為所有元件之間的通訊提供者。</span><span class="sxs-lookup"><span data-stu-id="0fd01-192">The agent acts as a communication provider between all of the components.</span></span>


### <a name="replication-process"></a><span data-ttu-id="0fd01-193">複寫程序</span><span class="sxs-lookup"><span data-stu-id="0fd01-193">Replication process</span></span>

1. <span data-ttu-id="0fd01-194">您會在每個網站 (組態、處理序、主要目標) 中設定元件伺服器，並在您要複寫的機器上安裝整合代理程式。</span><span class="sxs-lookup"><span data-stu-id="0fd01-194">You set up the component servers in each site (configuration, process, master target), and install the Unified Agent on machines that you want to replicate.</span></span>
2. <span data-ttu-id="0fd01-195">初始複寫之後，每部機器上的代理程式會將差異複寫變更傳送至處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fd01-195">After initial replication, the agent on each machine sends delta replication changes to the process server.</span></span>
3. <span data-ttu-id="0fd01-196">處理序伺服器會最佳化此資料，並且將其傳輸至次要網站上的主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="0fd01-196">The process server optimizes the data, and transfers it to the master target server on the secondary site.</span></span> <span data-ttu-id="0fd01-197">設定伺服器會管理複寫程序。</span><span class="sxs-lookup"><span data-stu-id="0fd01-197">The configuration server manages the replication process.</span></span>

<span data-ttu-id="0fd01-198">**圖 2：VMware 到 VMware 的複寫**</span><span class="sxs-lookup"><span data-stu-id="0fd01-198">**Figure 2: VMware to VMware replication**</span></span>

![VMware 至 VMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a><span data-ttu-id="0fd01-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fd01-200">Next steps</span></span>

<span data-ttu-id="0fd01-201">檢閱[支援矩陣](site-recovery-support-matrix-to-sec-site.md)</span><span class="sxs-lookup"><span data-stu-id="0fd01-201">Review the [support matrix](site-recovery-support-matrix-to-sec-site.md)</span></span>
