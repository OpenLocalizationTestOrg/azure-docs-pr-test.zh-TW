---
title: "aaaCreate Azure 服務匯流排命名空間主題訂用帳戶使用 Azure Resource Manager 範本 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題和訂用帳戶"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題和訂用帳戶

本文示範如何 toouse Azure Resource Manager 範本，建立服務匯流排命名空間的主題和訂用帳戶，該命名空間中。 您將學習如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。 您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求

如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。

Hello 完成範本，請參閱 hello[主題和訂用帳戶的服務匯流排命名空間][ Service Bus namespace with topic and subscription]範本。

> [!NOTE]
> hello 下列 Azure 資源管理員範本可供下載和部署。
> 
> * [建立服務匯流排命名空間](service-bus-resource-manager-namespace.md)
> * [建立服務匯流排命名空間與佇列](service-bus-resource-manager-namespace-queue.md)
> * [建立服務匯流排命名空間與佇列和授權規則](service-bus-resource-manager-namespace-auth-rule.md)
> * [建立服務匯流排命名空間與主題、訂用帳戶和規則](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋 「 Service Bus 」。
> 
> 

## <a name="what-will-you-deploy"></a>您將部署什麼？

使用此範本，您將部署具有主題和訂用帳戶的服務匯流排命名空間。

[服務匯流排主題和訂用帳戶](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)使用「發佈/訂閱」模式，提供一對多的通訊形式。

toorun 自動 hello 部署，請按一下下列按鈕 hello:

[![部署 tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)

## <a name="parameters"></a>參數

使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。 hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。 您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。 不會定義參數的值，會一律保持 hello 相同。 每個參數值用於 hello 範本 toodefine hello 資源部署。

hello 範本會定義下列參數的 hello。

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
hello 服務匯流排命名空間 toocreate hello 名稱。

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
hello hello hello 服務匯流排命名空間中建立的主題名稱。

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
hello 建立 hello 服務匯流排命名空間中的 hello 訂用帳戶的名稱。

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
hello hello 範本的服務匯流排 API 版本。

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a>資源 toodeploy
建立 **訊息**類型的標準服務匯流排命名空間與主題和訂用帳戶。

```json
"resources ": [{
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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>命令 toorun 部署
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a>後續步驟
既然您已經建立及部署使用 Azure 資源管理員的資源，了解如何 toomanage 檢視這些文件的下列資源：

* [使用 PowerShell 管理服務匯流排](service-bus-manage-with-ps.md)
* [管理 Service Bus Explorer hello 與服務匯流排資源](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
