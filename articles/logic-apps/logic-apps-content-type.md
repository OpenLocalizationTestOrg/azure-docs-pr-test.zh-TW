---
title: "aaaHandle 內容類型 Azure 邏輯應用程式 |Microsoft 文件"
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
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="17ec0-103">在邏輯應用程式中處理內容類型</span><span class="sxs-lookup"><span data-stu-id="17ec0-103">Handle content types in logic apps</span></span>

<span data-ttu-id="17ec0-104">許多不同類型的內容可以在整個邏輯應用程式中流動，包括 JSON、XML、一般檔案及二進位資料。</span><span class="sxs-lookup"><span data-stu-id="17ec0-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="17ec0-105">即使 hello 邏輯應用程式引擎支援所有的內容類型，但是某些原生解讀的 hello 邏輯應用程式的引擎。</span><span class="sxs-lookup"><span data-stu-id="17ec0-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="17ec0-106">有些則可能要視需要進行轉型或轉換。</span><span class="sxs-lookup"><span data-stu-id="17ec0-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="17ec0-107">本文說明 hello 引擎如何處理不同的內容類型，以及 toocorrectly 如何處理在必要時，這些型別。</span><span class="sxs-lookup"><span data-stu-id="17ec0-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="17ec0-108">Content-Type 標頭</span><span class="sxs-lookup"><span data-stu-id="17ec0-108">Content-Type Header</span></span>

<span data-ttu-id="17ec0-109">toostart 基本上，讓我們看看兩個 hello `Content-Types` ，不需要轉換或轉型，您可以使用邏輯應用程式中：`application/json`和`text/plain`。</span><span class="sxs-lookup"><span data-stu-id="17ec0-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="17ec0-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="17ec0-110">Application/JSON</span></span>

<span data-ttu-id="17ec0-111">hello 工作流程引擎依賴 hello`Content-Type`來自 HTTP 標頭呼叫 toodetermine hello 適當的處理。</span><span class="sxs-lookup"><span data-stu-id="17ec0-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="17ec0-112">Hello 內容類型與任何要求`application/json`儲存及處理以 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="17ec0-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="17ec0-113">此外，JSON 內容預設就能剖析，不需要任何轉換。</span><span class="sxs-lookup"><span data-stu-id="17ec0-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="17ec0-114">例如，您無法剖析 hello 內容類型標頭的要求`application/json `使用運算式，例如工作流程中`@body('myAction')['foo'][0]`tooget hello 值`bar`在此情況下：</span><span class="sxs-lookup"><span data-stu-id="17ec0-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="17ec0-115">不需要任何額外的轉換。</span><span class="sxs-lookup"><span data-stu-id="17ec0-115">No additional casting is needed.</span></span> <span data-ttu-id="17ec0-116">如果您使用 json，但沒有指定的標頭的資料，您可以手動將它轉換使用 hello tooJSON`@json()`函式，例如： `@json(triggerBody())['foo']`。</span><span class="sxs-lookup"><span data-stu-id="17ec0-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="17ec0-117">結構描述和結構描述產生器</span><span class="sxs-lookup"><span data-stu-id="17ec0-117">Schema and schema generator</span></span>

<span data-ttu-id="17ec0-118">hello 要求觸發程序可讓您 tooenter JSON 結構描述為 hello 裝載您預期 tooreceive。</span><span class="sxs-lookup"><span data-stu-id="17ec0-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="17ec0-119">此結構描述可讓 hello 設計工具產生權杖，因此您可以使用 hello 的 hello 要求的內容。</span><span class="sxs-lookup"><span data-stu-id="17ec0-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="17ec0-120">如果您還沒有準備結構描述，選取**使用範例內容 toogenerate 結構描述**，因此您可以從範例裝載產生 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="17ec0-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![結構描述](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="17ec0-122">「剖析 JSON」動作</span><span class="sxs-lookup"><span data-stu-id="17ec0-122">'Parse JSON' action</span></span>

<span data-ttu-id="17ec0-123">hello`Parse JSON`動作可讓您 JSON 內容剖析成好記的語彙基元的邏輯應用程式消耗。</span><span class="sxs-lookup"><span data-stu-id="17ec0-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="17ec0-124">類似的 toohello 要求觸發程序，此動作可讓您輸入或產生的 JSON 結構描述內容想 tooparse hello。</span><span class="sxs-lookup"><span data-stu-id="17ec0-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="17ec0-125">此工具可讓您更容易地從服務匯流排、Azure Cosmos DB 等取用資料。</span><span class="sxs-lookup"><span data-stu-id="17ec0-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![剖析 JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="17ec0-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="17ec0-127">Text/plain</span></span>

