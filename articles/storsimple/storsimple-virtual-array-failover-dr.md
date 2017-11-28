---
title: "aaaStorSimple 虛擬陣列災害復原和裝置容錯移轉 |Microsoft 文件"
description: "深入了解如何 toofailover StorSimple 虛擬陣列。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a><span data-ttu-id="ca2c1-103">透過 Azure 入口網站進行 StorSimple Virtual Array 的災害復原和裝置容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ca2c1-103">Disaster recovery and device failover for your StorSimple Virtual Array via Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="ca2c1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ca2c1-104">Overview</span></span>
<span data-ttu-id="ca2c1-105">本文說明 hello 嚴重損壞修復您的 Microsoft Azure StorSimple 虛擬陣列包括 hello 詳細步驟 toofail 透過 tooanother 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-105">This article describes hello disaster recovery for your Microsoft Azure StorSimple Virtual Array including hello detailed steps toofail over tooanother virtual array.</span></span> <span data-ttu-id="ca2c1-106">在容錯移轉可讓您 toomove 資料從*來源*裝置 hello datacenter tooa*目標*裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-106">A failover allows you toomove your data from a *source* device in hello datacenter tooa *target* device.</span></span> <span data-ttu-id="ca2c1-107">hello 目標裝置可能在相同或不同的地理位置位於 hello。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-107">hello target device may be located in hello same or a different geographical location.</span></span> <span data-ttu-id="ca2c1-108">hello 裝置容錯移轉是 hello 整個裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-108">hello device failover is for hello entire device.</span></span> <span data-ttu-id="ca2c1-109">容錯移轉期間，hello hello 來源裝置的雲端資料會變更擁有權 toothat 的 hello 目標裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-109">During failover, hello cloud data for hello source device changes ownership toothat of hello target device.</span></span>

