---
title: "aaaAzure 事件方格訂用帳戶的結構描述"
description: "描述 Azure 事件方格 tooan 事件訂閱的 hello 屬性。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="07e77-103">事件格線訂用帳戶的結構描述</span><span class="sxs-lookup"><span data-stu-id="07e77-103">Event Grid subscription schema</span></span>

<span data-ttu-id="07e77-104">toocreate 事件方格訂用帳戶，您傳送要求 toohello Create Event 訂用帳戶作業。</span><span class="sxs-lookup"><span data-stu-id="07e77-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="07e77-105">使用下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="07e77-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="07e77-106">例如，toocreate 事件訂閱名為儲存體帳戶`examplestorage`資源群組中名為`examplegroup`，使用 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="07e77-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="07e77-107">hello 文章說明 hello 屬性和 hello hello 要求主體的結構描述。</span><span class="sxs-lookup"><span data-stu-id="07e77-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="07e77-108">事件訂用帳戶屬性</span><span class="sxs-lookup"><span data-stu-id="07e77-108">Event subscription properties</span></span>

| <span data-ttu-id="07e77-109">屬性</span><span class="sxs-lookup"><span data-stu-id="07e77-109">Property</span></span> | <span data-ttu-id="07e77-110">類型</span><span class="sxs-lookup"><span data-stu-id="07e77-110">Type</span></span> | <span data-ttu-id="07e77-111">說明</span><span class="sxs-lookup"><span data-stu-id="07e77-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="07e77-112">目的地</span><span class="sxs-lookup"><span data-stu-id="07e77-112">destination</span></span> | <span data-ttu-id="07e77-113">物件</span><span class="sxs-lookup"><span data-stu-id="07e77-113">object</span></span> | <span data-ttu-id="07e77-114">hello 定義 hello 端點的物件。</span><span class="sxs-lookup"><span data-stu-id="07e77-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="07e77-115">filter</span><span class="sxs-lookup"><span data-stu-id="07e77-115">filter</span></span> | <span data-ttu-id="07e77-116">物件</span><span class="sxs-lookup"><span data-stu-id="07e77-116">object</span></span> | <span data-ttu-id="07e77-117">篩選 hello 事件類型的選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="07e77-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="07e77-118">目的地物件</span><span class="sxs-lookup"><span data-stu-id="07e77-118">destination object</span></span>

| <span data-ttu-id="07e77-119">屬性</span><span class="sxs-lookup"><span data-stu-id="07e77-119">Property</span></span> | <span data-ttu-id="07e77-120">類型</span><span class="sxs-lookup"><span data-stu-id="07e77-120">Type</span></span> | <span data-ttu-id="07e77-121">說明</span><span class="sxs-lookup"><span data-stu-id="07e77-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="07e77-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="07e77-122">endpointType</span></span> | <span data-ttu-id="07e77-123">字串</span><span class="sxs-lookup"><span data-stu-id="07e77-123">string</span></span> | <span data-ttu-id="07e77-124">hello hello 訂用帳戶 （webhook/HTTP，事件中心或佇列） 的端點類型。</span><span class="sxs-lookup"><span data-stu-id="07e77-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="07e77-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="07e77-125">endpointUrl</span></span> | <span data-ttu-id="07e77-126">字串</span><span class="sxs-lookup"><span data-stu-id="07e77-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="07e77-127">篩選物件</span><span class="sxs-lookup"><span data-stu-id="07e77-127">filter object</span></span>

| <span data-ttu-id="07e77-128">屬性</span><span class="sxs-lookup"><span data-stu-id="07e77-128">Property</span></span> | <span data-ttu-id="07e77-129">類型</span><span class="sxs-lookup"><span data-stu-id="07e77-129">Type</span></span> | <span data-ttu-id="07e77-130">說明</span><span class="sxs-lookup"><span data-stu-id="07e77-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="07e77-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="07e77-131">includedEventTypes</span></span> | <span data-ttu-id="07e77-132">array</span><span class="sxs-lookup"><span data-stu-id="07e77-132">array</span></span> | <span data-ttu-id="07e77-133">比對這些事件的型別名稱的完全相符 tooone hello hello 事件訊息中的事件類型時。</span><span class="sxs-lookup"><span data-stu-id="07e77-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="07e77-134">事件名稱與 hello 事件來源的 hello 註冊事件類型名稱不相符時，會引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="07e77-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="07e77-135">預設會符合所有事件類型。</span><span class="sxs-lookup"><span data-stu-id="07e77-135">Default matches all event types.</span></span> |
| <span data-ttu-id="07e77-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="07e77-136">subjectBeginsWith</span></span> | <span data-ttu-id="07e77-137">字串</span><span class="sxs-lookup"><span data-stu-id="07e77-137">string</span></span> | <span data-ttu-id="07e77-138">前置詞比對篩選 toohello 主旨欄位 hello 事件訊息中。</span><span class="sxs-lookup"><span data-stu-id="07e77-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="07e77-139">hello 預設值或空字串比對所有。</span><span class="sxs-lookup"><span data-stu-id="07e77-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="07e77-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="07e77-140">subjectEndsWith</span></span> | <span data-ttu-id="07e77-141">字串</span><span class="sxs-lookup"><span data-stu-id="07e77-141">string</span></span> | <span data-ttu-id="07e77-142">後置詞比對篩選 toohello 主旨欄位 hello 事件訊息中。</span><span class="sxs-lookup"><span data-stu-id="07e77-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="07e77-143">hello 預設值或空字串比對所有。</span><span class="sxs-lookup"><span data-stu-id="07e77-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="07e77-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="07e77-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="07e77-145">字串</span><span class="sxs-lookup"><span data-stu-id="07e77-145">string</span></span> | <span data-ttu-id="07e77-146">控制篩選的區分大小寫比對。</span><span class="sxs-lookup"><span data-stu-id="07e77-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="07e77-147">範例訂用帳戶的結構描述</span><span class="sxs-lookup"><span data-stu-id="07e77-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="07e77-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07e77-148">Next steps</span></span>

* <span data-ttu-id="07e77-149">如簡介 tooEvent 格線，請參閱[事件方格是什麼？](overview.md)</span><span class="sxs-lookup"><span data-stu-id="07e77-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
