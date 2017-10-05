---
title: "StorSimple Virtual Array 的災害復原和裝置容錯移轉 | Microsoft Docs"
description: "深入了解如何容錯移轉 StorSimple Virtual Array。"
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
ms.openlocfilehash: 12079f8dbc409afe5acc274fa08bda878c90b76e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a><span data-ttu-id="c889a-103">透過 Azure 入口網站進行 StorSimple Virtual Array 的災害復原和裝置容錯移轉</span><span class="sxs-lookup"><span data-stu-id="c889a-103">Disaster recovery and device failover for your StorSimple Virtual Array via Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="c889a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c889a-104">Overview</span></span>
<span data-ttu-id="c889a-105">本文說明 Microsoft Azure StorSimple Virtual Array 的災害復原，包括容錯移轉至另一個虛擬陣列的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="c889a-105">This article describes the disaster recovery for your Microsoft Azure StorSimple Virtual Array including the detailed steps to fail over to another virtual array.</span></span> <span data-ttu-id="c889a-106">容錯移轉可讓您將資料從資料中心的「來源」裝置移至「目標」裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-106">A failover allows you to move your data from a *source* device in the datacenter to a *target* device.</span></span> <span data-ttu-id="c889a-107">目標裝置可能位於相同或不同的地理位置。</span><span class="sxs-lookup"><span data-stu-id="c889a-107">The target device may be located in the same or a different geographical location.</span></span> <span data-ttu-id="c889a-108">裝置容錯移轉適用於整個裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-108">The device failover is for the entire device.</span></span> <span data-ttu-id="c889a-109">在容錯移轉期間，來源裝置的雲端資料會將擁有權變更為目標裝置雲端資料。</span><span class="sxs-lookup"><span data-stu-id="c889a-109">During failover, the cloud data for the source device changes ownership to that of the target device.</span></span>

