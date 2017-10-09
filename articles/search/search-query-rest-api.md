---
title: "aaa\"查詢索引 (REST API 的 Azure 搜尋) |Microsoft 文件 」"
description: "建置在 Azure 搜尋的搜尋查詢，並使用搜尋參數 toofilter 和排序搜尋結果。"
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>查詢您的 Azure 搜尋索引使用 hello REST API
> [!div class="op_single_selector"]
>
> * [概觀](search-query-overview.md)
> * [入口網站](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

本文章將示範如何使用索引的 tooquery hello [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/)。

在開始閱讀本逐步解說前，請先[建立好 Azure 搜尋服務索引](search-what-is-an-index.md)，並[在索引中填入資料](search-what-is-data-import.md)。 如需有關背景資訊，請參閱[全文檢索搜尋如何在 Azure 搜尋服務中運作](search-lucene-query-architecture.md)。

## <a name="identify-your-azure-search-services-query-api-key"></a>識別 Azure 搜尋服務的查詢 API 金鑰
Hello Azure 搜尋 REST API 針對每個搜尋作業的重要元件是 hello *api 金鑰*產生 hello 您佈建的服務。 擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。

1. toofind 服務的 api 金鑰，您可以登入 toohello [Azure 入口網站](https://portal.azure.com/)
2. 移 tooyour Azure 搜尋服務的刀鋒視窗
3. 按一下 hello 「 金鑰 」 圖示

您的服務有「系統管理金鑰」和「查詢金鑰」。

* 您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。 有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。
* 您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。

基於 hello 查詢索引，您可以使用您的查詢索引鍵的其中一個。 系統管理金鑰也可以用於查詢，但您應該查詢索引鍵使用您的應用程式程式碼中，這更如下所示 hello[最低權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)。

## <a name="formulate-your-query"></a>編寫查詢
有兩種方式的太[搜尋索引使用 REST API hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)。 其中一種方式是 tooissue HTTP POST 要求，其中 hello 要求主體中的 JSON 物件中定義查詢參數。 hello 另一種方式是 tooissue HTTP GET 要求，其中定義查詢參數 hello 要求 URL 中。 文章中的多個[放寬限制](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)hello 大小比 GET 的查詢參數。 因此，除非您的情況特殊導致使用 GET 會比較方便，否則建議您使用 POST。

POST 與 GET，您需要 tooprovide 您*服務名稱*，*索引名稱*，並適當 hello *API 版本*(hello 目前的 API 版本是`2016-09-01`hello 次發行這份文件） 的 hello 在要求 URL。 為 GET、 hello*查詢字串*在 hello hello URL 的結尾會是您用來提供 hello 查詢參數。 Hello URL 格式，請參閱下面的內容：

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

hello 格式化的 POST 是 hello 相同，但只有 api 版本在 hello 查詢字串參數中。

#### <a name="example-queries"></a>查詢範例
以下是幾個名為 "hotels" 之索引的查詢範例。 範例中會同時顯示 GET 和 POST 格式的查詢。

搜尋 hello 詞彙 '預算' hello 整個索引並傳回僅 hello`hotelName`欄位：

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

套用篩選器 toohello 索引 toofind 旅館比每晚，$150 廉價，並傳回 hello`hotelId`和`description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

搜尋 hello 整個索引中，依特定欄位的順序 (`lastRenovationDate`) 以遞減順序，hello 前兩個結果，並只顯示`hotelName`和`lastRenovationDate`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a>提交 HTTP 要求
現在您已將查詢編寫為 HTTP 要求 URL (若為 GET) 或主體 (若為 POST) 的一部分，接下來您可以定義要求標頭並提交查詢。

#### <a name="request-and-request-headers"></a>要求和要求標頭
您必須為 GET 定義兩個要求標頭，若為 POST 則必須定義三個：

1. hello`api-key`標頭必須設定您在步驟中找到我上述 toohello 查詢索引鍵。 您也可以使用 管理金鑰為 hello`api-key`標頭，但建議您使用的是查詢索引鍵，因為它只會授與唯讀存取 tooindexes 和文件。
2. hello`Accept`標頭必須設定太`application/json`。
3. 只有 post hello`Content-Type`標頭也應該設定太`application/json`。

HTTP GET 要求 toosearch hello 「 旅館"索引使用 Azure 搜尋 REST API，使用簡單的查詢可搜尋 hello 詞彙"motel"hello，請參閱下面的內容：

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

以下是相同的 hello 範例查詢中，這次使用 HTTP POST:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

成功的查詢要求會導致狀態碼`200 OK`和 hello 搜尋結果傳回成 JSON hello 回應主體中。 以下是 hello 上述查詢看起來像是，假設 hello 「 旅館"索引填入資料中的 hello 範例會產生哪些 hello[在 Azure 搜尋中使用的資料匯入 hello REST API](search-import-data-rest-api.md) （請注意為了清楚起見，已設定格式 JSON 該 hello）。

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

toolearn 詳細資訊，請瀏覽 hello 「 回應 」 一節[搜尋文件](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)。 如需失敗時可能傳回的其他 HTTP 狀態碼詳細資訊，請參閱 [HTTP 狀態碼 (Azure 搜尋服務)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)。
