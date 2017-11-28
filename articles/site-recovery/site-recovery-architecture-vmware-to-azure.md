---
title: "在 Azure Site Recovery 中將 VMware 複寫至 Azure 如何運作？ | Microsoft Docs"
description: "本文提供使用 Azure Site Recovery 服務將內部部署 VMware VM 和實體伺服器複寫至 Azure 時所用元件和架構的概觀"
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
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-architecture
ms.openlocfilehash: 81f02c1277ae8a2c377ca0d6db67ec4211e9aa5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-vmware-replication-to-azure-work-in-site-recovery"></a><span data-ttu-id="1899d-104">在 Site Recovery 中將 VMware 複寫至 Azure 如何運作？</span><span class="sxs-lookup"><span data-stu-id="1899d-104">How does VMware replication to Azure work in Site Recovery?</span></span>

<span data-ttu-id="1899d-105">本文說明使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署 VMware 虛擬機器和 Windows/Linux 實體伺服器複寫至 Azure 時的相關元件和程序。</span><span class="sxs-lookup"><span data-stu-id="1899d-105">This article describes the components and processes involved when replicating on-premises VMware virtual machines, and Windows/Linux physical servers, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="1899d-106">當您將實體內部部署伺服器複寫至 Azure 時，複寫作業也會使用與 VMware VM 複寫相同的元件和程序，但有下列差異︰</span><span class="sxs-lookup"><span data-stu-id="1899d-106">When you replicate physical on-premises servers to Azure, replication uses also the same components and processes as VMware VM replication, with these differences:</span></span>

- <span data-ttu-id="1899d-107">您可以針對組態伺服器使用實體伺服器，而不是 VMware VM。</span><span class="sxs-lookup"><span data-stu-id="1899d-107">You can use a physical server for the configuration server, instead of a VMware VM.</span></span>
- <span data-ttu-id="1899d-108">您需要內部部署的 VMware 基礎結構以供進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="1899d-108">You will need an on-premises VMware infrastructure for failback.</span></span> <span data-ttu-id="1899d-109">您無法容錯回復到實體機器。</span><span class="sxs-lookup"><span data-stu-id="1899d-109">You can't fail back to a physical machine.</span></span>

<span data-ttu-id="1899d-110">請在本文下方張貼意見，或在 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="1899d-110">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="architectural-components"></a><span data-ttu-id="1899d-111">架構元件</span><span class="sxs-lookup"><span data-stu-id="1899d-111">Architectural components</span></span>

<span data-ttu-id="1899d-112">將 VMware VM 和實體伺服器複寫至 Azure 時，涉及許多元件。</span><span class="sxs-lookup"><span data-stu-id="1899d-112">There are a number of components involved when replicating VMware VMs and physical servers to Azure.</span></span>

