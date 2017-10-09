---
title: "模擬裝置與 Azure IoT 閘道 - 第 3 課：讀取訊息 | Microsoft Docs"
description: "在主機電腦 tooread hello 訊息上執行範例程式碼，從 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 雲端、 雲端資料收集、 iot 雲端服務、 iot 資料中的資料"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>讀取來自 IoT 中樞的傳入訊息

## <a name="what-you-will-do"></a>將執行的作業

- 執行範例程式碼在您的主機電腦 tooread 訊息從 IoT 中樞。

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標

如何 toouse hello 的 gulp 工具 tooread 訊息從 IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

- 中的 hello 模擬的裝置範例[設定及執行模擬的裝置雲端範例應用程式上傳](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)。

## <a name="get-your-iot-hub-and-device-connection-strings"></a>取得 IoT 中樞與裝置連接字串

hello 裝置連接字串會使用模擬的裝置 tooconnect tooyour IoT 中樞。 hello IoT 中樞連接字串是使用的 tooconnect toohello 身分識別登錄在 IoT 中樞 toomanage hello 裝置允許 tooconnect tooyour IoT 中樞。

- 列出資源群組中的所有您 IoT 中樞執行 hello 下列命令：

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   使用`iot-gateway`做為 hello 值`{resource group name}`如果您沒有變更它。
- 藉由執行下列命令的 hello 收到 hello IoT 中樞連接字串：

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`這是您在第 2 課中指定的 hello 名稱。

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>設定 hello hello 範例程式碼的裝置連線

更新中的 IoT 中樞與裝置連線組態`config-azure.json`藉由執行下列步驟的 hello:

1. 開啟`config-azure.json`在 Visual Studio 程式碼執行下列命令，在主控台視窗中的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. 請遵循取代 hello hello`config-azure.json`檔案：

   ![設定 azure 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   取代`[IoT hub connection string]`以 hello IoT 中樞連接字串。

## <a name="read-messages-from-your-iot-hub"></a>讀取來自 IoT 中樞的傳入訊息

執行 hello 模擬裝置的範例應用程式，並讀取 IoT 中樞訊息 hello 下列命令：

```bash
gulp run --iot-hub
```

hello 命令會執行每 2 秒會傳送訊息 tooyour IoT 中樞的 hello 應用程式。 它也會繁衍子處理序 tooreceive hello 訊息。

hello 訊息傳送，而且收到相同主控台視窗中的所有顯示立即在 hello hello 主機電腦。 hello 應用程式將會結束 40 秒中。

![模擬的範例應用程式及傳送和接收的訊息](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>摘要

您已成功地執行 hello 範例應用程式 toosend 資料 tooyour IoT 中樞，與模擬的裝置。 您也閱讀 tooyour IoT 中心已傳送 hello 訊息。

## <a name="next-steps"></a>後續步驟
[建立 Azure 函數應用程式與 Azure 儲存體帳戶](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


