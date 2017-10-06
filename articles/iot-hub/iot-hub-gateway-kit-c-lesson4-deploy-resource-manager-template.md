---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 4 課：建立函數應用程式 | Microsoft Docs"
description: "從 Intel NUC tooyour IoT 中樞儲存訊息、 將它們寫入 tooAzure 資料表儲存體，然後讀取它們從 hello 雲端。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "將資料儲存在 hello 雲端中，儲存在雲端中，資料 iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>建立 Azure 函式應用程式與儲存體帳戶

Azure 的函式是方案，輕鬆地執行_函式_（一些程式碼片段） hello 雲端中。 Azure 的函式應用程式裝載函式在 Azure 中的 hello 執行。 

## <a name="what-you-will-do"></a>將執行的作業

- Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。 hello Azure 函式應用程式會接聽 tooAzure IoT 中樞事件、 處理內送訊息，並將其寫入 tooAzure 資料表儲存體。

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。


## <a name="what-you-will-learn"></a>學習目標

在這一課，您將了解：

- 如何 toouse Azure 資源管理員 toodeploy Azure 資源。
- 如何 toouse Azure 函式應用程式 tooprocess IoT 中樞的訊息，並在 Azure 資料表儲存體中撰寫 tooa 資料表。

## <a name="what-you-need"></a>您需要什麼

您必須已順利完成 hello 先前的課程：

- [第 1 課：將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [第 2 課：準備好您的主機電腦和 Azure IoT 中樞](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [第 3 課︰接收來自 SensorTag 的訊息，並讀取來自 IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>開啟範例應用程式

移 tooyour`iot-hub-c-intel-nuc-gateway-getting-started`儲存機制資料夾，初始化 hello 設定檔，然後開啟 hello 範例專案在 Visual Studio 程式碼中藉由執行下列命令的 hello:

```bash
cd Lesson4
npm install
gulp init
code .
```

![存放庫結構](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- hello`arm-template.json`檔案是包含 Azure 的函式應用程式與 Azure 儲存體帳戶的 hello Azure Resource Manager 範本。
- hello`arm-template-param.json`檔案為 hello hello Azure Resource Manager 範本所使用的組態檔。
- hello`ReceiveDeviceMessages`子資料夾包含 hello Node.js hello Azure 函式程式碼。

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>在 Azure 中設定 Azure Resource Manager 範本並建立資源

更新 hello `arm-template-param.json` Visual Studio 程式碼中的檔案。

![arm 範本 json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- 將 `[your IoT Hub name]` 取代為您在第 2 課指定的 `{my hub name}`。

更新 hello 之後`arm-template-param.json`檔案中，執行下列命令的 hello 部署 hello 資源 tooAzure:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

使用`iot-gateway`做為 hello 值`{resource group name}`如果您沒有變更 hello 課程 2 中的值。

## <a name="summary"></a>摘要

您已建立您的 Azure 函式應用程式 tooprocess IoT 中樞訊息，與 Azure 儲存體帳戶的 toostore 這些訊息。 您現在可以讀取由您的閘道 tooyour IoT 中樞傳送的訊息。

## <a name="next-steps"></a>後續步驟
[讀取保存在 Azure 儲存體中的訊息](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)。
