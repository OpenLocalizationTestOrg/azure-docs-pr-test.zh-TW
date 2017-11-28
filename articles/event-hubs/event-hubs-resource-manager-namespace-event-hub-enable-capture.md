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
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="2523c-103">使用 Azure Resource Manager 範本建立含有一個事件中樞的事件中樞命名空間並啟用擷取</span><span class="sxs-lookup"><span data-stu-id="2523c-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="2523c-104">本文示範如何 toouse Azure Resource Manager 範本，建立事件中樞命名空間與一個事件中樞執行個體，也可讓 hello[擷取功能](event-hubs-capture-overview.md)hello 事件中心上。</span><span class="sxs-lookup"><span data-stu-id="2523c-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="2523c-105">hello 文章說明如何 toodefine 部署的資源，以及所 toodefine 參數指定 hello 部署執行時的方式。</span><span class="sxs-lookup"><span data-stu-id="2523c-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="2523c-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="2523c-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="2523c-107">這也文章 toospecify 到 Azure 儲存體 Blob 或 Azure 資料湖存放區中，確定已擷取事件根據 hello 的方式顯示您所選擇的目的地。</span><span class="sxs-lookup"><span data-stu-id="2523c-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="2523c-108">如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="2523c-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="2523c-109">如需 Azure 資源命名慣例相關模式和實務的詳細資訊，請參閱 [Azure 資源命名慣例][Azure Resources naming conventions]。</span><span class="sxs-lookup"><span data-stu-id="2523c-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="2523c-110">Hello 完成範本，按一下下列 GitHub 連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="2523c-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="2523c-111">[事件中樞，並啟用擷取 tooStorage 範本][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="2523c-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="2523c-112">[事件中樞，並啟用擷取 tooAzure Data Lake Store 的範本][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="2523c-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="2523c-113">toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋事件中心。</span><span class="sxs-lookup"><span data-stu-id="2523c-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="2523c-114">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="2523c-114">What will you deploy?</span></span>

<span data-ttu-id="2523c-115">使用此範本，您可部署含有事件中樞的事件中樞命名空間，也可啟用[事件中樞擷取](event-hubs-capture-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2523c-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="2523c-116">[事件中心](event-hubs-what-is-event-hubs.md)是處理用的服務 tooprovide 事件和遙測 ingress tooAzure 大規模、 可靠性高且延遲低的事件。</span><span class="sxs-lookup"><span data-stu-id="2523c-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="2523c-117">事件中心擷取可讓您 tooautomatically 傳送 hello 資料流處理指定的時間或您所選擇的大小間隔內的 事件中心 tooAzure Blob 儲存體中的資料或 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="2523c-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="2523c-118">按一下下列按鈕 tooenable 事件中心擷取到 Azure 儲存體的 hello:</span><span class="sxs-lookup"><span data-stu-id="2523c-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="2523c-119">[![部署 tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2523c-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="2523c-120">按一下下列按鈕 tooenable 事件中心擷取至 Azure Data Lake Store 的 hello:</span><span class="sxs-lookup"><span data-stu-id="2523c-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="2523c-121">[![部署 tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2523c-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="2523c-122">參數</span><span class="sxs-lookup"><span data-stu-id="2523c-122">Parameters</span></span>

<span data-ttu-id="2523c-123">使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="2523c-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="2523c-124">hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="2523c-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="2523c-125">您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境不同，這些值的參數。</span><span class="sxs-lookup"><span data-stu-id="2523c-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="2523c-126">不會定義參數的值一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="2523c-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="2523c-127">每個參數值用於 hello 範本 toodefine hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="2523c-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="2523c-128">hello 範本會定義下列參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="2523c-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="2523c-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="2523c-129">eventHubNamespaceName</span></span>

<span data-ttu-id="2523c-130">hello hello 名稱[事件中樞命名空間](event-hubs-create.md)toocreate。</span><span class="sxs-lookup"><span data-stu-id="2523c-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="2523c-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="2523c-131">eventHubName</span></span>

<span data-ttu-id="2523c-132">hello hello 中建立的事件中樞 hello 名稱[事件中樞命名空間](event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="2523c-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="2523c-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="2523c-133">messageRetentionInDays</span></span>

<span data-ttu-id="2523c-134">hello hello 事件中樞中的天數 tooretain hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="2523c-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

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

### <a name="partitioncount"></a><span data-ttu-id="2523c-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="2523c-135">partitionCount</span></span>

<span data-ttu-id="2523c-136">hello hello 事件中樞中的資料分割 toocreate 數目。</span><span class="sxs-lookup"><span data-stu-id="2523c-136">hello number of partitions toocreate in hello event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="2523c-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="2523c-137">captureEnabled</span></span>

<span data-ttu-id="2523c-138">啟用擷取 hello 事件中心上。</span><span class="sxs-lookup"><span data-stu-id="2523c-138">Enable Capture on hello event hub.</span></span>

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
### <a name="captureencodingformat"></a><span data-ttu-id="2523c-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="2523c-139">captureEncodingFormat</span></span>

<span data-ttu-id="2523c-140">hello 指定 tooserialize hello 事件資料的編碼格式。</span><span class="sxs-lookup"><span data-stu-id="2523c-140">hello encoding format you specify tooserialize hello event data.</span></span>

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

### <a name="capturetime"></a><span data-ttu-id="2523c-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="2523c-141">captureTime</span></span>

<span data-ttu-id="2523c-142">hello 擷取的事件中心開始的 hello 資料擷取的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="2523c-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

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

### <a name="capturesize"></a><span data-ttu-id="2523c-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="2523c-143">captureSize</span></span>
<span data-ttu-id="2523c-144">hello 大小間隔擷取啟動擷取 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2523c-144">hello size interval at which Capture starts capturing hello data.</span></span>

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

###<a name="capturenameformat"></a><span data-ttu-id="2523c-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="2523c-145">captureNameFormat</span></span>

<span data-ttu-id="2523c-146">事件中心擷取 toowrite hello Avro 檔案所使用的 hello 名稱格式。</span><span class="sxs-lookup"><span data-stu-id="2523c-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="2523c-147">請注意，擷取名稱格式必須包含 `{Namespace}`、`{EventHub}`、`{PartitionId}`、`{Year}`、`{Month}`、`{Day}`、`{Hour}`、`{Minute}` 和 `{Second}` 欄位。</span><span class="sxs-lookup"><span data-stu-id="2523c-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="2523c-148">這些欄位可以依任何順序排列 (不論是否有分隔符號)。</span><span class="sxs-lookup"><span data-stu-id="2523c-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="2523c-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2523c-149">apiVersion</span></span>

<span data-ttu-id="2523c-150">hello 範本 hello API 版本。</span><span class="sxs-lookup"><span data-stu-id="2523c-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="2523c-151">使用下列參數，如果您選擇 Azure 儲存體做為目的地的 hello。</span><span class="sxs-lookup"><span data-stu-id="2523c-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="2523c-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="2523c-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="2523c-153">擷取需要擷取 tooyour Azure 儲存體帳戶資源識別碼 tooenable 所需的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2523c-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="2523c-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="2523c-154">blobContainerName</span></span>

<span data-ttu-id="2523c-155">hello blob 容器中哪些 toocapture 事件資料。</span><span class="sxs-lookup"><span data-stu-id="2523c-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="2523c-156">使用下列參數，如果您選擇做為目的地的 Azure Data Lake Store 的 hello。</span><span class="sxs-lookup"><span data-stu-id="2523c-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="2523c-157">您必須在您想 tooCapture hello 事件的資料湖存放區路徑上設定權限。</span><span class="sxs-lookup"><span data-stu-id="2523c-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="2523c-158">tooset 權限，請參閱[本文](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account)。</span><span class="sxs-lookup"><span data-stu-id="2523c-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="2523c-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="2523c-159">subscriptionId</span></span>

<span data-ttu-id="2523c-160">Hello 事件中樞命名空間和 Azure Data Lake Store 的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="2523c-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="2523c-161">這兩個這些資源必須受到 hello 相同的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="2523c-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="2523c-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="2523c-162">dataLakeAccountName</span></span>

<span data-ttu-id="2523c-163">hello hello Azure 資料湖存放區名稱擷取的事件。</span><span class="sxs-lookup"><span data-stu-id="2523c-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="2523c-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="2523c-164">dataLakeFolderPath</span></span>

<span data-ttu-id="2523c-165">hello hello 目的地資料夾路徑擷取的事件。</span><span class="sxs-lookup"><span data-stu-id="2523c-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="2523c-166">將 toodeploy Azure 儲存體資源做為目的地 toocaptured 事件</span><span class="sxs-lookup"><span data-stu-id="2523c-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="2523c-167">建立類型的命名空間**EventHubs**、 與一個事件中心，而且也可讓您擷取 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2523c-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

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

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="2523c-168">Azure 資料湖存放區做為目的地資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="2523c-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="2523c-169">建立類型的命名空間**EventHubs**、 與一個事件中心，而且也可讓您擷取 tooAzure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="2523c-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="2523c-170">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="2523c-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="2523c-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2523c-171">PowerShell</span></span>

<span data-ttu-id="2523c-172">將事件中樞擷取您範本 tooenable 部署到 Azure 儲存體：</span><span class="sxs-lookup"><span data-stu-id="2523c-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="2523c-173">將事件中樞擷取您範本 tooenable 部署至 Azure 資料湖存放區：</span><span class="sxs-lookup"><span data-stu-id="2523c-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="2523c-174">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2523c-174">Azure CLI</span></span>

<span data-ttu-id="2523c-175">選擇 Azure Blob 儲存體作為目的地：</span><span class="sxs-lookup"><span data-stu-id="2523c-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="2523c-176">選擇 Azure Data Lake Store 作為目的地：</span><span class="sxs-lookup"><span data-stu-id="2523c-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="2523c-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2523c-177">Next steps</span></span>

<span data-ttu-id="2523c-178">您也可以設定事件中樞擷取透過 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2523c-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2523c-179">如需詳細資訊，請參閱[啟用事件中心擷取使用 hello Azure 入口網站](event-hubs-capture-enable-through-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2523c-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="2523c-180">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="2523c-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="2523c-181">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="2523c-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2523c-182">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="2523c-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="2523c-183">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="2523c-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
