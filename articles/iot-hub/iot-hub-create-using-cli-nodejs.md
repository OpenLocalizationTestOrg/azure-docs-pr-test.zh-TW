---
title: "使用 Azure CLI (azure.js) IoT 中樞 aaaCreate |Microsoft 文件"
description: "如何使用您建立 Azure IoT 中樞 toocreate hello 跨平台 Azure CLI (azure.js)。"
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>建立使用 Azure CLI hello IoT 中樞

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>簡介

您可以使用 Azure CLI (azure.js) toocreate，並以程式設計方式管理 Azure IoT 中樞。 本文章將示範如何 toouse 會 hello Azure CLI (azure.js) toocreate IoT 中樞。

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

* Azure CLI (azure.js) – hello CLI 傳統的 hello 與資源管理部署模型這篇文章中所述。
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello 新一代 CLI hello 資源管理部署模型。

toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* [Azure CLI 0.10.4][lnk-CLI-install] 或更新版本。 如果您已經有 hello Azure CLI 安裝，您可以驗證 hello 目前版本在 hello 命令提示字元以 hello 下列命令：

```azurecli
azure --version
```

> [!NOTE]
> Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 hello Azure CLI 必須是 Azure Resource Manager 模式：
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>設定 Azure 帳戶和訂用帳戶

1. 在 hello 命令提示字元中輸入下列命令的 hello 登入：

   ```azurecli
    azure login
   ```

   使用 hello 建議的網頁瀏覽器和程式碼 tooauthenticate。
1. 如果您有多個 Azure 訂用帳戶，連接 tooAzure 授與存取 tooall hello 與認證相關聯的 Azure 訂用帳戶。 您可以檢視 hello Azure 訂用帳戶，並找出哪一種 hello 預設，使用 hello 命令：

   ```azurecli
    azure account list
   ```

   您想要在其下 toorun hello 其餘的 hello 命令使用 tooset hello 訂用帳戶內容：

   ```azurecli
    azure account set <subscription name>
   ```

1. 如果您沒有資源群組，您可以建立一個名為 **exampleResourceGroup** 的資源群組：

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> hello 文章[使用 hello Azure CLI toomanage Azure 資源與資源群組][ lnk-CLI-arm]提供詳細的資訊關於如何 toouse hello Azure CLI toomanage Azure 資源。

## <a name="create-an-iot-hub"></a>建立 IoT 中樞

必要參數：

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resource-group**。 hello 資源群組名稱。 不區分大小寫英數字元、 底線和連字號，1-64 長度 hello 格式。
* **名稱**。 建立 hello IoT 中樞 toobe hello 名稱。 不區分大小寫英數字元、 底線和連字號、 3-50 長度 hello 格式。
* **location**。 hello 位置 （azure 區域/資料中心） tooprovision hello IoT 中樞。
* **sku-name**。 hello hello sku 的其中一個名稱: [F1、 S1、 S2、 S3]。 Hello 最新的完整清單，請參閱 toohello IoT 中樞定價頁面。
* **units**。 hello 佈建的單位數目。 範圍：F1 [1-1]：S1、S2 [1-200]：S3 [1-10]。 IoT 中樞單位以您想 tooconnect 您總訊息計數和 hello 裝置數目。

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee 所有 hello 參數可供建立，您可以使用命令提示字元中的 hello [說明] 命令：

```azurecli
azure iothub create -h
```

簡單的範例： toocreate IoT 中樞呼叫**exampleIoTHubName** hello 資源群組中**exampleResourceGroup**，請執行 hello 下列命令：

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> 此 Azure CLI 命令會新增您付費的「S1 標準 IoT 中樞」。 您可以刪除 hello IoT 中樞**exampleIoTHubName**使用下列命令：
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>後續步驟

toolearn 進一步了解開發的 IoT 中樞，請參閱下列文章 hello:

* [IoT SDK][lnk-sdks]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 hello Azure 入口網站 toomanage IoT 中樞][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
