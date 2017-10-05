---
title: "Azure Event Grid 事件結構描述"
description: "描述 Azure Event Grid 中事件提供的屬性。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 9e3c7b31ef23b29827d7184dc033227685ed92f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="bebe8-103">Event Grid 事件結構描述</span><span class="sxs-lookup"><span data-stu-id="bebe8-103">Event Grid event schema</span></span>

<span data-ttu-id="bebe8-104">本文提供事件之屬性與結構描述。</span><span class="sxs-lookup"><span data-stu-id="bebe8-104">This article provides the properties and schema for events.</span></span> <span data-ttu-id="bebe8-105">事件包含一組五個必要字串屬性和一個必要**資料**物件。</span><span class="sxs-lookup"><span data-stu-id="bebe8-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="bebe8-106">這些屬性通用於任何發行者的所有事件。</span><span class="sxs-lookup"><span data-stu-id="bebe8-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="bebe8-107">**資料**物件含有各發行者特有的屬性。</span><span class="sxs-lookup"><span data-stu-id="bebe8-107">The **data** object contains properties that are specific to each publisher.</span></span> <span data-ttu-id="bebe8-108">系統主題下的屬性專屬於資源提供者，像是儲存體或事件中樞。</span><span class="sxs-lookup"><span data-stu-id="bebe8-108">For system topics, these properties are specific to the resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="bebe8-109">事件會以陣列型態傳送至 Azure Event Grid，陣列中可包含多個事件物件。</span><span class="sxs-lookup"><span data-stu-id="bebe8-109">Events are sent to Azure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="bebe8-110">如果陣列中只有一個事件，則陣列長度為 1。</span><span class="sxs-lookup"><span data-stu-id="bebe8-110">If there is only a single event, the array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="bebe8-111">事件屬性</span><span class="sxs-lookup"><span data-stu-id="bebe8-111">Event properties</span></span>

<span data-ttu-id="bebe8-112">所有事件皆包含下列最高層級資料。</span><span class="sxs-lookup"><span data-stu-id="bebe8-112">All events will contain the same following top level data.</span></span>

| <span data-ttu-id="bebe8-113">屬性</span><span class="sxs-lookup"><span data-stu-id="bebe8-113">Property</span></span> | <span data-ttu-id="bebe8-114">類型</span><span class="sxs-lookup"><span data-stu-id="bebe8-114">Type</span></span> | <span data-ttu-id="bebe8-115">說明</span><span class="sxs-lookup"><span data-stu-id="bebe8-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="bebe8-116">主題</span><span class="sxs-lookup"><span data-stu-id="bebe8-116">topic</span></span> | <span data-ttu-id="bebe8-117">字串</span><span class="sxs-lookup"><span data-stu-id="bebe8-117">string</span></span> | <span data-ttu-id="bebe8-118">事件來源的完整資源路徑。</span><span class="sxs-lookup"><span data-stu-id="bebe8-118">Full resource path to the event source.</span></span> <span data-ttu-id="bebe8-119">此欄位不可寫入。</span><span class="sxs-lookup"><span data-stu-id="bebe8-119">This field is not writeable.</span></span> |
| <span data-ttu-id="bebe8-120">主旨</span><span class="sxs-lookup"><span data-stu-id="bebe8-120">subject</span></span> | <span data-ttu-id="bebe8-121">字串</span><span class="sxs-lookup"><span data-stu-id="bebe8-121">string</span></span> | <span data-ttu-id="bebe8-122">發行者定義事件主體的路徑。</span><span class="sxs-lookup"><span data-stu-id="bebe8-122">Publisher defined path to the event subject.</span></span> |
| <span data-ttu-id="bebe8-123">eventType</span><span class="sxs-lookup"><span data-stu-id="bebe8-123">eventType</span></span> | <span data-ttu-id="bebe8-124">字串</span><span class="sxs-lookup"><span data-stu-id="bebe8-124">string</span></span> | <span data-ttu-id="bebe8-125">此事件來源已註冊的事件類型之一。</span><span class="sxs-lookup"><span data-stu-id="bebe8-125">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="bebe8-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="bebe8-126">eventTime</span></span> | <span data-ttu-id="bebe8-127">字串</span><span class="sxs-lookup"><span data-stu-id="bebe8-127">string</span></span> | <span data-ttu-id="bebe8-128">事件產生的時間，以提供者之 UTC 時間為準。</span><span class="sxs-lookup"><span data-stu-id="bebe8-128">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="bebe8-129">id</span><span class="sxs-lookup"><span data-stu-id="bebe8-129">id</span></span> | <span data-ttu-id="bebe8-130">字串</span><span class="sxs-lookup"><span data-stu-id="bebe8-130">string</span></span> | <span data-ttu-id="bebe8-131">事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="bebe8-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="bebe8-132">data</span><span class="sxs-lookup"><span data-stu-id="bebe8-132">data</span></span> | <span data-ttu-id="bebe8-133">物件</span><span class="sxs-lookup"><span data-stu-id="bebe8-133">object</span></span> | <span data-ttu-id="bebe8-134">資源提供者特有的事件資料。</span><span class="sxs-lookup"><span data-stu-id="bebe8-134">Event data specific to the resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="bebe8-135">可用的事件來源</span><span class="sxs-lookup"><span data-stu-id="bebe8-135">Available event sources</span></span>

