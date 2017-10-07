---
title: "使用 Azure Resource Manager 範本 aaaCreate Azure 服務匯流排資源 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 tooautomate hello 建立服務匯流排資源"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>使用 Azure Resource Manager 範本建立服務匯流排資源

本文說明如何 toocreate 及部署服務匯流排資源使用 Azure Resource Manager 範本、 PowerShell 和 hello 服務匯流排資源提供者。

Azure 資源管理員範本可協助您定義 hello 資源 toodeploy 解決方案，及 toospecify 參數和變數可讓您針對不同的環境 tooinput 值。 hello 範本包含 JSON 和您可以為您的部署使用 tooconstruct 值的運算式。 如需撰寫 Azure 資源管理員範本，並討論 hello 範本格式的詳細資訊，請參閱[結構和語法的 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。

> [!NOTE]
> 如何 hello 這個發行項的顯示中的範例 toouse Azure 資源管理員 toocreate 服務匯流排命名空間和傳訊實體 （佇列）。 如需其他範本的範例，請瀏覽 hello [Azure 快速入門範本組件庫][ Azure Quickstart Templates gallery] ，並搜尋 「 Service Bus 」。
>
>

## <a name="service-bus-resource-manager-templates"></a>服務匯流排 Resource Manager 範本

這些服務匯流排 Azure Resource Manager 範本可供下載和部署。 按一下下列連結以取得有關每個，以在 GitHub 上的連結 toohello 範本的詳細資料的 hello:

* [建立服務匯流排命名空間](service-bus-resource-manager-namespace.md)
* [建立服務匯流排命名空間與佇列](service-bus-resource-manager-namespace-queue.md)
* [建立服務匯流排命名空間與主題和訂用帳戶](service-bus-resource-manager-namespace-topic.md)
* [建立服務匯流排命名空間與佇列和授權規則](service-bus-resource-manager-namespace-auth-rule.md)
* [建立服務匯流排命名空間與主題、訂用帳戶和規則](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>使用 PowerShell 部署

hello 下列程序描述如何 toouse PowerShell toodeploy Azure Resource Manager 範本，建立**標準**層服務匯流排命名空間，而該命名空間內的佇列。 這個範例根據 hello[建立服務匯流排命名空間與佇列](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue)範本。 hello 近似工作流程如下所示：

1. 安裝 PowerShell。
2. 建立 hello 範本以及 （選擇性） 參數檔案。
3. 在 PowerShell 中，登入 tooyour Azure 帳戶。
4. 如果沒有資源群組，請建立一個新的。
5. 測試 hello 部署。
6. 如有需要，請將 hello 部署模式設定。
7. 部署 hello 範本。

如需部署 Azure Resource Manager 範本的完整資訊，請參閱[使用 Azure Resource Manager 範本部署資源][Deploy resources with Azure Resource Manager templates]。

### <a name="install-powershell"></a>安裝 PowerShell

安裝 Azure PowerShell 中的 hello 指示[開始使用 Azure PowerShell](/powershell/azure/get-started-azureps)。

### <a name="create-a-template"></a>建立範本

再製或複製 hello [201 servicebus-建立-佇列](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json)從 GitHub 的範本：

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>建立參數檔案 (選擇性)

toouse 是選擇性參數檔案，複製 hello [201 servicebus-建立-佇列](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json)檔案。 取代 hello 值`serviceBusNamespaceName`hello hello 服務匯流排命名空間名稱與您想要此部署中 toocreate 值，取代成 hello`serviceBusQueueName`想 toocreate hello hello 佇列名稱。

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

如需詳細資訊，請參閱 hello[參數](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)主題。

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>登入 tooAzure 並設定 hello Azure 訂用帳戶

從 PowerShell 提示中，執行下列命令的 hello:

```powershell
Login-AzureRmAccount
```

您必須提示的 toolog tooyour Azure 帳戶上。 登入之後，執行下列命令 tooview hello 您可用的訂用帳戶。

```powershell
Get-AzureRMSubscription
```

這個命令會傳回可用的 Azure 訂用帳戶清單。 藉由執行下列命令的 hello 選擇訂閱 hello 目前工作階段。 取代`<YourSubscriptionId>`想 toouse hello GUID hello Azure 訂用帳戶。

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>設定 hello 資源群組

如果您沒有現有的資源群組中，建立新的資源群組以 hello * * 新增 AzureRmResourceGroup * * 命令。 提供 hello 名稱 hello 資源群組及您想要 toouse 的位置。 例如：

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

如果成功，則會顯示 hello 新資源群組的摘要。

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>測試 hello 部署

驗證您的部署執行 hello `Test-AzureRmResourceGroupDeployment` cmdlet。 測試時部署 hello，請在相同的方式執行 hello 部署時提供參數。

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>建立 hello 部署

toocreate hello 新的部署，執行 hello `New-AzureRmResourceGroupDeployment` cmdlet，並提供出現提示時，即 hello 必要參數。 hello 參數包括您的部署，您的資源群組和 hello 路徑或 URL toohello 範本檔案的 hello 名稱的名稱。 如果 hello**模式**未指定參數，hello 預設值是**Incremental**用。 如需詳細資訊，請參閱[累加部署與完整部署](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)。

hello 下列命令會提示您 hello PowerShell 視窗中的 hello 三個參數：

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify 參數檔案，請使用下列命令的 hello。

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

當您執行 hello 部署 cmdlet 時，您也可以使用內嵌參數。 hello 命令如下所示：

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun[完成](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)部署、 設定 hello**模式**參數太**完成**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>確認 hello 部署
如果已成功部署 hello 資源，hello 部署的摘要會顯示 hello PowerShell 視窗中：

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>後續步驟
您現在已經瞭解 hello 基本工作流程和部署 Azure Resource Manager 範本的命令。 如需詳細資訊，請造訪下列連結查看 hello:

* [Azure Resource Manager 概觀][Azure Resource Manager overview]
* [使用 Resource Manager 範本與 Azure PowerShell 來部署資源][Deploy resources with Azure Resource Manager templates]
* [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
