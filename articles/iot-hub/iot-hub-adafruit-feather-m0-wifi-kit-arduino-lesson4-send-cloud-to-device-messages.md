---
title: "Connect Arduino (C) tooAzure IoT-第 4 課： 雲端到裝置 |Microsoft 文件"
description: "範例應用程式會在 Adafruit Feather M0 WiFi 上執行，並監視從 IoT 中樞傳入的訊息。 新的 gulp 工作會從您的 IoT 中樞 tooblink hello LED 傳送訊息 tooAdafruit 羽毛 M0 WiFi。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "arduino 從 web 控制 led, arduino 透過 web 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="c0234-105">執行範例應用程式 tooreceive 雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="c0234-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="c0234-106">在本文中，您將在 Adafruit Feather M0 WiFi Arduino 面板上部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0234-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="c0234-107">hello 範例應用程式監視從 IoT 中樞的內送訊息。</span><span class="sxs-lookup"><span data-stu-id="c0234-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="c0234-108">您也 gulp 工作上執行您的電腦 toosend 訊息 tooyour Arduino 面板從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c0234-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="c0234-109">當 hello 範例應用程式收到 hello 訊息時，它會閃爍 hello LED。</span><span class="sxs-lookup"><span data-stu-id="c0234-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="c0234-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="c0234-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c0234-111">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="c0234-111">What you will do</span></span>
* <span data-ttu-id="c0234-112">連接 hello 範例應用程式 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c0234-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="c0234-113">部署和執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0234-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="c0234-114">從您 IoT 中樞 tooyour Arduino 面板 tooblink hello LED 傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="c0234-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c0234-115">學習目標</span><span class="sxs-lookup"><span data-stu-id="c0234-115">What you will learn</span></span>
<span data-ttu-id="c0234-116">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="c0234-116">In this article, you will learn:</span></span>
* <span data-ttu-id="c0234-117">如何 toomonitor 傳入訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c0234-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="c0234-118">如何從您的 IoT 中樞 tooyour Arduino 面板訊息 toosend 雲端到裝置。</span><span class="sxs-lookup"><span data-stu-id="c0234-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c0234-119">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="c0234-119">What you need</span></span>
* <span data-ttu-id="c0234-120">已設定並可供使用的 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="c0234-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="c0234-121">如何 tooset 向上 Arduino 面板，請參閱的 toolearn[設定您的裝置][configure-your-device]。</span><span class="sxs-lookup"><span data-stu-id="c0234-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="c0234-122">在您的 Azure 訂用帳戶中建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c0234-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="c0234-123">toolearn 如何 toocreate IoT 中樞，請參閱[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]。</span><span class="sxs-lookup"><span data-stu-id="c0234-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="c0234-124">連接 hello 範例應用程式 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="c0234-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="c0234-125">請確定您是在 hello 儲存機制資料夾`iot-hub-c-feather-m0-getting-started`。</span><span class="sxs-lookup"><span data-stu-id="c0234-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="c0234-126">開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0234-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="c0234-127">請注意 hello`app.ino`檔案在 hello`app`子資料夾。</span><span class="sxs-lookup"><span data-stu-id="c0234-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="c0234-128">hello`app.ino`檔案是 hello 金鑰來源檔案，其中包含從 hello IoT 中樞的 hello 碼 toomonitor 內送訊息。</span><span class="sxs-lookup"><span data-stu-id="c0234-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="c0234-129">hello`blinkLED`函式會閃爍 hello LED。</span><span class="sxs-lookup"><span data-stu-id="c0234-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Hello 範例應用程式中的儲存機制結構][repo-structure]

2. <span data-ttu-id="c0234-131">取得 hello hello 裝置探索 cli hello 裝置的序列通訊埠：</span><span class="sxs-lookup"><span data-stu-id="c0234-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="c0234-132">您應該看到的類似 toohello 下列輸出，並尋找 Arduino 面板 hello usb COM 連接埠：</span><span class="sxs-lookup"><span data-stu-id="c0234-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![裝置探索][device-discovery]

