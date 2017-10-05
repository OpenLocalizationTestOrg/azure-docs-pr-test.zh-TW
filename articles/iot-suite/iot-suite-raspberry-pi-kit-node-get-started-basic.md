---
title: "使用 Node.js 搭配真實感應器將 Raspberry Pi 連線到 Azure IoT 套件來支援韌體更新 | Microsoft Docs"
description: "使用 Raspberry Pi 3 和 Azure IoT 套件的 Microsoft Azure IoT 入門套件。 使用 Node.js 將 Raspberry Pi 連線到遠端監視解決方案、將遙測從感應器傳送到雲端，並回應解決方案儀表板所叫用的方法。"
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
ms.openlocfilehash: 91546157cc8eabf68706391ce706038d8dc5f82d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="a2b4d-104">將 Raspberry Pi 3 連線到遠端監視解決方案，並且使用 Node.js 從真實感應器傳送遙測</span><span class="sxs-lookup"><span data-stu-id="a2b4d-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="a2b4d-105">本教學課程會示範如何使用 Raspberry Pi 3 的 Microsoft Azure IoT 入門套件來開發可與雲端通訊的溫度與溼度讀取器。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="a2b4d-106">教學課程會使用：</span><span class="sxs-lookup"><span data-stu-id="a2b4d-106">The tutorial uses:</span></span>

- <span data-ttu-id="a2b4d-107">Raspbian OS、Node.js 程式設計語言和 Microsoft Azure IoT SDK for Node.js 來實作範例裝置。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="a2b4d-108">IoT 套件遠端監視預先設定解決方案作為以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="a2b4d-109">概觀</span><span class="sxs-lookup"><span data-stu-id="a2b4d-109">Overview</span></span>

<span data-ttu-id="a2b4d-110">在本教學課程中，您會完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a2b4d-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="a2b4d-111">將遠端監視預先設定解決方案的執行個體部署至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="a2b4d-112">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="a2b4d-113">設定您的裝置和感應器，以便與您的電腦和遠端監視解決方案進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="a2b4d-114">更新範例裝置程式碼以連線到遠端監視解決方案，並傳送您可以在解決方案儀表板上檢視的遙測。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="a2b4d-115">遠端監視解決方案會佈建一組 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="a2b4d-116">部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="a2b4d-117">若要避免不必要的 Azure 耗用量費用，當您使用完 azureiotsuite.com 中預先設定解決方案的執行個體時，請將它刪除。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="a2b4d-118">如果您還需要預先設定的解決方案，可以輕鬆地將它重新建立。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="a2b4d-119">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="a2b4d-120">下載並設定範例</span><span class="sxs-lookup"><span data-stu-id="a2b4d-120">Download and configure the sample</span></span>

<span data-ttu-id="a2b4d-121">您現在可以在 Raspberry Pi 上將遠端監視用戶端應用程式進行下載及設定。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="a2b4d-122">安裝 Node.js</span><span class="sxs-lookup"><span data-stu-id="a2b4d-122">Install Node.js</span></span>

<span data-ttu-id="a2b4d-123">在 Raspberry Pi 上安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="a2b4d-124">適用於 Node.js 的 IoT SDK 需要 Node.js 0.11.5 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-124">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="a2b4d-125">下列步驟說明如何在 Raspberry Pi 上安裝 Node.js 6.10.2 版：</span><span class="sxs-lookup"><span data-stu-id="a2b4d-125">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="a2b4d-126">若要更新 Raspberry Pi，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-126">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="a2b4d-127">若要將 Node.js 二進位檔下載至 Raspberry Pi，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-127">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a2b4d-128">使用下列命令來安裝二進位檔：</span><span class="sxs-lookup"><span data-stu-id="a2b4d-128">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="a2b4d-129">若要確認您已成功安裝 Node.js 6.10.2 版，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-129">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="a2b4d-130">複製存放庫</span><span class="sxs-lookup"><span data-stu-id="a2b4d-130">Clone the repositories</span></span>

<span data-ttu-id="a2b4d-131">如果您尚未這麼做，請在 Pi 上執行下列命令來複製所需的存放庫︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-131">If you haven't already done so, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="a2b4d-132">更新裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="a2b4d-132">Update the device connection string</span></span>

<span data-ttu-id="a2b4d-133">使用下列命令，將 **nano** 編輯器中的範例來源檔案開啟︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-133">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="a2b4d-134">請尋找以下這行︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-134">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="a2b4d-135">將預留位置值取代為本教學課程開頭所建立及儲存的裝置和 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-135">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="a2b4d-136">儲存您的變更 (**Ctrl-O**、**Enter**) 並結束編輯器 (**Ctrl-X**)。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-136">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="a2b4d-137">執行範例</span><span class="sxs-lookup"><span data-stu-id="a2b4d-137">Run the sample</span></span>

<span data-ttu-id="a2b4d-138">執行下列命令來安裝範例的必要條件套件︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-138">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="a2b4d-139">您現在可以在 Raspberry Pi 上執行範例程式。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-139">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="a2b4d-140">輸入命令：</span><span class="sxs-lookup"><span data-stu-id="a2b4d-140">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="a2b4d-141">下列範例輸出是您在 Raspberry Pi 的命令提示字元所看到的輸出範例︰</span><span class="sxs-lookup"><span data-stu-id="a2b4d-141">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Raspberry Pi 應用程式的輸出][img-raspberry-output]

<span data-ttu-id="a2b4d-143">按下 **CTRL-C** 可隨時結束程式。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-143">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="a2b4d-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2b4d-144">Next steps</span></span>

<span data-ttu-id="a2b4d-145">請瀏覽 [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)，取得更多 Azure IoT 的相關範例和文件。</span><span class="sxs-lookup"><span data-stu-id="a2b4d-145">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
