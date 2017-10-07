---
title: "aaaCreate Azure IoT 中樞使用的範本 (PowerShell) |Microsoft 文件"
description: "如何 toouse Azure Resource Manager 範本 toocreate IoT 中樞與 PowerShell。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>使用 Azure Resource Manager 範本建立 IoT 中樞 (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

您可以使用 Azure Resource Manager toocreate，並以程式設計方式管理 Azure IoT 中樞。 本教學課程示範如何 toouse Azure Resource Manager 範本 toocreate IoT 中樞與 PowerShell。

> [!NOTE]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。 本文件涵蓋使用 hello Azure Resource Manager 部署模型。

toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 <br/>如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* [Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。

> [!TIP]
> hello 文章[使用 Azure PowerShell 的 Azure Resource Manager] [ lnk-powershell-arm]提供更多有關 toouse PowerShell 和 Azure 資源管理員範本 toocreate Azure 資源。

## <a name="connect-tooyour-azure-subscription"></a>連接 tooyour Azure 訂用帳戶

在 PowerShell 命令提示字元中，輸入下列命令 toosign tooyour Azure 訂用帳戶中的 hello:

```powershell
Login-AzureRmAccount
```

如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 訂用帳戶。 使用下列命令 toolist hello Azure 訂用帳戶可讓您 toouse hello:

```powershell
Get-AzureRMSubscription
```

使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toocreate IoT 中樞的 hello。 您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

您可以使用下列命令 toodiscover 其中您可以部署 IoT 中樞與 hello 目前支援的 API 版本的 hello:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

建立資源群組 toocontain 您使用下列命令中其中一個支援的 hello 位置 IoT 中樞的 hello 的 IoT 中樞。 這個範例會建立一個稱為 **MyIoTRG1**的資源群組：

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>送出範本 toocreate IoT 中樞

使用資源群組中的 JSON 範本 toocreate IoT 中樞。 您也可以使用 Azure Resource Manager 範本 toomake 變更 tooan 現有 IoT 中樞。

1. 使用 Azure Resource Manager 範本所呼叫的文字編輯器 toocreate **template.json**與 hello 資源定義 toocreate 下列新的標準 IoT 中樞。 這個範例會將 hello IoT 中樞中 hello**美國東部**區域中，會建立兩個取用者群組 (**cg1**和**cg2**) hello 事件中樞相容的端點，以及使用 hello **2016年-02-03** API 版本。 此範本也需要您 toopass hello IoT 中樞名稱做為參數，呼叫**hubName**。 如 hello 目前的位置，其支援 IoT 中樞的清單，請參閱[Azure 狀態][lnk-status]。

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. 儲存在本機電腦上的 hello Azure 資源管理員範本檔案。 這個範例假設您將它儲存在名為 **c:\templates** 的資料夾中。

3. 執行下列命令 toodeploy hello 您新的 IoT 中樞，做為參數傳遞 hello IoT 中樞名稱。 在此範例中，是 hello hello IoT 中樞名稱`abcmyiothub`。 IoT 中樞 hello 名稱必須是全域唯一的：

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. hello 輸出會顯示 hello hello IoT 中樞，您所建立的索引鍵。

5. 您的應用程式加入的 tooverify hello IoT 中樞，請瀏覽 hello [Azure 入口網站][ lnk-azure-portal]並檢視您資源的清單。 或者，使用 hello **Get AzureRmResource** PowerShell cmdlet。

> [!NOTE]
> 此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。 您可以刪除透過 hello hello IoT 中樞[Azure 入口網站][ lnk-azure-portal]或使用 hello**移除 AzureRmResource** PowerShell 指令程式完成時。

## <a name="next-steps"></a>後續步驟

現在您已經部署使用 Azure Resource Manager 範本搭配 PowerShell IoT 中樞，您可以進一步 tooexplore:

* 閱讀有關 hello hello 功能[IoT 中樞資源提供者 REST API][lnk-rest-api]。
* 讀取[Azure 資源管理員概觀][ lnk-azure-rm-overview] toolearn 更多關於 hello 功能的 Azure 資源管理員。

進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:

* [簡介 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
