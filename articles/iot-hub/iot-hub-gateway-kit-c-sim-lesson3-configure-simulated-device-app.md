---
title: "模擬裝置與 Azure IoT 閘道 - 第 3 課︰執行範例應用程式 | Microsoft Docs"
description: "執行模擬的裝置範例應用程式 toosend 溫度資料 tooyour IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "資料 toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>設定並執行模擬裝置範例應用程式

## <a name="what-you-will-do"></a>將執行的作業

- 複製 hello 範例儲存機制。
- 使用您的 IoT 中樞與邏輯裝置資訊 hello Azure CLI tooget 用於模擬的裝置範例應用程式。 設定和執行 hello 模擬裝置的範例應用程式。

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標

在本文中，您將了解：

- 如何 tooconfigure 和執行的 hello 模擬裝置的範例應用程式。

## <a name="what-you-need"></a>您需要什麼

您必須已成功完成

- [建立 IoT 中樞並登錄您的裝置](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>複製 hello 範例儲存機制 toohello 主機電腦

tooclone hello 範例儲存機制，請遵循下列步驟在 hello 主機電腦上：

1. 在 Windows 上開啟命令提示字元，或在 macOS 或 Ubuntu 上開啟終端機。
2. 執行下列命令的 hello:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>設定 hello 模擬的裝置和您 NUC

1. 開啟 hello 設定檔`config.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   code config.json
   ```

2. 將 `"has_sensortag": true` 取代為 `"has_sensortag": false`

   ![設定為您沒有 TI SensorTag 裝置](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. 藉由執行下列命令的 hello 初始化 hello 設定檔：

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. 開啟`config-gateway.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. 找出 hello 下列程式碼行並取代`[device hostname or IP address]`與 hello Intel NUC 的 IP 位址或主機名稱。
   ![設定閘道器的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>取得您的 IoT 中樞邏輯裝置 hello 連接字串

tooget hello Azure IoT 中樞連接字串的邏輯裝置，執行下列命令在 hello 主機電腦上的 hello:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`是您所使用的 hello IoT 中樞名稱。 當做 hello 值使用 iot 閘道`{resource group name}`並用 mydevice 做為 hello 值`{device id}`如果您沒有變更 hello 課程 2 中的值。

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>設定 hello 模擬裝置的雲端上傳範例應用程式

tooconfigure 和執行的 hello 模擬裝置的雲端上傳範例應用程式，請遵循下列步驟在 hello 主機電腦上：

1. 開啟`config-sensortag.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![設定 sensortag 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. 請遵循取代 hello 程式碼中的 hello:
   - 取代`[IoT hub name]`hello IoT 中樞名稱。
   - 取代`[IoT device connection string]`hello 的 IoT 中樞的邏輯裝置的連接字串。

3. 執行 hello 應用程式。

   部署和執行 hello 應用程式，執行下列命令的 hello:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>確認 hello 範例應用程式可運作

您現在應該會看到類似 hello 下列輸出：

![模擬裝置範例應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

hello 應用程式傳送溫度資料 tooyour IoT 中樞，可在延續 40 秒。

## <a name="summary"></a>摘要

您已順利設定並執行的 hello 模擬裝置的雲端上傳範例應用程式傳送資料 tooyour IoT 中樞與模擬的裝置。

## <a name="next-steps"></a>後續步驟
[讀取來自 IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)