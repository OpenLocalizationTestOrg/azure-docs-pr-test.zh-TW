---
title: "如何從 Azure 容錯回復至 VMware | Microsoft Docs"
description: "將虛擬機器容錯移轉到 Azure 之後，您可以起始將虛擬機器容錯回復到內部部署的作業。 了解如何容錯回復的步驟。"
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
ms.openlocfilehash: 622604dc3ce69085feff6705168d58ad9938c429
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="fail-back-from-azure-to-an-on-premises-site"></a><span data-ttu-id="5f517-104">從 Azure 容錯回復至內部部署網站</span><span class="sxs-lookup"><span data-stu-id="5f517-104">Fail back from Azure to an on-premises site</span></span>

<span data-ttu-id="5f517-105">本文說明如何將虛擬機器從 Azure 虛擬機器容錯回復到內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="5f517-105">This article describes how to fail back virtual machines from Azure Virtual Machines to the on-premises site.</span></span> <span data-ttu-id="5f517-106">請遵循本文中的指示，將已使用[使用 Azure Site Recovery 將 VMWare 虛擬機器和實體伺服器複寫至 Azure](site-recovery-vmware-to-azure-classic.md) 教學課程從內部部署網站容錯移轉至 Azure 的 VMware 虛擬機器或 Windows/Linux 實體伺服器進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f517-106">Follow the instructions in this article to fail back your VMware virtual machines or Windows/Linux physical servers after they've failed over from the on-premises site to Azure by using the [Replicate VMware virtual machines and physical servers to Azure with Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) tutorial.</span></span>

> [!WARNING]
> <span data-ttu-id="5f517-107">如果您已[完成移轉](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)、已將虛擬機器移至另一個資源群組，或已刪除 Azure 虛擬機器，則您無法在之後執行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f517-107">If you have [completed migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), moved the virtual machine to another resource group, or deleted the Azure virtual machine, you cannot failback after that.</span></span>

> [!NOTE]
> <span data-ttu-id="5f517-108">如果您已對 VMware 虛擬機器進行容錯移轉，便無法容錯回復到 Hyper-v 主機。</span><span class="sxs-lookup"><span data-stu-id="5f517-108">If you have failed over VMware virtual machines then you cannot failback to a Hyper-v host.</span></span>

## <a name="overview-of-failback"></a><span data-ttu-id="5f517-109">容錯回復的概觀</span><span class="sxs-lookup"><span data-stu-id="5f517-109">Overview of failback</span></span>
<span data-ttu-id="5f517-110">容錯回復的運作方式如下。</span><span class="sxs-lookup"><span data-stu-id="5f517-110">Here is how failback works.</span></span> <span data-ttu-id="5f517-111">在容錯移轉至 Azure 之後，您可以透過幾個階段來容錯回復至內部部署網站：</span><span class="sxs-lookup"><span data-stu-id="5f517-111">After you have failed over to Azure, you fail back to your on-premises site in a few stages:</span></span>

