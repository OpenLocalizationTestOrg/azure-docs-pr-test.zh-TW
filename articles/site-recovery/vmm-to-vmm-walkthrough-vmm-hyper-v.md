---
title: "VMM 和 HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery 的 aaaSet |Microsoft 文件"
description: "描述如何 tooset System Center VMM 伺服器和 HYPER-V 主機複寫 tooa 次要 VMM 站台。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="ebdf2-103">步驟 4： 設定 VMM 和 HYPER-V 的 HYPER-V 虛擬機器複寫 tooa 次要站台</span><span class="sxs-lookup"><span data-stu-id="ebdf2-103">Step 4: Set up VMM and Hyper-V for Hyper-V VM replication tooa secondary site</span></span> 

<span data-ttu-id="ebdf2-104">您已備妥的網路功能之後，設定 System Center Virtual Machine Manager (VMM) 伺服器和 HYPER-V 主機的 HYPER-V 虛擬機器 (VM) 複寫 tooa 次要站台，使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-104">After you've prepared for networking, set up System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts for Hyper-V virtual machine (VM) replication tooa secondary site, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> 

<span data-ttu-id="ebdf2-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="prepare-vmm-servers"></a><span data-ttu-id="ebdf2-106">準備 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="ebdf2-106">Prepare VMM servers</span></span> 

<span data-ttu-id="ebdf2-107">tooprepare 部署：</span><span class="sxs-lookup"><span data-stu-id="ebdf2-107">tooprepare for deployment:</span></span>


