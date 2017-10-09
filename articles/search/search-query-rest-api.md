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
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="1f973-103">查詢您的 Azure 搜尋索引使用 hello REST API</span><span class="sxs-lookup"><span data-stu-id="1f973-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="1f973-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1f973-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="1f973-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="1f973-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="1f973-106">.NET</span><span class="sxs-lookup"><span data-stu-id="1f973-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="1f973-107">REST</span><span class="sxs-lookup"><span data-stu-id="1f973-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="1f973-108">本文章將示範如何使用索引的 tooquery hello [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="1f973-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="1f973-109">在開始閱讀本逐步解說前，請先[建立好 Azure 搜尋服務索引](search-what-is-an-index.md)，並[在索引中填入資料](search-what-is-data-import.md)。</span><span class="sxs-lookup"><span data-stu-id="1f973-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="1f973-110">如需有關背景資訊，請參閱[全文檢索搜尋如何在 Azure 搜尋服務中運作](search-lucene-query-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="1f973-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="1f973-111">識別 Azure 搜尋服務的查詢 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="1f973-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="1f973-112">Hello Azure 搜尋 REST API 針對每個搜尋作業的重要元件是 hello *api 金鑰*產生 hello 您佈建的服務。</span><span class="sxs-lookup"><span data-stu-id="1f973-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="1f973-113">擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。</span><span class="sxs-lookup"><span data-stu-id="1f973-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="1f973-114">toofind 服務的 api 金鑰，您可以登入 toohello [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="1f973-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="1f973-115">移 tooyour Azure 搜尋服務的刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="1f973-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="1f973-116">按一下 hello 「 金鑰 」 圖示</span><span class="sxs-lookup"><span data-stu-id="1f973-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="1f973-117">您的服務有「系統管理金鑰」和「查詢金鑰」。</span><span class="sxs-lookup"><span data-stu-id="1f973-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="1f973-118">您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。</span><span class="sxs-lookup"><span data-stu-id="1f973-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="1f973-119">有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="1f973-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="1f973-120">您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f973-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="1f973-121">基於 hello 查詢索引，您可以使用您的查詢索引鍵的其中一個。</span><span class="sxs-lookup"><span data-stu-id="1f973-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="1f973-122">系統管理金鑰也可以用於查詢，但您應該查詢索引鍵使用您的應用程式程式碼中，這更如下所示 hello[最低權限原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)。</span><span class="sxs-lookup"><span data-stu-id="1f973-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="1f973-123">編寫查詢</span><span class="sxs-lookup"><span data-stu-id="1f973-123">Formulate your query</span></span>
<span data-ttu-id="1f973-124">有兩種方式的太[搜尋索引使用 REST API hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)。</span><span class="sxs-lookup"><span data-stu-id="1f973-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="1f973-125">其中一種方式是 tooissue HTTP POST 要求，其中 hello 要求主體中的 JSON 物件中定義查詢參數。</span><span class="sxs-lookup"><span data-stu-id="1f973-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="1f973-126">hello 另一種方式是 tooissue HTTP GET 要求，其中定義查詢參數 hello 要求 URL 中。</span><span class="sxs-lookup"><span data-stu-id="1f973-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="1f973-127">文章中的多個[放寬限制](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)hello 大小比 GET 的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="1f973-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="1f973-128">因此，除非您的情況特殊導致使用 GET 會比較方便，否則建議您使用 POST。</span><span class="sxs-lookup"><span data-stu-id="1f973-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="1f973-129">POST 與 GET，您需要 tooprovide 您*服務名稱*，*索引名稱*，並適當 hello *API 版本*(hello 目前的 API 版本是`2016-09-01`hello 次發行這份文件） 的 hello 在要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1f973-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="1f973-130">為 GET、 hello*查詢字串*在 hello hello URL 的結尾會是您用來提供 hello 查詢參數。</span><span class="sxs-lookup"><span data-stu-id="1f973-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="1f973-131">Hello URL 格式，請參閱下面的內容：</span><span class="sxs-lookup"><span data-stu-id="1f973-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="1f973-132">hello 格式化的 POST 是 hello 相同，但只有 api 版本在 hello 查詢字串參數中。</span><span class="sxs-lookup"><span data-stu-id="1f973-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="1f973-133">查詢範例</span><span class="sxs-lookup"><span data-stu-id="1f973-133">Example Queries</span></span>
<span data-ttu-id="1f973-134">以下是幾個名為 "hotels" 之索引的查詢範例。</span><span class="sxs-lookup"><span data-stu-id="1f973-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="1f973-135">範例中會同時顯示 GET 和 POST 格式的查詢。</span><span class="sxs-lookup"><span data-stu-id="1f973-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="1f973-136">搜尋 hello 詞彙 '預算' hello 整個索引並傳回僅 hello`hotelName`欄位：</span><span class="sxs-lookup"><span data-stu-id="1f973-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="1f973-137">套用篩選器 toohello 索引 toofind 旅館比每晚，$150 廉價，並傳回 hello`hotelId`和`description`:</span><span class="sxs-lookup"><span data-stu-id="1f973-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="1f973-138">搜尋 hello 整個索引中，依特定欄位的順序 (`lastRenovationDate`) 以遞減順序，hello 前兩個結果，並只顯示`hotelName`和`lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="1f973-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="1f973-139">提交 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="1f973-139">Submit your HTTP request</span></span>
<span data-ttu-id="1f973-140">現在您已將查詢編寫為 HTTP 要求 URL (若為 GET) 或主體 (若為 POST) 的一部分，接下來您可以定義要求標頭並提交查詢。</span><span class="sxs-lookup"><span data-stu-id="1f973-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="1f973-141">要求和要求標頭</span><span class="sxs-lookup"><span data-stu-id="1f973-141">Request and Request Headers</span></span>
<span data-ttu-id="1f973-142">您必須為 GET 定義兩個要求標頭，若為 POST 則必須定義三個：</span><span class="sxs-lookup"><span data-stu-id="1f973-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="1f973-143">hello`api-key`標頭必須設定您在步驟中找到我上述 toohello 查詢索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1f973-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="1f973-144">您也可以使用 管理金鑰為 hello`api-key`標頭，但建議您使用的是查詢索引鍵，因為它只會授與唯讀存取 tooindexes 和文件。</span><span class="sxs-lookup"><span data-stu-id="1f973-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="1f973-145">hello`Accept`標頭必須設定太`application/json`。</span><span class="sxs-lookup"><span data-stu-id="1f973-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="1f973-146">只有 post hello`Content-Type`標頭也應該設定太`application/json`。</span><span class="sxs-lookup"><span data-stu-id="1f973-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="1f973-147">HTTP GET 要求 toosearch hello 「 旅館"索引使用 Azure 搜尋 REST API，使用簡單的查詢可搜尋 hello 詞彙"motel"hello，請參閱下面的內容：</span><span class="sxs-lookup"><span data-stu-id="1f973-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="1f973-148">以下是相同的 hello 範例查詢中，這次使用 HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="1f973-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="1f973-149">成功的查詢要求會導致狀態碼`200 OK`和 hello 搜尋結果傳回成 JSON hello 回應主體中。</span><span class="sxs-lookup"><span data-stu-id="1f973-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="1f973-150">以下是 hello 上述查詢看起來像是，假設 hello 「 旅館"索引填入資料中的 hello 範例會產生哪些 hello[在 Azure 搜尋中使用的資料匯入 hello REST API](search-import-data-rest-api.md) （請注意為了清楚起見，已設定格式 JSON 該 hello）。</span><span class="sxs-lookup"><span data-stu-id="1f973-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="1f973-151">toolearn 詳細資訊，請瀏覽 hello 「 回應 」 一節[搜尋文件](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)。</span><span class="sxs-lookup"><span data-stu-id="1f973-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="1f973-152">如需失敗時可能傳回的其他 HTTP 狀態碼詳細資訊，請參閱 [HTTP 狀態碼 (Azure 搜尋服務)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)。</span><span class="sxs-lookup"><span data-stu-id="1f973-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