1. <span data-ttu-id="5f517-112">[重新保護](site-recovery-how-to-reprotect.md) Azure 上的虛擬機器，讓它們開始複寫到內部部署網站中的 VMware 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f517-112">[Reprotect](site-recovery-how-to-reprotect.md) the virtual machines on Azure so that they start to replicate to VMware virtual machines in your on-premises site.</span></span> <span data-ttu-id="5f517-113">在此程序進行期間，您還需要︰</span><span class="sxs-lookup"><span data-stu-id="5f517-113">As part of this process, you also need to:</span></span>
    1. <span data-ttu-id="5f517-114">設定內部部署主要目標︰Windows 主要目標 (若為 Windows 虛擬機器) 和 [Linux 主要目標](site-recovery-how-to-install-linux-master-target.md) (若為 Linux 虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="5f517-114">Set up an on-premises master target: Windows master target for Windows virtual machines and [Linux master target](site-recovery-how-to-install-linux-master-target.md) for Linux virtual machines.</span></span>
    2. <span data-ttu-id="5f517-115">設定[處理序伺服器](site-recovery-vmware-setup-azure-ps-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="5f517-115">Set up a [process server](site-recovery-vmware-setup-azure-ps-resource-manager.md).</span></span>
    3. <span data-ttu-id="5f517-116">起始[重新保護](site-recovery-how-to-reprotect.md)。</span><span class="sxs-lookup"><span data-stu-id="5f517-116">Initiate [reprotect](site-recovery-how-to-reprotect.md).</span></span> <span data-ttu-id="5f517-117">這會關閉內部部署虛擬機器，並使 Azure 虛擬機器的資料與內部部署磁碟同步。</span><span class="sxs-lookup"><span data-stu-id="5f517-117">This will turn off the on-premises virtual machine and synchronize the Azure virtual machine's data with the on-premises disks.</span></span>
5. <span data-ttu-id="5f517-118">在 Azure 上的虛擬機器複寫至內部部署網站後，您可以起始從 Azure 到內部部署網站的容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f517-118">After your virtual machines on Azure are replicating to your on-premises site, you initiate a fail over from Azure to the on-premises site.</span></span>

<span data-ttu-id="5f517-119">容錯回復資料之後，您必須重新保護所容錯回復到的內部部署虛擬機器，使其開始複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="5f517-119">After your data has failed back, you reprotect the on-premises virtual machines that you failed back to, so that they start to replicate to Azure.</span></span>

<span data-ttu-id="5f517-120">如需快速概觀，請觀看下列有關如何從 Azure 容錯移轉到內部部署網站的影片。</span><span class="sxs-lookup"><span data-stu-id="5f517-120">For a quick overview, watch the following video about how to fail over from Azure to an on-premises site.</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-to-the-original-or-alternate-location"></a><span data-ttu-id="5f517-121">容錯回復到原始位置或替代位置</span><span class="sxs-lookup"><span data-stu-id="5f517-121">Fail back to the original or alternate location</span></span>

<span data-ttu-id="5f517-122">如果您已容錯移轉 VMware 虛擬機器，在它仍存在的前提下，您可以將它容錯回復到相同的來源內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f517-122">If you failed over a VMware virtual machine, you can fail back to the same source on-premises virtual machine if it still exists.</span></span> <span data-ttu-id="5f517-123">在此案例中，系統只會將變更複寫回來。</span><span class="sxs-lookup"><span data-stu-id="5f517-123">In this scenario, only the changes are replicated back.</span></span> <span data-ttu-id="5f517-124">此案例稱為原始位置復原。</span><span class="sxs-lookup"><span data-stu-id="5f517-124">This scenario is known as original location recovery.</span></span> <span data-ttu-id="5f517-125">如果內部部署虛擬機器不存在，則此案例是替代位置復原。</span><span class="sxs-lookup"><span data-stu-id="5f517-125">If the on-premises virtual machine does not exist, the scenario is an alternate location recovery.</span></span>

> [!NOTE]
> <span data-ttu-id="5f517-126">您只可容錯回復至原始的 vCenter 和組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f517-126">You can only failback to the original vCenter and configuration server.</span></span> <span data-ttu-id="5f517-127">您無法部署新的組態伺服器和使用它進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f517-127">You cannot deploy a new configuration server and failback using it.</span></span> <span data-ttu-id="5f517-128">此外，您無法將新的 vCenter 新增至現有組態伺服器及容錯回復到新的 vCenter。</span><span class="sxs-lookup"><span data-stu-id="5f517-128">Also, you cannot add a new vCenter to the exiting configuration server and failback into the new vCenter.</span></span>

#### <a name="original-location-recovery"></a><span data-ttu-id="5f517-129">原始位置復原</span><span class="sxs-lookup"><span data-stu-id="5f517-129">Original location recovery</span></span>

<span data-ttu-id="5f517-130">如果您要容錯回復到原始虛擬機器，則必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="5f517-130">If you fail back to the original virtual machine, the following conditions are required:</span></span>
* <span data-ttu-id="5f517-131">如果虛擬機器是由 vCenter 伺服器管理，主要目標的 ESX 主機應該可以存取虛擬機器資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5f517-131">If the virtual machine is managed by a vCenter server, then the master target's ESX host should have access to the virtual machine's datastore.</span></span>
* <span data-ttu-id="5f517-132">如果虛擬機器位於 ESX 主機上，但不是由 vCenter 管理，則虛擬機器的硬碟必須位於主要目標的主機可以存取的資料存放區中。</span><span class="sxs-lookup"><span data-stu-id="5f517-132">If the virtual machine is on an ESX host but isn’t managed by vCenter, then the hard disk of the virtual machine must be in a datastore that the master target's host can access.</span></span>
* <span data-ttu-id="5f517-133">如果虛擬機器位於 ESX 主機上，但未使用 vCenter，則應該先完成主要目標之 ESX 主機的探索後，才能重新保護。</span><span class="sxs-lookup"><span data-stu-id="5f517-133">If your virtual machine is on an ESX host and doesn't use vCenter, then you should complete discovery of the ESX host of the master target before you reprotect.</span></span> <span data-ttu-id="5f517-134">如果您要容錯回復實體伺服器，則也適用這一條件。</span><span class="sxs-lookup"><span data-stu-id="5f517-134">This applies if you're failing back physical servers, too.</span></span>
* <span data-ttu-id="5f517-135">您可以容錯回復至虛擬存放區域網路 (vSAN) 或以原始裝置對應 (RDM) 為基礎的磁碟 (如果磁碟已存在並連線到內部部署虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="5f517-135">You can fail back to a virtual storage area network (vSAN) or a disk that based on raw device mapping (RDM) if the disks already exist and are connected to the on-premises virtual machine.</span></span>

#### <a name="alternate-location-recovery"></a><span data-ttu-id="5f517-136">替代位置復原</span><span class="sxs-lookup"><span data-stu-id="5f517-136">Alternate location recovery</span></span>
<span data-ttu-id="5f517-137">如果在重新保護虛擬機器之前，內部部署虛擬機器不存在，則此案例稱為替代位置復原。</span><span class="sxs-lookup"><span data-stu-id="5f517-137">If the on-premises virtual machine does not exist before reprotecting the virtual machine, the scenario is called an alternate location recovery.</span></span> <span data-ttu-id="5f517-138">重新保護工作流程會重新建立內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f517-138">The reprotect workflow creates the on-premises virtual machine again.</span></span> <span data-ttu-id="5f517-139">這也會導致下載完整資料。</span><span class="sxs-lookup"><span data-stu-id="5f517-139">This will also cause a full data download.</span></span>

* <span data-ttu-id="5f517-140">當您容錯回復至替代位置時，虛擬機器會復原到主要目標伺服器部署所在的相同 ESX 主機上。</span><span class="sxs-lookup"><span data-stu-id="5f517-140">When you fail back to an alternate location, the virtual machine will be recovered to the same ESX host on which the master target server is deployed.</span></span> <span data-ttu-id="5f517-141">用於建立磁碟的資料存放區將會是重新保護虛擬機器時選取的相同資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5f517-141">The datastore that's used to create the disk will be the same datastore that was selected when reprotecting the virtual machine.</span></span>
* <span data-ttu-id="5f517-142">您只能容錯回復到虛擬機器檔案系統 (VMFS) 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5f517-142">You can fail back only to a virtual machine file system (VMFS) datastore.</span></span> <span data-ttu-id="5f517-143">若您有 vSAN 或 RDM，重新保護與容錯回復將無法運作。</span><span class="sxs-lookup"><span data-stu-id="5f517-143">If you have a vSAN or RDM, reprotect and failback will not work.</span></span>
* <span data-ttu-id="5f517-144">重新保護程序涉及一項大型的初始資料傳輸作業以及緊接著的變更作業。</span><span class="sxs-lookup"><span data-stu-id="5f517-144">Reprotect involves one large initial data transfer that's followed by the changes.</span></span> <span data-ttu-id="5f517-145">之所以會有此程序，是因為虛擬機器未存在於內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="5f517-145">This process exists because the virtual machine does not exist on premises.</span></span> <span data-ttu-id="5f517-146">系統需要將完整資料複寫回來。</span><span class="sxs-lookup"><span data-stu-id="5f517-146">The complete data needs to be replicated back.</span></span> <span data-ttu-id="5f517-147">此重新保護作業也需要比原始位置復原更長的時間。</span><span class="sxs-lookup"><span data-stu-id="5f517-147">This reprotect will also take more time than an original location recovery.</span></span>
* <span data-ttu-id="5f517-148">您無法容錯回復至 vSAN 或 RDM 型磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f517-148">You cannot fail back to vSAN- or RDM-based disks.</span></span> <span data-ttu-id="5f517-149">新的虛擬機器磁碟 (VMDK) 才能建立在 VMFS 資料存放區上。</span><span class="sxs-lookup"><span data-stu-id="5f517-149">Only new virtual machine disks (VMDKs) can be created on a VMFS datastore.</span></span>

<span data-ttu-id="5f517-150">將實體機器容錯回復到 Azure 時，只能容錯回復為 VMware 虛擬機器 (亦稱為 P2A2V)。</span><span class="sxs-lookup"><span data-stu-id="5f517-150">A physical machine, when failed over to Azure, can be failed back only as a VMware virtual machine (also referred to as P2A2V).</span></span> <span data-ttu-id="5f517-151">此流程是屬於替代位置復原的範圍。</span><span class="sxs-lookup"><span data-stu-id="5f517-151">This flow falls under the alternate location recovery.</span></span>

* <span data-ttu-id="5f517-152">Windows Server 2008 R2 SP1 實體伺服器如果受保護且容錯移轉至 Azure，則無法容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f517-152">A Windows Server 2008 R2 SP1 physical server, if protected and failed over to Azure, cannot be failed back.</span></span>
* <span data-ttu-id="5f517-153">請確定您至少探索一部主要目標伺服器以及需要容錯回復到的必要 ESX/ESXi 主機。</span><span class="sxs-lookup"><span data-stu-id="5f517-153">Ensure that you discover at least one master target server and the necessary ESX/ESXi hosts to which you need to fail back.</span></span>

## <a name="have-you-completed-reprotection"></a><span data-ttu-id="5f517-154">您已完成重新保護嗎？</span><span class="sxs-lookup"><span data-stu-id="5f517-154">Have you completed reprotection?</span></span>
<span data-ttu-id="5f517-155">繼續之前，請先完成重新保護步驟，使虛擬機器處於已複寫狀態，這樣才能起始容錯移轉回到內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="5f517-155">Before you proceed, complete the reprotect steps so that the virtual machines are in a replicated state, and you can initiate a failover back to an on-premises site.</span></span> <span data-ttu-id="5f517-156">如需詳細資訊，請參閱[如何從 Azure 移至內部部署來重新保護](site-recovery-how-to-reprotect.md)。</span><span class="sxs-lookup"><span data-stu-id="5f517-156">For more information, see [How to reprotect from Azure to on-premises](site-recovery-how-to-reprotect.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f517-157">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f517-157">Prerequisites</span></span>

* <span data-ttu-id="5f517-158">執行容錯回復時，組態伺服器必須為內部部署。</span><span class="sxs-lookup"><span data-stu-id="5f517-158">A configuration server is required on premises when you do a failback.</span></span> <span data-ttu-id="5f517-159">在容錯回復期間，虛擬機器必須存在於組態伺服器資料庫中，否則容錯回復會失敗。</span><span class="sxs-lookup"><span data-stu-id="5f517-159">During failback, the virtual machine must exist in the configuration server database, or failback won't succeed.</span></span> <span data-ttu-id="5f517-160">因此，請確定您有排定來定期備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f517-160">Thus, ensure that you take regularly scheduled backups of your server.</span></span> <span data-ttu-id="5f517-161">發生災害時，您需要使用相同的 IP 位址來還原伺服器，以便容錯回復能夠運作。</span><span class="sxs-lookup"><span data-stu-id="5f517-161">If there was a disaster, you will need to restore the server with the same IP address for failback to work.</span></span>
* <span data-ttu-id="5f517-162">觸發容錯回復之前，主要目標伺服器不能有任何快照集。</span><span class="sxs-lookup"><span data-stu-id="5f517-162">The master target server should not have any snapshots before triggering failback.</span></span>

## <a name="steps-to-fail-back"></a><span data-ttu-id="5f517-163">容錯回復的步驟</span><span class="sxs-lookup"><span data-stu-id="5f517-163">Steps to fail back</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f517-164">起始容錯回復之前，請確定您已完成虛擬機器的重新保護。</span><span class="sxs-lookup"><span data-stu-id="5f517-164">Before you initiate failback, ensure that you have completed reprotection of the virtual machines.</span></span> <span data-ttu-id="5f517-165">虛擬機器應該處於受保護狀態，且其健康狀態應該是**良好**。</span><span class="sxs-lookup"><span data-stu-id="5f517-165">The virtual machines should be in a protected state, and their health should be **OK**.</span></span> <span data-ttu-id="5f517-166">若要重新保護虛擬機器，請參閱[如何重新保護](site-recovery-how-to-reprotect.md)。</span><span class="sxs-lookup"><span data-stu-id="5f517-166">To reprotect the virtual machines, read [how to reprotect](site-recovery-how-to-reprotect.md).</span></span>

1. <span data-ttu-id="5f517-167">在 [複製的項目] 頁面中，請選取虛擬機器，並以滑鼠右鍵按一下以選取 [非計劃性容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="5f517-167">In the replicated items page, select the virtual machine, and right-click it to select **Unplanned Failover**.</span></span>
2. <span data-ttu-id="5f517-168">在 [確認容錯移轉] 中，確認容錯移轉方向 (以 Azure 為來源)，然後選取您想要用來進行容錯移轉的復原點 (最近的復原點或最近的應用程式一致復原點)。</span><span class="sxs-lookup"><span data-stu-id="5f517-168">In **Confirm Failover**, verify the failover direction (from Azure), and then select the recovery point (latest, or the latest app consistent) that you want to use for the failover.</span></span> <span data-ttu-id="5f517-169">應用程式一致復原點會在最近的復原點之後，並造成部分資料遺失。</span><span class="sxs-lookup"><span data-stu-id="5f517-169">The app consistent point is behind the latest point in time and causes some data loss.</span></span>
3. <span data-ttu-id="5f517-170">在容錯移轉期間，Site Recovery 會將 Azure 上的虛擬機器關閉。</span><span class="sxs-lookup"><span data-stu-id="5f517-170">During failover, Site Recovery shuts down the virtual machines on Azure.</span></span> <span data-ttu-id="5f517-171">在確認容錯回復已如預期完成後，您可以確認 Azure 上的虛擬機器是否已關閉。</span><span class="sxs-lookup"><span data-stu-id="5f517-171">After you check that failback has completed as expected, you can check that the virtual machines on Azure have been shut down.</span></span>

### <a name="to-what-recovery-point-can-i-fail-back-the-virtual-machines"></a><span data-ttu-id="5f517-172">我可以將虛擬機器容錯回復至哪個復原點？</span><span class="sxs-lookup"><span data-stu-id="5f517-172">To what recovery point can I fail back the virtual machines?</span></span>

<span data-ttu-id="5f517-173">在容錯回復期間，有兩個選項讓您容錯回復虛擬機器/復原方案。</span><span class="sxs-lookup"><span data-stu-id="5f517-173">During failback, you have two options to fail back the virtual machine/recovery plan.</span></span>

<span data-ttu-id="5f517-174">如果您選取最近處理的時間點，所有虛擬機器會容錯移轉至其最新可用的時間點。</span><span class="sxs-lookup"><span data-stu-id="5f517-174">If you select the latest processed point in time, all virtual machines will be failed over to their latest available point in time.</span></span> <span data-ttu-id="5f517-175">如果復原方案內有複寫群組，則複寫群組的每個虛擬機器會容錯移轉至其獨自的最新時間點。</span><span class="sxs-lookup"><span data-stu-id="5f517-175">In case there is a replication group within the recovery plan, then each virtual machine of the replication group will fail over to its independent latest point in time.</span></span>

<span data-ttu-id="5f517-176">虛擬機器擁有至少一個復原點之後，才能予以容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f517-176">You cannot fail back a virtual machine until it has at least one recovery point.</span></span> <span data-ttu-id="5f517-177">復原方案的所有虛擬機器至少要有一個復原點，您才能容錯回復此復原方案。</span><span class="sxs-lookup"><span data-stu-id="5f517-177">You cannot fail back a recovery plan until all its virtual machines have at least one recovery point.</span></span>

> [!NOTE]
> <span data-ttu-id="5f517-178">最新復原點是損毀一致復原點。</span><span class="sxs-lookup"><span data-stu-id="5f517-178">A latest recovery point is a crash-consistent recovery point.</span></span>

<span data-ttu-id="5f517-179">如果您選取應用程式一致復原點，單一虛擬機器容錯回復會復原至其最新可用的應用程式一致復原點。</span><span class="sxs-lookup"><span data-stu-id="5f517-179">If you select the application consistent recovery point, a single virtual machine failback will recover to its latest available application-consistent recovery point.</span></span> <span data-ttu-id="5f517-180">如果復原方案有複寫群組，每個複寫群組會復原至其一般可用的復原點。</span><span class="sxs-lookup"><span data-stu-id="5f517-180">In the case of a recovery plan with a replication group, each replication group will recover to its common available recovery point.</span></span>
<span data-ttu-id="5f517-181">請注意，應用程式一致復原點的時間會落後，可能會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="5f517-181">Note that application-consistent recovery points can be behind in time, and there might be loss in data.</span></span>

### <a name="what-happens-to-vmware-tools-post-failback"></a><span data-ttu-id="5f517-182">VMware 工具在容錯回復後會發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="5f517-182">What happens to VMware tools post failback?</span></span>

<span data-ttu-id="5f517-183">容錯移轉至 Azure 期間，VMware 工具無法在 Azure 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="5f517-183">During failover to Azure, the VMware tools cannot be running on the Azure virtual machine.</span></span> <span data-ttu-id="5f517-184">萬一遇上 Windows 虛擬機器，ASR 會在容錯移轉期間停用 VMware 工具。</span><span class="sxs-lookup"><span data-stu-id="5f517-184">In case of a Windows virtual machine, ASR disables the VMware tools during failover.</span></span> <span data-ttu-id="5f517-185">萬一遇上 Linux 虛擬機器，ASR 會在容錯移轉期間解除安裝 VMware 工具。</span><span class="sxs-lookup"><span data-stu-id="5f517-185">In case of Linux virtual machine, ASR uninstalls the VMware tools during failover.</span></span>

<span data-ttu-id="5f517-186">在 Windows 虛擬機器容錯回復期間，VMware 工具也會在容錯回復之後立即重新啟用。</span><span class="sxs-lookup"><span data-stu-id="5f517-186">During failback of the Windows virtual machine, the VMware tools are re-enabled upon failback.</span></span> <span data-ttu-id="5f517-187">同樣地，針對 Linux 虛擬機器，VMware 工具會在容錯回復期間重新安裝於電腦上。</span><span class="sxs-lookup"><span data-stu-id="5f517-187">Similarly, for a linux virtual machine, the VMware tools are reinstalled on the machine during failback.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f517-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f517-188">Next steps</span></span>

<span data-ttu-id="5f517-189">容錯回復完成之後，您必須認可虛擬機器，以確保系統會刪除 Azure 中的已復原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f517-189">After failback finishes, you need to commit the virtual machine to ensure that recovered virtual machines in Azure are deleted.</span></span>

### <a name="commit"></a><span data-ttu-id="5f517-190">認可</span><span class="sxs-lookup"><span data-stu-id="5f517-190">Commit</span></span>
<span data-ttu-id="5f517-191">需要認可，以便從 Azure 移除容錯移轉的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f517-191">Commit is required to remove the failed over virtual machine from Azure.</span></span>
<span data-ttu-id="5f517-192">請以滑鼠右鍵按一下受保護的項目，然後按一下 [認可]。</span><span class="sxs-lookup"><span data-stu-id="5f517-192">Right-click the protected item, and then click **Commit**.</span></span> <span data-ttu-id="5f517-193">此時會有作業移除 Azure 中已容錯移轉的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f517-193">A job will remove the failed over virtual machines in Azure.</span></span>

### <a name="reprotect-from-on-premises-to-azure"></a><span data-ttu-id="5f517-194">從內部部署移至 Azure 來重新保護</span><span class="sxs-lookup"><span data-stu-id="5f517-194">Reprotect from on-premises to Azure</span></span>

<span data-ttu-id="5f517-195">在認可完成後，虛擬機器會回到內部部署網站上，但不會受到保護。</span><span class="sxs-lookup"><span data-stu-id="5f517-195">After commit finishes, your virtual machine is back on the on-premises site, but it won’t be protected.</span></span> <span data-ttu-id="5f517-196">若要再次開始複寫至 Azure，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="5f517-196">To start to replicate to Azure again, do the following:</span></span>

1. <span data-ttu-id="5f517-197">在 [保存庫] > [設定] > [已複寫的項目] 中，選取已容錯回復的虛擬機器，然後按一下 [重新保護]。</span><span class="sxs-lookup"><span data-stu-id="5f517-197">In **Vault** > **Setting** > **Replicated items**, select the virtual machines that have failed back, and then click **Re-Protect**.</span></span>
2. <span data-ttu-id="5f517-198">提供必須用來將資料傳送回 Azure 之處理伺服器的值。</span><span class="sxs-lookup"><span data-stu-id="5f517-198">Give the value of the process server that needs to be used to send data back to Azure.</span></span>
3. <span data-ttu-id="5f517-199">按一下 [確定] 以開始重新保護作業。</span><span class="sxs-lookup"><span data-stu-id="5f517-199">Click **OK** to begin the reprotect job.</span></span>

> [!NOTE]
> <span data-ttu-id="5f517-200">在內部部署虛擬機器啟動之後，需要經過一些時間，代理程式才會註冊回到組態伺服器中 (最多 15 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="5f517-200">After an on-premises virtual machine boots up, it takes some time for the agent to register back to the configuration server (up to 15 minutes).</span></span> <span data-ttu-id="5f517-201">在這段時間，重新保護會失敗，並傳回錯誤訊息以指出未安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="5f517-201">During this time, reprotect fails and returns an error message stating that the agent is not installed.</span></span> <span data-ttu-id="5f517-202">請等候幾分鐘，然後再次嘗試重新保護。</span><span class="sxs-lookup"><span data-stu-id="5f517-202">Wait for a few minutes, and then try reprotect again.</span></span>

<span data-ttu-id="5f517-203">重新保護作業完成之後，虛擬機器會複寫回到 Azure，而且您可以執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5f517-203">After the reprotect job finishes, the virtual machine is replicating back to Azure, and you can do a failover.</span></span>

## <a name="common-issues"></a><span data-ttu-id="5f517-204">常見問題</span><span class="sxs-lookup"><span data-stu-id="5f517-204">Common issues</span></span>
<span data-ttu-id="5f517-205">請先確定 vCenter 處於已連線狀態，再進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f517-205">Make sure that the vCenter is in a connected state before you do a failback.</span></span> <span data-ttu-id="5f517-206">否則，將磁碟中斷連線並將它們重新連結至虛擬機器的作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="5f517-206">Otherwise, disconnecting disks and attaching them back to the virtual machine will fail.</span></span>
