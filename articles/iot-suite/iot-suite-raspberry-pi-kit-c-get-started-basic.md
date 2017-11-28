---
title: "aaaConnect 覆盆子 Pi tooAzure IoT 套件真實的感應器搭配使用 C |Microsoft 文件"
description: "使用 hello 覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件 hello 和 Azure IoT 套件。 使用 C tooconnect 遠端監視解決方案程式覆盆子 Pi toohello、 感應器從 toohello 雲端傳送遙測和回應 toomethods hello 方案儀表板從叫用。"
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="d6aea-104">連接遠端監視解決方案程式覆盆子 Pi 3 toohello 並傳送遙測，從使用 C 真實感應器</span><span class="sxs-lookup"><span data-stu-id="d6aea-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="d6aea-105">本教學課程會示範如何 toouse hello Microsoft Azure IoT 入門套件覆盆子 Pi 3 toodevelop 氣溫和溼度的讀取器可與 hello 雲端通訊。</span><span class="sxs-lookup"><span data-stu-id="d6aea-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="d6aea-106">hello 教學課程使用：</span><span class="sxs-lookup"><span data-stu-id="d6aea-106">hello tutorial uses:</span></span>

- <span data-ttu-id="d6aea-107">Raspbian OS、 hello C 程式設計語言和為 C tooimplement 範例裝置 hello Microsoft Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="d6aea-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="d6aea-108">hello IoT 套件遠端監視預先設定的解決方案做為 hello 以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="d6aea-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="d6aea-109">概觀</span><span class="sxs-lookup"><span data-stu-id="d6aea-109">Overview</span></span>

<span data-ttu-id="d6aea-110">在本教學課程中，您完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d6aea-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="d6aea-111">部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6aea-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="d6aea-112">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="d6aea-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="d6aea-113">設定您的電腦與 hello 與您的裝置與感應器 toocommunicate 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="d6aea-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="d6aea-114">更新 hello 範例裝置的程式碼 tooconnect toohello 遠端監視解決方案，並傳送嗨方案儀表板，您可以檢視的遙測。</span><span class="sxs-lookup"><span data-stu-id="d6aea-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="d6aea-115">hello 遠端監視解決方案會佈建一組您 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="d6aea-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="d6aea-116">hello 部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="d6aea-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="d6aea-117">當您完成與其 tooavoid 不必要的 Azure 使用費用，會刪除 hello 預先設定的解決方案，在 azureiotsuite.com 您執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6aea-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="d6aea-118">如果您需要再次 hello 預先設定的方案，您可以輕鬆地重新建立。</span><span class="sxs-lookup"><span data-stu-id="d6aea-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="d6aea-119">減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="d6aea-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="d6aea-120">下載及設定 hello 範例</span><span class="sxs-lookup"><span data-stu-id="d6aea-120">Download and configure hello sample</span></span>

<span data-ttu-id="d6aea-121">現在，您可以下載並設定覆盆子 pi hello 遠端監視用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6aea-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="d6aea-122">複製 hello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="d6aea-122">Clone hello repositories</span></span>

<span data-ttu-id="d6aea-123">如果您尚未這樣做，請複製 hello 所需執行的儲存機制 hello 遵循您 Pi 中終端機的命令：</span><span class="sxs-lookup"><span data-stu-id="d6aea-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="d6aea-124">更新 hello 裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="d6aea-124">Update hello device connection string</span></span>

<span data-ttu-id="d6aea-125">開啟 hello 範例原始程式檔中 hello **nano**編輯器使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d6aea-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="d6aea-126">找出下列幾行 hello:</span><span class="sxs-lookup"><span data-stu-id="d6aea-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="d6aea-127">Hello 預留位置值取代 hello 裝置和您建立並儲存在本教學課程中的 hello 開頭的 IoT 中樞資訊。</span><span class="sxs-lookup"><span data-stu-id="d6aea-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="d6aea-128">儲存您的變更 (**Ctrl-O**， **Enter**) 和結束 hello 編輯器 (**Ctrl X**)。</span><span class="sxs-lookup"><span data-stu-id="d6aea-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="d6aea-129">建立 hello 範例</span><span class="sxs-lookup"><span data-stu-id="d6aea-129">Build hello sample</span></span>

<span data-ttu-id="d6aea-130">安裝 c hello hello Microsoft Azure IoT 裝置 SDK 的必要條件套件執行 hello 遵循 hello 覆盆子 Pi 中終端機的命令：</span><span class="sxs-lookup"><span data-stu-id="d6aea-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="d6aea-131">您現在可以在 hello 覆盆子 Pi 建置 hello 更新範例方案：</span><span class="sxs-lookup"><span data-stu-id="d6aea-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="d6aea-132">您現在可以在 hello 覆盆子 Pi 執行 hello 範例程式。</span><span class="sxs-lookup"><span data-stu-id="d6aea-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="d6aea-133">輸入 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="d6aea-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="d6aea-134">hello 下列範例輸出是您 hello 覆盆子 Pi hello 命令提示字元下，請參閱 hello 輸出的範例：</span><span class="sxs-lookup"><span data-stu-id="d6aea-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Raspberry Pi 應用程式的輸出][img-raspberry-output]

<span data-ttu-id="d6aea-136">按**CTRL-C** tooexit hello 程式在任何時間。</span><span class="sxs-lookup"><span data-stu-id="d6aea-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="d6aea-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6aea-137">Next steps</span></span>

<span data-ttu-id="d6aea-138">請瀏覽 hello [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)取得更多範例和 Azure IoT 文件。</span><span class="sxs-lookup"><span data-stu-id="d6aea-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
