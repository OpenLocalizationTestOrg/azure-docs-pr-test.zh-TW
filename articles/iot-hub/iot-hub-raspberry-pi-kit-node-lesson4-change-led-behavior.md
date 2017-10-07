---
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 4 課： 修改應用程式 |Microsoft 文件"
description: "自訂 hello 訊息 toochange hello LED 的開啟和關閉行為。"
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
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="b30bb-104">變更 hello 開啟和關閉 hello LED 的行為</span><span class="sxs-lookup"><span data-stu-id="b30bb-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b30bb-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b30bb-105">What you will do</span></span>
<span data-ttu-id="b30bb-106">自訂 hello 訊息 toochange hello LED 的開啟和關閉行為。</span><span class="sxs-lookup"><span data-stu-id="b30bb-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="b30bb-107">如果您有任何問題，搜尋解決方案 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="b30bb-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b30bb-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="b30bb-108">What you will learn</span></span>
<span data-ttu-id="b30bb-109">使用 LED 的開啟和關閉行為額外的 Node.js 函式 toochange hello。</span><span class="sxs-lookup"><span data-stu-id="b30bb-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b30bb-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b30bb-110">What you need</span></span>
<span data-ttu-id="b30bb-111">您必須先成功完成[執行範例應用程式上覆盆子 Pi tooreceive 雲端到裝置訊息](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="b30bb-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="b30bb-112">新增 Node.js 函式</span><span class="sxs-lookup"><span data-stu-id="b30bb-112">Add Node.js functions</span></span>
1. <span data-ttu-id="b30bb-113">開啟 Visual Studio 程式碼中的 hello 範例應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b30bb-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="b30bb-114">開啟 hello`app.js`檔案，然後再新增 hello 遵循 hello 結尾的函式：</span><span class="sxs-lookup"><span data-stu-id="b30bb-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![具有所新增函式的 App.js 檔案](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="b30bb-116">新增下列條件，其中一個 hello 預設 hello hello 切換情況區塊中的 hello`receiveMessageCallback`函式：</span><span class="sxs-lookup"><span data-stu-id="b30bb-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="b30bb-117">現在您已設定 hello 範例應用程式 toorespond toomore 指示訊息。</span><span class="sxs-lookup"><span data-stu-id="b30bb-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="b30bb-118">「 開啟 」 指示的 hello 開啟 hello LED，並 「 關閉 」 指示的 hello 關閉 hello LED。</span><span class="sxs-lookup"><span data-stu-id="b30bb-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="b30bb-119">開啟 hello gulpfile.js 檔案，然後加入新的函式 hello 函式前面`sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="b30bb-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="b30bb-121">在 hello`sendMessage`函式中，取代 hello 一行`var message = buildMessage(sentMessageCount);`與 hello 新行 hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="b30bb-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="b30bb-122">儲存所有 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="b30bb-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="b30bb-123">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b30bb-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="b30bb-124">部署和執行 pi 的 hello 範例應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b30bb-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="b30bb-125">您應該會看到 hello LED 開啟兩秒，，然後關閉另一個兩秒。</span><span class="sxs-lookup"><span data-stu-id="b30bb-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="b30bb-126">hello 最後一個 「 停止 」 訊息就會停止執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b30bb-126">hello last "stop" message stops hello sample application from running.</span></span>

![具有開啟和關閉訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="b30bb-128">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b30bb-128">Congratulations!</span></span> <span data-ttu-id="b30bb-129">您已成功自訂從 IoT 中樞 tooPi 傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="b30bb-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="b30bb-130">摘要</span><span class="sxs-lookup"><span data-stu-id="b30bb-130">Summary</span></span>
<span data-ttu-id="b30bb-131">此選用小節會示範如何 toocustomize 訊息以便 hello 範例應用程式可以控制 hello 開啟和關閉 hello LED 的行為不同的方式。</span><span class="sxs-lookup"><span data-stu-id="b30bb-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

