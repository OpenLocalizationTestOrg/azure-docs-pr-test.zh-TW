---
title: "上傳資料 (REST API - Azure 搜尋服務) | Microsoft Docs"
description: "了解如何使用 REST API 將資料上傳至 Azure 搜尋服務中的索引。"
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
ms.openlocfilehash: f22a33ed86fbfc46dfa732239263a49f34c4afee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-rest-api"></a><span data-ttu-id="9f2c1-103">使用 REST API 將資料上傳至 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="9f2c1-103">Upload data to Azure Search using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="9f2c1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9f2c1-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="9f2c1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9f2c1-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="9f2c1-106">REST</span><span class="sxs-lookup"><span data-stu-id="9f2c1-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="9f2c1-107">本文將說明如何使用 [Azure 搜尋服務 REST API](https://docs.microsoft.com/rest/api/searchservice/) 將資料匯入 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-107">This article will show you how to use the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) to import data into an Azure Search index.</span></span>

<span data-ttu-id="9f2c1-108">在開始閱讀本逐步解說前，請先 [建立好 Azure 搜尋服務索引](search-what-is-an-index.md)。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="9f2c1-109">若要使用 REST API 將文件推送至索引，您會發出 HTTP POST 要求至您的索引 URL 端點。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-109">In order to push documents into your index using the REST API, you will issue an HTTP POST request to your index's URL endpoint.</span></span> <span data-ttu-id="9f2c1-110">HTTP 要求主體是包含要新增、修改或刪除之文件的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-110">The body of the HTTP request body is a JSON object containing the documents to be added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="9f2c1-111">識別 Azure 搜尋服務的系統管理 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="9f2c1-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="9f2c1-112">使用 REST API 對服務發出 HTTP 要求時，每個  API 要求都必須包含針對您佈建的搜尋服務所產生的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-112">When issuing HTTP requests against your service using the REST API, *each* API request must include the api-key that was generated for the Search service you provisioned.</span></span> <span data-ttu-id="9f2c1-113">擁有有效的金鑰就能為每個要求在傳送要求之應用程式與處理要求之服務間建立信任。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="9f2c1-114">若要尋找服務的 API 金鑰，您可以登入 [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9f2c1-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="9f2c1-115">前往 Azure 搜尋服務的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="9f2c1-116">按一下 [金鑰] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-116">Click on the "Keys" icon</span></span>

<span data-ttu-id="9f2c1-117">服務會有系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="9f2c1-118">主要和次要系統管理金鑰  會授與所有作業的完整權限，包括管理服務以及建立和刪除索引、索引子與資料來源的能力。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="9f2c1-119">由於有兩個金鑰，因此如果您決定重新產生主要金鑰，您可以繼續使用次要金鑰，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="9f2c1-120">查詢金鑰  會授與索引和文件的唯讀存取權，且通常會分派給發出搜尋要求的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="9f2c1-121">主要或次要系統管理金鑰都可用於將資料匯入索引。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-121">For the purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="9f2c1-122">決定要使用的索引編製動作</span><span class="sxs-lookup"><span data-stu-id="9f2c1-122">Decide which indexing action to use</span></span>
<span data-ttu-id="9f2c1-123">使用 REST API 時，您會發行具有 JSON 要求主體的 HTTP POST 要求到 Azure 搜尋服務索引的端點 URL。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-123">When using the REST API, you will issue HTTP POST requests with JSON request bodies to your Azure Search index's endpoint URL.</span></span> <span data-ttu-id="9f2c1-124">HTTP 要求主體中的 JSON 物件會包含名為 "value" 的單一 JSON 陣列，陣列中則有代表想要新增至索引、更新或刪除之文件的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-124">The JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like to add to your index, update, or delete.</span></span>

<span data-ttu-id="9f2c1-125">"value" 陣列中的每個 JSON 物件代表要編製索引的文件。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-125">Each JSON object in the "value" array represents a document to be indexed.</span></span> <span data-ttu-id="9f2c1-126">這些物件每一個都含有文件的索引鍵，並且會指定所需的索引編製動作 (上傳、合併、刪除等)。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-126">Each of these objects contains the document's key and specifies the desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="9f2c1-127">依據您在以下動作中所做的選擇，每個文件內只需包含某些欄位：</span><span class="sxs-lookup"><span data-stu-id="9f2c1-127">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="9f2c1-128">說明</span><span class="sxs-lookup"><span data-stu-id="9f2c1-128">Description</span></span> | <span data-ttu-id="9f2c1-129">每個文件的必要欄位</span><span class="sxs-lookup"><span data-stu-id="9f2c1-129">Necessary fields for each document</span></span> | <span data-ttu-id="9f2c1-130">注意事項</span><span class="sxs-lookup"><span data-stu-id="9f2c1-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="9f2c1-131">`upload` 動作類似「upsert」，如果是新文件，就會插入該文件，如果文件已經存在，就會更新/取代它。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-131">An `upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="9f2c1-132">索引鍵以及其他任何您想要定義的欄位</span><span class="sxs-lookup"><span data-stu-id="9f2c1-132">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="9f2c1-133">在更新/取代現有文件時，要求中未指定的欄位會將其欄位設定為 `null`。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-133">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="9f2c1-134">即使先前已將欄位設定為非 null 值也是一樣。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-134">This occurs even when the field was previously set to a non-null value.</span></span> |
| `merge` |<span data-ttu-id="9f2c1-135">使用指定的欄位更新現有文件。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-135">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="9f2c1-136">如果文件不存在於索引中，合併就會失敗。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-136">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="9f2c1-137">索引鍵以及其他任何您想要定義的欄位</span><span class="sxs-lookup"><span data-stu-id="9f2c1-137">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="9f2c1-138">您在合併中指定的任何欄位將取代文件中現有的欄位。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-138">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="9f2c1-139">這包括類型 `Collection(Edm.String)`的欄位。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="9f2c1-140">例如，如果文件包含欄位 `tags` 且值為 `["budget"]`，而您使用值 `["economy", "pool"]` 針對 `tags` 執行合併，則 `tags` 欄位最後的值會是 `["economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-140">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="9f2c1-141">而不會是 `["budget", "economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="9f2c1-142">如果含有指定索引鍵的文件已經存在於索引中，則此動作的行為會類似 `merge`。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-142">This action behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="9f2c1-143">如果文件不存在，其行為會類似新文件的 `upload` 。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-143">If the document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="9f2c1-144">索引鍵以及其他任何您想要定義的欄位</span><span class="sxs-lookup"><span data-stu-id="9f2c1-144">key, plus any other fields you wish to define</span></span> |- |
| `delete` |<span data-ttu-id="9f2c1-145">從索引中移除指定的文件。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-145">Removes the specified document from the index.</span></span> |<span data-ttu-id="9f2c1-146">僅索引鍵</span><span class="sxs-lookup"><span data-stu-id="9f2c1-146">key only</span></span> |<span data-ttu-id="9f2c1-147">您指定的所有欄位 (索引鍵欄位除外) 都將被忽略。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-147">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="9f2c1-148">如果您想要從文件中移除個別欄位，請改用 `merge` ，而且只需明確地將該欄位設為 null。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-148">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to null.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="9f2c1-149">建構 HTTP 要求和要求本文</span><span class="sxs-lookup"><span data-stu-id="9f2c1-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="9f2c1-150">既然您已收集好索引動作的必要欄位值，您可以開始建構實際的 HTTP 要求和 JSON 要求主體以匯入資料。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-150">Now that you have gathered the necessary field values for your index actions, you are ready to construct the actual HTTP request and JSON request body to import your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="9f2c1-151">要求和要求標頭</span><span class="sxs-lookup"><span data-stu-id="9f2c1-151">Request and Request Headers</span></span>
<span data-ttu-id="9f2c1-152">您需要在 URL 中提供服務名稱、索引名稱 (在本例中為 "hotels") 以及適當的 API 版本 (本文件發行時的最新 API 版本是 `2016-09-01` )。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-152">In the URL, you will need to provide your service name, index name ("hotels" in this case), as well as the proper API version (the current API version is `2016-09-01` at the time of publishing this document).</span></span> <span data-ttu-id="9f2c1-153">您也需要定義 `Content-Type` 和 `api-key` 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-153">You will need to define the `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="9f2c1-154">請對後者使用服務的其中一個系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-154">For the latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="9f2c1-155">要求本文</span><span class="sxs-lookup"><span data-stu-id="9f2c1-155">Request Body</span></span>
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
            "description": "Close to town hall and the river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="9f2c1-156">在本案例中，我們會使用 `upload`、`mergeOrUpload` 和 `delete` 做為搜尋動作。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="9f2c1-157">假設此 "hotels" 索引範例已填入幾份文件。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="9f2c1-158">請留意我們在使用 `mergeOrUpload` 時是如何不必指定所有可能的文件欄位，以及在使用 `delete` 時如何僅指定文件索引鍵 (`hotelId`)。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-158">Note how we did not have to specify all the possible document fields when using `mergeOrUpload` and how we only specified the document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="9f2c1-159">另請注意，每個索引編製要求中最多只能包含 1000 份文件 (或 16 MB)。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-159">Also, note that you can only include up to 1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="9f2c1-160">了解 HTTP 回應碼</span><span class="sxs-lookup"><span data-stu-id="9f2c1-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="9f2c1-161">200</span><span class="sxs-lookup"><span data-stu-id="9f2c1-161">200</span></span>
<span data-ttu-id="9f2c1-162">成功提交索引編製要求後，您會收到狀態碼為 `200 OK`的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="9f2c1-163">HTTP 回應的 JSON 主體如下所示：</span><span class="sxs-lookup"><span data-stu-id="9f2c1-163">The JSON body of the HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="9f2c1-164">207</span><span class="sxs-lookup"><span data-stu-id="9f2c1-164">207</span></span>
<span data-ttu-id="9f2c1-165">至少有一個項目未成功建立索引時會傳回狀態碼 `207` 。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="9f2c1-166">HTTP 回應的 JSON 主體會包含未成功之文件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-166">The JSON body of the HTTP response will contain information about the unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "The search service is too busy to process this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="9f2c1-167">這通常表示搜尋服務的負載即將達到索引編製要求會開始傳回 `503` 回應的臨界點。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-167">This often means that the load on your search service is reaching a point where indexing requests will begin to return `503` responses.</span></span> <span data-ttu-id="9f2c1-168">在此情況下，強烈建議您先讓用戶端程式碼退回並稍候一會，然後再重試。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="9f2c1-169">這可讓系統有時間復原，以增加未來之要求的成功機會。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-169">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="9f2c1-170">快速重試要求只會讓這種情況持續下去。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-170">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="9f2c1-171">429</span><span class="sxs-lookup"><span data-stu-id="9f2c1-171">429</span></span>
<span data-ttu-id="9f2c1-172">當您已經超過每個索引的文件數量配額時，將會傳回 `429` 的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-172">A status code of `429` will be returned when you have exceeded your quota on the number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="9f2c1-173">503</span><span class="sxs-lookup"><span data-stu-id="9f2c1-173">503</span></span>
<span data-ttu-id="9f2c1-174">如果要求中的所有項目皆未成功建立索引，將會傳回 `503` 的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-174">A status code of `503` will be returned if none of the items in the request were successfully indexed.</span></span> <span data-ttu-id="9f2c1-175">此錯誤表示系統負載過重，因此目前無法處理要求。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-175">This error means that the system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="9f2c1-176">在此情況下，強烈建議您先讓用戶端程式碼退回並稍候一會，然後再重試。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="9f2c1-177">這可讓系統有時間復原，以增加未來之要求的成功機會。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-177">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="9f2c1-178">快速重試要求只會讓這種情況持續下去。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-178">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

<span data-ttu-id="9f2c1-179">如需文件動作和成功/錯誤回應的詳細資訊，請參閱 [加入、更新或刪除文件](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="9f2c1-180">如需失敗時可能傳回的其他 HTTP 狀態碼詳細資訊，請參閱 [HTTP 狀態碼 (Azure 搜尋服務)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f2c1-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f2c1-181">Next steps</span></span>
<span data-ttu-id="9f2c1-182">在填入 Azure 搜尋服務索引後，您就可以開始發出查詢來搜尋文件。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-182">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="9f2c1-183">如需詳細資料，請參閱 [查詢 Azure 搜尋服務索引](search-query-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="9f2c1-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