<span data-ttu-id="17ec0-128">類似太`application/json`，HTTP 訊息接收以 hello`Content-Type`標頭`text/plain`以未經處理格式儲存。</span><span class="sxs-lookup"><span data-stu-id="17ec0-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="17ec0-129">此外，如果這些訊息包含於後續動作中而不需轉換，這些要求就會與 `Content-Type`: `text/plain` 標頭一同送出。</span><span class="sxs-lookup"><span data-stu-id="17ec0-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="17ec0-130">例如，使用一般檔案時，您可能會收到以下 HTTP 內容做為 `text/plain`︰</span><span class="sxs-lookup"><span data-stu-id="17ec0-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="17ec0-131">如果在 hello 下一步 動作中，您必須傳送 hello 要求做為另一個要求的 hello 主體 (`@body('flatfile')`)，必須 hello 要求`text/plain`Content-type 標頭。</span><span class="sxs-lookup"><span data-stu-id="17ec0-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="17ec0-132">如果您正在使用的是純文字，但沒有指定的標頭的資料，您可以手動將轉換使用 hello hello 資料 tootext`@string()`函式，例如： `@string(triggerBody())`。</span><span class="sxs-lookup"><span data-stu-id="17ec0-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="17ec0-133">Application/xml 和 Application/octet-stream 以及轉換器函數</span><span class="sxs-lookup"><span data-stu-id="17ec0-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="17ec0-134">hello 邏輯應用程式引擎一律會保留 hello`Content-Type`收到 hello HTTP 要求或回應上。</span><span class="sxs-lookup"><span data-stu-id="17ec0-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="17ec0-135">因此，如果 hello 引擎收到內容以 hello`Content-Type`的`application/octet-stream`，並將包含在後續的動作，而不用轉型的內容，hello 傳出要求的`Content-Type`: `application/octet-stream`。</span><span class="sxs-lookup"><span data-stu-id="17ec0-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="17ec0-136">如此一來，hello 引擎可以保證資料不是透過 hello 流程移動時遺失。</span><span class="sxs-lookup"><span data-stu-id="17ec0-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="17ec0-137">不過，將 hello 動作狀態 （輸入及輸出） 儲存在 JSON 物件，如 hello 透過 hello 的工作流程的狀態移動。</span><span class="sxs-lookup"><span data-stu-id="17ec0-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="17ec0-138">某些資料類型，hello 引擎將轉換的 toopreserve 因此 hello 與適當的中繼資料，同時保留內容 tooa 二進位 base64 編碼字串`$content`和`$content-type`，這會自動轉換。</span><span class="sxs-lookup"><span data-stu-id="17ec0-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="17ec0-139">`@json()`-轉換過的資料`application/json`</span><span class="sxs-lookup"><span data-stu-id="17ec0-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="17ec0-140">`@xml()`-轉換過的資料`application/xml`</span><span class="sxs-lookup"><span data-stu-id="17ec0-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="17ec0-141">`@binary()`-轉換過的資料`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="17ec0-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="17ec0-142">`@string()`-轉換過的資料`text/plain`</span><span class="sxs-lookup"><span data-stu-id="17ec0-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="17ec0-143">`@base64()`-將內容 tooa base64 字串轉換</span><span class="sxs-lookup"><span data-stu-id="17ec0-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="17ec0-144">`@base64toString()`-太將 base64 編碼字串轉換`text/plain`</span><span class="sxs-lookup"><span data-stu-id="17ec0-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="17ec0-145">`@base64toBinary()`-太將 base64 編碼字串轉換`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="17ec0-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="17ec0-146">`@encodeDataUri()` - 將字串編碼為 dataUri 位元組陣列</span><span class="sxs-lookup"><span data-stu-id="17ec0-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="17ec0-147">`@decodeDataUri()` - 將 dataUri 解碼為位元組陣列</span><span class="sxs-lookup"><span data-stu-id="17ec0-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="17ec0-148">例如，如果您收到的 HTTP 要求具有 `Content-Type`: `application/xml`：</span><span class="sxs-lookup"><span data-stu-id="17ec0-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="17ec0-149">您可以轉換，並在稍後搭配像是 `@xml(triggerBody())` 的項目使用，或者在像是 `@xpath(xml(triggerBody()), '/CustomerName')` 的函式內使用。</span><span class="sxs-lookup"><span data-stu-id="17ec0-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="17ec0-150">其他內容類型</span><span class="sxs-lookup"><span data-stu-id="17ec0-150">Other content types</span></span>

<span data-ttu-id="17ec0-151">其他內容類型支援和使用邏輯應用程式，但是可能需要手動擷取 hello 訊息本文解碼 hello `$content`。</span><span class="sxs-lookup"><span data-stu-id="17ec0-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="17ec0-152">例如，假設您觸發`application/x-www-url-formencoded`要求 where `$content` hello 裝載的所有資料都編碼為 base64 字串 toopreserve:</span><span class="sxs-lookup"><span data-stu-id="17ec0-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="17ec0-153">因為 hello 要求不是純文字或 JSON，hello 要求儲存在 hello 動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="17ec0-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

目前沒有為表單資料的原生函式，因此您仍無法使用工作流程中此資料，藉由手動存取具有函式的 hello 資料會像`@string(body('formdataAction'))`。 如果您想 hello tooalso 擁有 hello 的傳出要求`application/x-www-url-formencoded`內容類型標頭，您可以加入 hello 要求 toohello 動作主體而不用像任何轉型`@body('formdataAction')`。 不過，這個方法只適用於 hello 主體是在 hello hello 唯一參數`body`輸入。 <span data-ttu-id="17ec0-157">如果您嘗試 toouse`@body('formdataAction')`中`application/json`要求，因為會傳送 hello 編碼內文，取得執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="17ec0-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

