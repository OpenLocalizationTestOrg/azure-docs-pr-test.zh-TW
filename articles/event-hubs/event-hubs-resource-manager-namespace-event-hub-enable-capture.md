---
title: "使用範本來建立 Azure 事件中樞命名空間並啟用擷取 | Microsoft Docs"
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
ms.openlocfilehash: 19bbb51868e767aa1d15f4574628b7fd36607207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="ed6ca-103">使用 Azure Resource Manager 範本建立含有一個事件中樞的事件中樞命名空間並啟用擷取</span><span class="sxs-lookup"><span data-stu-id="ed6ca-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="ed6ca-104">本文說明如何使用 Azure Resource Manager 範本來建立含有一個事件中樞執行個體的事件中樞命名空間，也可在該事件中樞上啟用[擷取功能](event-hubs-capture-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-104">This article shows how to use an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub.</span></span> <span data-ttu-id="ed6ca-105">此文章說明如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-105">The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="ed6ca-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="ed6ca-107">本文也會示範如何根據您選擇的目的地，指定將事件擷取到 Azure 儲存體 Blob 或 Azure Data Lake Store 中。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-107">This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.</span></span>

<span data-ttu-id="ed6ca-108">如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="ed6ca-109">如需 Azure 資源命名慣例相關模式和實務的詳細資訊，請參閱 [Azure 資源命名慣例][Azure Resources naming conventions]。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="ed6ca-110">對於所有範本，按一下下列 GitHub 連結：</span><span class="sxs-lookup"><span data-stu-id="ed6ca-110">For the complete templates, click the following GitHub links:</span></span>

