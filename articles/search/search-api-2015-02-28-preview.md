---
title: "搜尋服務 REST API 版本 2015年-02-28-preview aaaAzure |Microsoft 文件"
description: "Azure 搜尋服務 REST API Version 2015-02-28-Preview 包含自然語言分析器和 moreLikeThis 搜尋等實驗性功能。"
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="1bf46-103">Azure 搜尋服務 REST API：版本 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="1bf46-104">這篇文章是 hello 參考文件集`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-105">這個預覽擴充 hello 正式推出新版， [api 版本 = 2015年-02-28](https://msdn.microsoft.com/library/dn798935.aspx)，藉由提供下列實驗性功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="1bf46-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="1bf46-106">`moreLikeThis`查詢參數 hello[搜尋文件](#SearchDocs)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1bf46-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="1bf46-107">它會找到相關 tooanother 特定文件的其他文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="1bf46-108">少數的其他組件 hello `2015-02-28-Preview` REST API 的說明文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="1bf46-109">其中包含：</span><span class="sxs-lookup"><span data-stu-id="1bf46-109">These include:</span></span>

* [<span data-ttu-id="1bf46-110">評分設定檔</span><span class="sxs-lookup"><span data-stu-id="1bf46-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="1bf46-111">索引子</span><span class="sxs-lookup"><span data-stu-id="1bf46-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="1bf46-112">Azure 搜尋服務可以在多個版本中使用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="1bf46-113">請參閱太[搜尋服務版本控制](http://msdn.microsoft.com/library/azure/dn864560.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1bf46-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="1bf46-114">本文件中的 API</span><span class="sxs-lookup"><span data-stu-id="1bf46-114">APIs in this document</span></span>
<span data-ttu-id="1bf46-115">Azure 搜尋服務 API 對 API 作業支援兩種 URL 語法：簡單和 OData (如需詳細資訊，請參閱 [OData 支援 (Azure 搜尋 API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) )。</span><span class="sxs-lookup"><span data-stu-id="1bf46-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="1bf46-116">hello 下列清單顯示 hello 簡單的語法。</span><span class="sxs-lookup"><span data-stu-id="1bf46-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="1bf46-117">建立索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-118">更新索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-119">取得索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-120">列出索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-121">取得索引統計資料</span><span class="sxs-lookup"><span data-stu-id="1bf46-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-122">測試分析器</span><span class="sxs-lookup"><span data-stu-id="1bf46-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-123">删除索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-124">新增、刪除及更新索引內的資料</span><span class="sxs-lookup"><span data-stu-id="1bf46-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-125">搜尋文件</span><span class="sxs-lookup"><span data-stu-id="1bf46-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-126">查閱文件</span><span class="sxs-lookup"><span data-stu-id="1bf46-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="1bf46-127">文件計數</span><span class="sxs-lookup"><span data-stu-id="1bf46-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="1bf46-128">建議</span><span class="sxs-lookup"><span data-stu-id="1bf46-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="1bf46-129">索引操作</span><span class="sxs-lookup"><span data-stu-id="1bf46-129">Index Operations</span></span>
<span data-ttu-id="1bf46-130">您可以針對指定的索引資源，透過簡單的 HTTP 要求 (POST、GET、PUT、DELETE)，在 Azure 搜尋服務中建立與管理索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="1bf46-131">toocreate 索引，請先 POST 描述 hello 索引結構描述的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="1bf46-132">hello 結構描述定義 hello 欄位 hello 索引、 其資料類型，以及如何使用它們 （例如，在全文檢索搜尋、 篩選、 排序或面相化）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="1bf46-133">它也會定義評分設定檔，建議工具和其他屬性 tooconfigure hello 索引的行為 hello。</span><span class="sxs-lookup"><span data-stu-id="1bf46-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="1bf46-134">hello 下列範例說明用於搜尋飯店資訊與 hello 描述欄位中使用兩種語言所定義的結構描述。</span><span class="sxs-lookup"><span data-stu-id="1bf46-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="1bf46-135">請注意屬性如何控制 hello 欄位的使用方式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="1bf46-136">例如 hello`hotelId`當做 hello 文件索引鍵 (`"key": true`)，會從全文檢索搜尋中排除 (`"searchable": false`)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="1bf46-137">建立 hello 索引之後，您將上傳會擴展 hello 索引的文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="1bf46-138">請參閱 [新增或更新文件](#AddOrUpdateDocuments) ，以取得這個後續步驟。</span><span class="sxs-lookup"><span data-stu-id="1bf46-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="1bf46-139">在 Azure 搜尋的影片介紹 tooindexing，請參閱 hello[頻道 9 雲端涵蓋的時段，對 Azure 搜尋](http://go.microsoft.com/fwlink/p/?LinkId=511509)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="1bf46-140">建立索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-140">Create Index</span></span>
<span data-ttu-id="1bf46-141">索引是 hello 組織和搜尋 Azure 搜尋中的文件的主要方式，類似 toohow 資料表中組織記錄資料庫。</span><span class="sxs-lookup"><span data-stu-id="1bf46-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="1bf46-142">每個索引有全部符合 toohello 索引結構描述 （欄位名稱、 資料類型和屬性），但是索引也會指定定義其他搜尋行為的其他建構 （建議工具、 計分設定檔和 CORS 選項） 的文件的集合。</span><span class="sxs-lookup"><span data-stu-id="1bf46-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="1bf46-143">您可以使用簡單的 HTTP POST 或 PUT 要求，在 Azure 搜尋服務中建立新的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="1bf46-144">hello hello 要求主體是指定 hello 索引和組態資訊的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="1bf46-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="1bf46-145">或者，您可以使用 PUT，並在 hello URI 上指定 hello 索引名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="1bf46-146">如果 hello 索引不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="1bf46-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="1bf46-147">建立索引決定 hello hello 文件結構的儲存，而且在搜尋操作中使用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="1bf46-148">填入 hello 索引是以個別的作業。</span><span class="sxs-lookup"><span data-stu-id="1bf46-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="1bf46-149">針對此步驟，您可以使用[索引子](https://msdn.microsoft.com/library/azure/mt183328.aspx) (適用於支援的資料類型) 或是[新增、更新或刪除文件](https://msdn.microsoft.com/library/azure/dn798930.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="1bf46-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="1bf46-150">發佈 hello 文件時，會產生 hello 反向索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="1bf46-151">**請注意**: hello 允許索引的數目上限依定價層而異。</span><span class="sxs-lookup"><span data-stu-id="1bf46-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="1bf46-152">hello 免費服務允許向上 too3 索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="1bf46-153">標準服務允許每個服務有 50 個索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="1bf46-154">如需詳細資訊，請參閱 [限制條件](http://msdn.microsoft.com/library/azure/dn798934.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="1bf46-155">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-155">**Request**</span></span>

<span data-ttu-id="1bf46-156">所有服務要求都需使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="1bf46-157">hello **Create Index**要求可以使用 POST 或 PUT 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="1bf46-158">使用 POST 時，您必須提供 hello 索引結構描述定義以及 hello 要求主體中的索引名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="1bf46-159">使用 PUT，hello 索引名稱會是 hello URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="1bf46-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="1bf46-160">如果 hello 索引不存在，它會建立它。</span><span class="sxs-lookup"><span data-stu-id="1bf46-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="1bf46-161">如果已經存在，則更新的 toohello 新定義。</span><span class="sxs-lookup"><span data-stu-id="1bf46-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="1bf46-162">hello 索引名稱必須是小寫、 以字母或數字開頭、 不含斜線或點，和不超過 128 個字元。</span><span class="sxs-lookup"><span data-stu-id="1bf46-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="1bf46-163">Hello 索引名稱開頭是字母或數字後, hello 其餘部分 hello 名稱可以包含任何字母、 數字和連字號，只要 hello 連字號不連續。</span><span class="sxs-lookup"><span data-stu-id="1bf46-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="1bf46-164">hello`api-version`需要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-164">hello `api-version` is required.</span></span> <span data-ttu-id="1bf46-165">如需可用版本清單，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="1bf46-166">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-166">**Request Headers**</span></span>

<span data-ttu-id="1bf46-167">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-168">`Content-Type`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-168">`Content-Type`: Required.</span></span> <span data-ttu-id="1bf46-169">設定得`application/json`</span><span class="sxs-lookup"><span data-stu-id="1bf46-169">Set this too`application/json`</span></span>
* <span data-ttu-id="1bf46-170">`api-key`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-170">`api-key`: Required.</span></span> <span data-ttu-id="1bf46-171">hello`api-key`是用來</span><span class="sxs-lookup"><span data-stu-id="1bf46-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="1bf46-172">驗證 hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-173">它是字串值、 唯一 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="1bf46-174">hello **Create Index**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-175">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-176">您可以取得這兩個 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-177">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-178"><a name="RequestData"></a>
**要求本文語法**</span><span class="sxs-lookup"><span data-stu-id="1bf46-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="1bf46-179">hello hello 要求主體包含結構描述定義，其中包括 hello 清單會送入此索引的文件中的資料欄位、 資料型別、 屬性，以及選擇性的計分設定檔清單會比對文件在使用的 tooscore查詢時間。</span><span class="sxs-lookup"><span data-stu-id="1bf46-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="1bf46-180">請注意，針對 POST 要求，您必須指定 hello 索引名稱 hello 要求主體中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="1bf46-181">Hello 索引中只能有一個索引鍵欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="1bf46-182">它有 toobe 字串欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-182">It has toobe a string field.</span></span> <span data-ttu-id="1bf46-183">此欄位會顯示 hello hello 索引內所儲存的每個文件的唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="1bf46-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="1bf46-184">hello 主要部份索引 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="1bf46-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="1bf46-185">`fields` 將提供給此索引，包括名稱、資料類型及屬性，以用來定義該欄位上允許的動作。</span><span class="sxs-lookup"><span data-stu-id="1bf46-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="1bf46-186">`suggesters` 可用於自動完成或自動提示查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="1bf46-187">`scoringProfiles` 可用於自訂搜尋分數評等。</span><span class="sxs-lookup"><span data-stu-id="1bf46-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="1bf46-188">如需詳細資訊，請參閱 [新增評分記錄檔](https://msdn.microsoft.com/library/azure/dn798928.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="1bf46-189">`analyzers``charFilters`， `tokenizers`，`tokenFilters`用的 toodefine 文件/查詢如何分解為可編索引/可搜尋的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="1bf46-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="1bf46-190">如需詳細資料，請參閱 [Azure 搜尋服務中的分析](https://aka.ms//azsanalysis) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="1bf46-191">`defaultScoringProfile`使用 toooverwrite hello 預設計分行為。</span><span class="sxs-lookup"><span data-stu-id="1bf46-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="1bf46-192">`corsOptions`tooallow 您對索引執行跨原始查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="1bf46-193">hello 建構 hello 要求裝載的語法如下所示。</span><span class="sxs-lookup"><span data-stu-id="1bf46-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="1bf46-194">本主題稍後會提供範例要求。</span><span class="sxs-lookup"><span data-stu-id="1bf46-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="1bf46-195">**索引屬性**</span><span class="sxs-lookup"><span data-stu-id="1bf46-195">**Index Attributes**</span></span>

<span data-ttu-id="1bf46-196">hello 設定下列屬性可以建立索引時。</span><span class="sxs-lookup"><span data-stu-id="1bf46-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="1bf46-197">如需評分和評分設定檔的詳細資訊，請參閱 [新增評分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="1bf46-198">`name`-設定 hello hello 欄位的名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="1bf46-199">`type`-設定 hello hello 欄位的資料類型。</span><span class="sxs-lookup"><span data-stu-id="1bf46-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="1bf46-200">`searchable`-將標示 hello 欄位為全文檢索搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="1bf46-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="1bf46-201">這表示它將在索引設定期間執行像是斷字的分析。</span><span class="sxs-lookup"><span data-stu-id="1bf46-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="1bf46-202">如果您設定`searchable`欄位 tooa 值，例如"sunny day"，在內部會分成 hello 個別的語彙基元"sunny"和 「 日 」。</span><span class="sxs-lookup"><span data-stu-id="1bf46-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="1bf46-203">這樣就能針對這些字詞進行全文檢索搜尋。</span><span class="sxs-lookup"><span data-stu-id="1bf46-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="1bf46-204">類型 `Edm.String` 或 `Collection(Edm.String)` 的欄位會預設為 `searchable`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="1bf46-205">其他類型的欄位不能是 `searchable`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="1bf46-206">**請注意**:`searchable`欄位會耗用額外的空間索引，因為 Azure 搜尋會儲存 hello 全文檢索搜尋的欄位值的其他語彙基元化的版本。</span><span class="sxs-lookup"><span data-stu-id="1bf46-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="1bf46-207">如果您希望 toosave 空間索引，您不需要包含在搜尋中欄位 toobe、 設定`searchable`太`false`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="1bf46-208">`filterable`-可讓參考中的 hello 欄位 toobe`$filter`查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="1bf46-209">`filterable` 處理字串的方式與 `searchable` 不同。</span><span class="sxs-lookup"><span data-stu-id="1bf46-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="1bf46-210">類型 `Edm.String` 或 `Collection(Edm.String)` 的欄位 (它們是 `filterable`) 不會執行斷字功能，因此，只會針對完全相符的項目進行比較。</span><span class="sxs-lookup"><span data-stu-id="1bf46-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="1bf46-211">例如，如果您將這類欄位`f`太"sunny day"，`$filter=f eq 'sunny'`會尋找相符的項目，但`$filter=f eq 'sunny day'`會。</span><span class="sxs-lookup"><span data-stu-id="1bf46-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="1bf46-212">所有欄位都會預設為 `filterable` 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="1bf46-213">`sortable`-Hello 系統根據預設依分數排序結果，但在許多經驗的使用者會想 toosort hello 文件中的欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="1bf46-214">類型 `Collection(Edm.String)` 的欄位不能是 `sortable`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="1bf46-215">所有的其他欄位都會預設為 `sortable` 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="1bf46-216">`facetable`- 通常用於搜尋結果的呈現方式，其中包括依類別排序的點閱數 (例如，搜尋數位相機，然後依照品牌、百萬像素、價格等項目來查看點閱數)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="1bf46-217">此選項無法與類型 `Edm.GeographyPoint`的欄位搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="1bf46-218">所有的其他欄位都會預設為 `facetable` 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="1bf46-219">**注意**：類型 `Edm.String` 的欄位 (它們是 `filterable`、`sortable` 或 `facetable`) 長度上限為 32 KB。</span><span class="sxs-lookup"><span data-stu-id="1bf46-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="1bf46-220">這是因為這類欄位會被視為單一搜尋詞彙，並在 Azure 搜尋詞彙的 hello 最大長度為 32 KB。</span><span class="sxs-lookup"><span data-stu-id="1bf46-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="1bf46-221">如果您需要 toostore 文字超過這個單一字串欄位中，您將需要 tooexplicitly 設定`filterable`， `sortable`，和`facetable`太`false`索引定義中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="1bf46-222">**請注意**： 如果欄位有無 hello 上述屬性設定太`true`(`searchable`， `filterable`， `sortable`，或`facetable`) hello 欄位有效地排除 hello 反向索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="1bf46-223">針對查詢中未使用，但需要在搜尋結果中使用的欄位來說，此選項非常實用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="1bf46-224">這類欄位排除 hello 索引可改善效能。</span><span class="sxs-lookup"><span data-stu-id="1bf46-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="1bf46-225">`key`-標記 hello 欄位為包含 hello 索引內的文件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1bf46-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="1bf46-226">只有一個欄位必須被選為 hello`key`欄位，它必須是型別`Edm.String`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="1bf46-227">索引鍵欄位可以是直接透過 hello 的文件使用的 toolook[查閱 API](#LookupAPI)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="1bf46-228">`retrievable`-設定是否可以在搜尋結果中傳回 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="1bf46-229">當您想 toouse 欄位 （例如，邊界） 要做為篩選、 排序或計分機制，但不是想 hello 欄位 toobe 可見 toohello 終端使用者，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="1bf46-230">針對 `true` for `key` 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="1bf46-231">`analyzer`-設定在搜尋時間及建立索引時 hello hello 分析器 toouse hello 欄位的名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="1bf46-232">Hello 允許一組值，請參閱[分析器](https://msdn.microsoft.com/library/mt605304.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="1bf46-233">此選項只可以搭配 `searchable` 欄位使用，而無法與 `searchAnalyzer` 或 `indexAnalyzer` 一起設定。</span><span class="sxs-lookup"><span data-stu-id="1bf46-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="1bf46-234">Hello 分析器選擇之後，就無法變更 hello 欄位中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="1bf46-235">`searchAnalyzer`-設定 hello hello 分析器次 hello 欄位搜尋使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="1bf46-236">Hello 允許一組值，請參閱[分析器](https://msdn.microsoft.com/library/mt605304.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="1bf46-237">此選項只能與 `searchable` 欄位搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="1bf46-238">它必須設定搭配`indexAnalyzer`而且不能設定以及 hello`analyzer`選項。</span><span class="sxs-lookup"><span data-stu-id="1bf46-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="1bf46-239">此分析器可在現有欄位上更新。</span><span class="sxs-lookup"><span data-stu-id="1bf46-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="1bf46-240">`indexAnalyzer`-設定 hello hello 分析器 hello 欄位建立索引時使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="1bf46-241">Hello 允許一組值，請參閱[分析器](https://msdn.microsoft.com/library/mt605304.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="1bf46-242">此選項只能與 `searchable` 欄位搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="1bf46-243">它必須設定搭配`searchAnalyzer`而且不能設定以及 hello`analyzer`選項。</span><span class="sxs-lookup"><span data-stu-id="1bf46-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="1bf46-244">Hello 分析器選擇之後，就無法變更 hello 欄位中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="1bf46-245">`suggesters`-設定 hello 搜尋模式和 hello 內容來源的 hello 建議的欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="1bf46-246">如需詳細資訊，請參閱 [建議工具](#Suggesters) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="1bf46-247">`scoringProfiles` - 定義自訂評分行為，讓您能夠影響搜尋結果中哪些項目的出現機率會比較高。</span><span class="sxs-lookup"><span data-stu-id="1bf46-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="1bf46-248">評分設定檔是由欄位權數和函式所組成。</span><span class="sxs-lookup"><span data-stu-id="1bf46-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="1bf46-249">請參閱[新增計分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx)如需有關使用計分設定檔中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="1bf46-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="1bf46-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**語言支援**</span><span class="sxs-lookup"><span data-stu-id="1bf46-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="1bf46-251">可搜尋的欄位最常執行的分析是斷字、文字正規化，以及篩選出字詞。</span><span class="sxs-lookup"><span data-stu-id="1bf46-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="1bf46-252">根據預設，在 Azure 搜尋可搜尋的欄位都會經過分析，以 hello [Apache Lucene 標準分析器](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html)文字分解為下列項目["Unicode 文字分割"](http://unicode.org/reports/tr29/)規則。</span><span class="sxs-lookup"><span data-stu-id="1bf46-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="1bf46-253">此外，hello 標準分析器會將所有字元 tootheir 小寫的形式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="1bf46-254">索引的文件和搜尋詞彙會編製索引和查詢處理期間經歷 hello 分析。</span><span class="sxs-lookup"><span data-stu-id="1bf46-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="1bf46-255">Azure 搜尋支援多種語言。</span><span class="sxs-lookup"><span data-stu-id="1bf46-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="1bf46-256">每一種語言都需要非標準的文字分析器，以負責指定語言的特性。</span><span class="sxs-lookup"><span data-stu-id="1bf46-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="1bf46-257">Azure 搜尋服務提供兩種類型的分析器：</span><span class="sxs-lookup"><span data-stu-id="1bf46-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="1bf46-258">由 Lucene 所支援的 35 種分析器。</span><span class="sxs-lookup"><span data-stu-id="1bf46-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="1bf46-259">由專屬的 Microsoft 自然語言處理技術所支援的 50 種分析器，此技術同樣用於 Office 和 Bing 中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="1bf46-260">有些開發人員可能會偏好 hello Lucene 的更熟悉、 簡單、 開放原始碼方案。</span><span class="sxs-lookup"><span data-stu-id="1bf46-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="1bf46-261">Lucene 分析器位於更快、 但 hello Microsoft 分析器具有進階的功能，例如詞形、 word decompounding （在語言，例如德文、 丹麥文、 荷蘭文、 瑞典文、 挪威文、 愛沙尼亞文、 完成、 匈牙利文、 斯洛伐克文） 和實體辨識 (Url電子郵件、 日期、 數字)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="1bf46-262">可能的話，您應該執行這兩個 hello Microsoft 和 Lucene 分析器 toodecide 哪一個是更適合的比較。</span><span class="sxs-lookup"><span data-stu-id="1bf46-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="1bf46-263">***比較它們的方法***</span><span class="sxs-lookup"><span data-stu-id="1bf46-263">***How they compare***</span></span>

<span data-ttu-id="1bf46-264">英文版的 hello Lucene 分析器會擴充 hello 標準分析器。</span><span class="sxs-lookup"><span data-stu-id="1bf46-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="1bf46-265">它會從字組中移除所有格 (結尾的 's)、為每個 [Porter 詞幹演算法](http://tartarus.org/~martin/PorterStemmer/)套用詞幹，然後移除英文[停用字詞](http://en.wikipedia.org/wiki/Stop_words)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="1bf46-266">相較之下，hello Microsoft 分析器執行詞形而不是詞幹分析。</span><span class="sxs-lookup"><span data-stu-id="1bf46-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="1bf46-267">這表示它可以把變形和不規則的字詞形式處理得更好，以得到相關性更強的搜尋結果 (如需詳細資訊，請參閱 [Azure 搜尋 MVA 簡報](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) 的模組 7)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="1bf46-268">索引包含 Microsoft 分析器平均是兩個 toothree 時間低於 Lucene 的對應項，視 hello 語言而定。</span><span class="sxs-lookup"><span data-stu-id="1bf46-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="1bf46-269">平均大小的查詢應不至大幅影響搜尋效能。</span><span class="sxs-lookup"><span data-stu-id="1bf46-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="1bf46-270">***組態***</span><span class="sxs-lookup"><span data-stu-id="1bf46-270">***Configuration***</span></span>

<span data-ttu-id="1bf46-271">Hello 索引定義中的每個欄位，您可以設定 hello`analyzer`屬性，指定的語言和廠商 tooan 分析器名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="1bf46-272">索引與搜尋該欄位時，就會套用相同的分析器 hello。</span><span class="sxs-lookup"><span data-stu-id="1bf46-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="1bf46-273">例如，您可以個別欄位的英文、 法文和西班牙文旅館說明在 hello 中並排存在於相同的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="1bf46-274">使用 hello ['searchFields' 查詢參數](#SearchQueryParameters)toospecify 針對哪些語言特有的欄位 toosearch 在查詢中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="1bf46-275">您可以檢閱查詢範例，包括 hello`analyzer`屬性[搜尋文件](#SearchDocs)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="1bf46-276">***分析器清單***</span><span class="sxs-lookup"><span data-stu-id="1bf46-276">***Analyzer list***</span></span>

<span data-ttu-id="1bf46-277">以下是支援的語言與 Lucene 和 Microsoft 分析器名稱 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="1bf46-278">語言</span><span class="sxs-lookup"><span data-stu-id="1bf46-278">Language</span></span></th>
        <th><span data-ttu-id="1bf46-279">Microsoft 分析器名稱</span><span class="sxs-lookup"><span data-stu-id="1bf46-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="1bf46-280">Lucene 分析器名稱</span><span class="sxs-lookup"><span data-stu-id="1bf46-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-281">阿拉伯文</span><span class="sxs-lookup"><span data-stu-id="1bf46-281">Arabic</span></span></td>
        <td><span data-ttu-id="1bf46-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-284">亞美尼亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="1bf46-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="1bf46-286">孟加拉文</span><span class="sxs-lookup"><span data-stu-id="1bf46-286">Bangla</span></span></td>
        <td><span data-ttu-id="1bf46-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="1bf46-288">巴斯克文</span><span class="sxs-lookup"><span data-stu-id="1bf46-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="1bf46-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="1bf46-290">保加利亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="1bf46-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="1bf46-293">卡達隆尼亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-293">Catalan</span></span></td>
        <td><span data-ttu-id="1bf46-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="1bf46-296">簡體中文</span><span class="sxs-lookup"><span data-stu-id="1bf46-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="1bf46-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-299">繁體中文</span><span class="sxs-lookup"><span data-stu-id="1bf46-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="1bf46-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="1bf46-302">克羅埃西亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-302">Croatian</span></span></td>
        <td><span data-ttu-id="1bf46-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-304">捷克文</span><span class="sxs-lookup"><span data-stu-id="1bf46-304">Czech</span></span></td>
        <td><span data-ttu-id="1bf46-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="1bf46-307">丹麥文</span><span class="sxs-lookup"><span data-stu-id="1bf46-307">Danish</span></span></td>
        <td><span data-ttu-id="1bf46-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="1bf46-310">荷蘭文</span><span class="sxs-lookup"><span data-stu-id="1bf46-310">Dutch</span></span></td>
        <td><span data-ttu-id="1bf46-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="1bf46-313">English</span><span class="sxs-lookup"><span data-stu-id="1bf46-313">English</span></span></td>        
        <td><span data-ttu-id="1bf46-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-316">愛沙尼亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-316">Estonian</span></span></td>
        <td><span data-ttu-id="1bf46-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-318">芬蘭文</span><span class="sxs-lookup"><span data-stu-id="1bf46-318">Finnish</span></span></td>
        <td><span data-ttu-id="1bf46-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="1bf46-321">法文</span><span class="sxs-lookup"><span data-stu-id="1bf46-321">French</span></span></td>
        <td><span data-ttu-id="1bf46-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-324">加里斯亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="1bf46-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="1bf46-326">德文</span><span class="sxs-lookup"><span data-stu-id="1bf46-326">German</span></span></td>
        <td><span data-ttu-id="1bf46-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-329">希臘文</span><span class="sxs-lookup"><span data-stu-id="1bf46-329">Greek</span></span></td>
        <td><span data-ttu-id="1bf46-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-332">古吉拉特文</span><span class="sxs-lookup"><span data-stu-id="1bf46-332">Gujarati</span></span></td>
        <td><span data-ttu-id="1bf46-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-334">希伯來文</span><span class="sxs-lookup"><span data-stu-id="1bf46-334">Hebrew</span></span></td>
        <td><span data-ttu-id="1bf46-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-336">北印度文</span><span class="sxs-lookup"><span data-stu-id="1bf46-336">Hindi</span></span></td>
        <td><span data-ttu-id="1bf46-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-339">匈牙利文</span><span class="sxs-lookup"><span data-stu-id="1bf46-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="1bf46-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-342">冰島文</span><span class="sxs-lookup"><span data-stu-id="1bf46-342">Icelandic</span></span></td>
        <td><span data-ttu-id="1bf46-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-344">印尼文 (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="1bf46-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="1bf46-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-347">愛爾蘭文</span><span class="sxs-lookup"><span data-stu-id="1bf46-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="1bf46-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-349">義大利文</span><span class="sxs-lookup"><span data-stu-id="1bf46-349">Italian</span></span></td>
        <td><span data-ttu-id="1bf46-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-352">日文</span><span class="sxs-lookup"><span data-stu-id="1bf46-352">Japanese</span></span></td>
        <td><span data-ttu-id="1bf46-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-355">坎那達文</span><span class="sxs-lookup"><span data-stu-id="1bf46-355">Kannada</span></span></td>
        <td><span data-ttu-id="1bf46-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-357">韓文</span><span class="sxs-lookup"><span data-stu-id="1bf46-357">Korean</span></span></td>
        <td><span data-ttu-id="1bf46-358">ko.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-360">拉脫維亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-360">Latvian</span></span></td>        
        <td><span data-ttu-id="1bf46-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-363">立陶宛文</span><span class="sxs-lookup"><span data-stu-id="1bf46-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="1bf46-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-365">馬來亞拉姆文</span><span class="sxs-lookup"><span data-stu-id="1bf46-365">Malayalam</span></span></td>
        <td><span data-ttu-id="1bf46-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-367">馬來文 (拉丁)</span><span class="sxs-lookup"><span data-stu-id="1bf46-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="1bf46-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-369">馬拉提文</span><span class="sxs-lookup"><span data-stu-id="1bf46-369">Marathi</span></span></td>
        <td><span data-ttu-id="1bf46-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-371">挪威文</span><span class="sxs-lookup"><span data-stu-id="1bf46-371">Norwegian</span></span></td>
        <td><span data-ttu-id="1bf46-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="1bf46-374">波斯文</span><span class="sxs-lookup"><span data-stu-id="1bf46-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="1bf46-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="1bf46-376">波蘭文</span><span class="sxs-lookup"><span data-stu-id="1bf46-376">Polish</span></span></td>
        <td><span data-ttu-id="1bf46-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-379">葡萄牙文 (巴西)</span><span class="sxs-lookup"><span data-stu-id="1bf46-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="1bf46-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-382">葡萄牙文 (葡萄牙)</span><span class="sxs-lookup"><span data-stu-id="1bf46-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="1bf46-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="1bf46-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-385">旁遮普文</span><span class="sxs-lookup"><span data-stu-id="1bf46-385">Punjabi</span></span></td>
        <td><span data-ttu-id="1bf46-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-387">羅馬尼亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-387">Romanian</span></span></td>
        <td><span data-ttu-id="1bf46-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-390">俄文</span><span class="sxs-lookup"><span data-stu-id="1bf46-390">Russian</span></span></td>
        <td><span data-ttu-id="1bf46-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-393">塞爾維亞文 (斯拉夫)</span><span class="sxs-lookup"><span data-stu-id="1bf46-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="1bf46-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-395">塞爾維亞文 (拉丁)</span><span class="sxs-lookup"><span data-stu-id="1bf46-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="1bf46-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-397">斯洛伐克文</span><span class="sxs-lookup"><span data-stu-id="1bf46-397">Slovak</span></span></td>
        <td><span data-ttu-id="1bf46-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-399">斯洛維尼亞文</span><span class="sxs-lookup"><span data-stu-id="1bf46-399">Slovenian</span></span></td>
        <td><span data-ttu-id="1bf46-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-401">西班牙文</span><span class="sxs-lookup"><span data-stu-id="1bf46-401">Spanish</span></span></td>
        <td><span data-ttu-id="1bf46-402">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-404">瑞典文</span><span class="sxs-lookup"><span data-stu-id="1bf46-404">Swedish</span></span></td>
        <td><span data-ttu-id="1bf46-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="1bf46-407">坦米爾文</span><span class="sxs-lookup"><span data-stu-id="1bf46-407">Tamil</span></span></td>
        <td><span data-ttu-id="1bf46-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-409">特拉古文</span><span class="sxs-lookup"><span data-stu-id="1bf46-409">Telugu</span></span></td>
        <td><span data-ttu-id="1bf46-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-411">泰文</span><span class="sxs-lookup"><span data-stu-id="1bf46-411">Thai</span></span></td>
        <td><span data-ttu-id="1bf46-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-414">土耳其文</span><span class="sxs-lookup"><span data-stu-id="1bf46-414">Turkish</span></span></td>
        <td><span data-ttu-id="1bf46-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="1bf46-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-417">烏克蘭文</span><span class="sxs-lookup"><span data-stu-id="1bf46-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="1bf46-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-419">烏都文</span><span class="sxs-lookup"><span data-stu-id="1bf46-419">Urdu</span></span></td>
        <td><span data-ttu-id="1bf46-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-421">越南文</span><span class="sxs-lookup"><span data-stu-id="1bf46-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="1bf46-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="1bf46-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="1bf46-423">此外，Azure 搜尋服務還提供無從驗證語言的分析器設定</span><span class="sxs-lookup"><span data-stu-id="1bf46-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="1bf46-424">標準 ASCII 摺疊</span><span class="sxs-lookup"><span data-stu-id="1bf46-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="1bf46-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="1bf46-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="1bf46-426">Unicode 文字分割 (標準的 Tokenizer)</span><span class="sxs-lookup"><span data-stu-id="1bf46-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="1bf46-427">ASCII 摺疊篩選器的轉換不屬於第一個 127 ASCII 字元 toohello 組與其 ASCII 相等項到 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="1bf46-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="1bf46-428">這在移除讀音符號時非常有用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="1bf46-429">所有名稱加上 <i>lucene</i> 註解的分析器都是由 [Apache Lucene 的語言分析器](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html)所提供。</span><span class="sxs-lookup"><span data-stu-id="1bf46-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="1bf46-430">可以找到 hello ASCII 摺疊篩選器的詳細資訊[這裡](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="1bf46-431">**建議工具**</span><span class="sxs-lookup"><span data-stu-id="1bf46-431">**Suggesters**</span></span>

<span data-ttu-id="1bf46-432">A`suggester`定義索引中的哪些欄位會使用的 toosupport 搜尋中的自動完成。</span><span class="sxs-lookup"><span data-stu-id="1bf46-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="1bf46-433">部分搜尋字串通常傳送 toohello[建議 API](#Suggestions) hello 使用者輸入搜尋查詢，而 hello API 會傳回一組建議的片語。</span><span class="sxs-lookup"><span data-stu-id="1bf46-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="1bf46-434">建議您在 hello 索引中定義的工具會決定哪些欄位是使用的 toobuild hello 預先輸入的搜尋詞彙。</span><span class="sxs-lookup"><span data-stu-id="1bf46-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="1bf46-435">如需組態詳細資料，請參閱[建議工具](#Suggesters)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="1bf46-436">**評分設定檔**</span><span class="sxs-lookup"><span data-stu-id="1bf46-436">**Scoring profiles**</span></span>

<span data-ttu-id="1bf46-437">A`scoringProfile`定義自訂計分行為，可讓您影響較高 hello 搜尋結果中出現的項目。</span><span class="sxs-lookup"><span data-stu-id="1bf46-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="1bf46-438">評分設定檔是由欄位權數和函式所組成。</span><span class="sxs-lookup"><span data-stu-id="1bf46-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="1bf46-439">toouse 它們，您指定設定檔在 hello 查詢字串的名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="1bf46-440">預設的計分設定檔運作背後 hello 場景 toocompute 結果集中的每個項目的搜尋分數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="1bf46-441">您可以使用 hello 內部且未命名評分設定檔。</span><span class="sxs-lookup"><span data-stu-id="1bf46-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="1bf46-442">或者，設定`defaultScoringProfile`toouse 為 hello 預設值，每當 hello 查詢字串中未指定自訂設定檔時叫用自訂設定檔。</span><span class="sxs-lookup"><span data-stu-id="1bf46-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="1bf46-443">請參閱[新增評分設定檔 tooa 搜尋索引 (Azure 搜尋服務 REST API)](search-api-scoring-profiles-2015-02-28-preview.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1bf46-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="1bf46-444">**CORS 選項**</span><span class="sxs-lookup"><span data-stu-id="1bf46-444">**CORS Options**</span></span>

<span data-ttu-id="1bf46-445">用戶端 Javascript 無法呼叫任何應用程式開發介面，根據預設，因為 hello 瀏覽器會防止所有跨原始要求。</span><span class="sxs-lookup"><span data-stu-id="1bf46-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="1bf46-446">啟用 CORS （跨原始資源共用） 設定 hello`corsOptions`屬性 tooallow 跨原始查詢 tooyour 索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="1bf46-447">請注意，基於安全緣故，只有查詢 API 支援 CORS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="1bf46-448">適用於 CORS，您可以設定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="1bf46-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="1bf46-449">`allowedOrigins`（必要）： 這是會被授與存取 tooyour 索引的原始來源清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="1bf46-450">這表示任何從該來源提供的 Javascript 程式碼會被允許 tooquery 您的索引 （假設其提供 hello 正確的 API 金鑰）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="1bf46-451">每個來源一般而言都會 hello 表單`protocol://fully-qualified-domain-name:port`雖然 hello 連接埠常會被省略。</span><span class="sxs-lookup"><span data-stu-id="1bf46-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="1bf46-452">如需詳細資訊，請參閱 [這篇文章](http://go.microsoft.com/fwlink/?LinkId=330822) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="1bf46-453">如果您想要 tooallow 存取 tooall 原始來源，包含`*`做為單一項目在 hello`allowedOrigins`陣列。</span><span class="sxs-lookup"><span data-stu-id="1bf46-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="1bf46-454">請注意， **不建議針對生產搜尋服務使用這個做法。**</span><span class="sxs-lookup"><span data-stu-id="1bf46-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="1bf46-455">但是，如果是基於開發或偵錯目的，它就非常實用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="1bf46-456">`maxAgeInSeconds`（選擇性）： 瀏覽器使用這個值 toodetermine hello 持續時間 （以秒為單位） toocache CORS 預檢回應。</span><span class="sxs-lookup"><span data-stu-id="1bf46-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="1bf46-457">這必須是非負數的整數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-457">This must be a non-negative integer.</span></span> <span data-ttu-id="1bf46-458">hello 較大的這個值就會越 hello 更佳的效能，但 CORS 原則變更 tootake 效果花費的 hello 較長。</span><span class="sxs-lookup"><span data-stu-id="1bf46-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="1bf46-459">若未設定，即會使用預設持續期間 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="1bf46-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="1bf46-460"><a name="CreateUpdateIndexExample"></a>
**要求本文範例**</span><span class="sxs-lookup"><span data-stu-id="1bf46-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="1bf46-461">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-461">**Response**</span></span>

