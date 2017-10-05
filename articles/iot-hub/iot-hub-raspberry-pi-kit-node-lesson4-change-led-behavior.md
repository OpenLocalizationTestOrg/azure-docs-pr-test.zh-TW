---
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 4 課：修改應用程式 | Microsoft Docs"
description: "自訂訊息以變更 LED 的開啟與關閉行為。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "控制 raspberry pi 的 led, raspberry pi led 控制, raspberry pi 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b2ae23ac9cc1723936c4b4e1900b95cdcde744df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="eab2b-104">變更 LED 的開與關行為</span><span class="sxs-lookup"><span data-stu-id="eab2b-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="eab2b-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="eab2b-105">What you will do</span></span>
<span data-ttu-id="eab2b-106">自訂訊息以變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="eab2b-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="eab2b-107">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="eab2b-107">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eab2b-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="eab2b-108">What you will learn</span></span>
<span data-ttu-id="eab2b-109">使用其他 Node.js 函式以變更 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="eab2b-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eab2b-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="eab2b-110">What you need</span></span>
<span data-ttu-id="eab2b-111">您必須已成功完成[在 Raspberry Pi 上執行範例應用程式以接收雲端到裝置訊息](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="eab2b-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="eab2b-112">新增 Node.js 函式</span><span class="sxs-lookup"><span data-stu-id="eab2b-112">Add Node.js functions</span></span>
1. <span data-ttu-id="eab2b-113">執行下列命令，以在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="eab2b-113">Open the sample application in Visual Studio code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="eab2b-114">開啟 `app.js` 檔案，然後在結尾新增下列函式：</span><span class="sxs-lookup"><span data-stu-id="eab2b-114">Open the `app.js` file, and then add the following functions at the end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![具有所新增函式的 App.js 檔案](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="eab2b-116">在 `receiveMessageCallback` 函式中 switch-case 區塊的預設條件前面新增下列條件：</span><span class="sxs-lookup"><span data-stu-id="eab2b-116">Add the following conditions before the default one in the switch-case block of the `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="eab2b-117">現在，您已設定範例應用程式，透過訊息來回應其他指示。</span><span class="sxs-lookup"><span data-stu-id="eab2b-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="eab2b-118">"on" 指示會開啟 LED，"off" 指示則會關閉 LED。</span><span class="sxs-lookup"><span data-stu-id="eab2b-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="eab2b-119">開啟 gulpfile.js 檔案，然後在 `sendMessage` 函式前面新增新的函式：</span><span class="sxs-lookup"><span data-stu-id="eab2b-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>
   
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
   
   ![具有所新增函式的 Gulpfile.js 檔案](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. <span data-ttu-id="eab2b-121">在 `sendMessage` 函式中，將 `var message = buildMessage(sentMessageCount);` 這行取代為下列片段中所顯示的新行：</span><span class="sxs-lookup"><span data-stu-id="eab2b-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="eab2b-122">儲存所有變更。</span><span class="sxs-lookup"><span data-stu-id="eab2b-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="eab2b-123">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="eab2b-123">Deploy and run the sample application</span></span>
<span data-ttu-id="eab2b-124">執行下列命令，以在 Pi 上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="eab2b-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="eab2b-125">您應該會看到 LED 開啟兩秒，然後再關閉兩秒。</span><span class="sxs-lookup"><span data-stu-id="eab2b-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="eab2b-126">最後一個 "stop" 訊息會停止執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="eab2b-126">The last "stop" message stops the sample application from running.</span></span>

![具有開啟和關閉訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="eab2b-128">恭喜！</span><span class="sxs-lookup"><span data-stu-id="eab2b-128">Congratulations!</span></span> <span data-ttu-id="eab2b-129">您已成功自訂從 IoT 中樞傳送至 Pi 的訊息。</span><span class="sxs-lookup"><span data-stu-id="eab2b-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="eab2b-130">摘要</span><span class="sxs-lookup"><span data-stu-id="eab2b-130">Summary</span></span>
<span data-ttu-id="eab2b-131">此選讀小節示範如何自訂訊息，讓範例應用程式可以使用不同的方式控制 LED 的開與關行為。</span><span class="sxs-lookup"><span data-stu-id="eab2b-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

