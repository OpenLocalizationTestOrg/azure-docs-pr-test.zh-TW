---
title: "處理內容類型 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps 在設計階段與執行階段處理內容類型的方式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="3abad-103">在邏輯應用程式中處理內容類型</span><span class="sxs-lookup"><span data-stu-id="3abad-103">Handle content types in logic apps</span></span>

<span data-ttu-id="3abad-104">許多不同類型的內容可以在整個邏輯應用程式中流動，包括 JSON、XML、一般檔案及二進位資料。</span><span class="sxs-lookup"><span data-stu-id="3abad-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="3abad-105">儘管 Logic Apps 引擎支援所有的內容類型，但有些是透過 Logic Apps 引擎進行原生了解。</span><span class="sxs-lookup"><span data-stu-id="3abad-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="3abad-106">有些則可能要視需要進行轉型或轉換。</span><span class="sxs-lookup"><span data-stu-id="3abad-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="3abad-107">本文說明引擎如何處理不同的內容類型，以及如何視需要正確處理這些類型。</span><span class="sxs-lookup"><span data-stu-id="3abad-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="3abad-108">Content-Type 標頭</span><span class="sxs-lookup"><span data-stu-id="3abad-108">Content-Type Header</span></span>

<span data-ttu-id="3abad-109">若要從基本開始，讓我們看看下列這兩個 `Content-Types`，它們不需要轉換或轉型，就能在邏輯應用程式中使用：`application/json` 和 `text/plain`。</span><span class="sxs-lookup"><span data-stu-id="3abad-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="3abad-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="3abad-110">Application/JSON</span></span>

<span data-ttu-id="3abad-111">工作流程引擎依賴來自 HTTP 呼叫的 `Content-Type` 標頭來決定適當的處理。</span><span class="sxs-lookup"><span data-stu-id="3abad-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="3abad-112">內容類型為 `application/json` 的所有要求都會以 JSON 物件的形式儲存並加以處理。</span><span class="sxs-lookup"><span data-stu-id="3abad-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="3abad-113">此外，JSON 內容預設就能剖析，不需要任何轉換。</span><span class="sxs-lookup"><span data-stu-id="3abad-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="3abad-114">例如，在此例中使用 `@body('myAction')['foo'][0]` 之類的運算式來取得 `bar` 值，可以剖析工作流程中具有 `application/json ` 內容類型標頭的要求︰</span><span class="sxs-lookup"><span data-stu-id="3abad-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="3abad-115">不需要任何額外的轉換。</span><span class="sxs-lookup"><span data-stu-id="3abad-115">No additional casting is needed.</span></span> <span data-ttu-id="3abad-116">如果您正在使用格式為 JSON 的資料，但並未指定標頭，則可使用 `@json()` 函式手動將它轉換為 JSON，例如 `@json(triggerBody())['foo']`。</span><span class="sxs-lookup"><span data-stu-id="3abad-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="3abad-117">結構描述和結構描述產生器</span><span class="sxs-lookup"><span data-stu-id="3abad-117">Schema and schema generator</span></span>

<span data-ttu-id="3abad-118">要求觸發程序可讓您輸入您希望接收之承載的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="3abad-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="3abad-119">此結構描述可讓設計工具產生權杖，以便您取用要求的內容。</span><span class="sxs-lookup"><span data-stu-id="3abad-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="3abad-120">如果您尚未準備好結構描述，選取 [請使用範例承載產生結構描述]，如此便能從範例承載中產生 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="3abad-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![結構描述](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="3abad-122">「剖析 JSON」動作</span><span class="sxs-lookup"><span data-stu-id="3abad-122">'Parse JSON' action</span></span>

<span data-ttu-id="3abad-123">`Parse JSON` 動作可讓您將 JSON 內容剖析為易記權杖，以便在邏輯應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="3abad-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="3abad-124">此動作類似於要求觸發程序，可讓您輸入或產生所要剖析內容的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="3abad-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="3abad-125">此工具可讓您更容易地從服務匯流排、Azure Cosmos DB 等取用資料。</span><span class="sxs-lookup"><span data-stu-id="3abad-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![剖析 JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="3abad-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="3abad-127">Text/plain</span></span>

