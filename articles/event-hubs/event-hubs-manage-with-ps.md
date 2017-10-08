---
title: "aaaUse PowerShell toomanage Azure 事件中樞資源 |Microsoft 文件"
description: "使用 PowerShell 模組 toocreate 和管理事件中心"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a>使用 PowerShell toomanage 事件中心的資源

Microsoft Azure PowerShell 是指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理 Azure 服務。 本文說明如何 toouse hello[事件中樞資源管理員 PowerShell 模組](/powershell/module/azurerm.eventhub)tooprovision 和管理事件中心的實體 （命名空間，個別的事件中樞取用者群組） 使用本機的 Azure PowerShell 主控台或指令碼。

您也可以使用 Azure Resource Manager 範本來管理事件中樞資源。 如需詳細資訊，請參閱 hello 文章[建立事件中樞命名空間與使用 Azure Resource Manager 範本事件中樞與取用者群組](event-hubs-resource-manager-namespace-event-hub.md)。

## <a name="prerequisites"></a>必要條件

開始之前，您必須先 hello 下列：

* Azure 訂用帳戶。 如需取得訂用帳戶的詳細資訊，請參閱[購買選項][purchase options]、[成員優惠][member offers]或[免費帳戶][free account]。
* 具備 Azure PowerShell 的電腦。 如需指示，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps)。
* PowerShell 指令碼及 NuGet 套件 hello.NET Framework 的基本認識。

## <a name="get-started"></a>開始使用

hello 第一個步驟是 toouse PowerShell toolog 中 tooyour Azure 帳戶和 Azure 訂用帳戶。 請依照下列中的 hello 指示[開始使用 Azure PowerShell cmdlet](/powershell/azure/get-started-azureps) toolog 中 tooyour Azure 帳戶，然後擷取並存取您的 Azure 訂用帳戶中的 hello 資源。

## <a name="provision-an-event-hubs-namespace"></a>佈建事件中樞命名空間

當使用事件中樞命名空間，您可以使用 hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace)，[新增 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace)，[移除 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace)與[組 AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet。

此範例會建立一些區域變數中 hello 指令碼。`$Namespace`和`$Location`。

* `$Namespace`這是 hello 我們想 toowork hello 事件中樞命名空間名稱。
* `$Location`識別 hello 資料中心中的我們將會佈建 hello 命名空間。
* `$CurrentNamespace`儲存 hello 參考命名空間中，我們擷取 （或建立）。

在實際的指令碼中，`$Namespace` 和 `$Location` 可以參數的方式傳遞。

Hello 指令碼的這個部分未 hello 遵循：

1. 嘗試 tooretrieve hello 的事件中樞命名空間指定的名稱。
2. 如果找到 hello 命名空間，它會報告找到的項目。
3. 如果找不到 hello 命名空間，它會建立 hello 命名空間，並接著會擷取新建立的命名空間的 hello。

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a>建立事件中心

toocreate 事件中心，執行使用 hello 前一節中的 hello 指令碼命名空間檢查。 然後，使用 hello[新增 AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello 事件中心：

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a>建立取用者群組

toocreate 取用者群組內的事件中心執行 hello 命名空間和事件中樞檢查 hello 前一節中使用 hello 指令碼。 然後，使用 hello[新增 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello hello 事件中心內的取用者群組。 例如：

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a>設定使用者中繼資料

在執行之後 hello 指令碼 hello 前幾節中，您可以使用 hello[組 AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello 屬性的取用者群組，如 hello 下列範例所示：

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>移除事件中樞

您建立 tooremove hello 事件中心，您可以使用 hello `Remove-*` cmdlet，如 hello 下列範例所示：

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>後續步驟

- 請參閱 hello 完整事件中樞資源管理員 PowerShell 模組的文件[這裡](/powershell/module/azurerm.eventhub)。 此頁面會列出所有可用的 Cmdlet。
- 如需使用 Azure Resource Manager 範本資訊，請參閱 hello 文章[建立事件中樞命名空間與使用 Azure Resource Manager 範本事件中樞與取用者群組](event-hubs-resource-manager-namespace-event-hub.md)。
- [事件中樞 .NET 管理程式庫](event-hubs-management-libraries.md)的相關資訊。

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
