---
title: "Azure 事件中樞命名空間，並啟用擷取使用範本 aaaCreate |Microsoft 文件"
description: "使用 Azure Resource Manager 範本建立含有一個事件中樞的 Azure 事件中樞命名空間並啟用擷取"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本建立含有一個事件中樞的事件中樞命名空間並啟用擷取

本文示範如何 toouse Azure Resource Manager 範本，建立事件中樞命名空間與一個事件中樞執行個體，也可讓 hello[擷取功能](event-hubs-capture-overview.md)hello 事件中心上。 hello 文章說明如何 toodefine 部署的資源，以及所 toodefine 參數指定 hello 部署執行時的方式。 您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。

這也文章 toospecify 到 Azure 儲存體 Blob 或 Azure 資料湖存放區中，確定已擷取事件根據 hello 的方式顯示您所選擇的目的地。

如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。

如需 Azure 資源命名慣例相關模式和實務的詳細資訊，請參閱 [Azure 資源命名慣例][Azure Resources naming conventions]。

Hello 完成範本，按一下下列 GitHub 連結查看 hello:

- [事件中樞，並啟用擷取 tooStorage 範本][Event Hub and enable Capture tooStorage template] 
- [事件中樞，並啟用擷取 tooAzure Data Lake Store 的範本][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋事件中心。
> 
> 

## <a name="what-will-you-deploy"></a>您將部署什麼？

使用此範本，您可部署含有事件中樞的事件中樞命名空間，也可啟用[事件中樞擷取](event-hubs-capture-overview.md)。

[事件中心](event-hubs-what-is-event-hubs.md)是處理用的服務 tooprovide 事件和遙測 ingress tooAzure 大規模、 可靠性高且延遲低的事件。 事件中心擷取可讓您 tooautomatically 傳送 hello 資料流處理指定的時間或您所選擇的大小間隔內的 事件中心 tooAzure Blob 儲存體中的資料或 Azure 資料湖存放區。

按一下下列按鈕 tooenable 事件中心擷取到 Azure 儲存體的 hello:

[![部署 tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

按一下下列按鈕 tooenable 事件中心擷取至 Azure Data Lake Store 的 hello:

[![部署 tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>參數

使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。 hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。 您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境不同，這些值的參數。 不會定義參數的值一律保持 hello 相同。 每個參數值用於 hello 範本 toodefine hello 資源部署。

hello 範本會定義下列參數的 hello。

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

hello hello 名稱[事件中樞命名空間](event-hubs-create.md)toocreate。

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

hello hello 中建立的事件中樞 hello 名稱[事件中樞命名空間](event-hubs-create.md)。

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

hello hello 事件中樞中的天數 tooretain hello 訊息數目。 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

hello hello 事件中樞中的資料分割 toocreate 數目。

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

啟用擷取 hello 事件中心上。

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

hello 指定 tooserialize hello 事件資料的編碼格式。

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

hello 擷取的事件中心開始的 hello 資料擷取的時間間隔。

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
hello 大小間隔擷取啟動擷取 hello 資料。

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

事件中心擷取 toowrite hello Avro 檔案所使用的 hello 名稱格式。 請注意，擷取名稱格式必須包含 `{Namespace}`、`{EventHub}`、`{PartitionId}`、`{Year}`、`{Month}`、`{Day}`、`{Hour}`、`{Minute}` 和 `{Second}` 欄位。 這些欄位可以依任何順序排列 (不論是否有分隔符號)。
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

hello 範本 hello API 版本。

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

使用下列參數，如果您選擇 Azure 儲存體做為目的地的 hello。

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

擷取需要擷取 tooyour Azure 儲存體帳戶資源識別碼 tooenable 所需的儲存體帳戶。

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

hello blob 容器中哪些 toocapture 事件資料。

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

使用下列參數，如果您選擇做為目的地的 Azure Data Lake Store 的 hello。 您必須在您想 tooCapture hello 事件的資料湖存放區路徑上設定權限。 tooset 權限，請參閱[本文](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account)。

###<a name="subscriptionid"></a>subscriptionId

Hello 事件中樞命名空間和 Azure Data Lake Store 的訂用帳戶 ID。 這兩個這些資源必須受到 hello 相同的訂用帳戶識別碼。

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

hello hello Azure 資料湖存放區名稱擷取的事件。

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

hello hello 目的地資料夾路徑擷取的事件。

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>將 toodeploy Azure 儲存體資源做為目的地 toocaptured 事件

建立類型的命名空間**EventHubs**、 與一個事件中心，而且也可讓您擷取 tooAzure Blob 儲存體。

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Azure 資料湖存放區做為目的地資源 toodeploy

建立類型的命名空間**EventHubs**、 與一個事件中心，而且也可讓您擷取 tooAzure 資料湖存放區。

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>命令 toorun 部署

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

將事件中樞擷取您範本 tooenable 部署到 Azure 儲存體：
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

將事件中樞擷取您範本 tooenable 部署至 Azure 資料湖存放區：

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>Azure CLI

選擇 Azure Blob 儲存體作為目的地：

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

選擇 Azure Data Lake Store 作為目的地：

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>後續步驟

您也可以設定事件中樞擷取透過 hello [Azure 入口網站](https://portal.azure.com)。 如需詳細資訊，請參閱[啟用事件中心擷取使用 hello Azure 入口網站](event-hubs-capture-enable-through-portal.md)。

您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