<span data-ttu-id="1bf46-462">要求成功：「201 已建立」。</span><span class="sxs-lookup"><span data-stu-id="1bf46-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="1bf46-463">根據預設 hello 回應主體會包含 hello JSON hello 索引定義所建立。</span><span class="sxs-lookup"><span data-stu-id="1bf46-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="1bf46-464">如果 hello`Prefer`要求標頭設定得`return=minimal`hello 回應主體會是空白，hello 成功狀態碼將會是 「 204 沒有內容 」 而不是 「 201 已建立 」。</span><span class="sxs-lookup"><span data-stu-id="1bf46-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="1bf46-465">這是無論 PUT 或 POST 是使用的 toocreate hello 索引，則為 true。</span><span class="sxs-lookup"><span data-stu-id="1bf46-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="1bf46-466">**備註**</span><span class="sxs-lookup"><span data-stu-id="1bf46-466">**Remarks**</span></span>

<span data-ttu-id="1bf46-467">目前針對索引結構描述更新提供有限支援。</span><span class="sxs-lookup"><span data-stu-id="1bf46-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="1bf46-468">目前不支援任何需要重新編製索引的結構描述更新 (例如，變更欄位類型)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="1bf46-469">雖然無法變更現有欄位，或已刪除，則新欄位可以隨時加入 tooan 現有的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="1bf46-470">當加入新的欄位時，hello 索引中的所有現有文件會自動提供該欄位的 null 值。</span><span class="sxs-lookup"><span data-stu-id="1bf46-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="1bf46-471">新文件加入 toohello 索引之前，將耗用額外的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="1bf46-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="1bf46-472">建議工具</span><span class="sxs-lookup"><span data-stu-id="1bf46-472">Suggesters</span></span>
<span data-ttu-id="1bf46-473">在 Azure 搜尋中的 hello 建議功能是提供一份潛在回應 toopartial 字串輸入的搜尋方塊中輸入搜尋詞彙的自動填寫或自動完成查詢功能。</span><span class="sxs-lookup"><span data-stu-id="1bf46-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="1bf46-474">當您使用商業 Web 搜尋引擎時，您可能已經注意到查詢建議：在 Bing 中輸入 ".NET" 會產生 ".NET 4.5"、".NET Framework 3.5" 等等的詞彙清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="1bf46-475">使用 hello 搜尋服務 REST API 時，自訂的 Azure 搜尋應用程式中實作建議需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1bf46-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="1bf46-476">藉由新增啟用建議**建議工具**叫用您在索引中，提供 hello 名稱、 搜尋模式和欄位清單的預先輸入的建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="1bf46-477">例如，如果您指定"cityName"做為來源欄位，輸入部分搜尋字串"Sea"將會導致 「 西雅圖 」、"Seaside"和"Seatac"（三個都是實際城市名稱） 提供做查詢建議 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="1bf46-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="1bf46-478">叫用呼叫 hello 建議[建議 API](#Suggestions)應用程式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="1bf46-479">通常部分搜尋字串 hello 使用者輸入搜尋查詢，而此 API 會傳回一組建議的片語傳送 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="1bf46-480">這篇文章說明如何 tooconfigure**建議工具**。</span><span class="sxs-lookup"><span data-stu-id="1bf46-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="1bf46-481">您也應該檢閱 hello[建議 API](#Suggestions)的建議工具的使用方式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1bf46-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="1bf46-482">**用法**</span><span class="sxs-lookup"><span data-stu-id="1bf46-482">**Usage**</span></span>

<span data-ttu-id="1bf46-483">`Suggesters`hello 索引中建立和使用時效果最佳 toosuggest 特定文件，而不是鬆散的詞彙或片語。</span><span class="sxs-lookup"><span data-stu-id="1bf46-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="1bf46-484">hello 最佳候選項目欄位是標題、 名稱和其他相對較短的片語，可以識別項目。</span><span class="sxs-lookup"><span data-stu-id="1bf46-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="1bf46-485">不太有效的是重複的欄位 (例如，類別和標記) 或非常長的欄位 (例如，說明或註解欄位)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="1bf46-486">Hello 索引定義的一部分，您可以加入單一建議工具 toohello`suggesters`集合。</span><span class="sxs-lookup"><span data-stu-id="1bf46-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="1bf46-487">這些屬性定義的建議工具 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="1bf46-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="1bf46-488">`name`: hello hello 建議工具名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="1bf46-489">呼叫 hello 時，使用 hello hello 建議工具名稱`suggest`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1bf46-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="1bf46-490">`searchMode`: hello 用策略 toosearch 候選片語。</span><span class="sxs-lookup"><span data-stu-id="1bf46-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="1bf46-491">hello 只有目前支援的模式是`analyzingInfixMatching`，它會執行彈性比對片語 hello 開頭或 hello 中間的句子。</span><span class="sxs-lookup"><span data-stu-id="1bf46-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="1bf46-492">`sourceFields`： 一或多個欄位清單的 hello 內容來源的 hello 的建議。</span><span class="sxs-lookup"><span data-stu-id="1bf46-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="1bf46-493">只有類型 `Edm.String` 和 `Collection(Edm.String)` 的欄位可以用來做為提供建議的來源。</span><span class="sxs-lookup"><span data-stu-id="1bf46-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="1bf46-494">您只能使用未設定自訂語言分析器的欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="1bf46-495">**建議工具範例**</span><span class="sxs-lookup"><span data-stu-id="1bf46-495">**Suggester Example**</span></span>

<span data-ttu-id="1bf46-496">建議工具是 hello 索引的一部分。</span><span class="sxs-lookup"><span data-stu-id="1bf46-496">A suggester is part of hello index.</span></span> <span data-ttu-id="1bf46-497">只能有一個建議工具可以存在於 hello `suggesters` hello 目前版本，與 hello 並列中的集合的欄位集合和`scoringProfiles`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="1bf46-498">如果您使用 hello Azure 搜尋公用預覽版本`suggesters`取代較舊的布林值屬性 (`"suggestions": false`)，僅支援簡短字串 （3-25 個字元） 前置詞建議。</span><span class="sxs-lookup"><span data-stu-id="1bf46-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="1bf46-499">一個取代， `suggesters`，支援中置比對的 hello 開頭或欄位內容的 hello 中間尋找相符詞彙具有較佳的搜尋字串中的錯誤容錯性。</span><span class="sxs-lookup"><span data-stu-id="1bf46-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="1bf46-500">從 hello 上市版本開始，這是現在 hello 唯一 hello 建議應用程式開發介面的實作。</span><span class="sxs-lookup"><span data-stu-id="1bf46-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="1bf46-501">較舊的 hello`suggestions`屬性中導入`api-version=2014-07-31-Preview`toowork 繼續在該版本中，但不是在 hello 操作`2015-02-28`或更新版本的 Azure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="1bf46-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="1bf46-502">更新索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-502">Update Index</span></span>
<span data-ttu-id="1bf46-503">您可以在 Azure 搜尋服務中，使用 HTTP PUT 要求來更新現有的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="1bf46-504">更新可以加入新欄位 toohello 現有結構描述、 修改 CORS 選項，以及修改計分設定檔。</span><span class="sxs-lookup"><span data-stu-id="1bf46-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="1bf46-505">如需詳細資訊，請參閱 [新增評分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="1bf46-506">您可以指定 hello 索引 tooupdate hello 名稱 hello 要求 URI:</span><span class="sxs-lookup"><span data-stu-id="1bf46-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="1bf46-507">**重要事項：**索引結構描述更新的支援是有限的 toooperations 不需要重建 hello 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="1bf46-508">目前不支援任何需要重新編製索引的結構描述更新 (例如，變更欄位類型)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="1bf46-509">儘管無法變更或刪除現有欄位，但可隨時新增欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="1bf46-510">hello 一樣太`suggesters`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="1bf46-511">Tooa 建議工具在 hello 時間 hello 欄位會新增，但無法從移除欄位，可能會加入新欄位`suggesters`，無法加入現有的欄位太`suggesters`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="1bf46-512">當加入新欄位 tooan 索引，hello 索引中的所有現有文件會自動提供該欄位的 null 值。</span><span class="sxs-lookup"><span data-stu-id="1bf46-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="1bf46-513">新文件加入 toohello 索引之前，將耗用額外的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="1bf46-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="1bf46-514">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-514">**Request**</span></span>

<span data-ttu-id="1bf46-515">所有服務要求都需使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="1bf46-516">hello**更新索引**要求使用 HTTP PUT 建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="1bf46-517">使用 PUT，hello 索引名稱會是 hello URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="1bf46-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="1bf46-518">如果 hello 索引不存在，它會建立它。</span><span class="sxs-lookup"><span data-stu-id="1bf46-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="1bf46-519">如果 hello 索引已經存在，則更新的 toohello 新定義。</span><span class="sxs-lookup"><span data-stu-id="1bf46-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="1bf46-520">hello 索引名稱必須是小寫、 以字母或數字開頭、 不含斜線或點，和不超過 128 個字元。</span><span class="sxs-lookup"><span data-stu-id="1bf46-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="1bf46-521">Hello 索引名稱開頭是字母或數字後, hello 其餘部分 hello 名稱可以包含任何字母、 數字和連字號，只要 hello 連字號不連續。</span><span class="sxs-lookup"><span data-stu-id="1bf46-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="1bf46-522">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-523">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-524">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-525">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-525">**Request Headers**</span></span>

<span data-ttu-id="1bf46-526">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-527">`Content-Type`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-527">`Content-Type`: Required.</span></span> <span data-ttu-id="1bf46-528">設定得`application/json`</span><span class="sxs-lookup"><span data-stu-id="1bf46-528">Set this too`application/json`</span></span>
* <span data-ttu-id="1bf46-529">`api-key`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-529">`api-key`: Required.</span></span> <span data-ttu-id="1bf46-530">hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-531">它是字串值、 唯一 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="1bf46-532">hello**更新索引**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-533">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-534">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-535">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-536">**要求本文的語法**</span><span class="sxs-lookup"><span data-stu-id="1bf46-536">**Request Body Syntax**</span></span>

<span data-ttu-id="1bf46-537">在更新現有的索引，hello 主體必須包含原始結構描述定義 hello，加上您要新增，hello 新欄位，以及 hello 修改計分設定檔，建議工具和 CORS 選項，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="1bf46-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="1bf46-538">如果您未修改 hello 計分設定檔和 CORS 選項，您必須包含 hello hello 索引建立時的原始資料。</span><span class="sxs-lookup"><span data-stu-id="1bf46-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="1bf46-539">更新 hello 最佳模式 toouse 一般是使用 GET tooretrieve hello 索引定義，請修改它，然後使用 PUT 予以更新。</span><span class="sxs-lookup"><span data-stu-id="1bf46-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="1bf46-540">使用方便 hello 結構描述語法的 toocreate 索引在此處重現。</span><span class="sxs-lookup"><span data-stu-id="1bf46-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="1bf46-541">如需更多詳細資訊，請參閱 [建立索引](#CreateIndex) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="1bf46-542">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-542">**Response**</span></span>

<span data-ttu-id="1bf46-543">要求成功：「204 沒有內容」。</span><span class="sxs-lookup"><span data-stu-id="1bf46-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="1bf46-544">根據預設 hello 回應主體是空的。</span><span class="sxs-lookup"><span data-stu-id="1bf46-544">By default hello response body will be empty.</span></span> <span data-ttu-id="1bf46-545">不過，如果 hello`Prefer`要求標頭設定得`return=representation`，hello 回應主體會包含已更新的 hello 索引定義的 hello JSON。</span><span class="sxs-lookup"><span data-stu-id="1bf46-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="1bf46-546">Hello 成功狀態碼將會在此情況下，「 200 確定 」。</span><span class="sxs-lookup"><span data-stu-id="1bf46-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="1bf46-547">**使用自訂分析器來更新索引定義**</span><span class="sxs-lookup"><span data-stu-id="1bf46-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="1bf46-548">定義分析器、權杖化工具、語彙基元篩選或字元篩選之後，即無法進行修改。</span><span class="sxs-lookup"><span data-stu-id="1bf46-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="1bf46-549">新的可以 tooan 現有的索引，才加入 hello`allowIndexDowntime`旗標設定 tootrue hello 索引更新要求中：</span><span class="sxs-lookup"><span data-stu-id="1bf46-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="1bf46-550">請注意，這項作業將會放入您的離線索引至少幾秒，導致您的索引和查詢要求 toofail。</span><span class="sxs-lookup"><span data-stu-id="1bf46-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="1bf46-551">Hello 索引的效能和寫入可用性可以是障礙者數分鐘之後更新 hello 索引時，或較長時間非常大的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="1bf46-552">列出索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-552">List Indexes</span></span>
<span data-ttu-id="1bf46-553">hello**列出索引**作業會傳回一份 hello 索引目前在您的 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="1bf46-554">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-554">**Request**</span></span>

<span data-ttu-id="1bf46-555">所有服務要求都需使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="1bf46-556">hello**列出索引**要求可以使用 hello GET 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="1bf46-557">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-558">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-559">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-560">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-560">**Request Headers**</span></span>

<span data-ttu-id="1bf46-561">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-562">`api-key`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-562">`api-key`: Required.</span></span> <span data-ttu-id="1bf46-563">hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-564">它是字串值、 唯一 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="1bf46-565">hello**列出索引**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-566">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-567">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-568">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-569">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-569">**Request Body**</span></span>

<span data-ttu-id="1bf46-570">無。</span><span class="sxs-lookup"><span data-stu-id="1bf46-570">None.</span></span>

<span data-ttu-id="1bf46-571">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-571">**Response**</span></span>

<span data-ttu-id="1bf46-572">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="1bf46-573">下列為回應本文的範例：</span><span class="sxs-lookup"><span data-stu-id="1bf46-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="1bf46-574">請注意，您可以篩選您感興趣的 toojust hello 屬性下的 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="1bf46-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="1bf46-575">例如，如果您想要一份索引名稱，使用 hello OData`$select`查詢選項：</span><span class="sxs-lookup"><span data-stu-id="1bf46-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="1bf46-576">在此情況下，hello 回應 hello 上述範例中會出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1bf46-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="1bf46-577">如果您的搜尋服務中有大量索引，這是很有用的技巧 toosave 頻寬。</span><span class="sxs-lookup"><span data-stu-id="1bf46-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="1bf46-578">取得索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-578">Get Index</span></span>
<span data-ttu-id="1bf46-579">hello**取得索引**作業會從 Azure 搜尋取得 hello 索引定義。</span><span class="sxs-lookup"><span data-stu-id="1bf46-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="1bf46-580">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-580">**Request**</span></span>

<span data-ttu-id="1bf46-581">服務要求需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="1bf46-582">hello**取得索引**要求可以使用 hello GET 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="1bf46-583">hello [索引名稱] hello 要求 URI 中的指定從 hello 索引集合的索引 tooreturn。</span><span class="sxs-lookup"><span data-stu-id="1bf46-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="1bf46-584">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-585">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-586">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-587">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-587">**Request Headers**</span></span>

<span data-ttu-id="1bf46-588">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-589">`api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-590">它是字串值、 唯一 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="1bf46-591">hello**取得索引**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-592">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-593">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-594">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-595">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-595">**Request Body**</span></span>

<span data-ttu-id="1bf46-596">無。</span><span class="sxs-lookup"><span data-stu-id="1bf46-596">None.</span></span>

<span data-ttu-id="1bf46-597">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-597">**Response**</span></span>

<span data-ttu-id="1bf46-598">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="1bf46-599">請參閱 hello 範例 JSON 中[建立和更新索引](#CreateUpdateIndexExample)hello 回應裝載的範例。</span><span class="sxs-lookup"><span data-stu-id="1bf46-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="1bf46-600">删除索引</span><span class="sxs-lookup"><span data-stu-id="1bf46-600">Delete Index</span></span>
<span data-ttu-id="1bf46-601">hello**刪除索引**作業會從您的 Azure 搜尋服務移除索引和相關聯的文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="1bf46-602">您可以從 hello hello Azure 入口網站中的服務儀表板或 hello API 來取得 hello 索引名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="1bf46-603">如需詳細資訊，請參閱 [列出索引](#ListIndexes) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="1bf46-604">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-604">**Request**</span></span>

<span data-ttu-id="1bf46-605">服務要求需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="1bf46-606">hello**刪除索引**要求可以使用 hello DELETE 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="1bf46-607">hello [索引名稱] hello 要求 URI 中的指定從 hello 索引集合的索引 toodelete。</span><span class="sxs-lookup"><span data-stu-id="1bf46-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="1bf46-608">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-609">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-610">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-611">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-611">**Request Headers**</span></span>

<span data-ttu-id="1bf46-612">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-613">`api-key`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-613">`api-key`: Required.</span></span> <span data-ttu-id="1bf46-614">hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-615">它是字串值，唯一 tooyour 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="1bf46-616">hello**刪除索引**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-617">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-618">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-619">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-620">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-620">**Request Body**</span></span>

<span data-ttu-id="1bf46-621">無。</span><span class="sxs-lookup"><span data-stu-id="1bf46-621">None.</span></span>

<span data-ttu-id="1bf46-622">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-622">**Response**</span></span>

<span data-ttu-id="1bf46-623">狀態碼：回應成功時會傳回「204 沒有內容」。</span><span class="sxs-lookup"><span data-stu-id="1bf46-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="1bf46-624">取得索引統計資料</span><span class="sxs-lookup"><span data-stu-id="1bf46-624">Get Index Statistics</span></span>
<span data-ttu-id="1bf46-625">hello**取得索引統計資料**作業從 Azure 搜尋會傳回 hello 目前的索引，再加上的存放裝置使用量的文件計數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="1bf46-626">文件計數和儲存體大小的統計資料會每隔幾分鐘收集，不會即時收集。</span><span class="sxs-lookup"><span data-stu-id="1bf46-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="1bf46-627">因此，此 API 所傳回的 hello 統計資料可能無法反映新的索引作業所造成的變更中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="1bf46-628">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-628">**Request**</span></span>

<span data-ttu-id="1bf46-629">所有服務要求都需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="1bf46-630">hello**取得索引統計資料**要求可以使用 hello GET 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="1bf46-631">hello 要求 URI 中的 hello [索引名稱] 會告知 hello 服務 tooreturn 索引統計資料的 hello 指定的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="1bf46-632">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-633">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-634">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-635">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-635">**Request Headers**</span></span>

<span data-ttu-id="1bf46-636">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-637">`api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-638">它是字串值、 唯一 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="1bf46-639">hello**取得索引統計資料**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-640">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-641">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-642">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-643">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-643">**Request Body**</span></span>

<span data-ttu-id="1bf46-644">無。</span><span class="sxs-lookup"><span data-stu-id="1bf46-644">None.</span></span>

<span data-ttu-id="1bf46-645">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-645">**Response**</span></span>

<span data-ttu-id="1bf46-646">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="1bf46-647">hello 回應主體是在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="1bf46-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="1bf46-648">測試分析器</span><span class="sxs-lookup"><span data-stu-id="1bf46-648">Test Analyzer</span></span>
<span data-ttu-id="1bf46-649">hello**分析 API**分析器為語彙基元所分隔的文字會顯示。</span><span class="sxs-lookup"><span data-stu-id="1bf46-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="1bf46-650">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-650">**Request**</span></span>

<span data-ttu-id="1bf46-651">所有服務要求都需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="1bf46-652">hello**分析 API**要求可以使用 hello POST 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="1bf46-653">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-654">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-655">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-656">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-656">**Request Headers**</span></span>

<span data-ttu-id="1bf46-657">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-658">`api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-659">它是字串值、 唯一 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="1bf46-660">hello**分析 API**要求必須包含`api-key`組 tooan 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-661">您也必須 hello 索引名稱與 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-662">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-663">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-664">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="1bf46-665">或</span><span class="sxs-lookup"><span data-stu-id="1bf46-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="1bf46-666">hello `analyzer_name`， `tokenizer_name`，`token_filter_name`和`char_filter_name`hello 索引需要 toobe 的預先定義或自訂的分析器、 tokenizer、 語彙基元的篩選器和 char 篩選有效的名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="1bf46-667">toolearn 解 hello 語彙分析程序，請參閱[Azure 搜尋中的分析](https://aka.ms/azsanalysis)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="1bf46-668">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-668">**Response**</span></span>

<span data-ttu-id="1bf46-669">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="1bf46-670">hello 回應主體是在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="1bf46-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="1bf46-671">**分析 API 範例**</span><span class="sxs-lookup"><span data-stu-id="1bf46-671">**Analyze API example**</span></span>

<span data-ttu-id="1bf46-672">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="1bf46-673">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="1bf46-674">文件操作</span><span class="sxs-lookup"><span data-stu-id="1bf46-674">Document Operations</span></span>
<span data-ttu-id="1bf46-675">在 Azure 搜尋中，索引會儲存在 hello 雲端，並使用您上傳 toohello 服務的 JSON 文件填入。</span><span class="sxs-lookup"><span data-stu-id="1bf46-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="1bf46-676">您上傳的所有 hello 文件的各都構成 hello 主體的搜尋資料的分類。</span><span class="sxs-lookup"><span data-stu-id="1bf46-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="1bf46-677">文件會包含欄位，其中一些欄位會在它們上傳時語彙基元化為搜尋字詞。</span><span class="sxs-lookup"><span data-stu-id="1bf46-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="1bf46-678">hello `/docs` hello Azure 搜尋 API 中的 URL 區段代表 hello 集合中索引的文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="1bf46-679">例如上傳的 hello 集合上執行的所有作業，合併、 刪除或查詢文件都需要單一的索引，因此 hello Url hello 內容中的位置，這些作業一律會以啟動`/indexes/[index name]/docs`指定的索引名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="1bf46-680">應用程式程式碼必須產生 JSON 文件 tooupload tooAzure 搜尋，或者您可以使用[索引子](https://msdn.microsoft.com/library/dn946891.aspx)tooload 文件，如果 hello 資料來源是 Azure SQL Database 或 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="1bf46-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="1bf46-681">通常，索引是從您提供的單一資料集填入。</span><span class="sxs-lookup"><span data-stu-id="1bf46-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="1bf46-682">您應該計劃讓每個項目，您會想 toosearch 一份文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="1bf46-683">電影出租應用程式可能是每部電影有一份文件、店面應用程式可能是每個 SKU 有一份文件、線上課程應用程式可能是每個課程有一份文件、研究公司可能會在他們的存放庫中針對每份學術報告有一份文件，依此類推。</span><span class="sxs-lookup"><span data-stu-id="1bf46-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="1bf46-684">文件是由一或多個欄位所組成。</span><span class="sxs-lookup"><span data-stu-id="1bf46-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="1bf46-685">欄位包含已由 Azure 搜尋服務語彙基元化為搜尋字詞的文字，以及非語彙基元化或非文字的值 (這類值可用於篩選器或評分設定檔)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="1bf46-686">hello 名稱、 資料類型，以及支援每個欄位的搜尋功能取決於 hello 索引結構描述。</span><span class="sxs-lookup"><span data-stu-id="1bf46-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="1bf46-687">其中每個索引結構描述中的 hello 欄位必須指定為識別碼，以及每個文件必須具有唯一識別該文件 hello 索引中的 hello 識別碼欄位的值。</span><span class="sxs-lookup"><span data-stu-id="1bf46-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="1bf46-688">所有其他文件欄位是選擇性的若未將預設 tooa null 值。</span><span class="sxs-lookup"><span data-stu-id="1bf46-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="1bf46-689">請注意，null 值不會佔用 hello 搜尋索引中的空間。</span><span class="sxs-lookup"><span data-stu-id="1bf46-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="1bf46-690">您可以上傳文件之前，您必須已經建立 hello 索引 hello 服務上。</span><span class="sxs-lookup"><span data-stu-id="1bf46-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="1bf46-691">如需這第一個步驟的詳細資訊，請參閱 [建立索引](#CreateIndex) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="1bf46-692">新增、更新或刪除文件</span><span class="sxs-lookup"><span data-stu-id="1bf46-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="1bf46-693">您可以使用 HTTP POST，從指定的索引上傳、合併、合併或上傳，或者刪除文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="1bf46-694">對於大量的更新中，批次 （每個批次 too1000 文件） 或 16MB 批次的文件的建議。</span><span class="sxs-lookup"><span data-stu-id="1bf46-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="1bf46-695">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-695">**Request**</span></span>

<span data-ttu-id="1bf46-696">所有服務要求都需使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="1bf46-697">您可以使用 HTTP POST，從指定的索引上傳、合併、合併或上傳，或者刪除文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="1bf46-698">hello 要求 URI 包含 [索引名稱] 中，指定哪些索引 toopost 文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="1bf46-699">您只可以一次張貼的文件 tooone 索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="1bf46-700">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-701">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-702">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-703">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-703">**Request Headers**</span></span>

<span data-ttu-id="1bf46-704">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-705">`Content-Type`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-705">`Content-Type`: Required.</span></span> <span data-ttu-id="1bf46-706">設定得`application/json`</span><span class="sxs-lookup"><span data-stu-id="1bf46-706">Set this too`application/json`</span></span>
* <span data-ttu-id="1bf46-707">`api-key`：必要。</span><span class="sxs-lookup"><span data-stu-id="1bf46-707">`api-key`: Required.</span></span> <span data-ttu-id="1bf46-708">hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-709">它是字串值、 唯一 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="1bf46-710">hello**加入文件**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="1bf46-711">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-712">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-713">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-714">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-714">**Request Body**</span></span>

<span data-ttu-id="1bf46-715">hello hello 要求主體包含一或多個文件 toobe 編製索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="1bf46-716">文件是透過唯一的索引鍵來識別。</span><span class="sxs-lookup"><span data-stu-id="1bf46-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="1bf46-717">每份文件都會與下列某個動作相關聯：上傳、合併、合併或上傳，或是刪除。</span><span class="sxs-lookup"><span data-stu-id="1bf46-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="1bf46-718">上傳要求必須包含 hello 文件資料做為索引鍵/值組集合。</span><span class="sxs-lookup"><span data-stu-id="1bf46-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="1bf46-719">文件索引鍵可以只包含字母、數字、連字號 ("-")、底線 ("_")，及等號 ("=")。</span><span class="sxs-lookup"><span data-stu-id="1bf46-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="1bf46-720">如需詳細資訊，請參閱 [命名規則](https://msdn.microsoft.com/library/azure/dn857353.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="1bf46-721">**文件動作**</span><span class="sxs-lookup"><span data-stu-id="1bf46-721">**Document Actions**</span></span>

* <span data-ttu-id="1bf46-722">`upload`： 上傳動作是類似 tooan"upsert"(如果它是新插入和更新/取代如果它存在 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="1bf46-723">請注意在 hello 更新情況下會取代所有欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="1bf46-724">`merge`： 現有文件以 hello 合併更新指定的欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="1bf46-725">如果 hello 文件不存在，hello 合併將會失敗。</span><span class="sxs-lookup"><span data-stu-id="1bf46-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="1bf46-726">您在合併中指定任何欄位將會取代 hello hello 文件中的現有欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="1bf46-727">這包括類型 `Collection(Edm.String)`的欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="1bf46-728">例如，如果 hello 文件包含的欄位值的"tags"`["budget"]`和執行的合併值`["economy", "pool"]`hello 「 標記 」 欄位 hello 最終值將會是 「 標記 」， `["economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="1bf46-729">而**不**會是 `["budget", "economy", "pool"]`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="1bf46-730">`mergeOrUpload`： 行為類似`merge`如果 hello 索引中的文件以 hello 給定索引鍵已經存在。</span><span class="sxs-lookup"><span data-stu-id="1bf46-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="1bf46-731">如果 hello 文件不存在，其行為類似`upload`與新的文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="1bf46-732">`delete`: Delete 會移除 hello 索引中的 hello 指定文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="1bf46-733">請注意，所有的欄位您指定在`delete`hello 索引鍵欄位以外的作業將會被忽略。</span><span class="sxs-lookup"><span data-stu-id="1bf46-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="1bf46-734">如果您想 tooremove 個別欄位從 文件，請使用`merge`相反地，並直接將 hello 欄位明確太`null`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="1bf46-735">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-735">**Response**</span></span>

<span data-ttu-id="1bf46-736">成功回應時會傳回的狀態碼 200 (OK)，表示所有項目都已成功編製索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="1bf46-737">這會由 hello`status`屬性所設定的所有項目，以及 hello tootrue `statusCode` tooeither 201 （適用於新上傳的文件） 」 或 「 200 （如合併或刪除文件） 所設定的屬性：</span><span class="sxs-lookup"><span data-stu-id="1bf46-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="1bf46-738">至少有一個項目未成功建立索引時會傳回狀態碼 207 (多狀態)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="1bf46-739">未索引的項目具有 hello`status`欄位設定 toofalse。</span><span class="sxs-lookup"><span data-stu-id="1bf46-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="1bf46-740">hello`errorMessage`和`statusCode`屬性會指出 hello hello 索引錯誤的原因：</span><span class="sxs-lookup"><span data-stu-id="1bf46-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="1bf46-741">下表中的 hello 說明的 hello 各種個別文件可以 hello 回應中傳回的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="1bf46-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="1bf46-742">請注意一些表示 hello 要求本身的問題，而其他人指出暫時性錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="1bf46-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="1bf46-743">您應該在延遲之後重試的 hello 後者。</span><span class="sxs-lookup"><span data-stu-id="1bf46-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="1bf46-744">狀態碼</span><span class="sxs-lookup"><span data-stu-id="1bf46-744">Status code</span></span></th>
        <th><span data-ttu-id="1bf46-745">意義</span><span class="sxs-lookup"><span data-stu-id="1bf46-745">Meaning</span></span></th>
        <th><span data-ttu-id="1bf46-746">可重試</span><span class="sxs-lookup"><span data-stu-id="1bf46-746">Retryable</span></span></th>
        <th><span data-ttu-id="1bf46-747">注意事項</span><span class="sxs-lookup"><span data-stu-id="1bf46-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-748">200</span><span class="sxs-lookup"><span data-stu-id="1bf46-748">200</span></span></td>
        <td><span data-ttu-id="1bf46-749">已成功修改或刪除文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="1bf46-750">n/a</span><span class="sxs-lookup"><span data-stu-id="1bf46-750">n/a</span></span></td>
        <td><span data-ttu-id="1bf46-751">刪除作業為<a href="https://en.wikipedia.org/wiki/Idempotence">等冪</a>。</span><span class="sxs-lookup"><span data-stu-id="1bf46-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="1bf46-752">也就是說，即使文件索引鍵不存在於 hello 索引中，刪除作業嘗試以該金鑰會導致 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="1bf46-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-753">201</span><span class="sxs-lookup"><span data-stu-id="1bf46-753">201</span></span></td>
        <td><span data-ttu-id="1bf46-754">已成功建立文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="1bf46-755">n/a</span><span class="sxs-lookup"><span data-stu-id="1bf46-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-756">400</span><span class="sxs-lookup"><span data-stu-id="1bf46-756">400</span></span></td>
        <td><span data-ttu-id="1bf46-757">導致無法進行索引的 hello 文件時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1bf46-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="1bf46-758">否</span><span class="sxs-lookup"><span data-stu-id="1bf46-758">No</span></span></td>
        <td><span data-ttu-id="1bf46-759">hello 回應 hello 錯誤訊息將指出的錯誤與 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-760">404</span><span class="sxs-lookup"><span data-stu-id="1bf46-760">404</span></span></td>
        <td><span data-ttu-id="1bf46-761">無法合併 hello 文件，因為 hello 給定索引鍵不存在於 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="1bf46-762">否</span><span class="sxs-lookup"><span data-stu-id="1bf46-762">No</span></span></td>
        <td><span data-ttu-id="1bf46-763">此錯誤不會發生於上傳，因為它們會建立新文件，並且不會發生於刪除，因為它們是<a href="https://en.wikipedia.org/wiki/Idempotence">等冪</a>。</span><span class="sxs-lookup"><span data-stu-id="1bf46-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-764">409</span><span class="sxs-lookup"><span data-stu-id="1bf46-764">409</span></span></td>
        <td><span data-ttu-id="1bf46-765">嘗試 tooindex 文件時偵測到版本發生衝突。</span><span class="sxs-lookup"><span data-stu-id="1bf46-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="1bf46-766">是</span><span class="sxs-lookup"><span data-stu-id="1bf46-766">Yes</span></span></td>
        <td><span data-ttu-id="1bf46-767">當您考慮 tooindex hello 相同文件超過一次同時，也可能會發生。</span><span class="sxs-lookup"><span data-stu-id="1bf46-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-768">422</span><span class="sxs-lookup"><span data-stu-id="1bf46-768">422</span></span></td>
        <td><span data-ttu-id="1bf46-769">hello 索引是暫時無法使用，因為它已更新與 hello 'allowIndexDowntime' 旗標集 too'true'。</span><span class="sxs-lookup"><span data-stu-id="1bf46-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="1bf46-770">是</span><span class="sxs-lookup"><span data-stu-id="1bf46-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="1bf46-771">503</span><span class="sxs-lookup"><span data-stu-id="1bf46-771">503</span></span></td>
        <td><span data-ttu-id="1bf46-772">您的搜尋服務是暫時無法使用，可能是因為 tooheavy 負載。</span><span class="sxs-lookup"><span data-stu-id="1bf46-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="1bf46-773">是</span><span class="sxs-lookup"><span data-stu-id="1bf46-773">Yes</span></span></td>
        <td><span data-ttu-id="1bf46-774">您的程式碼應等待重試一次在此情況下，或您可能會延長 hello 服務無法使用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="1bf46-775">**請注意**： 如果您的用戶端程式碼經常發生 207 回應，一個可能的原因是 hello 系統是否承受負載。</span><span class="sxs-lookup"><span data-stu-id="1bf46-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="1bf46-776">您可以藉由檢查 hello 確認`statusCode`503 的屬性。</span><span class="sxs-lookup"><span data-stu-id="1bf46-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="1bf46-777">如果這是 hello 案例，我們建議您***節流索引要求***。</span><span class="sxs-lookup"><span data-stu-id="1bf46-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="1bf46-778">否則，如果索引的流量不會處理並減少，hello 系統可能會開始拒絕所有要求，出現 503 錯誤。</span><span class="sxs-lookup"><span data-stu-id="1bf46-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="1bf46-779">狀態碼 429 表示您已超過每個索引的文件的 hello 數目配額。</span><span class="sxs-lookup"><span data-stu-id="1bf46-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="1bf46-780">您必須建立新的索引，或進行升級以取得更高的容量限制。</span><span class="sxs-lookup"><span data-stu-id="1bf46-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="1bf46-781">**範例：**</span><span class="sxs-lookup"><span data-stu-id="1bf46-781">**Example:**</span></span>

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="1bf46-782">搜尋文件</span><span class="sxs-lookup"><span data-stu-id="1bf46-782">Search Documents</span></span>
<span data-ttu-id="1bf46-783">A**搜尋**作業發出為 GET 或 POST 要求，並指定參數，以提供選取相符文件的 hello 準則。</span><span class="sxs-lookup"><span data-stu-id="1bf46-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="1bf46-784">**當 toouse 張貼而不是 GET**</span><span class="sxs-lookup"><span data-stu-id="1bf46-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="1bf46-785">當您使用 HTTP GET toocall hello**搜尋**API，您需要 toobe 注意 hello hello 要求 URL 長度不能超過 8 KB。</span><span class="sxs-lookup"><span data-stu-id="1bf46-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="1bf46-786">這對大部分的應用程式通常已足夠。</span><span class="sxs-lookup"><span data-stu-id="1bf46-786">This is usually enough for most applications.</span></span> <span data-ttu-id="1bf46-787">不過，有些應用程式會產生非常大型的查詢或 OData 篩選條件運算式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="1bf46-788">對於這些應用程式而言，使用 HTTP POST 是較好的選擇，因為它允許比 GET 更大型的篩選與查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="1bf46-789">使用 POST、 hello 條款或在查詢子句數目 hello 限制因素，不 hello 的 hello 原始查詢因為 POST hello 要求大小限制為大約 16 MB 的大小。</span><span class="sxs-lookup"><span data-stu-id="1bf46-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-790">即使 hello POST 要求的大小限制是非常大，搜尋查詢及篩選條件運算式不能任意複雜。</span><span class="sxs-lookup"><span data-stu-id="1bf46-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="1bf46-791">如需搜尋查詢和篩選複雜性限制的詳細資訊，請參閱 [Lucene 查詢語法](https://msdn.microsoft.com/library/mt589323.aspx)和 [OData 運算式語法](https://msdn.microsoft.com/library/dn798921.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="1bf46-792">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-792">**Request**</span></span>

<span data-ttu-id="1bf46-793">服務要求需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="1bf46-794">hello**搜尋**要求可以使用 hello GET 或 POST 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="1bf46-795">hello 要求 URI 中指定的索引 tooquery，符合 hello 參數的所有文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="1bf46-796">Hello hello 大小寫的 GET 要求中的查詢字串上指定參數，並在 hello 要求在 hello 情況下，使用 post 要求主體要求。</span><span class="sxs-lookup"><span data-stu-id="1bf46-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="1bf46-797">最佳作法是建立 GET 要求時，請記住太[要作 URL 編碼](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx)參數呼叫時直接 hello REST API 的特定查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="1bf46-798">針對 **搜尋** 作業，這包括：</span><span class="sxs-lookup"><span data-stu-id="1bf46-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="1bf46-799">在上述查詢參數的 hello 只建議 URL 編碼。</span><span class="sxs-lookup"><span data-stu-id="1bf46-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="1bf46-800">如果您不小心 URL 編碼 hello 整個查詢字串 （所有項目之後 hello？），要求將會中斷。</span><span class="sxs-lookup"><span data-stu-id="1bf46-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="1bf46-801">此外，URL 編碼必要時才呼叫的 hello 直接使用 REST API 取得。</span><span class="sxs-lookup"><span data-stu-id="1bf46-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="1bf46-802">呼叫時，無編碼的 URL 是必要**搜尋**使用 POST，或在使用 hello [.NET 用戶端程式庫](https://msdn.microsoft.com/library/dn951165.aspx)，處理 URL 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="1bf46-803"><a name="SearchQueryParameters"></a>
**查詢參數**</span><span class="sxs-lookup"><span data-stu-id="1bf46-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="1bf46-804">**搜尋** 會接受數個可提供查詢準則以及指定搜尋行為的參數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="1bf46-805">您提供這些 hello URL 中的參數呼叫時，查詢字串**搜尋**透過 GET，以及當呼叫 hello 要求主體中的 JSON 屬性**搜尋**透過 POST。</span><span class="sxs-lookup"><span data-stu-id="1bf46-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="1bf46-806">某些參數的 hello 語法是 GET 和 POST 之間稍有不同。</span><span class="sxs-lookup"><span data-stu-id="1bf46-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="1bf46-807">這些差異已適當在以下標示：</span><span class="sxs-lookup"><span data-stu-id="1bf46-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="1bf46-808">`search=[string]`（選用）-hello 文字 toosearch 的。</span><span class="sxs-lookup"><span data-stu-id="1bf46-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="1bf46-809">除非指定 `searchFields`，否則預設會搜尋所有的 `searchable` 欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="1bf46-810">搜尋時`searchable`欄位，hello 搜尋文字本身會 token 化，因此可以由空白字元分隔多個詞彙 (例如： `search=hello world`)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="1bf46-811">toomatch 任何詞彙中，使用`*`（這可以是布林值篩選查詢很有用）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="1bf46-812">省略這個參數具有相同效果與將它設定太 hello`*`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="1bf46-813">請參閱[簡單查詢語法](https://msdn.microsoft.com/library/dn798920.aspx)hello 搜尋語法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1bf46-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="1bf46-814">**請注意**: hello 結果有時會令人意外查詢整個`searchable`欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="1bf46-815">hello tokenizer 邏輯 toohandle 案例常見 tooEnglish 中包括文字像是所有格符號、 逗號等數字。例如，`search=123,456`會比對單一字詞 123456，而不是 hello 個別字詞 123 與 456，因為逗號會做為千分位分隔符號的英文中大型數字。</span><span class="sxs-lookup"><span data-stu-id="1bf46-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="1bf46-816">基於這個理由，我們建議泛空白字元，而不是標點符號 tooseparate 詞彙在 hello`search`參數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="1bf46-817">`searchMode=any|all`(選擇性，預設值太`any`)-是否為相符的順序 toocount hello 文件中，則必須符合任何或所有 hello 搜尋詞彙。</span><span class="sxs-lookup"><span data-stu-id="1bf46-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="1bf46-818">`searchFields=[string]`（選用）-指定文字的逗號分隔的欄位名稱 toosearch hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="1bf46-819">目標欄位必須標記為 `searchable`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="1bf46-820">`queryType=simple|full`(選擇性的預設值太`simple`)-時設定太 「 簡單的 」 的搜尋文字會解譯使用允許的符號，例如簡單的查詢語言 +、 * 及""。</span><span class="sxs-lookup"><span data-stu-id="1bf46-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="1bf46-821">預設會跨越每份文件中的所有可搜尋欄位 (或以 `searchFields`表示的欄位) 評估查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="1bf46-822">Hello 查詢型別時設定太`full`搜尋的文字會解譯使用 hello 可讓特定的欄位和加權搜尋 Lucene 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="1bf46-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="1bf46-823">請參閱[簡單查詢語法](https://msdn.microsoft.com/library/dn798920.aspx)和[Lucene 的查詢語法](https://msdn.microsoft.com/library/mt589323.aspx)上 hello 搜尋語法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1bf46-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="1bf46-824">範圍 hello Lucene 改用 $filter 提供類似的功能不支援的查詢語言中的搜尋。</span><span class="sxs-lookup"><span data-stu-id="1bf46-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="1bf46-825">`moreLikeThis=[key]` (選用) **重要：**此功能僅適用於 `2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-826">這個選項不能包含 hello 文字搜尋參數，查詢中`search=[string]`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="1bf46-827">hello`moreLikeThis`參數會尋找類似 hello 文件索引鍵所指定的 toohello 文件的文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="1bf46-828">當使用已搜尋要求`moreLikeThis`，根據 hello 頻率和罕見的 hello 來源文件中的條款所產生的搜尋詞彙清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="1bf46-829">這些詞彙會接著使用的 toomake hello 要求。</span><span class="sxs-lookup"><span data-stu-id="1bf46-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="1bf46-830">根據預設，hello 的所有內容`searchable`欄位視為除非`searchFields`是使用的 toorestrict 會搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="1bf46-831">`$skip=#`（選用）-hello 數字的搜尋結果 tooskip;不能大於 100000 的。</span><span class="sxs-lookup"><span data-stu-id="1bf46-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="1bf46-832">如果您需要 tooscan 文件順序，但不能使用`$skip`到期 toothis 限制，請考慮使用`$orderby`完全排序索引鍵和`$filter`改為使用範圍查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-833">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `skip` 而不是 `$skip`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="1bf46-834">`$top=#`（選用）-hello 數字的搜尋結果 tooretrieve。</span><span class="sxs-lookup"><span data-stu-id="1bf46-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="1bf46-835">這可以用於搭配`$skip`tooimplement 用戶端分頁搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="1bf46-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-836">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `top` 而不是 `$top`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="1bf46-837">`$count=true|false`(選擇性，預設值太`false`)-指定是否 toofetch hello 結果的總計數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="1bf46-838">這是符合 hello 的所有文件的 hello 計數`search`和`$filter`參數，忽略`$top`和`$skip`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="1bf46-839">將此值設定為太`true`可能會造成效能影響。</span><span class="sxs-lookup"><span data-stu-id="1bf46-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="1bf46-840">請注意，傳回 hello 計數是近似值。</span><span class="sxs-lookup"><span data-stu-id="1bf46-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-841">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `count` 而不是 `$count`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="1bf46-842">`$orderby=[string]`（選用）-根據以逗號分隔的運算式 toosort hello 結果的清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="1bf46-843">每個運算式可以是欄位名稱，或是呼叫 toohello`geo.distance()`函式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="1bf46-844">每個運算式後面可以接著`asc`tooindicated 遞增，和`desc`tooindicate 遞減。</span><span class="sxs-lookup"><span data-stu-id="1bf46-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="1bf46-845">hello 預設為遞增順序。</span><span class="sxs-lookup"><span data-stu-id="1bf46-845">hello default is ascending order.</span></span> <span data-ttu-id="1bf46-846">繫結將會 hello 文件相符分數所中斷。</span><span class="sxs-lookup"><span data-stu-id="1bf46-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="1bf46-847">如果沒有`$orderby`指定，則 hello 預設排序順序依照文件相符分數遞減。</span><span class="sxs-lookup"><span data-stu-id="1bf46-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="1bf46-848">針對 `$orderby`，有 32 個子句的限制。</span><span class="sxs-lookup"><span data-stu-id="1bf46-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-849">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `orderby` 而不是 `$orderby`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="1bf46-850">`$select=[string]`（選用）-tooretrieve 以逗號分隔欄位的清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="1bf46-851">如果未指定，會包含 標示為可擷取 hello 結構描述中的所有欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="1bf46-852">您可以將這個參數設定為太，以同時也可以明確要求所有欄位`*`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-853">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `select` 而不是 `$select`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="1bf46-854">`facet=[string]`（零或多個）-由欄位 toofacet。</span><span class="sxs-lookup"><span data-stu-id="1bf46-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="1bf46-855">Hello 字串可能會選擇性地包含以逗號分隔的參數 toocustomize hello faceting`name:value`組。</span><span class="sxs-lookup"><span data-stu-id="1bf46-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="1bf46-856">有效參數包括：</span><span class="sxs-lookup"><span data-stu-id="1bf46-856">Valid parameters are:</span></span>

* <span data-ttu-id="1bf46-857">`count` (Facet 字詞的最大數目；預設值為 10)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="1bf46-858">沒有最大值，但較高的值會產生對應的 「 效能造成負面影響，特別是當 hello faceted 欄位包含大量的唯一字詞。</span><span class="sxs-lookup"><span data-stu-id="1bf46-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="1bf46-859">例如：`facet=category,count:5`取得 hello facet 結果中的前五個類別。</span><span class="sxs-lookup"><span data-stu-id="1bf46-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="1bf46-860">**請注意**： 如果 hello`count`參數小於唯一字詞數目 hello、 hello 結果可能不正確。</span><span class="sxs-lookup"><span data-stu-id="1bf46-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="1bf46-861">這是因為 faceting 查詢分散於分區 toohello 方式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="1bf46-862">增加`count`通常會增加 hello 精確度 hello 字詞計數，但在效能成本。</span><span class="sxs-lookup"><span data-stu-id="1bf46-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="1bf46-863">`sort`(其中`count`toosort*遞減*依計數， `-count` toosort*遞增*依計數， `value` toosort*遞增*值，或`-value` toosort*遞減*值)</span><span class="sxs-lookup"><span data-stu-id="1bf46-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="1bf46-864">例如：`facet=category,count:3,sort:count`取得 hello facet 結果中的每個縣 （市） 名稱的文件的 hello 數目，依遞減順序的前三個類別。</span><span class="sxs-lookup"><span data-stu-id="1bf46-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="1bf46-865">例如，如果 hello 前三個類別為預算、 Motel 和 Luxury，和 Budget 有 5 個命中、 Motel 有 6 個，而 Luxury 有 4，則 hello 值區會 hello 順序 Motel、 預算、 Luxury。</span><span class="sxs-lookup"><span data-stu-id="1bf46-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="1bf46-866">例如： `facet=rating,sort:-value` 會以依值的遞減排序方式，針對所有可能的評等來產生值區。</span><span class="sxs-lookup"><span data-stu-id="1bf46-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="1bf46-867">例如，如果 hello 評等是從 1 too5，hello 值區的排序是 5，4，3，2，1，不論是多少文件符合每個評等。</span><span class="sxs-lookup"><span data-stu-id="1bf46-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="1bf46-868">`values` (直立線符號分隔的數字或 `Edm.DateTimeOffset` 值，可指定一組動態的多面向項目值)</span><span class="sxs-lookup"><span data-stu-id="1bf46-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="1bf46-869">例如：`facet=baseRate,values:10|20`會產生三個值區： 一個用於基底費率 0 toobut 不包括 10，一個用於 10 向上 toobut 不包括 20，而另一個用於 20 或更高版本上。</span><span class="sxs-lookup"><span data-stu-id="1bf46-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="1bf46-870">舉例來說：`facet=lastRenovationDate,values:2010-02-01T00:00:00Z` 會產生兩個值區：一個用於 2010 年 2 月之前重新整修的旅館，另一個則用於 2010 年 2 月 1 日以後重新整修的旅館。</span><span class="sxs-lookup"><span data-stu-id="1bf46-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="1bf46-871">`interval` (如果是數字，整數間隔大於 0，如果是日期時間值，則為 `minute`、`hour`、`day`、`week`、`month`、`quarter` 或 `year`)</span><span class="sxs-lookup"><span data-stu-id="1bf46-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="1bf46-872">例如：`facet=baseRate,interval:100` 會根據大小為 100 的基本匯率範圍來產生值區。</span><span class="sxs-lookup"><span data-stu-id="1bf46-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="1bf46-873">舉例來說，如果基本匯率全都介於 60 美元到 600 美元之間，則會有下列值區：0-100、100-200、200-300、300-400、400-500 及 500-600。</span><span class="sxs-lookup"><span data-stu-id="1bf46-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="1bf46-874">例如：`facet=lastRenovationDate,interval:year` 會在旅館重新整修期間，每一年產生一個值區。</span><span class="sxs-lookup"><span data-stu-id="1bf46-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="1bf46-875">`timeoffset` ([+-]hh:mm、[+-]hhmm 或 [+-]hh) `timeoffset` 為選用項目。</span><span class="sxs-lookup"><span data-stu-id="1bf46-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="1bf46-876">僅可以結合以 hello `interval`  選項，並且只有當類型套用的 tooa 欄位`Edm.DateTimeOffset`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="1bf46-877">hello 值指定為 hello UTC 時間位移的 tooaccount 設定時間界限。</span><span class="sxs-lookup"><span data-stu-id="1bf46-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="1bf46-878">例如：`facet=lastRenovationDate,interval:day,timeoffset:-01:00`使用 hello 01:00:00 utc （hello 目標時區的午夜） 開始的日界限</span><span class="sxs-lookup"><span data-stu-id="1bf46-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="1bf46-879">**請注意**:`count`和`sort`可以結合在 hello 相同 facet 規格中，但它們無法與結合`interval`或`values`，和`interval`和`values`無法合併在一起。</span><span class="sxs-lookup"><span data-stu-id="1bf46-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="1bf46-880">**注意**：如果未指定 `timeoffset`，日期時間上的間隔 Facet 就會根據 UTC 時間來計算。</span><span class="sxs-lookup"><span data-stu-id="1bf46-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="1bf46-881">例如： 針對`facet=lastRenovationDate,interval:day`，00:00:00 utc 開始 hello 天界限。</span><span class="sxs-lookup"><span data-stu-id="1bf46-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="1bf46-882">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `facets` 而不是 `facet`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="1bf46-883">此外，您會將它指定為字串的 JSON 陣列，其中每個字串是不同的 facet 運算式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="1bf46-884">`$filter=[string]` (選用) - 使用標準 OData 語法的結構化搜尋運算式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-885">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `filter` 而不是 `$filter`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="1bf46-886">`highlight=[string]` (選用) - 一組適用於點閱數醒目提示的逗號分隔欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="1bf46-887">只有 `searchable` 欄位可用於點閱數醒目提示。</span><span class="sxs-lookup"><span data-stu-id="1bf46-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="1bf46-888">`highlightPreTag=[string]`(選擇性，預設值太`<em>`)-字串前面加上 toohit 反白顯示的標記。</span><span class="sxs-lookup"><span data-stu-id="1bf46-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="1bf46-889">必須使用 `highlightPostTag`來設定。</span><span class="sxs-lookup"><span data-stu-id="1bf46-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-890">當呼叫**搜尋**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="1bf46-891">`highlightPostTag=[string]`(選擇性，預設值太`</em>`)-將附加 toohit 反白顯示的字串標記。</span><span class="sxs-lookup"><span data-stu-id="1bf46-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="1bf46-892">必須使用 `highlightPreTag`來設定。</span><span class="sxs-lookup"><span data-stu-id="1bf46-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-893">當呼叫**搜尋**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="1bf46-894">`scoringProfile=[string]`（選用）-計分設定檔 tooevaluate hello 名稱符合分數排序 toosort hello 結果中的比對文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="1bf46-895">`scoringParameter=[string]`（零或多個）-表示 hello 計分函式中定義的每個參數的值 (例如， `referencePointParameter`) 使用 hello 格式`name-value1,value2,...`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="1bf46-896">例如，如果 hello 計分設定檔定義的函式參數，稱為"mylocation"hello 查詢字串選項會是`&scoringParameter=mylocation--122.2,44.8`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="1bf46-897">hello 第一個虛線 hello 名稱與分隔 hello 值清單中，雖然 hello 第二個虛線是 hello 第一個值 （在此範例中的經度） 的一部分。</span><span class="sxs-lookup"><span data-stu-id="1bf46-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="1bf46-898">計分的參數如標記在提升，可包含逗號，您可以逸出任何這類值使用單引號 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="1bf46-899">如果 hello 值本身包含單引號來逸出它們加倍。</span><span class="sxs-lookup"><span data-stu-id="1bf46-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="1bf46-900">例如，如果您有提升稱為 「 mytag"參數標記，而您想 tooboost hello 標記上的值"Hello，O'Brien"和"Smith"，hello 查詢字串選項會是`&scoringParameter=mytag-'Hello, O''Brien',Smith`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="1bf46-901">請注意，只有包含逗號的值需要引號。</span><span class="sxs-lookup"><span data-stu-id="1bf46-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-902">使用 POST 呼叫**搜尋**時，此參數的名稱會是 `scoringParameters` 而不是 `scoringParameter`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="1bf46-903">此外，您需以 JSON 字串陣列方式指定它，其中每個字串都是個別的 `name-values` 組。</span><span class="sxs-lookup"><span data-stu-id="1bf46-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="1bf46-904">`minimumCoverage`（選擇性，預設 too100）-介於 0 和 100 指出 hello 百分比 hello 索引的搜尋查詢，為了讓 hello 查詢 toobe 必須涵蓋的報告為成功。</span><span class="sxs-lookup"><span data-stu-id="1bf46-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="1bf46-905">根據預設，hello 整個索引必須是可用或`Search`會傳回 HTTP 狀態碼 503。</span><span class="sxs-lookup"><span data-stu-id="1bf46-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="1bf46-906">如果您設定`minimumCoverage`和`Search`成功，則會傳回 HTTP 200，並包含`@search.coverage`hello 回應指出 hello 百分比 hello 索引 hello 查詢中所包含的值。</span><span class="sxs-lookup"><span data-stu-id="1bf46-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-907">設定此參數 tooa 值低於 100 非常適合用於確保搜尋即使對於服務的一個複本的可用性。</span><span class="sxs-lookup"><span data-stu-id="1bf46-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="1bf46-908">但是，並非所有的相符文件都保證 toobe hello 搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="1bf46-909">如果搜尋重新叫用更重要的 tooyour 應用程式比可用性，則它是最佳 tooleave`minimumCoverage`在其預設值為 100。</span><span class="sxs-lookup"><span data-stu-id="1bf46-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="1bf46-910">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-911">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-912">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-913">注意： 這項作業，hello`api-version`做為查詢參數，不論呼叫 hello URL 中指定**搜尋**具有 GET 或 POST。</span><span class="sxs-lookup"><span data-stu-id="1bf46-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="1bf46-914">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-914">**Request Headers**</span></span>

<span data-ttu-id="1bf46-915">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-916">`api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-917">它是字串值，唯一 tooyour 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="1bf46-918">hello**搜尋**要求可以指定將管理金鑰或查詢索引鍵`api-key`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="1bf46-919">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-920">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-921">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-922">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-922">**Request Body**</span></span>

<span data-ttu-id="1bf46-923">針對 GET：None。</span><span class="sxs-lookup"><span data-stu-id="1bf46-923">For GET: None.</span></span>

<span data-ttu-id="1bf46-924">針對 POST：</span><span class="sxs-lookup"><span data-stu-id="1bf46-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="1bf46-925">**接續部分搜尋回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="1bf46-926">有時 Azure 搜尋無法傳回所有 hello 單一搜尋回應中的要求的結果。</span><span class="sxs-lookup"><span data-stu-id="1bf46-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="1bf46-927">這可能是不同的原因，例如當 hello 查詢要求太多文件未指定`$top`或指定的值`$top`太大。</span><span class="sxs-lookup"><span data-stu-id="1bf46-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="1bf46-928">在這種情況下，Azure 搜尋會包含 hello`@odata.nextLink`在 hello 回應主體中，註解以及`@search.nextPageParameters`是否 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="1bf46-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="1bf46-929">您可以使用這些註解 tooformulate hello 值搜尋要求 tooget hello 下一步的另一部分 hello 搜尋回應。</span><span class="sxs-lookup"><span data-stu-id="1bf46-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="1bf46-930">這稱為***接續***hello 原始搜尋要求和 hello 的註解通常稱為***接續 token***。</span><span class="sxs-lookup"><span data-stu-id="1bf46-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="1bf46-931">請參閱[hello 例會](#SearchResponse)如這些註解以及其中會顯示 hello 回應主體中的 hello 語法的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1bf46-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="1bf46-932">為什麼 Azure 搜尋可能會傳回接續 token 的 hello 原因是實作特定與主旨 toochange。</span><span class="sxs-lookup"><span data-stu-id="1bf46-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="1bf46-933">穩定的用戶端應該一律是準備 toohandle 案例，其中會傳回比預期較少的文件，而接續 token 是擷取文件包含的 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1bf46-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="1bf46-934">也請注意，您必須使用 hello 與 hello 原始要求順序 toocontinue 中相同的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="1bf46-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="1bf46-935">例如，如果您傳送 GET 要求，則您傳送的所有接續要求也必須使用 GET (同樣適用於 POST)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="1bf46-936"><a name="SearchResponse"></a>
**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="1bf46-937">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="1bf46-938">**範例：**</span><span class="sxs-lookup"><span data-stu-id="1bf46-938">**Examples:**</span></span>

<span data-ttu-id="1bf46-939">您可以在 hello 找到其他範例[Azure 搜尋的 OData 運算式語法](https://msdn.microsoft.com/library/azure/dn798921.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="1bf46-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="1bf46-940">搜尋 hello 依照日期遞減排序的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="1bf46-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="1bf46-943">在多面向搜尋中，搜尋 hello 索引並擷取 facet 類別、 評等、 標記，以及特定範圍中具有 baseRate 的項目：</span><span class="sxs-lookup"><span data-stu-id="1bf46-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="1bf46-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="1bf46-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="1bf46-946">Hello 使用者按下之後，使用篩選器，縮小先前多面向查詢結果 hello 評等 3 和分類"Motel":</span><span class="sxs-lookup"><span data-stu-id="1bf46-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="1bf46-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="1bf46-949">在多面向搜尋中，為查詢中傳回的唯一字詞數目設定上限。</span><span class="sxs-lookup"><span data-stu-id="1bf46-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="1bf46-950">hello 預設值為 10，但您可以增加或減少此值使用 hello `count` hello 參數`facet`屬性：</span><span class="sxs-lookup"><span data-stu-id="1bf46-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="1bf46-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="1bf46-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="1bf46-953">搜尋特定的欄位; 中的 hello 索引例如，將語言特定欄位：</span><span class="sxs-lookup"><span data-stu-id="1bf46-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="1bf46-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="1bf46-956">跨多個欄位搜尋 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="1bf46-957">例如，您可以儲存和查詢可搜尋的欄位，在多個語言中，全部都在 hello 相同的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="1bf46-958">如果英文和法文描述共存於 hello 相同文件中，您可以傳回任何或所有在 hello 查詢結果：</span><span class="sxs-lookup"><span data-stu-id="1bf46-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="1bf46-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="1bf46-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="1bf46-961">請注意，您一次只能查詢一個索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="1bf46-962">請勿建立針對每個語言的多個索引，除非您規劃 tooquery 一一次。</span><span class="sxs-lookup"><span data-stu-id="1bf46-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="1bf46-963">分頁-取得 hello 第 1 頁的項目 （頁面大小為 10）：</span><span class="sxs-lookup"><span data-stu-id="1bf46-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="1bf46-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="1bf46-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="1bf46-966">分頁-取得 hello 第 2 頁的項目 （頁面大小為 10）：</span><span class="sxs-lookup"><span data-stu-id="1bf46-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="1bf46-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="1bf46-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="1bf46-969">抓取一組特定的欄位：</span><span class="sxs-lookup"><span data-stu-id="1bf46-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="1bf46-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="1bf46-972">抓取符合特定篩選運算式的文件：</span><span class="sxs-lookup"><span data-stu-id="1bf46-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="1bf46-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="1bf46-975">搜尋 hello 索引並傳回具有叫用會反白顯示片段</span><span class="sxs-lookup"><span data-stu-id="1bf46-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="1bf46-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="1bf46-978">搜尋 hello 索引和從遠離的參考位置較接近 toofarther 排序傳回的文件</span><span class="sxs-lookup"><span data-stu-id="1bf46-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="1bf46-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="1bf46-981">搜尋 hello 索引假設名為"currentlocation"的計分設定檔與兩個距離評分函數，一個定義的參數名"為 Lastlocation"和"Geo"的呼叫的參數</span><span class="sxs-lookup"><span data-stu-id="1bf46-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="1bf46-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="1bf46-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="1bf46-984">尋找文件以 hello 索引使用[簡單查詢語法](https://msdn.microsoft.com/library/dn798920.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="1bf46-985">此查詢會傳回可搜尋的欄位位置包含 hello"comfort"和"location"但不是"motel"的旅館：</span><span class="sxs-lookup"><span data-stu-id="1bf46-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="1bf46-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="1bf46-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="1bf46-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="1bf46-988">請注意 hello 使用`searchMode=all`上方。</span><span class="sxs-lookup"><span data-stu-id="1bf46-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="1bf46-989">包含此參數會覆寫 hello 預設值是`searchMode=any`，確保可`-motel`表示"AND NOT"而不是"OR NOT"。</span><span class="sxs-lookup"><span data-stu-id="1bf46-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="1bf46-990">不含`searchMode=all`、 您得到"OR NOT"這會展開，而不是限制搜尋結果，這可能是違反直覺 toosome 使用者。</span><span class="sxs-lookup"><span data-stu-id="1bf46-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="1bf46-991">尋找文件以 hello 索引使用[lucene 的查詢語法](https://msdn.microsoft.com/library/mt589323.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="1bf46-992">此查詢會傳回的旅館其中 hello category 欄位包含 hello 詞彙"budget"和"最近整修"hello 片語的所有可搜尋欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="1bf46-993">包含 「 最近整修"hello 片語的文件是次序比它高 hello 詞彙增量值 (3) 的結果</span><span class="sxs-lookup"><span data-stu-id="1bf46-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="1bf46-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="1bf46-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="1bf46-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="1bf46-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="1bf46-996">查閱文件</span><span class="sxs-lookup"><span data-stu-id="1bf46-996">Lookup Document</span></span>
<span data-ttu-id="1bf46-997">hello**查閱文件**作業會從 Azure 搜尋擷取文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="1bf46-998">使用者按一下特定的搜尋結果，而且您想 toolook 該文件的相關特定詳細資料時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="1bf46-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="1bf46-999">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-999">**Request**</span></span>

<span data-ttu-id="1bf46-1000">服務要求需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="1bf46-1001">hello**查閱文件**要求可以下列方式建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="1bf46-1002">或者，您可以使用 hello 傳統的 OData 語法進行索引鍵查閱：</span><span class="sxs-lookup"><span data-stu-id="1bf46-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="1bf46-1003">hello 要求 URI 包含 [索引名稱] 和 [索引鍵]，指定從哪個索引的文件 tooretrieve。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="1bf46-1004">您一次只能取得一份文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1004">You can only get one document at a time.</span></span> <span data-ttu-id="1bf46-1005">使用**搜尋**tooget 單一要求中的多個文件。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="1bf46-1006">**查詢參數**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1006">**Query Parameters**</span></span>

<span data-ttu-id="1bf46-1007">`$select=[string]`（選用）-tooretrieve 以逗號分隔欄位的清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="1bf46-1008">如果未指定或設定得`*`，hello 投影中包含標示為可擷取 hello 結構描述中的所有欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="1bf46-1009">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-1010">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-1011">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-1012">注意： 這項作業，hello`api-version`指定為查詢參數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="1bf46-1013">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1013">**Request Headers**</span></span>

<span data-ttu-id="1bf46-1014">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-1015">`api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-1016">它是字串值，唯一 tooyour 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="1bf46-1017">hello**查閱文件**要求可以指定將管理金鑰或查詢索引鍵`api-key`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="1bf46-1018">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-1019">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-1020">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-1021">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1021">**Request Body**</span></span>

<span data-ttu-id="1bf46-1022">無。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1022">None.</span></span>

<span data-ttu-id="1bf46-1023">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1023">**Response**</span></span>

<span data-ttu-id="1bf46-1024">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="1bf46-1025">**範例**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1025">**Example**</span></span>

<span data-ttu-id="1bf46-1026">具有索引鍵 '2' 的查閱 hello 文件</span><span class="sxs-lookup"><span data-stu-id="1bf46-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="1bf46-1027">具有索引鍵 '3' 使用 OData 語法查閱 hello 文件：</span><span class="sxs-lookup"><span data-stu-id="1bf46-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="1bf46-1028">文件計數</span><span class="sxs-lookup"><span data-stu-id="1bf46-1028">Count Documents</span></span>
<span data-ttu-id="1bf46-1029">hello**計算文件**作業會擷取搜尋索引文件的 hello 數目的計數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="1bf46-1030">hello`$count`語法是 hello OData 通訊協定的一部分。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="1bf46-1031">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1031">**Request**</span></span>

<span data-ttu-id="1bf46-1032">服務要求需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="1bf46-1033">hello**計算文件**要求可以使用 hello GET 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="1bf46-1034">hello 要求 URI 中的 hello [索引名稱] 會告知 hello 服務 tooreturn 所有項目計數 hello 文件集合中的 hello 指定的索引。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="1bf46-1035">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-1036">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-1037">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-1038">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1038">**Request Headers**</span></span>

<span data-ttu-id="1bf46-1039">hello 下列清單描述所需的 hello 和選擇性要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="1bf46-1040">`Accept`： 這個值必須設定太`text/plain`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="1bf46-1041">`api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-1042">它是字串值，唯一 tooyour 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="1bf46-1043">hello**計算文件**要求可以指定將管理金鑰或查詢索引鍵`api-key`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="1bf46-1044">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-1045">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-1046">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-1047">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1047">**Request Body**</span></span>

<span data-ttu-id="1bf46-1048">無。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1048">None.</span></span>

<span data-ttu-id="1bf46-1049">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1049">**Response**</span></span>

<span data-ttu-id="1bf46-1050">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="1bf46-1051">hello 回應主體會包含 hello 計數值為純文字格式的整數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="1bf46-1052">建議</span><span class="sxs-lookup"><span data-stu-id="1bf46-1052">Suggestions</span></span>
<span data-ttu-id="1bf46-1053">hello**建議**作業會擷取部分搜尋輸入為基礎的建議。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="1bf46-1054">它通常用於搜尋方塊 tooprovide 預先輸入建議在使用者輸入搜尋詞彙。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="1bf46-1055">建議要求以建議目標文件為目標，因此 hello 建議可能重複文字，是否多個候選文件符合 hello 相同搜尋輸入。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="1bf46-1056">您可以使用`$select`tooretrieve 其他文件欄位 （包括 hello 文件索引鍵），以便您可以分辨哪份文件是一項建議的 hello 來源。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="1bf46-1057">**建議** 作業會以 GET 或 POST 要求發出。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="1bf46-1058">**當 toouse 張貼而不是 GET**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="1bf46-1059">當您使用 HTTP GET toocall hello**建議**API，您需要 toobe 注意 hello hello 要求 URL 長度不能超過 8 KB。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="1bf46-1060">這對大部分的應用程式通常已足夠。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="1bf46-1061">不過，有些應用程式會產生非常大型的查詢，特別是 OData 篩選條件運算式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="1bf46-1062">對於這些應用程式而言，使用 HTTP POST 是較好的選擇，因為它允許比 GET 更大型的篩選。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="1bf46-1063">使用 post 要求在篩選子句的 hello 數目是 hello 限制因素，不 hello hello 未經處理的篩選字串的大小，因為 POST hello 要求大小限制為大約 16 MB。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1064">即使 hello POST 要求的大小限制是非常大，不能任意複雜的篩選條件運算式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="1bf46-1065">如需有關篩選複雜性限制的詳細資訊，請參閱 [OData 運算式語法](https://msdn.microsoft.com/library/dn798921.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="1bf46-1066">**要求**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1066">**Request**</span></span>

<span data-ttu-id="1bf46-1067">服務要求需要使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="1bf46-1068">hello**建議**要求可以使用 hello GET 或 POST 方法建構。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="1bf46-1069">hello 要求 URI 會指定 hello 索引 tooquery hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="1bf46-1070">Hello hello 大小寫的 GET 要求中的查詢字串中指定參數，例如 hello 部分輸入的搜尋詞彙，並在 hello 要求在 hello 情況下，使用 post 要求主體要求。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="1bf46-1071">最佳作法是建立 GET 要求時，請記住太[要作 URL 編碼](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx)參數呼叫時直接 hello REST API 的特定查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="1bf46-1072">針對 **建議** 作業，這包括：</span><span class="sxs-lookup"><span data-stu-id="1bf46-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="1bf46-1073">在上述查詢參數的 hello 只建議 URL 編碼。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="1bf46-1074">如果您不小心 URL 編碼 hello 整個查詢字串 （所有項目之後 hello？），要求將會中斷。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="1bf46-1075">此外，URL 編碼必要時才呼叫的 hello 直接使用 REST API 取得。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="1bf46-1076">呼叫時，無編碼的 URL 是必要**建議**使用 POST，或在使用 hello [.NET 用戶端程式庫](https://msdn.microsoft.com/library/dn951165.aspx)，處理 URL 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="1bf46-1077">**查詢參數**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1077">**Query Parameters**</span></span>

<span data-ttu-id="1bf46-1078">**建議** 會接受數個可提供查詢準則以及指定搜尋行為的參數。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="1bf46-1079">您提供這些 hello URL 中的參數呼叫時，查詢字串**建議**透過 GET，以及當呼叫 hello 要求主體中的 JSON 屬性**建議**透過 POST。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="1bf46-1080">某些參數的 hello 語法是 GET 和 POST 之間稍有不同。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="1bf46-1081">這些差異已適當在以下標示：</span><span class="sxs-lookup"><span data-stu-id="1bf46-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="1bf46-1082">`search=[string]`-hello 搜尋文字 toouse toosuggest 查詢。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="1bf46-1083">必須至少 1 個字元，而且不能多於 100 個字元。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="1bf46-1084">`highlightPreTag=[string]`（選用）-toosearch 命中結果前面加上字串標記。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="1bf46-1085">必須使用 `highlightPostTag`來設定。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1086">當呼叫**建議**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="1bf46-1087">`highlightPostTag=[string]`（選用）-將附加 toosearch 叫用的字串標記。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="1bf46-1088">必須使用 `highlightPreTag`來設定。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1089">當呼叫**建議**使用 GET，hello URL 中的保留的字元必須是百分比編碼 （例如，%23 而不是 #）。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="1bf46-1090">`suggesterName=[string]`-hello 中所指定的 hello 與 hello 建議工具名稱`suggesters`屬於 hello 索引定義的集合。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="1bf46-1091">`suggester` 會判斷要針對建議的查詢字詞掃描哪些欄位。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="1bf46-1092">如需詳細資訊，請參閱 [建議工具](#Suggesters) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="1bf46-1093">`fuzzy=[boolean]`(選擇性，預設值 = false)-當設定 tootrue API 也會尋找建議，即使在 hello 搜尋文字取代或遺失的字元。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="1bf46-1094">儘管這在某些案例中可提供較佳的體驗，但它也需要付出效能成本代價，因為模糊建議搜尋的速度較慢且耗用更多資源。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="1bf46-1095">`searchFields=[string]`（選用）-指定搜尋文字的逗號分隔的欄位名稱 toosearch hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="1bf46-1096">您必須啟用目標欄位才能提供建議。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="1bf46-1097">`$top=#`(選擇性，預設值 = 5)-hello 建議 tooretrieve 數目。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="1bf46-1098">必須是 1 到 100 之間的數字。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1099">使用 POST 呼叫**建議**時，此參數的名稱是 `top` 而不是 `$top`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="1bf46-1100">`$filter=[string]`（選用）-篩選 hello 文件的運算式被視為建議。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1101">使用 POST 呼叫**建議**時，此參數的名稱是 `filter` 而不是 `$filter`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="1bf46-1102">`$orderby=[string]`（選用）-根據以逗號分隔的運算式 toosort hello 結果的清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="1bf46-1103">每個運算式可以是欄位名稱，或是呼叫 toohello`geo.distance()`函式。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="1bf46-1104">每個運算式後面可以接著`asc`tooindicated 遞增，和`desc`tooindicate 遞減。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="1bf46-1105">hello 預設為遞增順序。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1105">hello default is ascending order.</span></span> <span data-ttu-id="1bf46-1106">針對 `$orderby`，有 32 個子句的限制。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1107">使用 POST 呼叫**建議**時，此參數的名稱是 `orderby` 而不是 `$orderby`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="1bf46-1108">`$select=[string]`（選用）-tooretrieve 以逗號分隔欄位的清單。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="1bf46-1109">如果未指定，只有 hello 文件索引鍵，並傳回建議的文字。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="1bf46-1110">將這個參數設定過，您可以明確要求所有欄位`*`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1111">使用 POST 呼叫**建議**時，此參數的名稱是 `select` 而不是 `$select`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="1bf46-1112">`minimumCoverage`（選擇性，預設 too80）-介於 0 和 100 指出 hello 百分比 hello 索引順序 hello 查詢 toobe 建議查詢必須涵蓋的報告為成功。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="1bf46-1113">根據預設，在至少 80%的 hello 索引必須是可用或`Suggest`會傳回 HTTP 狀態碼 503。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="1bf46-1114">如果您設定`minimumCoverage`和`Suggest`成功，則會傳回 HTTP 200，並包含`@search.coverage`hello 回應指出 hello 百分比 hello 索引 hello 查詢中所包含的值。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="1bf46-1115">設定此參數 tooa 值低於 100 非常適合用於確保搜尋即使對於服務的一個複本的可用性。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="1bf46-1116">但是，並非所有相符的建議都保證 toobe hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="1bf46-1117">如果重新叫用是更重要的 tooyour 應用程式可用性，則最不 toolower 比`minimumCoverage`下方其預設值 80。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="1bf46-1118">`api-version=[string]` (必要)。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="1bf46-1119">hello 預覽版本`api-version=2015-02-28-Preview`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="1bf46-1120">如需詳細資訊和替代版本，請參閱 [搜尋服務版本設定](http://msdn.microsoft.com/library/azure/dn864560.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="1bf46-1121">注意： 這項作業，hello`api-version`做為查詢參數，不論呼叫 hello URL 中指定**建議**具有 GET 或 POST。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="1bf46-1122">**要求標頭**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1122">**Request Headers**</span></span>

<span data-ttu-id="1bf46-1123">hello 下列清單描述所需的 hello 和選擇性要求標頭</span><span class="sxs-lookup"><span data-stu-id="1bf46-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="1bf46-1124">`api-key`: hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="1bf46-1125">它是字串值，唯一 tooyour 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="1bf46-1126">hello**建議**要求可以指定將管理金鑰或查詢索引鍵為 hello `api-key`。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="1bf46-1127">您也需要 hello 服務名稱 tooconstruct hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="1bf46-1128">您可以取得 hello 服務名稱和`api-key`從服務儀表板 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="1bf46-1129">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)取得頁面導覽說明。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="1bf46-1130">**要求本文**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1130">**Request Body**</span></span>

<span data-ttu-id="1bf46-1131">針對 GET：None。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1131">For GET: None.</span></span>

<span data-ttu-id="1bf46-1132">針對 POST：</span><span class="sxs-lookup"><span data-stu-id="1bf46-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="1bf46-1133">**回應**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1133">**Response**</span></span>

<span data-ttu-id="1bf46-1134">回應成功時會傳回狀態碼：200 OK。</span><span class="sxs-lookup"><span data-stu-id="1bf46-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="1bf46-1135">如果 hello 投影選項是使用的 tooretrieve 欄位在 hello 陣列的每個項目包括：</span><span class="sxs-lookup"><span data-stu-id="1bf46-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="1bf46-1136">**範例**</span><span class="sxs-lookup"><span data-stu-id="1bf46-1136">**Example**</span></span>

<span data-ttu-id="1bf46-1137">擷取其中 hello 部分搜尋輸入是 'lux' 的 5 個建議</span><span class="sxs-lookup"><span data-stu-id="1bf46-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
