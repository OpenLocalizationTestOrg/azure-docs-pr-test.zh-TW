---
featureFlags: usabilla
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 4 課： 雲端到裝置 |Microsoft 文件"
description: "hello 範例應用程式在 Pi 上執行，並監視從 IoT 中樞的內送訊息。 新的 gulp 工作會從您的 IoT 中樞 tooblink hello LED 傳送訊息 tooPi。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "雲端 toodevice，來自雲端的訊息"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>執行 hello 範例應用程式 tooreceive 雲端到裝置訊息
在本文中，您將在 Raspberry Pi 3 上部署範例應用程式。 hello 範例應用程式監視從 IoT 中樞的內送訊息。 您也 gulp 工作上執行您的電腦 toosend 訊息 tooPi 從 IoT 中樞。 當 hello 範例應用程式收到 hello 訊息時，它會閃爍 hello LED。 如果您有任何問題，搜尋解決方案 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。

## <a name="what-you-will-do"></a>將執行的作業
* 連接 hello 範例應用程式 tooyour IoT 中樞。
* 部署和執行 hello 範例應用程式。
* 從您 IoT 中樞 tooPi tooblink hello LED 傳送訊息。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 從您的 IoT 中樞 toomonitor 傳入訊息的方式
* 如何從您的 IoT 中樞 tooPi 訊息 toosend 雲端到裝置。

## <a name="what-you-need"></a>您需要什麼
* Raspberry Pi 3，以完成使用設定。 如何 tooset 向上 Pi，請參閱的 toolearn[設定您的裝置](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)。
* 在您的 Azure 訂用帳戶中建立的 IoT 中樞。 toolearn 如何 toocreate IoT 中樞，請參閱[建立 IoT 中樞，並註冊覆盆子 Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)。

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>連接 hello 範例應用程式 tooyour IoT 中樞
1. 請確定您是在 hello 儲存機制資料夾`iot-hub-node-raspberrypi-getting-started`。 開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   請注意 hello`app.js`檔案在 hello`app`子資料夾。 hello`app.js`檔案是 hello 金鑰來源檔案，其中包含從 hello IoT 中樞的 hello 碼 toomonitor 內送訊息。 hello`blinkLED`函式會閃爍 hello LED。
   
   ![Hello 範例應用程式中的儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. 使用下列命令的 hello 初始化 hello 設定檔：
   
   ```bash
   npm install
   gulp init
   ```
   
   如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)此電腦上所有的 hello 組態繼承的因此您可以略過部署和執行 hello 範例應用程式的 toohello 工作。 如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)不同電腦上，您需要在 hello tooreplace hello 預留位置`config-raspberrypi.json`檔案。 hello`config-raspberrypi.json`檔案是在主資料夾 hello 子資料夾。
   
   ![Hello config raspberrypi.json 檔案的內容](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* 取代**[裝置的主機名稱或 IP 位址]** Pi 或 hello 主機名稱，您會得到執行 hello hello IP 位址與`devdisco list --eth`命令。
* 取代**[IoT 裝置連接字串]** hello 裝置連接字串，您會得到執行 hello`az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`命令。
* 取代**[IoT 中樞連接字串]**以 hello IoT 中樞連接字串，您會得到執行 hello`az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`命令。

> [!NOTE]
> 也請執行 **gulp install-tools** (如果您未在第 1 課這麼做)。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行 pi 的 hello 範例應用程式，執行下列命令的 hello:

```bash
gulp deploy && gulp run
```

hello 命令會將部署 hello 範例應用程式 tooPi。 然後，它 hello 應用程式上執行 Pi 和您的主機上的個別工作電腦 toosend 20 閃爍訊息 tooPi 從 IoT 中樞。

Hello 範例應用程式執行之後，它會啟動接聽 toomessages 從 IoT 中樞。 同時，hello gulp 工作會從您的 IoT 中樞 tooPi 傳送"閃爍 」 的數個訊息。 每個閃爍訊息接收 Pi hello 範例應用程式呼叫 hello`blinkLED`函式 tooblink hello LED。

您應該會看到的 gulp 工作傳送 20 則訊息從您的 IoT 中樞 tooPi hello LED 閃爍 hello 為每隔兩秒鐘。 hello 最後是 「 停止 」 的訊息，告知 hello 應用程式 toostop 執行。

![具有 gulp 命令和閃爍訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>摘要
您已成功傳送訊息，從您 IoT 中樞 tooPi tooblink hello LED。 是選擇性的 hello 下一項工作： 變更 hello 開啟和關閉 hello LED 的行為。

## <a name="next-steps"></a>後續步驟
[變更 hello 開啟和關閉 hello LED 的行為](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

