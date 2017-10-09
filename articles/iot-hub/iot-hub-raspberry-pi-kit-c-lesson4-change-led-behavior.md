---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 4 課： 修改應用程式 |Microsoft 文件"
description: "自訂 hello 訊息 toochange hello LED 的開啟和關閉行為。"
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
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="c4ee4-104">變更 hello 開啟和關閉 hello LED 的行為</span><span class="sxs-lookup"><span data-stu-id="c4ee4-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c4ee4-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="c4ee4-105">What you will do</span></span>
<span data-ttu-id="c4ee4-106">自訂 hello 訊息 toochange hello LED 的開啟和關閉行為。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="c4ee4-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c4ee4-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="c4ee4-108">What you will learn</span></span>
<span data-ttu-id="c4ee4-109">使用 LED 的開啟和關閉行為額外的 Node.js 函式 toochange hello。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c4ee4-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="c4ee4-110">What you need</span></span>
<span data-ttu-id="c4ee4-111">您必須先成功完成[toodevice 訊息覆盆子 Pi tooreceive 雲端上執行範例應用程式](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud toodevice messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="c4ee4-112">新增函式 toomain.c 和 gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="c4ee4-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="c4ee4-113">開啟 Visual Studio 程式碼中的 hello 範例應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4ee4-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="c4ee4-114">開啟 hello`main.c`檔案，然後再加入下列函式 blinkLED() 函式後面的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4ee4-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="c4ee4-116">新增下列條件，其中一個 hello 預設 hello 中的 hello`if`區塊 hello`receiveMessageCallback`函式：</span><span class="sxs-lookup"><span data-stu-id="c4ee4-116">Add hello following conditions before hello default one in hello `if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="c4ee4-117">現在您已設定 hello 範例應用程式 toorespond toomore 指示訊息。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="c4ee4-118">「 開啟 」 指示的 hello 開啟 hello LED，並 「 關閉 」 指示的 hello 關閉 hello LED。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="c4ee4-119">開啟 hello gulpfile.js 檔案，然後加入新的函式 hello 函式前面`sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="c4ee4-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="c4ee4-121">在 hello`sendMessage`函式中，取代 hello 一行`var message = buildMessage(sentMessageCount);`與 hello 新行 hello 下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="c4ee4-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="c4ee4-122">儲存所有 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c4ee4-123">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="c4ee4-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="c4ee4-124">部署和執行 pi 的 hello 範例應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4ee4-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="c4ee4-125">您應該會看到 hello LED 開啟兩秒，，然後關閉另一個兩秒。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="c4ee4-126">hello 最後一個 「 停止 」 訊息就會停止執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-126">hello last "stop" message stops hello sample application from running.</span></span>

![具有開啟和關閉訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="c4ee4-128">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c4ee4-128">Congratulations!</span></span> <span data-ttu-id="c4ee4-129">您已成功自訂從 IoT 中樞 tooPi 傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="c4ee4-130">摘要</span><span class="sxs-lookup"><span data-stu-id="c4ee4-130">Summary</span></span>
<span data-ttu-id="c4ee4-131">此選用小節會示範如何 toocustomize 訊息以便 hello 範例應用程式可以控制 hello 開啟和關閉 hello LED 的行為不同的方式。</span><span class="sxs-lookup"><span data-stu-id="c4ee4-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>
