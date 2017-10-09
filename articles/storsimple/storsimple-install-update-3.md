---
title: "在您的 StorSimple 裝置上的 Update 3 aaaInstall |Microsoft 文件"
description: "說明如何在您的 StorSimple 8000 系列裝置 tooinstall StorSimple 8000 系列 Update 3。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a><span data-ttu-id="d6e73-103">在 StorSimple 8000 系列裝置上安裝 Update 3</span><span class="sxs-lookup"><span data-stu-id="d6e73-103">Install Update 3 on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="d6e73-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d6e73-104">Overview</span></span>

<span data-ttu-id="d6e73-105">本教學課程說明如何在執行較舊的軟體版本，透過 StorSimple 裝置上的 Update 3 tooinstall hello Azure 傳統入口網站，並使用 hello hotfix 方法。</span><span class="sxs-lookup"><span data-stu-id="d6e73-105">This tutorial explains how tooinstall Update 3 on a StorSimple device running an earlier software version via hello Azure classic portal and using hello hotfix method.</span></span> <span data-ttu-id="d6e73-106">不同於 hello StorSimple 裝置的 DATA 0 網路介面上已設定閘道和您嘗試更新前 1 軟體版本從 tooupdate 時使用 hello hotfix 方法。</span><span class="sxs-lookup"><span data-stu-id="d6e73-106">hello hotfix method is used when a gateway is configured on a network interface other than DATA 0 of hello StorSimple device and you are trying tooupdate from a pre-Update 1 software version.</span></span>

