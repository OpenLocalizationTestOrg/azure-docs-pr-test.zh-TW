---
title: "aaaConnect 覆盆子 Pi tooAzure IoT 套件使用 C toosupport 韌體更新 |Microsoft 文件"
description: "使用 hello 覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件 hello 和 Azure IoT 套件。 使用 C tooconnect 遠端監視解決方案程式覆盆子 Pi toohello、 感應器從傳送遙測 toohello 雲端，並執行遠端軔體更新。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="4afac-104">連接遠端監視解決方案程式覆盆子 Pi 3 toohello 並啟用遠端韌體更新使用 C</span><span class="sxs-lookup"><span data-stu-id="4afac-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="4afac-105">本教學課程會示範如何 toouse hello 至覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件：</span><span class="sxs-lookup"><span data-stu-id="4afac-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="4afac-106">開發氣溫和溼度的讀取器可與 hello 雲端通訊。</span><span class="sxs-lookup"><span data-stu-id="4afac-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="4afac-107">啟用及執行遠端韌體更新 tooupdate hello 用戶端應用程式上 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="4afac-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="4afac-108">hello 教學課程使用：</span><span class="sxs-lookup"><span data-stu-id="4afac-108">hello tutorial uses:</span></span>

* <span data-ttu-id="4afac-109">Raspbian OS、 hello C 程式設計語言和為 C tooimplement 範例裝置 hello Microsoft Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="4afac-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="4afac-110">hello IoT 套件遠端監視預先設定的解決方案做為 hello 以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="4afac-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="4afac-111">概觀</span><span class="sxs-lookup"><span data-stu-id="4afac-111">Overview</span></span>

<span data-ttu-id="4afac-112">在本教學課程中，您完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4afac-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="4afac-113">部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4afac-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="4afac-114">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4afac-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="4afac-115">設定您的電腦與 hello 與您的裝置與感應器 toocommunicate 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="4afac-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="4afac-116">更新 hello 範例裝置的程式碼 tooconnect toohello 遠端監視解決方案，並傳送嗨方案儀表板，您可以檢視的遙測。</span><span class="sxs-lookup"><span data-stu-id="4afac-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="4afac-117">使用 hello 範例裝置的程式碼 tooupdate hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="4afac-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="4afac-118">hello 遠端監視解決方案會佈建一組您 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4afac-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="4afac-119">hello 部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="4afac-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="4afac-120">當您完成與其 tooavoid 不必要的 Azure 使用費用，會刪除 hello 預先設定的解決方案，在 azureiotsuite.com 您執行個體。</span><span class="sxs-lookup"><span data-stu-id="4afac-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="4afac-121">如果您需要再次 hello 預先設定的方案，您可以輕鬆地重新建立。</span><span class="sxs-lookup"><span data-stu-id="4afac-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="4afac-122">減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="4afac-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="4afac-123">下載及設定 hello 範例</span><span class="sxs-lookup"><span data-stu-id="4afac-123">Download and configure hello sample</span></span>

<span data-ttu-id="4afac-124">現在，您可以下載並設定覆盆子 pi hello 遠端監視用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="4afac-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="4afac-125">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="4afac-125">Clone hello repositories</span></span>

<span data-ttu-id="4afac-126">如果還沒有這麼做，複製 hello 所需執行的儲存機制 hello 您 pi 下列命令：</span><span class="sxs-lookup"><span data-stu-id="4afac-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="4afac-127">更新 hello 裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="4afac-127">Update hello device connection string</span></span>

<span data-ttu-id="4afac-128">開啟 hello 範例組態檔中 hello **nano**編輯器使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4afac-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="4afac-129">Hello 預留位置值 hello 裝置識別碼和 IoT 中樞資訊來取代您建立並儲存在本教學課程中的 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="4afac-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="4afac-130">當您完成之後時，hello hello deviceinfo 檔內容看起來應該像下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4afac-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="4afac-131">儲存您的變更 (**Ctrl-O**， **Enter**) 和結束 hello 編輯器 (**Ctrl X**)。</span><span class="sxs-lookup"><span data-stu-id="4afac-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="4afac-132">建立 hello 範例</span><span class="sxs-lookup"><span data-stu-id="4afac-132">Build hello sample</span></span>