<span data-ttu-id="1899d-113">**元件**</span><span class="sxs-lookup"><span data-stu-id="1899d-113">**Component**</span></span> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <span data-ttu-id="1899d-115">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="1899d-115">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="1899d-116">**Azure**</span><span class="sxs-lookup"><span data-stu-id="1899d-116">**Azure**</span></span> | <span data-ttu-id="1899d-117">在 Azure 中，您需要 Azure 帳戶、Azure 儲存體帳戶和 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="1899d-117">In Azure you need an Azure account, an Azure storage account, and an Azure network.</span></span> | <span data-ttu-id="1899d-118">所複寫的資料會儲存在儲存體帳戶中，而在從內部部署網站進行容錯移轉時，便會以複寫的資料建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="1899d-118">Replicated data is stored in the storage account, and Azure VMs are created with the replicated data when failover from your on-premises site occurs.</span></span> <span data-ttu-id="1899d-119">Azure VM 在建立後會連線到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1899d-119">The Azure VMs connect to the Azure virtual network when they're created.</span></span>
<span data-ttu-id="1899d-120">**組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="1899d-120">**Configuration server**</span></span> | <span data-ttu-id="1899d-121">單一內部部署管理伺服器 (VMWare VM)，它會執行部署所需的所有內部部署元件，包括組態伺服器、處理序伺服器、主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="1899d-121">A single on-premises management server (VMWare VM) that runs all the on-premises components that are needed for the deployment, including the configuration server, process server, master target server</span></span> | <span data-ttu-id="1899d-122">組態伺服器元件會協調內部部署與 Azure 之間的通訊，以及管理資料複寫。</span><span class="sxs-lookup"><span data-stu-id="1899d-122">The configuration server component coordinates communications between on-premises and Azure, and manages data replication.</span></span>
 <span data-ttu-id="1899d-123">**處理序伺服器**：</span><span class="sxs-lookup"><span data-stu-id="1899d-123">**Process server**:</span></span>  | <span data-ttu-id="1899d-124">預設會安裝在組態伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1899d-124">Installed by default on the configuration server.</span></span> | <span data-ttu-id="1899d-125">會做為複寫閘道器。</span><span class="sxs-lookup"><span data-stu-id="1899d-125">Acts as a replication gateway.</span></span> <span data-ttu-id="1899d-126">接收複寫資料，以快取、壓縮和加密進行最佳化，然後將複寫資料傳送至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1899d-126">Receives replication data, optimizes it with caching, compression, and encryption, and sends it to Azure storage.</span></span><br/><br/> <span data-ttu-id="1899d-127">處理序伺服器還會處理用來保護機器的行動服務的推入安裝，並執行 VMWare VM 的自動探索。</span><span class="sxs-lookup"><span data-stu-id="1899d-127">The process server also handles push installation of the Mobility service to protected machines, and performs automatic discovery of VMware VMs.</span></span><br/><br/> <span data-ttu-id="1899d-128">隨著部署規模擴大，您可以新增更多個別的專用處理序伺服器，以處理日益增加的複寫流量。</span><span class="sxs-lookup"><span data-stu-id="1899d-128">As your deployment grows you can add additional separate dedicated process servers to handle increasing volumes of replication traffic.</span></span>
 <span data-ttu-id="1899d-129">**主要目標伺服器**</span><span class="sxs-lookup"><span data-stu-id="1899d-129">**Master target server**</span></span> | <span data-ttu-id="1899d-130">預設會安裝在內部部署組態伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1899d-130">Installed by default on the on-premises configuration server.</span></span> | <span data-ttu-id="1899d-131">在從 Azure 容錯回復期間，處理複寫資料。</span><span class="sxs-lookup"><span data-stu-id="1899d-131">Handles replication data during failback from Azure.</span></span><br/><br/> <span data-ttu-id="1899d-132">如果容錯回復的流量很高，您可以部署個別的主要目標伺服器來供容錯回復使用。</span><span class="sxs-lookup"><span data-stu-id="1899d-132">If volumes of failback traffic are high, you can deploy a separate master target server for failback.</span></span>
<span data-ttu-id="1899d-133">**VMware 伺服器**</span><span class="sxs-lookup"><span data-stu-id="1899d-133">**VMware servers**</span></span> | <span data-ttu-id="1899d-134">VMware VM 裝載在 vSphere ESXi 伺服器上，我們建議使用 vCenter 伺服器來管理主機。</span><span class="sxs-lookup"><span data-stu-id="1899d-134">VMware VMs are hosted on vSphere ESXi servers, and we recommend a vCenter server to manage the hosts.</span></span> | <span data-ttu-id="1899d-135">您可以將 VMware 伺服器新增至您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="1899d-135">You add VMware servers to your Recovery Services vault.</span></span>
<span data-ttu-id="1899d-136">**複寫的機器**</span><span class="sxs-lookup"><span data-stu-id="1899d-136">**Replicated machines**</span></span> | <span data-ttu-id="1899d-137">行動服務將會安裝在您要複寫的每部 VMware VM 上。</span><span class="sxs-lookup"><span data-stu-id="1899d-137">The Mobility service will be installed on each VMware VM you want to replicate.</span></span> <span data-ttu-id="1899d-138">您可以手動將它安裝在每部電腦上，或是從處理序伺服器進行推入安裝。</span><span class="sxs-lookup"><span data-stu-id="1899d-138">It can be installed manually on each machine, or with a push installation from the process server.</span></span>