<span data-ttu-id="d6e73-107">Update 3 包含裝置軟體、LSI 驅動程式和韌體以及 Storport 和 Spaceport 的更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-107">Update 3 includes device software, LSI driver and firmware, Storport and Spaceport updates.</span></span> <span data-ttu-id="d6e73-108">如果從 Update 2 或更早的版本更新，也會是必要的 tooapply iSCSI、 WMI、 並在某些情況下，磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-108">If updating from Update 2 or an earlier version, you will also be required tooapply iSCSI, WMI, and in certain cases, disk firmware updates.</span></span> <span data-ttu-id="d6e73-109">hello 裝置軟體、 WMI、 iSCSI、 LSI 驅動程式、 太空和 Storport 修正非干擾性更新作業，而且可以透過 hello Azure 傳統入口網站套用。</span><span class="sxs-lookup"><span data-stu-id="d6e73-109">hello device software, WMI, iSCSI, LSI driver, Spaceport, and Storport fixes are non-disruptive updates and can be applied via hello Azure classic portal.</span></span> <span data-ttu-id="d6e73-110">hello 磁碟韌體更新更新具有干擾性，並只能透過 hello 裝置 hello Windows PowerShell 介面套用。</span><span class="sxs-lookup"><span data-stu-id="d6e73-110">hello disk firmware updates are disruptive updates and can only be applied via hello Windows PowerShell interface of hello device.</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="d6e73-111">一組預先手動與自動檢查已完成先前 toohello 安裝 toodetermine hello 裝置健全狀況方面硬體狀態和網路連線。</span><span class="sxs-lookup"><span data-stu-id="d6e73-111">A set of manual and automatic pre-checks are done prior toohello install toodetermine hello device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="d6e73-112">只有當您從 Azure 傳統入口網站 hello 套用 hello 更新時，才執行這些前置檢查。</span><span class="sxs-lookup"><span data-stu-id="d6e73-112">These pre-checks are performed only if you apply hello updates from hello Azure classic portal.</span></span>
> * <span data-ttu-id="d6e73-113">我們建議您安裝 hello 軟體，並透過的驅動程式更新 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="d6e73-113">We recommend that you install hello software and driver updates via hello Azure  classic portal.</span></span> <span data-ttu-id="d6e73-114">如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="d6e73-114">You should only go toohello Windows PowerShell interface of hello device (tooinstall updates) if hello pre-update gateway check fails in hello portal.</span></span> <span data-ttu-id="d6e73-115">您正在從 hello 版本而定，hello 更新可能需要 1.5-2.5 小時 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="d6e73-115">Depending upon hello version you are updating from, hello updates may take 1.5-2.5 hours tooinstall.</span></span> <span data-ttu-id="d6e73-116">hello 維護模式更新必須透過 hello 裝置 hello Windows PowerShell 介面安裝。</span><span class="sxs-lookup"><span data-stu-id="d6e73-116">hello maintenance mode updates must be installed via hello Windows PowerShell interface of hello device.</span></span> <span data-ttu-id="d6e73-117">由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。</span><span class="sxs-lookup"><span data-stu-id="d6e73-117">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> * <span data-ttu-id="d6e73-118">如果執行 hello 選擇性 StorSimple Snapshot Manager，請確定您已升級 Snapshot Manager 版本 tooUpdate 2 先前 tooupdating hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="d6e73-118">If running hello optional StorSimple Snapshot Manager, ensure that you have upgraded your Snapshot Manager version tooUpdate 2 prior tooupdating hello device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a><span data-ttu-id="d6e73-119">透過 hello Azure 傳統入口網站安裝 Update 3</span><span class="sxs-lookup"><span data-stu-id="d6e73-119">Install Update 3 via hello Azure classic portal</span></span>
<span data-ttu-id="d6e73-120">執行下列步驟 tooupdate hello 裝置太[Update 3](storsimple-update3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="d6e73-120">Perform hello following steps tooupdate your device too[Update 3](storsimple-update3-release-notes.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d6e73-121">如果您要套用 Update 2 或更新版本 （包括 Update 2.1)，Microsoft 將會無法 toopull 其他診斷的資訊從裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="d6e73-121">If you are applying Update 2 or later (including Update 2.1), Microsoft will be able toopull additional diagnostic information from hello device.</span></span> <span data-ttu-id="d6e73-122">如此一來，當我們作業小組會識別發生問題的裝置，我們會更好的配備的 toocollect 資訊從裝置 hello 和診斷問題。</span><span class="sxs-lookup"><span data-stu-id="d6e73-122">As a result, when our operations team identifies devices that are having problems, we are better equipped toocollect information from hello device and diagnose issues.</span></span> <span data-ttu-id="d6e73-123">接受更新 2 或更新版本，您允許我們 tooprovide 主動式這項支援。</span><span class="sxs-lookup"><span data-stu-id="d6e73-123">By accepting Update 2 or later, you allow us tooprovide this proactive support.</span></span>
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

<span data-ttu-id="d6e73-124">確認您裝置執行的是 **StorSimple 8000 系列 Update 3 (6.3.9600.17759)**。</span><span class="sxs-lookup"><span data-stu-id="d6e73-124">Verify that your device is running **StorSimple 8000 Series Update 3 (6.3.9600.17759)**.</span></span> <span data-ttu-id="d6e73-125">hello**上次更新日期**也應修改。</span><span class="sxs-lookup"><span data-stu-id="d6e73-125">hello **Last updated date** should also be modified.</span></span> 
   - <span data-ttu-id="d6e73-126">如果您要更新的版本先前 tooUpdate 2，您也會看到 hello 維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。</span><span class="sxs-lookup"><span data-stu-id="d6e73-126">If you are updating from a version prior tooUpdate 2, you will also see that hello Maintenance mode updates are available (this message might continue toobe displayed for up too24 hours after you install hello updates).</span></span>
     <span data-ttu-id="d6e73-127">維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-127">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via hello Windows PowerShell interface of your device.</span></span> <span data-ttu-id="d6e73-128">在某些情況下當您執行更新 1.2、 磁碟韌體可能已經是最新狀態，在此情況下，您不需要 tooinstall 任何維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-128">In some cases when you are running Update 1.2, your disk firmware might already be up-to-date, in which case you don't need tooinstall any maintenance mode updates.</span></span>
   - <span data-ttu-id="d6e73-129">如果您是從 Update 2 或更新版本進行更新，您的裝置現在應該已是最新狀態。</span><span class="sxs-lookup"><span data-stu-id="d6e73-129">If you are updating from Update 2 or later, your device should now be up-to-date.</span></span> <span data-ttu-id="d6e73-130">您可以略過 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d6e73-130">You can skip hello next step.</span></span>

<span data-ttu-id="d6e73-131">使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB3121899，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。</span><span class="sxs-lookup"><span data-stu-id="d6e73-131">Download hello maintenance mode updates by using hello steps listed in [toodownload hotfixes](#to-download-hotfixes) toosearch for and download KB3121899, which installs disk firmware updates (hello other updates should already be installed by now).</span></span> <span data-ttu-id="d6e73-132">中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-132">Follow hello steps listed in [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello maintenance mode updates.</span></span> 

## <a name="install-update-3-as-a-hotfix"></a><span data-ttu-id="d6e73-133">以 Hotfix 方式安裝 Update 3</span><span class="sxs-lookup"><span data-stu-id="d6e73-133">Install Update 3 as a hotfix</span></span>
<span data-ttu-id="d6e73-134">如果您無法 hello 閘道核取時，嘗試透過 hello Azure 傳統入口網站的 tooinstall hello 更新，請使用此程序。</span><span class="sxs-lookup"><span data-stu-id="d6e73-134">Use this procedure if you fail hello gateway check when trying tooinstall hello updates through hello Azure classic portal.</span></span> <span data-ttu-id="d6e73-135">hello 檢查失敗，因為您已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本先前 tooUpdate 1。</span><span class="sxs-lookup"><span data-stu-id="d6e73-135">hello check fails as you have a gateway assigned tooa non-DATA 0 network interface and your device is running a software version prior tooUpdate 1.</span></span>

<span data-ttu-id="d6e73-136">可以使用 hello hotfix 方法來升級的 hello 軟體版本如下：</span><span class="sxs-lookup"><span data-stu-id="d6e73-136">hello software versions that can be upgraded using hello hotfix method are:</span></span>

* <span data-ttu-id="d6e73-137">Update 0.1、0.2、0.3</span><span class="sxs-lookup"><span data-stu-id="d6e73-137">Update 0.1, 0.2, 0.3</span></span>
* <span data-ttu-id="d6e73-138">Update 1、1.1、1.2</span><span class="sxs-lookup"><span data-stu-id="d6e73-138">Update 1, 1.1, 1.2</span></span>
* <span data-ttu-id="d6e73-139">Update 2、2.1、2.2</span><span class="sxs-lookup"><span data-stu-id="d6e73-139">Update 2, 2.1, 2.2</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="d6e73-140">如果您的裝置正在執行版本 (GA) 版本，請連絡[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooassist hello 與更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-140">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist you with hello update.</span></span>
> 
> 

<span data-ttu-id="d6e73-141">hello hotfix 方法牽涉到下列三個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d6e73-141">hello hotfix method involves hello following three steps:</span></span>

1. <span data-ttu-id="d6e73-142">從 Microsoft Update 類別目錄 hello 下載 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="d6e73-142">Download hello hotfixes from hello Microsoft Update Catalog.</span></span>
2. <span data-ttu-id="d6e73-143">安裝並確認 hello 一般模式 hotfix。</span><span class="sxs-lookup"><span data-stu-id="d6e73-143">Install and verify hello regular mode hotfixes.</span></span>
3. <span data-ttu-id="d6e73-144">安裝並確認 hello 維護模式 hotfix （只有在從更新前 2 的軟體更新）。</span><span class="sxs-lookup"><span data-stu-id="d6e73-144">Install and verify hello maintenance mode hotfix (only when updating from pre-Update 2 software).</span></span>

#### <a name="download-updates-for-your-device"></a><span data-ttu-id="d6e73-145">下載適用於您裝置的更新</span><span class="sxs-lookup"><span data-stu-id="d6e73-145">Download updates for your device</span></span>
<span data-ttu-id="d6e73-146">**如果您的裝置正在執行 Update 2.1 或 2.2**，您必須下載並安裝下列 hotfix hello 規定順序中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d6e73-146">**If your device is running Update 2.1 or 2.2**, you must download and install hello following hotfixes in hello prescribed order:</span></span>

| <span data-ttu-id="d6e73-147">順序</span><span class="sxs-lookup"><span data-stu-id="d6e73-147">Order</span></span> | <span data-ttu-id="d6e73-148">KB</span><span class="sxs-lookup"><span data-stu-id="d6e73-148">KB</span></span> | <span data-ttu-id="d6e73-149">說明</span><span class="sxs-lookup"><span data-stu-id="d6e73-149">Description</span></span> | <span data-ttu-id="d6e73-150">更新類型</span><span class="sxs-lookup"><span data-stu-id="d6e73-150">Update type</span></span> | <span data-ttu-id="d6e73-151">安裝時間</span><span class="sxs-lookup"><span data-stu-id="d6e73-151">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d6e73-152">1.</span><span class="sxs-lookup"><span data-stu-id="d6e73-152">1.</span></span> |<span data-ttu-id="d6e73-153">KB3186843</span><span class="sxs-lookup"><span data-stu-id="d6e73-153">KB3186843</span></span> |<span data-ttu-id="d6e73-154">軟體更新 &#42;</span><span class="sxs-lookup"><span data-stu-id="d6e73-154">Software update &#42;</span></span> |<span data-ttu-id="d6e73-155">定期 </span><span class="sxs-lookup"><span data-stu-id="d6e73-155">Regular</span></span> <br></br><span data-ttu-id="d6e73-156">非干擾性</span><span class="sxs-lookup"><span data-stu-id="d6e73-156">Non-disruptive</span></span> |<span data-ttu-id="d6e73-157">~ 45 分鐘</span><span class="sxs-lookup"><span data-stu-id="d6e73-157">~ 45 mins</span></span> |
| <span data-ttu-id="d6e73-158">2.</span><span class="sxs-lookup"><span data-stu-id="d6e73-158">2.</span></span> |<span data-ttu-id="d6e73-159">KB3186859</span><span class="sxs-lookup"><span data-stu-id="d6e73-159">KB3186859</span></span> |<span data-ttu-id="d6e73-160">LSI 驅動程式與韌體</span><span class="sxs-lookup"><span data-stu-id="d6e73-160">LSI driver and firmware</span></span> |<span data-ttu-id="d6e73-161">定期 </span><span class="sxs-lookup"><span data-stu-id="d6e73-161">Regular</span></span> <br></br><span data-ttu-id="d6e73-162">非干擾性</span><span class="sxs-lookup"><span data-stu-id="d6e73-162">Non-disruptive</span></span> |<span data-ttu-id="d6e73-163">~ 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="d6e73-163">~ 20 mins</span></span> |
| <span data-ttu-id="d6e73-164">3.</span><span class="sxs-lookup"><span data-stu-id="d6e73-164">3.</span></span> |<span data-ttu-id="d6e73-165">KB3121261</span><span class="sxs-lookup"><span data-stu-id="d6e73-165">KB3121261</span></span> |<span data-ttu-id="d6e73-166">Storport 和 Spaceport 修正程式 </span><span class="sxs-lookup"><span data-stu-id="d6e73-166">Storport and Spaceport fix</span></span> </br> <span data-ttu-id="d6e73-167">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d6e73-167">Windows Server 2012 R2</span></span> |<span data-ttu-id="d6e73-168">定期 </span><span class="sxs-lookup"><span data-stu-id="d6e73-168">Regular</span></span> <br></br><span data-ttu-id="d6e73-169">非干擾性</span><span class="sxs-lookup"><span data-stu-id="d6e73-169">Non-disruptive</span></span> |<span data-ttu-id="d6e73-170">~ 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="d6e73-170">~ 20 mins</span></span> |

<span data-ttu-id="d6e73-171">&#42; *Hello 軟體更新包含兩個二進位檔案的附註： 裝置軟體更新，前面加上`all-hcsmdssoftwareupdate`hello Ci 和 Mds 代理程式做為開頭`all-cismdsagentupdatebundle`。 hello Ci 和 Mds 之前必須先安裝 hello 裝置軟體更新代理程式。您也必須重新啟動 hello 作用中的控制器透過 hello `Restart-HcsController` cmdlet 套用 hello Ci 和 Mds 代理程式更新之後 （和套用 hello 剩餘更新之前）。*</span><span class="sxs-lookup"><span data-stu-id="d6e73-171">&#42;  *Note that hello software update consists of two binary files: device software update prefaced with `all-hcsmdssoftwareupdate` and hello Cis and Mds agent prefaced with `all-cismdsagentupdatebundle`. hello device software update must be installed before hello Cis and Mds agent. You must also restart hello active controller via hello `Restart-HcsController` cmdlet after you apply hello Cis and Mds agent update (and before applying hello remaining updates).*</span></span> 

<span data-ttu-id="d6e73-172">**如果您的裝置會執行 Update 0.1、 0.2、 0.3、 1.0、 1.1、 1.2 或 2.0**，您必須下載並安裝下列 hotfix 加法 toohello 軟體 LSI 驅動程式中的 hello 和韌體更新 hello 規定順序 (顯示的 hello 前面資料表)，動作：</span><span class="sxs-lookup"><span data-stu-id="d6e73-172">**If your device is running Update 0.1, 0.2, 0.3, 1.0, 1.1, 1.2, or 2.0**, you must download and install hello following hotfixes in addition toohello software, LSI driver and firmware updates (shown in hello preceding table), in hello prescribed order:</span></span>

| <span data-ttu-id="d6e73-173">順序</span><span class="sxs-lookup"><span data-stu-id="d6e73-173">Order</span></span> | <span data-ttu-id="d6e73-174">KB</span><span class="sxs-lookup"><span data-stu-id="d6e73-174">KB</span></span> | <span data-ttu-id="d6e73-175">說明</span><span class="sxs-lookup"><span data-stu-id="d6e73-175">Description</span></span> | <span data-ttu-id="d6e73-176">更新類型</span><span class="sxs-lookup"><span data-stu-id="d6e73-176">Update type</span></span> | <span data-ttu-id="d6e73-177">安裝時間</span><span class="sxs-lookup"><span data-stu-id="d6e73-177">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d6e73-178">4.</span><span class="sxs-lookup"><span data-stu-id="d6e73-178">4.</span></span> |<span data-ttu-id="d6e73-179">KB3146621</span><span class="sxs-lookup"><span data-stu-id="d6e73-179">KB3146621</span></span> |<span data-ttu-id="d6e73-180">iSCSI 封裝</span><span class="sxs-lookup"><span data-stu-id="d6e73-180">iSCSI package</span></span> |<span data-ttu-id="d6e73-181">定期 </span><span class="sxs-lookup"><span data-stu-id="d6e73-181">Regular</span></span> <br></br><span data-ttu-id="d6e73-182">非干擾性</span><span class="sxs-lookup"><span data-stu-id="d6e73-182">Non-disruptive</span></span> |<span data-ttu-id="d6e73-183">~ 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="d6e73-183">~ 20 mins</span></span> |
| <span data-ttu-id="d6e73-184">5.</span><span class="sxs-lookup"><span data-stu-id="d6e73-184">5.</span></span> |<span data-ttu-id="d6e73-185">KB3103616</span><span class="sxs-lookup"><span data-stu-id="d6e73-185">KB3103616</span></span> |<span data-ttu-id="d6e73-186">WMI 封裝</span><span class="sxs-lookup"><span data-stu-id="d6e73-186">WMI package</span></span> |<span data-ttu-id="d6e73-187">定期 </span><span class="sxs-lookup"><span data-stu-id="d6e73-187">Regular</span></span> <br></br><span data-ttu-id="d6e73-188">非干擾性</span><span class="sxs-lookup"><span data-stu-id="d6e73-188">Non-disruptive</span></span> |<span data-ttu-id="d6e73-189">~ 12 分鐘</span><span class="sxs-lookup"><span data-stu-id="d6e73-189">~ 12 mins</span></span> |

<br></br>

<span data-ttu-id="d6e73-190">**如果您的裝置正在執行版本 0.2、 0.3、 1.0、 1.1 和 1.2**，您可能也需要在頂端顯示 hello 先前資料表中的所有 hello 更新 tooinstall 磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-190">**If your device is running versions 0.2, 0.3, 1.0, 1.1, and 1.2**, you may also need tooinstall disk firmware updates on top of all hello updates shown in hello preceding tables.</span></span> <span data-ttu-id="d6e73-191">您可以確認您是否需要執行 hello 來 hello 磁碟韌體更新`Get-HcsFirmwareVersion`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d6e73-191">You can verify whether you need hello disk firmware updates by running hello `Get-HcsFirmwareVersion` cmdlet.</span></span> <span data-ttu-id="d6e73-192">如果您執行這些韌體版本： `XMGG`， `XGEG`， `KZ50`， `F6C2`， `VR08`，則您不需要 tooinstall 這些更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-192">If you are running these firmware versions: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, then you do not need tooinstall these updates.</span></span>

| <span data-ttu-id="d6e73-193">順序</span><span class="sxs-lookup"><span data-stu-id="d6e73-193">Order</span></span> | <span data-ttu-id="d6e73-194">KB</span><span class="sxs-lookup"><span data-stu-id="d6e73-194">KB</span></span> | <span data-ttu-id="d6e73-195">說明</span><span class="sxs-lookup"><span data-stu-id="d6e73-195">Description</span></span> | <span data-ttu-id="d6e73-196">更新類型</span><span class="sxs-lookup"><span data-stu-id="d6e73-196">Update type</span></span> | <span data-ttu-id="d6e73-197">安裝時間</span><span class="sxs-lookup"><span data-stu-id="d6e73-197">Install time</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d6e73-198">6.</span><span class="sxs-lookup"><span data-stu-id="d6e73-198">6.</span></span> |<span data-ttu-id="d6e73-199">KB3121899</span><span class="sxs-lookup"><span data-stu-id="d6e73-199">KB3121899</span></span> |<span data-ttu-id="d6e73-200">磁碟韌體</span><span class="sxs-lookup"><span data-stu-id="d6e73-200">Disk firmware</span></span> |<span data-ttu-id="d6e73-201">維護 </span><span class="sxs-lookup"><span data-stu-id="d6e73-201">Maintenance</span></span> <br></br><span data-ttu-id="d6e73-202">干擾性</span><span class="sxs-lookup"><span data-stu-id="d6e73-202">Disruptive</span></span> |<span data-ttu-id="d6e73-203">~ 30 分鐘</span><span class="sxs-lookup"><span data-stu-id="d6e73-203">~ 30 mins</span></span> |

<br></br>

> [!IMPORTANT]
> * <span data-ttu-id="d6e73-204">此程序需求 toobe 只能執行一次 tooapply Update 3。</span><span class="sxs-lookup"><span data-stu-id="d6e73-204">This procedure needs toobe performed only once tooapply Update 3.</span></span> <span data-ttu-id="d6e73-205">您可以使用 hello Azure 傳統入口網站 tooapply 後續更新。</span><span class="sxs-lookup"><span data-stu-id="d6e73-205">You can use hello Azure classic portal tooapply subsequent updates.</span></span>
> * <span data-ttu-id="d6e73-206">如果從更新 2.2 更新，hello 總計的安裝時間將會是關閉 too1.1 小時。</span><span class="sxs-lookup"><span data-stu-id="d6e73-206">If updating from Update 2.2, hello total install time is close too1.1 hours.</span></span>
> * <span data-ttu-id="d6e73-207">使用此程序 tooapply hello 前更新，請確定兩個 hello 裝置控制器都在線上，而且所有 hello 硬體元件都均狀況良好。</span><span class="sxs-lookup"><span data-stu-id="d6e73-207">Before using this procedure tooapply hello update, make sure that both hello device controllers are online and all hello hardware components are healthy.</span></span>
> 
> 

<span data-ttu-id="d6e73-208">執行下列步驟 toodownload hello 和安裝 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="d6e73-208">Perform hello following steps toodownload and install hello hotfixes.</span></span>

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="d6e73-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6e73-209">Next steps</span></span>
<span data-ttu-id="d6e73-210">深入了解 hello [Update 3 版本](storsimple-update3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="d6e73-210">Learn more about hello [Update 3 release](storsimple-update3-release-notes.md).</span></span>

