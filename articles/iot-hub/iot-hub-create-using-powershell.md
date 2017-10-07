---
title: "使用 PowerShell 指令程式的 Azure IoT 中樞 aaaCreate |Microsoft 文件"
description: "如何 toouse PowerShell cmdlet toocreate IoT 中樞。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>建立 IoT 中心使用 hello 新增 AzureRmIotHub cmdlet

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>簡介

您可以使用 Azure PowerShell cmdlet toocreate 和管理 Azure IoT 中樞。 本教學課程示範如何使用 PowerShell IoT 中樞 toocreate。

> [!NOTE]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。 本文件涵蓋使用 hello Azure Resource Manager 部署模型。

toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 <br/>如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* [Azure PowerShell Cmdlet][lnk-powershell-install]。

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

## <a name="create-resource-group"></a>建立資源群組

您需要的資源群組 toodeploy IoT 中樞。 您可以使用現有的資源群組，或建立一個新的群組。

您可以使用下列命令 toodiscover hello 位置，您可以在其中部署 IoT 中樞的 hello:

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate IoT 中樞，下列命令使用 hello hello 支援位置其中之一的 IoT 中心的資源群組。 這個範例會建立一個稱為資源群組**MyIoTRG1**在 hello**美國東部**區域：

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>建立 IoT 中樞

toocreate IoT 中心在您建立在 hello 先前步驟中，下列命令使用 hello hello 資源群組中。 這個範例會建立**S1**中樞呼叫**MyTestIoTHub**在 hello**美國東部**區域：

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

hello hello IoT 中樞名稱不得重複。

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


您可以使用下列命令的 hello 您訂用帳戶中列出所有 hello IoT 中心：

```powershell
Get-AzureRmIotHub
```

hello 前一個範例會將 S1 標準 IoT 中樞，您需要付費。 您可以刪除 hello IoT 中樞使用 hello 下列命令：

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

或者，您可以移除資源群組，而且所有 hello 它包含使用下列命令的 hello 的資源：

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>後續步驟

現在您已經部署 IoT 中心使用 PowerShell cmdlet，您可以進一步 tooexplore:

* 探索其他[搭配您的 IoT 中樞使用的 PowerShell Cmdlet][lnk-iothub-cmdlets]。
* 閱讀有關 hello hello 功能[IoT 中樞資源提供者 REST API][lnk-rest-api]。

進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:

* [簡介 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 IoT Edge 來模擬裝置][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
