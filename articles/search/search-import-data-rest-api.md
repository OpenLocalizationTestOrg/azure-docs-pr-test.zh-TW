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
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="f5062-103">上傳資料 tooAzure 搜尋使用 hello REST API</span><span class="sxs-lookup"><span data-stu-id="f5062-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="f5062-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f5062-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="f5062-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f5062-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="f5062-106">REST</span><span class="sxs-lookup"><span data-stu-id="f5062-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="f5062-107">這篇文章將示範如何 toouse hello [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport 資料到 Azure 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="f5062-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="f5062-108">在開始閱讀本逐步解說前，請先 [建立好 Azure 搜尋服務索引](search-what-is-an-index.md)。</span><span class="sxs-lookup"><span data-stu-id="f5062-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="f5062-109">在訂單 toopush 文件至您的索引使用 hello REST API，您將會發出 HTTP POST 要求 tooyour 索引 URL 端點。</span><span class="sxs-lookup"><span data-stu-id="f5062-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="f5062-110">hello 主體的 hello HTTP 要求主體是包含 toobe 新增、 修改或刪除的 hello 文件的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="f5062-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="f5062-111">識別 Azure 搜尋服務的系統管理 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="f5062-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="f5062-112">發行您的服務使用 hello REST API，針對 HTTP 要求時*每個*API 要求都必須包含 hello api 金鑰 hello 您佈建的搜尋服務所產生。</span><span class="sxs-lookup"><span data-stu-id="f5062-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="f5062-113">擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。</span><span class="sxs-lookup"><span data-stu-id="f5062-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="f5062-114">toofind 服務的 api 金鑰，您可以登入 toohello [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="f5062-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="f5062-115">移 tooyour Azure 搜尋服務的刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="f5062-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="f5062-116">按一下 hello 「 金鑰 」 圖示</span><span class="sxs-lookup"><span data-stu-id="f5062-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="f5062-117">服務會有系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="f5062-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="f5062-118">您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。</span><span class="sxs-lookup"><span data-stu-id="f5062-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="f5062-119">有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="f5062-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="f5062-120">您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5062-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="f5062-121">基於 hello 匯入資料到索引，您可以使用主要或次要管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="f5062-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="f5062-122">決定哪個索引動作 toouse</span><span class="sxs-lookup"><span data-stu-id="f5062-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="f5062-123">使用 hello REST API，您就會發出 HTTP POST 要求，JSON 要求內文 tooyour Azure 搜尋索引的端點 URL。</span><span class="sxs-lookup"><span data-stu-id="f5062-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="f5062-124">您的 HTTP 要求主體中的 hello JSON 物件會包含單一的 JSON 陣列名為"value"包含代表您想要 tooadd tooyour 索引的文件的 JSON 物件，更新或刪除。</span><span class="sxs-lookup"><span data-stu-id="f5062-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="f5062-125">Hello"value"陣列中的每個 JSON 物件表示文件 toobe 編製索引。</span><span class="sxs-lookup"><span data-stu-id="f5062-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="f5062-126">每個物件包含 hello 文件索引鍵，並指定所需的 hello 索引動作 （上傳、 合併、 刪除等等）。</span><span class="sxs-lookup"><span data-stu-id="f5062-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="f5062-127">取決於哪些 hello 下列您選擇的動作，只有特定欄位必須包含每個文件：</span><span class="sxs-lookup"><span data-stu-id="f5062-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="f5062-128">說明</span><span class="sxs-lookup"><span data-stu-id="f5062-128">Description</span></span> | <span data-ttu-id="f5062-129">每個文件的必要欄位</span><span class="sxs-lookup"><span data-stu-id="f5062-129">Necessary fields for each document</span></span> | <span data-ttu-id="f5062-130">注意事項</span><span class="sxs-lookup"><span data-stu-id="f5062-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="f5062-131">`upload`動作是類似 tooan"upsert"(如果它是新插入和更新/取代如果它存在 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="f5062-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="f5062-132">索引鍵，再加上您想 toodefine 的任何其他欄位</span><span class="sxs-lookup"><span data-stu-id="f5062-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="f5062-133">當更新/取代現有的文件，hello 要求中未指定任何欄位將會有其欄位太設定`null`。</span><span class="sxs-lookup"><span data-stu-id="f5062-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="f5062-134">這是即使 hello 欄位先前設定 tooa 非 null 值。</span><span class="sxs-lookup"><span data-stu-id="f5062-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="f5062-135">更新現有文件以 hello 指定欄位。</span><span class="sxs-lookup"><span data-stu-id="f5062-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="f5062-136">Hello 文件不存在 hello 索引中，如果 hello 合併將會失敗。</span><span class="sxs-lookup"><span data-stu-id="f5062-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="f5062-137">索引鍵，再加上您想 toodefine 的任何其他欄位</span><span class="sxs-lookup"><span data-stu-id="f5062-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="f5062-138">您在合併中指定任何欄位將會取代 hello hello 文件中的現有欄位。</span><span class="sxs-lookup"><span data-stu-id="f5062-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="f5062-139">這包括類型 `Collection(Edm.String)`的欄位。</span><span class="sxs-lookup"><span data-stu-id="f5062-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="f5062-140">例如，如果 hello 文件包含欄位`tags`值`["budget"]`和執行的合併值`["economy", "pool"]`的`tags`，hello hello 的最終值`tags`欄位就是`["economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="f5062-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="f5062-141">而不會是 `["budget", "economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="f5062-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="f5062-142">此動作的行為類似`merge`如果 hello 索引中的文件以 hello 給定索引鍵已經存在。</span><span class="sxs-lookup"><span data-stu-id="f5062-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="f5062-143">如果 hello 文件不存在，它的行為類似`upload`與新的文件。</span><span class="sxs-lookup"><span data-stu-id="f5062-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="f5062-144">索引鍵，再加上您想 toodefine 的任何其他欄位</span><span class="sxs-lookup"><span data-stu-id="f5062-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="f5062-145">從 hello 索引中移除 hello 指定文件。</span><span class="sxs-lookup"><span data-stu-id="f5062-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="f5062-146">僅索引鍵</span><span class="sxs-lookup"><span data-stu-id="f5062-146">key only</span></span> |<span data-ttu-id="f5062-147">您指定其他非 hello 索引鍵欄位將會忽略所有的欄位。</span><span class="sxs-lookup"><span data-stu-id="f5062-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="f5062-148">如果您想 tooremove 個別欄位從 文件，請使用`merge`相反地，並直接將 hello 欄位明確 toonull。</span><span class="sxs-lookup"><span data-stu-id="f5062-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="f5062-149">建構 HTTP 要求和要求本文</span><span class="sxs-lookup"><span data-stu-id="f5062-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="f5062-150">既然您已經收集 hello 必要的欄位值的索引動作，您已準備好 tooconstruct hello 實際的 HTTP 要求和 JSON 要求主體 tooimport 您的資料。</span><span class="sxs-lookup"><span data-stu-id="f5062-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="f5062-151">要求和要求標頭</span><span class="sxs-lookup"><span data-stu-id="f5062-151">Request and Request Headers</span></span>
<span data-ttu-id="f5062-152">在 hello URL，您將需要 tooprovide 您服務名稱、 索引名稱 （"旅館 「 在此情況下），以及 hello 適當的 API 版本 (hello 目前的 API 版本是`2016-09-01`次發行本文件的 hello)。</span><span class="sxs-lookup"><span data-stu-id="f5062-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="f5062-153">您將需要 toodefine hello`Content-Type`和`api-key`要求標頭。</span><span class="sxs-lookup"><span data-stu-id="f5062-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="f5062-154">Hello 後者，使用其中一個服務的系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="f5062-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="f5062-155">要求本文</span><span class="sxs-lookup"><span data-stu-id="f5062-155">Request Body</span></span>
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

<span data-ttu-id="f5062-156">在本案例中，我們會使用 `upload`、`mergeOrUpload` 和 `delete` 做為搜尋動作。</span><span class="sxs-lookup"><span data-stu-id="f5062-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="f5062-157">假設此 "hotels" 索引範例已填入幾份文件。</span><span class="sxs-lookup"><span data-stu-id="f5062-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="f5062-158">請注意如何我們沒有 toospecify hello 可能文件的所有欄位時使用`mergeOrUpload`以及我們僅指定 hello 文件索引鍵的方式 (`hotelId`) 時使用`delete`。</span><span class="sxs-lookup"><span data-stu-id="f5062-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="f5062-159">此外，請注意，您只可包含 too1000 文件 （或 16MB） 在單一索引要求。</span><span class="sxs-lookup"><span data-stu-id="f5062-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="f5062-160">了解 HTTP 回應碼</span><span class="sxs-lookup"><span data-stu-id="f5062-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="f5062-161">200</span><span class="sxs-lookup"><span data-stu-id="f5062-161">200</span></span>
<span data-ttu-id="f5062-162">成功提交索引編製要求後，您會收到狀態碼為 `200 OK`的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="f5062-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="f5062-163">hello hello HTTP 回應的 JSON 主體會如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5062-163">hello JSON body of hello HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="f5062-164">207</span><span class="sxs-lookup"><span data-stu-id="f5062-164">207</span></span>
<span data-ttu-id="f5062-165">至少有一個項目未成功建立索引時會傳回狀態碼 `207` 。</span><span class="sxs-lookup"><span data-stu-id="f5062-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="f5062-166">hello hello HTTP 回應的 JSON 主體會包含 hello 失敗的文件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f5062-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

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
> <span data-ttu-id="f5062-167">這通常表示該 hello 載入您的搜尋服務即將達到索引要求會在開始 tooreturn 點`503`回應。</span><span class="sxs-lookup"><span data-stu-id="f5062-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="f5062-168">在此情況下，強烈建議您先讓用戶端程式碼退回並稍候一會，然後再重試。</span><span class="sxs-lookup"><span data-stu-id="f5062-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="f5062-169">這可讓某些時間 toorecover，增加未來的要求將會成功的 hello 機會 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="f5062-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="f5062-170">快速重試您的要求將只會在保留 hello 的情況。</span><span class="sxs-lookup"><span data-stu-id="f5062-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="f5062-171">429</span><span class="sxs-lookup"><span data-stu-id="f5062-171">429</span></span>
<span data-ttu-id="f5062-172">狀態碼`429`您已超過每個索引的文件的 hello 數目配額時，會傳回。</span><span class="sxs-lookup"><span data-stu-id="f5062-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="f5062-173">503</span><span class="sxs-lookup"><span data-stu-id="f5062-173">503</span></span>
<span data-ttu-id="f5062-174">狀態碼`503`將會傳回如果無 hello hello 要求中的項目已成功編製索引。</span><span class="sxs-lookup"><span data-stu-id="f5062-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="f5062-175">此錯誤表示 hello 系統負載過重時，此時無法處理您的要求。</span><span class="sxs-lookup"><span data-stu-id="f5062-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="f5062-176">在此情況下，強烈建議您先讓用戶端程式碼退回並稍候一會，然後再重試。</span><span class="sxs-lookup"><span data-stu-id="f5062-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="f5062-177">這可讓某些時間 toorecover，增加未來的要求將會成功的 hello 機會 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="f5062-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="f5062-178">快速重試您的要求將只會在保留 hello 的情況。</span><span class="sxs-lookup"><span data-stu-id="f5062-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="f5062-179">如需文件動作和成功/錯誤回應的詳細資訊，請參閱 [加入、更新或刪除文件](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)。</span><span class="sxs-lookup"><span data-stu-id="f5062-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="f5062-180">如需失敗時可能傳回的其他 HTTP 狀態碼詳細資訊，請參閱 [HTTP 狀態碼 (Azure 搜尋服務)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)。</span><span class="sxs-lookup"><span data-stu-id="f5062-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5062-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5062-181">Next steps</span></span>
<span data-ttu-id="f5062-182">填入您的 Azure 搜尋索引之後, 會準備 toostart 發出查詢 toosearch 文件。</span><span class="sxs-lookup"><span data-stu-id="f5062-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="f5062-183">如需詳細資料，請參閱 [查詢 Azure 搜尋服務索引](search-query-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="f5062-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
