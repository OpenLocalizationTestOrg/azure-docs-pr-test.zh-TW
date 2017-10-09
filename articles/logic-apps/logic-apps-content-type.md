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
# <a name="handle-content-types-in-logic-apps"></a>在邏輯應用程式中處理內容類型

許多不同類型的內容可以在整個邏輯應用程式中流動，包括 JSON、XML、一般檔案及二進位資料。 即使 hello 邏輯應用程式引擎支援所有的內容類型，但是某些原生解讀的 hello 邏輯應用程式的引擎。 有些則可能要視需要進行轉型或轉換。 本文說明 hello 引擎如何處理不同的內容類型，以及 toocorrectly 如何處理在必要時，這些型別。

## <a name="content-type-header"></a>Content-Type 標頭

toostart 基本上，讓我們看看兩個 hello `Content-Types` ，不需要轉換或轉型，您可以使用邏輯應用程式中：`application/json`和`text/plain`。

## <a name="applicationjson"></a>Application/JSON

hello 工作流程引擎依賴 hello`Content-Type`來自 HTTP 標頭呼叫 toodetermine hello 適當的處理。 Hello 內容類型與任何要求`application/json`儲存及處理以 JSON 物件。 此外，JSON 內容預設就能剖析，不需要任何轉換。 

例如，您無法剖析 hello 內容類型標頭的要求`application/json `使用運算式，例如工作流程中`@body('myAction')['foo'][0]`tooget hello 值`bar`在此情況下：

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

不需要任何額外的轉換。 如果您使用 json，但沒有指定的標頭的資料，您可以手動將它轉換使用 hello tooJSON`@json()`函式，例如： `@json(triggerBody())['foo']`。

### <a name="schema-and-schema-generator"></a>結構描述和結構描述產生器

hello 要求觸發程序可讓您 tooenter JSON 結構描述為 hello 裝載您預期 tooreceive。 此結構描述可讓 hello 設計工具產生權杖，因此您可以使用 hello 的 hello 要求的內容。 如果您還沒有準備結構描述，選取**使用範例內容 toogenerate 結構描述**，因此您可以從範例裝載產生 JSON 結構描述。

![結構描述](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>「剖析 JSON」動作

hello`Parse JSON`動作可讓您 JSON 內容剖析成好記的語彙基元的邏輯應用程式消耗。 類似的 toohello 要求觸發程序，此動作可讓您輸入或產生的 JSON 結構描述內容想 tooparse hello。 此工具可讓您更容易地從服務匯流排、Azure Cosmos DB 等取用資料。

![剖析 JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>Text/plain

類似太`application/json`，HTTP 訊息接收以 hello`Content-Type`標頭`text/plain`以未經處理格式儲存。 此外，如果這些訊息包含於後續動作中而不需轉換，這些要求就會與 `Content-Type`: `text/plain` 標頭一同送出。 例如，使用一般檔案時，您可能會收到以下 HTTP 內容做為 `text/plain`︰

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

如果在 hello 下一步 動作中，您必須傳送 hello 要求做為另一個要求的 hello 主體 (`@body('flatfile')`)，必須 hello 要求`text/plain`Content-type 標頭。 如果您正在使用的是純文字，但沒有指定的標頭的資料，您可以手動將轉換使用 hello hello 資料 tootext`@string()`函式，例如： `@string(triggerBody())`。

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml 和 Application/octet-stream 以及轉換器函數

hello 邏輯應用程式引擎一律會保留 hello`Content-Type`收到 hello HTTP 要求或回應上。 因此，如果 hello 引擎收到內容以 hello`Content-Type`的`application/octet-stream`，並將包含在後續的動作，而不用轉型的內容，hello 傳出要求的`Content-Type`: `application/octet-stream`。 如此一來，hello 引擎可以保證資料不是透過 hello 流程移動時遺失。 不過，將 hello 動作狀態 （輸入及輸出） 儲存在 JSON 物件，如 hello 透過 hello 的工作流程的狀態移動。 某些資料類型，hello 引擎將轉換的 toopreserve 因此 hello 與適當的中繼資料，同時保留內容 tooa 二進位 base64 編碼字串`$content`和`$content-type`，這會自動轉換。 

* `@json()`-轉換過的資料`application/json`
* `@xml()`-轉換過的資料`application/xml`
* `@binary()`-轉換過的資料`application/octet-stream`
* `@string()`-轉換過的資料`text/plain`
* `@base64()`-將內容 tooa base64 字串轉換
* `@base64toString()`-太將 base64 編碼字串轉換`text/plain`
* `@base64toBinary()`-太將 base64 編碼字串轉換`application/octet-stream`
* `@encodeDataUri()` - 將字串編碼為 dataUri 位元組陣列
* `@decodeDataUri()` - 將 dataUri 解碼為位元組陣列

例如，如果您收到的 HTTP 要求具有 `Content-Type`: `application/xml`：

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

您可以轉換，並在稍後搭配像是 `@xml(triggerBody())` 的項目使用，或者在像是 `@xpath(xml(triggerBody()), '/CustomerName')` 的函式內使用。

## <a name="other-content-types"></a>其他內容類型

其他內容類型支援和使用邏輯應用程式，但是可能需要手動擷取 hello 訊息本文解碼 hello `$content`。 例如，假設您觸發`application/x-www-url-formencoded`要求 where `$content` hello 裝載的所有資料都編碼為 base64 字串 toopreserve:

```
CustomerName=Frank&Address=123+Avenue
```

因為 hello 要求不是純文字或 JSON，hello 要求儲存在 hello 動作，如下所示：

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

目前沒有為表單資料的原生函式，因此您仍無法使用工作流程中此資料，藉由手動存取具有函式的 hello 資料會像`@string(body('formdataAction'))`。 如果您想 hello tooalso 擁有 hello 的傳出要求`application/x-www-url-formencoded`內容類型標頭，您可以加入 hello 要求 toohello 動作主體而不用像任何轉型`@body('formdataAction')`。 不過，這個方法只適用於 hello 主體是在 hello hello 唯一參數`body`輸入。 如果您嘗試 toouse`@body('formdataAction')`中`application/json`要求，因為會傳送 hello 編碼內文，取得執行階段錯誤。

