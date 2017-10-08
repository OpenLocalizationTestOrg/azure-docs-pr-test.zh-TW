---
title: "Connect Arduino (C) tooAzure IoT-第 4 課： 雲端到裝置 |Microsoft 文件"
description: "範例應用程式會在 Adafruit Feather M0 WiFi 上執行，並監視從 IoT 中樞傳入的訊息。 新的 gulp 工作會從您的 IoT 中樞 tooblink hello LED 傳送訊息 tooAdafruit 羽毛 M0 WiFi。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "arduino 從 web 控制 led, arduino 透過 web 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>執行範例應用程式 tooreceive 雲端到裝置訊息
在本文中，您將在 Adafruit Feather M0 WiFi Arduino 面板上部署範例應用程式。

hello 範例應用程式監視從 IoT 中樞的內送訊息。 您也 gulp 工作上執行您的電腦 toosend 訊息 tooyour Arduino 面板從 IoT 中樞。 當 hello 範例應用程式收到 hello 訊息時，它會閃爍 hello LED。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-do"></a>將執行的作業
* 連接 hello 範例應用程式 tooyour IoT 中樞。
* 部署和執行 hello 範例應用程式。
* 從您 IoT 中樞 tooyour Arduino 面板 tooblink hello LED 傳送訊息。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何 toomonitor 傳入訊息從 IoT 中樞。
* 如何從您的 IoT 中樞 tooyour Arduino 面板訊息 toosend 雲端到裝置。

## <a name="what-you-need"></a>您需要什麼
* 已設定並可供使用的 Arduino 面板。 如何 tooset 向上 Arduino 面板，請參閱的 toolearn[設定您的裝置][configure-your-device]。
* 在您的 Azure 訂用帳戶中建立的 IoT 中樞。 toolearn 如何 toocreate IoT 中樞，請參閱[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]。

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>連接 hello 範例應用程式 tooyour IoT 中樞

1. 請確定您是在 hello 儲存機制資料夾`iot-hub-c-feather-m0-getting-started`。

   開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:

   ```bash
   cd Lesson4
   code .
   ```

   請注意 hello`app.ino`檔案在 hello`app`子資料夾。 hello`app.ino`檔案是 hello 金鑰來源檔案，其中包含從 hello IoT 中樞的 hello 碼 toomonitor 內送訊息。 hello`blinkLED`函式會閃爍 hello LED。

   ![Hello 範例應用程式中的儲存機制結構][repo-structure]

2. 取得 hello hello 裝置探索 cli hello 裝置的序列通訊埠：

   ```bash
   devdisco list --usb
   ```

   您應該看到的類似 toohello 下列輸出，並尋找 Arduino 面板 hello usb COM 連接埠：

   ![裝置探索][device-discovery]

3. 開啟 hello 檔案`config.json`hello 課程資料夾，然後輸入的 hello hello 找到 COM 連接埠號碼值中：

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Hello COM 連接埠，Windows 平台上，它有 hello 格式`COM1, COM2, ...`。 在 macOS 或 Ubuntu 上，它將以 `/dev/` 做為開頭。

4. 藉由執行下列命令的 hello 初始化 hello 設定檔：

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. 請遵循取代 hello hello`config-arduino.json`檔案：

   如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]此電腦上所有的 hello 組態繼承的因此您可以略過部署的 hello 步驟 toohello 工作和執行 hello 範例應用程式。 如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]不同電腦上，您需要在 hello tooreplace hello 預留位置`config-arduino.json`檔案。 hello`config-arduino.json`檔案是在主資料夾 hello 子資料夾。

   ![Hello config arduino.json 檔案的內容][config-arduino-json]

   * 取代**[Wi-fi SSID]**具有連接 toohello 網際網路您 Wi-fi SSID。
   * 以 Wi-Fi 密碼取代 **[Wi-Fi password]**。 如果您 Wi-fi 不需要密碼，請移除 hello 字串。
   * 取代**[IoT 裝置連接字串]** hello 裝置連接字串，您會得到執行 hello`az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`命令。
   * 取代**[IoT 中樞連接字串]**以 hello IoT 中樞連接字串，您會得到執行 hello`az iot hub show-connection-string --name {my hub name}`命令。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行 hello 範例應用程式 Arduino 面板上，執行下列命令的 hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

hello gulp 命令會將部署 hello 範例應用程式 tooyour Arduino 面板。 然後，它 hello 應用程式上執行 Arduino 面板和您的主機上的個別工作電腦 toosend 20 閃爍訊息 tooyour Arduino 面板從 IoT 中樞。

Hello 範例應用程式執行之後，它會啟動接聽 toomessages 從 IoT 中樞。 同時，hello gulp 工作會從您的 IoT 中樞 tooyour Arduino 面板中，傳送"閃爍 」 的數個訊息。 Hello 範例應用程式的每個 hello 面板的閃爍訊息接收時，呼叫 hello`blinkLED`函式 tooblink hello LED。

您應該會看見 hello LED 閃爍每隔兩秒鐘，因為 hello gulp 工作會從您的 IoT 中樞 tooyour Arduino 面板傳送 20 則訊息。 hello 上次是停止 hello 應用程式無法執行 「 停止 」 訊息。

![具有 gulp 命令和閃爍訊息的範例應用程式][sample-application]

## <a name="summary"></a>摘要
您已成功傳送訊息，從您 IoT 中樞 tooyour Arduino 面板 tooblink hello LED。 是選擇性的 hello 下一項工作： 變更 hello 開啟和關閉 hello LED 的行為。

## <a name="next-steps"></a>後續步驟
[變更 hello 開啟和關閉 hello LED 的行為][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md