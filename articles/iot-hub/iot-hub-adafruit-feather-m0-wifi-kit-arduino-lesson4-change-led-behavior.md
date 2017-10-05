---
title: "將 Arduino (C) 連接到 Azure IoT - 第 4 課：修改應用程式 | Microsoft Docs"
description: "自訂訊息以變更 LED 的開啟與關閉行為。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "使用 arduino 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5009a0466f2c5689b8ab426049f4c4f02272512b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="77cc9-104">變更 LED 的開與關行為</span><span class="sxs-lookup"><span data-stu-id="77cc9-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="77cc9-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="77cc9-105">What you will do</span></span>
<span data-ttu-id="77cc9-106">自訂訊息以變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="77cc9-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="77cc9-107">如果您有任何問題，請在 Adafruit Feather M0 WiFi Arduino 面版的[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="77cc9-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="77cc9-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="77cc9-108">What you will learn</span></span>
<span data-ttu-id="77cc9-109">使用其他 Arduino 函式以變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="77cc9-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="77cc9-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="77cc9-110">What you need</span></span>
<span data-ttu-id="77cc9-111">您必須已成功完成[在 Arduino 面板上執行範例應用程式以接收雲端到裝置訊息][receive-cloud-to-device-messages]。</span><span class="sxs-lookup"><span data-stu-id="77cc9-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="77cc9-112">在 main.c 和 gulpfile.js 中新增函式</span><span class="sxs-lookup"><span data-stu-id="77cc9-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="77cc9-113">執行下列命令，以在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="77cc9-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="77cc9-114">開啟 `app.ino` 檔案，然後在 blinkLED() 函式後新增下列函式：</span><span class="sxs-lookup"><span data-stu-id="77cc9-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![具有所新增函式的 app.ino 檔案][app-ino-file]
3. <span data-ttu-id="77cc9-116">在 `receiveMessageCallback` 函式的 `else if` 區塊前新增下列條件：</span><span class="sxs-lookup"><span data-stu-id="77cc9-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="77cc9-117">現在，您已設定範例應用程式，透過訊息來回應其他指示。</span><span class="sxs-lookup"><span data-stu-id="77cc9-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="77cc9-118">"on" 指示會開啟 LED，"off" 指示則會關閉 LED。</span><span class="sxs-lookup"><span data-stu-id="77cc9-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="77cc9-119">開啟 gulpfile.js 檔案，然後在 `sendMessage` 函式前面新增新的函式：</span><span class="sxs-lookup"><span data-stu-id="77cc9-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![具有所新增函式的 Gulpfile.js 檔案][gulp-file-js]
5. <span data-ttu-id="77cc9-121">在 `sendMessage` 函式中，將 `var message = buildMessage(sentMessageCount);` 這行取代為下列片段中所顯示的新行：</span><span class="sxs-lookup"><span data-stu-id="77cc9-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="77cc9-122">儲存所有變更。</span><span class="sxs-lookup"><span data-stu-id="77cc9-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="77cc9-123">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="77cc9-123">Deploy and run the sample application</span></span>
<span data-ttu-id="77cc9-124">執行下列命令，以在 Arduino 面板上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="77cc9-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="77cc9-125">您應該會看到 LED 開啟兩秒，然後再關閉兩秒。</span><span class="sxs-lookup"><span data-stu-id="77cc9-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="77cc9-126">最後一個 "stop" 訊息會停止執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="77cc9-126">The last "stop" message stops the sample application from running.</span></span>

![on 和 off][on-and-off]

<span data-ttu-id="77cc9-128">恭喜！</span><span class="sxs-lookup"><span data-stu-id="77cc9-128">Congratulations!</span></span> <span data-ttu-id="77cc9-129">您已成功自訂從 IoT 中樞傳送至 Arduino 面板的訊息。</span><span class="sxs-lookup"><span data-stu-id="77cc9-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="77cc9-130">摘要</span><span class="sxs-lookup"><span data-stu-id="77cc9-130">Summary</span></span>
<span data-ttu-id="77cc9-131">此選讀小節示範如何自訂訊息，讓範例應用程式可以使用不同的方式控制 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="77cc9-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png