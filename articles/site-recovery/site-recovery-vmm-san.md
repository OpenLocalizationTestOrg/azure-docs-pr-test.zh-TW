---
title: "使用 Azure Site Recovery 以 SAN 複寫 VMM 中的 Hyper-V VM | Microsoft Docs"
description: "本文說明如何使用 SAN 複寫，搭配 Azure Site Recovery 在兩個網站之間複寫 Hyper-V 虛擬機器。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 3df38802fcdc86e4553253d38c49faff455f873e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-to-a-secondary-site-with-azure-site-recovery-by-using-san"></a><span data-ttu-id="b27c3-103">使用 SAN 搭配 Azure Site Recovery 將 VMM 雲端中的 Hyper-V VM 複寫至次要網站</span><span class="sxs-lookup"><span data-stu-id="b27c3-103">Replicate Hyper-V VMs in VMM clouds to a secondary site with Azure Site Recovery by using SAN</span></span>


<span data-ttu-id="b27c3-104">如果您想要部署 [Azure Site Recovery](site-recovery-overview.md)，在傳統入口網站中使用 Azure Site Recovery，以管理將 Hyper-V VM (在 System Center Virtual Machine Manager 雲端中管理) 複寫至次要 VMM 網站，請閱讀本文。</span><span class="sxs-lookup"><span data-stu-id="b27c3-104">Use this article if you want to deploy [Azure Site Recovery](site-recovery-overview.md) to manage replication of Hyper-V VMs (managed in System Center Virtual Machine Manager clouds) to a secondary VMM site, using Azure Site Recovery in the classic portal.</span></span> <span data-ttu-id="b27c3-105">此案例不適用於新的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b27c3-105">This scenario isn't available in the new Azure portal.</span></span>



<span data-ttu-id="b27c3-106">若有任何意見，請張貼於文末。</span><span class="sxs-lookup"><span data-stu-id="b27c3-106">Post any comments at the end of this article.</span></span> <span data-ttu-id="b27c3-107">請至 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 尋找技術問題的解答。</span><span class="sxs-lookup"><span data-stu-id="b27c3-107">Get answers to technical questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="why-replicate-with-san-and-site-recovery"></a><span data-ttu-id="b27c3-108">為什麼使用 SAN 搭配 Site Recovery 進行複寫？</span><span class="sxs-lookup"><span data-stu-id="b27c3-108">Why replicate with SAN and Site Recovery?</span></span>

* <span data-ttu-id="b27c3-109">SAN 提供企業層級、可調整的複寫解決方案，使包含 Hyper-V 與 SAN 的主要網站可利用 SAN 將 LUN 複寫至次要網站。</span><span class="sxs-lookup"><span data-stu-id="b27c3-109">SAN provides an enterprise-level, scalable replication solution so that a primary site containing Hyper-V with SAN can replicate LUNs to a secondary site with SAN.</span></span> <span data-ttu-id="b27c3-110">儲存體由 VMM 管理，複寫及容錯移轉使用 Site Recovery 進行協調。</span><span class="sxs-lookup"><span data-stu-id="b27c3-110">Storage is managed by VMM, and replication and failover is orchestrated with Site Recovery.</span></span>
* <span data-ttu-id="b27c3-111">Site Recovery 與數個 [SAN 存放裝置合作夥伴](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx)合作，提供跨光纖通道及 iSCSI 存放裝置的複寫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-111">Site Recovery has worked with several [SAN storage partners](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) to provide replication across Fibre Channel and iSCSI storage.</span></span>  
* <span data-ttu-id="b27c3-112">利用您現有的 SAN 基礎結構，保護部署在 Hyper-V 叢集中的關鍵任務應用程式。</span><span class="sxs-lookup"><span data-stu-id="b27c3-112">Use your existing SAN infrastructure to protect mission-critical apps deployed in Hyper-V clusters.</span></span> <span data-ttu-id="b27c3-113">VM 可以整組複寫，使多層式架構應用程式可以一致地容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-113">VMs can be replicated as a group so that N-tier apps can be failed over consistently.</span></span>
* <span data-ttu-id="b27c3-114">SAN 複寫藉由低 RTO 與 RPO 的同步複寫，以及高彈性的非同步複寫 (視存放裝置陣列功能而定) 確保不同層應用程式的複寫一致性。</span><span class="sxs-lookup"><span data-stu-id="b27c3-114">SAN replication ensures replication consistency across different tiers of an application with synchronized replication for low RTO and RPO, and asynchronized replication for high flexibility (depending on your storage array capabilities).</span></span>  
* <span data-ttu-id="b27c3-115">您可以在 VMM 網狀架構中管理 SAN 存放裝置，並在 VMM 中使用 SMI-S 探索現有的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="b27c3-115">You can manage SAN storage in the VMM fabric and use SMI-S in VMM to discover existing storage.</span></span>  

<span data-ttu-id="b27c3-116">請注意：</span><span class="sxs-lookup"><span data-stu-id="b27c3-116">Note that:</span></span>
- <span data-ttu-id="b27c3-117">在 Azure 入口網站中無法使用網站對網站複寫搭配 SAN。</span><span class="sxs-lookup"><span data-stu-id="b27c3-117">Site-to-site replication with SAN isn't available in the Azure portal.</span></span> <span data-ttu-id="b27c3-118">只有在傳統入口網站中才能使用。</span><span class="sxs-lookup"><span data-stu-id="b27c3-118">It's only available in the classic portal.</span></span> <span data-ttu-id="b27c3-119">在傳統入口網站中無法建立新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-119">New vaults can't be created in the classic portal.</span></span> <span data-ttu-id="b27c3-120">可以保留現有的保存庫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-120">Existing vaults can be maintained.</span></span>
- <span data-ttu-id="b27c3-121">不支援從 SAN 複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b27c3-121">Replication from SAN to Azure isn't supported.</span></span>
- <span data-ttu-id="b27c3-122">您無法複寫共用 VHDX 或是透過 iSCSI 或光纖通道直接連線到 VM 的邏輯單元 (LUN)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-122">You can't replicate shared VHDXs, or logical units (LUNs) that are directly connected to VMs via iSCSI or Fibre Channel.</span></span> <span data-ttu-id="b27c3-123">可以複寫客體叢集。</span><span class="sxs-lookup"><span data-stu-id="b27c3-123">Guest clusters can be replicated.</span></span>


## <a name="architecture"></a><span data-ttu-id="b27c3-124">架構</span><span class="sxs-lookup"><span data-stu-id="b27c3-124">Architecture</span></span>

![SAN 架構](./media/site-recovery-vmm-san/architecture.png)

- <span data-ttu-id="b27c3-126">**Azure**︰在 Azure 入口網站中設定 Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-126">**Azure**: Set up a Site Recovery vault in the Azure portal.</span></span>
- <span data-ttu-id="b27c3-127">**SAN 存放裝置**︰在 VMM 網狀架構中管理 SAN 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="b27c3-127">**SAN storage**: SAN storage is managed in the VMM fabric.</span></span> <span data-ttu-id="b27c3-128">您新增儲存體提供者、建立儲存體分類，並設定存放集區。</span><span class="sxs-lookup"><span data-stu-id="b27c3-128">You add the storage provider, create storage classifications, and set up storage pools.</span></span>
- <span data-ttu-id="b27c3-129">**VMM 與 Hyper-V**：我們建議一個網站一部 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-129">**VMM and Hyper-V**: We recommend a VMM server in each site.</span></span> <span data-ttu-id="b27c3-130">設定 VMM 私人雲端，並將 Hyper-V 叢集放在這些雲端中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-130">Set up VMM private clouds, and place Hyper-V clusters in those clouds.</span></span> <span data-ttu-id="b27c3-131">部署期間，Azure Site Recovery 提供者是安裝在每部 VMM 伺服器上，伺服器則註冊於保存庫中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-131">During deployment, the Azure Site Recovery Provider is installed on each VMM server, and the server is registered in the vault.</span></span> <span data-ttu-id="b27c3-132">提供者會與 Site Recovery 服務通訊以管理複寫、容錯移轉和容錯回復。</span><span class="sxs-lookup"><span data-stu-id="b27c3-132">The Provider communicates with the Site Recovery service to manage replication, failover, and failback.</span></span>
- <span data-ttu-id="b27c3-133">**複寫**︰在 VMM 中設定儲存體並在 Site Recovery 中設定複寫之後，就會在主要和次要 SAN 存放裝置之間進行複寫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-133">**Replication**: After you set up storage in VMM and configure replication in Site Recovery, replication occurs between the primary and secondary SAN storage.</span></span> <span data-ttu-id="b27c3-134">複寫資料不會傳送至 Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="b27c3-134">No replication data is sent to Site Recovery.</span></span>
- <span data-ttu-id="b27c3-135">**容錯移轉**︰在 Site Recovery 入口網站中啟用容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-135">**Failover**: Enable failover in the Site Recovery portal.</span></span> <span data-ttu-id="b27c3-136">由於複寫是同步作業，容錯移轉期間不會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="b27c3-136">There is zero data loss during failover because replication is synchronous.</span></span>
- <span data-ttu-id="b27c3-137">**容錯回復**︰若要容錯回復，您可以啟用反向複寫，將差異變更從次要網站傳送到主要網站。</span><span class="sxs-lookup"><span data-stu-id="b27c3-137">**Failback**: To fail back, you enable reverse replication to transfer delta changes from the secondary site to the primary site.</span></span> <span data-ttu-id="b27c3-138">反向複寫完成後，則執行從次要到主要的計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-138">After reverse replication is complete, you run a planned failover from secondary to primary.</span></span> <span data-ttu-id="b27c3-139">這個規劃的容錯移轉會停止次要網站上的複本 VM，並在主要網站上啟動它們。</span><span class="sxs-lookup"><span data-stu-id="b27c3-139">This planned failover stops the replica VMs on the secondary site and starts them on the primary site.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="b27c3-140">開始之前</span><span class="sxs-lookup"><span data-stu-id="b27c3-140">Before you start</span></span>


<span data-ttu-id="b27c3-141">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="b27c3-141">**Prerequisites**</span></span> | <span data-ttu-id="b27c3-142">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="b27c3-142">**Details**</span></span>
--- | ---
<span data-ttu-id="b27c3-143">**Azure**</span><span class="sxs-lookup"><span data-stu-id="b27c3-143">**Azure**</span></span> |<span data-ttu-id="b27c3-144">您需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b27c3-144">You need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="b27c3-145">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="b27c3-145">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="b27c3-146">[深入了解](https://azure.microsoft.com/pricing/details/site-recovery/) Site Recovery 價格。</span><span class="sxs-lookup"><span data-stu-id="b27c3-146">[Learn more](https://azure.microsoft.com/pricing/details/site-recovery/) about Site Recovery pricing.</span></span> <span data-ttu-id="b27c3-147">建立 Azure Site Recovery 保存庫來設定和管理複寫及容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-147">Create an Azure Site Recovery vault to configure and manage replication and failover.</span></span>
<span data-ttu-id="b27c3-148">**VMM**</span><span class="sxs-lookup"><span data-stu-id="b27c3-148">**VMM**</span></span> | <span data-ttu-id="b27c3-149">您可以使用單一 VMM 伺服器，並在不同的雲端之間進行複寫，但我們建議在主要網站和次要網站中各部署一個 VMM。</span><span class="sxs-lookup"><span data-stu-id="b27c3-149">You can use a single VMM server and replicate between different clouds, but we recommend one VMM in the primary site and one in the secondary site.</span></span> <span data-ttu-id="b27c3-150">VMM 可部署為實體或虛擬獨立伺服器，或是一個叢集。</span><span class="sxs-lookup"><span data-stu-id="b27c3-150">A VMM can be deployed as a physical or virtual standalone server, or as a cluster.</span></span> <br/><br/><span data-ttu-id="b27c3-151">VMM 伺服器應執行附帶最新累計更新的 System Center 2012 R2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b27c3-151">The VMM server should be running System Center 2012 R2 or later with the latest cumulative updates.</span></span><br/><br/> <span data-ttu-id="b27c3-152">您需要至少有一個雲端設定在您想要保護的主要 VMM 伺服器上，一個雲端要設定在您想要用於容錯移轉的次要 VMM 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b27c3-152">You need at least one cloud configured on the primary VMM server you want to protect and one cloud configured on the secondary VMM server you want to use for failover.</span></span><br/><br/> <span data-ttu-id="b27c3-153">來源雲端必須包含一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-153">The source cloud must contain one or more VMM host groups.</span></span><br/><br/> <span data-ttu-id="b27c3-154">所有的 VMM 雲端都必須設定 Hyper-V 容量設定檔。</span><span class="sxs-lookup"><span data-stu-id="b27c3-154">All VMM clouds must have the Hyper-V Capacity profile set.</span></span><br/><br/> <span data-ttu-id="b27c3-155">如需設定 VMM 雲端的相關資訊，請參閱[部署私人 VM 雲端](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-155">For more about setting up VMM clouds, see [Deploy a private VM cloud](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).</span></span>
<span data-ttu-id="b27c3-156">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="b27c3-156">**Hyper-V**</span></span> | <span data-ttu-id="b27c3-157">在主要和次要 VMM 雲端中，您需要一或多個 Hyper-V 叢集。</span><span class="sxs-lookup"><span data-stu-id="b27c3-157">You need one or more Hyper-V clusters in primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="b27c3-158">來源 Hyper-V 叢集必須包含一或多部 VM。</span><span class="sxs-lookup"><span data-stu-id="b27c3-158">The source Hyper-V cluster must contain one or more VMs.</span></span><br/><br/> <span data-ttu-id="b27c3-159">主要和次要網站中的 VMM 主機群組必須包含至少一個 Hyper-V 叢集。</span><span class="sxs-lookup"><span data-stu-id="b27c3-159">The VMM host groups in the primary and secondary sites must contain at least one of the Hyper-V clusters.</span></span><br/><br/><span data-ttu-id="b27c3-160">主機和目標 Hyper-V 伺服器必須執行 Hyper-V 角色的 Windows Server 2012 或更新版本，並且安裝最新更新。</span><span class="sxs-lookup"><span data-stu-id="b27c3-160">The host and target Hyper-V servers must be running Windows Server 2012 or later with the Hyper-V role and the latest updates installed.</span></span><br/><br/> <span data-ttu-id="b27c3-161">如果您在叢集中執行 Hyper-V，且您具有靜態 IP 位址叢集，則不會自動建立叢集訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="b27c3-161">If you're running Hyper-V in a cluster and have a static IP address-based cluster, cluster broker isn't created automatically.</span></span> <span data-ttu-id="b27c3-162">您必須手動進行設定。</span><span class="sxs-lookup"><span data-stu-id="b27c3-162">You must configure it manually.</span></span> <span data-ttu-id="b27c3-163">如需詳細資訊，請參閱[準備 Hyper-V 複本的主機叢集](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-163">For more information, see [Preparing host clusters for Hyper-V replica](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters).</span></span>
<span data-ttu-id="b27c3-164">**SAN 儲存體**</span><span class="sxs-lookup"><span data-stu-id="b27c3-164">**SAN storage**</span></span> | <span data-ttu-id="b27c3-165">您可以藉由 iSCSI 或光纖通道存放裝置，或藉由使用共用虛擬硬碟 (vhdx)，複寫客體叢集化虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-165">You can replicate guest-clustered virtual machines with iSCSI or channel storage, or by using shared virtual hard disks (vhdx).</span></span><br/><br/> <span data-ttu-id="b27c3-166">您需要兩個 SAN 陣列：一個在主要網站中，一個在次要網站中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-166">You need two SAN arrays: one in the primary site, and one in the secondary site.</span></span><br/><br/> <span data-ttu-id="b27c3-167">網路基礎結構應設定在陣列之間。</span><span class="sxs-lookup"><span data-stu-id="b27c3-167">A network infrastructure should be set up between the arrays.</span></span> <span data-ttu-id="b27c3-168">應該設定對等互連和複寫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-168">Peering and replication should be configured.</span></span> <span data-ttu-id="b27c3-169">應該根據存放裝置陣列需求設定複寫授權。</span><span class="sxs-lookup"><span data-stu-id="b27c3-169">Replication licenses should be set up in accordance with the storage array requirements.</span></span><br/><br/><span data-ttu-id="b27c3-170">在 Hyper-V 主機伺服器與存放裝置陣列之間設定網路功能，讓主機可以使用 iSCSI 或光纖通道與存放裝置 LUN 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b27c3-170">Set up networking between the Hyper-V host servers and the storage array so that hosts can communicate with storage LUNs by using iSCSI or Fibre Channel.</span></span><br/><br/> <span data-ttu-id="b27c3-171">請參閱[支援的儲存體陣列](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-171">Check [supported storage arrays](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).</span></span><br/><br/> <span data-ttu-id="b27c3-172">應該安裝存放裝置陣列製造商所提供的 SMI-S 提供者，並且應該由此提供者管理 SAN 陣列。</span><span class="sxs-lookup"><span data-stu-id="b27c3-172">SMI-S providers from storage array manufacturers should be installed, and the SAN arrays should be managed by the provider.</span></span> <span data-ttu-id="b27c3-173">依照製造商指示設定提供者。</span><span class="sxs-lookup"><span data-stu-id="b27c3-173">Set up the Provider according to manufacturer instructions.</span></span><br/><br/><span data-ttu-id="b27c3-174">確定陣列的 SMI-S 提供者所在的伺服器，是 VMM 伺服器可透過網路以 IP 位址或 FQDN 存取的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-174">Make sure that the array's SMI-S provider is on a server that the VMM server can access over the network with an IP address or FQDN.</span></span><br/><br/> <span data-ttu-id="b27c3-175">每個 SAN 陣列都應該要有一或多個可用的存放集區。</span><span class="sxs-lookup"><span data-stu-id="b27c3-175">Each SAN array should have one or more available storage pools.</span></span><br/><br/> <span data-ttu-id="b27c3-176">主要 VMM 伺服器應該管理主要陣列，而次要 VMM 伺服器應該管理次要陣列。</span><span class="sxs-lookup"><span data-stu-id="b27c3-176">The primary VMM server should manage the primary array, and the secondary VMM server should manage the secondary array.</span></span>
<span data-ttu-id="b27c3-177">**網路對應**</span><span class="sxs-lookup"><span data-stu-id="b27c3-177">**Network mapping**</span></span> | <span data-ttu-id="b27c3-178">設定網路對應，以確保在容錯移轉後，會以最佳方式將已複寫的虛擬機器置於次要 Hyper-V 主機伺服器上，使這些虛擬機器可以連線到適當的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-178">Set up network mapping so that replicated virtual machines are optimally placed on secondary Hyper-V host servers after failover, and so that they're connected to appropriate VM networks.</span></span> <span data-ttu-id="b27c3-179">如果您沒有設定網路對應，複本 VM 將不會在容錯移轉之後連接到任何網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-179">If you don't configure network mapping, replica VMs won't be connected to any network after failover.</span></span><br/><br/> <span data-ttu-id="b27c3-180">請確定 VMM 網路設定正確，才能在 Site Recovery 部署期間設定網路對應。</span><span class="sxs-lookup"><span data-stu-id="b27c3-180">Make sure that VMM networks are configured correctly so that you can set up network mapping during Site Recovery deployment.</span></span> <span data-ttu-id="b27c3-181">在 VMM 中，來源 Hyper-V 主機上的 VM 應連線到 VMM VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-181">In VMM, the VMs on the source Hyper-V host should be connected to a VMM VM network.</span></span> <span data-ttu-id="b27c3-182">該網路應該連結到與雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-182">That network should be linked to a logical network that is associated with the cloud.</span></span><br/><br/> <span data-ttu-id="b27c3-183">目標雲端應該設定相對應的 VM 網路，而該網路應該連結到與目標雲端相關聯的相對應邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-183">The target cloud should have a corresponding VM network, and it in turn should be linked to a corresponding logical network that is associated with the target cloud.</span></span><br/><br/><span data-ttu-id="b27c3-184">。</span><span class="sxs-lookup"><span data-stu-id="b27c3-184">.</span></span>

## <a name="step-1-prepare-the-vmm-infrastructure"></a><span data-ttu-id="b27c3-185">步驟 1：準備 VMM 基礎結構</span><span class="sxs-lookup"><span data-stu-id="b27c3-185">Step 1: Prepare the VMM infrastructure</span></span>
<span data-ttu-id="b27c3-186">若要準備您的 VMM 基礎結構，您需要：</span><span class="sxs-lookup"><span data-stu-id="b27c3-186">To prepare your VMM infrastructure, you need to:</span></span>

1. <span data-ttu-id="b27c3-187">確認 VMM 雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-187">Verify VMM clouds.</span></span>
2. <span data-ttu-id="b27c3-188">將 VMM 中的 SAN 存放裝置整合並分類。</span><span class="sxs-lookup"><span data-stu-id="b27c3-188">Integrate and classify SAN storage in VMM.</span></span>
3. <span data-ttu-id="b27c3-189">建立 LUN 並配置存放裝置。</span><span class="sxs-lookup"><span data-stu-id="b27c3-189">Create LUNs and allocate storage.</span></span>
4. <span data-ttu-id="b27c3-190">建立複寫群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-190">Create replication groups.</span></span>
5. <span data-ttu-id="b27c3-191">設定 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-191">Set up VM networks.</span></span>

### <a name="verify-vmm-clouds"></a><span data-ttu-id="b27c3-192">確認 VMM 雲端</span><span class="sxs-lookup"><span data-stu-id="b27c3-192">Verify VMM clouds</span></span>

<span data-ttu-id="b27c3-193">開始 Site Recovery 部署之前，請確定您的 VMM 雲端已妥善設定。</span><span class="sxs-lookup"><span data-stu-id="b27c3-193">Make sure your VMM clouds are set up properly before you begin Site Recovery deployment.</span></span>

### <a name="integrate-and-classify-san-storage-in-the-vmm-fabric"></a><span data-ttu-id="b27c3-194">將 VMM 網狀架構中的 SAN 存放裝置整合並分類</span><span class="sxs-lookup"><span data-stu-id="b27c3-194">Integrate and classify SAN storage in the VMM fabric</span></span>

1. <span data-ttu-id="b27c3-195">在 VMM 主控台，移至 [網狀架構] > [儲存體] > [新增資源] > [存放裝置]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-195">In the VMM console, go to **Fabric** > **Storage** > **Add Resources** > **Storage Devices**.</span></span>
2. <span data-ttu-id="b27c3-196">在 [新增存放裝置]精靈中，選取 [選取存放裝置提供者類型]，然後選取 [由 SMI-S 提供者探索到及管理的 SAN 和 NAS 裝置]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-196">In the **Add Storage Devices** wizard, select **Select a storage provider type** and select **SAN and NAS devices discovered and managed by an SMI-S provider**.</span></span>

    ![提供者類型](./media/site-recovery-vmm-san/provider-type.png)

3. <span data-ttu-id="b27c3-198">在 [指定儲存 SMI-S 提供者的通訊協定與位址] 頁面上，選取 [SMI-S CIMXML]，並指定用來連線到提供者的設定。</span><span class="sxs-lookup"><span data-stu-id="b27c3-198">On the **Specify Protocol and Address of the Storage SMI-S Provider** page, select **SMI-S CIMXML** and specify the settings for connecting to the provider.</span></span>
4. <span data-ttu-id="b27c3-199">在 [提供者 IP 位址或 FQDN] 和 [TCP/IP 連接埠] 中，指定用來連線到提供者的設定。</span><span class="sxs-lookup"><span data-stu-id="b27c3-199">In **Provider IP address or FQDN** and **TCP/IP port**, specify the settings for connecting to the provider.</span></span> <span data-ttu-id="b27c3-200">您只能針對 SMI-S CIMXML 使用 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="b27c3-200">You can use an SSL connection for SMI-S CIMXML only.</span></span>

    ![提供者連接](./media/site-recovery-vmm-san/connect-settings.png)
5. <span data-ttu-id="b27c3-202">在 [執行身分帳戶] 中，指定一個可以存取提供者的 VMM 執行身分帳戶，或建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="b27c3-202">In **Run as account**, specify a VMM Run As account that can access the provider, or create an account.</span></span>
6. <span data-ttu-id="b27c3-203">在 [收集資訊]  頁面上，VMM 會自動嘗試探索並匯入存放裝置資訊。</span><span class="sxs-lookup"><span data-stu-id="b27c3-203">On the **Gather Information** page, VMM automatically tries to discover and import the storage device information.</span></span> <span data-ttu-id="b27c3-204">若要重新嘗試探索，請按一下 [掃描提供者] 。</span><span class="sxs-lookup"><span data-stu-id="b27c3-204">To retry discovery, click **Scan Provider**.</span></span> <span data-ttu-id="b27c3-205">如果探索程序成功，頁面上就會列出探索到的存放裝置陣列、存放集區、製造商、型號及容量。</span><span class="sxs-lookup"><span data-stu-id="b27c3-205">If the discovery process succeeds, the discovered storage arrays, storage pools, manufacturer, model, and capacity are listed on the page.</span></span>

    ![探索儲存體](./media/site-recovery-vmm-san/discover.png)
7. <span data-ttu-id="b27c3-207">在 [選取要列入管理的存放集區並指派分類] 中，選取 VMM 將管理的存放集區，並為它們指派一個分類。</span><span class="sxs-lookup"><span data-stu-id="b27c3-207">In **Select storage pools to place under management and assign a classification**, select the storage pools that VMM will manage and assign them a classification.</span></span> <span data-ttu-id="b27c3-208">LUN 資訊會從存放集區匯入。</span><span class="sxs-lookup"><span data-stu-id="b27c3-208">LUN information is imported from the storage pools.</span></span> <span data-ttu-id="b27c3-209">請根據您需要保護的應用程式、其容量需求，以及您對於哪些項目要一起複寫的需求，建立 LUN。</span><span class="sxs-lookup"><span data-stu-id="b27c3-209">Create LUNs based on the applications you need to protect, their capacity requirements, and your requirements for what needs to replicate together.</span></span>

    ![分類儲存體](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a><span data-ttu-id="b27c3-211">建立 LUN 並配置存放裝置</span><span class="sxs-lookup"><span data-stu-id="b27c3-211">Create LUNs and allocate storage</span></span>

<span data-ttu-id="b27c3-212">請根據您需要保護的應用程式、容量需求，以及您對於哪些項目要一起複寫的需求，建立 LUN。</span><span class="sxs-lookup"><span data-stu-id="b27c3-212">Create LUNs based on the applications you need to protect, capacity requirements, and your requirements for what needs to replicate together.</span></span>

1. <span data-ttu-id="b27c3-213">存放裝置出現在 VMM 網狀架構之後，您可以[佈建 LUN](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-213">After the storage appears in the VMM fabric, you can [provision LUNs](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).</span></span>

     > [!NOTE]
     > <span data-ttu-id="b27c3-214">請勿將已啟用複寫的 VM 的 VHD 新增到 LUN。</span><span class="sxs-lookup"><span data-stu-id="b27c3-214">Don't add VHDs for the VM that are enabled for replication to LUNs.</span></span> <span data-ttu-id="b27c3-215">如果這些 LUN 不在 Site Recovery 複寫群組中，Site Recovery 不會偵測到它們。</span><span class="sxs-lookup"><span data-stu-id="b27c3-215">If those LUNs aren't in a Site Recovery replication group, they won't be detected by Site Recovery.</span></span>
     >

2. <span data-ttu-id="b27c3-216">配置儲存容量給 Hyper-V 主機叢集，讓 VMM 可以將虛擬機器資料部署到已佈建的存放裝置上：</span><span class="sxs-lookup"><span data-stu-id="b27c3-216">Allocate storage capacity to the Hyper-V host cluster so that VMM can deploy virtual machine data to the provisioned storage:</span></span>

   * <span data-ttu-id="b27c3-217">將存放裝置配置給叢集之前，您必須先將其配置給叢集所在的 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-217">Before allocating storage to the cluster, you need to allocate it to the VMM host group on which the cluster resides.</span></span> <span data-ttu-id="b27c3-218">如需詳細資訊，請參閱[如何將存放裝置邏輯單元配置給 VMM 中的主機群組](https://technet.microsoft.com/library/gg610686.aspx)及[如何將存放集區配置給 VMM 中的主機群組](https://technet.microsoft.com/library/gg610635.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-218">For more information, see [How to allocate storage logical units to a host group in VMM](https://technet.microsoft.com/library/gg610686.aspx) and [How to allocate storage pools to a host group in VMM](https://technet.microsoft.com/library/gg610635.aspx).</span></span>
   * <span data-ttu-id="b27c3-219">依照[如何在 VMM 中設定 Hyper-V 主機叢集上的存放裝置](https://technet.microsoft.com/library/gg610692.aspx)中所述，配置儲存容量給叢集。</span><span class="sxs-lookup"><span data-stu-id="b27c3-219">Allocate storage capacity to the cluster as described in [How to configure storage on a Hyper-V host cluster in VMM](https://technet.microsoft.com/library/gg610692.aspx).</span></span>

    ![提供者類型](./media/site-recovery-vmm-san/provider-type.png)
3. <span data-ttu-id="b27c3-221">在 [請指定儲存 SMI-S 提供者的通訊協定與位址]中，選取 [SMI-S CIMXML]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-221">In **Specify Protocol and Address of the Storage SMI-S Provider**, select **SMI-S CIMXML**.</span></span> <span data-ttu-id="b27c3-222">指定連接到提供者的設定。</span><span class="sxs-lookup"><span data-stu-id="b27c3-222">Specify the settings for connecting to the provider.</span></span> <span data-ttu-id="b27c3-223">您只能針對 SMI-S CIMXML 使用 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="b27c3-223">You can use an SSL connection only for SMI-S CIMXML.</span></span>

    ![提供者連接](./media/site-recovery-vmm-san/connect-settings.png)
4. <span data-ttu-id="b27c3-225">在 [執行身分帳戶] 中，指定一個可以存取提供者的 VMM 執行身分帳戶，或建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="b27c3-225">In **Run as account**, specify a VMM Run As account that can access the provider, or create an account.</span></span>
5. <span data-ttu-id="b27c3-226">在 [收集資訊]  中，VMM 會自動嘗試探索並匯入存放裝置資訊。</span><span class="sxs-lookup"><span data-stu-id="b27c3-226">In **Gather Information**, VMM automatically tries to discover and import the storage device information.</span></span> <span data-ttu-id="b27c3-227">若需要重試，請按一下 [掃描提供者]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-227">If you need to retry, click **Scan Provider**.</span></span> <span data-ttu-id="b27c3-228">當探索程序成功時，頁面上就會列出存放裝置陣列、存放集區、製造商、型號及容量。</span><span class="sxs-lookup"><span data-stu-id="b27c3-228">When the discovery process succeeds, the storage arrays, storage pools, manufacturer, model, and capacity are listed on the page.</span></span>

    ![探索儲存體](./media/site-recovery-vmm-san/discover.png)
7. <span data-ttu-id="b27c3-230">在 [選取要列入管理的存放集區並指派分類] 中，選取 VMM 將管理的存放集區，並為它們指派一個分類。</span><span class="sxs-lookup"><span data-stu-id="b27c3-230">In **Select storage pools to place under management and assign a classification**, select the storage pools that VMM will manage, and assign them a classification.</span></span> <span data-ttu-id="b27c3-231">LUN 資訊會從存放集區匯入。</span><span class="sxs-lookup"><span data-stu-id="b27c3-231">LUN information is imported from the storage pools.</span></span>

    ![分類儲存體](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a><span data-ttu-id="b27c3-233">建立複寫群組</span><span class="sxs-lookup"><span data-stu-id="b27c3-233">Create replication groups</span></span>

<span data-ttu-id="b27c3-234">建立複寫群組，其中包含所有需要一起進行複寫的 LUN。</span><span class="sxs-lookup"><span data-stu-id="b27c3-234">Create a replication group that includes all the LUNs that will need to replicate together.</span></span>

1. <span data-ttu-id="b27c3-235">在 VMM 主控台中，開啟存放裝置陣列屬性的 [複寫群組] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-235">In the VMM console, open the **Replication Groups** tab of the storage array properties, and then click **New**.</span></span>
2. <span data-ttu-id="b27c3-236">建立複寫群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-236">Create the replication group.</span></span>

    ![SAN 複寫群組](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a><span data-ttu-id="b27c3-238">設定網路</span><span class="sxs-lookup"><span data-stu-id="b27c3-238">Set up networks</span></span>

<span data-ttu-id="b27c3-239">如果您想要設定網路對應，請執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="b27c3-239">If you want to configure network mapping, do the following:</span></span>

1. <span data-ttu-id="b27c3-240">請參閱 Site Recovery 網路對應。</span><span class="sxs-lookup"><span data-stu-id="b27c3-240">See Site Recovery network mapping.</span></span>
2. <span data-ttu-id="b27c3-241">在 VMM 中準備 VM 網路：</span><span class="sxs-lookup"><span data-stu-id="b27c3-241">Prepare VM networks in VMM:</span></span>

   * <span data-ttu-id="b27c3-242">[設定邏輯網路](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-242">[Set up logical networks](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).</span></span>
   * <span data-ttu-id="b27c3-243">[設定 VM 網路](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-243">[Set up VM networks](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).</span></span>


## <a name="step-2-create-a-vault"></a><span data-ttu-id="b27c3-244">步驟 2：建立保存庫</span><span class="sxs-lookup"><span data-stu-id="b27c3-244">Step 2: Create a vault</span></span>

1. <span data-ttu-id="b27c3-245">從您想要在保存庫中註冊的 VMM 伺服器登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-245">Sign in to the [Azure portal](https://portal.azure.com) from the VMM server you want to register in the vault.</span></span>
2. <span data-ttu-id="b27c3-246">展開 [資料服務] > [復原服務]，然後按一下 [Site Recovery 保存庫]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-246">Expand **Data Services** > **Recovery Services**, and then click **Site Recovery Vault**.</span></span>
3. <span data-ttu-id="b27c3-247">按一下 [新建]  >  [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-247">Click **Create New** > **Quick Create**.</span></span>
4. <span data-ttu-id="b27c3-248">在 [ **名稱**] 中，輸入保存庫的易記識別名稱。</span><span class="sxs-lookup"><span data-stu-id="b27c3-248">In **Name**, enter a friendly name to identify the vault.</span></span>
5. <span data-ttu-id="b27c3-249">在 [區域] 中，選取保存庫的地理區域。</span><span class="sxs-lookup"><span data-stu-id="b27c3-249">In **Region**, select the geographic region for the vault.</span></span> <span data-ttu-id="b27c3-250">若要查看支援的地區，請參閱 [Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-250">To check supported regions, see [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
6. <span data-ttu-id="b27c3-251">按一下 [建立保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="b27c3-251">Click **Create vault**.</span></span>

    ![新增保存庫](./media/site-recovery-vmm-san/create-vault.png)

<span data-ttu-id="b27c3-253">檢查狀態列，以確認是否順利建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-253">Check the status bar to confirm that the vault was successfully created.</span></span> <span data-ttu-id="b27c3-254">保存庫在主要 [復原服務] 頁面上會列為 [使用中]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-254">The vault will be listed as **Active** on the main **Recovery Services** page.</span></span>

### <a name="register-the-vmm-servers"></a><span data-ttu-id="b27c3-255">註冊 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="b27c3-255">Register the VMM servers</span></span>

1. <span data-ttu-id="b27c3-256">從 [復原服務] 頁面開啟 [快速啟動] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b27c3-256">Open the **Quick Start** page from the **Recovery Services** page.</span></span> <span data-ttu-id="b27c3-257">您也可以選擇圖示隨時開啟 [快速啟動]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-257">Quick Start can also be opened at any time by choosing the icon.</span></span>

    ![快速啟動圖示](./media/site-recovery-vmm-san/quick-start-icon.png)
2. <span data-ttu-id="b27c3-259">在下拉式清單方塊中，選取 [在使用陣列複寫的 Hyper-V 內部部署站台之間]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-259">In the drop-down box, select **Between Hyper-V on-premises site using array replication**.</span></span>

    ![註冊金鑰](./media/site-recovery-vmm-san/select-san.png)
3. <span data-ttu-id="b27c3-261">在 [準備 VMM 伺服器] 中，下載最新版本的 Azure Site Recovery 提供者安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="b27c3-261">In **Prepare VMM servers**, download the latest version of the Azure Site Recovery Provider installation file.</span></span>
4. <span data-ttu-id="b27c3-262">在來源 VMM 伺服器上執行此檔案。</span><span class="sxs-lookup"><span data-stu-id="b27c3-262">Run this file on the source VMM server.</span></span> <span data-ttu-id="b27c3-263">如果 VMM 部署在叢集中，且您是第一次安裝提供者，請將提供者安裝在作用中節點上，並完成安裝以在保存庫中註冊 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-263">If VMM is deployed in a cluster and you're installing the Provider for the first time, install the Provider on an active node and finish the installation to register the VMM server in the vault.</span></span> <span data-ttu-id="b27c3-264">然後在其他節點上安裝提供者。</span><span class="sxs-lookup"><span data-stu-id="b27c3-264">Then install the Provider on the other nodes.</span></span> <span data-ttu-id="b27c3-265">如果您要升級提供者，您必須在所有節點上升級，使它們有相同的提供者版本。</span><span class="sxs-lookup"><span data-stu-id="b27c3-265">If you're upgrading the Provider, you need to upgrade on all nodes so that they have the same Provider version.</span></span>
5. <span data-ttu-id="b27c3-266">安裝程式會檢查需求，並要求停止 VMM 服務的權限，以便開始安裝提供者。</span><span class="sxs-lookup"><span data-stu-id="b27c3-266">The installer checks requirements and requests permission to stop the VMM service to begin Provider setup.</span></span> <span data-ttu-id="b27c3-267">當安裝完成之後，服務將會自動重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b27c3-267">The service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="b27c3-268">在 VMM 叢集上，您會收到停止叢集角色的提示。</span><span class="sxs-lookup"><span data-stu-id="b27c3-268">On a VMM cluster, you'll be prompted to stop the Cluster role.</span></span>
6. <span data-ttu-id="b27c3-269">在 [Microsoft Update] 中，您可以選擇進行更新，將會根據您的 Microsoft Update 原則安裝提供者更新。</span><span class="sxs-lookup"><span data-stu-id="b27c3-269">In **Microsoft Update**, you can opt in for updates, and Provider updates will be installed according to your Microsoft Update policy.</span></span>

    ![Microsoft Update](./media/site-recovery-vmm-san/ms-update.png)

7. <span data-ttu-id="b27c3-271">根據預設，提供者的安裝位置為 <SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin。</span><span class="sxs-lookup"><span data-stu-id="b27c3-271">By default, the install location for the Provider is <SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin.</span></span> <span data-ttu-id="b27c3-272">按一下 [安裝] 以開始。</span><span class="sxs-lookup"><span data-stu-id="b27c3-272">Click **Install** to begin.</span></span>

    ![安裝位置](./media/site-recovery-vmm-san/install-location.png)

8. <span data-ttu-id="b27c3-274">安裝提供者之後，請按一下 [註冊]，在保存庫中註冊 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-274">After the Provider is installed, click **Register** to register the VMM server in the vault.</span></span>

    ![安裝完成](./media/site-recovery-vmm-san/install-complete.png)

9. <span data-ttu-id="b27c3-276">在 [網際網路連線] 中，指定提供者連線到網際網路的方式。</span><span class="sxs-lookup"><span data-stu-id="b27c3-276">In **Internet Connection**, specify how the Provider connects to the Internet.</span></span> <span data-ttu-id="b27c3-277">如果您想使用伺服器上的預設網際網路連線設定，請選取 [使用預設的系統 Proxy 設定]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-277">Select **Use default system proxy settings** if you want to use the default Internet connection settings on the server.</span></span>

    ![網際網路設定](./media/site-recovery-vmm-san/proxy-details.png)

   * <span data-ttu-id="b27c3-279">如果您想要使用自訂的 Proxy，請在安裝提供者之前先設定它。</span><span class="sxs-lookup"><span data-stu-id="b27c3-279">If you want to use a custom proxy, set it up before you install the Provider.</span></span> <span data-ttu-id="b27c3-280">當您進行自訂 Proxy 設定時，會執行一項測試以檢查 Proxy 連線。</span><span class="sxs-lookup"><span data-stu-id="b27c3-280">When you configure custom proxy settings, a test runs to check the proxy connection.</span></span>
   * <span data-ttu-id="b27c3-281">如果您使用自訂 proxy，或者您的預設 proxy 需要驗證，您應輸入 Proxy 詳細資料，包含位址和連接埠。</span><span class="sxs-lookup"><span data-stu-id="b27c3-281">If you do use a custom proxy, or if your default proxy requires authentication, you should enter the proxy details, including the address and port.</span></span>
   * <span data-ttu-id="b27c3-282">必須能夠從 VMM 伺服器存取必要的 URL。</span><span class="sxs-lookup"><span data-stu-id="b27c3-282">The required URLs should be accessible from the VMM server.</span></span>
   * <span data-ttu-id="b27c3-283">如果您使用的是自訂 proxy，則會使用指定的 proxy 認證自動建立 VMM RunAs 帳戶 (DRAProxyAccount)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-283">If you use a custom proxy, a VMM Run As account (DRAProxyAccount) is created automatically by using the specified proxy credentials.</span></span> <span data-ttu-id="b27c3-284">設定 Proxy 伺服器，讓此帳戶可以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b27c3-284">Configure the proxy server so that this account can authenticate.</span></span> <span data-ttu-id="b27c3-285">您可以在 VMM 主控台修改 RunAs 帳戶設定 ([設定]  > [安全性] > [執行身分帳戶] > [DRAProxyAccount])。</span><span class="sxs-lookup"><span data-stu-id="b27c3-285">You can modify the Run As account settings in the VMM console (**Settings** > **Security** > **Run As Accounts** > **DRAProxyAccount**).</span></span> <span data-ttu-id="b27c3-286">您必須重新啟動 VMM 服務，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="b27c3-286">You must restart the VMM service for the change to take effect.</span></span>
10. <span data-ttu-id="b27c3-287">在 [註冊金鑰] 中，選取您從入口網站下載並複製到 VMM 伺服器的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b27c3-287">In **Registration Key**, select the key that you downloaded from the portal and copied to the VMM server.</span></span>
11. <span data-ttu-id="b27c3-288">在 [保存庫名稱] 中，確認要註冊伺服器的保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="b27c3-288">In **Vault name**, verify the name of the vault in which the server will be registered.</span></span>

    ![伺服器註冊](./media/site-recovery-vmm-san/vault-creds.png)
12. <span data-ttu-id="b27c3-290">加密設定僅用於 VMM 至 Azure 的複寫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-290">The encryption setting is only used for VMM to Azure replication.</span></span> <span data-ttu-id="b27c3-291">您可以忽略它。</span><span class="sxs-lookup"><span data-stu-id="b27c3-291">You can ignore it.</span></span>

    ![伺服器註冊](./media/site-recovery-vmm-san/encrypt.png)
13. <span data-ttu-id="b27c3-293">在 [伺服器名稱] 中，指定保存庫中 VMM 伺服器的易記識別名稱。</span><span class="sxs-lookup"><span data-stu-id="b27c3-293">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="b27c3-294">在叢集設定中，指定 VMM 叢集角色名稱。</span><span class="sxs-lookup"><span data-stu-id="b27c3-294">In a cluster configuration, specify the VMM cluster role name.</span></span>
14. <span data-ttu-id="b27c3-295">在 [初始雲端中繼資料同步] 中，選取您是否要將 VMM 伺服器上所有雲端的中繼資料同步。</span><span class="sxs-lookup"><span data-stu-id="b27c3-295">In **Initial cloud metadata sync**, select whether you want to synchronize metadata for all clouds on the VMM server.</span></span> <span data-ttu-id="b27c3-296">這個動作只需要在每個伺服器上進行一次。</span><span class="sxs-lookup"><span data-stu-id="b27c3-296">This action only needs to happen once on each server.</span></span> <span data-ttu-id="b27c3-297">如果不要同步所有雲端，您可以取消核取這項設定，再於 VMM 主控台的雲端屬性中個別同步每個雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-297">If you don't want to synchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in the cloud properties in the VMM console.</span></span>

    ![伺服器註冊](./media/site-recovery-vmm-san/friendly-name.png)

15. <span data-ttu-id="b27c3-299">按 [下一步]  ，完成此程序。</span><span class="sxs-lookup"><span data-stu-id="b27c3-299">Click **Next** to complete the process.</span></span> <span data-ttu-id="b27c3-300">註冊後，Azure Site Recovery 即可從 VMM 伺服器擷取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b27c3-300">After registration, metadata from the VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="b27c3-301">伺服器將顯示於保存庫中的 [伺服器]  >  [VMM伺服器] 中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-301">The server is displayed in **Servers** > **VMM Servers** in the vault.</span></span>

### <a name="command-line-installation"></a><span data-ttu-id="b27c3-302">命令列安裝</span><span class="sxs-lookup"><span data-stu-id="b27c3-302">Command-line installation</span></span>

<span data-ttu-id="b27c3-303">您也可以使用下列命令列來安裝 Azure Site Recovery 提供者。</span><span class="sxs-lookup"><span data-stu-id="b27c3-303">The Azure Site Recovery Provider can also be installed by using the following command line.</span></span> <span data-ttu-id="b27c3-304">這個方法可以用來在適用於 Windows Server 2012 R2 的伺服器核心上安裝提供者。</span><span class="sxs-lookup"><span data-stu-id="b27c3-304">This method can be used to install the provider on Server Core for Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="b27c3-305">將提供者安裝檔案和註冊金鑰下載至資料夾。</span><span class="sxs-lookup"><span data-stu-id="b27c3-305">Download the Provider installation file and registration key to a folder.</span></span> <span data-ttu-id="b27c3-306">例如，C:\ASR。</span><span class="sxs-lookup"><span data-stu-id="b27c3-306">For example, C:\ASR.</span></span>
2. <span data-ttu-id="b27c3-307">停止 VMM 服務。</span><span class="sxs-lookup"><span data-stu-id="b27c3-307">Stop the VMM service.</span></span>
3. <span data-ttu-id="b27c3-308">解壓縮提供者安裝程式。</span><span class="sxs-lookup"><span data-stu-id="b27c3-308">Extract the Provider installer.</span></span> <span data-ttu-id="b27c3-309">以系統管理員身分執行這些命令︰</span><span class="sxs-lookup"><span data-stu-id="b27c3-309">Run these commands as an administrator:</span></span>

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. <span data-ttu-id="b27c3-310">安裝提供者：</span><span class="sxs-lookup"><span data-stu-id="b27c3-310">Install the Provider:</span></span>

        C:\ASR> setupdr.exe /i
5. <span data-ttu-id="b27c3-311">註冊提供者：</span><span class="sxs-lookup"><span data-stu-id="b27c3-311">Register the Provider:</span></span>

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>         

<span data-ttu-id="b27c3-312">參數：</span><span class="sxs-lookup"><span data-stu-id="b27c3-312">Parameters:</span></span>

* <span data-ttu-id="b27c3-313">**/Credentials**：必要參數，代表註冊金鑰檔案所在的位置。</span><span class="sxs-lookup"><span data-stu-id="b27c3-313">**/Credentials**: Required parameter for the location in which the registration key file is located.</span></span>  
* <span data-ttu-id="b27c3-314">**/FriendlyName**：必要參數，代表 Hyper-V 主機伺服器的名稱，該伺服器會出現在 Azure Site Recovery 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-314">**/FriendlyName**: Required parameter for the name of the Hyper-V host server that appears in the Azure Site Recovery portal.</span></span>
* <span data-ttu-id="b27c3-315">**/EncryptionEnabled**︰選用參數，只會在從 VMM 複寫到 Azure 時使用。</span><span class="sxs-lookup"><span data-stu-id="b27c3-315">**/EncryptionEnabled**: Optional parameter only used when replicating from VMM to Azure.</span></span>
* <span data-ttu-id="b27c3-316">**/proxyAddress**：指定 Proxy 伺服器位址的選用參數。</span><span class="sxs-lookup"><span data-stu-id="b27c3-316">**/proxyAddress**: Optional parameter that specifies the address of the proxy server.</span></span>
* <span data-ttu-id="b27c3-317">**/proxyport**：指定 Proxy 伺服器連接埠的選用參數。</span><span class="sxs-lookup"><span data-stu-id="b27c3-317">**/proxyport**: Optional parameter that specifies the port of the proxy server.</span></span>
* <span data-ttu-id="b27c3-318">**/proxyUsername**：選用參數，指定 Proxy 使用者名稱 (如果 Proxy 需要驗證)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-318">**/proxyUsername**: Optional parameter that specifies the proxy user name (if the proxy requires authentication).</span></span>
* <span data-ttu-id="b27c3-319">**/proxyPassword**：選用參數，指定用以驗證 Proxy 伺服器的密碼 (如果 Proxy 需要驗證)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-319">**/proxyPassword**: Optional parameter that specifies the password for authenticating with the proxy server (if the proxy requires authentication).</span></span>

## <a name="step-3-map-storage-arrays-and-pools"></a><span data-ttu-id="b27c3-320">步驟 3：對應存放裝置陣列和集區</span><span class="sxs-lookup"><span data-stu-id="b27c3-320">Step 3: Map storage arrays and pools</span></span>

<span data-ttu-id="b27c3-321">對應主要和次要陣列，以指定哪一個次要存放集區要從主要集區接收複寫資料。</span><span class="sxs-lookup"><span data-stu-id="b27c3-321">Map primary and secondary arrays to specify which secondary storage pool receives replication data from the primary pool.</span></span> <span data-ttu-id="b27c3-322">請在設定複寫之前先對應存放裝置，因為在您為複寫群組啟用保護時，會使用此對應資訊。</span><span class="sxs-lookup"><span data-stu-id="b27c3-322">Map storage before you configure replication, because the mapping information is used when you enable protection for replication groups.</span></span>

<span data-ttu-id="b27c3-323">在開始之前，請先確定 VMM 雲端有出現在保存庫中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-323">Before you start, check that VMM clouds appear in the vault.</span></span> <span data-ttu-id="b27c3-324">當您在安裝提供者期間同步處理所有雲端時，或在 VMM 主控台中同步處理特定雲端時，就會偵測雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-324">Clouds are detected either when you synchronize all clouds during Provider installation or when you synchronize a specific cloud in the VMM console.</span></span>

1. <span data-ttu-id="b27c3-325">按一下 [資源]  >  [伺服器存放裝置]  >  [對應來源和目標陣列]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-325">Click **Resources** > **Server Storage** > **Map Source and Target Arrays**.</span></span>
    <span data-ttu-id="b27c3-326">![伺服器註冊](./media/site-recovery-vmm-san/storage-map.png)</span><span class="sxs-lookup"><span data-stu-id="b27c3-326">![Server registration](./media/site-recovery-vmm-san/storage-map.png)</span></span>

2. <span data-ttu-id="b27c3-327">選取主要網站上的存放裝置陣列，然後將它們對應至次要網站上的存放裝置陣列。</span><span class="sxs-lookup"><span data-stu-id="b27c3-327">Select the storage arrays on the primary site, and map them to storage arrays on the secondary site.</span></span> <span data-ttu-id="b27c3-328">在 [存放集區] 中，選取要對應的來源和目標存放集區。</span><span class="sxs-lookup"><span data-stu-id="b27c3-328">In **Storage Pools**, select a source and target storage pool to map.</span></span>

    ![伺服器註冊](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a><span data-ttu-id="b27c3-330">步驟 4︰設定複寫設定</span><span class="sxs-lookup"><span data-stu-id="b27c3-330">Step 4: Configure replication settings</span></span>

<span data-ttu-id="b27c3-331">註冊 VMM 伺服器之後，設定雲端保護設定。</span><span class="sxs-lookup"><span data-stu-id="b27c3-331">After VMM servers are registered, configure cloud protection settings.</span></span>

1. <span data-ttu-id="b27c3-332">在 [快速啟動] 頁面上，按一下 [設定 VMM 雲端的保護]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-332">On the **Quick Start** page, click **Set up protection for VMM clouds**.</span></span>
2. <span data-ttu-id="b27c3-333">在 [受保護的項目] 索引標籤上，選取雲端 [組態]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-333">On the **Protected Items** tab, select the cloud **Configuration**.</span></span>
3. <span data-ttu-id="b27c3-334">在 [目標] 中，選取 [VMM]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-334">In **Target**, select **VMM**.</span></span>
4. <span data-ttu-id="b27c3-335">在 [目標位置] 中，選取管理您要用於復原之雲端的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-335">In **Target location**, select the VMM server that manages the cloud you want to use for recovery.</span></span>
5. <span data-ttu-id="b27c3-336">在 [目標雲端] 中，選取您想要用於 VM 容錯移轉的目標雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-336">In **Target cloud**, select the target cloud you want to use for VM failover.</span></span>
   * <span data-ttu-id="b27c3-337">建議您，選取的目標雲端要符合您所保護之虛擬機器的復原需求。</span><span class="sxs-lookup"><span data-stu-id="b27c3-337">We recommend that you select a target cloud that meets recovery requirements for the virtual machines you protect.</span></span>
   * <span data-ttu-id="b27c3-338">雲端只能屬於單一雲端組 -- 當作主要雲端或目標雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-338">A cloud can only belong to a single cloud pair--as either a primary or a target cloud.</span></span>
6. <span data-ttu-id="b27c3-339">Site Recovery 會確認雲端能夠存取 SAN 存放裝置，並確認存放裝置陣列已對應。</span><span class="sxs-lookup"><span data-stu-id="b27c3-339">Site Recovery verifies that clouds have access to SAN storage, and that the storage arrays are mapped.</span></span>
7. <span data-ttu-id="b27c3-340">如果驗證成功，請在 [複寫類型] 中，選取 [SAN]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-340">If verification is successful, in **Replication type**, select **SAN**.</span></span>

<span data-ttu-id="b27c3-341">儲存設定之後會建立一個作業，供您在 [作業] 索引標籤上監視。</span><span class="sxs-lookup"><span data-stu-id="b27c3-341">After you save the settings, a job is created that can be monitored on the **Jobs** tab.</span></span> <span data-ttu-id="b27c3-342">在 [設定] 索引標籤上可修改設定。</span><span class="sxs-lookup"><span data-stu-id="b27c3-342">Settings can be modified on the **Configure** tab.</span></span> <span data-ttu-id="b27c3-343">如果您要修改目標位置或目標雲端，則必須移除雲端組態，然後重新設定雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-343">If you want to modify the target location or target cloud, you must remove the cloud configuration and then reconfigure the cloud.</span></span>

## <a name="step-5-enable-network-mapping"></a><span data-ttu-id="b27c3-344">步驟 5：啟用網路對應</span><span class="sxs-lookup"><span data-stu-id="b27c3-344">Step 5: Enable network mapping</span></span>

1. <span data-ttu-id="b27c3-345">在 [快速入門] 頁面上，按一下 [對應網路]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-345">On the **Quick Start** page, click **Map networks**.</span></span>
2. <span data-ttu-id="b27c3-346">選取來源 VMM 伺服器，然後選取網路將對應的目標 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-346">Select the source VMM server, and then select the target VMM server to which the networks will be mapped.</span></span> <span data-ttu-id="b27c3-347">隨即會顯示來源網路的清單和與其相關聯的目標網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-347">The list of source networks and their associated target networks are displayed.</span></span> <span data-ttu-id="b27c3-348">對於未對應的網路，將顯示空白值。</span><span class="sxs-lookup"><span data-stu-id="b27c3-348">A blank value is shown for networks that aren't mapped.</span></span> <span data-ttu-id="b27c3-349">按一下來源和目標網路名稱旁邊的資訊圖示，以檢視每個網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-349">Click the information icon next to the source and target network names to view the subnets for each network.</span></span>
3. <span data-ttu-id="b27c3-350">在 [來源上的網路] 中選取網路，然後按一下 [對應]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-350">Select a network in **Network on source**, and then click **Map**.</span></span> <span data-ttu-id="b27c3-351">服務會偵測目標伺服器上的 VM 網路並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="b27c3-351">The service detects the VM networks on the target server and displays them.</span></span>

    ![SAN 架構](./media/site-recovery-vmm-san/network-map1.png)
4. <span data-ttu-id="b27c3-353">從目標 VMM 伺服器選取其中一個 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-353">Select one of the VM networks from the target VMM server.</span></span>

    ![SAN 架構](./media/site-recovery-vmm-san/network-map2.png)

5. <span data-ttu-id="b27c3-355">當您選曲目標網路時，隨即會顯示使用來源網路的受保護雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-355">When you select a target network, the protected clouds that use the source network are displayed.</span></span> <span data-ttu-id="b27c3-356">也會顯示可用的目標網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-356">Available target networks are also displayed.</span></span> <span data-ttu-id="b27c3-357">建議您選取所有用於複寫之雲端都可用的目標網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-357">We recommend that you select a target network that is available to all the clouds you're using for replication.</span></span>
6. <span data-ttu-id="b27c3-358">按一下打勾記號完成對應程序。</span><span class="sxs-lookup"><span data-stu-id="b27c3-358">Click the check mark to complete the mapping process.</span></span> <span data-ttu-id="b27c3-359">此時會啟動一個作業來追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="b27c3-359">A job starts that tracks progress.</span></span> <span data-ttu-id="b27c3-360">您可以在 [工作]  索引標籤上檢視它。</span><span class="sxs-lookup"><span data-stu-id="b27c3-360">You can view it on the **Jobs** tab.</span></span>

## <a name="step-6-enable-replication-for-replication-groups"></a><span data-ttu-id="b27c3-361">步驟 6：為複寫群組啟用複寫</span><span class="sxs-lookup"><span data-stu-id="b27c3-361">Step 6: Enable replication for replication groups</span></span>

<span data-ttu-id="b27c3-362">您必須先為存放裝置複寫群組啟用複寫，才能為虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="b27c3-362">Before you can enable protection for virtual machines, you need to enable replication for storage replication groups.</span></span>

1. <span data-ttu-id="b27c3-363">在 Site Recovery 入口網站中，請在主要雲端的 [屬性] 頁面開啟 [虛擬機器] 索引標籤，然後按一下 [新增複寫群組]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-363">On the **Properties** page of the primary cloud in the Site Recovery portal, open the **Virtual Machines** tab and click **Add Replication Group**.</span></span>
2. <span data-ttu-id="b27c3-364">選取一個或多個與雲端關聯的 VMM 複寫群組、確認來源和目標陣列，然後指定複寫頻率。</span><span class="sxs-lookup"><span data-stu-id="b27c3-364">Select one or more VMM replication groups that are associated with the cloud, verify the source and target arrays, and specify the replication frequency.</span></span>

<span data-ttu-id="b27c3-365">Site Recovery、VMM 和 SMI-S 提供者會佈建目標網站存放裝置 LUN，並啟用存放裝置複寫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-365">Site Recovery, VMM, and the SMI-S providers provision the target site storage LUNs and enable storage replication.</span></span> <span data-ttu-id="b27c3-366">如果複寫群組已經被複寫，Site Recovery 便會重複使用現有的複寫關係並更新資訊。</span><span class="sxs-lookup"><span data-stu-id="b27c3-366">If the replication group is already replicated, Site Recovery reuses the existing replication relationship and updates the information.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="b27c3-367">步驟 7：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="b27c3-367">Step 7: Enable protection for virtual machines</span></span>


<span data-ttu-id="b27c3-368">當存放裝置群組在複寫時，請使用下列其中一個方法，在 VMM 主控台中為 VM 啟用保護：</span><span class="sxs-lookup"><span data-stu-id="b27c3-368">When a storage group is replicating, enable protection for VMs in the VMM console with one of the following methods:</span></span>

* <span data-ttu-id="b27c3-369">**新增虛擬機器**：當您建立 VM 時，啟用複寫並將該 VM 與複寫群組建立關聯。</span><span class="sxs-lookup"><span data-stu-id="b27c3-369">**New virtual machine**: When you create a VM, you enable replication and associate the VM with the replication group.</span></span>
  <span data-ttu-id="b27c3-370">使用此選項時，VMM 會使用智慧型放置，以最佳方式將 VM 存放裝置放置在複寫群組的 LUN 上。</span><span class="sxs-lookup"><span data-stu-id="b27c3-370">With this option, VMM uses intelligent placement to optimally place the VM storage on the LUNs of the replication group.</span></span> <span data-ttu-id="b27c3-371">Site Recovery 會在次要網站上協調建立陰影 VM 並配置容量，以便能夠在容錯移轉後啟動複本 VM。</span><span class="sxs-lookup"><span data-stu-id="b27c3-371">Site Recovery orchestrates the creation of a shadow VM on the secondary site and allocates capacity so that replica VMs can be started after failover.</span></span>
* <span data-ttu-id="b27c3-372">**現有的虛擬機器**：如果 VMM 中已經部署虛擬機器，您可以啟用複寫，並將存放裝置移轉至複寫群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-372">**Existing virtual machine**: If a virtual machine is already deployed in VMM, you can enable replication and perform a storage migration to a replication group.</span></span> <span data-ttu-id="b27c3-373">完成之後，VMM 和 Site Recovery 會偵測新的虛擬機器，並開始在 Site Recovery 中管理它。</span><span class="sxs-lookup"><span data-stu-id="b27c3-373">After completion, VMM and Site Recovery detect the new VM and start managing it in Site Recovery.</span></span> <span data-ttu-id="b27c3-374">建立影子 VM 時，會在次要網站上建立並配置容量，以便能夠在容錯移轉後啟動複本 VM。</span><span class="sxs-lookup"><span data-stu-id="b27c3-374">A shadow VM is created on the secondary site, and capacity is allocated so that the replica VM can be started after failover.</span></span>

![啟用保護。](./media/site-recovery-vmm-san/enable-protect.png)

<span data-ttu-id="b27c3-376">VM 啟用複寫後，就會顯示在 Site Recovery 主控台。</span><span class="sxs-lookup"><span data-stu-id="b27c3-376">After VMs are enabled for replication, they appear in the Site Recovery console.</span></span> <span data-ttu-id="b27c3-377">您可以檢視 VM 內容、追蹤狀態，以及追蹤包含多個 VM 的容錯移轉複寫群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-377">You can view VM properties, track status, and track failover replication groups that contain multiple VMs.</span></span> <span data-ttu-id="b27c3-378">在 SAN 複寫中，與複寫群組關聯的所有 VM 必須都一起進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-378">In SAN replication, all VMs associated with a replication group must fail over together.</span></span> <span data-ttu-id="b27c3-379">這是因為容錯移轉會先發生在儲存層。</span><span class="sxs-lookup"><span data-stu-id="b27c3-379">This is because failover occurs at the storage layer first.</span></span> <span data-ttu-id="b27c3-380">請務必正確地組成您的複寫群組，只將相關聯的 VM 放在一起。</span><span class="sxs-lookup"><span data-stu-id="b27c3-380">It’s important to group your replication groups properly and place only associated VMs together.</span></span>

> [!NOTE]
> <span data-ttu-id="b27c3-381">啟用 VM 的複寫之後，請勿將它的 VHD 新增至 LUN，除非這些 VHD 位於 Site Recovery 複寫群組中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-381">After you've enabled replication for a VM, don't add its VHDs to LUNs unless they are located in a Site Recovery replication group.</span></span> <span data-ttu-id="b27c3-382">Site Recovery 只能偵測位於 Site Recovery 複寫群組中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="b27c3-382">VHDs will only be detected by Site Recovery if they are located in a Site Recovery replication group.</span></span>
>
>

<span data-ttu-id="b27c3-383">您可以在 [作業] 索引標籤追蹤進度，包括初始複寫。</span><span class="sxs-lookup"><span data-stu-id="b27c3-383">You can track progress, including the initial replication, on the **Jobs** tab.</span></span> <span data-ttu-id="b27c3-384">執行「完成保護」工作之後，虛擬機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-384">After the Finalize Protection job runs, the virtual machine is ready for failover.</span></span>

![虛擬機器保護工作](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-the-deployment"></a><span data-ttu-id="b27c3-386">步驟 8：測試部署</span><span class="sxs-lookup"><span data-stu-id="b27c3-386">Step 8: Test the deployment</span></span>

<span data-ttu-id="b27c3-387">測試您的部署，以確定 VM 容錯移轉如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="b27c3-387">Test your deployment to make sure that VMs fail over as expected.</span></span> <span data-ttu-id="b27c3-388">若要這樣做，請建立復原方案並執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-388">To do this, create a recovery plan and run a test failover.</span></span>

1. <span data-ttu-id="b27c3-389">在 [復原方案] 索引標籤上，按一下 [建立復原方案]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-389">On the **Recovery Plans** tab, click **Create Recovery Plan**.</span></span>
2. <span data-ttu-id="b27c3-390">指定復原計劃的名稱，並選取來源和目標 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b27c3-390">Specify a name for the recovery plan, and select source and target VMM servers.</span></span> <span data-ttu-id="b27c3-391">來源伺服器必須有已啟用容錯移轉和復原功能的 VM。</span><span class="sxs-lookup"><span data-stu-id="b27c3-391">The source server must have VMs that are enabled for failover and recovery.</span></span> <span data-ttu-id="b27c3-392">選取 [SAN]  ，僅檢視為 SAN 複寫設定的雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-392">Select **SAN** to view only clouds that are configured for SAN replication.</span></span>

    ![建立復原計畫](./media/site-recovery-vmm-san/r-plan.png)

3. <span data-ttu-id="b27c3-394">在 [選取虛擬機器] 中，選取複寫群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-394">In **Select Virtual Machines**, select replication groups.</span></span> <span data-ttu-id="b27c3-395">與群組相關聯的所有 VM 都會加入復原方案。</span><span class="sxs-lookup"><span data-stu-id="b27c3-395">All VMs associated with the group are added to the recovery plan.</span></span> <span data-ttu-id="b27c3-396">這些 VM 將新增到復原方案的預設群組 (群組 1)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-396">These VMs are added to the recovery plan default group (Group 1).</span></span> <span data-ttu-id="b27c3-397">您可以視需要新增更多群組。</span><span class="sxs-lookup"><span data-stu-id="b27c3-397">You can add more groups if necessary.</span></span> <span data-ttu-id="b27c3-398">複寫之後，VM 會根據復原計劃群組的順序來編號。</span><span class="sxs-lookup"><span data-stu-id="b27c3-398">After replication, VMs are numbered according to the order of the recovery plan groups.</span></span>

    ![選取虛擬機器](./media/site-recovery-vmm-san/r-plan-vm.png)
4. <span data-ttu-id="b27c3-400">建立復原方案之後，它會出現在 [復原方案] 索引標籤上的清單中。</span><span class="sxs-lookup"><span data-stu-id="b27c3-400">After the recovery plan is created, it appears in the list on the **Recovery Plans** tab.</span></span> <span data-ttu-id="b27c3-401">選取方案，然後選擇 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-401">Select the plan and choose **Test Failover**.</span></span>
5. <span data-ttu-id="b27c3-402">在 [確認測試容錯移轉] 頁面上，選取 [無]。</span><span class="sxs-lookup"><span data-stu-id="b27c3-402">On the **Confirm Test Failover** page, select **None**.</span></span> <span data-ttu-id="b27c3-403">啟用此選項時，容錯移轉的複本 VM 將不會連線到任何網路。</span><span class="sxs-lookup"><span data-stu-id="b27c3-403">With this option enabled, the failed over replica VMs won't be connected to any network.</span></span> <span data-ttu-id="b27c3-404">這會測試 VM 容錯移轉是否如預期般運作，但不會測試網路環境。</span><span class="sxs-lookup"><span data-stu-id="b27c3-404">This tests that the VMs fail over as expected, but it doesn't test the network environment.</span></span> <span data-ttu-id="b27c3-405">如需其他網路功能選項的相關資訊，請參閱 [Site Recovery 容錯移轉](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="b27c3-405">For more about other networking options, see [Site Recovery failover](site-recovery-failover.md).</span></span>

    ![選取測試網路](./media/site-recovery-vmm-san/test-fail1.png)

6. <span data-ttu-id="b27c3-407">將會在複本 VM 所在的相同主機上建立測試 VM。</span><span class="sxs-lookup"><span data-stu-id="b27c3-407">The test VM is created on the same host as the host on which the replica VM exists.</span></span> <span data-ttu-id="b27c3-408">它不會新增至複本 VM 所在的雲端。</span><span class="sxs-lookup"><span data-stu-id="b27c3-408">It isn’t added to the cloud in which the replica VM is located.</span></span>
2. <span data-ttu-id="b27c3-409">複寫之後，複本 VM 會有不同於主要虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b27c3-409">After replication, the replica VM will have a different IP address than the primary virtual machine.</span></span> <span data-ttu-id="b27c3-410">如果您是從 DHCP 發出位址，則會自動更新位址。</span><span class="sxs-lookup"><span data-stu-id="b27c3-410">If you're issuing addresses from DHCP, it will be updated automatically.</span></span> <span data-ttu-id="b27c3-411">如果您不是使用 DHCP 而想要相同位址，則需要執行數個指令碼。</span><span class="sxs-lookup"><span data-stu-id="b27c3-411">If you're not using DHCP and you want the same addresses, you need to run a couple of scripts.</span></span>
3. <span data-ttu-id="b27c3-412">執行此指令碼以擷取 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="b27c3-412">Run this script to retrieve the IP address:</span></span>

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. <span data-ttu-id="b27c3-413">執行此範例指令碼以更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="b27c3-413">Run this sample script to update DNS.</span></span> <span data-ttu-id="b27c3-414">指定您擷取的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b27c3-414">Specify the IP address you retrieved.</span></span>

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a><span data-ttu-id="b27c3-415">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b27c3-415">Next steps</span></span>

<span data-ttu-id="b27c3-416">在您執行測試容錯移轉以檢查您的環境是否如預期般運作之後，請參閱 [Site Recovery 容錯移轉](site-recovery-failover.md)，以深入了解不同類型的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b27c3-416">After you've run a test failover to check that your environment is working as expected, see [Site Recovery failover](site-recovery-failover.md) to learn about different types of failovers.</span></span>
