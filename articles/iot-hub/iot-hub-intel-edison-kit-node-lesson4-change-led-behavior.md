---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 4 課： 閃爍 hello LED |Microsoft 文件"
description: "自訂 hello 訊息 toochange hello LED 的開啟和關閉行為。"
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
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>變更 hello 開啟和關閉 hello LED 的行為
## <a name="what-you-will-do"></a>將執行的作業
自訂 hello 訊息 toochange hello LED 的開啟和關閉行為。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-learn"></a>學習目標
使用其他函數 toochange hello LED 的開啟和關閉行為。

## <a name="what-you-need"></a>您需要什麼
您必須先成功完成[toodevice 訊息 Intel Edison tooreceive 雲端上執行範例應用程式][receive-cloud-to-device-messages]。

## <a name="add-functions-tooappjs-and-gulpfilejs"></a>新增函式 tooapp.js 和 gulpfile.js
1. 開啟 Visual Studio 程式碼中的 hello 範例應用程式，執行下列命令的 hello:

   ```bash
   cd Lesson4
   code .
   ```
2. 開啟 hello`app.js`檔案，然後再加入下列函式 blinkLED() 函式後面的 hello:

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![具有所新增函式的 App.js 檔案](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. 新增 hello 下列條件，hello 'blink' hello hello 切換情況區塊中的案例`receiveMessageCallback`函式：

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   現在您已設定 hello 範例應用程式 toorespond toomore 指示訊息。 「 開啟 」 指示的 hello 開啟 hello LED，並 「 關閉 」 指示的 hello 關閉 hello LED。
4. 開啟 hello gulpfile.js 檔案，然後加入新的函式 hello 函式前面`sendMessage`:

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
5. 在 hello`sendMessage`函式中，取代 hello 一行`var message = buildMessage(sentMessageCount);`與 hello 新行 hello 下列程式碼片段所示：

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. 儲存所有 hello 變更。

### <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行下列命令的 hello Edison 執行 hello 範例應用程式：

```bash
gulp deploy && gulp run
```

您應該會看到 hello LED 開啟兩秒，，然後關閉另一個兩秒。 hello 最後一個 「 停止 」 訊息就會停止執行 hello 範例應用程式。

![on 和 off][on-and-off]

恭喜！ 您已成功自訂從 IoT 中樞 tooEdison 傳送 hello 訊息。

### <a name="summary"></a>摘要
此選用小節會示範如何 toocustomize 訊息以便 hello 範例應用程式可以控制 hello 開啟和關閉 hello LED 的行為不同的方式。

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
