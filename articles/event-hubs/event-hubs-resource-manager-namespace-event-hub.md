---
title: "使用範本的 Azure 事件中樞命名空間和取用者群組 aaaCreate |Microsoft 文件"
description: "使用 Azure Resource Manager 範本來建立含有事件中樞和取用者群組的事件中樞命名空間"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本，以事件中樞和取用者群組來建立事件中樞命名空間

本文將說明如何 toouse Azure Resource Manager 範本所建立的命名空間類型事件中心的一個事件中樞與一個取用者群組。 hello 文章顯示如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。 您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求

如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。

Hello 完成範本，請參閱 hello[事件中樞與取用者群組範本][ Event Hub and consumer group template] GitHub 上。

> [!NOTE]
> toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋事件中心。
> 
> 

## <a name="what-will-you-deploy"></a>您將部署什麼？
藉由此範本，您將部署含有事件中樞和取用者群組的「事件中樞」命名空間。

[事件中心](event-hubs-what-is-event-hubs.md)是處理用的服務 tooprovide 事件和遙測 ingress tooAzure 大規模、 可靠性高且延遲低的事件。

toorun 自動 hello 部署，請按一下下列按鈕 hello:

[![部署 tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)

## <a name="parameters"></a>參數
使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。 hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。 您應該定義將會不同，根據您要部署的 hello 專案，或根據您要部署的 hello 環境 toowhich 這些值的參數。 不會定義參數的值一律保持 hello 相同。 Hello 範本中的每個參數值定義部署的 hello 資源。

hello 範本會定義下列參數的 hello:

### <a name="eventhubnamespacename"></a>eventHubNamespaceName
hello 事件中樞命名空間 toocreate hello 名稱。

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a>eventHubName
hello hello hello 事件中樞命名空間中建立的事件中樞的名稱。

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a>eventHubConsumerGroupName
hello hello 事件中心建立的 hello 取用者群組的名稱。

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a>apiVersion
hello 範本 hello API 版本。

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>資源 toodeploy
建立類型為 **EventHubs**、含有事件中樞和取用者群組的命名空間。

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a>命令 toorun 部署
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a>Azure CLI
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