<span data-ttu-id="ca2c1-110">本文是只適用 tooStorSimple 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-110">This article is applicable tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="ca2c1-111">8000 系列裝置，透過 toofail 移過[您的 StorSimple 裝置的裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-111">toofail over an 8000 series device, go too[Device failover and disaster recovery of your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>

## <a name="what-is-disaster-recovery-and-device-failover"></a><span data-ttu-id="ca2c1-112">什麼是災害復原和裝置容錯移轉？</span><span class="sxs-lookup"><span data-stu-id="ca2c1-112">What is disaster recovery and device failover?</span></span>

<span data-ttu-id="ca2c1-113">在災害復原 (DR) 案例中，hello 主要裝置會停止運作。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-113">In a disaster recovery (DR) scenario, hello primary device stops functioning.</span></span> <span data-ttu-id="ca2c1-114">在此案例中，您可以移動 hello 與 hello 失敗的裝置 tooanother 裝置相關聯的雲端資料。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-114">In this scenario, you can move hello cloud data associated with hello failed device tooanother device.</span></span> <span data-ttu-id="ca2c1-115">您可以使用 hello 主要裝置當做 hello*來源*並指定另一個裝置當做 hello*目標*。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-115">You can use hello primary device as hello *source* and specify another device as hello *target*.</span></span> <span data-ttu-id="ca2c1-116">此程序為參照的 tooas hello*容錯移轉*。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-116">This process is referred tooas hello *failover*.</span></span> <span data-ttu-id="ca2c1-117">容錯移轉期間，所有 hello 磁碟區，或從 hello 來源裝置 hello 共用變更擁有權，而且傳送的 toohello 目標裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-117">During failover, all hello volumes or hello shares from hello source device change ownership and are transferred toohello target device.</span></span> <span data-ttu-id="ca2c1-118">允許 hello 資料沒有篩選。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-118">No filtering of hello data is allowed.</span></span>

<span data-ttu-id="ca2c1-119">DR 會模型化為使用 hello 熱度圖型階層處理及追蹤完整的裝置還原。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-119">DR is modeled as a full device restore using hello heat map–based tiering and tracking.</span></span> <span data-ttu-id="ca2c1-120">熱門地圖是由指派熱度值 toohello 根據資料的讀取和寫入模式中定義。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-120">A heat map is defined by assigning a heat value toohello data based on read and write patterns.</span></span> <span data-ttu-id="ca2c1-121">此熱度對應則層 hello 最低熱資料區塊 （chunk） toohello 雲端第一次同時 hello 本機層中的 hello 高 （最常使用） 的熱資料區塊。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-121">This heat map then tiers hello lowest heat data chunks toohello cloud first while keeping hello high heat (most used) data chunks in hello local tier.</span></span> <span data-ttu-id="ca2c1-122">在 DR 期間，StorSimple 使用 hello 熱度圖 toorestore 和解除凍結 hello hello 雲端的資料。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-122">During a DR, StorSimple uses hello heat map toorestore and rehydrate hello data from hello cloud.</span></span> <span data-ttu-id="ca2c1-123">hello 裝置擷取所有 hello 磁碟區/共用 hello 最後一個新的備份中 （如同取決於在內部），並會從該備份執行還原。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-123">hello device fetches all hello volumes/shares in hello last recent backup (as determined internally) and performs a restore from that backup.</span></span> <span data-ttu-id="ca2c1-124">hello 虛擬陣列會協調 hello 整個 DR 程序。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-124">hello virtual array orchestrates hello entire DR process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca2c1-125">在裝置容錯移轉的 hello 結尾刪除 hello 來源裝置，因此不支援容錯回復。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-125">hello source device is deleted at hello end of device failover and hence a failback is not supported.</span></span>
> 
> 

<span data-ttu-id="ca2c1-126">嚴重損壞修復協調透過 hello 裝置容錯移轉功能，並起始從 hello**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-126">Disaster recovery is orchestrated via hello device failover feature and is initiated from hello **Devices** blade.</span></span> <span data-ttu-id="ca2c1-127">此刀鋒視窗會製為表格所有 hello StorSimple 裝置連線的 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-127">This blade tabulates all hello StorSimple devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ca2c1-128">對於每個裝置，您可以查看 hello 易記名稱、 狀態、 已佈建和最大容量、 類型和模型。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-128">For each device, you can see hello friendly name, status, provisioned and maximum capacity, type, and model.</span></span>

## <a name="prerequisites-for-device-failover"></a><span data-ttu-id="ca2c1-129">裝置容錯移轉需求</span><span class="sxs-lookup"><span data-stu-id="ca2c1-129">Prerequisites for device failover</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ca2c1-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="ca2c1-130">Prerequisites</span></span>

<span data-ttu-id="ca2c1-131">裝置容錯移轉，請確定符合下列必要條件，hello:</span><span class="sxs-lookup"><span data-stu-id="ca2c1-131">For a device failover, ensure that hello following prerequisites are satisfied:</span></span>

* <span data-ttu-id="ca2c1-132">hello 來源裝置必須在 toobe **Deactivated**狀態。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-132">hello source device needs toobe in a **Deactivated** state.</span></span>
* <span data-ttu-id="ca2c1-133">hello 目標裝置需要 tooshow 向上為**已 tooset 準備註冊**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-133">hello target device needs tooshow up as **Ready tooset up** in hello Azure portal.</span></span> <span data-ttu-id="ca2c1-134">佈建 hello 的目標虛擬陣列相同或更高的容量。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-134">Provision a target virtual array of hello same or higher capacity.</span></span> <span data-ttu-id="ca2c1-135">使用 hello 本機 web UI tooconfigure，成功註冊 hello 目標虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-135">Use hello local web UI tooconfigure and successfully register hello target virtual array.</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="ca2c1-136">請勿嘗試 tooconfigure hello 註冊虛擬裝置透過 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-136">Do not attempt tooconfigure hello registered virtual device through hello service.</span></span> <span data-ttu-id="ca2c1-137">任何裝置設定應該透過 hello 服務來不執行。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-137">No device configuration should be performed through hello service.</span></span>
  > 
  > 
* <span data-ttu-id="ca2c1-138">hello 目標裝置不能有名稱為 hello 來源裝置相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-138">hello target device cannot have hello same name as hello source device.</span></span>
* <span data-ttu-id="ca2c1-139">hello 來源和目標裝置沒有 toobe hello 相同的型別。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-139">hello source and target device have toobe hello same type.</span></span> <span data-ttu-id="ca2c1-140">您只可以容錯移轉設定為檔案伺服器 tooanother 檔案伺服器的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-140">You can only fail over a virtual array configured as a file server tooanother file server.</span></span> <span data-ttu-id="ca2c1-141">hello 也適用於 iSCSI 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-141">hello same is true for an iSCSI server.</span></span>
* <span data-ttu-id="ca2c1-142">針對檔案伺服器 DR，我們建議您加入 hello 目標裝置 toohello hello 來源相同的網域。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-142">For a file server DR, we recommend that you join hello target device toohello same domain as hello source.</span></span> <span data-ttu-id="ca2c1-143">此組態可確保 hello 共用權限會自動進行解析。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-143">This configuration ensures that hello share permissions are automatically resolved.</span></span> <span data-ttu-id="ca2c1-144">只有 hello 容錯移轉 tooa 目標裝置 hello 中的相同的網域。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-144">Only hello failover tooa target device in hello same domain.</span></span>
* <span data-ttu-id="ca2c1-145">hello dr 的可用目標裝置所擁有的裝置 hello 相同或較大的容量相較 toohello 來源裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-145">hello available target devices for DR are devices that have hello same or larger capacity compared toohello source device.</span></span> <span data-ttu-id="ca2c1-146">hello 裝置所連接的 tooyour 服務但不是符合 hello 做為目標裝置沒有足夠空間標準。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-146">hello devices that are connected tooyour service but do not meet hello criteria of sufficient space are not available as target devices.</span></span>

### <a name="other-considerations"></a><span data-ttu-id="ca2c1-147">其他考量</span><span class="sxs-lookup"><span data-stu-id="ca2c1-147">Other considerations</span></span>

* <span data-ttu-id="ca2c1-148">規劃的容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ca2c1-148">For a planned failover</span></span> 
  
  * <span data-ttu-id="ca2c1-149">我們建議您先進行離線 hello 來源裝置上所有 hello 磁碟區或共用。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-149">We recommend that you take all hello volumes or shares on hello source device offline.</span></span>
  * <span data-ttu-id="ca2c1-150">我們建議您進行 hello 裝置的備份，並再繼續 hello 容錯移轉 toominimize 遺失資料。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-150">We recommend that you take a backup of hello device and then proceed with hello failover toominimize data loss.</span></span> 
* <span data-ttu-id="ca2c1-151">未規劃的容錯移轉，hello 裝置會使用 hello 最新備份 toorestore hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-151">For an unplanned failover, hello device uses hello most recent backup toorestore hello data.</span></span>

### <a name="device-failover-prechecks"></a><span data-ttu-id="ca2c1-152">裝置容錯移轉前置檢查</span><span class="sxs-lookup"><span data-stu-id="ca2c1-152">Device failover prechecks</span></span>

<span data-ttu-id="ca2c1-153">Hello DR 開始之前, hello 裝置執行 prechecks。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-153">Before hello DR begins, hello device performs prechecks.</span></span> <span data-ttu-id="ca2c1-154">這些檢查有助於確保 DR 開始時不會發生任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-154">These checks help ensure that no errors occur when DR commences.</span></span> <span data-ttu-id="ca2c1-155">hello prechecks 包括：</span><span class="sxs-lookup"><span data-stu-id="ca2c1-155">hello prechecks include:</span></span>

* <span data-ttu-id="ca2c1-156">正在驗證 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-156">Validating hello storage account.</span></span>
* <span data-ttu-id="ca2c1-157">正在檢查 hello 雲端連線 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-157">Checking hello cloud connectivity tooAzure.</span></span>
* <span data-ttu-id="ca2c1-158">正在檢查 hello 目標裝置上的可用空間。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-158">Checking available space on hello target device.</span></span>
* <span data-ttu-id="ca2c1-159">檢查 iSCSI 伺服器來源裝置磁碟區是否有</span><span class="sxs-lookup"><span data-stu-id="ca2c1-159">Checking if an iSCSI server source device volume has</span></span>
  
  * <span data-ttu-id="ca2c1-160">有效的 ACR 名稱。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-160">valid ACR names.</span></span>
  * <span data-ttu-id="ca2c1-161">有效的 IQN (不超過 220 個字元)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-161">valid IQN (not exceeding 220 characters).</span></span>
  * <span data-ttu-id="ca2c1-162">有效的 CHAP 密碼 (長度為 12-16 個字元)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-162">valid CHAP passwords (12-16 characters long).</span></span>

<span data-ttu-id="ca2c1-163">如果任何上述 prechecks hello 失敗，您無法進行 hello DR。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-163">If any of hello preceding prechecks fail, you cannot proceed with hello DR.</span></span> <span data-ttu-id="ca2c1-164">解決這些問題，然後重試 DR。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-164">Resolve those issues and then retry DR.</span></span>

<span data-ttu-id="ca2c1-165">Hello DR 順利完成之後，hello hello 雲端上的資料 hello 來源裝置的擁有權會是傳送的 toohello 目標裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-165">After hello DR is successfully completed, hello ownership of hello cloud data on hello source device is transferred toohello target device.</span></span> <span data-ttu-id="ca2c1-166">hello 來源裝置就不再 hello 入口網站中，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-166">hello source device is then no longer available in hello portal.</span></span> <span data-ttu-id="ca2c1-167">存取 tooall hello 磁碟區/共用 hello 來源裝置上遭到封鎖，hello 目標裝置會變成作用中。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-167">Access tooall hello volumes/shares on hello source device is blocked and hello target device becomes active.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca2c1-168">Hello 裝置已無法再使用，雖然 hello 您 hello 主機系統佈建的虛擬機器仍然會消耗資源。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-168">Though hello device is no longer available, hello virtual machine that you provisioned on hello host system is still consuming resources.</span></span> <span data-ttu-id="ca2c1-169">Hello DR 順利完成之後，您可以從主機系統來刪除此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-169">Once hello DR is successfully complete, you can delete this virtual machine from your host system.</span></span>
> 
> 

## <a name="fail-over-tooa-virtual-array"></a><span data-ttu-id="ca2c1-170">容錯移轉 tooa 虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="ca2c1-170">Fail over tooa virtual array</span></span>

<span data-ttu-id="ca2c1-171">執行此程序之前，建議您先佈建、設定另一個 StorSimple Virtual Array 並向 StorSimple 裝置管理員服務註冊。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-171">We recommend that you provision, configure, and register another StorSimple Virtual Array with your StorSimple Device Manager service before you run this procedure.</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="ca2c1-172">您無法從 StorSimple 8000 系列裝置 tooa 1200 虛擬裝置容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-172">You cannot fail over from a StorSimple 8000 series device tooa 1200 virtual device.</span></span>
> * <span data-ttu-id="ca2c1-173">您可以從美國聯邦資訊處理標準 (FIPS) 啟用虛擬裝置 tooanother FIPS 已啟用的裝置或 tooa 非 FIPS 裝置 hello 政府入口網站中部署容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-173">You can fail over from a Federal Information Processing Standard (FIPS) enabled virtual device tooanother FIPS enabled device or tooa non-FIPS device deployed in hello Government portal.</span></span>


<span data-ttu-id="ca2c1-174">執行下列步驟 toorestore hello tooa 目標 StorSimple 虛擬裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-174">Perform hello following steps toorestore hello device tooa target StorSimple virtual device.</span></span>

1. <span data-ttu-id="ca2c1-175">佈建及設定的目標裝置符合 hello[用於裝置容錯移轉的必要條件](#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-175">Provision and configure a target device that meets hello [prerequisites for device failover](#prerequisites).</span></span> <span data-ttu-id="ca2c1-176">完成透過 hello 本機 web UI 的 hello 裝置設定，然後登錄 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-176">Complete hello device configuration via hello local web UI and register it tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ca2c1-177">如果建立檔案伺服器，請移至的 toostep 1[設定為檔案伺服器](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-177">If creating a file server, go toostep 1 of [set up as file server](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span> <span data-ttu-id="ca2c1-178">如果建立 iSCSI 伺服器，請移至的 toostep 1[設定 iSCSI 伺服器為](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-178">If creating an iSCSI server, go toostep 1 of [set up as iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span>

2. <span data-ttu-id="ca2c1-179">Hello 主機上讓磁碟區/共用離線。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-179">Take volumes/shares offline on hello host.</span></span> <span data-ttu-id="ca2c1-180">tootake hello 磁碟區/共用離線，請參閱 「 hello 主機 toohello 作業系統特定指示。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-180">tootake hello volumes/shares offline, refer toohello operating system–specific instructions for hello host.</span></span> <span data-ttu-id="ca2c1-181">如果沒有已經離線，您需要 tootake 所有 hello 磁碟區/共用離線 hello 裝置上執行 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-181">If not already offline, you need tootake all hello volumes/shares offline on hello device by doing hello following.</span></span>
   
    1. <span data-ttu-id="ca2c1-182">跳過**裝置**刀鋒視窗中，選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-182">Go too**Devices** blade and select your device.</span></span>
   
    2. <span data-ttu-id="ca2c1-183">跳過**設定 > 管理 > 共用**(或**設定 > 管理 > 磁碟區**)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-183">Go too**Settings > Manage > Shares** (or **Settings > Manage > Volumes**).</span></span> 
   
    3. <span data-ttu-id="ca2c1-184">選取共用/磁碟區，按一下滑鼠右鍵並選取 [離線]。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-184">Select a share/volume, right click and select **Take offline**.</span></span> 
   
    4. <span data-ttu-id="ca2c1-185">當提示確認時，會檢查**我了解 hello 影響離線此共用。**</span><span class="sxs-lookup"><span data-stu-id="ca2c1-185">When prompted for confirmation, check **I understand hello impact of taking this share offline.**</span></span> 
   
    5. <span data-ttu-id="ca2c1-186">按一下 [離線]。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-186">Click **Take offline**.</span></span>

3. <span data-ttu-id="ca2c1-187">在您的 StorSimple 裝置管理員服務移過**管理 > 裝置**。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-187">In your StorSimple Device Manager service, go too**Management > Devices**.</span></span> <span data-ttu-id="ca2c1-188">在 hello**裝置**刀鋒視窗中，選取，然後按一下 來源裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-188">In hello **Devices** blade, select and click your source device.</span></span>

4. <span data-ttu-id="ca2c1-189">在 [裝置儀表板] 刀鋒視窗中，按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-189">In your **Device dashboard** blade, click **Deactivate**.</span></span>

5. <span data-ttu-id="ca2c1-190">在 hello**停用**刀鋒視窗中，系統會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-190">In hello **Deactivate** blade, you are prompted for confirmation.</span></span> <span data-ttu-id="ca2c1-191">裝置停用是無法復原的「永久性」程序。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-191">Device deactivation is a *permanent* process that cannot be undone.</span></span> <span data-ttu-id="ca2c1-192">您也會收到提醒 tootake 共用/磁碟區離線 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-192">You are also reminded tootake your shares/volumes offline on hello host.</span></span> <span data-ttu-id="ca2c1-193">輸入 hello 裝置名稱 tooconfirm，然後按一下**停用**。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-193">Type hello device name tooconfirm and click **Deactivate**.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. <span data-ttu-id="ca2c1-194">啟動 hello 停用。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-194">hello deactivation starts.</span></span> <span data-ttu-id="ca2c1-195">Hello 停用作業成功完成之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-195">You will receive a notification after hello deactivation is successfully completed.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. <span data-ttu-id="ca2c1-196">在 hello 裝置 頁面上，hello 裝置狀態將會立即變更太**Deactivated**。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-196">On hello Devices page, hello device state will now change too**Deactivated**.</span></span>
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. <span data-ttu-id="ca2c1-197">在 hello**裝置**刀鋒視窗中，選取並按一下 hello 停用的來源裝置容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-197">In hello **Devices** blade, select and click hello deactivated source device for failover.</span></span> 
9. <span data-ttu-id="ca2c1-198">在 hello**裝置儀表板**刀鋒視窗中，按一下 **容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-198">In hello **Device dashboard** blade, click **Fail over**.</span></span> 
10. <span data-ttu-id="ca2c1-199">在 hello**容錯移轉裝置**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="ca2c1-199">In hello **Fail over device** blade, do hello following:</span></span>
    
    1. <span data-ttu-id="ca2c1-200">hello 來源裝置 欄位會自動填入。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-200">hello source device field is automatically populated.</span></span> <span data-ttu-id="ca2c1-201">請注意 hello 來源裝置 hello 總資料大小。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-201">Note hello total data size for hello source device.</span></span> <span data-ttu-id="ca2c1-202">hello 資料大小應該小於 hello hello 目標裝置上的可用容量。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-202">hello data size should be lesser than hello available capacity on hello target device.</span></span> <span data-ttu-id="ca2c1-203">檢閱 hello hello 來源裝置，例如裝置名稱、 總容量和 hello 的容錯移轉的 hello 共用的名稱與相關聯的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-203">Review hello details associated with hello source device such as device name, total capacity, and hello names of hello shares that are failed over.</span></span>

    2. <span data-ttu-id="ca2c1-204">從可用裝置 hello 下拉式清單中，選擇 **目標裝置**。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-204">From hello dropdown list of available devices, choose a **Target device**.</span></span> <span data-ttu-id="ca2c1-205">僅限 hello 擁有足夠的容量的裝置會顯示在 [hello] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-205">Only hello devices that have sufficient capacity are displayed in hello dropdown list.</span></span>

    3. <span data-ttu-id="ca2c1-206">請檢查**我了解這項作業將會容錯移轉資料 toohello 目標裝置**。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-206">Check that **I understand that this operation will fail over data toohello target device**.</span></span> 

    4. <span data-ttu-id="ca2c1-207">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-207">Click **Fail over**.</span></span>
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. <span data-ttu-id="ca2c1-208">容錯移轉工作起始，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-208">A failover job initiates and you receive a notification.</span></span> <span data-ttu-id="ca2c1-209">跳過**裝置 > 工作**toomonitor hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-209">Go too**Devices > Jobs** toomonitor hello failover.</span></span>
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. <span data-ttu-id="ca2c1-210">在 hello**作業**刀鋒視窗中，您會看到針對 hello 來源裝置而建立的容錯移轉工作。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-210">In hello **Jobs** blade, you see a failover job created for hello source device.</span></span> <span data-ttu-id="ca2c1-211">此工作會執行 hello DR prechecks。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-211">This job performs hello DR prechecks.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     <span data-ttu-id="ca2c1-212">Hello DR prechecks 成功之後，hello 容錯移轉作業會產生每個共用/磁碟區的來源裝置上的還原作業。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-212">After hello DR prechecks are successful, hello failover job will spawn restore jobs for each share/volume that exists on your source device.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. <span data-ttu-id="ca2c1-213">Hello 容錯移轉完成，請移 toohello 之後**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-213">After hello failover is complete, go toohello **Devices** blade.</span></span>
    
    1. <span data-ttu-id="ca2c1-214">選取並按一下 hello StorSimple 裝置已用來作為 hello hello 容錯移轉程序的目標裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-214">Select and click hello StorSimple device that was used as hello target device for hello failover process.</span></span>
    2. <span data-ttu-id="ca2c1-215">跳過**設定 > 管理 > 共用**(或**磁碟區**如果 iSCSI 伺服器)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-215">Go too**Settings > Management > Shares** (or **Volumes** if iSCSI server).</span></span> <span data-ttu-id="ca2c1-216">在 hello**共用**刀鋒視窗中，您可以檢視 hello 舊裝置中所有的 hello 共用 （磁碟區）。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-216">In hello **Shares** blade, you can view all hello shares (volumes) from hello old device.</span></span>
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. <span data-ttu-id="ca2c1-217">您必須太[建立 DNS 別名](https://support.microsoft.com/kb/168322)tooconnect，讓所有 hello 嘗試的應用程式可以取得重新導向的 toohello 新裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-217">You will need too[create a DNS alias](https://support.microsoft.com/kb/168322) so that all hello applications that are trying tooconnect can get redirected toohello new device.</span></span>

## <a name="errors-during-dr"></a><span data-ttu-id="ca2c1-218">DR 期間發生錯誤</span><span class="sxs-lookup"><span data-stu-id="ca2c1-218">Errors during DR</span></span>

<span data-ttu-id="ca2c1-219">**DR 期間雲端連線能力中斷**</span><span class="sxs-lookup"><span data-stu-id="ca2c1-219">**Cloud connectivity outage during DR**</span></span>

<span data-ttu-id="ca2c1-220">DR hello 雲端連線中斷之後是否已啟動並 hello DR hello 裝置還原已經完成之前，將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-220">If hello cloud connectivity is disrupted after DR has started and before hello device restore is complete, hello DR will fail.</span></span> <span data-ttu-id="ca2c1-221">您會收到失敗通知。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-221">You receive a failore notification.</span></span> <span data-ttu-id="ca2c1-222">DR 的 hello 目標裝置已標示為*無法使用。*</span><span class="sxs-lookup"><span data-stu-id="ca2c1-222">hello target device for DR is marked as *unusable.*</span></span> <span data-ttu-id="ca2c1-223">您無法使用 hello 未來 DRs 的相同目標裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-223">You cannot use hello same target device for future DRs.</span></span>

<span data-ttu-id="ca2c1-224">**沒有相容的目標裝置**</span><span class="sxs-lookup"><span data-stu-id="ca2c1-224">**No compatible target devices**</span></span>

<span data-ttu-id="ca2c1-225">如果 hello 可用目標裝置沒有足夠的空間，您會看到錯誤 toohello 效果沒有相容的目標裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-225">If hello available target devices do not have sufficient space, you see an error toohello effect that there are no compatible target devices.</span></span>

<span data-ttu-id="ca2c1-226">**前置檢查失敗**</span><span class="sxs-lookup"><span data-stu-id="ca2c1-226">**Precheck failures**</span></span>

<span data-ttu-id="ca2c1-227">如果沒有符合的 hello prechecks 其中一個，您會看到 precheck 失敗。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-227">If one of hello prechecks is not satisfied, then you see precheck failures.</span></span>

## <a name="business-continuity-disaster-recovery-bcdr"></a><span data-ttu-id="ca2c1-228">業務持續性災害復原 (BCDR)</span><span class="sxs-lookup"><span data-stu-id="ca2c1-228">Business continuity disaster recovery (BCDR)</span></span>

<span data-ttu-id="ca2c1-229">Hello 整個 Azure 資料中心都停止運作時，就會發生商務持續性災害復原 (BCDR) 案例。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-229">A business continuity disaster recovery (BCDR) scenario occurs when hello entire Azure datacenter stops functioning.</span></span> <span data-ttu-id="ca2c1-230">這可能會影響您的 StorSimple 裝置管理員服務與 hello StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-230">This can affect your StorSimple Device Manager service and hello associated StorSimple devices.</span></span>

<span data-ttu-id="ca2c1-231">如果是在災害發生時之前, 已註冊的 StorSimple 裝置，這些 StorSimple 裝置可能需要刪除 toobe。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-231">If there are StorSimple devices that were registered just before a disaster occurred, then these StorSimple devices may need toobe deleted.</span></span> <span data-ttu-id="ca2c1-232">Hello 損毀之後, 您可以重新建立並設定這些裝置。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-232">After hello disaster, you can recreate and configure those devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca2c1-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca2c1-233">Next steps</span></span>

<span data-ttu-id="ca2c1-234">深入了解如何太[管理使用本機 web UI hello 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="ca2c1-234">Learn more about how too[administer your StorSimple Virtual Array using hello local web UI](storsimple-ova-web-ui-admin.md).</span></span>