- <span data-ttu-id="ed6ca-111">[事件中樞和啟用擷取至儲存體範本][Event Hub and enable Capture to Storage template]</span><span class="sxs-lookup"><span data-stu-id="ed6ca-111">[Event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]</span></span> 
- <span data-ttu-id="ed6ca-112">[事件中樞和啟用擷取至 Azure Data Lake Store 範本][Event Hub and enable Capture to Azure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="ed6ca-112">[Event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="ed6ca-113">若要檢查最新的範本，請造訪 [Azure 快速入門範本][Azure Quickstart Templates] 資源庫並搜尋事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-113">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="ed6ca-114">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="ed6ca-114">What will you deploy?</span></span>

<span data-ttu-id="ed6ca-115">使用此範本，您可部署含有事件中樞的事件中樞命名空間，也可啟用[事件中樞擷取](event-hubs-capture-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="ed6ca-116">[事件中樞](event-hubs-what-is-event-hubs.md) 是事件處理服務，用於提供大規模進入 Azure 的事件和遙測入口，並具備低延遲和高可靠性等特性。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="ed6ca-117">事件中樞擷取功能讓您能夠在指定時間或大小間隔內，自動將事件中樞的串流資料傳遞到 Azure Blob 儲存體或 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-117">Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="ed6ca-118">按一下以下按鈕來啟用「事件中心擷取到 Azure 儲存體中」：</span><span class="sxs-lookup"><span data-stu-id="ed6ca-118">Click the following button to enable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="ed6ca-119">[![部署至 Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ed6ca-119">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="ed6ca-120">按一下以下按鈕來啟用「事件中心擷取到 Azure Data Lake Store 中」：</span><span class="sxs-lookup"><span data-stu-id="ed6ca-120">Click the following button to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="ed6ca-121">[![部署至 Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ed6ca-121">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="ed6ca-122">參數</span><span class="sxs-lookup"><span data-stu-id="ed6ca-122">Parameters</span></span>

<span data-ttu-id="ed6ca-123">透過 Azure 資源管理員，您可以定義在部署範本時想要指定之值的參數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="ed6ca-124">此範本有一個 `Parameters` 區段，內含所有參數值。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-124">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="ed6ca-125">您應該為會隨著要部署的專案或要部署到的環境而變化的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-125">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="ed6ca-126">請不要為永遠保持不變的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-126">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="ed6ca-127">每個參數值都可在範本中用來定義所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="ed6ca-128">範本會定義下列參數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-128">The template defines the following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="ed6ca-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="ed6ca-129">eventHubNamespaceName</span></span>

<span data-ttu-id="ed6ca-130">要建立的[事件中樞命名空間](event-hubs-create.md)名稱。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-130">The name of the [Event Hubs namespace](event-hubs-create.md) to create.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of the EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="ed6ca-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="ed6ca-131">eventHubName</span></span>

<span data-ttu-id="ed6ca-132">在[事件中樞命名空間](event-hubs-create.md)中建立的事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-132">The name of the event hub created in the [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of the event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="ed6ca-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="ed6ca-133">messageRetentionInDays</span></span>

<span data-ttu-id="ed6ca-134">要在事件中樞中保留訊息的天數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-134">The number of days to retain the messages in the event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long to retain the data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="ed6ca-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="ed6ca-135">partitionCount</span></span>

<span data-ttu-id="ed6ca-136">要在事件中樞中建立的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-136">The number of partitions to create in the event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="ed6ca-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="ed6ca-137">captureEnabled</span></span>

<span data-ttu-id="ed6ca-138">在事件中樞上啟用封存擷取功能。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-138">Enable Capture on the event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable the Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="ed6ca-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="ed6ca-139">captureEncodingFormat</span></span>

<span data-ttu-id="ed6ca-140">您指定用來將事件資料序列化的編碼格式。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-140">The encoding format you specify to serialize the event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"The encoding format in which Capture serializes the EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="ed6ca-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="ed6ca-141">captureTime</span></span>

<span data-ttu-id="ed6ca-142">事件中樞擷取功能開始擷取資料的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-142">The time interval in which Event Hubs Capture starts capturing the data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"the time window in seconds for the capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="ed6ca-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="ed6ca-143">captureSize</span></span>
<span data-ttu-id="ed6ca-144">擷取功能開始擷取資料的大小間隔。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-144">The size interval at which Capture starts capturing the data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"The size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="ed6ca-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="ed6ca-145">captureNameFormat</span></span>

<span data-ttu-id="ed6ca-146">事件中樞擷取功能用來寫入 Avro 檔案的名稱格式。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-146">The name format used by Event Hubs Capture to write the Avro files.</span></span> <span data-ttu-id="ed6ca-147">請注意，擷取名稱格式必須包含 `{Namespace}`、`{EventHub}`、`{PartitionId}`、`{Year}`、`{Month}`、`{Day}`、`{Hour}`、`{Minute}` 和 `{Second}` 欄位。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="ed6ca-148">這些欄位可以依任何順序排列 (不論是否有分隔符號)。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="ed6ca-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="ed6ca-149">apiVersion</span></span>

<span data-ttu-id="ed6ca-150">範本的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-150">The API version of the template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by the template"
    }
 }
```

<span data-ttu-id="ed6ca-151">如果您選擇 Azure 儲存體作為目的地，請使用下列參數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-151">Use the following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="ed6ca-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="ed6ca-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="ed6ca-153">擷取功能需要有 Azure 儲存體帳戶資源識別碼，才能為您所需的儲存體帳戶啟用擷取功能。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-153">Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want the blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="ed6ca-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="ed6ca-154">blobContainerName</span></span>

<span data-ttu-id="ed6ca-155">用來擷取存事件資料的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-155">The blob container in which to capture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want the blobs captured"
    }
}
```

<span data-ttu-id="ed6ca-156">如果您選擇 Azure Data Lake Store 作為目的地，請使用下列參數。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-156">Use the following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="ed6ca-157">您必須在您想要擷取事件的 Data Lake Store 路徑上設定權限。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-157">You must set permissions on your Data Lake Store path, in which you want to Capture the event.</span></span> <span data-ttu-id="ed6ca-158">若要設定權限，請參閱[本文](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account)。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-158">To set permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="ed6ca-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="ed6ca-159">subscriptionId</span></span>

<span data-ttu-id="ed6ca-160">事件中樞命名空間和 Azure Data Lake Store 的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-160">Subscription ID for the Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="ed6ca-161">這兩個資源都必須屬於同一個訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-161">Both these resources must be under the same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="ed6ca-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="ed6ca-162">dataLakeAccountName</span></span>

<span data-ttu-id="ed6ca-163">已擷取事件的 Azure Data Lake Store 名稱。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-163">The Azure Data Lake Store name for the captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="ed6ca-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="ed6ca-164">dataLakeFolderPath</span></span>

<span data-ttu-id="ed6ca-165">已擷取事件的目的地資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-165">The destination folder path for the captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-to-deploy-for-azure-storage-as-destination-to-captured-events"></a><span data-ttu-id="ed6ca-166">要針對 Azure 儲存體部署為已擷取事件之目的地的資源</span><span class="sxs-lookup"><span data-stu-id="ed6ca-166">Resources to deploy for Azure Storage as destination to captured events</span></span>

<span data-ttu-id="ed6ca-167">建立類型為 **EventHubs**、含有一個事件中樞，而且也會啟用「擷取至 Azure Blob 儲存體」功能的命名空間。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Blob Storage.</span></span>

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

## <a name="resources-to-deploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="ed6ca-168">要針對 Azure Data Lake Store 部署為目的地的資源</span><span class="sxs-lookup"><span data-stu-id="ed6ca-168">Resources to deploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="ed6ca-169">建立類型為 **EventHubs**、含有一個事件中樞，而且也會啟用「擷取至 Azure Data Lake Store」功能的命名空間。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Data Lake Store.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="ed6ca-170">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="ed6ca-170">Commands to run deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="ed6ca-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed6ca-171">PowerShell</span></span>

<span data-ttu-id="ed6ca-172">部署您的範本，以啟用「事件中樞擷取至 Azure 儲存體」功能：</span><span class="sxs-lookup"><span data-stu-id="ed6ca-172">Deploy your template to enable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="ed6ca-173">部署您的範本，以啟用「事件中樞擷取至 Azure Data Lake Store」功能：</span><span class="sxs-lookup"><span data-stu-id="ed6ca-173">Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="ed6ca-174">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ed6ca-174">Azure CLI</span></span>

<span data-ttu-id="ed6ca-175">選擇 Azure Blob 儲存體作為目的地：</span><span class="sxs-lookup"><span data-stu-id="ed6ca-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="ed6ca-176">選擇 Azure Data Lake Store 作為目的地：</span><span class="sxs-lookup"><span data-stu-id="ed6ca-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="ed6ca-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed6ca-177">Next steps</span></span>

<span data-ttu-id="ed6ca-178">您也可以透過 [Azure 入口網站](https://portal.azure.com)設定事件中樞擷取功能。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-178">You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ed6ca-179">如需詳細資訊，請參閱[使用 Azure 入口網站啟用事件中樞擷取功能](event-hubs-capture-enable-through-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ed6ca-179">For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="ed6ca-180">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="ed6ca-180">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="ed6ca-181">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="ed6ca-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ed6ca-182">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="ed6ca-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ed6ca-183">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="ed6ca-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture to Storage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture to Azure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls