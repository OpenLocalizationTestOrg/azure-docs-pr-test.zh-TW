---
title: "從 Azure 重新保護到內部部署網站 | Microsoft Docs"
description: "將 VM 容錯移轉到 Azure 之後，您可以起始將 VM 容錯回復到內部部署的作業。 了解如何在容錯回復之前重新保護。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 181ed544ae4697753490642fea8eef636322a114
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="reprotect-from-azure-to-an-on-premises-site"></a><span data-ttu-id="fa871-104">從 Azure 重新保護至內部部署網站</span><span class="sxs-lookup"><span data-stu-id="fa871-104">Reprotect from Azure to an on-premises site</span></span>



## <a name="overview"></a><span data-ttu-id="fa871-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fa871-105">Overview</span></span>
<span data-ttu-id="fa871-106">此文章說明如何將 Azure 虛擬機器從 Azure 重新保護到內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="fa871-106">This article describes how to reprotect Azure virtual machines from Azure to an on-premises site.</span></span> <span data-ttu-id="fa871-107">當您準備好使用已從內部部署網站容錯移轉至 Azure 的 VMware 虛擬機器或 Windows/Linux 實體伺服器容錯回復時，請依照此文章中的指示執行 (如[使用 Azure Site Recovery 將 VMware 虛擬機器和實體伺服器複寫至 Azure](site-recovery-failover.md)所述)。</span><span class="sxs-lookup"><span data-stu-id="fa871-107">Follow the instructions in this article when you're ready to fail back your VMware virtual machines or Windows/Linux physical servers after they've failed over from the on-premises site to Azure (as described in [Replicate VMware virtual machines and physical servers to Azure with Azure Site Recovery](site-recovery-failover.md)).</span></span>

> [!WARNING]
> <span data-ttu-id="fa871-108">您[完成移轉](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)、將虛擬機器移至另一個資源群組，或刪除 Azure 虛擬機器之後，則無法執行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="fa871-108">You cannot fail back after you [complete migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), move a virtual machine to another resource group, or delete an Azure virtual machine.</span></span>


<span data-ttu-id="fa871-109">完成重新保護且受保護的虛擬機器開始複寫之後，您可以在虛擬機器上起始容錯回復，以將它們回復到內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="fa871-109">After reprotection finishes and the protected virtual machines are replicating, you can initiate a failback on the virtual machines to bring them to the on-premises site.</span></span>

<span data-ttu-id="fa871-110">在本文末尾或 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 中張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="fa871-110">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

<span data-ttu-id="fa871-111">如需快速概觀，請觀看下列有關如何從 Azure 容錯移轉到內部部署網站的影片。</span><span class="sxs-lookup"><span data-stu-id="fa871-111">For a quick overview, watch the following video about how to fail over from Azure to an on-premises site.</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a><span data-ttu-id="fa871-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="fa871-112">Prerequisites</span></span>
<span data-ttu-id="fa871-113">您準備要重新保護虛擬機器時，請採取或考量下列的必要動作：</span><span class="sxs-lookup"><span data-stu-id="fa871-113">When you prepare to reprotect virtual machines, take or consider the following prerequisite actions:</span></span>

* <span data-ttu-id="fa871-114">如果 vCenter 伺服器管理您想要容錯回復到的目標虛擬機器，您必須確定已擁有在 vCenter 伺服器上探索虛擬機器的[必要權限](site-recovery-vmware-to-azure-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="fa871-114">If a vCenter server manages the virtual machines that you want to fail back to, make sure that you have the [required permissions](site-recovery-vmware-to-azure-classic.md) for discovery of virtual machines on vCenter servers.</span></span>

  > [!WARNING]
  > <span data-ttu-id="fa871-115">如果內部部署的主要目標或虛擬機器上有快照集，重新保護程序將會失敗。</span><span class="sxs-lookup"><span data-stu-id="fa871-115">If snapshots are present on the on-premises master target or the virtual machine, reprotection fails.</span></span> <span data-ttu-id="fa871-116">您可以先刪除主要目標上的快照集，再進行重新保護。</span><span class="sxs-lookup"><span data-stu-id="fa871-116">You can delete the snapshots on the master target before you proceed to reprotect.</span></span> <span data-ttu-id="fa871-117">虛擬機器上的快照集會在重新保護作業期間自動合併。</span><span class="sxs-lookup"><span data-stu-id="fa871-117">The snapshots on the virtual machine are automatically merged during a reprotect job.</span></span>

* <span data-ttu-id="fa871-118">在容錯回復之前，先建立兩個其他元件：</span><span class="sxs-lookup"><span data-stu-id="fa871-118">Before you fail back, create two additional components:</span></span>

  * <span data-ttu-id="fa871-119">**處理序伺服器**：[處理序伺服器](site-recovery-vmware-setup-azure-ps-resource-manager.md)會從在 Azure 中受保護的虛擬機器接收資料，並將資料傳送至內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="fa871-119">**Process server**: The [process server](site-recovery-vmware-setup-azure-ps-resource-manager.md) receives data from the protected virtual machine in Azure and sends data to the on-premises site.</span></span> <span data-ttu-id="fa871-120">低延遲網路必須位於處理伺服器與受保護虛擬機器之間。</span><span class="sxs-lookup"><span data-stu-id="fa871-120">A low-latency network is required between the process server and the protected virtual machine.</span></span> <span data-ttu-id="fa871-121">因此，如果您使用 Azure ExpressRoute 連線，或 Azure 型處理序伺服器和 VPN，則可擁有內部部署處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-121">Thus, you can have an on-premises process server if you're using an Azure ExpressRoute connection or an Azure-based process server and a VPN.</span></span>
  
  * <span data-ttu-id="fa871-122">**主要目標伺服器**：主要目標伺服器會接收容錯回復資料。</span><span class="sxs-lookup"><span data-stu-id="fa871-122">**Master target server**: The master target server receives failback data.</span></span> <span data-ttu-id="fa871-123">您建立的內部部署管理伺服器預設會安裝主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-123">The on-premises management server that you created has a master target server installed by default.</span></span> <span data-ttu-id="fa871-124">不過，您可能必須根據容錯回復流量的大小，另外建立一部用來容錯回復的主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-124">However, depending on the volume of failed-back traffic, you might need to create a separate master target server for failback.</span></span>
    * <span data-ttu-id="fa871-125">[Linux 虛擬機器需要 Linux 主要目標伺服器](site-recovery-how-to-install-linux-master-target.md)。</span><span class="sxs-lookup"><span data-stu-id="fa871-125">[A Linux virtual machine needs a Linux master target server](site-recovery-how-to-install-linux-master-target.md).</span></span>
    * <span data-ttu-id="fa871-126">Windows 虛擬機器需要 Windows 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-126">A Windows virtual machine needs a Windows master target server.</span></span> <span data-ttu-id="fa871-127">您可以再次使用內部部署處理序伺服器和主要目標電腦。</span><span class="sxs-lookup"><span data-stu-id="fa871-127">You can use the on-premises process server and master target machines again.</span></span>

    <span data-ttu-id="fa871-128">[重新保護之前在主要目標上檢查的常見項目](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server)中，列出主要目標的其他必要條件。</span><span class="sxs-lookup"><span data-stu-id="fa871-128">The master target has other prerequisites that are listed in [Common things to check on a master target before reprotect](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).</span></span>

* <span data-ttu-id="fa871-129">執行容錯回復時，組態伺服器必須為內部部署。</span><span class="sxs-lookup"><span data-stu-id="fa871-129">A configuration server is required on-premises when you fail back.</span></span> <span data-ttu-id="fa871-130">在容錯回復期間，虛擬機器必須存在於組態伺服器資料庫中。</span><span class="sxs-lookup"><span data-stu-id="fa871-130">During failback, the virtual machine must exist in the configuration server database.</span></span> <span data-ttu-id="fa871-131">否則，將無法成功容錯回復。</span><span class="sxs-lookup"><span data-stu-id="fa871-131">Otherwise, failback is unsuccessful.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fa871-132">請確定您定期排程備份設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-132">Make sure that you take regularly scheduled backups of your configuration server.</span></span> <span data-ttu-id="fa871-133">發生災害時，使用相同的 IP 位址還原伺服器，讓容錯回復運作。</span><span class="sxs-lookup"><span data-stu-id="fa871-133">If there's a disaster, restore the server with the same IP address so that failback works.</span></span>

* <span data-ttu-id="fa871-134">在 VMware 的主要目標虛擬機器組態參數中，進行 `disk.EnableUUID=true` 設定。</span><span class="sxs-lookup"><span data-stu-id="fa871-134">Set the `disk.EnableUUID=true` setting in the configuration parameters of the master target virtual machine in VMware.</span></span> <span data-ttu-id="fa871-135">如果此列不存在，請新增它。</span><span class="sxs-lookup"><span data-stu-id="fa871-135">If this row does not exist, add it.</span></span> <span data-ttu-id="fa871-136">需要此設定才能提供一致的 UUID 給虛擬機器磁碟 (VMDK)，使其可正確掛接。</span><span class="sxs-lookup"><span data-stu-id="fa871-136">This setting is required to provide a consistent UUID to the virtual machine disk (VMDK) so that it mounts correctly.</span></span>

* <span data-ttu-id="fa871-137">*您無法使用主要目標伺服器的儲存體 vMotion*。</span><span class="sxs-lookup"><span data-stu-id="fa871-137">*You cannot use Storage vMotion on the master target server*.</span></span> <span data-ttu-id="fa871-138">這會造成容錯回復失敗。</span><span class="sxs-lookup"><span data-stu-id="fa871-138">This can cause the failback to fail.</span></span> <span data-ttu-id="fa871-139">虛擬機器無法啟動，因為磁碟不可供其使用。</span><span class="sxs-lookup"><span data-stu-id="fa871-139">The virtual machine can't start because the disks are not available to it.</span></span> <span data-ttu-id="fa871-140">若要避免這個問題，請從 vMotion 清單中排除主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-140">To prevent this problem, exclude the master target servers from your vMotion list.</span></span>

* <span data-ttu-id="fa871-141">將新的磁碟機新增至主要目標伺服器：保留磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fa871-141">Add a new drive to the master target server: a retention drive.</span></span> <span data-ttu-id="fa871-142">新增磁碟並格式化磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fa871-142">Add a new disk and format the drive.</span></span>


### <a name="frequently-asked-questions"></a><span data-ttu-id="fa871-143">常見問題集</span><span class="sxs-lookup"><span data-stu-id="fa871-143">Frequently asked questions</span></span>

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-to-replicate-data-back-to-the-on-premises-site"></a><span data-ttu-id="fa871-144">為什麼需要 S2S VPN 或 ExpressRoute 連線，才能將資料複寫回到內部部署網站？</span><span class="sxs-lookup"><span data-stu-id="fa871-144">Why do I need a S2S VPN or an ExpressRoute connection to replicate data back to the on-premises site?</span></span>
<span data-ttu-id="fa871-145">從內部部署複寫到 Azure 的動作可以透過網際網路或具有公用對等互連的 ExpressRoute 連線來執行，重新保護和容錯回復需要站台對站台 (S2S) VPN 以複寫資料。</span><span class="sxs-lookup"><span data-stu-id="fa871-145">Whereas replication from on-premises to Azure can happen over the Internet or an ExpressRoute connection that has public peering, reprotection and failback require a site-to-site (S2S) VPN to replicate data.</span></span> <span data-ttu-id="fa871-146">提供網路，讓 Azure 中已容錯移轉的虛擬機器可以觸達 (偵測) 內部部署組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-146">Provide the network so that the failed-over virtual machines in Azure can reach (ping) the on-premises configuration server.</span></span> <span data-ttu-id="fa871-147">您也可能會在容錯移轉虛擬機器的 Azure 網路中部署處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-147">You might also deploy a process server in the Azure network of the failed-over virtual machine.</span></span> <span data-ttu-id="fa871-148">此處理序伺服器也應該能夠與內部部署組態設定伺服器進行通訊。</span><span class="sxs-lookup"><span data-stu-id="fa871-148">This process server should also be able to communicate with the on-premises configuration server.</span></span>

#### <a name="when-should-i-install-a-process-server-in-azure"></a><span data-ttu-id="fa871-149">何時應該在 Azure 中安裝處理序伺服器？</span><span class="sxs-lookup"><span data-stu-id="fa871-149">When should I install a process server in Azure?</span></span>


<span data-ttu-id="fa871-150">您要在 Azure 上重新保護的虛擬機器會將複寫資料傳送至處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-150">The virtual machines on Azure that you want to reprotect send replication data to a process server.</span></span> <span data-ttu-id="fa871-151">設定網路，以便 Azure 上的虛擬機器可以連線到處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-151">Set up your network so that the virtual machines on Azure can reach the process server.</span></span>

<span data-ttu-id="fa871-152">您可以在 Azure 中部署處理伺服器，或使用在容錯移轉期間使用的現有處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-152">You can deploy a process server in Azure or use the existing process server that you used during failover.</span></span> <span data-ttu-id="fa871-153">要考量的重點是將資料從 Azure 上的虛擬機器傳送到處理伺服器的延遲。</span><span class="sxs-lookup"><span data-stu-id="fa871-153">The important point to consider is the latency to send the data from the virtual machines on Azure to the process server.</span></span>

<span data-ttu-id="fa871-154">如果您已設定 ExpressRoute 連線，可使用內部部署處理序伺服器來傳送資料，因為虛擬機器和處理序伺服器之間的延遲很低。</span><span class="sxs-lookup"><span data-stu-id="fa871-154">If you have an ExpressRoute connection set up, you can use an on-premises process server to send data because the latency between the virtual machine and the process server is low.</span></span>

 ![Expressroute 的架構圖](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



<span data-ttu-id="fa871-156">不過若您只有 S2S VPN，我們建議您在 Azure 中部署處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-156">However, if you have only an S2S VPN, we recommend deploying the process server in Azure.</span></span>

 ![VPN 的架構圖](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


<span data-ttu-id="fa871-158">請記住，複寫只能透過 S2S VPN 或您 ExpressRoute 網路的私人對等互連。</span><span class="sxs-lookup"><span data-stu-id="fa871-158">Remember that replication happens only over the S2S VPN or the private peering of your ExpressRoute network.</span></span> <span data-ttu-id="fa871-159">請確定該網路通道上有足夠的可用頻寬。</span><span class="sxs-lookup"><span data-stu-id="fa871-159">Ensure that enough bandwidth is available over that network channel.</span></span>

<span data-ttu-id="fa871-160">如需安裝 Azure 型處理序伺服器的資訊，請參閱[管理在 Azure 中執行的處理伺服器](site-recovery-vmware-setup-azure-ps-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="fa871-160">For information about installing an Azure-based process server, see [Manage a process server running in Azure](site-recovery-vmware-setup-azure-ps-resource-manager.md).</span></span>

> [!TIP]
> <span data-ttu-id="fa871-161">我們建議在容錯回復期間使用 Azure 型處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-161">We recommend using an Azure-based process server during failback.</span></span> <span data-ttu-id="fa871-162">如果處理序伺服器比較接近複寫的虛擬機器 (在 Azure 中容錯移轉的機器)，則複寫效能較高。</span><span class="sxs-lookup"><span data-stu-id="fa871-162">The replication performance is higher if the process server is closer to the replicating virtual machine (the failed-over machine in Azure).</span></span> <span data-ttu-id="fa871-163">不過，在概念證明 (POC) 或示範的期間，您可以透過私人對等互連，使用內部部署處理序伺服器以及 ExpressRoute 更快完成 POC。</span><span class="sxs-lookup"><span data-stu-id="fa871-163">However, during your proof of concept (POC) or demonstration, you can use the on-premises process server along with ExpressRoute with private peering to complete the POC faster.</span></span>



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a><span data-ttu-id="fa871-164">在不同的元件上應該開啟哪些連接埠，重新保護才能運作？</span><span class="sxs-lookup"><span data-stu-id="fa871-164">What ports should I open on different components so that reprotection can work?</span></span>

![容錯移轉和容錯回復的端點](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a><span data-ttu-id="fa871-166">哪一個主要目標伺服器應用於重新保護？</span><span class="sxs-lookup"><span data-stu-id="fa871-166">Which master target server should I use for reprotection?</span></span>
<span data-ttu-id="fa871-167">必須有內部部署主要目標伺服器才可接收來自處理伺服器的資料，並接著將資料寫入到內部部署內部部署的 VMDK。</span><span class="sxs-lookup"><span data-stu-id="fa871-167">An on-premises master target server is required to receive data from the process server and then write to the on-premises virtual machine's VMDK.</span></span> <span data-ttu-id="fa871-168">如果您要保護 Windows 虛擬機器，您需要 Windows 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-168">If you are protecting Windows virtual machines, you need a Windows master target server.</span></span> <span data-ttu-id="fa871-169">您可以再次使用內部部署處理序伺服器和主要目標伺服器 <!-- !todo component -->。</span><span class="sxs-lookup"><span data-stu-id="fa871-169">You can reuse the on-premises process server and master target<!-- !todo component -->.</span></span> <span data-ttu-id="fa871-170">針對 Linux 虛擬機器，您需要設定其他內部部署 Linux 主要目標。</span><span class="sxs-lookup"><span data-stu-id="fa871-170">For Linux virtual machines, you need to set up an additional on-premises Linux master target.</span></span>


<span data-ttu-id="fa871-171">如需安裝主要目標伺服器的資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="fa871-171">For information about installing a master target server, see:</span></span>

* [<span data-ttu-id="fa871-172">如何安裝 Windows 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="fa871-172">How to install Windows master target server</span></span>](site-recovery-vmware-to-azure.md)
* [<span data-ttu-id="fa871-173">如何安裝 Linux 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="fa871-173">How to install Linux master target server</span></span>](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-the-on-premises-esxi-host-during-failback"></a><span data-ttu-id="fa871-174">在容錯回復期間，內部部署 ESXi 主機支援哪些資料存放區類型？</span><span class="sxs-lookup"><span data-stu-id="fa871-174">What datastore types are supported on the on-premises ESXi host during failback?</span></span>

<span data-ttu-id="fa871-175">目前，Azure Site Recovery 僅支援虛擬機器檔案系統 (VMFS) 或 vSAN 資料存放區的容錯回復。</span><span class="sxs-lookup"><span data-stu-id="fa871-175">Currently, Azure Site Recovery supports failing back only to a virtual machine file system (VMFS) or vSAN datastore.</span></span> <span data-ttu-id="fa871-176">不支援 NFS 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-176">A NFS datastore is not supported.</span></span> <span data-ttu-id="fa871-177">由於這項限制，重新保護畫面的資料存放區選取範圍輸入在 NFS 資料存放區中將找不到任何資料，或是仍會顯示 vSAN 資料存放區但在作業期間卻不會顯示。</span><span class="sxs-lookup"><span data-stu-id="fa871-177">Due to this limitation, the datastore selection input on the reprotect screen is empty in the case of NFS datastores, or it shows the vSAN datastore but fails during the job.</span></span> <span data-ttu-id="fa871-178">如果您想要容錯回復，可建立內部部署的 VMFS 資料存放區，也可容錯回復到 VMFS 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-178">If you intend to fail back, you can create a VMFS datastore on-premises and fail back to it.</span></span> <span data-ttu-id="fa871-179">此容錯回復會導致完整下載 VMDK。</span><span class="sxs-lookup"><span data-stu-id="fa871-179">This failback will cause a full download of the VMDK.</span></span>

### <a name="common-things-to-check-after-completing-installation-of-the-master-target-server"></a><span data-ttu-id="fa871-180">完成主要目標伺服器安裝後必須檢查的常見項目</span><span class="sxs-lookup"><span data-stu-id="fa871-180">Common things to check after completing installation of the master target server</span></span>

* <span data-ttu-id="fa871-181">若虛擬機器存在於內部部署 vCenter 伺服器上，主要目標伺服器必須能夠存取內部部署虛擬機器的 VMDK。</span><span class="sxs-lookup"><span data-stu-id="fa871-181">If the virtual machine is present on-premises on the vCenter server, the master target server needs access to the on-premises virtual machine's VMDK.</span></span> <span data-ttu-id="fa871-182">需要存取才可將複寫的資料寫入虛擬機器的磁碟。</span><span class="sxs-lookup"><span data-stu-id="fa871-182">Access is needed to write the replicated data to the virtual machine's disks.</span></span> <span data-ttu-id="fa871-183">請確定內部部署內部部署的資料存放區已掛接在主要目標的主機上並已設定讀寫權限。</span><span class="sxs-lookup"><span data-stu-id="fa871-183">Ensure that the on-premises virtual machine's datastore is mounted on the master target's host with read/write access.</span></span>

* <span data-ttu-id="fa871-184">如果虛擬機器不在 vCenter 伺服器上的內部部署環境，Site Recovery 服務需要在重新保護期間建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa871-184">If the virtual machine is not present on-premises on the vCenter server, the Site Recovery service needs to create a new virtual machine during reprotection.</span></span> <span data-ttu-id="fa871-185">您必須在建立主要目標的 ESX 主機上建立此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa871-185">This virtual machine is created on the ESX host on which you create the master target.</span></span> <span data-ttu-id="fa871-186">請謹慎選擇 ESX 主機，以便在您要的主機上建立容錯回復虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa871-186">Choose the ESX host carefully, so that the failback virtual machine is created on the host that you want.</span></span>

* <span data-ttu-id="fa871-187">您無法使用主要目標伺服器的儲存體 vMotion。</span><span class="sxs-lookup"><span data-stu-id="fa871-187">*You cannot use Storage vMotion for the master target server*.</span></span> <span data-ttu-id="fa871-188">這會造成容錯回復失敗。</span><span class="sxs-lookup"><span data-stu-id="fa871-188">This can cause the failback to fail.</span></span> <span data-ttu-id="fa871-189">虛擬機器無法啟動，因為磁碟不可供其使用。</span><span class="sxs-lookup"><span data-stu-id="fa871-189">The virtual machine can't start because the disks are not available to it.</span></span>

  > [!WARNING]
  > <span data-ttu-id="fa871-190">如果主要目標在重新保護後經歷儲存體 vMotion 工作，連結到主要目標的受保護虛擬機器磁碟將移轉到 vMotion 工作的目標。</span><span class="sxs-lookup"><span data-stu-id="fa871-190">If a master target undergoes a Storage vMotion task after reprotection, the protected virtual machines disks that are attached to the master target migrate to the target of the vMotion task.</span></span> <span data-ttu-id="fa871-191">如果您嘗試在此之後進行容錯回復，則中斷磁碟連結會由於找不到磁碟而失敗。</span><span class="sxs-lookup"><span data-stu-id="fa871-191">If you try to fail back after this, detachment of the disk fails because the disks are not found.</span></span> <span data-ttu-id="fa871-192">後來就很難在您的儲存體帳戶中找到磁碟。</span><span class="sxs-lookup"><span data-stu-id="fa871-192">It then becomes hard to find the disks in your storage accounts.</span></span> <span data-ttu-id="fa871-193">您必須手動找到這些磁碟並附加到虛擬機器之上。</span><span class="sxs-lookup"><span data-stu-id="fa871-193">You need to find them manually and attach them to the virtual machine.</span></span> <span data-ttu-id="fa871-194">而後，就可以啟動內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa871-194">After that, the on-premises virtual machine can be booted.</span></span>

* <span data-ttu-id="fa871-195">將新的磁碟機新增至現有的 Windows 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-195">Add a retention drive to your existing Windows master target server.</span></span> <span data-ttu-id="fa871-196">新增磁碟並格式化磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fa871-196">Add a new disk and format the drive.</span></span> <span data-ttu-id="fa871-197">保留磁碟機可用來停止虛擬機器複寫回到內部部署站台時的時間點。</span><span class="sxs-lookup"><span data-stu-id="fa871-197">The retention drive is used to stop the points in time when the virtual machine replicates back to the on-premises site.</span></span> <span data-ttu-id="fa871-198">以下是保留磁碟機的一些條件。</span><span class="sxs-lookup"><span data-stu-id="fa871-198">Following are some criteria of a retention drive.</span></span> <span data-ttu-id="fa871-199">若沒有這些條件，將不會針對主要目標伺服器列出磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fa871-199">Without these criteria, the drive will not be listed for the master target server.</span></span>

   * <span data-ttu-id="fa871-200">磁碟區不能使用於其他用途，例如做為複寫目標。</span><span class="sxs-lookup"><span data-stu-id="fa871-200">The volume is not used for any other purpose, such as a target of replication.</span></span>

   * <span data-ttu-id="fa871-201">磁碟區不處於鎖定模式。</span><span class="sxs-lookup"><span data-stu-id="fa871-201">The volume is not in lock mode.</span></span>

   * <span data-ttu-id="fa871-202">磁碟區不是快取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fa871-202">The volume is not a cache volume.</span></span> <span data-ttu-id="fa871-203">該磁碟區上不能有主要目標安裝。</span><span class="sxs-lookup"><span data-stu-id="fa871-203">The master target installation shouldn't exist on that volume.</span></span> <span data-ttu-id="fa871-204">處理伺服器和主要目標的自訂安裝磁碟區不符合做為保留磁碟區的資格。</span><span class="sxs-lookup"><span data-stu-id="fa871-204">The custom installation volume for the process server and master target is not eligible for a retention volume.</span></span> <span data-ttu-id="fa871-205">當處理序伺服器和主要目標安裝在磁碟區時，磁碟區是主要目標的快取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fa871-205">When the process server and master target are installed on a volume, the volume is a cache volume of the master target.</span></span>

   * <span data-ttu-id="fa871-206">磁碟區的檔案系統類型不能是 FAT 或 FAT32。</span><span class="sxs-lookup"><span data-stu-id="fa871-206">The file system type of the volume is not FAT or FAT32.</span></span>

   * <span data-ttu-id="fa871-207">磁碟區容量不是零。</span><span class="sxs-lookup"><span data-stu-id="fa871-207">The volume capacity is nonzero.</span></span>

   * <span data-ttu-id="fa871-208">Windows 的預設保留磁碟區為 R 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fa871-208">The default retention volume for Windows is the R volume.</span></span>

   * <span data-ttu-id="fa871-209">Linux 的預設保留磁碟區為 /mnt/retention。</span><span class="sxs-lookup"><span data-stu-id="fa871-209">The default retention volume for Linux is /mnt/retention.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="fa871-210">如果您使用現有的處理序伺服器/組態伺服器電腦，或使用級別或處理序伺服器/主要目標伺服器電腦，需要新增磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fa871-210">You need to add a new drive if you're using an existing process server/configuration server machine or a scale or a process server/master target server machine.</span></span> <span data-ttu-id="fa871-211">新的磁碟機應該符合前述需求。</span><span class="sxs-lookup"><span data-stu-id="fa871-211">The new drive should meet the preceding requirements.</span></span> <span data-ttu-id="fa871-212">如果保留磁碟機不存在，則不會出現在入口網站上的選取項目下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="fa871-212">If the retention drive is not present, it doesn't appear in the selection drop-down list on the portal.</span></span> <span data-ttu-id="fa871-213">將磁碟機新增至內部部署主要目標之後，磁碟機最多需要 15 分鐘才會出現在入口網站上的選取項目中。</span><span class="sxs-lookup"><span data-stu-id="fa871-213">After you add a drive to the on-premises master target, it takes up to 15 minutes for the drive to appear in the selection on the portal.</span></span> <span data-ttu-id="fa871-214">如果磁碟機未在 15 分鐘之後出現，您也可以重新整理設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-214">You can also refresh the configuration server if the drive does not appear after 15 minutes.</span></span>

* <span data-ttu-id="fa871-215">Linux 容錯移轉虛擬機器需要 Linux 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-215">A Linux failed-over virtual machine requires a Linux master target server.</span></span> <span data-ttu-id="fa871-216">Windows 容錯移轉虛擬機器需要 Windows 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-216">A Windows failed-over virtual machine requires a Windows master target server.</span></span>

* <span data-ttu-id="fa871-217">在主要目標伺服器上安裝 VMware 工具。</span><span class="sxs-lookup"><span data-stu-id="fa871-217">Install VMware tools on the master target server.</span></span> <span data-ttu-id="fa871-218">若沒有 VMware 工具，將無法偵測主要目標之 ESXi 主機上的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-218">Without the VMware tools, the datastores on the master target's ESXi host cannot be detected.</span></span>

* <span data-ttu-id="fa871-219">使用 vCenter 屬性在主要目標虛擬機器上啟用 `disk.EnableUUID=true` 參數。</span><span class="sxs-lookup"><span data-stu-id="fa871-219">Enable the `disk.EnableUUID=true` parameter on the master target virtual machine by using the vCenter properties.</span></span> <!-- !todo Needs link. -->

* <span data-ttu-id="fa871-220">主要目標應該至少連結一個 VMFS 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-220">The master target should have at least one VMFS datastore attached.</span></span> <span data-ttu-id="fa871-221">如果沒有的話，重新保護頁面上的**資料存放區**輸入會空白，您將無法繼續。</span><span class="sxs-lookup"><span data-stu-id="fa871-221">If there is none, the **Datastore** input on the reprotect page will be empty, and you can't proceed.</span></span>

* <span data-ttu-id="fa871-222">主要目標伺服器在磁碟上不能有快照集。</span><span class="sxs-lookup"><span data-stu-id="fa871-222">The master target server cannot have snapshots on the disks.</span></span> <span data-ttu-id="fa871-223">如果有快照集，重新保護和容錯回復會失敗。</span><span class="sxs-lookup"><span data-stu-id="fa871-223">If there are snapshots, reprotection and failback fail.</span></span>

* <span data-ttu-id="fa871-224">主要目標不能有 Paravirtual SCSI 控制器。</span><span class="sxs-lookup"><span data-stu-id="fa871-224">The master target cannot have a Paravirtual SCSI controller.</span></span> <span data-ttu-id="fa871-225">控制器只能是 LSI Logic 控制器。</span><span class="sxs-lookup"><span data-stu-id="fa871-225">The controller can only be an LSI Logic controller.</span></span> <span data-ttu-id="fa871-226">如果沒有 LSI Logic 控制器，重新保護會失敗。</span><span class="sxs-lookup"><span data-stu-id="fa871-226">Without an LSI Logic controller, reprotection fails.</span></span>

<!--
### Failback policy
To replicate back to on-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with the configuration server during creation.
2. This policy is not editable.
3. The set values of the policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-to-reprotect"></a><span data-ttu-id="fa871-227">重新保護的步驟</span><span class="sxs-lookup"><span data-stu-id="fa871-227">Steps to reprotect</span></span>

> [!NOTE]
> <span data-ttu-id="fa871-228">在 Azure 虛擬機器啟動之後，需要經過一些時間，代理程式才會註冊回到組態伺服器中 (最多 15 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="fa871-228">After a virtual machine boots in Azure, it takes some time for the agent to register back to the configuration server (up to 15 minutes).</span></span> <span data-ttu-id="fa871-229">在這段時間，重新保護會失敗，且有錯誤訊息指出未安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="fa871-229">During this time, reprotection fails, and an error message indicates that the agent is not installed.</span></span> <span data-ttu-id="fa871-230">請等候幾分鐘，然後再次嘗試重新保護。</span><span class="sxs-lookup"><span data-stu-id="fa871-230">Wait for a few minutes, and then try reprotection again.</span></span>



1. <span data-ttu-id="fa871-231">在 [保存庫] > [已複寫的項目] 中，以滑鼠右鍵按一下已容錯移轉的虛擬機器，然後選取 [重新保護]。</span><span class="sxs-lookup"><span data-stu-id="fa871-231">In **Vault** > **Replicated items**, right-click the virtual machine that's been failed over, and then select **Re-Protect**.</span></span> <span data-ttu-id="fa871-232">您也可以按一下機器，並從命令按鈕中選取**重新保護**。</span><span class="sxs-lookup"><span data-stu-id="fa871-232">You can also click the machine and select **Re-Protect** from the command buttons.</span></span>
2. <span data-ttu-id="fa871-233">在刀鋒視窗中，您可以看到已選取保護方向 [Azure 至內部部署]。</span><span class="sxs-lookup"><span data-stu-id="fa871-233">In the blade, notice that the direction of protection, **Azure to On-premises**, is already selected.</span></span>
3. <span data-ttu-id="fa871-234">在 [主要目標伺服器] 和 [處理伺服器] 中，選取內部部署主要目標伺服器和處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-234">In **Master Target Server** and **Process Server**, select the on-premises master target server and the process server.</span></span>
4. <span data-ttu-id="fa871-235">對於 [資料存放區]，選取您想要將內部部署磁碟復原至該位置的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-235">For **Datastore**, select the datastore to which you want to recover the disks on-premises.</span></span> <span data-ttu-id="fa871-236">當內部部署虛擬機器已被刪除且您需要建立新的磁碟時，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="fa871-236">This option is used when the on-premises virtual machine is deleted, and you need to create new disks.</span></span> <span data-ttu-id="fa871-237">如果磁碟已存在，則會忽略此選項，但您仍然需要指定一個值。</span><span class="sxs-lookup"><span data-stu-id="fa871-237">This option is ignored if the disks already exist, but you still need to specify a value.</span></span>
5. <span data-ttu-id="fa871-238">選擇保留磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fa871-238">Choose the retention drive.</span></span>
6. <span data-ttu-id="fa871-239">系統會自動選取容錯回復原則。</span><span class="sxs-lookup"><span data-stu-id="fa871-239">The failback policy is automatically selected.</span></span>
7. <span data-ttu-id="fa871-240">按一下 [確定] 以開始重新保護。</span><span class="sxs-lookup"><span data-stu-id="fa871-240">Click **OK** to begin reprotection.</span></span> <span data-ttu-id="fa871-241">隨即開始執行將虛擬機器從 Azure 複寫到內部部署網站的作業。</span><span class="sxs-lookup"><span data-stu-id="fa871-241">A job begins to replicate the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="fa871-242">您可以在 [作業]  索引標籤上追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="fa871-242">You can track the progress on the **Jobs** tab.</span></span>

<span data-ttu-id="fa871-243">如果您想要復原到替代位置 (當內部部署虛擬機器已被刪除時)，請選取為主要目標伺服器所設定的保留磁碟機和資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-243">If you want to recover to an alternate location (when the on-premises virtual machine is deleted), select the retention drive and datastore that are configured for the master target server.</span></span> <span data-ttu-id="fa871-244">當您容錯回復到內部部署網站時，容錯回復保護計畫中的 VMware 虛擬機器會使用與主要目標伺服器相同的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-244">When you fail back to the on-premises site, the VMware virtual machines in the failback protection plan use the same datastore as the master target server.</span></span> <span data-ttu-id="fa871-245">接著會在 vCenter 中建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa871-245">A new virtual machine is then created in vCenter.</span></span>

<span data-ttu-id="fa871-246">若要將 Azure 上的虛擬機器復原到現有的內部部署虛擬機器，請在主要目標伺服器的 ESXi 主機上掛接內部部署虛擬機器的資料存放區並設定讀寫權限。</span><span class="sxs-lookup"><span data-stu-id="fa871-246">If you want to recover the virtual machine on Azure to an existing on-premises virtual machine, mount the on-premises virtual machine's datastores with read/write access on the master target server's ESXi host.</span></span>
    <span data-ttu-id="fa871-247">![重新保護對話方塊](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)</span><span class="sxs-lookup"><span data-stu-id="fa871-247">![Re-protect dialog box](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)</span></span>

<span data-ttu-id="fa871-248">您也可以在復原計劃層級重新保護。</span><span class="sxs-lookup"><span data-stu-id="fa871-248">You can also reprotect at the level of a recovery plan.</span></span> <span data-ttu-id="fa871-249">只能透過復原方案重新保護複寫群組。</span><span class="sxs-lookup"><span data-stu-id="fa871-249">A replication group can be reprotected only through a recovery plan.</span></span> <span data-ttu-id="fa871-250">當您使用復原方案來重新保護時，您必須為每部受保護機器提供值。</span><span class="sxs-lookup"><span data-stu-id="fa871-250">When you reprotect by using a recovery plan, you need to provide the values for every protected machine.</span></span>

> [!NOTE]
> <span data-ttu-id="fa871-251">使用相同的主要目標伺服器來重新保護複寫群組。</span><span class="sxs-lookup"><span data-stu-id="fa871-251">Use the same master target server to reprotect a replication group.</span></span> <span data-ttu-id="fa871-252">如果使用不同的主要目標伺服器重新保護複寫群組，則伺服器無法提供共同的時間點。</span><span class="sxs-lookup"><span data-stu-id="fa871-252">If you use a different master target server to reprotect a replication group, the server cannot provide a common point in time.</span></span>

> [!NOTE]
> <span data-ttu-id="fa871-253">執行重新保護的期間，內部部署虛擬機器將會關閉。</span><span class="sxs-lookup"><span data-stu-id="fa871-253">The on-premises virtual machine is turned off during reprotection.</span></span> <span data-ttu-id="fa871-254">這有助於確保資料在複寫期間的一致性。</span><span class="sxs-lookup"><span data-stu-id="fa871-254">This helps ensure data consistency during replication.</span></span> <span data-ttu-id="fa871-255">完成重新保護之後，請勿開啟虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa871-255">Do not turn on the virtual machine after reprotection finishes.</span></span>

<span data-ttu-id="fa871-256">重新保護成功之後，虛擬機器將進入受保護狀態。</span><span class="sxs-lookup"><span data-stu-id="fa871-256">After the reprotection succeeds, the virtual machine will enter a protected state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa871-257">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa871-257">Next steps</span></span>

<span data-ttu-id="fa871-258">在虛擬機器進入受保護狀態後，您就可以[起始容錯回復](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back)。</span><span class="sxs-lookup"><span data-stu-id="fa871-258">After the virtual machine has entered a protected state, you can [initiate a failback](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back).</span></span> 

<span data-ttu-id="fa871-259">容錯回復會關閉 Azure 中的虛擬機器，並啟動內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa871-259">The failback will shut down the virtual machine in Azure and boot the on-premises virtual machine.</span></span> <span data-ttu-id="fa871-260">預期應用程式停機一段時間。</span><span class="sxs-lookup"><span data-stu-id="fa871-260">Expect some downtime for the application.</span></span> <span data-ttu-id="fa871-261">選擇應用程式允許停機時的容錯回復時間。</span><span class="sxs-lookup"><span data-stu-id="fa871-261">Choose a time for failback when the application can tolerate downtime.</span></span>

## <a name="common-problems"></a><span data-ttu-id="fa871-262">常見問題</span><span class="sxs-lookup"><span data-stu-id="fa871-262">Common problems</span></span>

* <span data-ttu-id="fa871-263">如果您使用範本來建立虛擬機器，請確定每部虛擬機器有磁碟本身的 UUID。</span><span class="sxs-lookup"><span data-stu-id="fa871-263">If you used a template to create your virtual machines, ensure that each virtual machine has its own UUID for the disks.</span></span> <span data-ttu-id="fa871-264">如果內部部署虛擬機器和主要目標的 UUID 衝突 (因為兩者都是從相同的範本建立)，則重新保護會失敗。</span><span class="sxs-lookup"><span data-stu-id="fa871-264">If the on-premises virtual machine's UUID clashes with that of the master target because both were created from the same template, reprotection fails.</span></span> <span data-ttu-id="fa871-265">部署另一個不是從相同範本建立的主要目標。</span><span class="sxs-lookup"><span data-stu-id="fa871-265">Deploy another master target that has not been created from the same template.</span></span>

* <span data-ttu-id="fa871-266">如果您執行唯讀的使用者 vCenter 探索並保護虛擬機器，保護會成功且容錯回復可作用。</span><span class="sxs-lookup"><span data-stu-id="fa871-266">If you perform a read-only user vCenter discovery and protect virtual machines, protection succeeds, and failover works.</span></span> <span data-ttu-id="fa871-267">在重新保護期間，容錯回復會失敗，因為無法探索資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-267">During reprotection, failover fails because the datastores cannot be discovered.</span></span> <span data-ttu-id="fa871-268">重新保護期間未列出資料存放區是容錯失敗的徵兆。</span><span class="sxs-lookup"><span data-stu-id="fa871-268">A symptom is that the datastores aren't listed during reprotection.</span></span> <span data-ttu-id="fa871-269">若要解決此問題，您可以使用有適當權限的帳戶更新 vCenter 認證並重試作業。</span><span class="sxs-lookup"><span data-stu-id="fa871-269">To resolve this problem, you can update the vCenter credential with an appropriate account that has permissions, and retry the job.</span></span> <span data-ttu-id="fa871-270">如需詳細資訊，請參閱[使用 Azure Site Recovery 將 VMWare 虛擬機器和實體伺服器複寫至 Azure](site-recovery-vmware-to-azure-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="fa871-270">For more information, see [Replicate VMware virtual machines and physical servers to Azure with Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).</span></span>

* <span data-ttu-id="fa871-271">當您將 Linux 虛擬機器容錯回復並在內部部署執行它時，您會看到 Network Manager 封裝已從該機器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="fa871-271">When you fail back a Linux virtual machine and run it on-premises, you can see that the Network Manager package has been uninstalled from the machine.</span></span> <span data-ttu-id="fa871-272">發生此解除安裝的原因是，當在 Azure 中復原虛擬機器時，Network Manager 套件已被移除。</span><span class="sxs-lookup"><span data-stu-id="fa871-272">This uninstallation happens because the Network Manager package is removed when the virtual machine is recovered in Azure.</span></span>

* <span data-ttu-id="fa871-273">當 Linux 虛擬機器已設定靜態 IP 位址且容錯移轉至 Azure 時，就會從 DHCP 取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fa871-273">When a Linux virtual machine is configured with a static IP address and is failed over to Azure, the IP address is acquired from DHCP.</span></span> <span data-ttu-id="fa871-274">當您容錯移轉至內部部署時，該虛擬機器會繼續使用 DHCP 取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fa871-274">When you fail over to on-premises, the virtual machine continues to use DHCP to acquire the IP address.</span></span> <span data-ttu-id="fa871-275">視需要手動登入機器，並將 IP 位址設定回靜態位址。</span><span class="sxs-lookup"><span data-stu-id="fa871-275">Manually sign in to the machine, and set the IP address back to a static address if necessary.</span></span> <span data-ttu-id="fa871-276">Windows 虛擬機器可以再次取得其靜態 IP。</span><span class="sxs-lookup"><span data-stu-id="fa871-276">A Windows virtual machine can acquire its static IP again.</span></span>

* <span data-ttu-id="fa871-277">如果您是使用 ESXi 5.5 免費版或 vSphere 6 Hypervisor 免費版，則容錯移轉會成功，但容錯回復不會成功。</span><span class="sxs-lookup"><span data-stu-id="fa871-277">If you use either ESXi 5.5 free edition or vSphere 6 Hypervisor free edition, failover succeeds, but failback does not succeed.</span></span> <span data-ttu-id="fa871-278">若要啟用容錯回復，請升級到上述程式的評估授權。</span><span class="sxs-lookup"><span data-stu-id="fa871-278">To enable failback, upgrade to either program's evaluation license.</span></span>

* <span data-ttu-id="fa871-279">若無法從處理伺服器連線到組態伺服器，請使用 Telnet 檢查連線到組態伺服器連接埠 443 的連線。</span><span class="sxs-lookup"><span data-stu-id="fa871-279">If you cannot reach the configuration server from the process server, use Telnet to check connectivity to the configuration server on port 443.</span></span> <span data-ttu-id="fa871-280">您也可以嘗試從處理伺服器 Ping 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa871-280">You can also try to ping the configuration server from the process server.</span></span> <span data-ttu-id="fa871-281">當處理伺服器已連線到組態伺服器時，應該會有活動訊號。</span><span class="sxs-lookup"><span data-stu-id="fa871-281">A process server should also have a heartbeat when it is connected to the configuration server.</span></span>

* <span data-ttu-id="fa871-282">如果您要嘗試容錯回復至替代的 vCenter，請確定您的新 vCenter 和主要目標伺服器均已被探索到。</span><span class="sxs-lookup"><span data-stu-id="fa871-282">If you are trying to fail back to an alternate vCenter, make sure that your new vCenter and the master target server are discovered.</span></span> <span data-ttu-id="fa871-283">一般的徵兆是，您會發現在 [重新保護] 對話方塊中無法存取/看到資料存放區。</span><span class="sxs-lookup"><span data-stu-id="fa871-283">A typical symptom is that the datastores are not accessible or visible in the **Reprotect** dialog box.</span></span>

* <span data-ttu-id="fa871-284">做為實體內部部署伺服器保護的 Windows Server 2008 R2 SP1 伺服器無法從 Azure 容錯回復到內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="fa871-284">A Windows Server 2008 R2 SP1 server that is protected as a physical on-premises server cannot be failed back from Azure to an on-premises site.</span></span>
