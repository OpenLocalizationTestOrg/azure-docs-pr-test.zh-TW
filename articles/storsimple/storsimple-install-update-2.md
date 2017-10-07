---
title: "在您的 StorSimple 裝置上的 Update 2 aaaInstall |Microsoft 文件"
description: "說明如何在您的 StorSimple 8000 系列裝置 tooinstall StorSimple 8000 系列 Update 2。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a><span data-ttu-id="7a102-103">在 StorSimple 裝置上安裝 Update 2</span><span class="sxs-lookup"><span data-stu-id="7a102-103">Install Update 2 on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="7a102-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7a102-104">Overview</span></span>
<span data-ttu-id="7a102-105">本教學課程說明如何 tooinstall 更新 2 透過 hello Azure 傳統入口網站中執行較早的版本的 StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="7a102-105">This tutorial explains how tooinstall Update 2 on a StorSimple device running an earlier software version via hello Azure classic portal.</span></span> <span data-ttu-id="7a102-106">hello 教學課程也涵蓋 hello 閘道設定成以外的 hello StorSimple 裝置的 DATA 0 網路介面上，且您嘗試更新前 1 軟體版本從 tooupdate hello 更新所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="7a102-106">hello tutorial also covers hello steps required for hello update when a gateway is configured on a network interface other than DATA 0 of hello StorSimple device and you are trying tooupdate from a pre-Update 1 software version.</span></span>

