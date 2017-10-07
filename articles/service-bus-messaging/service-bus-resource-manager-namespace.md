---
title: "使用 Azure Resource Manager 範本 aaaCreate 服務匯流排命名空間 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 toocreate 服務匯流排命名空間"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本來建立服務匯流排命名空間

本文說明如何 toouse Azure Resource Manager 範本建立服務匯流排命名空間的型別**傳訊**與 Standard/Basic SKU。 hello 發行項也會定義 hello 參數所指定的 hello 部署的 hello 執行。 您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。

如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。

Hello 完成範本，請參閱 hello[服務匯流排命名空間範本][ Service Bus namespace template] GitHub 上。

> [!NOTE]
> hello 下列 Azure 資源管理員範本可供下載和部署。 
> 
> * [建立服務匯流排命名空間與佇列](service-bus-resource-manager-namespace-queue.md)
> * [建立服務匯流排命名空間與主題和訂用帳戶](service-bus-resource-manager-namespace-topic.md)
> * [建立服務匯流排命名空間與佇列和授權規則](service-bus-resource-manager-namespace-auth-rule.md)
> * [建立服務匯流排命名空間與主題、訂用帳戶和規則](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋服務匯流排。
> 
> 

## <a name="what-will-you-deploy"></a>您將部署什麼？
使用此範本時，您將部署具有[基本、標準或進階](https://azure.microsoft.com/pricing/details/service-bus/) SKU 的「服務匯流排」命名空間。

toorun 自動 hello 部署，請按一下下列按鈕 hello:

[![部署 tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)

## <a name="parameters"></a>參數
使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。 hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。 您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。 不會定義參數的值，會一律保持 hello 相同。 每個參數值用於 hello 範本 toodefine hello 資源部署。

此範本會定義下列參數的 hello。

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
hello 服務匯流排命名空間 toocreate hello 名稱。

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a>serviceBusSKU
服務匯流排 hello hello 名稱[SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate。

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

hello 範本可定義 hello （Basic、 Standard 或 Premium），此參數允許的值，並指派的預設值 （標準），如果未不指定任何值。

如需服務匯流排定價的詳細資訊，請參閱[服務匯流排定價與計費][Service Bus pricing and billing]。

### <a name="servicebusapiversion"></a>serviceBusApiVersion
hello hello 範本的服務匯流排 API 版本。

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a>資源 toodeploy
### <a name="service-bus-namespace"></a>服務匯流排命名空間
建立 **訊息**類型的標準服務匯流排命名空間。

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a>命令 toorun 部署
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a>後續步驟
既然您已經建立及部署使用 Azure 資源管理員的資源，了解如何 toomanage 這些資源，藉由讀取這些文件：

* [使用 PowerShell 管理服務匯流排](service-bus-manage-with-ps.md)
* [管理 Service Bus Explorer hello 與服務匯流排資源](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
