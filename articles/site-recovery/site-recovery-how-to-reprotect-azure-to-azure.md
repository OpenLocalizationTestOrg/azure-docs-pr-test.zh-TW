---
title: "如何對於容錯移轉的 Azure 虛擬機器在回復到主要 Azure 區域時重新保護 |Microsoft Docs"
description: "VM 從一個 Azure 區域容錯移轉到另一個 Azure 區域後，您可以使用 Azure Site Recovery 反方向保護機器。 了解在容錯移轉之前再次進行重新保護的步驟。"
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
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 32f5d2d142940bc515849dcd0edb1bb1f152aa6d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-to-primary-region"></a><span data-ttu-id="5f7ba-104">對於容錯移轉的 Azure 區域在回復到主要區域時重新保護</span><span class="sxs-lookup"><span data-stu-id="5f7ba-104">Reprotect from failed over Azure region back to primary region</span></span>



>[!NOTE]
>
> <span data-ttu-id="5f7ba-105">Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-105">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>


## <a name="overview"></a><span data-ttu-id="5f7ba-106">概觀</span><span class="sxs-lookup"><span data-stu-id="5f7ba-106">Overview</span></span>
<span data-ttu-id="5f7ba-107">您將虛擬機器從一個 Azure 區域[容錯移轉](site-recovery-failover.md)到另一個區域時，虛擬機器處於未受保護的狀態。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-107">When you [failover](site-recovery-failover.md) the virtual machines from one Azure region to another, the virtual machines are in an unprotected state.</span></span> <span data-ttu-id="5f7ba-108">如果您想要使它們回復到主要區域，需要先保護虛擬機器，然後再次進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-108">If you want to bring them back to the primary region, you need to first protect the virtual machines and then failover again.</span></span> <span data-ttu-id="5f7ba-109">朝任一個方向進行容錯移轉沒有任何差異。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-109">There is no difference between how you failover in one direction or other.</span></span> <span data-ttu-id="5f7ba-110">同樣地，啟用虛擬機器的保護後，容錯移轉後或容錯回復後的重新保護沒有任何差異。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-110">Similarly, post enable protection of the virtual machines, there is no difference between the reprotect post failover, or post failback.</span></span>
<span data-ttu-id="5f7ba-111">為了說明重新保護的工作流程，並避免混淆，我們將使用東亞地區做為受保護電腦的主要網站，並使用東南亞地區做為機器的復原網站。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-111">To explain the workflows of reprotect, and to avoid confusion, we will use the primary site of the protected machines as East Asia region, and the recovery site of the machines as South East Asia region.</span></span> <span data-ttu-id="5f7ba-112">在容錯移轉期間，您會將虛擬機器容錯移轉至東南亞地區。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-112">During failover, you will failover the virtual machines to the South East Asia region.</span></span> <span data-ttu-id="5f7ba-113">在容錯回復前，您需要重新保護從東南亞回復到東亞的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-113">Before you failback, you need to reprotect the virtual machines from South East Asia back to East Asia.</span></span> <span data-ttu-id="5f7ba-114">本文說明使用重新保護的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-114">This article describes the steps on how to reprotect.</span></span>

> [!WARNING]
> <span data-ttu-id="5f7ba-115">如果您已[完成移轉](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)、已將虛擬機器移至另一個資源群組，或已刪除 Azure 虛擬機器，則您無法在之後執行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-115">If you have [completed migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), moved the virtual machine to another resource group, or deleted the Azure virtual machine, you cannot failback after that.</span></span>

<span data-ttu-id="5f7ba-116">完成重新保護且受保護的虛擬機器開始複寫之後，您可以在虛擬機器上起始容錯移轉，以將它們回復到東亞地區。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-116">After reprotect finishes and the protected virtual machines are replicating, you can initiate a failover on the virtual machines to bring them back to East Asia region.</span></span>

