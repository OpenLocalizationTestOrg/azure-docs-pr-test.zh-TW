---
title: "在您的 StorSimple 裝置上的更新 1.2 aaaInstall |Microsoft 文件"
description: "說明如何在您的 StorSimple 8000 系列裝置 tooinstall StorSimple 8000 系列 Update 1.2。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a><span data-ttu-id="2d1e8-103">在 StorSimple 8000 系列裝置上安裝 Update 1.2</span><span class="sxs-lookup"><span data-stu-id="2d1e8-103">Install Update 1.2 on your StorSimple 8000 series device</span></span>
## <a name="overview"></a><span data-ttu-id="2d1e8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2d1e8-104">Overview</span></span>
<span data-ttu-id="2d1e8-105">本教學課程說明如何 tooinstall 更新 1.2 執行軟體版本先前 tooUpdate 1 在 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-105">This tutorial explains how tooinstall Update 1.2 on a StorSimple device that is running a software version prior tooUpdate 1.</span></span> <span data-ttu-id="2d1e8-106">hello 教學課程也涵蓋 hello hello 更新以外的 hello StorSimple 裝置的 DATA 0 網路介面上設定閘道時所需的額外步驟。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-106">hello tutorial also covers hello additional steps required for hello update when a gateway is configured on a network interface other than DATA 0 of hello StorSimple device.</span></span>

<span data-ttu-id="2d1e8-107">Update 1.2 包括裝置軟體更新、LSI 驅動程式更新和磁碟韌體更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-107">Update 1.2 includes device software updates, LSI driver updates and disk firmware updates.</span></span> <span data-ttu-id="2d1e8-108">hello 軟體和 LSI 驅動程式更新非干擾性更新，所以可以套用透過 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-108">hello software and LSI driver updates are non-disruptive updates and can be applied via hello Azure classic portal.</span></span> <span data-ttu-id="2d1e8-109">hello 磁碟韌體更新更新具有干擾性，並只能透過 hello 裝置 hello Windows PowerShell 介面套用。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-109">hello disk firmware updates are disruptive updates and can only be applied via hello Windows PowerShell interface of hello device.</span></span>

<span data-ttu-id="2d1e8-110">根據正在執行的裝置版本，您可以判斷是否套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-110">Depending upon which version your device is running, you can determine if Update 1.2 will be applied.</span></span> <span data-ttu-id="2d1e8-111">您可以檢查您的裝置 hello 軟體版本，瀏覽 toohello**快速概覽**> 一節，您的裝置**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-111">You can check hello software version of your device by navigating toohello **quick glance** section of your device **Dashboard**.</span></span>

</br>

| <span data-ttu-id="2d1e8-112">如果執行的軟體版本...</span><span class="sxs-lookup"><span data-stu-id="2d1e8-112">If running software version …</span></span> | <span data-ttu-id="2d1e8-113">Hello 入口網站中會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="2d1e8-113">What happens in hello portal?</span></span> |
| --- | --- |
| <span data-ttu-id="2d1e8-114">Release - GA</span><span class="sxs-lookup"><span data-stu-id="2d1e8-114">Release - GA</span></span> |<span data-ttu-id="2d1e8-115">如果您正在執行 Release 版本 (GA)，請勿套用此更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-115">If you are running Release version (GA), do not apply this update.</span></span> <span data-ttu-id="2d1e8-116">請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooupdate 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-116">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate your device.</span></span> |
| <span data-ttu-id="2d1e8-117">Update 0.1</span><span class="sxs-lookup"><span data-stu-id="2d1e8-117">Update 0.1</span></span> |<span data-ttu-id="2d1e8-118">入口網站套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-118">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="2d1e8-119">Update 0.2</span><span class="sxs-lookup"><span data-stu-id="2d1e8-119">Update 0.2</span></span> |<span data-ttu-id="2d1e8-120">入口網站套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-120">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="2d1e8-121">Update 0.3</span><span class="sxs-lookup"><span data-stu-id="2d1e8-121">Update 0.3</span></span> |<span data-ttu-id="2d1e8-122">入口網站套用 Update 1.2。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-122">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="2d1e8-123">Update 1</span><span class="sxs-lookup"><span data-stu-id="2d1e8-123">Update 1</span></span> |<span data-ttu-id="2d1e8-124">此更新將無法使用。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-124">This update will not be available.</span></span> |
| <span data-ttu-id="2d1e8-125">Update 1.1</span><span class="sxs-lookup"><span data-stu-id="2d1e8-125">Update 1.1</span></span> |<span data-ttu-id="2d1e8-126">此更新將無法使用。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-126">This update will not be available.</span></span> |