<span data-ttu-id="7a102-107">Update 2 包括裝置軟體更新、LSI 驅動程式更新和磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="7a102-107">Update 2 includes device software updates, LSI driver updates, and disk firmware updates.</span></span> <span data-ttu-id="7a102-108">hello 裝置軟體和 LSI 更新非干擾性更新，並透過 hello Azure 傳統入口網站，可以套用。</span><span class="sxs-lookup"><span data-stu-id="7a102-108">hello device software and LSI updates are non-disruptive updates and can be applied via hello Azure classic portal.</span></span> <span data-ttu-id="7a102-109">hello 磁碟韌體更新更新具有干擾性，並只能透過 hello 裝置 hello Windows PowerShell 介面套用。</span><span class="sxs-lookup"><span data-stu-id="7a102-109">hello disk firmware updates are disruptive updates and can only be applied via hello Windows PowerShell interface of hello device.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7a102-110">您可能不會看到更新 2 立即，因為我們會執行 hello 更新分階段導入。</span><span class="sxs-lookup"><span data-stu-id="7a102-110">You may not see Update 2 immediately because we do a phased rollout of hello updates.</span></span> <span data-ttu-id="7a102-111">請在數天內再次掃描更新，因為很快就會提供 Update。</span><span class="sxs-lookup"><span data-stu-id="7a102-111">Scan for updates in a few days again as this Update will become available soon.</span></span>
> * <span data-ttu-id="7a102-112">一組預先手動與自動檢查已完成先前 toohello 安裝 toodetermine hello 裝置健全狀況方面硬體狀態和網路連線。</span><span class="sxs-lookup"><span data-stu-id="7a102-112">A set of manual and automatic pre-checks are done prior toohello install toodetermine hello device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="7a102-113">只有當您從 Azure 傳統入口網站 hello 套用 hello 更新時，才執行這些前置檢查。</span><span class="sxs-lookup"><span data-stu-id="7a102-113">These pre-checks are performed only if you apply hello updates from hello Azure classic portal.</span></span>
> * <span data-ttu-id="7a102-114">我們建議您安裝 hello 軟體，並透過的驅動程式更新 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="7a102-114">We recommend that you install hello software and driver updates via hello Azure  classic portal.</span></span> <span data-ttu-id="7a102-115">如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="7a102-115">You should only go toohello Windows PowerShell interface of hello device (tooinstall updates) if hello pre-update gateway check fails in hello portal.</span></span> <span data-ttu-id="7a102-116">hello 更新可能需要 4-7 小時 tooinstall （包括 hello Windows 更新）。</span><span class="sxs-lookup"><span data-stu-id="7a102-116">hello updates may take 4-7 hours tooinstall (including hello Windows Updates).</span></span> <span data-ttu-id="7a102-117">hello 維護模式更新必須透過 hello 裝置 hello Windows PowerShell 介面安裝。</span><span class="sxs-lookup"><span data-stu-id="7a102-117">hello maintenance mode updates must be installed via hello Windows PowerShell interface of hello device.</span></span> <span data-ttu-id="7a102-118">由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。</span><span class="sxs-lookup"><span data-stu-id="7a102-118">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> * <span data-ttu-id="7a102-119">如果執行 hello 選擇性 StorSimple Snapshot Manager，請確定您已升級 Snapshot Manager 版本 tooUpdate 2 先前 tooupdating hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7a102-119">If running hello optional StorSimple Snapshot Manager, ensure that you have upgraded your Snapshot Manager version tooUpdate 2 prior tooupdating hello device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a><span data-ttu-id="7a102-120">透過 hello Azure 傳統入口網站安裝 Update 2</span><span class="sxs-lookup"><span data-stu-id="7a102-120">Install Update 2 via hello Azure classic portal</span></span>
<span data-ttu-id="7a102-121">執行下列步驟 tooupdate hello 裝置太[Update 2](storsimple-update2-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="7a102-121">Perform hello following steps tooupdate your device too[Update 2](storsimple-update2-release-notes.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7a102-122">Update 2 讓 Microsoft toopull 其他診斷資訊從裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="7a102-122">Update 2 enables Microsoft toopull additional diagnostic information from hello device.</span></span> <span data-ttu-id="7a102-123">如此一來，當我們作業小組會識別發生問題的裝置，我們會更好的配備的 toocollect 資訊從裝置 hello 和診斷問題。</span><span class="sxs-lookup"><span data-stu-id="7a102-123">As a result, when our operations team identifies devices that are having problems, we are better equipped toocollect information from hello device and diagnose issues.</span></span> <span data-ttu-id="7a102-124">接受 Update 2 中，您允許我們 tooprovide 主動式這項支援。</span><span class="sxs-lookup"><span data-stu-id="7a102-124">By accepting Update 2, you allow us tooprovide this proactive support.</span></span>
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. <span data-ttu-id="7a102-125">驗證您的裝置正在執行 **StorSimple 8000 系列 Update 2 (6.3.9600.17673)**。</span><span class="sxs-lookup"><span data-stu-id="7a102-125">Verify that your device is running **StorSimple 8000 Series Update 2 (6.3.9600.17673)**.</span></span> <span data-ttu-id="7a102-126">hello**上次更新日期**也應修改。</span><span class="sxs-lookup"><span data-stu-id="7a102-126">hello **Last updated date** should also be modified.</span></span> <span data-ttu-id="7a102-127">您也會看到維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。</span><span class="sxs-lookup"><span data-stu-id="7a102-127">You'll also see that Maintenance mode updates are available (this message might continue toobe displayed for up too24 hours after you install hello updates).</span></span>
   
   <span data-ttu-id="7a102-128">維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。</span><span class="sxs-lookup"><span data-stu-id="7a102-128">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via hello Windows PowerShell interface of your device.</span></span> <span data-ttu-id="7a102-129">在某些情況下當您執行更新 1.2、 磁碟韌體可能已經是最新狀態，在此情況下，您不需要 tooinstall 任何維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="7a102-129">In some cases when you are running Update 1.2, your disk firmware might already be up-to-date, in which case you don't need tooinstall any maintenance mode updates.</span></span>
2. <span data-ttu-id="7a102-130">使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB3121899，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。</span><span class="sxs-lookup"><span data-stu-id="7a102-130">Download hello maintenance mode updates by using hello steps listed in [toodownload hotfixes](#to-download-hotfixes) toosearch for and download KB3121899, which installs disk firmware updates (hello other updates should already be installed by now).</span></span>
3. <span data-ttu-id="7a102-131">中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="7a102-131">Follow hello steps listed in [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello maintenance mode updates.</span></span>

## <a name="install-update-2-as-a-hotfix"></a><span data-ttu-id="7a102-132">以 Hotfix 的方式安裝 Update 2</span><span class="sxs-lookup"><span data-stu-id="7a102-132">Install Update 2 as a hotfix</span></span>
<span data-ttu-id="7a102-133">如果您無法 hello 閘道核取時，嘗試透過 hello Azure 傳統入口網站的 tooinstall hello 更新，請使用此程序。</span><span class="sxs-lookup"><span data-stu-id="7a102-133">Use this procedure if you fail hello gateway check when trying tooinstall hello updates through hello Azure classic portal.</span></span> <span data-ttu-id="7a102-134">hello 檢查失敗，因為您已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本先前 tooUpdate 1。</span><span class="sxs-lookup"><span data-stu-id="7a102-134">hello check fails as you have a gateway assigned tooa non-DATA 0 network interface and your device is running a software version prior tooUpdate 1.</span></span>

<span data-ttu-id="7a102-135">hello 軟體版本，可以使用 hello hotfix 方法來升級為更新 0.1、 更新 0.2，和 Update 0.3、 更新 1、 更新 1.1 和更新 1.2。</span><span class="sxs-lookup"><span data-stu-id="7a102-135">hello software versions that can be upgraded using hello hotfix method are Update 0.1, Update 0.2, and Update 0.3, Update 1, Update 1.1, and Update 1.2.</span></span> <span data-ttu-id="7a102-136">hello hotfix 方法牽涉到下列三個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a102-136">hello hotfix method involves hello following three steps:</span></span>

* <span data-ttu-id="7a102-137">從 Microsoft Update 類別目錄 hello 下載 hello hotfix。</span><span class="sxs-lookup"><span data-stu-id="7a102-137">Download hello hotfixes from hello Microsoft Update Catalog.</span></span>
* <span data-ttu-id="7a102-138">安裝並確認 hello 一般模式 hotfix。</span><span class="sxs-lookup"><span data-stu-id="7a102-138">Install and verify hello regular mode hotfixes.</span></span>
* <span data-ttu-id="7a102-139">安裝並確認 hello 維護模式 hotfix。</span><span class="sxs-lookup"><span data-stu-id="7a102-139">Install and verify hello maintenance mode hotfix.</span></span>

<span data-ttu-id="7a102-140">tooinstall Update 2，以 hotfix 的形式，您必須下載並安裝下列 hotfix hello:</span><span class="sxs-lookup"><span data-stu-id="7a102-140">tooinstall Update 2 as a hotfix, you must download and install hello following hotfixes:</span></span>

| <span data-ttu-id="7a102-141">順序</span><span class="sxs-lookup"><span data-stu-id="7a102-141">Order</span></span> | <span data-ttu-id="7a102-142">KB</span><span class="sxs-lookup"><span data-stu-id="7a102-142">KB</span></span> | <span data-ttu-id="7a102-143">說明</span><span class="sxs-lookup"><span data-stu-id="7a102-143">Description</span></span> | <span data-ttu-id="7a102-144">更新類型</span><span class="sxs-lookup"><span data-stu-id="7a102-144">Update type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a102-145">1</span><span class="sxs-lookup"><span data-stu-id="7a102-145">1</span></span> |<span data-ttu-id="7a102-146">KB3121901</span><span class="sxs-lookup"><span data-stu-id="7a102-146">KB3121901</span></span> |<span data-ttu-id="7a102-147">軟體更新</span><span class="sxs-lookup"><span data-stu-id="7a102-147">Software update</span></span> |<span data-ttu-id="7a102-148">定期</span><span class="sxs-lookup"><span data-stu-id="7a102-148">Regular</span></span> |
| <span data-ttu-id="7a102-149">2</span><span class="sxs-lookup"><span data-stu-id="7a102-149">2</span></span> |<span data-ttu-id="7a102-150">KB3121900</span><span class="sxs-lookup"><span data-stu-id="7a102-150">KB3121900</span></span> |<span data-ttu-id="7a102-151">LSI 驅動程式</span><span class="sxs-lookup"><span data-stu-id="7a102-151">LSI driver</span></span> |<span data-ttu-id="7a102-152">定期</span><span class="sxs-lookup"><span data-stu-id="7a102-152">Regular</span></span> |
| <span data-ttu-id="7a102-153">3</span><span class="sxs-lookup"><span data-stu-id="7a102-153">3</span></span> |<span data-ttu-id="7a102-154">KB3080728</span><span class="sxs-lookup"><span data-stu-id="7a102-154">KB3080728</span></span> |<span data-ttu-id="7a102-155">Storport 修正程式 </span><span class="sxs-lookup"><span data-stu-id="7a102-155">Storport fix</span></span> </br> <span data-ttu-id="7a102-156">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7a102-156">Windows Server 2012 R2</span></span> |<span data-ttu-id="7a102-157">定期</span><span class="sxs-lookup"><span data-stu-id="7a102-157">Regular</span></span> |
| <span data-ttu-id="7a102-158">4</span><span class="sxs-lookup"><span data-stu-id="7a102-158">4</span></span> |<span data-ttu-id="7a102-159">KB3090322</span><span class="sxs-lookup"><span data-stu-id="7a102-159">KB3090322</span></span> |<span data-ttu-id="7a102-160">Spaceport 修正程式 </span><span class="sxs-lookup"><span data-stu-id="7a102-160">Spaceport fix</span></span> </br> <span data-ttu-id="7a102-161">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7a102-161">Windows Server 2012 R2</span></span> |<span data-ttu-id="7a102-162">定期</span><span class="sxs-lookup"><span data-stu-id="7a102-162">Regular</span></span> |
| <span data-ttu-id="7a102-163">5</span><span class="sxs-lookup"><span data-stu-id="7a102-163">5</span></span> |<span data-ttu-id="7a102-164">KB3121899</span><span class="sxs-lookup"><span data-stu-id="7a102-164">KB3121899</span></span> |<span data-ttu-id="7a102-165">磁碟韌體</span><span class="sxs-lookup"><span data-stu-id="7a102-165">Disk firmware</span></span> |<span data-ttu-id="7a102-166">維護 </span><span class="sxs-lookup"><span data-stu-id="7a102-166">Maintenance</span></span> |

> [!IMPORTANT]
> * <span data-ttu-id="7a102-167">如果您的裝置正在執行版本 (GA) 版本，請連絡[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooassist hello 與更新。</span><span class="sxs-lookup"><span data-stu-id="7a102-167">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist you with hello update.</span></span>
> * <span data-ttu-id="7a102-168">此程序需求 toobe 只能執行一次 tooapply Update 2。</span><span class="sxs-lookup"><span data-stu-id="7a102-168">This procedure needs toobe performed only once tooapply Update 2.</span></span> <span data-ttu-id="7a102-169">您可以使用 hello Azure 傳統入口網站 tooapply 後續更新。</span><span class="sxs-lookup"><span data-stu-id="7a102-169">You can use hello Azure classic portal tooapply subsequent updates.</span></span>
> * <span data-ttu-id="7a102-170">每個的 hotfix 安裝可能需要約 20 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7a102-170">Each hotfix installation can take about 20 minutes toocomplete.</span></span> <span data-ttu-id="7a102-171">總計的安裝時間是關閉 too2 小時。</span><span class="sxs-lookup"><span data-stu-id="7a102-171">Total install time is close too2 hours.</span></span>
> * <span data-ttu-id="7a102-172">使用此程序 tooapply hello 前更新，請確定兩個裝置控制器都在線上，而且所有 hello 硬體元件都均狀況良好。</span><span class="sxs-lookup"><span data-stu-id="7a102-172">Before using this procedure tooapply hello update, make sure that both device controllers are online and all hello hardware components are healthy.</span></span>
> 
> 

<span data-ttu-id="7a102-173">執行下列步驟 tooapply hello 這個更新以 hotfix 的形式。</span><span class="sxs-lookup"><span data-stu-id="7a102-173">Perform hello following steps tooapply this update as a hotfix.</span></span>

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="7a102-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a102-174">Next steps</span></span>
<span data-ttu-id="7a102-175">深入了解 hello [Update 2 版本](storsimple-update2-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="7a102-175">Learn more about hello [Update 2 release](storsimple-update2-release-notes.md).</span></span>