<span data-ttu-id="5f7ba-117">在本文末尾或 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 中張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-117">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f7ba-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f7ba-118">Prerequisites</span></span>
1. <span data-ttu-id="5f7ba-119">虛擬機器應該已獲得認可。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-119">The virtual machines should have been committed.</span></span>
2. <span data-ttu-id="5f7ba-120">目標網站 (在此情況下為東亞 Azure 區域) 應該可供使用，而且應該能夠存取/建立該區域的新資源。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-120">The target site - in this case the East Asia Azure region should be available and should be able to access/create new resources in that region.</span></span>

## <a name="steps-to-reprotect"></a><span data-ttu-id="5f7ba-121">重新保護的步驟</span><span class="sxs-lookup"><span data-stu-id="5f7ba-121">Steps to reprotect</span></span>

<span data-ttu-id="5f7ba-122">以下是使用預設設定重新保護虛擬機器的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-122">Following are the steps to reprotect a virtual machine using the defaults.</span></span>

1. <span data-ttu-id="5f7ba-123">在 [保存庫] > [已複寫的項目] 中，以滑鼠右鍵按一下已容錯移轉的虛擬機器，然後選取 [重新保護]。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-123">In **Vault** > **Replicated items**, right-click the virtual machine that's been failed over, and then select **Re-Protect**.</span></span> <span data-ttu-id="5f7ba-124">您也可以按一下機器，並從命令按鈕中選取**重新保護**。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-124">You can also click the machine and select **Re-Protect** from the command buttons.</span></span>

