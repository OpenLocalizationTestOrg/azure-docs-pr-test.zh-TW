---
title: "透過 Azure 虛擬機器回復 tooprimary Azure 區域無法從 aaaHow tooReprotect |Microsoft 文件"
description: "容錯移轉之後的 Vm 從一個 Azure 區域 tooanother，您可以使用 Azure Site Recovery tooprotect hello 機器反方向。 深入了解如何 hello 步驟 toodo 的容錯移轉之前重新保護。"
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
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a><span data-ttu-id="ae980-104">從重新保護容錯移轉的 Azure 區域後 tooprimary 區域</span><span class="sxs-lookup"><span data-stu-id="ae980-104">Reprotect from failed over Azure region back tooprimary region</span></span>



>[!NOTE]
>
> <span data-ttu-id="ae980-105">Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="ae980-105">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>


## <a name="overview"></a><span data-ttu-id="ae980-106">概觀</span><span class="sxs-lookup"><span data-stu-id="ae980-106">Overview</span></span>
<span data-ttu-id="ae980-107">當您[容錯移轉](site-recovery-failover.md)hello 虛擬機器從一個 Azure 區域 tooanother hello 虛擬機器處於未受保護狀態。</span><span class="sxs-lookup"><span data-stu-id="ae980-107">When you [failover](site-recovery-failover.md) hello virtual machines from one Azure region tooanother, hello virtual machines are in an unprotected state.</span></span> <span data-ttu-id="ae980-108">如果您想要 toobring 送回 toohello 主要區域，您需要 toofirst 再次保護 hello 虛擬機器，然後容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ae980-108">If you want toobring them back toohello primary region, you need toofirst protect hello virtual machines and then failover again.</span></span> <span data-ttu-id="ae980-109">朝任一個方向進行容錯移轉沒有任何差異。</span><span class="sxs-lookup"><span data-stu-id="ae980-109">There is no difference between how you failover in one direction or other.</span></span> <span data-ttu-id="ae980-110">同樣地，張貼的 hello 虛擬機器啟用保護，沒有任何容錯移轉 hello 重新保護後或 post 容錯回復之間的差異。</span><span class="sxs-lookup"><span data-stu-id="ae980-110">Similarly, post enable protection of hello virtual machines, there is no difference between hello reprotect post failover, or post failback.</span></span>
<span data-ttu-id="ae980-111">重新保護，以及 tooavoid 混淆 tooexplain hello 工作流程，我們將使用 hello 主要站台的 hello 受保護的電腦為東亞地區和 hello 復原站台的 hello 機器為東南亞區域。</span><span class="sxs-lookup"><span data-stu-id="ae980-111">tooexplain hello workflows of reprotect, and tooavoid confusion, we will use hello primary site of hello protected machines as East Asia region, and hello recovery site of hello machines as South East Asia region.</span></span> <span data-ttu-id="ae980-112">容錯移轉期間，您將會容錯移轉 hello 虛擬機器 toohello 東南亞區域。</span><span class="sxs-lookup"><span data-stu-id="ae980-112">During failover, you will failover hello virtual machines toohello South East Asia region.</span></span> <span data-ttu-id="ae980-113">您的容錯回復之前，您會需要從東南亞後 tooEast 亞洲 tooreprotect hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ae980-113">Before you failback, you need tooreprotect hello virtual machines from South East Asia back tooEast Asia.</span></span> <span data-ttu-id="ae980-114">本文說明如何 hello 步驟 tooreprotect。</span><span class="sxs-lookup"><span data-stu-id="ae980-114">This article describes hello steps on how tooreprotect.</span></span>

> [!WARNING]
> <span data-ttu-id="ae980-115">如果您有[完成移轉](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)，移動的 hello 的虛擬機器 tooanother 資源群組，或已刪除 hello Azure 虛擬機器，您之後就無法容錯回復。</span><span class="sxs-lookup"><span data-stu-id="ae980-115">If you have [completed migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), moved hello virtual machine tooanother resource group, or deleted hello Azure virtual machine, you cannot failback after that.</span></span>

