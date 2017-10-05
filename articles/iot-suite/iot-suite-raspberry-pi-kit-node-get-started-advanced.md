---
title: "使用 Node.js 將 Raspberry Pi 連線到 Azure IoT 套件來支援韌體更新 | Microsoft Docs"
description: "使用 Raspberry Pi 3 和 Azure IoT 套件的 Microsoft Azure IoT 入門套件。 使用 Node.js 將 Raspberry Pi 連線到遠端監視解決方案、將遙測從感應器傳送到雲端，並執行遠端韌體更新。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 54503d5d6a636239d240509d7d09cf334234bac7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="bec0c-104">將 Raspberry Pi 3 連線到遠端監視解決方案，並且使用 Node.js 來啟用遠端韌體更新</span><span class="sxs-lookup"><span data-stu-id="bec0c-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="bec0c-105">本教學課程將示範如何使用 Raspberry Pi 3 的 Microsoft Azure IoT 入門套件進行︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="bec0c-106">開發可與雲端通訊的溫度與溼度讀取器。</span><span class="sxs-lookup"><span data-stu-id="bec0c-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="bec0c-107">啟用及執行遠端韌體更新，來更新 Raspberry Pi 上的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="bec0c-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="bec0c-108">教學課程會使用：</span><span class="sxs-lookup"><span data-stu-id="bec0c-108">The tutorial uses:</span></span>

- <span data-ttu-id="bec0c-109">Raspbian OS、Node.js 程式設計語言和 Microsoft Azure IoT SDK for Node.js 來實作範例裝置。</span><span class="sxs-lookup"><span data-stu-id="bec0c-109">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="bec0c-110">IoT 套件遠端監視預先設定解決方案作為以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="bec0c-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="bec0c-111">概觀</span><span class="sxs-lookup"><span data-stu-id="bec0c-111">Overview</span></span>

<span data-ttu-id="bec0c-112">在本教學課程中，您會完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bec0c-112">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="bec0c-113">將遠端監視預先設定解決方案的執行個體部署至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bec0c-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="bec0c-114">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="bec0c-115">設定您的裝置和感應器，以便與您的電腦和遠端監視解決方案進行通訊。</span><span class="sxs-lookup"><span data-stu-id="bec0c-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="bec0c-116">更新範例裝置程式碼以連線到遠端監視解決方案，並傳送您可以在解決方案儀表板上檢視的遙測。</span><span class="sxs-lookup"><span data-stu-id="bec0c-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
- <span data-ttu-id="bec0c-117">使用範例裝置程式碼來更新用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="bec0c-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="bec0c-118">遠端監視解決方案會佈建一組 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="bec0c-119">部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="bec0c-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="bec0c-120">若要避免不必要的 Azure 耗用量費用，當您使用完 azureiotsuite.com 中預先設定解決方案的執行個體時，請將它刪除。</span><span class="sxs-lookup"><span data-stu-id="bec0c-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="bec0c-121">如果您還需要預先設定的解決方案，可以輕鬆地將它重新建立。</span><span class="sxs-lookup"><span data-stu-id="bec0c-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="bec0c-122">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="bec0c-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="bec0c-123">下載並設定範例</span><span class="sxs-lookup"><span data-stu-id="bec0c-123">Download and configure the sample</span></span>

<span data-ttu-id="bec0c-124">您現在可以在 Raspberry Pi 上將遠端監視用戶端應用程式進行下載及設定。</span><span class="sxs-lookup"><span data-stu-id="bec0c-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="bec0c-125">安裝 Node.js</span><span class="sxs-lookup"><span data-stu-id="bec0c-125">Install Node.js</span></span>

<span data-ttu-id="bec0c-126">如果您尚未這麼做，請在 Raspberry Pi 上安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="bec0c-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="bec0c-127">適用於 Node.js 的 IoT SDK 需要 Node.js 0.11.5 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bec0c-127">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="bec0c-128">下列步驟說明如何在 Raspberry Pi 上安裝 Node.js 6.10.2 版：</span><span class="sxs-lookup"><span data-stu-id="bec0c-128">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="bec0c-129">若要更新 Raspberry Pi，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-129">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="bec0c-130">若要將 Node.js 二進位檔下載至 Raspberry Pi，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-130">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="bec0c-131">使用下列命令來安裝二進位檔：</span><span class="sxs-lookup"><span data-stu-id="bec0c-131">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="bec0c-132">若要確認您已成功安裝 Node.js 6.10.2 版，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-132">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="bec0c-133">複製存放庫</span><span class="sxs-lookup"><span data-stu-id="bec0c-133">Clone the repositories</span></span>

<span data-ttu-id="bec0c-134">如果您尚未這麼做，請在 Pi 上執行下列命令來複製所需的存放庫︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-134">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="bec0c-135">更新裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="bec0c-135">Update the device connection string</span></span>

