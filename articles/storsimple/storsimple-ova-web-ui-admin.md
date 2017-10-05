---
title: "StorSimple Virtual Array Web UI 管理 |Microsoft Docs"
description: "描述如何透過 StorSimple Virtual Array Web UI 執行基本的裝置管理工作。"
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
ms.openlocfilehash: 989e7b697f9b527df549fb32be18edd1d3c8d224
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-web-ui-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="26e22-103">使用 Web UI 來管理 StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="26e22-103">Use the Web UI to administer your StorSimple Virtual Array</span></span>
![安裝程序流程](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="26e22-105">概觀</span><span class="sxs-lookup"><span data-stu-id="26e22-105">Overview</span></span>
<span data-ttu-id="26e22-106">本文中的教學課程適用於執行 2016 年 3 月公開上市 (GA) 版的 Microsoft Azure StorSimple Virtual Array (也稱為 StorSimple 內部部署虛擬裝置)。</span><span class="sxs-lookup"><span data-stu-id="26e22-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="26e22-107">本文將說明一些可以在 StorSimple Virtual Array 執行的複雜工作流程和管理工作。</span><span class="sxs-lookup"><span data-stu-id="26e22-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span></span> <span data-ttu-id="26e22-108">您可以使用 StorSimple Manager 服務 UI (又稱為入口網站 UI) 和裝置的本機 Web UI 來管理 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="26e22-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span></span> <span data-ttu-id="26e22-109">本文著重於可使用 Web UI 執行的工作。</span><span class="sxs-lookup"><span data-stu-id="26e22-109">This article focuses on the tasks that you can perform using the web UI.</span></span>

<span data-ttu-id="26e22-110">本文包含下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="26e22-110">This article includes the following tutorials:</span></span>

* <span data-ttu-id="26e22-111">取得服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="26e22-111">Get the service data encryption key</span></span>
* <span data-ttu-id="26e22-112">疑難排解 Web UI 安裝程式錯誤</span><span class="sxs-lookup"><span data-stu-id="26e22-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="26e22-113">產生記錄檔封裝</span><span class="sxs-lookup"><span data-stu-id="26e22-113">Generate a log package</span></span>
* <span data-ttu-id="26e22-114">關閉或重新啟動您的裝置</span><span class="sxs-lookup"><span data-stu-id="26e22-114">Shut down or restart your device</span></span>

## <a name="get-the-service-data-encryption-key"></a><span data-ttu-id="26e22-115">取得服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="26e22-115">Get the service data encryption key</span></span>
<span data-ttu-id="26e22-116">當您向 StorSimple Manager 服務註冊您的第一個裝置時，會產生服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="26e22-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span></span> <span data-ttu-id="26e22-117">這個金鑰需要與服務註冊金鑰搭配使用，以向 StorSimple Manager 服務註冊其他裝置。</span><span class="sxs-lookup"><span data-stu-id="26e22-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span></span>

<span data-ttu-id="26e22-118">如果您弄丟您的服務資料加密金鑰而需要擷取它，請在向您的服務註冊的裝置的本機 Web UI 中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="26e22-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span></span>

#### <a name="to-get-the-service-data-encryption-key"></a><span data-ttu-id="26e22-119">取得服務資料加密金鑰</span><span class="sxs-lookup"><span data-stu-id="26e22-119">To get the service data encryption key</span></span>
1. <span data-ttu-id="26e22-120">連線到本機 Web UI。</span><span class="sxs-lookup"><span data-stu-id="26e22-120">Connect to the local web UI.</span></span> <span data-ttu-id="26e22-121">移至 [組態]  >  [雲端設定]。</span><span class="sxs-lookup"><span data-stu-id="26e22-121">Go to **Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="26e22-122">按一下頁面底部的 [取得服務資料加密金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="26e22-122">At the bottom of the page, click **Get service data encryption key**.</span></span> <span data-ttu-id="26e22-123">金鑰將會顯示。</span><span class="sxs-lookup"><span data-stu-id="26e22-123">A key will appear.</span></span> <span data-ttu-id="26e22-124">複製並儲存此金鑰。</span><span class="sxs-lookup"><span data-stu-id="26e22-124">Copy and save this key.</span></span>
   
    ![取得服務資料加密金鑰 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="26e22-126">疑難排解 Web UI 安裝程式錯誤</span><span class="sxs-lookup"><span data-stu-id="26e22-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="26e22-127">在某些情況下，當您透過本機 Web UI 設定裝置時，可能會遇到錯誤。</span><span class="sxs-lookup"><span data-stu-id="26e22-127">In some instances when you configure the device through the local web UI, you might run into errors.</span></span> <span data-ttu-id="26e22-128">若要診斷和移難排解這類錯誤，您可以執行診斷測試。</span><span class="sxs-lookup"><span data-stu-id="26e22-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span></span>

#### <a name="to-run-the-diagnostic-tests"></a><span data-ttu-id="26e22-129">執行診斷測試</span><span class="sxs-lookup"><span data-stu-id="26e22-129">To run the diagnostic tests</span></span>
1. <span data-ttu-id="26e22-130">在本機 Web UI 中，移至 [疑難排解]  >  [診斷測試]。</span><span class="sxs-lookup"><span data-stu-id="26e22-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![執行診斷 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="26e22-132">按一下頁面底部的 [執行診斷測試] 。</span><span class="sxs-lookup"><span data-stu-id="26e22-132">At the bottom of the page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="26e22-133">這樣會起始測試以診斷和您的網路、裝置、Web Proxy、時間或雲端設定相關的任何可能問題。</span><span class="sxs-lookup"><span data-stu-id="26e22-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="26e22-134">您將收到裝置正在執行測試的通知。</span><span class="sxs-lookup"><span data-stu-id="26e22-134">You will be notified that the device is running tests.</span></span>
3. <span data-ttu-id="26e22-135">測試完成後會顯示結果。</span><span class="sxs-lookup"><span data-stu-id="26e22-135">After the tests have completed, the results will be displayed.</span></span> <span data-ttu-id="26e22-136">下列範例顯示診斷測試的結果。</span><span class="sxs-lookup"><span data-stu-id="26e22-136">The following example shows the results of diagnostic tests.</span></span> <span data-ttu-id="26e22-137">請注意，此裝置上未設定 Web Proxy 設定，因此未執行 Web Proxy 測試。</span><span class="sxs-lookup"><span data-stu-id="26e22-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span></span> <span data-ttu-id="26e22-138">網路設定、DNS 伺服器和時間設定的所有其他測試均成功。</span><span class="sxs-lookup"><span data-stu-id="26e22-138">All the other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![執行診斷 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="26e22-140">產生記錄檔封裝</span><span class="sxs-lookup"><span data-stu-id="26e22-140">Generate a log package</span></span>
<span data-ttu-id="26e22-141">記錄檔封裝包含有助於 Microsoft 支援小組疑難排解任何裝置問題的所有相關記錄檔。</span><span class="sxs-lookup"><span data-stu-id="26e22-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="26e22-142">在此版本中，可透過本機 Web UI 產生記錄檔封裝。</span><span class="sxs-lookup"><span data-stu-id="26e22-142">In this release, a log package can be generated via the local web UI.</span></span>

#### <a name="to-generate-the-log-package"></a><span data-ttu-id="26e22-143">產生記錄檔封裝</span><span class="sxs-lookup"><span data-stu-id="26e22-143">To generate the log package</span></span>
1. <span data-ttu-id="26e22-144">在本機 Web UI 中，移至 [疑難排解]  >  [系統記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="26e22-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span></span>
   
    ![產生記錄檔封裝 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="26e22-146">按一下頁面底部的 [建立記錄檔封裝] 。</span><span class="sxs-lookup"><span data-stu-id="26e22-146">At the bottom of the page, click **Create log package**.</span></span> <span data-ttu-id="26e22-147">將建立系統記錄檔的封裝。</span><span class="sxs-lookup"><span data-stu-id="26e22-147">A package of the system logs will be created.</span></span> <span data-ttu-id="26e22-148">這需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="26e22-148">This will take a couple of minutes.</span></span>
   
    ![產生記錄檔封裝 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="26e22-150">系統會通知您已成功建立封裝，並會更新頁面以顯示封裝建立的日期與時間。</span><span class="sxs-lookup"><span data-stu-id="26e22-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span></span>
   
    ![產生記錄檔封裝 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="26e22-152">按一下 [下載記錄檔封裝] 。</span><span class="sxs-lookup"><span data-stu-id="26e22-152">Click **Download log package**.</span></span> <span data-ttu-id="26e22-153">壓縮的封裝將會下載到您的系統上。</span><span class="sxs-lookup"><span data-stu-id="26e22-153">A zipped package will be downloaded on your system.</span></span>
   
    ![產生記錄檔封裝 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="26e22-155">您可以解壓縮下載的記錄檔封裝，並檢視系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="26e22-155">You can unzip the downloaded log package and view the system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="26e22-156">關閉並重新啟動您的裝置</span><span class="sxs-lookup"><span data-stu-id="26e22-156">Shut down and restart your device</span></span>
<span data-ttu-id="26e22-157">您可以使用本機 Web UI 關閉或重新啟動您的虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="26e22-157">You can shut down or restart your virtual device using the local web UI.</span></span> <span data-ttu-id="26e22-158">我們建議您在重新啟動之前，讓主機上的磁碟區或共用離線，然後讓裝置離線。</span><span class="sxs-lookup"><span data-stu-id="26e22-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span></span> <span data-ttu-id="26e22-159">這樣可以讓資料損毀的可能性降至最低。</span><span class="sxs-lookup"><span data-stu-id="26e22-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="to-shut-down-your-virtual-device"></a><span data-ttu-id="26e22-160">關閉虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="26e22-160">To shut down your virtual device</span></span>
1. <span data-ttu-id="26e22-161">在本機 Web UI 中，移至 [維護]  >  [電源設定]。</span><span class="sxs-lookup"><span data-stu-id="26e22-161">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="26e22-162">按一下頁面底部的 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="26e22-162">At the bottom of the page, click **Shutdown**.</span></span>
   
    ![裝置關閉 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="26e22-164">會出現警告，指出關閉裝置將中斷已在進行的任何 IO，因而導致停機。</span><span class="sxs-lookup"><span data-stu-id="26e22-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="26e22-165">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="26e22-165">Click the check icon</span></span> ![核取圖示](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="26e22-167">。</span><span class="sxs-lookup"><span data-stu-id="26e22-167">.</span></span>
   
    ![裝置關閉警告](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="26e22-169">系統會通知您已起始關機。</span><span class="sxs-lookup"><span data-stu-id="26e22-169">You will be notified that the shutdown has been initiated.</span></span>
   
    ![已開始關閉裝置](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="26e22-171">裝置會立即關閉。</span><span class="sxs-lookup"><span data-stu-id="26e22-171">The device will now shut down.</span></span> <span data-ttu-id="26e22-172">如果您想要啟動您的裝置，您必須透過 Hyper-V 管理員執行。</span><span class="sxs-lookup"><span data-stu-id="26e22-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span></span>

#### <a name="to-restart-your-virtual-device"></a><span data-ttu-id="26e22-173">重新啟動虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="26e22-173">To restart your virtual device</span></span>
1. <span data-ttu-id="26e22-174">在本機 Web UI 中，移至 [維護]  >  [電源設定]。</span><span class="sxs-lookup"><span data-stu-id="26e22-174">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="26e22-175">按一下頁面底部的 [重新啟動] 。</span><span class="sxs-lookup"><span data-stu-id="26e22-175">At the bottom of the page, click **Restart**.</span></span>
   
    ![裝置重新啟動](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="26e22-177">會出現警告，指出重新啟動裝置將中斷已在進行的任何 IO，因而導致停機。</span><span class="sxs-lookup"><span data-stu-id="26e22-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="26e22-178">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="26e22-178">Click the check icon</span></span> ![核取圖示](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="26e22-180">。</span><span class="sxs-lookup"><span data-stu-id="26e22-180">.</span></span>
   
    ![重新啟動警告](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="26e22-182">系統會通知您已起始重新啟動。</span><span class="sxs-lookup"><span data-stu-id="26e22-182">You will be notified that the restart has been initiated.</span></span>
   
    ![已起始重新啟動](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="26e22-184">重新啟動時，將會中斷 UI 連線。</span><span class="sxs-lookup"><span data-stu-id="26e22-184">While the restart is in progress, you will lose the connection to the UI.</span></span> <span data-ttu-id="26e22-185">您可以定期重新整理 UI 以監視重新啟動的情況。</span><span class="sxs-lookup"><span data-stu-id="26e22-185">You can monitor the restart by refreshing the UI periodically.</span></span> <span data-ttu-id="26e22-186">或者，您可以透過 Hyper-V 管理員監視裝置重新啟動狀態。</span><span class="sxs-lookup"><span data-stu-id="26e22-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26e22-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26e22-187">Next steps</span></span>
<span data-ttu-id="26e22-188">了解如何 [使用 StorSimple Manager 服務管理裝置](storsimple-virtual-array-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="26e22-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