<span data-ttu-id="ae980-116">完成之後重新保護和 hello 受保護的虛擬機器要複寫，您可以起始 hello 虛擬機器 toobring 的容錯移轉後加以備份 tooEast 亞洲區域。</span><span class="sxs-lookup"><span data-stu-id="ae980-116">After reprotect finishes and hello protected virtual machines are replicating, you can initiate a failover on hello virtual machines toobring them back tooEast Asia region.</span></span>

<span data-ttu-id="ae980-117">將註解或問題張貼結尾 hello 這份文件或在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="ae980-117">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae980-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="ae980-118">Prerequisites</span></span>
1. <span data-ttu-id="ae980-119">hello 虛擬機器應該已認可。</span><span class="sxs-lookup"><span data-stu-id="ae980-119">hello virtual machines should have been committed.</span></span>
2. <span data-ttu-id="ae980-120">hello 目標站台-在此情況下 hello 東亞 Azure 區域應該可以使用而且應該能夠 tooaccess/建立該區域中的新資源。</span><span class="sxs-lookup"><span data-stu-id="ae980-120">hello target site - in this case hello East Asia Azure region should be available and should be able tooaccess/create new resources in that region.</span></span>

## <a name="steps-tooreprotect"></a><span data-ttu-id="ae980-121">步驟 tooreprotect</span><span class="sxs-lookup"><span data-stu-id="ae980-121">Steps tooreprotect</span></span>

<span data-ttu-id="ae980-122">下列是 hello 步驟 tooreprotect 虛擬機器使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="ae980-122">Following are hello steps tooreprotect a virtual machine using hello defaults.</span></span>

1. <span data-ttu-id="ae980-123">在**保存庫** > **複寫項目**，hello 已容錯移轉的虛擬機器上按一下滑鼠右鍵，然後選取**重新保護**。</span><span class="sxs-lookup"><span data-stu-id="ae980-123">In **Vault** > **Replicated items**, right-click hello virtual machine that's been failed over, and then select **Re-Protect**.</span></span> <span data-ttu-id="ae980-124">您也可以按一下電腦，並選取 hello**重新保護**hello 命令按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae980-124">You can also click hello machine and select **Re-Protect** from hello command buttons.</span></span>