<span data-ttu-id="bec0c-136">使用下列命令，將 **nano** 編輯器中的範例組態檔開啟︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-136">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="bec0c-137">將預留位置值取代為本教學課程開頭所建立及儲存的裝置識別碼和 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="bec0c-137">Replace the placeholder values with the device id and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="bec0c-138">當您完成時，deviceinfo 檔案的內容看起來應該如下列範例︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-138">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="bec0c-139">儲存您的變更 (**Ctrl-O**、**Enter**) 並結束編輯器 (**Ctrl-X**)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-139">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="bec0c-140">執行範例</span><span class="sxs-lookup"><span data-stu-id="bec0c-140">Run the sample</span></span>

<span data-ttu-id="bec0c-141">執行下列命令來安裝範例的必要條件套件︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-141">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="bec0c-142">您現在可以在 Raspberry Pi 上執行範例程式。</span><span class="sxs-lookup"><span data-stu-id="bec0c-142">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="bec0c-143">輸入命令：</span><span class="sxs-lookup"><span data-stu-id="bec0c-143">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="bec0c-144">下列範例輸出是您在 Raspberry Pi 的命令提示字元所看到的輸出範例︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-144">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Raspberry Pi 應用程式的輸出][img-raspberry-output]

<span data-ttu-id="bec0c-146">按下 **CTRL-C** 可隨時結束程式。</span><span class="sxs-lookup"><span data-stu-id="bec0c-146">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="bec0c-147">在解決方案儀表板中，按一下 [裝置] 以造訪 [裝置] 頁面。</span><span class="sxs-lookup"><span data-stu-id="bec0c-147">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="bec0c-148">在 [裝置清單] 中選取您的 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="bec0c-148">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="bec0c-149">然後選擇 [方法]：</span><span class="sxs-lookup"><span data-stu-id="bec0c-149">Then choose **Methods**:</span></span>

    ![在儀表板中列出裝置][img-list-devices]

1. <span data-ttu-id="bec0c-151">在 [叫用方法] 頁面上，選擇 [方法] 下拉式清單中的 [InitiateFirmwareUpdate]。</span><span class="sxs-lookup"><span data-stu-id="bec0c-151">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="bec0c-152">在 **FWPackageURI** 欄位中，輸入 **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**。</span><span class="sxs-lookup"><span data-stu-id="bec0c-152">In the **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="bec0c-153">這個檔案包含 2.0 版韌體的實作。</span><span class="sxs-lookup"><span data-stu-id="bec0c-153">This file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="bec0c-154">選擇 [InvokeMethod]。</span><span class="sxs-lookup"><span data-stu-id="bec0c-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="bec0c-155">Raspberry Pi 上的應用程式會將通知傳回解決方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="bec0c-155">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="bec0c-156">接著，它會下載新版的韌體來啟動韌體更新程序︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-156">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![顯示方法歷程記錄][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="bec0c-158">觀察軔體更新程序</span><span class="sxs-lookup"><span data-stu-id="bec0c-158">Observe the firmware update process</span></span>

<span data-ttu-id="bec0c-159">您可以觀察在裝置上執行時的軔體更新程序，方法為檢視解決方案儀表板中的報告內容︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-159">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="bec0c-160">您可以在 Raspberry Pi 上的更新程序檢視進度︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-160">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![顯示更新進度][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="bec0c-162">更新完成時，會以無訊息模式將遠端監視應用程式重新啟動。</span><span class="sxs-lookup"><span data-stu-id="bec0c-162">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="bec0c-163">使用 `ps -ef` 命令來確認它正在執行。</span><span class="sxs-lookup"><span data-stu-id="bec0c-163">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="bec0c-164">如果您想要終止程序，請使用 `kill` 命令與程序識別碼。</span><span class="sxs-lookup"><span data-stu-id="bec0c-164">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="bec0c-165">您可以在解決方案入口網站中，檢視如裝置所報告的韌體更新狀態。</span><span class="sxs-lookup"><span data-stu-id="bec0c-165">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="bec0c-166">下列螢幕擷取畫面會顯示更新程序每個階段的狀態和持續時間，以及新的韌體版本︰</span><span class="sxs-lookup"><span data-stu-id="bec0c-166">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![顯示作業狀態][img-job-status]

    <span data-ttu-id="bec0c-168">如果您瀏覽回到儀表板，可以確認裝置仍在將下列韌體更新傳送給遙測。</span><span class="sxs-lookup"><span data-stu-id="bec0c-168">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="bec0c-169">如果讓遠端監視解決方案繼續在您的 Azure 帳戶中執行，您需支付其執行期間的費用。</span><span class="sxs-lookup"><span data-stu-id="bec0c-169">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="bec0c-170">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="bec0c-170">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="bec0c-171">使用完畢時，從您的 Azure 帳戶將預先設定的解決方案刪除。</span><span class="sxs-lookup"><span data-stu-id="bec0c-171">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bec0c-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bec0c-172">Next steps</span></span>

<span data-ttu-id="bec0c-173">請瀏覽 [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)，取得更多 Azure IoT 的相關範例和文件。</span><span class="sxs-lookup"><span data-stu-id="bec0c-173">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
