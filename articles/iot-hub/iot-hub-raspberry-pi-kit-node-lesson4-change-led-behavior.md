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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>變更 hello 開啟和關閉 hello LED 的行為
## <a name="what-you-will-do"></a>將執行的作業
自訂 hello 訊息 toochange hello LED 的開啟和關閉行為。 如果您有任何問題，搜尋解決方案 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標
使用 LED 的開啟和關閉行為額外的 Node.js 函式 toochange hello。

## <a name="what-you-need"></a>您需要什麼
您必須先成功完成[執行範例應用程式上覆盆子 Pi tooreceive 雲端到裝置訊息](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)。

## <a name="add-nodejs-functions"></a>新增 Node.js 函式
1. 開啟 Visual Studio 程式碼中的 hello 範例應用程式，執行下列命令的 hello:
   
   ```bash
   cd Lesson4
   code .
   ```
2. 開啟 hello`app.js`檔案，然後再新增 hello 遵循 hello 結尾的函式：
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![具有所新增函式的 App.js 檔案](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. 新增下列條件，其中一個 hello 預設 hello hello 切換情況區塊中的 hello`receiveMessageCallback`函式：
   
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
   
   ![具有所新增函式的 Gulpfile.js 檔案](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. 在 hello`sendMessage`函式中，取代 hello 一行`var message = buildMessage(sentMessageCount);`與 hello 新行 hello 下列程式碼片段所示：
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. 儲存所有 hello 變更。

### <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行 pi 的 hello 範例應用程式，執行下列命令的 hello:

```bash
gulp deploy && gulp run
```

您應該會看到 hello LED 開啟兩秒，，然後關閉另一個兩秒。 hello 最後一個 「 停止 」 訊息就會停止執行 hello 範例應用程式。

![具有開啟和關閉訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

恭喜！ 您已成功自訂從 IoT 中樞 tooPi 傳送 hello 訊息。

### <a name="summary"></a>摘要
此選用小節會示範如何 toocustomize 訊息以便 hello 範例應用程式可以控制 hello 開啟和關閉 hello LED 的行為不同的方式。