<span data-ttu-id="bebe8-136">下列事件來源透過 Event Grid 來發佈事件：</span><span class="sxs-lookup"><span data-stu-id="bebe8-136">The following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="bebe8-137">資源群組 (管理作業)</span><span class="sxs-lookup"><span data-stu-id="bebe8-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="bebe8-138">Azure 訂用帳戶 (管理作業)</span><span class="sxs-lookup"><span data-stu-id="bebe8-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="bebe8-139">事件中樞</span><span class="sxs-lookup"><span data-stu-id="bebe8-139">Event Hubs</span></span>
* <span data-ttu-id="bebe8-140">自訂主題</span><span class="sxs-lookup"><span data-stu-id="bebe8-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="bebe8-141">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bebe8-141">Azure Subscriptions</span></span>

<span data-ttu-id="bebe8-142">Azure 訂用帳戶現在可從 Azure Resource Manager 發出管理事件，像是在虛擬機器建立時或儲存體帳戶刪除時皆可使用此功能。</span><span class="sxs-lookup"><span data-stu-id="bebe8-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="bebe8-143">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="bebe8-143">Available event types</span></span>

- <span data-ttu-id="bebe8-144">**Microsoft.Resources.ResourceWriteSuccess**：在資源建立或更新作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="bebe8-145">**Microsoft.Resources.ResourceWriteFailure**：在資源建立或更新作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="bebe8-146">**Microsoft.Resources.ResourceWriteCancel**：在資源建立或更新作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="bebe8-147">**Microsoft.Resources.ResourceDeleteSuccess**：在資源刪除作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="bebe8-148">**Microsoft.Resources.ResourceDeleteFailure**：在資源刪除作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="bebe8-149">**Microsoft.Resources.ResourceDeleteCancel**：在資源刪除作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="bebe8-150">這會在範本部署取消時發生。</span><span class="sxs-lookup"><span data-stu-id="bebe8-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="bebe8-151">事件結構描述範例</span><span class="sxs-lookup"><span data-stu-id="bebe8-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="bebe8-152">資源群組</span><span class="sxs-lookup"><span data-stu-id="bebe8-152">Resource Groups</span></span>

<span data-ttu-id="bebe8-153">資源群組現在可從 Azure Resource Manager 發出管理事件，像是在虛擬機器建立時或儲存體帳戶刪除時皆可使用此功能。</span><span class="sxs-lookup"><span data-stu-id="bebe8-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="bebe8-154">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="bebe8-154">Available event types</span></span>