<span data-ttu-id="1899d-139">了解[支援矩陣](site-recovery-support-matrix-to-azure.md)中每個元件的部署必要條件和需求。</span><span class="sxs-lookup"><span data-stu-id="1899d-139">Learn about the deployment prerequisites and requirements for each of these components in the [support matrix](site-recovery-support-matrix-to-azure.md).</span></span>

<span data-ttu-id="1899d-140">**圖 1：VMware 到 Azure 的元件**</span><span class="sxs-lookup"><span data-stu-id="1899d-140">**Figure 1: VMware to Azure components**</span></span>

![元件](./media/site-recovery-components/arch-enhanced.png)

## <a name="replication-process"></a><span data-ttu-id="1899d-142">複寫程序</span><span class="sxs-lookup"><span data-stu-id="1899d-142">Replication process</span></span>

1. <span data-ttu-id="1899d-143">您要設定部署 (包括 Azure 元件) 和復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="1899d-143">You set up the deployment, including Azure components, and a Recovery Services vault.</span></span> <span data-ttu-id="1899d-144">在保存庫中指定複寫來源和目標、設定組態伺服器、新增 VMware 伺服器、建立複寫原則、部署行動服務、啟用複寫，以及執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1899d-144">In the vault you specify the replication source and target, set up the configuration server, add VMware servers, create a replication policy, deploy the Mobility service, enable replication, and run a test failover.</span></span>
2.  <span data-ttu-id="1899d-145">機器根據複寫原則開始複寫，並將資料的初始複本複寫到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1899d-145">Machines start replicating in accordance with the replication policy, and an initial copy of the data is replicated to Azure storage.</span></span>
4. <span data-ttu-id="1899d-146">初始複寫完成之後，就會開始將差異變更複寫到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1899d-146">Replication of delta changes to Azure begins after the initial replication finishes.</span></span> <span data-ttu-id="1899d-147">機器的追蹤變更會保存在 .hrl 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1899d-147">Tracked changes for a machine are held in a .hrl file.</span></span>
    - <span data-ttu-id="1899d-148">複寫機器會在輸入連接埠 HTTPS 443 上與組態伺服器進行通訊，以管理複寫。</span><span class="sxs-lookup"><span data-stu-id="1899d-148">Replicating machines communicate with the configuration server on port HTTPS 443 inbound, for replication management.</span></span>
    - <span data-ttu-id="1899d-149">複寫機器會在輸入連接埠 HTTPS 9443 (可加以設定) 上將複寫資料傳送至處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="1899d-149">Replicating machines send replication data to the process server on port HTTPS 9443 inbound (can be configured).</span></span>
    - <span data-ttu-id="1899d-150">組態伺服器會透過輸出連接埠 HTTPS 443 與 Azure 協調複寫管理。</span><span class="sxs-lookup"><span data-stu-id="1899d-150">The configuration server orchestrates replication management with Azure over port HTTPS 443 outbound.</span></span>
    - <span data-ttu-id="1899d-151">處理序伺服器會透過輸出連接埠 443，接收來源機器所傳來的資料、將其最佳化並加密，再將它傳送至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1899d-151">The process server receives data from source machines, optimizes and encrypts it, and sends it to Azure storage over port 443 outbound.</span></span>
    - <span data-ttu-id="1899d-152">如果您啟用多部 VM 一致性，則複寫群組中的機器會透過連接埠 20004 彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="1899d-152">If you enable multi-VM consistency, then machines in the replication group communicate with each other over port 20004.</span></span> <span data-ttu-id="1899d-153">如果您將多部機器群組為幾個共用當機時保持一致復原點和應用程式一致復原點的複寫群組，當這些群組在進行容錯移轉時，便會使用多部 VM。</span><span class="sxs-lookup"><span data-stu-id="1899d-153">Multi-VM is used if you group multiple machines into replication groups that share crash-consistent and app-consistent recovery points when they fail over.</span></span> <span data-ttu-id="1899d-154">如果機器執行的是相同的工作負載，且需要保持一致，此功能就很實用。</span><span class="sxs-lookup"><span data-stu-id="1899d-154">This is useful if machines are running the same workload and need to be consistent.</span></span>