1. <span data-ttu-id="ebdf2-108">請確定 VMM 伺服器符合 hello[支援需求](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)，和[部署必要條件](vmm-to-vmm-walkthrough-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-108">Make sure VMM servers comply with hello [support requirements](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), and [deployment prerequisites](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
2. <span data-ttu-id="ebdf2-109">請確定 VMM 伺服器可以連線的 toohello 網際網路，而且有存取 toothese Url。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-109">Make sure VMM servers are connected toohello internet and have access toothese URLs.</span></span>
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - <span data-ttu-id="ebdf2-110">如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
    - <span data-ttu-id="ebdf2-111">允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
    - <span data-ttu-id="ebdf2-112">允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>
3. <span data-ttu-id="ebdf2-113">請確定 hello VMM 伺服器[準備網路對應](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)</span><span class="sxs-lookup"><span data-stu-id="ebdf2-113">Make sure hello VMM server is [prepared for network mapping](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)</span></span>


## <a name="prepare-hyper-v-hostsclusters"></a><span data-ttu-id="ebdf2-114">準備 Hyper-V 主機/叢集</span><span class="sxs-lookup"><span data-stu-id="ebdf2-114">Prepare Hyper-V hosts/clusters</span></span>

1. <span data-ttu-id="ebdf2-115">請確定 HYPER-V 主機叢集符合 hello[支援需求](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)，和[部署必要條件](vmm-to-vmm-walkthrough-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-115">Make sure Hyper-V hosts/clusters comply with hello [support requirements](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), and [deployment prerequisites](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
2. <span data-ttu-id="ebdf2-116">確認 hello 需求[HYPER-V Vm](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)</span><span class="sxs-lookup"><span data-stu-id="ebdf2-116">Verify hello requirements for [Hyper-V VMs](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)</span></span>
3. <span data-ttu-id="ebdf2-117">驗證[網路](site-recovery-support-matrix-to-sec-site.md#network-configuration)和[儲存體](site-recovery-support-matrix-to-sec-site.md#storage)需求。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-117">Verify [network](site-recovery-support-matrix-to-sec-site.md#network-configuration) and [storage](site-recovery-support-matrix-to-sec-site.md#storage) requirements.</span></span>
4. <span data-ttu-id="ebdf2-118">請確定在 HYPER-V 主機連線的 toohello 網際網路，而且有存取 toothese Url。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-118">Make sure Hyper-V hosts are connected toohello internet and have access toothese URLs.</span></span>
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - <span data-ttu-id="ebdf2-119">如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-119">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
    - <span data-ttu-id="ebdf2-120">允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-120">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
    - <span data-ttu-id="ebdf2-121">允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-121">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

## <a name="prepare-for-single-server-deployment"></a><span data-ttu-id="ebdf2-122">準備進行單一伺服器部署</span><span class="sxs-lookup"><span data-stu-id="ebdf2-122">Prepare for single server deployment</span></span>


<span data-ttu-id="ebdf2-123">如果您只有單一 VMM 伺服器，您可以將複寫 Vm hello VMM 雲端中的 HYPER-V 主機中太[Azure](hyper-v-site-walkthrough-overview.md)或 tooa 次要 VMM 雲端，這份文件中所述。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-123">If you only have a single VMM server, you can replicate VMs in Hyper-V hosts in hello VMM cloud too[Azure](hyper-v-site-walkthrough-overview.md) or tooa secondary VMM cloud, as described in this document.</span></span> <span data-ttu-id="ebdf2-124">我們建議 hello 第一個選項，因為雲端之間的複寫不順暢。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-124">We recommend hello first option because replicating between clouds isn't seamless.</span></span>

<span data-ttu-id="ebdf2-125">如果您想 tooreplicate 雲端之間，您可以使用單一獨立 VMM 伺服器，或複寫延展 Windows 叢集中部署一部 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="ebdf2-125">If you do want tooreplicate between clouds, you can replicate with a single standalone VMM server, or with a single VMM server deployed in a stretched Windows cluster</span></span>

### <a name="replicate-with-a-standalone-vmm-server"></a><span data-ttu-id="ebdf2-126">以獨立 VMM 伺服器進行複寫</span><span class="sxs-lookup"><span data-stu-id="ebdf2-126">Replicate with a standalone VMM server</span></span>

<span data-ttu-id="ebdf2-127">在此案例中，您為虛擬機器在 hello 主要站台部署單一 VMM 伺服器 hello 和複寫 VM tooa 此次要站台使用站台復原 」 和 「 HYPER-V 複本。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-127">In this scenario, you deploy hello single VMM server as a virtual machine in hello primary site, and replicate this VM tooa secondary site using Site Recovery and Hyper-V Replica.</span></span>

1. <span data-ttu-id="ebdf2-128">**在 Hyper-V VM 上設定 VMM**。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-128">**Set up VMM on a Hyper-V VM**.</span></span> <span data-ttu-id="ebdf2-129">我們建議您將共置 hello hello 上使用 VMM 的 SQL Server 執行個體相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-129">We suggest that you colocate hello SQL Server instance used by VMM on hello same VM.</span></span> <span data-ttu-id="ebdf2-130">這可以節省時間只能有一個 VM 仍為 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-130">This saves time as only one VM has toobe created.</span></span> <span data-ttu-id="ebdf2-131">如果您想 toouse 遠端 SQL Server 執行個體發生中斷，您需要 toorecover 該執行個體之前，您可以復原 VMM。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-131">If you want toouse remote instance of SQL Server and an outage occurs, you need toorecover that instance before you can recover VMM.</span></span>
2. <span data-ttu-id="ebdf2-132">**請 hello VMM 伺服器已設定至少兩個雲端**。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-132">**Ensure hello VMM server has at least two clouds configured**.</span></span> <span data-ttu-id="ebdf2-133">一個雲端會包含您想 tooreplicate 和 hello 其他雲端的 Vm 將做為 hello 次要位置的 hello。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-133">One cloud will contain hello VMs you want tooreplicate and hello other cloud will serve as hello secondary location.</span></span> <span data-ttu-id="ebdf2-134">hello，其中包含您想要 tooprotect 應遵守的 hello Vm 雲端[必要條件](#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-134">hello cloud that contains hello VMs you want tooprotect should comply with [prerequisites](#prerequisites).</span></span>
3. <span data-ttu-id="ebdf2-135">以本文所述的方式設定 Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-135">Set up Site Recovery as described in this article.</span></span> <span data-ttu-id="ebdf2-136">建立及註冊保存庫中的 hello VMM 伺服器、 設定的複寫原則，並啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-136">Create and register hello VMM server in a vault, set up a replication policy, and enable replication.</span></span> <span data-ttu-id="ebdf2-137">hello 來源與目標 VMM 名稱將 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-137">hello source and target VMM names will be hello same.</span></span> <span data-ttu-id="ebdf2-138">指定初始複寫會透過 hello 網路進行。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-138">Specify that initial replication takes place over hello network.</span></span>
4. <span data-ttu-id="ebdf2-139">當您設定網路對應會對應 hello hello 主要雲端 toohello hello 次要雲端的 VM 網路的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-139">When you set up network mapping you map hello VM network for hello primary cloud toohello VM network for hello secondary cloud.</span></span>
5. <span data-ttu-id="ebdf2-140">在 hello HYPER-V 管理員主控台中，包含 hello VMM VM 的 hello HYPER-V 主機上啟用 HYPER-V 複本和 hello VM 上啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-140">In hello Hyper-V Manager console, enable Hyper-V Replica on hello Hyper-V host that contains hello VMM VM, and enable replication on hello VM.</span></span> <span data-ttu-id="ebdf2-141">請確定您不要新增 hello VMM 虛擬機器 tooclouds Site recovery，tooensure HYPER-V 複本設定不覆寫 Site recovery 保護。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-141">Make sure you don't add hello VMM virtual machine tooclouds that are protected by Site Recovery, tooensure that Hyper-V Replica settings aren't overridden by Site Recovery.</span></span>
6. <span data-ttu-id="ebdf2-142">如果您建立您所使用的容錯移轉的復原計劃 hello 相同的 VMM 伺服器，來源和目標。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-142">If you create recovery plans for failover you use hello same VMM server for source and target.</span></span>
7. <span data-ttu-id="ebdf2-143">在完全中斷運作的情況下，您進行容錯移轉和復原的方式如下︰</span><span class="sxs-lookup"><span data-stu-id="ebdf2-143">In a complete outage, you fail over and recover as follows:</span></span>

   1. <span data-ttu-id="ebdf2-144">Hello hello 次要站台中，toofail hello 主要 VMM VM toohello 次要站台上的 HYPER-V Manager 主控台中，執行未規劃的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-144">Run an unplanned failover in hello Hyper-V Manager console in hello secondary site, toofail over hello primary VMM VM toohello secondary site.</span></span>
   2. <span data-ttu-id="ebdf2-145">請確認 VMM VM 已啟動該 hello 並正常執行，並在 hello 保存庫 hello Vm 上執行規劃的容錯移轉 toofail 從主要 toosecondary 雲端。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-145">Verify that hello VMM VM is up and running, and in hello vault, run an unplanned failover toofail over hello VMs from primary toosecondary clouds.</span></span> <span data-ttu-id="ebdf2-146">認可 hello 容錯移轉，並視需要選取替代的復原點。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-146">Commit hello failover, and select an alternate recovery point if required.</span></span>
   3. <span data-ttu-id="ebdf2-147">Hello 規劃的容錯移轉完成之後，所有存取的資源可以從 hello 主要站台一次。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-147">After hello unplanned failover is complete, all resources can be accessed from hello primary site again.</span></span>
   4. <span data-ttu-id="ebdf2-148">同樣地，在 hello hello 次要站台中的 HYPER-V Manager 主控台中可用 hello 主要站台時，啟用 hello VMM VM 的反向複寫。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-148">When hello primary site is available again, in hello Hyper-V Manager console in hello secondary site, enable reverse replication for hello VMM VM.</span></span> <span data-ttu-id="ebdf2-149">這是從次要 tooprimary 開始 hello VM 的複寫。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-149">This starts replication for hello VM from secondary tooprimary.</span></span>
   5. <span data-ttu-id="ebdf2-150">Hello hello 次要站台中，toofail hello VMM VM toohello 主要站台上的 HYPER-V Manager 主控台中執行規劃的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-150">Run a planned failover in hello Hyper-V Manager console in hello secondary site, toofail over hello VMM VM toohello primary site.</span></span> <span data-ttu-id="ebdf2-151">認可 hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-151">Commit hello failover.</span></span> <span data-ttu-id="ebdf2-152">再啟用反向複寫，如此 hello VMM VM 會再次從伺服器複寫主要 toosecondary。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-152">Then enable reverse replication, so that hello VMM VM is again replicating from primary toosecondary.</span></span>
   6. <span data-ttu-id="ebdf2-153">在 hello 復原服務保存庫，讓 hello 工作負載的 Vm，從次要 tooprimary 複寫它們 toostart 的反向複寫。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-153">In hello Recovery Services vault, enable reverse replication for hello workload VMs, toostart replicating them from secondary tooprimary.</span></span>
   7. <span data-ttu-id="ebdf2-154">Hello 復原服務保存庫中，執行規劃的容錯移轉 toofail 後 hello 工作負載 Vm toohello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-154">In hello Recovery Services vault, run a planned failover toofail back hello workload VMs toohello primary site.</span></span> <span data-ttu-id="ebdf2-155">認可 hello 容錯移轉 toocomplete 它。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-155">Commit hello failover toocomplete it.</span></span> <span data-ttu-id="ebdf2-156">然後啟用反向複寫 toostart 複寫 hello 工作負載 Vm 從主要 toosecondary。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-156">Then enable reverse replication toostart replicating hello workload VMs from primary toosecondary.</span></span>

### <a name="replicate-with-a-stretched-vmm-cluster"></a><span data-ttu-id="ebdf2-157">以延伸的 VMM 叢集複寫</span><span class="sxs-lookup"><span data-stu-id="ebdf2-157">Replicate with a stretched VMM cluster</span></span>

<span data-ttu-id="ebdf2-158">而是作為複寫 tooa 次要站台 VM 部署獨立 VMM 伺服器，您可以讓 VMM 高可用性部署為 Windows 容錯移轉叢集中的 VM。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-158">Instead of deploying a standalone VMM server as a VM that replicates tooa secondary site, you can make VMM highly available by deploying it as a VM in a Windows failover cluster.</span></span> <span data-ttu-id="ebdf2-159">這可以提供工作負載彈性及硬體故障的防護。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-159">This provides workload resilience and protection against hardware failure.</span></span> <span data-ttu-id="ebdf2-160">在各地不同的站台之間，應該自動縮放叢集中部署 toodeploy 以 Site Recovery hello VMM VM。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-160">toodeploy with Site Recovery hello VMM VM should be deployed in a stretch cluster across geographically separate sites.</span></span> <span data-ttu-id="ebdf2-161">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="ebdf2-161">toodo this:</span></span>

1. <span data-ttu-id="ebdf2-162">在 Windows 容錯移轉叢集中的虛擬機器上安裝 VMM，並在安裝期間選取 hello 選項 toorun hello 伺服器為高可用性。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-162">Install VMM on a virtual machine in a Windows failover cluster, and select hello option toorun hello server as highly available during setup.</span></span>
2. <span data-ttu-id="ebdf2-163">hello SQL Server 執行個體，以供 VMM 應該複寫使用 SQL Server AlwaysOn 可用性群組，使 hello hello 次要站台資料庫複本。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-163">hello SQL Server instance that's used by VMM should be replicated with SQL Server AlwaysOn availability groups, so that there's a replica of hello database in hello secondary site.</span></span>
3. <span data-ttu-id="ebdf2-164">遵循本文章 toocreate 保存庫中的 hello 指示，註冊 hello 伺服器，以及設定保護。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-164">Follow hello instructions in this article toocreate a vault, register hello server, and set up protection.</span></span> <span data-ttu-id="ebdf2-165">您需要的 tooregister hello 復原服務保存庫中的 hello 中的每部 VMM 伺服器叢集。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-165">You need tooregister each VMM server in hello cluster in hello Recovery Services vault.</span></span> <span data-ttu-id="ebdf2-166">toodo，作用中節點上，安裝 hello 提供者，並註冊 hello VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-166">toodo this, you install hello Provider on an active node, and register hello VMM server.</span></span> <span data-ttu-id="ebdf2-167">然後您可以安裝 hello 提供者的其他節點上。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-167">Then you install hello Provider on other nodes.</span></span>
4. <span data-ttu-id="ebdf2-168">發生中斷時，會容錯移轉，而且從 hello 次要站台存取 hello VMM 伺服器和其相對應的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-168">When an outage occurs, hello VMM server and its corresponding SQL Server database are failed over, and accessed from hello secondary site.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ebdf2-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebdf2-169">Next steps</span></span>

<span data-ttu-id="ebdf2-170">跳過[步驟 5： 設定保存庫](vmm-to-vmm-walkthrough-create-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="ebdf2-170">Go too[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>
