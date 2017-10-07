---
title: "aaaUse PowerShell toomanage Azure 服務匯流排資源 |Microsoft 文件"
description: "使用 PowerShell 模組 toocreate 和管理服務匯流排資源"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a>使用 PowerShell toomanage 服務匯流排資源

Microsoft Azure PowerShell 是指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理 Azure 服務。 本文說明如何 toouse hello[服務匯流排資源管理員 PowerShell 模組](/powershell/module/azurerm.servicebus)tooprovision 和管理服務匯流排實體 （命名空間、 佇列、 主題和訂用帳戶） 使用本機的 Azure PowerShell 主控台或指令碼。

您也可以使用 Azure Resource Manager 範本來管理服務匯流排實體。 如需詳細資訊，請參閱 hello 文章[使用 Azure Resource Manager 範本建立服務匯流排資源](service-bus-resource-manager-overview.md)。

## <a name="prerequisites"></a>必要條件

開始之前，您必須先 hello 下列：

* Azure 訂用帳戶。 如需取得訂用帳戶的詳細資訊，請參閱[購買選項][purchase options]、[成員優惠][member offers]或[免費帳戶][free account]。
* 具備 Azure PowerShell 的電腦。 如需指示，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/get-started-azureps)。
* PowerShell 指令碼及 NuGet 套件 hello.NET Framework 的基本認識。

## <a name="get-started"></a>開始使用

hello 第一個步驟是 toouse PowerShell toolog 中 tooyour Azure 帳戶和 Azure 訂用帳戶。 請依照下列中的 hello 指示[開始使用 Azure PowerShell cmdlet](/powershell/azure/get-started-azureps) toolog tooyour Azure 帳戶和擷取及存取您的 Azure 訂用帳戶中的 hello 資源中。

## <a name="provision-a-service-bus-namespace"></a>佈建服務匯流排命名空間

當使用服務匯流排命名空間，您可以使用 hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace)，[新增 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace)，[移除 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace)，和[組 AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet。

此範例會建立一些區域變數中 hello 指令碼。`$Namespace`和`$Location`。

* `$Namespace`這是 hello 我們想 toowork hello 服務匯流排命名空間名稱。
* `$Location`識別 hello 資料中心中的我們將會佈建 hello 命名空間。
* `$CurrentNamespace`儲存 hello 參考命名空間中，我們擷取 （或建立）。

在實際的指令碼中，`$Namespace` 和 `$Location` 可以參數的方式傳遞。

Hello 指令碼的這個部分未 hello 遵循：

1. 嘗試 tooretrieve hello 與服務匯流排命名空間指定的名稱。
2. 如果找到 hello 命名空間，它會報告找到的項目。
3. 如果找不到 hello 命名空間，它會建立 hello 命名空間，並接著會擷取新建立的命名空間的 hello。
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a>建立命名空間授權規則

hello 下列範例示範如何使用 toomanage 命名空間授權規則 hello[新增 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule)， [Get AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule)，[組 AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule)，和[移除 AzureRmServiceBusNamespaceAuthorizationRule cmdlet](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule)。

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a>建立佇列

toocreate 佇列或主題時，執行使用 hello 前一節中的 hello 指令碼的命名空間檢查。 然後，建立 hello 佇列：

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a>修改佇列屬性

在執行之後 hello 指令碼 hello 前面一節中，您可以使用 hello[組 AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello 佇列，如 hello 下列範例所示的屬性：

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>佈建其他服務匯流排實體

您可以使用 hello[服務匯流排 PowerShell 模組](/powershell/module/azurerm.servicebus)tooprovision 其他實體，例如主題和訂閱。 這些指令程式是語法類似 toohello 佇列建立指令程式 hello 上一節所示。

## <a name="next-steps"></a>後續步驟

- 請參閱 hello 完整服務匯流排資源管理員 PowerShell 模組的文件[這裡](/powershell/module/azurerm.servicebus)。 此頁面會列出所有可用的 Cmdlet。
- 如需使用 Azure Resource Manager 範本資訊，請參閱 hello 文章[使用 Azure Resource Manager 範本建立服務匯流排資源](service-bus-resource-manager-overview.md)。
- [服務匯流排 .NET 管理程式庫](service-bus-management-libraries.md)的相關資訊。

有一些替代 toomanage 服務匯流排實體，如下列部落格文章所述：

* [如何 toocreate 服務匯流排佇列、 主題和訂用帳戶的 PowerShell 指令碼](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [如何為服務匯流排命名空間，並使用 PowerShell 指令碼的事件中樞的 toocreate](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [服務匯流排 PowerShell 指令碼](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