![以滑鼠右鍵按一下 tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. <span data-ttu-id="ae980-126">在 hello 刀鋒視窗中，請注意的保護，該 hello 方向**東南亞 tooEast 亞洲**，已選取。</span><span class="sxs-lookup"><span data-stu-id="ae980-126">In hello blade, notice that hello direction of protection, **Southeast Asia tooEast asia**, is already selected.</span></span>

![重新保護刀鋒視窗](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. <span data-ttu-id="ae980-128">檢閱 hello**資源群組，網路、 儲存體和可用性集**資訊並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ae980-128">Review hello **Resource group, Network, Storage and Availability sets** information and click OK.</span></span> <span data-ttu-id="ae980-129">如果沒有任何標記 （新） 的資源，也會建立 hello 一部分重新保護。</span><span class="sxs-lookup"><span data-stu-id="ae980-129">If there are any resources marked (new), they will be created as part of hello reprotect.</span></span>

<span data-ttu-id="ae980-130">這將會觸發程序作業重新 hello 最新的資料，保護會先植入 hello 目標站台 (在此情況下 SEA) 的工作一旦完成，請將複寫您的容錯移轉之前的 hello 差異備份 tooSoutheast 亞洲。</span><span class="sxs-lookup"><span data-stu-id="ae980-130">This will trigger a job reprotect job that will first seed hello target site (SEA in this case) with hello latest data, and once that completes, will replicate hello deltas before you failover back tooSoutheast Asia.</span></span>

### <a name="reprotect-customization"></a><span data-ttu-id="ae980-131">重新保護自訂</span><span class="sxs-lookup"><span data-stu-id="ae980-131">Reprotect customization</span></span>
<span data-ttu-id="ae980-132">如果您想 toochoose hello 擷取儲存體帳戶或 hello 網路期間重新保護，因此使用 hello 自訂 hello 重新保護刀鋒視窗上提供選項，您可以執行。</span><span class="sxs-lookup"><span data-stu-id="ae980-132">If you want toochoose hello extract storage account or hello network during reprotect, you can do so using hello customize option provided on hello reprotect blade.</span></span>

![自訂選項](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

<span data-ttu-id="ae980-134">您可以自訂 hello 期間重新保護下列他目標虛擬機器的內容。</span><span class="sxs-lookup"><span data-stu-id="ae980-134">You can customize hello following properties of he target virtual machine during reprotect.</span></span>

![自訂刀鋒視窗](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|<span data-ttu-id="ae980-136">屬性</span><span class="sxs-lookup"><span data-stu-id="ae980-136">Property</span></span> |<span data-ttu-id="ae980-137">注意事項</span><span class="sxs-lookup"><span data-stu-id="ae980-137">Notes</span></span>  |
|---------|---------|
|<span data-ttu-id="ae980-138">目標資源群組</span><span class="sxs-lookup"><span data-stu-id="ae980-138">Target resource group</span></span>     | <span data-ttu-id="ae980-139">您可以選擇將在其中建立個虛擬機器的 toochange hello 目標資源群組。</span><span class="sxs-lookup"><span data-stu-id="ae980-139">You can choose toochange hello target resource group in which th virtual machine will be created.</span></span> <span data-ttu-id="ae980-140">Hello 在重新保護，將刪除 hello 目標虛擬機器，因此您可以選擇新的資源群組，您可以在其下建立 hello VM post 容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ae980-140">As hello part of reprotect, hello target virtual machine will be deleted, hence you can choose a new resource group under which you can create hello VM post failover</span></span>         |
|<span data-ttu-id="ae980-141">目標虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ae980-141">Target Virtual Network</span></span>     | <span data-ttu-id="ae980-142">Hello 重新保護時，就無法變更網路。</span><span class="sxs-lookup"><span data-stu-id="ae980-142">Network cannot be changed during hello reprotect.</span></span> <span data-ttu-id="ae980-143">toochange hello 網路封包，重做 hello 網路對應。</span><span class="sxs-lookup"><span data-stu-id="ae980-143">toochange hello network, redo hello network mapping.</span></span>         |
|<span data-ttu-id="ae980-144">目標儲存體</span><span class="sxs-lookup"><span data-stu-id="ae980-144">Target Storage</span></span>     | <span data-ttu-id="ae980-145">您可以變更 hello toowhich hello 虛擬機器將會容錯移轉後建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae980-145">You can change hello storage account toowhich hello virtual machine will be created post failover.</span></span>         |
|<span data-ttu-id="ae980-146">快取儲存體</span><span class="sxs-lookup"><span data-stu-id="ae980-146">Cache Storage</span></span>     | <span data-ttu-id="ae980-147">您可以指定將在複寫期間使用的快取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae980-147">You can specify a cache storage account which will be used during replication.</span></span> <span data-ttu-id="ae980-148">如果您進行 hello 預設值，新的快取儲存體帳戶將會建立，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="ae980-148">If you go with hello defaults, a new cache storage account will be created, if it does not already exist.</span></span>         |
|<span data-ttu-id="ae980-149">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="ae980-149">Availability Set</span></span>     |<span data-ttu-id="ae980-150">如果 hello 東亞中的虛擬機器的可用性設定組的一部分，您可以選擇在東南亞 hello 目標虛擬機器設定可用性。</span><span class="sxs-lookup"><span data-stu-id="ae980-150">If hello virtual machine in East Asia is part of an availability set, you can choose an availability set for hello target virtual machine in Southeast Asia.</span></span> <span data-ttu-id="ae980-151">預設值會尋找 hello 現有 SEA 可用性設定組，並再試一次 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="ae980-151">Defaults will find hello existing SEA availability set and try toouse it.</span></span> <span data-ttu-id="ae980-152">進行自訂時，您可以指定全新的 AV 設定組。</span><span class="sxs-lookup"><span data-stu-id="ae980-152">During customization, you can specify a completely new AV set.</span></span>         |


### <a name="what-happens-during-reprotect"></a><span data-ttu-id="ae980-153">重新保護期間會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="ae980-153">What happens during reprotect?</span></span>

<span data-ttu-id="ae980-154">就像 hello 之後第一次啟用保護時，以下是 hello artefacts，如果您使用 hello 預設值建立的。</span><span class="sxs-lookup"><span data-stu-id="ae980-154">Just like after hello first enable protection, following are hello artefacts that get created if you use hello defaults.</span></span>
1. <span data-ttu-id="ae980-155">快取儲存體帳戶取得 hello 東亞地區中建立。</span><span class="sxs-lookup"><span data-stu-id="ae980-155">A cache storage account gets created in hello East Asia region.</span></span>
2. <span data-ttu-id="ae980-156">如果 hello 目標儲存體帳戶 （hello 原始儲存體帳戶的 hello 東南亞 VM） 不存在，則會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="ae980-156">If hello target storage account (hello original storage account of hello Southeast Asia VM) does not exist, a new one is created.</span></span> <span data-ttu-id="ae980-157">hello 名稱是後置字元為"asr"hello 東亞虛擬機器的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae980-157">hello name is hello East Asia virtual machine's storage account suffixed with "asr".</span></span>
3. <span data-ttu-id="ae980-158">如果 hello 目標 AV 集不存在，而且 hello 預設值可讓您偵測它，則它會建立 hello 的一部分時，才需要的 toocreate 新 AV 設定，請重新保護工作。</span><span class="sxs-lookup"><span data-stu-id="ae980-158">If hello target AV set does not exist, and hello defaults detect that it needs toocreate a new AV set, then it will be created as part of hello reprotect job.</span></span> <span data-ttu-id="ae980-159">如果您已自訂 hello 重新保護，然後將會使用選取的 hello AV 集。</span><span class="sxs-lookup"><span data-stu-id="ae980-159">If you have customized hello reprotect, then hello selected AV set will be used.</span></span>
4.

<span data-ttu-id="ae980-160">hello 下面是 hello 觸發重新保護工作時，就可能發生的步驟清單。</span><span class="sxs-lookup"><span data-stu-id="ae980-160">hello following are hello list of steps that happen when you trigger a reprotect job.</span></span> <span data-ttu-id="ae980-161">這是在虛擬機器存在 hello 案例 hello 目標端。</span><span class="sxs-lookup"><span data-stu-id="ae980-161">This is in hello case hello target side virtual machine exists.</span></span>

1. <span data-ttu-id="ae980-162">hello 需要 artefacts 會建立為重新保護的一部分。</span><span class="sxs-lookup"><span data-stu-id="ae980-162">hello required artefacts are created as part of reprotect.</span></span> <span data-ttu-id="ae980-163">如果這些項目已存在，則會重複使用。</span><span class="sxs-lookup"><span data-stu-id="ae980-163">If they already exist, then they are reused.</span></span>
2. <span data-ttu-id="ae980-164">hello 目標端 （東南亞） 關閉虛擬機器是第一次，如果它正在執行。</span><span class="sxs-lookup"><span data-stu-id="ae980-164">hello target side (Southeast Asia) virtual machine is first turned off, if it is running.</span></span>
3. <span data-ttu-id="ae980-165">hello 目標端虛擬機器的磁碟會為種子 blob，Azure Site recovery 複製到容器。</span><span class="sxs-lookup"><span data-stu-id="ae980-165">hello target side virtual machine's disk is copied by Azure Site Recovery into a container as a seed blob.</span></span>
4. <span data-ttu-id="ae980-166">然後刪除 hello 目標端的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ae980-166">hello target side virtual machine is then deleted.</span></span>
5. <span data-ttu-id="ae980-167">hello 目前來源端 （東亞） 虛擬機器 tooreplicate 使用 hello 種子 blob。</span><span class="sxs-lookup"><span data-stu-id="ae980-167">hello seed blob is used by hello current source side (East Asia) virtual machine tooreplicate.</span></span> <span data-ttu-id="ae980-168">這可確保僅複寫差異部份。</span><span class="sxs-lookup"><span data-stu-id="ae980-168">This ensures that only deltas are replicated.</span></span>
6. <span data-ttu-id="ae980-169">hello hello 來源磁碟和 hello 種子 blob 之間的重大變更會同步處理。</span><span class="sxs-lookup"><span data-stu-id="ae980-169">hello major changes between hello source disk and hello seed blob are synchronized.</span></span> <span data-ttu-id="ae980-170">這可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="ae980-170">This can take some time toocomplete.</span></span>
7. <span data-ttu-id="ae980-171">Hello 重新保護工作完成，hello 差異複寫會開始建立 hello 原則根據復原點。</span><span class="sxs-lookup"><span data-stu-id="ae980-171">Once hello reprotect job completes, hello delta replication begins that creates a recovery point as per hello policy.</span></span>

> [!NOTE]
> <span data-ttu-id="ae980-172">您無法在復原計劃層級進行保護。</span><span class="sxs-lookup"><span data-stu-id="ae980-172">You cannot protect at a recovery plan level.</span></span> <span data-ttu-id="ae980-173">您只能在每個 VM 層級進行重新保護。</span><span class="sxs-lookup"><span data-stu-id="ae980-173">You can only reprotect at a per VM level.</span></span>

<span data-ttu-id="ae980-174">Hello 重新保護之後成功，hello 虛擬機器將會進入受保護的狀態。</span><span class="sxs-lookup"><span data-stu-id="ae980-174">After hello reprotect succeed, hello virtual machine will enter a protected state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae980-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae980-175">Next steps</span></span>

<span data-ttu-id="ae980-176">Hello 虛擬機器已進入受保護的狀態之後，您可以起始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ae980-176">After hello virtual machine has entered a protected state, you can initiate a failover.</span></span> <span data-ttu-id="ae980-177">hello 容錯移轉將 hello 東亞 Azure 區域中的虛擬機器關機，然後建立並開機 hello 東南亞區域虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ae980-177">hello failover will shut down hello virtual machine in East Asia Azure region and then create and boot hello Southeast Asia region virtual machine.</span></span> <span data-ttu-id="ae980-178">因此是短暫的停機時間 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae980-178">Hence there is a small downtime for hello application.</span></span> <span data-ttu-id="ae980-179">如果您的應用程式可以容許停機時間，因此，請選擇 hello 容錯移轉時間。</span><span class="sxs-lookup"><span data-stu-id="ae980-179">So, choose hello time for failover when your application can tolerate a downtime.</span></span> <span data-ttu-id="ae980-180">建議您先測試容錯移轉 hello 虛擬機器 toomake 確定它接下來是否正確，才能起始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ae980-180">It is recommended that you first test failover hello virtual machine toomake sure it is coming up correctly, before initiating a failover.</span></span>

-   [<span data-ttu-id="ae980-181">步驟 tooinitiate 測試 hello 虛擬機器容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ae980-181">Steps tooinitiate test failover of hello virtual machine</span></span>](site-recovery-test-failover-to-azure.md)

-   [<span data-ttu-id="ae980-182">步驟 tooinitiate hello 虛擬機器容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ae980-182">Steps tooinitiate failover of hello virtual machine</span></span>](site-recovery-failover.md)
