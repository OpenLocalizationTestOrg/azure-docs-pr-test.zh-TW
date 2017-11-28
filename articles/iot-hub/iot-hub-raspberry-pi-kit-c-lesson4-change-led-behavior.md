---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 第 4 課：修改應用程式 | Microsoft Docs"
description: "自訂訊息以變更 LED 的開與關行為。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "控制 raspberry pi 的 led, raspberry pi led 控制, raspberry pi 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b1e441b20e161f4a03d4c2c300b21aca4fedb2a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="9122f-104">變更 LED 的開與關行為</span><span class="sxs-lookup"><span data-stu-id="9122f-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9122f-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="9122f-105">What you will do</span></span>
<span data-ttu-id="9122f-106">自訂訊息以變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="9122f-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="9122f-107">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="9122f-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9122f-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="9122f-108">What you will learn</span></span>
<span data-ttu-id="9122f-109">使用其他 Node.js 函式以變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="9122f-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9122f-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="9122f-110">What you need</span></span>
<span data-ttu-id="9122f-111">您必須已成功完成[在 Raspberry Pi 上執行範例應用程式以接收雲端到裝置訊息](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="9122f-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud to device messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="9122f-112">在 main.c 和 gulpfile.js 中新增函式</span><span class="sxs-lookup"><span data-stu-id="9122f-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="9122f-113">執行下列命令，以在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="9122f-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="9122f-114">開啟 `main.c` 檔案，然後在 blinkLED() 函式後新增下列函式：</span><span class="sxs-lookup"><span data-stu-id="9122f-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![已新增函式的 main.c 檔案](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. <span data-ttu-id="9122f-116">在 `receiveMessageCallback` 函式的 `if` 區塊中，於預覽條件前面新增下列條件：</span><span class="sxs-lookup"><span data-stu-id="9122f-116">Add the following conditions before the default one in the `if` block of the `receiveMessageCallback` function:</span></span>

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="9122f-117">現在，您已設定範例應用程式，透過訊息來回應其他指示。</span><span class="sxs-lookup"><span data-stu-id="9122f-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="9122f-118">"on" 指示會開啟 LED，"off" 指示則會關閉 LED。</span><span class="sxs-lookup"><span data-stu-id="9122f-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="9122f-119">開啟 gulpfile.js 檔案，然後在 `sendMessage` 函式前面新增新的函式：</span><span class="sxs-lookup"><span data-stu-id="9122f-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![具有所新增函式的 Gulpfile.js 檔案](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. <span data-ttu-id="9122f-121">在 `sendMessage` 函式中，將 `var message = buildMessage(sentMessageCount);` 這行取代為下列片段中所顯示的新行：</span><span class="sxs-lookup"><span data-stu-id="9122f-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="9122f-122">儲存所有變更。</span><span class="sxs-lookup"><span data-stu-id="9122f-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="9122f-123">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="9122f-123">Deploy and run the sample application</span></span>
<span data-ttu-id="9122f-124">執行下列命令，以在 Pi 上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="9122f-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="9122f-125">您應該會看到 LED 開啟兩秒，然後再關閉兩秒。</span><span class="sxs-lookup"><span data-stu-id="9122f-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="9122f-126">最後一個 "stop" 訊息會停止執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="9122f-126">The last "stop" message stops the sample application from running.</span></span>

![具有開啟和關閉訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="9122f-128">恭喜！</span><span class="sxs-lookup"><span data-stu-id="9122f-128">Congratulations!</span></span> <span data-ttu-id="9122f-129">您已成功自訂從 IoT 中樞傳送至 Pi 的訊息。</span><span class="sxs-lookup"><span data-stu-id="9122f-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="9122f-130">摘要</span><span class="sxs-lookup"><span data-stu-id="9122f-130">Summary</span></span>
<span data-ttu-id="9122f-131">此選讀小節示範如何自訂訊息，讓範例應用程式可以使用不同的方式控制 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="9122f-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>