3. <span data-ttu-id="c0234-134">開啟 hello 檔案`config.json`hello 課程資料夾，然後輸入的 hello hello 找到 COM 連接埠號碼值中：</span><span class="sxs-lookup"><span data-stu-id="c0234-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="c0234-136">Hello COM 連接埠，Windows 平台上，它有 hello 格式`COM1, COM2, ...`。</span><span class="sxs-lookup"><span data-stu-id="c0234-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="c0234-137">在 macOS 或 Ubuntu 上，它將以 `/dev/` 做為開頭。</span><span class="sxs-lookup"><span data-stu-id="c0234-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="c0234-138">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="c0234-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="c0234-139">請遵循取代 hello hello`config-arduino.json`檔案：</span><span class="sxs-lookup"><span data-stu-id="c0234-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="c0234-140">如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]此電腦上所有的 hello 組態繼承的因此您可以略過部署的 hello 步驟 toohello 工作和執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0234-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="c0234-141">如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]不同電腦上，您需要在 hello tooreplace hello 預留位置`config-arduino.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="c0234-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="c0234-142">hello`config-arduino.json`檔案是在主資料夾 hello 子資料夾。</span><span class="sxs-lookup"><span data-stu-id="c0234-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Hello config arduino.json 檔案的內容][config-arduino-json]

   * <span data-ttu-id="c0234-144">取代**[Wi-fi SSID]**具有連接 toohello 網際網路您 Wi-fi SSID。</span><span class="sxs-lookup"><span data-stu-id="c0234-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="c0234-145">以 Wi-Fi 密碼取代 **[Wi-Fi password]**。</span><span class="sxs-lookup"><span data-stu-id="c0234-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="c0234-146">如果您 Wi-fi 不需要密碼，請移除 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="c0234-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="c0234-147">取代**[IoT 裝置連接字串]** hello 裝置連接字串，您會得到執行 hello`az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`命令。</span><span class="sxs-lookup"><span data-stu-id="c0234-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="c0234-148">取代**[IoT 中樞連接字串]**以 hello IoT 中樞連接字串，您會得到執行 hello`az iot hub show-connection-string --name {my hub name}`命令。</span><span class="sxs-lookup"><span data-stu-id="c0234-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c0234-149">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="c0234-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="c0234-150">部署和執行 hello 範例應用程式 Arduino 面板上，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0234-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="c0234-151">hello gulp 命令會將部署 hello 範例應用程式 tooyour Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="c0234-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="c0234-152">然後，它 hello 應用程式上執行 Arduino 面板和您的主機上的個別工作電腦 toosend 20 閃爍訊息 tooyour Arduino 面板從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c0234-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="c0234-153">Hello 範例應用程式執行之後，它會啟動接聽 toomessages 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c0234-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="c0234-154">同時，hello gulp 工作會從您的 IoT 中樞 tooyour Arduino 面板中，傳送"閃爍 」 的數個訊息。</span><span class="sxs-lookup"><span data-stu-id="c0234-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="c0234-155">Hello 範例應用程式的每個 hello 面板的閃爍訊息接收時，呼叫 hello`blinkLED`函式 tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="c0234-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="c0234-156">您應該會看見 hello LED 閃爍每隔兩秒鐘，因為 hello gulp 工作會從您的 IoT 中樞 tooyour Arduino 面板傳送 20 則訊息。</span><span class="sxs-lookup"><span data-stu-id="c0234-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="c0234-157">hello 上次是停止 hello 應用程式無法執行 「 停止 」 訊息。</span><span class="sxs-lookup"><span data-stu-id="c0234-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![具有 gulp 命令和閃爍訊息的範例應用程式][sample-application]

## <a name="summary"></a><span data-ttu-id="c0234-159">摘要</span><span class="sxs-lookup"><span data-stu-id="c0234-159">Summary</span></span>
<span data-ttu-id="c0234-160">您已成功傳送訊息，從您 IoT 中樞 tooyour Arduino 面板 tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="c0234-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="c0234-161">是選擇性的 hello 下一項工作： 變更 hello 開啟和關閉 hello LED 的行為。</span><span class="sxs-lookup"><span data-stu-id="c0234-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0234-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0234-162">Next steps</span></span>
<span data-ttu-id="c0234-163">[變更 hello 開啟和關閉 hello LED 的行為][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="c0234-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md