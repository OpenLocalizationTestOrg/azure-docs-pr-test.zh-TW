---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 4 課：讓 LED 閃爍 | Microsoft Docs"
description: "自訂訊息以變更 LED 的開與關行為。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "使用 arduino 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa99050dad62534e2825e93f1170d2f3ecf5a3ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="b1fe8-104">變更 LED 的開與關行為</span><span class="sxs-lookup"><span data-stu-id="b1fe8-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b1fe8-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b1fe8-105">What you will do</span></span>
<span data-ttu-id="b1fe8-106">自訂訊息以變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="b1fe8-107">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b1fe8-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="b1fe8-108">What you will learn</span></span>
<span data-ttu-id="b1fe8-109">使用其他函式變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-109">Use additional functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b1fe8-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b1fe8-110">What you need</span></span>
<span data-ttu-id="b1fe8-111">您必須已成功完成[在 Intel Edison 上執行範例應用程式以接收雲端到裝置訊息][receive-cloud-to-device-messages]。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-appjs-and-gulpfilejs"></a><span data-ttu-id="b1fe8-112">在 app.js 和 gulpfile.js 中新增函式</span><span class="sxs-lookup"><span data-stu-id="b1fe8-112">Add functions to app.js and gulpfile.js</span></span>
1. <span data-ttu-id="b1fe8-113">執行下列命令，以在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="b1fe8-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="b1fe8-114">開啟 `app.js` 檔案，然後在 blinkLED() 函式後新增下列函式：</span><span class="sxs-lookup"><span data-stu-id="b1fe8-114">Open the `app.js` file, and then add the following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![具有所新增函式的 App.js 檔案](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="b1fe8-116">在 `receiveMessageCallback` 函式中 switch-case 區塊的 'blink' 案例前面新增下列條件：</span><span class="sxs-lookup"><span data-stu-id="b1fe8-116">Add the following conditions before the 'blink' case in the switch-case block of the `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="b1fe8-117">現在，您已設定範例應用程式，透過訊息來回應其他指示。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="b1fe8-118">"on" 指示會開啟 LED，"off" 指示則會關閉 LED。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="b1fe8-119">開啟 gulpfile.js 檔案，然後在 `sendMessage` 函式前面新增新的函式：</span><span class="sxs-lookup"><span data-stu-id="b1fe8-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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

   ![具有所新增函式的 Gulpfile.js 檔案][gulpfile]
5. <span data-ttu-id="b1fe8-121">在 `sendMessage` 函式中，將 `var message = buildMessage(sentMessageCount);` 這行取代為下列片段中所顯示的新行：</span><span class="sxs-lookup"><span data-stu-id="b1fe8-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="b1fe8-122">儲存所有變更。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="b1fe8-123">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b1fe8-123">Deploy and run the sample application</span></span>
<span data-ttu-id="b1fe8-124">執行下列命令，在 Edison 上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="b1fe8-124">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="b1fe8-125">您應該會看到 LED 開啟兩秒，然後再關閉兩秒。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="b1fe8-126">最後一個 "stop" 訊息會停止執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-126">The last "stop" message stops the sample application from running.</span></span>

![on 和 off][on-and-off]

<span data-ttu-id="b1fe8-128">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b1fe8-128">Congratulations!</span></span> <span data-ttu-id="b1fe8-129">您已成功自訂從 IoT 中樞傳送至 Edison 的訊息。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="b1fe8-130">摘要</span><span class="sxs-lookup"><span data-stu-id="b1fe8-130">Summary</span></span>
<span data-ttu-id="b1fe8-131">此選讀小節示範如何自訂訊息，讓範例應用程式可以使用不同的方式控制 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="b1fe8-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