5. <span data-ttu-id="1899d-155">流量透過網際網路複寫到 Azure 儲存體的公用端點。</span><span class="sxs-lookup"><span data-stu-id="1899d-155">Traffic is replicated to Azure storage public endpoints, over the internet.</span></span> <span data-ttu-id="1899d-156">或者，您可以使用 Azure ExpressRoute [公用對等](../expressroute/expressroute-circuit-peerings.md#public-peering)。</span><span class="sxs-lookup"><span data-stu-id="1899d-156">Alternately, you can use Azure ExpressRoute [public peering](../expressroute/expressroute-circuit-peerings.md#public-peering).</span></span> <span data-ttu-id="1899d-157">不支援從內部部署網站透過站台對站台 VPN 將流量複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="1899d-157">Replicating traffic over a site-to-site VPN from an on-premises site to Azure isn't supported.</span></span>

<span data-ttu-id="1899d-158">**圖 2：VMware 到 Azure 的複寫**</span><span class="sxs-lookup"><span data-stu-id="1899d-158">**Figure 2: VMware to Azure replication**</span></span>

![增強](./media/site-recovery-components/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="1899d-160">容錯移轉和容錯回復程序</span><span class="sxs-lookup"><span data-stu-id="1899d-160">Failover and failback process</span></span>

1. <span data-ttu-id="1899d-161">確認測試容錯移轉如預期般運作之後，您可以視需要執行至 Azure 的未計劃容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1899d-161">After you verify that test failover is working as expected, you can run unplanned failovers to Azure as required.</span></span> <span data-ttu-id="1899d-162">不支援有計劃的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1899d-162">Planned failover isn't supported.</span></span>
2. <span data-ttu-id="1899d-163">您可以容錯移轉單一機器，或建立[復原計劃](site-recovery-create-recovery-plans.md)，來容錯移轉多部 VM。</span><span class="sxs-lookup"><span data-stu-id="1899d-163">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md), to fail over multiple VMs.</span></span>
3. <span data-ttu-id="1899d-164">當您執行容錯移轉時，會在 Azure 中建立複本 VM。</span><span class="sxs-lookup"><span data-stu-id="1899d-164">When you run a failover, replica VMs are created in Azure.</span></span> <span data-ttu-id="1899d-165">您要認可讓容錯移轉開始存取來自複本 Azure VM 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="1899d-165">You commit a failover to start accessing the workload from the replica Azure VM.</span></span>
4. <span data-ttu-id="1899d-166">當主要的內部部署網站恢復可用狀態時，您就可以容錯回復。</span><span class="sxs-lookup"><span data-stu-id="1899d-166">When your primary on-premises site is available again, you can fail back.</span></span> <span data-ttu-id="1899d-167">您要設定容錯回復基礎結構、開始將機器從次要網站複寫到主要網站，以及從次要網站執行非計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1899d-167">You set up a failback infrastructure, start replicating the machine from the secondary site to the primary, and run an unplanned failover from the secondary site.</span></span> <span data-ttu-id="1899d-168">在認可此容錯移轉後，資料會回到內部部署網站，而您必須再次啟用複寫至 Azure 的功能。</span><span class="sxs-lookup"><span data-stu-id="1899d-168">After you commit this failover, data will be back on-premises, and you need to enable replication to Azure again.</span></span> [<span data-ttu-id="1899d-169">深入了解</span><span class="sxs-lookup"><span data-stu-id="1899d-169">Learn more</span></span>](site-recovery-failback-azure-to-vmware.md)

<span data-ttu-id="1899d-170">容錯回復有以下幾項需求︰</span><span class="sxs-lookup"><span data-stu-id="1899d-170">There are a few failback requirements:</span></span>


- <span data-ttu-id="1899d-171">**Azure 中的暫存處理序伺服器**︰如果您想要在容錯移轉後從 Azure 容錯回復，您必須將 Azure VM 設定為處理序伺服器，以處理來自 Azure 的複寫。</span><span class="sxs-lookup"><span data-stu-id="1899d-171">**Temporary process server in Azure**: If you want to fail back from Azure after failover you'll need to set up an Azure VM configured as a process server, to handle replication from Azure.</span></span> <span data-ttu-id="1899d-172">容錯回復完成後，您可以刪除此 VM。</span><span class="sxs-lookup"><span data-stu-id="1899d-172">You can delete this VM after failback finishes.</span></span>
- <span data-ttu-id="1899d-173">**VPN 連線**：如需容錯回復，您需要設定從 Azure 網路到內部部署網站的 VPN 連線 (或 Azure ExpressRoute)。</span><span class="sxs-lookup"><span data-stu-id="1899d-173">**VPN connection**: For failback you'll need a VPN connection (or Azure ExpressRoute) set up from the Azure network to the on-premises site.</span></span>
- <span data-ttu-id="1899d-174">**個別內部部署主要目標伺服器**︰內部部署主要目標伺服器會處理容錯回復。</span><span class="sxs-lookup"><span data-stu-id="1899d-174">**Separate on-premises master target server**: The on-premises master target server handles failback.</span></span> <span data-ttu-id="1899d-175">主要目標伺服器預設會安裝在管理伺服器上，但如果要容錯回復大量資料，您應該就此目的設定個別的內部部署主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="1899d-175">The master target server is installed by default on the management server, but if you're failing back larger volumes of traffic you should set up a separate on-premises master target server for this purpose.</span></span>
- <span data-ttu-id="1899d-176">**容錯回復原則**︰若要複寫回到內部部署網站，您需要容錯回復原則。</span><span class="sxs-lookup"><span data-stu-id="1899d-176">**Failback policy**: To replicate back to your on-premises site, you need a failback policy.</span></span> <span data-ttu-id="1899d-177">此原則會在您建立複寫原則時自動建立。</span><span class="sxs-lookup"><span data-stu-id="1899d-177">This is automatically created when you created your replication policy.</span></span>
- <span data-ttu-id="1899d-178">**VMware 基礎結構**：您必須容錯回復到內部部署 VMware VM。</span><span class="sxs-lookup"><span data-stu-id="1899d-178">**VMware infrastructure**: You must fail back to an on-premises VMware VM.</span></span> <span data-ttu-id="1899d-179">這表示您需要內部部署 VMware 基礎結構，即使是將內部部署實體伺服器複寫到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1899d-179">This means you need an on-premises VMware infrastructure, even if you're replicating on-premises physical servers to Azure.</span></span>

<span data-ttu-id="1899d-180">**圖 3：VMware/實體容錯回復**</span><span class="sxs-lookup"><span data-stu-id="1899d-180">**Figure 3: VMware/physical failback**</span></span>

![容錯回復](./media/site-recovery-components/enhanced-failback.png)


## <a name="next-steps"></a><span data-ttu-id="1899d-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1899d-182">Next steps</span></span>

<span data-ttu-id="1899d-183">檢閱[支援矩陣](site-recovery-support-matrix-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="1899d-183">Review the [support matrix](site-recovery-support-matrix-to-azure.md)</span></span>
