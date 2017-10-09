---
title: "連接 Arduino tooAzure IoT-第 1 課： 將應用程式部署 |Microsoft 文件"
description: "複製 hello 範例 Arduino 應用程式從 GitHub，並執行此應用程式 tooyour Adafruit 羽毛 M0 WiFi gulp toodeploy。 此範例應用程式會閃爍 hello GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 專案, arduino led 閃爍, arduino led 閃爍程式碼, arduino 閃爍程式, arduino 閃爍範例"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="5b864-105">建立及部署 hello 閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="5b864-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5b864-106">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="5b864-106">What you will do</span></span>
<span data-ttu-id="5b864-107">複製 hello 範例 Arduino 應用程式從 GitHub，並使用 hello gulp 工具 toodeploy hello 範例應用程式 tooyour Adafruit 羽毛 M0 WiFi Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="5b864-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="5b864-108">hello 範例應用程式的閃爍 hello GPIO #13 上-barod LED 每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="5b864-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="5b864-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting-page]。</span><span class="sxs-lookup"><span data-stu-id="5b864-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5b864-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="5b864-110">What you will learn</span></span>
* <span data-ttu-id="5b864-111">如何 toodeploy 和執行的 hello 範例 Arduino 面板上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b864-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5b864-112">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="5b864-112">What you need</span></span>
<span data-ttu-id="5b864-113">您必須先成功完成下列作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b864-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="5b864-114">[設定裝置][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="5b864-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="5b864-115">[取得 hello 工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="5b864-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="5b864-116">開啟 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="5b864-116">Open hello sample application</span></span>
<span data-ttu-id="5b864-117">tooopen hello 範例應用程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b864-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="5b864-118">藉由執行下列命令的 hello 複製從 GitHub hello 範例儲存機制：</span><span class="sxs-lookup"><span data-stu-id="5b864-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="5b864-119">開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b864-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![儲存機制結構][repo-structure]

<span data-ttu-id="5b864-121">hello`app.ino`檔案在 hello`app`子資料夾是包含 hello 程式碼 toocontrol hello LED 的 hello 金鑰來源檔案。</span><span class="sxs-lookup"><span data-stu-id="5b864-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="5b864-122">安裝應用程式相依性</span><span class="sxs-lookup"><span data-stu-id="5b864-122">Install application dependencies</span></span>
<span data-ttu-id="5b864-123">安裝 hello 程式庫和其他您需要執行下列命令的 hello hello 範例應用程式的模組：</span><span class="sxs-lookup"><span data-stu-id="5b864-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="5b864-124">設定 hello 裝置連線</span><span class="sxs-lookup"><span data-stu-id="5b864-124">Configure hello device connection</span></span>
<span data-ttu-id="5b864-125">tooconfigure hello 裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b864-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="5b864-126">取得 hello hello 裝置探索 cli hello 裝置的序列通訊埠：</span><span class="sxs-lookup"><span data-stu-id="5b864-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="5b864-127">您應該看到的類似 toohello 下列輸出，並尋找 Arduino 面板 hello usb COM 連接埠：![裝置探索][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="5b864-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="5b864-128">開啟 hello 檔案`config.json`在 hello 課程資料夾並加入 hello 的 hello 找到 COM 連接埠號碼的值：</span><span class="sxs-lookup"><span data-stu-id="5b864-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="5b864-130">Hello COM 連接埠，Windows 平台上，它有 hello 格式`COM1, COM2, ...`。</span><span class="sxs-lookup"><span data-stu-id="5b864-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="5b864-131">在 macOS 或 Ubuntu 上，它是以 `/dev/` 開頭。</span><span class="sxs-lookup"><span data-stu-id="5b864-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="5b864-132">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="5b864-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="5b864-133">安裝所需的 hello 工具 Arduino 面板</span><span class="sxs-lookup"><span data-stu-id="5b864-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="5b864-134">安裝 hello Azure IoT 中樞 SDK Arduino 板執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b864-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="5b864-135">這項工作可能需要很長的時間 toocomplete，取決於您的網路連線。</span><span class="sxs-lookup"><span data-stu-id="5b864-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="5b864-136">請結束時執行的 gulp 工作執行 Arduino IDE 執行個體的 hello: `install-tools`， `run`。</span><span class="sxs-lookup"><span data-stu-id="5b864-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="5b864-137">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="5b864-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="5b864-138">部署和執行 hello 範例應用程式藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b864-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="5b864-139">確認 hello 應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="5b864-139">Verify hello app works</span></span>
<span data-ttu-id="5b864-140">如果您沒有看到 hello LED 閃爍不停，請參閱 hello[疑難排解指南][ troubleshooting-page]解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="5b864-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![LED 閃爍][led-blinking]

## <a name="summary"></a><span data-ttu-id="5b864-142">摘要</span><span class="sxs-lookup"><span data-stu-id="5b864-142">Summary</span></span>
<span data-ttu-id="5b864-143">您所需的 hello 工具 toowork 隨 Arduino 面板，並部署範例應用程式 tooyour Arduino 面板 tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="5b864-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="5b864-144">您現在可以建立、 部署和執行另一個連接您 Arduino 面板 tooAzure IoT 中樞 toosend 範例應用程式和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="5b864-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b864-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b864-145">Next steps</span></span>
<span data-ttu-id="5b864-146">[取得 hello Azure tools][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="5b864-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md