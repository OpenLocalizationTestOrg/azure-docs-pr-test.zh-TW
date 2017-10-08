---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 3 課︰執行範例應用程式 | Microsoft Docs"
description: "從 B SensorTag 以及 IoT 中樞，請執行範例應用程式 tooreceive b 的資料。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "b 應用程式、 感應器監視應用程式、 感應器資料收集、 感應器資料 toocloud 感應器資料"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>設定和執行 BLE 範例應用程式

## <a name="what-you-will-do"></a>將執行的作業

- 複製 hello 範例儲存機制。 
- 設定 hello SensorTag 和 Intel NUC 之間的連線。 
- 使用您的 IoT 中樞與 SensorTag 資訊 hello Azure CLI tooget b （藍芽低能源） 範例應用程式。 設定和執行 hello b 範例應用程式。 

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標

在本文中，您將了解：

- 如何 tooconfigure 和執行的 hello b 範例應用程式。

## <a name="what-you-need"></a>您需要什麼

您必須已成功完成

- [建立 IoT 中樞並登錄裝置](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>複製 hello 範例儲存機制 toohello 主機電腦

tooclone hello 範例儲存機制，請遵循下列步驟在 hello 主機電腦上：

1. 在 Windows 上開啟命令提示字元視窗，或在 macOS 或 Ubuntu 上開啟終端機。
2. 執行下列命令的 hello:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>設定 hello SensorTag 和 Intel NUC 之間的連線

tooset 向上 hello 連線，請遵循下列步驟，在 hello 主機電腦上：

1. 藉由執行下列命令的 hello 初始化 hello 設定檔：

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. 開啟`config-gateway.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. 找出 hello 下列程式碼行並取代`[device hostname or IP address]`hello IP 位址或主機名稱為 Intel NUC。
   ![設定閘道器的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. 安裝在 Intel NUC 協助程式工具執行下列命令的 hello:

   ```bash
   gulp install-tools
   ```

5. 開啟 SensorTag 為 hello 下列圖片中，按下 hello 電源按鈕並 hello 綠色 LED 應閃爍。

   ![開啟 SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. 藉由執行下列命令的 hello 掃描 SensorTag 裝置：

   ```bash
   gulp discover-sensortag
   ```

7. 藉由執行下列命令的 hello 測試 hello hello SensorTag 和 Intel NUC 之間的連線：

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   取代`{mac address}`以 hello hello 先前步驟中取得的 MAC 位址。

## <a name="get-hello-connection-string-of-sensortag"></a>取得 SensorTag hello 連接字串

tooget hello SensorTag，執行下列命令在 hello 主機電腦上的 hello Azure IoT 中樞連接字串：

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`是您所使用的 hello IoT 中樞名稱。 當做 hello 值使用 iot 閘道`{resource group name}`並用 mydevice 做為 hello 值`{device id}`如果您沒有變更 hello 課程 2 中的值。

## <a name="configure-hello-ble-sample-application"></a>Hello b 範例應用程式設定

tooconfigure 和執行的 hello b 範例應用程式，請遵循下列步驟在 hello 主機電腦上：

1. 開啟`config-sensortag.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![設定 sensortag 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. 請遵循取代 hello 程式碼中的 hello:
   - 取代`[IoT hub name]`與您所使用的 hello IoT 中樞名稱。
   - 取代`[IoT device connection string]`與 hello SensorTag 取得的連接字串。
   - 取代`[device_mac_address]`以 hello hello SensorTag 取得的 MAC 位址。

3. 執行 hello b 範例應用程式。

   toorun hello b 範例應用程式，請遵循下列步驟，在 hello 主機電腦上：

   1. 開啟 SensorTag。

   2. 部署及執行 hello b 範例應用程式在 Intel NUC 上執行下列命令的 hello:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>確認 hello b 範例應用程式可正常運作

您現在應該會看到類似 hello 下列輸出：

![BLE 範例應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

hello 範例應用程式會持續收集溫度資料，並傳送它 tooyour IoT 中樞。 hello 範例應用程式會在傳送 40 秒後自動終止。

## <a name="summary"></a>摘要

您已成功設定 hello SensorTag 和 Intel NUC 之間的連線，並執行會收集並傳送資料，從 SensorTag tooyour IoT 中樞 b 範例應用程式。 您已準備好 toolearn tooverify 的 IoT 中樞收到 hello 資料的方式。

## <a name="next-steps"></a>後續步驟
[讀取來自 IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)