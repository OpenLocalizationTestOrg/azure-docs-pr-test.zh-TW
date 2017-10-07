---
title: "aaaStorSimple 虛擬陣列 web UI 管理 |Microsoft 文件"
description: "描述如何 tooperform 基本裝置系統管理工作透過 hello StorSimple Virtual Array web UI。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="c6842-103">使用您的 StorSimple Virtual Array hello Web UI tooadminister</span><span class="sxs-lookup"><span data-stu-id="c6842-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![安裝程序流程](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="c6842-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c6842-105">Overview</span></span>
<span data-ttu-id="c6842-106">這篇文章中的 hello 教學課程適用於 toohello Microsoft Azure StorSimple Virtual Array （也稱為 hello StorSimple 內部部署虛擬裝置） 執行 2016 年 3 月公開上市 (GA) 版本。</span><span class="sxs-lookup"><span data-stu-id="c6842-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="c6842-107">本文說明某些 hello 複雜工作流程及管理工作可以在 hello StorSimple Virtual Array 執行。</span><span class="sxs-lookup"><span data-stu-id="c6842-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="c6842-108">您可以管理 hello StorSimple Virtual Array 使用 hello StorSimple Manager 服務 UI （參考的 tooas hello 入口網站 UI） 和 hello hello 裝置的本機 web UI。</span><span class="sxs-lookup"><span data-stu-id="c6842-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="c6842-109">本文著重在 hello 工作，您可以使用執行 hello web UI。</span><span class="sxs-lookup"><span data-stu-id="c6842-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="c6842-110">這篇文章包含下列教學課程的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6842-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="c6842-111">取得 hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="c6842-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="c6842-112">疑難排解 Web UI 安裝程式錯誤</span><span class="sxs-lookup"><span data-stu-id="c6842-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="c6842-113">產生記錄檔封裝</span><span class="sxs-lookup"><span data-stu-id="c6842-113">Generate a log package</span></span>
* <span data-ttu-id="c6842-114">關閉或重新啟動您的裝置</span><span class="sxs-lookup"><span data-stu-id="c6842-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="c6842-115">取得 hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="c6842-115">Get hello service data encryption key</span></span>
<span data-ttu-id="c6842-116">當您以 hello StorSimple Manager 服務註冊第一個裝置時，會產生服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="c6842-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="c6842-117">這個索引鍵是所需要的 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="c6842-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="c6842-118">如果您有錯置的服務資料加密金鑰，需要 tooretrieve，執行 hello 下列步驟在 hello 本機 web UI hello 裝置註冊服務。</span><span class="sxs-lookup"><span data-stu-id="c6842-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="c6842-119">tooget hello 服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="c6842-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="c6842-120">連接 toohello 本機 web UI。</span><span class="sxs-lookup"><span data-stu-id="c6842-120">Connect toohello local web UI.</span></span> <span data-ttu-id="c6842-121">跳過**組態** > **雲端設定**。</span><span class="sxs-lookup"><span data-stu-id="c6842-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="c6842-122">在 hello hello 頁面底部，按一下**Get 的服務資料加密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="c6842-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="c6842-123">金鑰將會顯示。</span><span class="sxs-lookup"><span data-stu-id="c6842-123">A key will appear.</span></span> <span data-ttu-id="c6842-124">複製並儲存此金鑰。</span><span class="sxs-lookup"><span data-stu-id="c6842-124">Copy and save this key.</span></span>
   
    ![取得服務資料加密金鑰 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="c6842-126">疑難排解 Web UI 安裝程式錯誤</span><span class="sxs-lookup"><span data-stu-id="c6842-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="c6842-127">在某些情況下當您設定 hello 裝置透過 hello 本機 web UI，您可能會遇到錯誤。</span><span class="sxs-lookup"><span data-stu-id="c6842-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="c6842-128">toodiagnose 和疑難排解這類錯誤，您可以執行 hello 診斷測試。</span><span class="sxs-lookup"><span data-stu-id="c6842-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="c6842-129">toorun hello 診斷測試</span><span class="sxs-lookup"><span data-stu-id="c6842-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="c6842-130">在本機 web UI hello，移過**疑難排解** > **診斷測試**。</span><span class="sxs-lookup"><span data-stu-id="c6842-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![執行診斷 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="c6842-132">在 hello hello 頁面底部，按一下**執行診斷測試**。</span><span class="sxs-lookup"><span data-stu-id="c6842-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="c6842-133">這會起始測試 toodiagnose 任何可能與您的網路、 裝置、 web proxy、 時間或雲端設定的問題。</span><span class="sxs-lookup"><span data-stu-id="c6842-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="c6842-134">系統會通知您該 hello 裝置正在執行測試。</span><span class="sxs-lookup"><span data-stu-id="c6842-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="c6842-135">Hello 測試都已完成之後，將會顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="c6842-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="c6842-136">hello 下列範例顯示 hello 診斷測試結果。</span><span class="sxs-lookup"><span data-stu-id="c6842-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="c6842-137">請注意，hello web proxy 設定未設定此裝置，因此，無法執行 hello web proxy 測試。</span><span class="sxs-lookup"><span data-stu-id="c6842-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="c6842-138">所有 hello 其他測試網路設定，DNS 伺服器，以及時間設定成功。</span><span class="sxs-lookup"><span data-stu-id="c6842-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![執行診斷 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="c6842-140">產生記錄檔封裝</span><span class="sxs-lookup"><span data-stu-id="c6842-140">Generate a log package</span></span>
<span data-ttu-id="c6842-141">記錄檔套件包含所有 hello 相關記錄，有助於協助 Microsoft 支援服務，任何裝置的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="c6842-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="c6842-142">在此版本中，可以透過 hello 本機 web UI 產生記錄檔套件。</span><span class="sxs-lookup"><span data-stu-id="c6842-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="c6842-143">toogenerate hello 記錄封裝</span><span class="sxs-lookup"><span data-stu-id="c6842-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="c6842-144">在本機 web UI hello，移過**疑難排解** > **系統記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="c6842-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![產生記錄檔封裝 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="c6842-146">在 hello hello 頁面底部，按一下**建立記錄檔套件**。</span><span class="sxs-lookup"><span data-stu-id="c6842-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="c6842-147">將建立 hello 系統記錄檔的封裝。</span><span class="sxs-lookup"><span data-stu-id="c6842-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="c6842-148">這需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c6842-148">This will take a couple of minutes.</span></span>
   
    ![產生記錄檔封裝 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="c6842-150">已成功建立 hello 封裝，並 tooindicate hello 時間和日期建立 hello 封裝時，將會更新 hello 頁面之後，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="c6842-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![產生記錄檔封裝 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="c6842-152">按一下 [下載記錄檔封裝] 。</span><span class="sxs-lookup"><span data-stu-id="c6842-152">Click **Download log package**.</span></span> <span data-ttu-id="c6842-153">壓縮的封裝將會下載到您的系統上。</span><span class="sxs-lookup"><span data-stu-id="c6842-153">A zipped package will be downloaded on your system.</span></span>
   
    ![產生記錄檔封裝 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="c6842-155">您可以解壓縮 hello 下載記錄檔的封裝，並檢視 hello 系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c6842-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="c6842-156">關閉並重新啟動您的裝置</span><span class="sxs-lookup"><span data-stu-id="c6842-156">Shut down and restart your device</span></span>
<span data-ttu-id="c6842-157">您可以關閉或重新啟動虛擬裝置 hello 本機 web UI。</span><span class="sxs-lookup"><span data-stu-id="c6842-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="c6842-158">我們建議，再重新啟動、 hello 主機上讓 hello 磁碟區或共用離線再 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="c6842-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="c6842-159">這樣可以讓資料損毀的可能性降至最低。</span><span class="sxs-lookup"><span data-stu-id="c6842-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="c6842-160">tooshut 向您的虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="c6842-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="c6842-161">在本機 web UI hello，移過**維護** > **電源設定**。</span><span class="sxs-lookup"><span data-stu-id="c6842-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="c6842-162">在 hello hello 頁面底部，按一下**關機**。</span><span class="sxs-lookup"><span data-stu-id="c6842-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![裝置關閉 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="c6842-164">會出現警告，指出關機的 hello 裝置將會中斷已在進行中，進入停機狀態造成任何 IO。</span><span class="sxs-lookup"><span data-stu-id="c6842-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="c6842-165">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="c6842-165">Click hello check icon</span></span> ![核取圖示](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="c6842-167">。</span><span class="sxs-lookup"><span data-stu-id="c6842-167">.</span></span>
   
    ![裝置關閉警告](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="c6842-169">系統會通知您已起始 hello 關閉。</span><span class="sxs-lookup"><span data-stu-id="c6842-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![已開始關閉裝置](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="c6842-171">hello 裝置會立即關閉。</span><span class="sxs-lookup"><span data-stu-id="c6842-171">hello device will now shut down.</span></span> <span data-ttu-id="c6842-172">如果您想 toostart 您的裝置，您需要 toodo，透過 hello HYPER-V 管理員。</span><span class="sxs-lookup"><span data-stu-id="c6842-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="c6842-173">toorestart 虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="c6842-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="c6842-174">在本機 web UI hello，移過**維護** > **電源設定**。</span><span class="sxs-lookup"><span data-stu-id="c6842-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="c6842-175">在 hello hello 頁面底部，按一下**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="c6842-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![裝置重新啟動](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="c6842-177">會出現警告，指出該重新啟動的 hello 裝置將會中斷已在進行中，導致停機所有 IOs。</span><span class="sxs-lookup"><span data-stu-id="c6842-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="c6842-178">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="c6842-178">Click hello check icon</span></span> ![核取圖示](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="c6842-180">。</span><span class="sxs-lookup"><span data-stu-id="c6842-180">.</span></span>
   
    ![重新啟動警告](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="c6842-182">系統會通知您已起始 hello 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c6842-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![已起始重新啟動](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="c6842-184">在進行 hello 重新啟動時，您將會遺失 hello 連接 toohello UI。</span><span class="sxs-lookup"><span data-stu-id="c6842-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="c6842-185">您可以透過定期重新整理 hello UI 監視 hello 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c6842-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="c6842-186">或者，您可以監視透過 HYPER-V 管理員 hello hello 裝置重新啟動狀態。</span><span class="sxs-lookup"><span data-stu-id="c6842-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6842-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6842-187">Next steps</span></span>
<span data-ttu-id="c6842-188">了解如何太[使用 hello StorSimple Manager 服務 toomanage 裝置](storsimple-virtual-array-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="c6842-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