<span data-ttu-id="c889a-110">本文僅適用於 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="c889a-110">This article is applicable to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="c889a-111">若要容錯移轉 8000 系列裝置，請參閱 [StorSimple 裝置的裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="c889a-111">To fail over an 8000 series device, go to [Device failover and disaster recovery of your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>

## <a name="what-is-disaster-recovery-and-device-failover"></a><span data-ttu-id="c889a-112">什麼是災害復原和裝置容錯移轉？</span><span class="sxs-lookup"><span data-stu-id="c889a-112">What is disaster recovery and device failover?</span></span>

<span data-ttu-id="c889a-113">在災害復原 (DR) 案例中，主要裝置會停止運作。</span><span class="sxs-lookup"><span data-stu-id="c889a-113">In a disaster recovery (DR) scenario, the primary device stops functioning.</span></span> <span data-ttu-id="c889a-114">在此情況下，您可以將與故障裝置相關聯的雲端資料移至另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-114">In this scenario, you can move the cloud data associated with the failed device to another device.</span></span> <span data-ttu-id="c889a-115">您可以使用主要裝置當做「來源」，並指定另一個裝置做為「目標」。</span><span class="sxs-lookup"><span data-stu-id="c889a-115">You can use the primary device as the *source* and specify another device as the *target*.</span></span> <span data-ttu-id="c889a-116">這個程序就稱為「容錯移轉」 。</span><span class="sxs-lookup"><span data-stu-id="c889a-116">This process is referred to as the *failover*.</span></span> <span data-ttu-id="c889a-117">在容錯移轉期間，來源裝置的所有磁碟區或共用都會變更擁有權，並移轉到目標裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-117">During failover, all the volumes or the shares from the source device change ownership and are transferred to the target device.</span></span> <span data-ttu-id="c889a-118">不允許篩選資料。</span><span class="sxs-lookup"><span data-stu-id="c889a-118">No filtering of the data is allowed.</span></span>

<span data-ttu-id="c889a-119">使用熱度圖分層和追蹤，可將 DR 模型化為完整裝置還原。</span><span class="sxs-lookup"><span data-stu-id="c889a-119">DR is modeled as a full device restore using the heat map–based tiering and tracking.</span></span> <span data-ttu-id="c889a-120">熱度圖的定義方式，是根據讀取和寫入模式，將熱度值指派給資料。</span><span class="sxs-lookup"><span data-stu-id="c889a-120">A heat map is defined by assigning a heat value to the data based on read and write patterns.</span></span> <span data-ttu-id="c889a-121">這個熱度圖接著先將最低熱度資料區塊分層至雲端，同時將高熱 (最常用) 資料區塊保留在本機層中。</span><span class="sxs-lookup"><span data-stu-id="c889a-121">This heat map then tiers the lowest heat data chunks to the cloud first while keeping the high heat (most used) data chunks in the local tier.</span></span> <span data-ttu-id="c889a-122">在 DR 期間，StorSimple 會使用熱度圖來還原和解除凍結雲端中的資料。</span><span class="sxs-lookup"><span data-stu-id="c889a-122">During a DR, StorSimple uses the heat map to restore and rehydrate the data from the cloud.</span></span> <span data-ttu-id="c889a-123">裝置會擷取最新備份 (如內部決定) 中的所有磁碟區/共用，並從該備份執行還原。</span><span class="sxs-lookup"><span data-stu-id="c889a-123">The device fetches all the volumes/shares in the last recent backup (as determined internally) and performs a restore from that backup.</span></span> <span data-ttu-id="c889a-124">虛擬陣列會協調整個 DR 程序。</span><span class="sxs-lookup"><span data-stu-id="c889a-124">The virtual array orchestrates the entire DR process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c889a-125">裝置容錯移轉結束時會刪除來源裝置，因此不支援容錯回復。</span><span class="sxs-lookup"><span data-stu-id="c889a-125">The source device is deleted at the end of device failover and hence a failback is not supported.</span></span>
> 
> 

<span data-ttu-id="c889a-126">災害復原是透過裝置容錯移轉功能來策劃，而且是從 [裝置] 刀鋒視窗起始。</span><span class="sxs-lookup"><span data-stu-id="c889a-126">Disaster recovery is orchestrated via the device failover feature and is initiated from the **Devices** blade.</span></span> <span data-ttu-id="c889a-127">此刀鋒視窗會以表格列出所有連接至 StorSimple 裝置管理員服務的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-127">This blade tabulates all the StorSimple devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="c889a-128">您可以看到每個裝置的易記名稱、狀態、已佈建和最大容量、類型及模型。</span><span class="sxs-lookup"><span data-stu-id="c889a-128">For each device, you can see the friendly name, status, provisioned and maximum capacity, type, and model.</span></span>

## <a name="prerequisites-for-device-failover"></a><span data-ttu-id="c889a-129">裝置容錯移轉需求</span><span class="sxs-lookup"><span data-stu-id="c889a-129">Prerequisites for device failover</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c889a-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="c889a-130">Prerequisites</span></span>

<span data-ttu-id="c889a-131">對於裝置容錯移轉，請確定符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="c889a-131">For a device failover, ensure that the following prerequisites are satisfied:</span></span>

* <span data-ttu-id="c889a-132">來源裝置需要處於 [已停用]  狀態。</span><span class="sxs-lookup"><span data-stu-id="c889a-132">The source device needs to be in a **Deactivated** state.</span></span>
* <span data-ttu-id="c889a-133">在 Azure 入口網站中，目標裝置必須顯示為 [準備好進行設定] 。</span><span class="sxs-lookup"><span data-stu-id="c889a-133">The target device needs to show up as **Ready to set up** in the Azure portal.</span></span> <span data-ttu-id="c889a-134">佈建容量相同或更大的目標虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="c889a-134">Provision a target virtual array of the same or higher capacity.</span></span> <span data-ttu-id="c889a-135">使用本機 Web UI 來設定並成功註冊目標虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="c889a-135">Use the local web UI to configure and successfully register the target virtual array.</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="c889a-136">請不要嘗試透過服務來設定已註冊的虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-136">Do not attempt to configure the registered virtual device through the service.</span></span> <span data-ttu-id="c889a-137">您不應該透過服務執行任何裝置設定。</span><span class="sxs-lookup"><span data-stu-id="c889a-137">No device configuration should be performed through the service.</span></span>
  > 
  > 
* <span data-ttu-id="c889a-138">目標裝置不能與來源裝置同名。</span><span class="sxs-lookup"><span data-stu-id="c889a-138">The target device cannot have the same name as the source device.</span></span>
* <span data-ttu-id="c889a-139">來源和目標裝置的類型必須相同。</span><span class="sxs-lookup"><span data-stu-id="c889a-139">The source and target device have to be the same type.</span></span> <span data-ttu-id="c889a-140">您只能將設定為檔案伺服器的虛擬陣列容錯移轉至另一個檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="c889a-140">You can only fail over a virtual array configured as a file server to another file server.</span></span> <span data-ttu-id="c889a-141">這適用於 iSCSI 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c889a-141">The same is true for an iSCSI server.</span></span>
* <span data-ttu-id="c889a-142">針對檔案伺服器 DR，建議您將目標裝置加入與來源相同的網域。</span><span class="sxs-lookup"><span data-stu-id="c889a-142">For a file server DR, we recommend that you join the target device to the same domain as the source.</span></span> <span data-ttu-id="c889a-143">此設定可確保自動解析共用權限。</span><span class="sxs-lookup"><span data-stu-id="c889a-143">This configuration ensures that the share permissions are automatically resolved.</span></span> <span data-ttu-id="c889a-144">只容錯移轉至相同網域中的目標裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-144">Only the failover to a target device in the same domain.</span></span>
* <span data-ttu-id="c889a-145">DR 的可用目標裝置是容量與來源裝置相同或更高的裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-145">The available target devices for DR are devices that have the same or larger capacity compared to the source device.</span></span> <span data-ttu-id="c889a-146">已連接至服務但不符合足夠空間條件的裝置無法做為目標裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-146">The devices that are connected to your service but do not meet the criteria of sufficient space are not available as target devices.</span></span>

### <a name="other-considerations"></a><span data-ttu-id="c889a-147">其他考量</span><span class="sxs-lookup"><span data-stu-id="c889a-147">Other considerations</span></span>

* <span data-ttu-id="c889a-148">規劃的容錯移轉</span><span class="sxs-lookup"><span data-stu-id="c889a-148">For a planned failover</span></span> 
  
  * <span data-ttu-id="c889a-149">建議您將來源裝置上的所有磁碟區或共用離線。</span><span class="sxs-lookup"><span data-stu-id="c889a-149">We recommend that you take all the volumes or shares on the source device offline.</span></span>
  * <span data-ttu-id="c889a-150">建議您先備份裝置，再繼續容錯移轉，以儘可能避免資料遺失。</span><span class="sxs-lookup"><span data-stu-id="c889a-150">We recommend that you take a backup of the device and then proceed with the failover to minimize data loss.</span></span> 
* <span data-ttu-id="c889a-151">如果是未規劃的容錯移轉，裝置會使用最新備份來還原資料。</span><span class="sxs-lookup"><span data-stu-id="c889a-151">For an unplanned failover, the device uses the most recent backup to restore the data.</span></span>

### <a name="device-failover-prechecks"></a><span data-ttu-id="c889a-152">裝置容錯移轉前置檢查</span><span class="sxs-lookup"><span data-stu-id="c889a-152">Device failover prechecks</span></span>

<span data-ttu-id="c889a-153">DR 開始之前，裝置會執行前置檢查。</span><span class="sxs-lookup"><span data-stu-id="c889a-153">Before the DR begins, the device performs prechecks.</span></span> <span data-ttu-id="c889a-154">這些檢查有助於確保 DR 開始時不會發生任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="c889a-154">These checks help ensure that no errors occur when DR commences.</span></span> <span data-ttu-id="c889a-155">前置檢查包括：</span><span class="sxs-lookup"><span data-stu-id="c889a-155">The prechecks include:</span></span>

* <span data-ttu-id="c889a-156">驗證儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c889a-156">Validating the storage account.</span></span>
* <span data-ttu-id="c889a-157">檢查 Azure 的雲端連線。</span><span class="sxs-lookup"><span data-stu-id="c889a-157">Checking the cloud connectivity to Azure.</span></span>
* <span data-ttu-id="c889a-158">檢查目標裝置上的可用空間。</span><span class="sxs-lookup"><span data-stu-id="c889a-158">Checking available space on the target device.</span></span>
* <span data-ttu-id="c889a-159">檢查 iSCSI 伺服器來源裝置磁碟區是否有</span><span class="sxs-lookup"><span data-stu-id="c889a-159">Checking if an iSCSI server source device volume has</span></span>
  
  * <span data-ttu-id="c889a-160">有效的 ACR 名稱。</span><span class="sxs-lookup"><span data-stu-id="c889a-160">valid ACR names.</span></span>
  * <span data-ttu-id="c889a-161">有效的 IQN (不超過 220 個字元)。</span><span class="sxs-lookup"><span data-stu-id="c889a-161">valid IQN (not exceeding 220 characters).</span></span>
  * <span data-ttu-id="c889a-162">有效的 CHAP 密碼 (長度為 12-16 個字元)。</span><span class="sxs-lookup"><span data-stu-id="c889a-162">valid CHAP passwords (12-16 characters long).</span></span>

<span data-ttu-id="c889a-163">如果上述任何前置檢查失敗，則無法繼續進行 DR。</span><span class="sxs-lookup"><span data-stu-id="c889a-163">If any of the preceding prechecks fail, you cannot proceed with the DR.</span></span> <span data-ttu-id="c889a-164">解決這些問題，然後重試 DR。</span><span class="sxs-lookup"><span data-stu-id="c889a-164">Resolve those issues and then retry DR.</span></span>

<span data-ttu-id="c889a-165">DR 順利完成之後，來源裝置上雲端資料的擁有權會移轉給目標裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-165">After the DR is successfully completed, the ownership of the cloud data on the source device is transferred to the target device.</span></span> <span data-ttu-id="c889a-166">來源裝置就無法再於入口網站中使用。</span><span class="sxs-lookup"><span data-stu-id="c889a-166">The source device is then no longer available in the portal.</span></span> <span data-ttu-id="c889a-167">會封鎖對來源裝置上所有磁碟區/共用的存取，而目標裝置會變成使用中。</span><span class="sxs-lookup"><span data-stu-id="c889a-167">Access to all the volumes/shares on the source device is blocked and the target device becomes active.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c889a-168">雖然裝置無法再使用，但是您在主機系統上佈建的虛擬機器仍然會耗用資源。</span><span class="sxs-lookup"><span data-stu-id="c889a-168">Though the device is no longer available, the virtual machine that you provisioned on the host system is still consuming resources.</span></span> <span data-ttu-id="c889a-169">DR 順利完成之後，您就可以從主機系統中刪除此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c889a-169">Once the DR is successfully complete, you can delete this virtual machine from your host system.</span></span>
> 
> 

## <a name="fail-over-to-a-virtual-array"></a><span data-ttu-id="c889a-170">容錯移轉至虛擬陣列</span><span class="sxs-lookup"><span data-stu-id="c889a-170">Fail over to a virtual array</span></span>

<span data-ttu-id="c889a-171">執行此程序之前，建議您先佈建、設定另一個 StorSimple Virtual Array 並向 StorSimple 裝置管理員服務註冊。</span><span class="sxs-lookup"><span data-stu-id="c889a-171">We recommend that you provision, configure, and register another StorSimple Virtual Array with your StorSimple Device Manager service before you run this procedure.</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="c889a-172">您無法從 StorSimple 8000 系列裝置容錯移轉至 1200 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-172">You cannot fail over from a StorSimple 8000 series device to a 1200 virtual device.</span></span>
> * <span data-ttu-id="c889a-173">您可以從一個通過美國聯邦資訊處理標準 (FIPS) 的虛擬裝置，容錯移轉至另一個通過 FIPS 的裝置，或容錯移轉至部署於政府入口網站中的非 FIPS 裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-173">You can fail over from a Federal Information Processing Standard (FIPS) enabled virtual device to another FIPS enabled device or to a non-FIPS device deployed in the Government portal.</span></span>


<span data-ttu-id="c889a-174">請執行下列步驟以將裝置還原至目標 StorSimple 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-174">Perform the following steps to restore the device to a target StorSimple virtual device.</span></span>

1. <span data-ttu-id="c889a-175">佈建及設定符合[裝置容錯移轉求](#prerequisites)的目標裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-175">Provision and configure a target device that meets the [prerequisites for device failover](#prerequisites).</span></span> <span data-ttu-id="c889a-176">透過本機 Web UI 完成裝置設定，並向 StorSimple 裝置管理員服務註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-176">Complete the device configuration via the local web UI and register it to your StorSimple Device Manager service.</span></span> <span data-ttu-id="c889a-177">如果是建立檔案伺服器，請移至[設定為檔案伺服器](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)的步驟 1。</span><span class="sxs-lookup"><span data-stu-id="c889a-177">If creating a file server, go to step 1 of [set up as file server](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span> <span data-ttu-id="c889a-178">如果是建立 iSCSI 伺服器，請移至[設定為 iSCSI 伺服器](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)的步驟 1。</span><span class="sxs-lookup"><span data-stu-id="c889a-178">If creating an iSCSI server, go to step 1 of [set up as iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span>

2. <span data-ttu-id="c889a-179">將主機上的磁碟區/共用離線。</span><span class="sxs-lookup"><span data-stu-id="c889a-179">Take volumes/shares offline on the host.</span></span> <span data-ttu-id="c889a-180">若要讓磁碟區/共用離線，請參閱依作業系統而定的主機指示。</span><span class="sxs-lookup"><span data-stu-id="c889a-180">To take the volumes/shares offline, refer to the operating system–specific instructions for the host.</span></span> <span data-ttu-id="c889a-181">如果尚未離線，您需要執行下列動作，讓裝置上的所有磁碟區/共用離線。</span><span class="sxs-lookup"><span data-stu-id="c889a-181">If not already offline, you need to take all the volumes/shares offline on the device by doing the following.</span></span>
   
    1. <span data-ttu-id="c889a-182">移至 [裝置] 刀鋒視窗，然後選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-182">Go to **Devices** blade and select your device.</span></span>
   
    2. <span data-ttu-id="c889a-183">移至 [設定] > [管理] > [共用] \(或 [設定] > [管理] > [磁碟區])。</span><span class="sxs-lookup"><span data-stu-id="c889a-183">Go to **Settings > Manage > Shares** (or **Settings > Manage > Volumes**).</span></span> 
   
    3. <span data-ttu-id="c889a-184">選取共用/磁碟區，按一下滑鼠右鍵並選取 [離線]。</span><span class="sxs-lookup"><span data-stu-id="c889a-184">Select a share/volume, right click and select **Take offline**.</span></span> 
   
    4. <span data-ttu-id="c889a-185">提示您確認時，請勾選 [我了解讓此共用離線的影響]。</span><span class="sxs-lookup"><span data-stu-id="c889a-185">When prompted for confirmation, check **I understand the impact of taking this share offline.**</span></span> 
   
    5. <span data-ttu-id="c889a-186">按一下 [離線]。</span><span class="sxs-lookup"><span data-stu-id="c889a-186">Click **Take offline**.</span></span>

3. <span data-ttu-id="c889a-187">在 StorSimple 裝置管理員服務中，移至 [管理] > [裝置]。</span><span class="sxs-lookup"><span data-stu-id="c889a-187">In your StorSimple Device Manager service, go to **Management > Devices**.</span></span> <span data-ttu-id="c889a-188">在 [裝置] 刀鋒視窗中，選取並按一下您的來源裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-188">In the **Devices** blade, select and click your source device.</span></span>

4. <span data-ttu-id="c889a-189">在 [裝置儀表板] 刀鋒視窗中，按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="c889a-189">In your **Device dashboard** blade, click **Deactivate**.</span></span>

5. <span data-ttu-id="c889a-190">在 [停用] 刀鋒視窗中，系統會提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="c889a-190">In the **Deactivate** blade, you are prompted for confirmation.</span></span> <span data-ttu-id="c889a-191">裝置停用是無法復原的「永久性」程序。</span><span class="sxs-lookup"><span data-stu-id="c889a-191">Device deactivation is a *permanent* process that cannot be undone.</span></span> <span data-ttu-id="c889a-192">系統也會提醒您讓主機上的共用/磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="c889a-192">You are also reminded to take your shares/volumes offline on the host.</span></span> <span data-ttu-id="c889a-193">輸入裝置名稱加以確認，然後按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="c889a-193">Type the device name to confirm and click **Deactivate**.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. <span data-ttu-id="c889a-194">開始停用。</span><span class="sxs-lookup"><span data-stu-id="c889a-194">The deactivation starts.</span></span> <span data-ttu-id="c889a-195">停用順利完成之後，您將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="c889a-195">You will receive a notification after the deactivation is successfully completed.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. <span data-ttu-id="c889a-196">在 [裝置] 頁面上，裝置狀態現在會變更為 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="c889a-196">On the Devices page, the device state will now change to **Deactivated**.</span></span>
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. <span data-ttu-id="c889a-197">在 [裝置] 刀鋒視窗上，選取並按一下已停用的裝置來進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c889a-197">In the **Devices** blade, select and click the deactivated source device for failover.</span></span> 
9. <span data-ttu-id="c889a-198">在 [裝置儀表板] 刀鋒視窗中，按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="c889a-198">In the **Device dashboard** blade, click **Fail over**.</span></span> 
10. <span data-ttu-id="c889a-199">在 [容錯移轉裝置] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="c889a-199">In the **Fail over device** blade, do the following:</span></span>
    
    1. <span data-ttu-id="c889a-200">[來源裝置] 欄位會自動填入。</span><span class="sxs-lookup"><span data-stu-id="c889a-200">The source device field is automatically populated.</span></span> <span data-ttu-id="c889a-201">請注意來源裝置的資料大小總計。</span><span class="sxs-lookup"><span data-stu-id="c889a-201">Note the total data size for the source device.</span></span> <span data-ttu-id="c889a-202">資料大小應該小於目標裝置上的可用容量。</span><span class="sxs-lookup"><span data-stu-id="c889a-202">The data size should be lesser than the available capacity on the target device.</span></span> <span data-ttu-id="c889a-203">檢閱與來源裝置相關聯的詳細資料，例如裝置名稱、容量總計，以及要容錯移轉的共用名稱。</span><span class="sxs-lookup"><span data-stu-id="c889a-203">Review the details associated with the source device such as device name, total capacity, and the names of the shares that are failed over.</span></span>

    2. <span data-ttu-id="c889a-204">從可用裝置的下拉式清單中，選擇 [目標裝置]。</span><span class="sxs-lookup"><span data-stu-id="c889a-204">From the dropdown list of available devices, choose a **Target device**.</span></span> <span data-ttu-id="c889a-205">下拉式清單中只會顯示具有足夠容量的裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-205">Only the devices that have sufficient capacity are displayed in the dropdown list.</span></span>

    3. <span data-ttu-id="c889a-206">勾選 [我了解這項作業會將資料容錯移轉至目標裝置]。</span><span class="sxs-lookup"><span data-stu-id="c889a-206">Check that **I understand that this operation will fail over data to the target device**.</span></span> 

    4. <span data-ttu-id="c889a-207">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="c889a-207">Click **Fail over**.</span></span>
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. <span data-ttu-id="c889a-208">容錯移轉工作起始，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="c889a-208">A failover job initiates and you receive a notification.</span></span> <span data-ttu-id="c889a-209">移至 [裝置] > [作業] 來監視容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c889a-209">Go to **Devices > Jobs** to monitor the failover.</span></span>
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. <span data-ttu-id="c889a-210">在 [作業] 刀鋒視窗中，您會看到針對來源裝置所建立的容錯移轉作業。</span><span class="sxs-lookup"><span data-stu-id="c889a-210">In the **Jobs** blade, you see a failover job created for the source device.</span></span> <span data-ttu-id="c889a-211">此工作會執行 DR 前置檢查。</span><span class="sxs-lookup"><span data-stu-id="c889a-211">This job performs the DR prechecks.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     <span data-ttu-id="c889a-212">DR 前置檢查成功之後，容錯移轉工作會產生來源裝置上每個共用/磁碟區的還原作業。</span><span class="sxs-lookup"><span data-stu-id="c889a-212">After the DR prechecks are successful, the failover job will spawn restore jobs for each share/volume that exists on your source device.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. <span data-ttu-id="c889a-213">完成容錯移轉後，移至 [裝置] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c889a-213">After the failover is complete, go to the **Devices** blade.</span></span>
    
    1. <span data-ttu-id="c889a-214">選取並按一下已做為容錯移轉程序目標裝置的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-214">Select and click the StorSimple device that was used as the target device for the failover process.</span></span>
    2. <span data-ttu-id="c889a-215">移至 [設定] > [管理] > [共用] \(如果是 iSCSI 伺服器，則移至 [磁碟區])。</span><span class="sxs-lookup"><span data-stu-id="c889a-215">Go to **Settings > Management > Shares** (or **Volumes** if iSCSI server).</span></span> <span data-ttu-id="c889a-216">在 [共用] 刀鋒視窗中，您可以檢視來自舊裝置的所有共用 (磁碟區)。</span><span class="sxs-lookup"><span data-stu-id="c889a-216">In the **Shares** blade, you can view all the shares (volumes) from the old device.</span></span>
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. <span data-ttu-id="c889a-217">您將需要[建立 DNS 別名](https://support.microsoft.com/kb/168322)，讓所有嘗試連接的應用程式都可以重新導向至新的裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-217">You will need to [create a DNS alias](https://support.microsoft.com/kb/168322) so that all the applications that are trying to connect can get redirected to the new device.</span></span>

## <a name="errors-during-dr"></a><span data-ttu-id="c889a-218">DR 期間發生錯誤</span><span class="sxs-lookup"><span data-stu-id="c889a-218">Errors during DR</span></span>

<span data-ttu-id="c889a-219">**DR 期間雲端連線能力中斷**</span><span class="sxs-lookup"><span data-stu-id="c889a-219">**Cloud connectivity outage during DR**</span></span>

<span data-ttu-id="c889a-220">從 DR 啟動之後到裝置還原完成之前，如果雲端連線中斷，DR 將會失敗。</span><span class="sxs-lookup"><span data-stu-id="c889a-220">If the cloud connectivity is disrupted after DR has started and before the device restore is complete, the DR will fail.</span></span> <span data-ttu-id="c889a-221">您會收到失敗通知。</span><span class="sxs-lookup"><span data-stu-id="c889a-221">You receive a failore notification.</span></span> <span data-ttu-id="c889a-222">DR 的目標裝置會標示為 [無法使用]。</span><span class="sxs-lookup"><span data-stu-id="c889a-222">The target device for DR is marked as *unusable.*</span></span> <span data-ttu-id="c889a-223">您無法將相同的目標裝置用於未來的 DR。</span><span class="sxs-lookup"><span data-stu-id="c889a-223">You cannot use the same target device for future DRs.</span></span>

<span data-ttu-id="c889a-224">**沒有相容的目標裝置**</span><span class="sxs-lookup"><span data-stu-id="c889a-224">**No compatible target devices**</span></span>

<span data-ttu-id="c889a-225">如果可用目標裝置的空間不足，您會看到錯誤，指出沒有相容的目標裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-225">If the available target devices do not have sufficient space, you see an error to the effect that there are no compatible target devices.</span></span>

<span data-ttu-id="c889a-226">**前置檢查失敗**</span><span class="sxs-lookup"><span data-stu-id="c889a-226">**Precheck failures**</span></span>

<span data-ttu-id="c889a-227">如果其中一項前置檢查未通過，您會看到前置檢查失敗。</span><span class="sxs-lookup"><span data-stu-id="c889a-227">If one of the prechecks is not satisfied, then you see precheck failures.</span></span>

## <a name="business-continuity-disaster-recovery-bcdr"></a><span data-ttu-id="c889a-228">業務持續性災害復原 (BCDR)</span><span class="sxs-lookup"><span data-stu-id="c889a-228">Business continuity disaster recovery (BCDR)</span></span>

<span data-ttu-id="c889a-229">當整個 Azure 資料中心停止運作時，就構成業務持續性災害復原 (BCDR) 狀況。</span><span class="sxs-lookup"><span data-stu-id="c889a-229">A business continuity disaster recovery (BCDR) scenario occurs when the entire Azure datacenter stops functioning.</span></span> <span data-ttu-id="c889a-230">這會影響您的 StorSimple 裝置管理員服務和相關聯的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-230">This can affect your StorSimple Device Manager service and the associated StorSimple devices.</span></span>

<span data-ttu-id="c889a-231">如果 StorSimple 裝置在發生災害的前一刻才剛註冊，則可能需要刪除這些 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-231">If there are StorSimple devices that were registered just before a disaster occurred, then these StorSimple devices may need to be deleted.</span></span> <span data-ttu-id="c889a-232">災害之後，您可以重建並設定這些裝置。</span><span class="sxs-lookup"><span data-stu-id="c889a-232">After the disaster, you can recreate and configure those devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c889a-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c889a-233">Next steps</span></span>

<span data-ttu-id="c889a-234">深入了解如何 [使用本機 Web UI 管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="c889a-234">Learn more about how to [administer your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span></span>