<span data-ttu-id="3abad-128">類似於 `application/json`，若所收到的 HTTP 訊息中 `Content-Type` 標頭為 `text/plain`，就會以原始格式來儲存。</span><span class="sxs-lookup"><span data-stu-id="3abad-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="3abad-129">此外，如果這些訊息包含於後續動作中而不需轉換，這些要求就會與 `Content-Type`: `text/plain` 標頭一同送出。</span><span class="sxs-lookup"><span data-stu-id="3abad-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="3abad-130">例如，使用一般檔案時，您可能會收到以下 HTTP 內容做為 `text/plain`︰</span><span class="sxs-lookup"><span data-stu-id="3abad-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="3abad-131">如果在下一個動作中，您將要求做為另一個要求的內文 (`@body('flatfile')`) 來傳送，則要求必須含有 `text/plain` Content-Type 標頭。</span><span class="sxs-lookup"><span data-stu-id="3abad-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="3abad-132">如果您正在使用格式為純文字的資料，但並未指定標頭，則可使用 `@string()` 函式 (例如：`@string(triggerBody())`) 手動將資料轉換為文字。</span><span class="sxs-lookup"><span data-stu-id="3abad-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="3abad-133">Application/xml 和 Application/octet-stream 以及轉換器函數</span><span class="sxs-lookup"><span data-stu-id="3abad-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="3abad-134">邏輯應用程式引擎一律會保留在 HTTP 要求或回應上接收到的 `Content-Type`。</span><span class="sxs-lookup"><span data-stu-id="3abad-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="3abad-135">因此，如果引擎收到 `Content-Type` 為 `application/octet-stream` 的內容，而且您在後續動作中納入未經轉型的內容，則外送要求具有 `Content-Type`: `application/octet-stream`。</span><span class="sxs-lookup"><span data-stu-id="3abad-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="3abad-136">如此一來，引擎就可以保證資料在整個工作流程中移動時不會遺失。</span><span class="sxs-lookup"><span data-stu-id="3abad-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="3abad-137">不過，當動作狀態 (輸入和輸出) 通過工作流程時，該狀態會儲存於 JSON 物件中。</span><span class="sxs-lookup"><span data-stu-id="3abad-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="3abad-138">所以，為了保留某些資料類型，引擎會將內容轉換為二進位 Base64 編碼的字串，其中包含可保留 `$content` 和 `$content-type` (都會自動轉換) 的適當中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3abad-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="3abad-139">`@json()` - 將資料轉換為 `application/json`</span><span class="sxs-lookup"><span data-stu-id="3abad-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="3abad-140">`@xml()` - 將資料轉換為 `application/xml`</span><span class="sxs-lookup"><span data-stu-id="3abad-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="3abad-141">`@binary()` - 將資料轉換為 `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="3abad-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="3abad-142">`@string()` - 將資料轉換為 `text/plain`</span><span class="sxs-lookup"><span data-stu-id="3abad-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="3abad-143">`@base64()` - 將內容轉換為 Base64 字串</span><span class="sxs-lookup"><span data-stu-id="3abad-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="3abad-144">`@base64toString()` - 將 Base64 編碼的字串轉換為 `text/plain`</span><span class="sxs-lookup"><span data-stu-id="3abad-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="3abad-145">`@base64toBinary()` - 將 Base64 編碼的字串轉換為 `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="3abad-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="3abad-146">`@encodeDataUri()` - 將字串編碼為 dataUri 位元組陣列</span><span class="sxs-lookup"><span data-stu-id="3abad-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="3abad-147">`@decodeDataUri()` - 將 dataUri 解碼為位元組陣列</span><span class="sxs-lookup"><span data-stu-id="3abad-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="3abad-148">例如，如果您收到的 HTTP 要求具有 `Content-Type`: `application/xml`：</span><span class="sxs-lookup"><span data-stu-id="3abad-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="3abad-149">您可以轉換，並在稍後搭配像是 `@xml(triggerBody())` 的項目使用，或者在像是 `@xpath(xml(triggerBody()), '/CustomerName')` 的函式內使用。</span><span class="sxs-lookup"><span data-stu-id="3abad-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="3abad-150">其他內容類型</span><span class="sxs-lookup"><span data-stu-id="3abad-150">Other content types</span></span>

<span data-ttu-id="3abad-151">有其他內容類型也受到支援，而且可與邏輯應用程式一起運作，但是可能需要藉由將 `$content` 解碼來手動擷取訊息內文。</span><span class="sxs-lookup"><span data-stu-id="3abad-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="3abad-152">例如，假設您觸發 `application/x-www-url-formencoded` 要求，其 `$content` 是編碼為 Base64 字串的承載，可保留所有資料：</span><span class="sxs-lookup"><span data-stu-id="3abad-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="3abad-153">因為要求不是純文字或 JSON，所以要求會儲存在動作中，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3abad-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

目前沒有任何適用於 form-data 的原生函式，所以您仍可藉由使用 `@string(body('formdataAction'))` 之類的函式手動存取資料，進而在工作流程中使用此資料。 如果您希望外送要求也具有 `application/x-www-url-formencoded` 內容類型標頭，您可以直接將要求新增到動作內文，而不需使用任何像是 `@body('formdataAction')` 的轉換。 不過，唯有當內文是 `body` 輸入中的唯一參數時，才適用這種方法。 <span data-ttu-id="3abad-157">如果您嘗試在 `application/json` 要求中使用 `@body('formdataAction')`，您會因為傳送已編碼的內文而發生執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="3abad-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