</br>

> [!IMPORTANT]
> * <span data-ttu-id="2d1e8-127">您可能不會看到更新 1.2 立即，因為我們會執行 hello 更新分階段導入。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-127">You may not see Update 1.2 immediately because we do a phased rollout of hello updates.</span></span> <span data-ttu-id="2d1e8-128">請在數天內再次掃描更新，因為很快就會提供 Update。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-128">Scan for updates in a few days again as this Update will become available soon.</span></span>
> * <span data-ttu-id="2d1e8-129">此更新包括手動和自動預先檢查 toodetermine hello 裝置的健全狀況方面硬體狀態和網路連線的一組。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-129">This update includes a set of manual and automatic pre-checks toodetermine hello device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="2d1e8-130">只有當您從 Azure 傳統入口網站 hello 套用 hello 更新時，才執行這些前置檢查。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-130">These pre-checks are performed only if you apply hello updates from hello Azure classic portal.</span></span>
> * <span data-ttu-id="2d1e8-131">我們建議您安裝 hello 軟體，並透過的驅動程式更新 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-131">We recommend that you install hello software and driver updates via hello Azure classic portal.</span></span> <span data-ttu-id="2d1e8-132">如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-132">You should only go toohello Windows PowerShell interface of hello device (tooinstall updates) if hello pre-update gateway check fails in hello portal.</span></span> <span data-ttu-id="2d1e8-133">hello 更新可能需要 5-10 小時 tooinstall （包括 hello Windows 更新）。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-133">hello updates may take 5-10 hours tooinstall (including hello Windows Updates).</span></span> <span data-ttu-id="2d1e8-134">hello 維護模式更新必須透過 hello 裝置 hello Windows PowerShell 介面安裝。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-134">hello maintenance mode updates must be installed via hello Windows PowerShell interface of hello device.</span></span> <span data-ttu-id="2d1e8-135">由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-135">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a><span data-ttu-id="2d1e8-136">安裝更新 1.2 透過 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="2d1e8-136">Install Update 1.2 via hello Azure classic portal</span></span>
<span data-ttu-id="2d1e8-137">執行下列步驟 tooupdate hello 裝置太[更新 1.2](storsimple-update1-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-137">Perform hello following steps tooupdate your device too[Update 1.2](storsimple-update1-release-notes.md).</span></span> <span data-ttu-id="2d1e8-138">只有當您在裝置上的 DATA 0 網路介面上設定閘道器時才使用此程序。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-138">Use this procedure only if you have a gateway configured on DATA 0 network interface on your device.</span></span>

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. <span data-ttu-id="2d1e8-139">確認您的裝置是否正在執行 **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-139">Verify that your device is running **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**.</span></span> <span data-ttu-id="2d1e8-140">hello**上次更新日期**也應修改。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-140">hello **Last updated date** should also be modified.</span></span> <span data-ttu-id="2d1e8-141">您也會看到維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-141">You'll also see that Maintenance mode updates are available (this message might continue toobe displayed for up too24 hours after you install hello updates).</span></span>
   
   <span data-ttu-id="2d1e8-142">維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-142">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via hello Windows PowerShell interface of your device.</span></span>
   
   <span data-ttu-id="2d1e8-143">![維護頁面](./media/storsimple-install-update-1/InstallUpdate12_10M.png "維護頁面")</span><span class="sxs-lookup"><span data-stu-id="2d1e8-143">![Maintenance page](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Maintenance page")</span></span>
2. <span data-ttu-id="2d1e8-144">使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB3063416，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-144">Download hello maintenance mode updates by using hello steps listed in [toodownload hotfixes](#to-download-hotfixes) toosearch for and download KB3063416, which installs disk firmware updates (hello other updates should already be installed by now).</span></span>
3. <span data-ttu-id="2d1e8-145">中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-145">Follow hello steps listed in [Install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello maintenance mode updates.</span></span>
4. <span data-ttu-id="2d1e8-146">在 hello Azure 傳統入口網站中瀏覽 toohello**維護**頁面，然後在 hello hello 頁面底部，按一下**掃描更新**toocheck 的任何 Windows 更新，然後按一下**安裝更新**.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-146">In hello Azure classic portal, navigate toohello **Maintenance** page and at hello bottom of hello page, click **Scan Updates** toocheck for any Windows Updates and then click **Install Updates**.</span></span> <span data-ttu-id="2d1e8-147">您已完成在所有的 hello 成功安裝更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-147">You're finished after all of hello updates are successfully installed.</span></span>

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a><span data-ttu-id="2d1e8-148">在含有為非 DATA 0 網路介面設定之閘道器的裝置上安裝 Update 1.2</span><span class="sxs-lookup"><span data-stu-id="2d1e8-148">Install Update 1.2 on a device that has a gateway configured for a non-DATA 0 network interface</span></span>
<span data-ttu-id="2d1e8-149">只有當您檢查無法通過 hello 閘道嘗試 tooinstall hello 更新 hello Azure 傳統入口網站時，您應該使用此程序。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-149">You should use this procedure only if you fail hello gateway check when trying tooinstall hello updates through hello Azure classic portal.</span></span> <span data-ttu-id="2d1e8-150">hello 檢查失敗，因為您已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本先前 tooUpdate 1。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-150">hello check fails as you have a gateway assigned tooa non-DATA 0 network interface and your device is running a software version prior tooUpdate 1.</span></span> <span data-ttu-id="2d1e8-151">如果您的裝置上的非 DATA 0 網路介面沒有閘道，您可以更新您的裝置直接從 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-151">If your device does not have a gateway on a non-DATA 0 network interface, you can update your device directly from hello Azure classic portal.</span></span> <span data-ttu-id="2d1e8-152">請參閱[透過 hello Azure 傳統入口網站安裝更新 1.2](#install-update-1.2-via-the-azure-classic-portal)。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-152">See [Install update 1.2 via hello Azure classic portal](#install-update-1.2-via-the-azure-classic-portal).</span></span>

<span data-ttu-id="2d1e8-153">hello 軟體版本，可以使用這個方法來升級為更新 0.1，更新 0.2 和 Update 0.3。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-153">hello software versions that can be upgraded using this method are Update 0.1, Update 0.2, and Update 0.3.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="2d1e8-154">如果您的裝置正在執行版本 (GA) 版本，請連絡[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooassist hello 與更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-154">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist you with hello update.</span></span>
> * <span data-ttu-id="2d1e8-155">此程序需求 toobe 只能執行一次 tooapply 更新 1.2。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-155">This procedure needs toobe performed only once tooapply Update 1.2.</span></span> <span data-ttu-id="2d1e8-156">您可以使用 hello Azure 傳統入口網站 tooapply 後續更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-156">You can use hello Azure classic portal tooapply subsequent updates.</span></span>
> 
> 

<span data-ttu-id="2d1e8-157">如果您的裝置正在執行更新前 1 軟體，而且它有一組不同於 DATA 0 網路介面閘道，您可以在 hello 下列兩種方式套用更新 1.2:</span><span class="sxs-lookup"><span data-stu-id="2d1e8-157">If your device is running pre-Update 1 software and it has a gateway set for a network interface other than DATA 0, you can apply Update 1.2 in hello following two ways:</span></span>

* <span data-ttu-id="2d1e8-158">**選項 1**： 下載 hello 更新，並將它套用使用 hello `Start-HcsHotfix` cmdlet 從 hello 裝置 hello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-158">**Option 1**: Download hello update and apply it by using hello `Start-HcsHotfix` cmdlet from hello Windows PowerShell interface of hello device.</span></span> <span data-ttu-id="2d1e8-159">這是 hello 建議使用的方法。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-159">This is hello recommended method.</span></span> <span data-ttu-id="2d1e8-160">**如果您的裝置正在執行更新 1.0 或更新 1.1，請勿使用此方法 tooapply 更新 1.2。**</span><span class="sxs-lookup"><span data-stu-id="2d1e8-160">**Do not use this method tooapply Update 1.2 if your device is running Update 1.0 or Update 1.1.**</span></span>
* <span data-ttu-id="2d1e8-161">**選項 2**： 移除 hello 閘道組態和安裝 hello 直接從 hello Azure 傳統入口網站的更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-161">**Option 2**: Remove hello gateway configuration and install hello update directly from hello Azure classic portal.</span></span>

<span data-ttu-id="2d1e8-162">Hello 下列各節提供每個詳細的指示。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-162">Detailed instructions for each of these are provided in hello following sections.</span></span>

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a><span data-ttu-id="2d1e8-163">選項 1： 使用 Windows PowerShell for StorSimple tooapply 更新 1.2 以 hotfix 的形式</span><span class="sxs-lookup"><span data-stu-id="2d1e8-163">Option 1: Use Windows PowerShell for StorSimple tooapply Update 1.2 as a hotfix</span></span>
<span data-ttu-id="2d1e8-164">只有在您執行更新 0.1，0.2、 0.3，所以如果您的閘道簽入失敗嘗試 tooinstall 更新從 hello Azure 傳統入口網站時，您應該使用此程序。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-164">You should use this procedure only if you are running Update 0.1, 0.2, 0.3 and if your gateway check has failed when trying tooinstall updates from hello Azure classic portal.</span></span> <span data-ttu-id="2d1e8-165">如果您正在執行軟體版本 (GA)，請[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooupdate 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-165">If you are running Release (GA) software, please [Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate your device.</span></span>

<span data-ttu-id="2d1e8-166">tooinstall 更新 1.2 以 hotfix 的形式，您必須下載並安裝下列 hotfix hello:</span><span class="sxs-lookup"><span data-stu-id="2d1e8-166">tooinstall Update 1.2 as a hotfix, you must download and install hello following hotfixes:</span></span>

| <span data-ttu-id="2d1e8-167">順序</span><span class="sxs-lookup"><span data-stu-id="2d1e8-167">Order</span></span> | <span data-ttu-id="2d1e8-168">KB</span><span class="sxs-lookup"><span data-stu-id="2d1e8-168">KB</span></span> | <span data-ttu-id="2d1e8-169">說明</span><span class="sxs-lookup"><span data-stu-id="2d1e8-169">Description</span></span> | <span data-ttu-id="2d1e8-170">更新類型</span><span class="sxs-lookup"><span data-stu-id="2d1e8-170">Update type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2d1e8-171">1</span><span class="sxs-lookup"><span data-stu-id="2d1e8-171">1</span></span> |<span data-ttu-id="2d1e8-172">KB3063418</span><span class="sxs-lookup"><span data-stu-id="2d1e8-172">KB3063418</span></span> |<span data-ttu-id="2d1e8-173">軟體更新</span><span class="sxs-lookup"><span data-stu-id="2d1e8-173">Software update</span></span> |<span data-ttu-id="2d1e8-174">定期</span><span class="sxs-lookup"><span data-stu-id="2d1e8-174">Regular</span></span> |
| <span data-ttu-id="2d1e8-175">2</span><span class="sxs-lookup"><span data-stu-id="2d1e8-175">2</span></span> |<span data-ttu-id="2d1e8-176">KB3043005</span><span class="sxs-lookup"><span data-stu-id="2d1e8-176">KB3043005</span></span> |<span data-ttu-id="2d1e8-177">LSI SAS 控制器更新</span><span class="sxs-lookup"><span data-stu-id="2d1e8-177">LSI SAS controller update</span></span> |<span data-ttu-id="2d1e8-178">定期</span><span class="sxs-lookup"><span data-stu-id="2d1e8-178">Regular</span></span> |
| <span data-ttu-id="2d1e8-179">3</span><span class="sxs-lookup"><span data-stu-id="2d1e8-179">3</span></span> |<span data-ttu-id="2d1e8-180">KB3063416</span><span class="sxs-lookup"><span data-stu-id="2d1e8-180">KB3063416</span></span> |<span data-ttu-id="2d1e8-181">磁碟韌體</span><span class="sxs-lookup"><span data-stu-id="2d1e8-181">Disk firmware</span></span> |<span data-ttu-id="2d1e8-182">維護 </span><span class="sxs-lookup"><span data-stu-id="2d1e8-182">Maintenance</span></span> |

<span data-ttu-id="2d1e8-183">使用此程序 tooapply hello 前更新，請確定：</span><span class="sxs-lookup"><span data-stu-id="2d1e8-183">Before using this procedure tooapply hello update, make sure that:</span></span>

* <span data-ttu-id="2d1e8-184">這兩個裝置控制器都在線上。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-184">Both device controllers are online.</span></span>

<span data-ttu-id="2d1e8-185">執行下列步驟 tooapply 更新 1.2 hello。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-185">Perform hello following steps tooapply Update 1.2.</span></span> <span data-ttu-id="2d1e8-186">**hello 更新可能需要大約 2 小時 toocomplete （大約 30 分鐘的軟體，30 分鐘的時間驅動程式，如磁碟韌體 45 分鐘內）。**</span><span class="sxs-lookup"><span data-stu-id="2d1e8-186">**hello updates could take around 2 hours toocomplete (approximately 30 minutes for software, 30 minutes for driver, 45 minutes for disk firmware).**</span></span>

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a><span data-ttu-id="2d1e8-187">選項 2： 使用 Azure 傳統入口網站 tooapply 更新 1.2 hello 移除 hello 閘道設定之後</span><span class="sxs-lookup"><span data-stu-id="2d1e8-187">Option 2: Use hello Azure classic portal tooapply Update 1.2 after removing hello gateway configuration</span></span>
<span data-ttu-id="2d1e8-188">此程序適用於正在執行軟體版本先前 tooUpdate 1，且有不同於 DATA 0 網路介面上設定的閘道 tooStorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-188">This procedure applies only tooStorSimple devices that are running a software version prior tooUpdate 1 and have a gateway set on a network interface other than DATA 0.</span></span> <span data-ttu-id="2d1e8-189">您將需要 tooclear hello 閘道設定先前 tooapplying hello 更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-189">You will need tooclear hello gateway setting prior tooapplying hello update.</span></span>

<span data-ttu-id="2d1e8-190">hello 更新可能需要幾小時 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-190">hello update may take a few hours toocomplete.</span></span> <span data-ttu-id="2d1e8-191">如果您的主機位於不同子網路，移除 hello hello iSCSI 介面上的閘道設定可能會導致停機時間。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-191">If your hosts are in different subnets, removing hello gateway configuration on hello iSCSI interfaces could result in downtime.</span></span> <span data-ttu-id="2d1e8-192">我們建議您在 iSCSI 流量 tooreduce hello 停機時間的設定資料 0。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-192">We recommend that you configure DATA 0 for iSCSI traffic tooreduce hello downtime.</span></span>

<span data-ttu-id="2d1e8-193">執行下列步驟 toodisable hello 與 hello 閘道的網路介面的 hello，然後套用 hello 更新。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-193">Perform hello following steps toodisable hello network interface with hello gateway and then apply hello update.</span></span>

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="2d1e8-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d1e8-194">Next steps</span></span>
<span data-ttu-id="2d1e8-195">深入了解 hello[更新 1.2 版本](storsimple-update1-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1e8-195">Learn more about hello [Update 1.2 release](storsimple-update1-release-notes.md).</span></span>

