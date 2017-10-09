---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 4 課： 接收訊息 |Microsoft 文件"
description: "範例應用程式會在 Edison 上執行，並監視來自 IoT 中樞的傳入訊息。 新的 gulp 工作會從您的 IoT 中樞 tooblink hello LED 傳送訊息 tooEdison。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "arduino 從 web 控制 led, arduino 透過 web 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>執行範例應用程式 tooreceive 雲端到裝置訊息
在本文中，您將在 Intel Edison 上部署範例應用程式。 hello 範例應用程式監視從 IoT 中樞的內送訊息。 您也 gulp 工作上執行您的電腦 toosend 訊息 tooEdison 從 IoT 中樞。 當 hello 範例應用程式收到 hello 訊息時，它會閃爍 hello LED。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-do"></a>將執行的作業
* 連接 hello 範例應用程式 tooyour IoT 中樞。
* 部署和執行 hello 範例應用程式。
* 從您 IoT 中樞 tooEdison tooblink hello LED 傳送訊息。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何 toomonitor 傳入訊息從 IoT 中樞。
* 如何從您的 IoT 中樞 tooEdison 訊息 toosend 雲端到裝置。

## <a name="what-you-need"></a>您需要什麼
* Intel Edison，進行設定以供使用。 如何 tooset 向上 Edison，請參閱的 toolearn[設定您的裝置][configure-your-device]。
* 在您的 Azure 訂用帳戶中建立的 IoT 中樞。 toolearn 如何 toocreate IoT 中樞，請參閱[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]。

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>連接 hello 範例應用程式 tooyour IoT 中樞
1. 請確定您是在 hello 儲存機制資料夾`iot-hub-node-edison-getting-started`。 開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:

   ```bash
   cd Lesson4
   code .
   ```

   hello 檔案在 hello`app`子資料夾會包含從 hello IoT 中樞的 hello 碼 toomonitor 內送訊息的 hello 索引鍵的原始程式檔。 hello`blinkLED`函式會閃爍 hello LED。

   ![Hello 範例應用程式中的儲存機制結構][repo-structure]
2. 藉由執行下列命令的 hello 初始化 hello 設定檔：

   ```bash
   npm install
   gulp init
   ```

   如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]此電腦上所有的 hello 組態繼承的因此您可以略過部署的 hello 步驟 toohello 工作和執行 hello 範例應用程式。 如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]不同電腦上，您需要在 hello tooreplace hello 預留位置`config-edison.json`檔案。 hello`config-edison.json`檔案是在主資料夾 hello 子資料夾。

   ![Hello config edison.json 檔案的內容](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * 取代**[裝置的主機名稱或 IP 位址]** hello 裝置的 IP 位址設定您的裝置時關閉標記。
   * 取代**[IoT 裝置連接字串]** hello 裝置連接字串，您會得到執行 hello`az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`命令。
   * 取代**[IoT 中樞連接字串]**以 hello IoT 中樞連接字串，您會得到執行 hello`az iot hub show-connection-string --name {my hub name}`命令。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行下列命令的 hello Edison 執行 hello 範例應用程式：

```bash
gulp deploy && gulp run
```

hello gulp 命令會將部署 hello 範例應用程式 tooEdison。 然後，它 hello 應用程式上執行 Edison 和您的主機上的個別工作電腦 toosend 20 閃爍訊息 tooEdison 從 IoT 中樞。

Hello 範例應用程式執行之後，它會啟動接聽 toomessages 從 IoT 中樞。 同時，hello gulp 工作會從您的 IoT 中樞 tooEdison 傳送"閃爍 」 的數個訊息。 每個閃爍訊息 Edison 接收 hello 範例應用程式呼叫 hello`blinkLED`函式 tooblink hello LED。

您應該會看到的 gulp 工作傳送 20 則訊息從您的 IoT 中樞 tooEdison hello LED 閃爍 hello 為每隔兩秒鐘。 hello 上次是停止 hello 應用程式無法執行 「 停止 」 訊息。

![具有 gulp 命令和閃爍訊息的範例應用程式][gulp-command-and-blink-messages]

## <a name="summary"></a>摘要
您已成功傳送訊息，從您 IoT 中樞 tooEdison tooblink hello LED。 是選擇性的 hello 下一項工作： 變更 hello 開啟和關閉 hello LED 的行為。

## <a name="next-steps"></a>後續步驟
[變更 hello 開啟和關閉 hello LED 的行為][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md