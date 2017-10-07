---
title: "aaaAzure 事件方格事件結構描述"
description: "描述可供事件的 Azure 事件方格的 hello 屬性。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="0253c-103">Event Grid 事件結構描述</span><span class="sxs-lookup"><span data-stu-id="0253c-103">Event Grid event schema</span></span>

<span data-ttu-id="0253c-104">這篇文章提供 hello 屬性和結構描述的事件。</span><span class="sxs-lookup"><span data-stu-id="0253c-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="0253c-105">事件包含一組五個必要字串屬性和一個必要**資料**物件。</span><span class="sxs-lookup"><span data-stu-id="0253c-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="0253c-106">hello 屬性都是常見的 tooall 事件，從任何發行者。</span><span class="sxs-lookup"><span data-stu-id="0253c-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="0253c-107">hello**資料**物件包含特定 tooeach 發行者的屬性。</span><span class="sxs-lookup"><span data-stu-id="0253c-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="0253c-108">如需系統主題，這些屬性是特定 toohello 資源提供者，例如儲存體或事件中心。</span><span class="sxs-lookup"><span data-stu-id="0253c-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="0253c-109">事件可以包含多個事件物件的陣列中傳送 tooAzure 事件方格。</span><span class="sxs-lookup"><span data-stu-id="0253c-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="0253c-110">如果沒有單一事件，hello 陣列長度為 1。</span><span class="sxs-lookup"><span data-stu-id="0253c-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="0253c-111">事件屬性</span><span class="sxs-lookup"><span data-stu-id="0253c-111">Event properties</span></span>

<span data-ttu-id="0253c-112">所有事件都將都包含 hello 下列最上層資料相同。</span><span class="sxs-lookup"><span data-stu-id="0253c-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="0253c-113">屬性</span><span class="sxs-lookup"><span data-stu-id="0253c-113">Property</span></span> | <span data-ttu-id="0253c-114">類型</span><span class="sxs-lookup"><span data-stu-id="0253c-114">Type</span></span> | <span data-ttu-id="0253c-115">說明</span><span class="sxs-lookup"><span data-stu-id="0253c-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="0253c-116">主題</span><span class="sxs-lookup"><span data-stu-id="0253c-116">topic</span></span> | <span data-ttu-id="0253c-117">字串</span><span class="sxs-lookup"><span data-stu-id="0253c-117">string</span></span> | <span data-ttu-id="0253c-118">完整資源路徑 toohello 事件來源。</span><span class="sxs-lookup"><span data-stu-id="0253c-118">Full resource path toohello event source.</span></span> <span data-ttu-id="0253c-119">此欄位不可寫入。</span><span class="sxs-lookup"><span data-stu-id="0253c-119">This field is not writeable.</span></span> |
| <span data-ttu-id="0253c-120">主旨</span><span class="sxs-lookup"><span data-stu-id="0253c-120">subject</span></span> | <span data-ttu-id="0253c-121">字串</span><span class="sxs-lookup"><span data-stu-id="0253c-121">string</span></span> | <span data-ttu-id="0253c-122">發行者端定義的路徑 toohello 事件主體。</span><span class="sxs-lookup"><span data-stu-id="0253c-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="0253c-123">eventType</span><span class="sxs-lookup"><span data-stu-id="0253c-123">eventType</span></span> | <span data-ttu-id="0253c-124">字串</span><span class="sxs-lookup"><span data-stu-id="0253c-124">string</span></span> | <span data-ttu-id="0253c-125">其中一個 hello 註冊事件來源的事件類型。</span><span class="sxs-lookup"><span data-stu-id="0253c-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="0253c-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="0253c-126">eventTime</span></span> | <span data-ttu-id="0253c-127">字串</span><span class="sxs-lookup"><span data-stu-id="0253c-127">string</span></span> | <span data-ttu-id="0253c-128">hello 時間 hello 事件會產生 hello 提供者的 UTC 時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="0253c-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="0253c-129">id</span><span class="sxs-lookup"><span data-stu-id="0253c-129">id</span></span> | <span data-ttu-id="0253c-130">字串</span><span class="sxs-lookup"><span data-stu-id="0253c-130">string</span></span> | <span data-ttu-id="0253c-131">Hello 事件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0253c-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="0253c-132">data</span><span class="sxs-lookup"><span data-stu-id="0253c-132">data</span></span> | <span data-ttu-id="0253c-133">物件</span><span class="sxs-lookup"><span data-stu-id="0253c-133">object</span></span> | <span data-ttu-id="0253c-134">事件資料特定 toohello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="0253c-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="0253c-135">可用的事件來源</span><span class="sxs-lookup"><span data-stu-id="0253c-135">Available event sources</span></span>

<span data-ttu-id="0253c-136">下列事件來源的 hello 發行事件方格透過取用的事件：</span><span class="sxs-lookup"><span data-stu-id="0253c-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="0253c-137">資源群組 (管理作業)</span><span class="sxs-lookup"><span data-stu-id="0253c-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="0253c-138">Azure 訂用帳戶 (管理作業)</span><span class="sxs-lookup"><span data-stu-id="0253c-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="0253c-139">事件中樞</span><span class="sxs-lookup"><span data-stu-id="0253c-139">Event Hubs</span></span>
* <span data-ttu-id="0253c-140">自訂主題</span><span class="sxs-lookup"><span data-stu-id="0253c-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="0253c-141">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0253c-141">Azure Subscriptions</span></span>

