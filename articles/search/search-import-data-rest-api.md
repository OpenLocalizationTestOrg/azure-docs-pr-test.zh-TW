---
title: "aaa 」 上傳資料 (REST API 的 Azure 搜尋) |Microsoft 文件 」"
description: "了解如何在 Azure 搜尋中使用 tooupload 資料 tooan 索引 hello REST API。"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>上傳資料 tooAzure 搜尋使用 hello REST API
> [!div class="op_single_selector"]
>
> * [概觀](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

這篇文章將示範如何 toouse hello [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport 資料到 Azure 搜尋索引。

在開始閱讀本逐步解說前，請先 [建立好 Azure 搜尋服務索引](search-what-is-an-index.md)。

在訂單 toopush 文件至您的索引使用 hello REST API，您將會發出 HTTP POST 要求 tooyour 索引 URL 端點。 hello 主體的 hello HTTP 要求主體是包含 toobe 新增、 修改或刪除的 hello 文件的 JSON 物件。

## <a name="identify-your-azure-search-services-admin-api-key"></a>識別 Azure 搜尋服務的系統管理 API 金鑰
發行您的服務使用 hello REST API，針對 HTTP 要求時*每個*API 要求都必須包含 hello api 金鑰 hello 您佈建的搜尋服務所產生。 擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。

1. toofind 服務的 api 金鑰，您可以登入 toohello [Azure 入口網站](https://portal.azure.com/)
2. 移 tooyour Azure 搜尋服務的刀鋒視窗
3. 按一下 hello 「 金鑰 」 圖示

服務會有系統管理金鑰和查詢金鑰。

* 您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。 有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。
* 您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。

基於 hello 匯入資料到索引，您可以使用主要或次要管理金鑰。

## <a name="decide-which-indexing-action-toouse"></a>決定哪個索引動作 toouse
使用 hello REST API，您就會發出 HTTP POST 要求，JSON 要求內文 tooyour Azure 搜尋索引的端點 URL。 您的 HTTP 要求主體中的 hello JSON 物件會包含單一的 JSON 陣列名為"value"包含代表您想要 tooadd tooyour 索引的文件的 JSON 物件，更新或刪除。

Hello"value"陣列中的每個 JSON 物件表示文件 toobe 編製索引。 每個物件包含 hello 文件索引鍵，並指定所需的 hello 索引動作 （上傳、 合併、 刪除等等）。 取決於哪些 hello 下列您選擇的動作，只有特定欄位必須包含每個文件：

| @search.action | 說明 | 每個文件的必要欄位 | 注意事項 |
| --- | --- | --- | --- |
| `upload` |`upload`動作是類似 tooan"upsert"(如果它是新插入和更新/取代如果它存在 hello 文件。 |索引鍵，再加上您想 toodefine 的任何其他欄位 |當更新/取代現有的文件，hello 要求中未指定任何欄位將會有其欄位太設定`null`。 這是即使 hello 欄位先前設定 tooa 非 null 值。 |
| `merge` |更新現有文件以 hello 指定欄位。 Hello 文件不存在 hello 索引中，如果 hello 合併將會失敗。 |索引鍵，再加上您想 toodefine 的任何其他欄位 |您在合併中指定任何欄位將會取代 hello hello 文件中的現有欄位。 這包括類型 `Collection(Edm.String)`的欄位。 例如，如果 hello 文件包含欄位`tags`值`["budget"]`和執行的合併值`["economy", "pool"]`的`tags`，hello hello 的最終值`tags`欄位就是`["economy", "pool"]`。 而不會是 `["budget", "economy", "pool"]`。 |
| `mergeOrUpload` |此動作的行為類似`merge`如果 hello 索引中的文件以 hello 給定索引鍵已經存在。 如果 hello 文件不存在，它的行為類似`upload`與新的文件。 |索引鍵，再加上您想 toodefine 的任何其他欄位 |- |
| `delete` |從 hello 索引中移除 hello 指定文件。 |僅索引鍵 |您指定其他非 hello 索引鍵欄位將會忽略所有的欄位。 如果您想 tooremove 個別欄位從 文件，請使用`merge`相反地，並直接將 hello 欄位明確 toonull。 |

## <a name="construct-your-http-request-and-request-body"></a>建構 HTTP 要求和要求本文
既然您已經收集 hello 必要的欄位值的索引動作，您已準備好 tooconstruct hello 實際的 HTTP 要求和 JSON 要求主體 tooimport 您的資料。

#### <a name="request-and-request-headers"></a>要求和要求標頭
在 hello URL，您將需要 tooprovide 您服務名稱、 索引名稱 （"旅館 「 在此情況下），以及 hello 適當的 API 版本 (hello 目前的 API 版本是`2016-09-01`次發行本文件的 hello)。 您將需要 toodefine hello`Content-Type`和`api-key`要求標頭。 Hello 後者，使用其中一個服務的系統管理金鑰。

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>要求本文
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

在本案例中，我們會使用 `upload`、`mergeOrUpload` 和 `delete` 做為搜尋動作。

假設此 "hotels" 索引範例已填入幾份文件。 請注意如何我們沒有 toospecify hello 可能文件的所有欄位時使用`mergeOrUpload`以及我們僅指定 hello 文件索引鍵的方式 (`hotelId`) 時使用`delete`。

此外，請注意，您只可包含 too1000 文件 （或 16MB） 在單一索引要求。

## <a name="understand-your-http-response-code"></a>了解 HTTP 回應碼
#### <a name="200"></a>200
成功提交索引編製要求後，您會收到狀態碼為 `200 OK`的 HTTP 回應。 hello hello HTTP 回應的 JSON 主體會如下所示：

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
至少有一個項目未成功建立索引時會傳回狀態碼 `207` 。 hello hello HTTP 回應的 JSON 主體會包含 hello 失敗的文件的相關資訊。

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> 這通常表示該 hello 載入您的搜尋服務即將達到索引要求會在開始 tooreturn 點`503`回應。 在此情況下，強烈建議您先讓用戶端程式碼退回並稍候一會，然後再重試。 這可讓某些時間 toorecover，增加未來的要求將會成功的 hello 機會 hello 系統。 快速重試您的要求將只會在保留 hello 的情況。
>
>

#### <a name="429"></a>429
狀態碼`429`您已超過每個索引的文件的 hello 數目配額時，會傳回。

#### <a name="503"></a>503
狀態碼`503`將會傳回如果無 hello hello 要求中的項目已成功編製索引。 此錯誤表示 hello 系統負載過重時，此時無法處理您的要求。

> [!NOTE]
> 在此情況下，強烈建議您先讓用戶端程式碼退回並稍候一會，然後再重試。 這可讓某些時間 toorecover，增加未來的要求將會成功的 hello 機會 hello 系統。 快速重試您的要求將只會在保留 hello 的情況。
>
>

如需文件動作和成功/錯誤回應的詳細資訊，請參閱 [加入、更新或刪除文件](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)。 如需失敗時可能傳回的其他 HTTP 狀態碼詳細資訊，請參閱 [HTTP 狀態碼 (Azure 搜尋服務)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)。

## <a name="next-steps"></a>後續步驟
填入您的 Azure 搜尋索引之後, 會準備 toostart 發出查詢 toosearch 文件。 如需詳細資料，請參閱 [查詢 Azure 搜尋服務索引](search-query-overview.md) 。
