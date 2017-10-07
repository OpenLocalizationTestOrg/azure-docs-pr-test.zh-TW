---
title: "Connect Arduino (C) tooAzure IoT-第 3 課： 執行範例 |Microsoft 文件"
description: "部署和執行範例應用程式 tooAdafruit 羽毛 M0 WiFi 傳送訊息 tooyour IoT 中樞和閃爍 hello LED。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務，arduino 傳送資料 toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>執行範例應用程式 toosend 裝置到雲端訊息
## <a name="what-you-will-do"></a>將執行的作業
本文將告訴您 toodeploy 及執行範例應用程式上 Adafruit 羽毛 M0 WiFi Arduino board 該傳送訊息 tooyour IoT 中樞。

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-learn"></a>學習目標
您將學習如何 toouse hello 的 gulp 工具 toodeploy 和 Arduino 面板上執行 hello 範例 Arduino 應用程式。

## <a name="what-you-need"></a>您需要什麼
* 在開始這項工作之前，您必須已順利完成[建立 Azure 的函式應用程式與儲存體帳戶 tooprocess 和市集 IoT 中樞訊息][process-and-store-iot-hub-messages]。

## <a name="get-your-iot-hub-and-device-connection-strings"></a>取得 IoT 中樞與裝置連接字串
hello 裝置連接字串是使用的 tooconnect Arduino 面板 tooyour IoT 中樞。 hello IoT 中樞連接字串是使用的 tooconnect 您 IoT 中樞 toohello 裝置身分識別，表示您 Arduino 面板在 hello IoT 中樞。

* 列出資源群組中的所有您 IoT 中樞執行下列 Azure CLI 命令的 hello:

```bash
az iot hub list -g iot-sample --query [].name
```

使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。

* 藉由執行下列 Azure CLI 命令的 hello 收到 hello IoT 中樞連接字串：

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`這是您指定當您建立 IoT 中樞，並註冊 Arduino 面板 hello 名稱。

* 藉由執行下列命令的 hello 收到 hello 裝置連接字串：

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

使用`mym0wifi`做為 hello 值`{device id}`如果您沒有變更 hello 值。
## <a name="configure-hello-device-connection"></a>設定 hello 裝置連線
tooconfigure hello 裝置連線，請遵循下列步驟：

1. 取得 hello hello 裝置探索 cli hello 裝置的序列通訊埠：

   ```bash
   devdisco list --usb
   ```

   您應該看到的類似 toohello 下列輸出，並尋找 Arduino 面板 hello usb COM 連接埠：

   ![裝置探索][device-discovery]

2. 開啟 hello 檔案`config.json`在 hello 課程資料夾並加入 hello 的 hello 找到 COM 連接埠號碼的值：

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Hello COM 連接埠，Windows 平台上，它有 hello 格式`COM1, COM2, ...`。 在 macOS 或 Ubuntu 上，它是以 `/dev/` 開頭。

3. 藉由執行下列命令的 hello 初始化 hello 設定檔：

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. 開啟 hello 裝置組態檔`config-arduino.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. 請遵循取代 hello hello`config-arduino.json`檔案：

   * 取代**[Wi-fi SSID]**具有連接 toohello 網際網路您 Wi-fi SSID。
   * 以 Wi-Fi 密碼取代 **[Wi-Fi password]**。 如果您 Wi-fi 不需要密碼，請移除 hello 字串。
   * 取代**[IoT 裝置連接字串]**以 hello`device connection string`您取得的。
   * 取代**[IoT 中樞連接字串]**以 hello`iot hub connection string`您取得的。

   > [!NOTE]
   > 您在本文中不需要 `azure_storage_connection_string`。 請讓它保持原狀。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行 hello 範例應用程式 Arduino 面板上，執行下列命令的 hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> hello 預設 gulp 工作執行`install-tools`和`run`循序的工作。 當您[hello 閃爍應用程式部署][deployed-the-blink-app]，個別執行這些工作。

## <a name="verify-that-hello-sample-application-works"></a>確認 hello 範例應用程式可正常運作
您應該會看到 hello GPIO #0 主機板 LED 閃爍不停每隔兩秒鐘。 每次 hello LED 閃爍，hello 範例應用程式傳送訊息 tooyour IoT 中樞，並確認該 hello 訊息已成功傳送 tooyour IoT 中樞。 此外，收到 hello IoT 中樞的每個訊息會列印 hello 主控台視窗中。 hello 範例應用程式會自動終止後傳送 20 則訊息。

![具有所傳送和接收之訊息的範例應用程式][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>摘要
您部署，並在您 Arduino 面板 toosend 裝置到雲端訊息 tooyour IoT 中樞執行 hello 新閃爍範例應用程式。 您現在監視您的郵件將它們寫入 toohello 儲存體帳戶。

## <a name="next-steps"></a>後續步驟
[讀取保存在 Azure 儲存體中的訊息][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md