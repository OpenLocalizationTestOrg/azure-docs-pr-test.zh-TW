---
title: "查詢索引 (REST API - Azure 搜尋服務) | Microsoft Docs"
description: "在 Azure 搜尋服務中建立搜尋查詢，並使用搜尋參數來篩選及排序搜尋結果。"
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
ms.openlocfilehash: 49062bec233ad35cd457f9665fa94c1855343582
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-rest-api"></a><span data-ttu-id="9befa-103">使用 REST API 查詢 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="9befa-103">Query your Azure Search index using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="9befa-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9befa-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="9befa-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="9befa-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="9befa-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9befa-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="9befa-107">REST</span><span class="sxs-lookup"><span data-stu-id="9befa-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="9befa-108">本文說明如何使用 [Azure 搜尋服務 REST API](https://docs.microsoft.com/rest/api/searchservice/) 查詢索引。</span><span class="sxs-lookup"><span data-stu-id="9befa-108">This article shows you how to query an index using the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="9befa-109">在開始閱讀本逐步解說前，請先[建立好 Azure 搜尋服務索引](search-what-is-an-index.md)，並[在索引中填入資料](search-what-is-data-import.md)。</span><span class="sxs-lookup"><span data-stu-id="9befa-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="9befa-110">如需有關背景資訊，請參閱[全文檢索搜尋如何在 Azure 搜尋服務中運作](search-lucene-query-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="9befa-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="9befa-111">識別 Azure 搜尋服務的查詢 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="9befa-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="9befa-112">針對 Azure 搜尋服務 REST API 所執行之每個搜尋作業的主要元件是針對所佈建之服務產生的 API 金鑰  。</span><span class="sxs-lookup"><span data-stu-id="9befa-112">A key component of every search operation against the Azure Search REST API is the *api-key* that was generated for the service you provisioned.</span></span> <span data-ttu-id="9befa-113">擁有有效的金鑰就能為每個要求在傳送要求之應用程式與處理要求之服務間建立信任。</span><span class="sxs-lookup"><span data-stu-id="9befa-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="9befa-114">若要尋找服務的 API 金鑰，您可以登入 [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9befa-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="9befa-115">前往 Azure 搜尋服務的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9befa-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="9befa-116">按一下 [金鑰] 圖示</span><span class="sxs-lookup"><span data-stu-id="9befa-116">Click the "Keys" icon</span></span>

<span data-ttu-id="9befa-117">您的服務有「系統管理金鑰」和「查詢金鑰」。</span><span class="sxs-lookup"><span data-stu-id="9befa-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="9befa-118">主要和次要系統管理金鑰  會授與所有作業的完整權限，包括管理服務以及建立和刪除索引、索引子與資料來源的能力。</span><span class="sxs-lookup"><span data-stu-id="9befa-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="9befa-119">由於有兩個金鑰，因此如果您決定重新產生主要金鑰，您可以繼續使用次要金鑰，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="9befa-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="9befa-120">查詢金鑰  會授與索引和文件的唯讀存取權，且通常會分派給發出搜尋要求的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="9befa-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="9befa-121">若要查詢索引，您可以使用其中一個查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="9befa-121">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="9befa-122">系統管理金鑰也可以用於進行查詢，但是您應該在應用程式的程式碼中使用查詢金鑰，因為查詢金鑰更加符合 [最低權限準則](https://en.wikipedia.org/wiki/Principle_of_least_privilege)。</span><span class="sxs-lookup"><span data-stu-id="9befa-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="9befa-123">編寫查詢</span><span class="sxs-lookup"><span data-stu-id="9befa-123">Formulate your query</span></span>
<span data-ttu-id="9befa-124">有兩種方式可以 [使用 REST API 搜尋索引](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)。</span><span class="sxs-lookup"><span data-stu-id="9befa-124">There are two ways to [search your index using the REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="9befa-125">其中一種方式是發出 HTTP POST 要求，並將查詢參數定義在要求主體的 JSON 物件中。</span><span class="sxs-lookup"><span data-stu-id="9befa-125">One way is to issue an HTTP POST request where your query parameters are defined in a JSON object in the request body.</span></span> <span data-ttu-id="9befa-126">另一種方式是發出 HTTP GET 要求，並將查詢參數定義在要求 URL 中。</span><span class="sxs-lookup"><span data-stu-id="9befa-126">The other way is to issue an HTTP GET request where your query parameters are defined within the request URL.</span></span> <span data-ttu-id="9befa-127">在查詢參數的大小方面，POST 比 GET 擁有[更寬鬆的限制](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)。</span><span class="sxs-lookup"><span data-stu-id="9befa-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on the size of query parameters than GET.</span></span> <span data-ttu-id="9befa-128">因此，除非您的情況特殊導致使用 GET 會比較方便，否則建議您使用 POST。</span><span class="sxs-lookup"><span data-stu-id="9befa-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="9befa-129">不管是 POST 還是 GET，您都需要在要求 URL 中提供服務名稱、索引名稱和適當的 API 版本 (本文件發行時的最新 API 版本是 `2016-09-01`)。</span><span class="sxs-lookup"><span data-stu-id="9befa-129">For both POST and GET, you need to provide your *service name*, *index name*, and the proper *API version* (the current API version is `2016-09-01` at the time of publishing this document) in the request URL.</span></span> <span data-ttu-id="9befa-130">若為 GET，URL 結尾的「查詢字串」是您用來提供查詢參數的位置。</span><span class="sxs-lookup"><span data-stu-id="9befa-130">For GET, the *query string* at the end of the URL is where you provide the query parameters.</span></span> <span data-ttu-id="9befa-131">URL 的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="9befa-131">See below for the URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="9befa-132">POST 的格式同上，但查詢字串參數中只有 API 版本。</span><span class="sxs-lookup"><span data-stu-id="9befa-132">The format for POST is the same, but with only api-version in the query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="9befa-133">查詢範例</span><span class="sxs-lookup"><span data-stu-id="9befa-133">Example Queries</span></span>
<span data-ttu-id="9befa-134">以下是幾個名為 "hotels" 之索引的查詢範例。</span><span class="sxs-lookup"><span data-stu-id="9befa-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="9befa-135">範例中會同時顯示 GET 和 POST 格式的查詢。</span><span class="sxs-lookup"><span data-stu-id="9befa-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="9befa-136">在整個索引中搜尋 'budget' 一詞，並只傳回 `hotelName` 欄位：</span><span class="sxs-lookup"><span data-stu-id="9befa-136">Search the entire index for the term 'budget' and return only the `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="9befa-137">將篩選套用到索引，以尋找每晚房價低於美金 $150 元的旅館，並傳回 `hotelId` 和 `description`：</span><span class="sxs-lookup"><span data-stu-id="9befa-137">Apply a filter to the index to find hotels cheaper than $150 per night, and return the `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="9befa-138">搜尋整個索引，依特定欄位 (`lastRenovationDate`) 以遞減順序排序，取前兩個結果，並只顯示 `hotelName` 和 `lastRenovationDate`：</span><span class="sxs-lookup"><span data-stu-id="9befa-138">Search the entire index, order by a specific field (`lastRenovationDate`) in descending order, take the top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="9befa-139">提交 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="9befa-139">Submit your HTTP request</span></span>
<span data-ttu-id="9befa-140">現在您已將查詢編寫為 HTTP 要求 URL (若為 GET) 或主體 (若為 POST) 的一部分，接下來您可以定義要求標頭並提交查詢。</span><span class="sxs-lookup"><span data-stu-id="9befa-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="9befa-141">要求和要求標頭</span><span class="sxs-lookup"><span data-stu-id="9befa-141">Request and Request Headers</span></span>
<span data-ttu-id="9befa-142">您必須為 GET 定義兩個要求標頭，若為 POST 則必須定義三個：</span><span class="sxs-lookup"><span data-stu-id="9befa-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="9befa-143">`api-key` 標頭必須設為您在上面的步驟 I 中找到的查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="9befa-143">The `api-key` header must be set to the query key you found in step I above.</span></span> <span data-ttu-id="9befa-144">您也可以使用系統管理金鑰作為 `api-key` 標頭，但建議您使用查詢金鑰，因為其可獨佔授與索引和文件的唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="9befa-144">You can also use an admin key as the `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access to indexes and documents.</span></span>
2. <span data-ttu-id="9befa-145">`Accept` 標頭必須設為 `application/json`。</span><span class="sxs-lookup"><span data-stu-id="9befa-145">The `Accept` header must be set to `application/json`.</span></span>
3. <span data-ttu-id="9befa-146">僅對於 POST，`Content-Type` 標頭也應該設為 `application/json`。</span><span class="sxs-lookup"><span data-stu-id="9befa-146">For POST only, the `Content-Type` header should also be set to `application/json`.</span></span>

<span data-ttu-id="9befa-147">請參閱以下內容來取得使用 Azure 搜尋服務 REST API 搜尋 "hotels" 索引的 HTTP GET 要求，其使用簡單的查詢來搜尋 "motel" 一詞：</span><span class="sxs-lookup"><span data-stu-id="9befa-147">See below for an HTTP GET request to search the "hotels" index using the Azure Search REST API, using a simple query that searches for the term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="9befa-148">以下是相同的查詢範例，但這次使用的是 HTTP POST：</span><span class="sxs-lookup"><span data-stu-id="9befa-148">Here is the same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="9befa-149">成功的查詢要求會產生 `200 OK` 的狀態碼，且搜尋結果會在回應主體中以 JSON 形式傳回。</span><span class="sxs-lookup"><span data-stu-id="9befa-149">A successful query request will result in a Status Code of `200 OK` and the search results are returned as JSON in the response body.</span></span> <span data-ttu-id="9befa-150">以下是上述查詢結果的可能樣貌，此處假設 "hotels" 索引是以 [在 Azure 搜尋服務中使用 REST API 匯入資料](search-import-data-rest-api.md) 中的範例資料填入 (請注意，為了清楚起見，JSON 已經過格式化)。</span><span class="sxs-lookup"><span data-stu-id="9befa-150">Here is what the results for the above query look like, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the REST API](search-import-data-rest-api.md) (note that the JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="9befa-151">若要深入了解，請瀏覽 [搜尋文件](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)的＜回應＞一節。</span><span class="sxs-lookup"><span data-stu-id="9befa-151">To learn more, please visit the "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="9befa-152">如需失敗時可能傳回的其他 HTTP 狀態碼詳細資訊，請參閱 [HTTP 狀態碼 (Azure 搜尋服務)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)。</span><span class="sxs-lookup"><span data-stu-id="9befa-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