<span data-ttu-id="0253c-142">Azure 訂用帳戶現在可從 Azure Resource Manager 發出管理事件，像是在虛擬機器建立時或儲存體帳戶刪除時皆可使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0253c-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0253c-143">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="0253c-143">Available event types</span></span>

- <span data-ttu-id="0253c-144">**Microsoft.Resources.ResourceWriteSuccess**：在資源建立或更新作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="0253c-145">**Microsoft.Resources.ResourceWriteFailure**：在資源建立或更新作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="0253c-146">**Microsoft.Resources.ResourceWriteCancel**：在資源建立或更新作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="0253c-147">**Microsoft.Resources.ResourceDeleteSuccess**：在資源刪除作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="0253c-148">**Microsoft.Resources.ResourceDeleteFailure**：在資源刪除作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="0253c-149">**Microsoft.Resources.ResourceDeleteCancel**：在資源刪除作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="0253c-150">這會在範本部署取消時發生。</span><span class="sxs-lookup"><span data-stu-id="0253c-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="0253c-151">事件結構描述範例</span><span class="sxs-lookup"><span data-stu-id="0253c-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="0253c-152">資源群組</span><span class="sxs-lookup"><span data-stu-id="0253c-152">Resource Groups</span></span>

<span data-ttu-id="0253c-153">資源群組現在可從 Azure Resource Manager 發出管理事件，像是在虛擬機器建立時或儲存體帳戶刪除時皆可使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0253c-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0253c-154">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="0253c-154">Available event types</span></span>

- <span data-ttu-id="0253c-155">**Microsoft.Resources.ResourceWriteSuccess**：在資源建立或更新作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="0253c-156">**Microsoft.Resources.ResourceWriteFailure**：在資源建立或更新作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="0253c-157">**Microsoft.Resources.ResourceWriteCancel**：在資源建立或更新作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="0253c-158">**Microsoft.Resources.ResourceDeleteSuccess**：在資源刪除作業成功時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="0253c-159">**Microsoft.Resources.ResourceDeleteFailure**：在資源刪除作業失敗時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="0253c-160">**Microsoft.Resources.ResourceDeleteCancel**：在資源刪除作業取消時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="0253c-161">這會在範本部署取消時發生。</span><span class="sxs-lookup"><span data-stu-id="0253c-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="0253c-162">事件範例</span><span class="sxs-lookup"><span data-stu-id="0253c-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="0253c-163">事件中樞</span><span class="sxs-lookup"><span data-stu-id="0253c-163">Event Hubs</span></span>

<span data-ttu-id="0253c-164">事件中心事件正在 toostorage 使用 hello 擷取功能會自動傳送檔案時，才發出。</span><span class="sxs-lookup"><span data-stu-id="0253c-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0253c-165">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="0253c-165">Available event types</span></span>

- <span data-ttu-id="0253c-166">**Microsoft.EventHub.CaptureFileCreated**：擷取檔案建立時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="0253c-167">事件範例</span><span class="sxs-lookup"><span data-stu-id="0253c-167">Example event</span></span>

<span data-ttu-id="0253c-168">此範例事件顯示 hello 擷取儲存檔案時引發的事件中樞事件的結構描述。</span><span class="sxs-lookup"><span data-stu-id="0253c-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="0253c-169">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="0253c-169">Azure Blob Storage</span></span>

<span data-ttu-id="0253c-170">Azure Blob 儲存體目前提供私人預覽，註冊後可與 Event Grid 整合使用。</span><span class="sxs-lookup"><span data-stu-id="0253c-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="0253c-171">可用的事件類型</span><span class="sxs-lookup"><span data-stu-id="0253c-171">Available event types</span></span>

- <span data-ttu-id="0253c-172">**Microsoft.Storage.BlobCreated**：blob 建立時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="0253c-173">**Microsoft.Storage.BlobDeleted**：blob 刪除時引發。</span><span class="sxs-lookup"><span data-stu-id="0253c-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="0253c-174">事件範例</span><span class="sxs-lookup"><span data-stu-id="0253c-174">Example event</span></span>

<span data-ttu-id="0253c-175">此範例事件顯示 hello 結構描述建立 blob 時引發的儲存體事件。</span><span class="sxs-lookup"><span data-stu-id="0253c-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="0253c-176">自訂主題</span><span class="sxs-lookup"><span data-stu-id="0253c-176">Custom Topics</span></span>

<span data-ttu-id="0253c-177">您的自訂事件的 hello 資料裝載由您所定義，而且可以是任何也格式的 JSON。</span><span class="sxs-lookup"><span data-stu-id="0253c-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="0253c-178">hello 上方層級的資料應包含相同欄位所定義的標準資源事件 hello。</span><span class="sxs-lookup"><span data-stu-id="0253c-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="0253c-179">發行事件 toocustom 主題時，您應該考慮模型中路由與篩選您的事件 tooaid hello 主體。</span><span class="sxs-lookup"><span data-stu-id="0253c-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="0253c-180">事件範例</span><span class="sxs-lookup"><span data-stu-id="0253c-180">Example event</span></span>

<span data-ttu-id="0253c-181">hello 下列範例顯示事件，以供自訂主題：</span><span class="sxs-lookup"><span data-stu-id="0253c-181">hello following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="0253c-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0253c-182">Next steps</span></span>

* <span data-ttu-id="0253c-183">如簡介 tooEvent 格線，請參閱[事件方格是什麼？](overview.md)</span><span class="sxs-lookup"><span data-stu-id="0253c-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="0253c-184">toolearn 有關建立事件方格訂用帳戶，請參閱[事件方格訂用帳戶的結構描述](subscription-creation-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="0253c-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