![按一下滑鼠右鍵進行重新保護](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. <span data-ttu-id="5f7ba-126">在刀鋒視窗中，注意保護的方向，[東南亞至東亞] 已選取。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-126">In the blade, notice that the direction of protection, **Southeast Asia to East asia**, is already selected.</span></span>

![重新保護刀鋒視窗](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. <span data-ttu-id="5f7ba-128">檢閱**資源群組、網路、儲存體和可用性設定組**資訊，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-128">Review the **Resource group, Network, Storage and Availability sets** information and click OK.</span></span> <span data-ttu-id="5f7ba-129">如果沒有任何標記為 (新) 的資源，將在重新保護時建立資訊。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-129">If there are any resources marked (new), they will be created as part of the reprotect.</span></span>

<span data-ttu-id="5f7ba-130">這將觸發工作重新保護工作，首先會在目標網站 (在此情況下為 SEA) 植入最新的資料，完成後將複寫差異部分，然後容錯移轉回東南亞。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-130">This will trigger a job reprotect job that will first seed the target site (SEA in this case) with the latest data, and once that completes, will replicate the deltas before you failover back to Southeast Asia.</span></span>

### <a name="reprotect-customization"></a><span data-ttu-id="5f7ba-131">重新保護自訂</span><span class="sxs-lookup"><span data-stu-id="5f7ba-131">Reprotect customization</span></span>
<span data-ttu-id="5f7ba-132">如果您要在重新保護時選擇擷取儲存體帳戶或網路，可以使用重新保護刀鋒視窗上提供的自訂選項。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-132">If you want to choose the extract storage account or the network during reprotect, you can do so using the customize option provided on the reprotect blade.</span></span>

![自訂選項](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

<span data-ttu-id="5f7ba-134">您可以在重新保護期間自訂目標虛擬機器的下列屬性。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-134">You can customize the following properties of he target virtual machine during reprotect.</span></span>

![自訂刀鋒視窗](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|<span data-ttu-id="5f7ba-136">屬性</span><span class="sxs-lookup"><span data-stu-id="5f7ba-136">Property</span></span> |<span data-ttu-id="5f7ba-137">注意事項</span><span class="sxs-lookup"><span data-stu-id="5f7ba-137">Notes</span></span>  |
|---------|---------|
|<span data-ttu-id="5f7ba-138">目標資源群組</span><span class="sxs-lookup"><span data-stu-id="5f7ba-138">Target resource group</span></span>     | <span data-ttu-id="5f7ba-139">您可以選擇變更將建立虛擬機器的目標資源群組。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-139">You can choose to change the target resource group in which th virtual machine will be created.</span></span> <span data-ttu-id="5f7ba-140">進行重新保護時，會刪除目標虛擬機器，因此您可以選擇新的資源群組，以便在容錯移轉後建立 VM</span><span class="sxs-lookup"><span data-stu-id="5f7ba-140">As the part of reprotect, the target virtual machine will be deleted, hence you can choose a new resource group under which you can create the VM post failover</span></span>         |
|<span data-ttu-id="5f7ba-141">目標虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5f7ba-141">Target Virtual Network</span></span>     | <span data-ttu-id="5f7ba-142">重新保護時無法變更網路。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-142">Network cannot be changed during the reprotect.</span></span> <span data-ttu-id="5f7ba-143">若要變更網路，請重新進行網路對應。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-143">To change the network, redo the network mapping.</span></span>         |
|<span data-ttu-id="5f7ba-144">目標儲存體</span><span class="sxs-lookup"><span data-stu-id="5f7ba-144">Target Storage</span></span>     | <span data-ttu-id="5f7ba-145">您可以變更將在容錯移轉後建立虛擬機器的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-145">You can change the storage account to which the virtual machine will be created post failover.</span></span>         |
|<span data-ttu-id="5f7ba-146">快取儲存體</span><span class="sxs-lookup"><span data-stu-id="5f7ba-146">Cache Storage</span></span>     | <span data-ttu-id="5f7ba-147">您可以指定將在複寫期間使用的快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-147">You can specify a cache storage account which will be used during replication.</span></span> <span data-ttu-id="5f7ba-148">如果您使用預設值，將建立新的快取儲存體帳戶 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-148">If you go with the defaults, a new cache storage account will be created, if it does not already exist.</span></span>         |
|<span data-ttu-id="5f7ba-149">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="5f7ba-149">Availability Set</span></span>     |<span data-ttu-id="5f7ba-150">如果東亞中的虛擬機器屬於可用性設定組，您可以在東南亞選擇目標虛擬機器的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-150">If the virtual machine in East Asia is part of an availability set, you can choose an availability set for the target virtual machine in Southeast Asia.</span></span> <span data-ttu-id="5f7ba-151">預設值會尋找現有 SEA 可用性設定組，並試著使用它。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-151">Defaults will find the existing SEA availability set and try to use it.</span></span> <span data-ttu-id="5f7ba-152">進行自訂時，您可以指定全新的 AV 設定組。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-152">During customization, you can specify a completely new AV set.</span></span>         |


### <a name="what-happens-during-reprotect"></a><span data-ttu-id="5f7ba-153">重新保護期間會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="5f7ba-153">What happens during reprotect?</span></span>

<span data-ttu-id="5f7ba-154">就和第一個啟用保護之後的情況一樣，以下是您使用預設設定建立的項目。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-154">Just like after the first enable protection, following are the artefacts that get created if you use the defaults.</span></span>
1. <span data-ttu-id="5f7ba-155">在東亞地區中會建立快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-155">A cache storage account gets created in the East Asia region.</span></span>
2. <span data-ttu-id="5f7ba-156">如果目標儲存體帳戶 (東南亞 VM 的原始儲存體帳戶) 不存在，會建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-156">If the target storage account (the original storage account of the Southeast Asia VM) does not exist, a new one is created.</span></span> <span data-ttu-id="5f7ba-157">名稱為東亞虛擬機器的儲存體帳戶加上後置字元「asr」。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-157">The name is the East Asia virtual machine's storage account suffixed with "asr".</span></span>
3. <span data-ttu-id="5f7ba-158">如果目標 AV 設定組不存在，而且預設值偵測到需要建立新的 AV 設定組，則會在重新保護工作中建立。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-158">If the target AV set does not exist, and the defaults detect that it needs to create a new AV set, then it will be created as part of the reprotect job.</span></span> <span data-ttu-id="5f7ba-159">如果您已自訂重新保護，將使用選取的 AV 設定組。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-159">If you have customized the reprotect, then the selected AV set will be used.</span></span>
4.

<span data-ttu-id="5f7ba-160">以下是將觸發重新保護工作時發生的步驟列出的清單。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-160">The following are the list of steps that happen when you trigger a reprotect job.</span></span> <span data-ttu-id="5f7ba-161">這是以目標端虛擬機器存在的情況為準。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-161">This is in the case the target side virtual machine exists.</span></span>

1. <span data-ttu-id="5f7ba-162">重新保護時會建立需要的項目。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-162">The required artefacts are created as part of reprotect.</span></span> <span data-ttu-id="5f7ba-163">如果這些項目已存在，則會重複使用。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-163">If they already exist, then they are reused.</span></span>
2. <span data-ttu-id="5f7ba-164">目標端 (東南亞) 虛擬機器會先關閉 (如果正在執行)。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-164">The target side (Southeast Asia) virtual machine is first turned off, if it is running.</span></span>
3. <span data-ttu-id="5f7ba-165">目標端虛擬機器的磁碟會由 Azure Site Recovery 複製到容器做為種子 blob。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-165">The target side virtual machine's disk is copied by Azure Site Recovery into a container as a seed blob.</span></span>
4. <span data-ttu-id="5f7ba-166">然後將刪除目標端虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-166">The target side virtual machine is then deleted.</span></span>
5. <span data-ttu-id="5f7ba-167">種子 blob 將由目前來源端 (東亞) 虛擬機器用來複寫。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-167">The seed blob is used by the current source side (East Asia) virtual machine to replicate.</span></span> <span data-ttu-id="5f7ba-168">這可確保僅複寫差異部份。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-168">This ensures that only deltas are replicated.</span></span>
6. <span data-ttu-id="5f7ba-169">來源磁碟與種子 blob 之間的重大變更會同步處理。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-169">The major changes between the source disk and the seed blob are synchronized.</span></span> <span data-ttu-id="5f7ba-170">這需要一些時間才會完成。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-170">This can take some time to complete.</span></span>
7. <span data-ttu-id="5f7ba-171">重新保護工作完成之後，差異複寫會開始依據原則建立復原點。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-171">Once the reprotect job completes, the delta replication begins that creates a recovery point as per the policy.</span></span>

> [!NOTE]
> <span data-ttu-id="5f7ba-172">您無法在復原計劃層級進行保護。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-172">You cannot protect at a recovery plan level.</span></span> <span data-ttu-id="5f7ba-173">您只能在每個 VM 層級進行重新保護。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-173">You can only reprotect at a per VM level.</span></span>

<span data-ttu-id="5f7ba-174">重新保護成功之後，虛擬機器將進入受保護狀態。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-174">After the reprotect succeed, the virtual machine will enter a protected state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f7ba-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f7ba-175">Next steps</span></span>

<span data-ttu-id="5f7ba-176">在虛擬機器進入受保護狀態後，您就可以起始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-176">After the virtual machine has entered a protected state, you can initiate a failover.</span></span> <span data-ttu-id="5f7ba-177">容錯移轉將關閉東亞 Azure 區域中的虛擬機器，然後建立並啟動東南亞區域虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-177">The failover will shut down the virtual machine in East Asia Azure region and then create and boot the Southeast Asia region virtual machine.</span></span> <span data-ttu-id="5f7ba-178">因此，應用程式有一小段停機時間。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-178">Hence there is a small downtime for the application.</span></span> <span data-ttu-id="5f7ba-179">因此，請選擇應用程式允許停機時的容錯移轉時間。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-179">So, choose the time for failover when your application can tolerate a downtime.</span></span> <span data-ttu-id="5f7ba-180">建議您先測試虛擬機器的容錯移轉，確定運作正常，然後再起始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5f7ba-180">It is recommended that you first test failover the virtual machine to make sure it is coming up correctly, before initiating a failover.</span></span>

-   [<span data-ttu-id="5f7ba-181">起始虛擬機器測試容錯移轉的步驟</span><span class="sxs-lookup"><span data-stu-id="5f7ba-181">Steps to initiate test failover of the virtual machine</span></span>](site-recovery-test-failover-to-azure.md)

-   [<span data-ttu-id="5f7ba-182">起始虛擬機器容錯移轉的步驟</span><span class="sxs-lookup"><span data-stu-id="5f7ba-182">Steps to initiate failover of the virtual machine</span></span>](site-recovery-failover.md)
