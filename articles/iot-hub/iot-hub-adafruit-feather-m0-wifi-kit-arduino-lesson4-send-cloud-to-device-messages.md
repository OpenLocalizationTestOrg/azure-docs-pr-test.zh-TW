---
title: "將 Arduino (C) 連接到 Azure IoT - 第 4 課：雲端到裝置 | Microsoft Docs"
description: "範例應用程式會在 Adafruit Feather M0 WiFi 上執行，並監視從 IoT 中樞傳入的訊息。 新的 Gulp 工作會從 IoT 中樞將訊息傳送到 Adafruit Feather M0 WiFi 來使 LED 閃爍。"
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
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="a0942-105">執行範例應用程式以接收雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="a0942-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="a0942-106">在本文中，您將在 Adafruit Feather M0 WiFi Arduino 面板上部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0942-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="a0942-107">範例應用程式會監視來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="a0942-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="a0942-108">您也會在電腦上執行 Gulp 工作，以從 IoT 中樞將訊息傳送到 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="a0942-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="a0942-109">當範例應用程式收到訊息時，便會使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="a0942-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="a0942-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="a0942-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a0942-111">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="a0942-111">What you will do</span></span>
* <span data-ttu-id="a0942-112">將範例應用程式連接到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a0942-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="a0942-113">部署並執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0942-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="a0942-114">從 IoT 中樞將訊息傳送到 Arduino 面板來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="a0942-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a0942-115">學習目標</span><span class="sxs-lookup"><span data-stu-id="a0942-115">What you will learn</span></span>
<span data-ttu-id="a0942-116">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="a0942-116">In this article, you will learn:</span></span>
* <span data-ttu-id="a0942-117">如何監視來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="a0942-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="a0942-118">現在，您可以從 IoT 中樞將雲端到裝置訊息傳送至 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="a0942-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a0942-119">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="a0942-119">What you need</span></span>
* <span data-ttu-id="a0942-120">已設定並可供使用的 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="a0942-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="a0942-121">若要了解如何設定 Arduino 面板，請參閱[設定裝置][configure-your-device]。</span><span class="sxs-lookup"><span data-stu-id="a0942-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="a0942-122">在您的 Azure 訂用帳戶中建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a0942-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="a0942-123">若要了解如何建立 IoT 中樞，請參閱[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]。</span><span class="sxs-lookup"><span data-stu-id="a0942-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="a0942-124">將範例應用程式連接到 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="a0942-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="a0942-125">請確定您已位於存放庫資料夾 `iot-hub-c-feather-m0-getting-started`。</span><span class="sxs-lookup"><span data-stu-id="a0942-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="a0942-126">執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="a0942-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="a0942-127">請注意到 `app` 子資料夾中的 `app.ino` 檔案。</span><span class="sxs-lookup"><span data-stu-id="a0942-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="a0942-128">`app.ino` 檔案為關鍵的來源檔案，這個來源檔案包含監視來自 IoT 中樞之傳入訊息的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a0942-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="a0942-129">`blinkLED` 函數會使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="a0942-129">The `blinkLED` function blinks the LED.</span></span>

   ![範例應用程式中的儲存機制結構][repo-structure]

2. <span data-ttu-id="a0942-131">透過裝置探索 cli 取得裝置的序列連接埠︰</span><span class="sxs-lookup"><span data-stu-id="a0942-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="a0942-132">您應該會看到類似下列的輸出，並找到 Arduino 面板的 usb COM 連接埠︰</span><span class="sxs-lookup"><span data-stu-id="a0942-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![裝置探索][device-discovery]