- <span data-ttu-id="bebe8-155">**Microsoft.Resources.ResourceWriteSuccess**：在資源建立或更新作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="bebe8-156">**Microsoft.Resources.ResourceWriteFailure**：在資源建立或更新作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="bebe8-157">**Microsoft.Resources.ResourceWriteCancel**：在資源建立或更新作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="bebe8-158">**Microsoft.Resources.ResourceDeleteSuccess**：在資源刪除作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="bebe8-159">**Microsoft.Resources.ResourceDeleteFailure**：在資源刪除作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="bebe8-160">**Microsoft.Resources.ResourceDeleteCancel**：在資源刪除作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="bebe8-161">這會在範本部署取消時發生。</span><span class="sxs-lookup"><span data-stu-id="bebe8-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="bebe8-162">事件範例</span><span class="sxs-lookup"><span data-stu-id="bebe8-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="bebe8-163">事件中樞</span><span class="sxs-lookup"><span data-stu-id="bebe8-163">Event Hubs</span></span>

<span data-ttu-id="bebe8-164">事件中樞事件目前只有在使用擷取功能自動傳送檔案至儲存體時發出。</span><span class="sxs-lookup"><span data-stu-id="bebe8-164">Event Hubs events are currently only emitted when a file is automatically sent to storage using the Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="bebe8-165">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="bebe8-165">Available event types</span></span>

- <span data-ttu-id="bebe8-166">**Microsoft.EventHub.CaptureFileCreated**：擷取檔案建立時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="bebe8-167">事件範例</span><span class="sxs-lookup"><span data-stu-id="bebe8-167">Example event</span></span>

<span data-ttu-id="bebe8-168">此範例顯示在擷取功能儲存檔案時引發之事件中樞事件的結構描述。</span><span class="sxs-lookup"><span data-stu-id="bebe8-168">This sample event shows the schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="bebe8-169">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="bebe8-169">Azure Blob Storage</span></span>

<span data-ttu-id="bebe8-170">Azure Blob 儲存體目前提供私人預覽，註冊後可與 Event Grid 整合使用。</span><span class="sxs-lookup"><span data-stu-id="bebe8-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="bebe8-171">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="bebe8-171">Available event types</span></span>

- <span data-ttu-id="bebe8-172">**Microsoft.Storage.BlobCreated**：blob 建立時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="bebe8-173">**Microsoft.Storage.BlobDeleted**：blob 刪除時引發。</span><span class="sxs-lookup"><span data-stu-id="bebe8-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="bebe8-174">事件範例</span><span class="sxs-lookup"><span data-stu-id="bebe8-174">Example event</span></span>

<span data-ttu-id="bebe8-175">此事件範例顯示建立 blob 時引發之儲存體事件的結構描述。</span><span class="sxs-lookup"><span data-stu-id="bebe8-175">This sample event shows the schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="bebe8-176">自訂主題</span><span class="sxs-lookup"><span data-stu-id="bebe8-176">Custom Topics</span></span>

<span data-ttu-id="bebe8-177">您自訂事件的資料承載由您定義，可用任何格式正確的 JSON 來進行。</span><span class="sxs-lookup"><span data-stu-id="bebe8-177">The data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="bebe8-178">最高層級的資料應包含與標準資源定義事件相同的欄位。</span><span class="sxs-lookup"><span data-stu-id="bebe8-178">The top level data should contain the same fields as standard resource defined events.</span></span> <span data-ttu-id="bebe8-179">在發佈事件至自訂主題時，您應考慮以幫助路由與篩選為目標建立事件的主體。</span><span class="sxs-lookup"><span data-stu-id="bebe8-179">When publishing events to custom topics you should consider modeling the subject of your events to aid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="bebe8-180">事件範例</span><span class="sxs-lookup"><span data-stu-id="bebe8-180">Example event</span></span>

<span data-ttu-id="bebe8-181">以下範例為自訂主題的事件：</span><span class="sxs-lookup"><span data-stu-id="bebe8-181">The following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="bebe8-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bebe8-182">Next steps</span></span>

* <span data-ttu-id="bebe8-183">若要初步了解事件格線，請參閱[什麼是事件格線？](overview.md)</span><span class="sxs-lookup"><span data-stu-id="bebe8-183">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="bebe8-184">若要了解 Event Grid 訂用帳戶的建立，請參閱 [Event Grid 訂用帳戶結構描述](subscription-creation-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="bebe8-184">To learn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