<span data-ttu-id="4afac-133">如果您尚未這樣做，執行命令在終止後 hello 覆盆子 Pi hello hello hello Microsoft Azure IoT 裝置 SDK 的必要條件套件安裝 c:</span><span class="sxs-lookup"><span data-stu-id="4afac-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="4afac-134">您現在可以在 hello 覆盆子 Pi 建置 hello 範例方案：</span><span class="sxs-lookup"><span data-stu-id="4afac-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="4afac-135">您現在可以在 hello 覆盆子 Pi 執行 hello 範例程式。</span><span class="sxs-lookup"><span data-stu-id="4afac-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="4afac-136">輸入 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="4afac-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="4afac-137">hello 下列範例輸出是您 hello 覆盆子 Pi hello 命令提示字元下，請參閱 hello 輸出的範例：</span><span class="sxs-lookup"><span data-stu-id="4afac-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Raspberry Pi 應用程式的輸出][img-raspberry-output]

<span data-ttu-id="4afac-139">按**CTRL-C** tooexit hello 程式在任何時間。</span><span class="sxs-lookup"><span data-stu-id="4afac-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="4afac-140">在 hello 方案儀表板中，按一下 **裝置**toovisit hello**裝置**頁面。</span><span class="sxs-lookup"><span data-stu-id="4afac-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="4afac-141">選取在 hello 覆盆子 Pi**裝置清單**。</span><span class="sxs-lookup"><span data-stu-id="4afac-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="4afac-142">然後選擇 [方法]：</span><span class="sxs-lookup"><span data-stu-id="4afac-142">Then choose **Methods**:</span></span>

    ![在儀表板中列出裝置][img-list-devices]

1. <span data-ttu-id="4afac-144">在 hello**叫用方法**頁面上，選擇**InitiateFirmwareUpdate**在 hello**方法**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="4afac-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="4afac-145">在 hello **FWPackageURI**欄位中，輸入**https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**。</span><span class="sxs-lookup"><span data-stu-id="4afac-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="4afac-146">這個封存檔案包含 hello hello 韌體版本 2.0 實作。</span><span class="sxs-lookup"><span data-stu-id="4afac-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="4afac-147">選擇 [InvokeMethod]。</span><span class="sxs-lookup"><span data-stu-id="4afac-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="4afac-148">hello hello 覆盆子 Pi 上的應用程式傳送的通知後 toohello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="4afac-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="4afac-149">接著它會啟動 hello 韌體更新程序下載新版 hello 韌體 hello:</span><span class="sxs-lookup"><span data-stu-id="4afac-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![顯示方法歷程記錄][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="4afac-151">觀察 hello 韌體更新程序</span><span class="sxs-lookup"><span data-stu-id="4afac-151">Observe hello firmware update process</span></span>

<span data-ttu-id="4afac-152">您可以在 hello 裝置上執行，觀察 hello 韌體更新程序及檢視 hello 回報 hello 方案儀表板中的屬性：</span><span class="sxs-lookup"><span data-stu-id="4afac-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="4afac-153">您可以檢視 hello 覆盆子 Pi hello 正在進行中的 hello 更新程序：</span><span class="sxs-lookup"><span data-stu-id="4afac-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![顯示更新進度][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="4afac-155">hello 遠端監視應用程式會重新啟動以無訊息模式，hello 更新完成時。</span><span class="sxs-lookup"><span data-stu-id="4afac-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="4afac-156">使用 hello 命令`ps -ef`tooverify 它正在執行。</span><span class="sxs-lookup"><span data-stu-id="4afac-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="4afac-157">如果您想 tooterminate hello 程序，使用 hello`kill`命令與 hello 處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="4afac-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="4afac-158">Hello 方案入口網站中的 hello 裝置所報告，您可以檢視 hello 韌體更新，hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="4afac-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="4afac-159">hello 下列螢幕擷取畫面顯示 hello 狀態和持續時間的 hello 更新程序，以及 hello 新的韌體版本每個階段：</span><span class="sxs-lookup"><span data-stu-id="4afac-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![顯示作業狀態][img-job-status]

    <span data-ttu-id="4afac-161">如果您瀏覽後 toohello 儀表板，您可以確認 hello 裝置仍在傳送 hello 韌體更新之後的遙測。</span><span class="sxs-lookup"><span data-stu-id="4afac-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="4afac-162">如果您離開 hello 遠端監視您的 Azure 帳戶中執行的解決方案，您所要支付 hello 次執行。</span><span class="sxs-lookup"><span data-stu-id="4afac-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="4afac-163">減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="4afac-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="4afac-164">使用完畢時，請從您的 Azure 帳戶刪除 hello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4afac-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4afac-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4afac-165">Next steps</span></span>

<span data-ttu-id="4afac-166">請瀏覽 hello [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)取得更多範例和 Azure IoT 文件。</span><span class="sxs-lookup"><span data-stu-id="4afac-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md