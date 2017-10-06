---
title: "模擬裝置與 Azure IoT 閘道 - 第 4 課：表格儲存體 | Microsoft Docs"
description: "從 Intel NUC tooyour IoT 中樞儲存訊息、 將它們寫入 tooAzure 資料表儲存體，然後讀取它們從 hello 雲端。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "從雲端擷取資料, iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>讀取保存在 Azure 表格儲存體中的訊息

## <a name="what-you-will-do"></a>將執行的作業

- 傳送訊息 tooyour IoT 中樞在閘道上執行 hello 閘道範例應用程式。
- 在您的 Azure 資料表儲存體中的主機電腦 tooread 訊息執行範例程式碼。

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標

如何 toouse hello 的 gulp 工具 toorun hello 範例程式碼 tooread 訊息在您的 Azure 資料表儲存體。

## <a name="what-you-need"></a>您需要什麼

您有已成功地完成下列工作 hello:

- [建立 hello Azure 函式應用程式和 hello Azure 儲存體帳戶](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)。
- [執行應用程式-閘道範例 hello](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)。
- [讀取來自 IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)。

## <a name="get-your-azure-storage-connection-strings"></a>取得您的 Azure 儲存體連接字串

稍早在本課程中，您已成功建立 Azure 儲存體帳戶。 hello Azure 儲存體帳戶，執行下列命令的 hello tooget hello 連接字串：

* 列出您的所有儲存體帳戶。

```bash
az storage account list -g iot-gateway --query [].name
```

* 取得 Azure 儲存體連接字串。

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

使用`iot-gateway`做為 hello 值`{resource group name}`如果您沒有變更 hello 課程 2 中的值。

## <a name="configure-hello-device-connection"></a>設定 hello 裝置連線

更新 hello`config-azure.json`檔案，以便在 hello 主機電腦執行的 hello 範例程式碼可以讀取您的 Azure 資料表儲存體中的訊息。 tooconfigure hello 裝置連線，請遵循下列步驟：

1. 開啟 hello 裝置組態檔`config-azure.json`藉由執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![組態](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. 取代`[Azure storage connection string]`以 hello 您取得的 Azure 儲存體連接字串。

   `[IoT hub connection string]` 應該已經在第 3 課的[讀取來自 Azure IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)中被取代。

## <a name="read-messages-in-your-azure-table-storage"></a>讀取 Azure 表格儲存體中的訊息

執行 hello 閘道範例應用程式，並讀取 Azure 資料表儲存體訊息 hello 下列命令：

```bash
gulp run --table-storage
```

IoT 中樞觸發您 Azure 函式的應用程式 toosave 訊息到您的 Azure 資料表儲存體，新訊息到達時。
hello`gulp run`命令執行閘道範例應用程式所傳送訊息 tooyour IoT 中樞。 與`table-storage`參數，它也會產生您的 Azure 資料表儲存體中儲存訊息的子處理序 tooreceive hello。

hello 訊息傳送，而且收到相同主控台視窗中的所有顯示立即在 hello hello 主機電腦。 hello 範例應用程式執行個體將會自動在 40 秒終止。

   ![gulp 讀取](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a>摘要

您已在您 Azure 函式應用程式所儲存的 Azure 資料表儲存體執行 hello 範例程式碼 tooread hello 訊息。