3. <span data-ttu-id="a0942-134">開啟課程資料夾中的 `config.json` 檔案並輸入找到的 COM 連接埠號碼值︰</span><span class="sxs-lookup"><span data-stu-id="a0942-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="a0942-136">針對 COM 連接埠，它在 Windows 平台上的格式為 `COM1, COM2, ...`。</span><span class="sxs-lookup"><span data-stu-id="a0942-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="a0942-137">在 macOS 或 Ubuntu 上，它將以 `/dev/` 做為開頭。</span><span class="sxs-lookup"><span data-stu-id="a0942-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="a0942-138">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="a0942-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="a0942-139">在 `config-arduino.json` 檔案中進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="a0942-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="a0942-140">如果您已在此電腦上完成[建立 Azure 函數應用程式與儲存體帳戶][create-an-azure-function-app-and-storage-account]中的步驟，則會繼承所有組態，因此您可以略過部署和執行範例應用程式之工作的步驟。</span><span class="sxs-lookup"><span data-stu-id="a0942-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="a0942-141">如果您是在不同電腦上完成[建立 Azure 函數應用程式與儲存體帳戶][create-an-azure-function-app-and-storage-account]中的步驟，您必須取代 `config-arduino.json` 檔案中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="a0942-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="a0942-142">`config-arduino.json` 檔案位於您主資料夾的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a0942-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![config-arduino.json 檔案的內容][config-arduino-json]

   * <span data-ttu-id="a0942-144">以連線至網際網路的 Wi-Fi SSID 取代 **[Wi-Fi SSID]**。</span><span class="sxs-lookup"><span data-stu-id="a0942-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="a0942-145">以 Wi-Fi 密碼取代 **[Wi-Fi password]**。</span><span class="sxs-lookup"><span data-stu-id="a0942-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="a0942-146">如果 Wi-Fi 不需要密碼，請移除字串。</span><span class="sxs-lookup"><span data-stu-id="a0942-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="a0942-147">以透過執行 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 命令所取得的裝置連接字串取代 **[IoT device connection string]**。</span><span class="sxs-lookup"><span data-stu-id="a0942-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="a0942-148">以透過執行 `az iot hub show-connection-string --name {my hub name}` 命令所取得的 IoT 中樞連接字串取代 **[IoT hub connection string]**。</span><span class="sxs-lookup"><span data-stu-id="a0942-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="a0942-149">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="a0942-149">Deploy and run the sample application</span></span>
<span data-ttu-id="a0942-150">執行下列命令，以在 Arduino 面板上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="a0942-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="a0942-151">gulp 命令會將範例應用程式部署到 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="a0942-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="a0942-152">然後，它會在 Arduino 面板上執行應用程式，並在主機電腦上執行個別的工作，以從 IoT 中樞將 20 個閃爍訊息傳送到 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="a0942-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="a0942-153">在範例應用程式執行後，它便會開始接聽來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="a0942-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="a0942-154">同時，Gulp 工作會從 IoT 中樞將數個「閃爍」訊息傳送到 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="a0942-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="a0942-155">每當面板收到閃爍訊息時，範例應用程式便會呼叫 `blinkLED` 函數來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="a0942-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="a0942-156">當 gulp 工作從 IoT 中樞將 20 個訊息傳送到 Arduino 面板時，LED 每兩秒應該會閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="a0942-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="a0942-157">最後將會有一個「停止」訊息，讓應用程式停止執行。</span><span class="sxs-lookup"><span data-stu-id="a0942-157">The last one is a "stop" message that stops the application from running.</span></span>

![具有 gulp 命令和閃爍訊息的範例應用程式][sample-application]

## <a name="summary"></a><span data-ttu-id="a0942-159">摘要</span><span class="sxs-lookup"><span data-stu-id="a0942-159">Summary</span></span>
<span data-ttu-id="a0942-160">您已成功從 IoT 中樞將訊息傳送到 Arduino 面板來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="a0942-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="a0942-161">下一個工作是「選讀：變更 LED 的開與關行為」。</span><span class="sxs-lookup"><span data-stu-id="a0942-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0942-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0942-162">Next steps</span></span>
<span data-ttu-id="a0942-163">[變更 LED 的開與關行為][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="a0942-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


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