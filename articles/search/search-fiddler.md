---
title: "aaaHow toouse Fiddler tooevaluate 和測試 Azure 搜尋 REST Api |Microsoft 文件"
description: "使用 Fiddler 無程式碼的方法 tooverifying Azure 搜尋可用性，並嘗試 hello REST Api。"
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="fb653-103">使用 Fiddler tooevaluate 和測試 Azure 搜尋 REST Api</span><span class="sxs-lookup"><span data-stu-id="fb653-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="fb653-104">概觀</span><span class="sxs-lookup"><span data-stu-id="fb653-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="fb653-105">搜尋總管</span><span class="sxs-lookup"><span data-stu-id="fb653-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="fb653-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="fb653-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="fb653-107">.NET</span><span class="sxs-lookup"><span data-stu-id="fb653-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="fb653-108">REST</span><span class="sxs-lookup"><span data-stu-id="fb653-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="fb653-109">這篇文章說明如何 toouse Fiddler，可做為[telerik 免費下載](http://www.telerik.com/fiddler)、 使用 hello Azure 搜尋 REST API，而不需要任何程式碼 toowrite tooissue HTTP 要求 tooand 檢視回應。</span><span class="sxs-lookup"><span data-stu-id="fb653-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="fb653-110">Azure 搜尋服務是 Microsoft Azure 上完整管理的雲端託管搜尋服務，可輕鬆地透過 .NET 和 REST API 程式化。</span><span class="sxs-lookup"><span data-stu-id="fb653-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="fb653-111">hello Azure 搜尋服務 REST Api 的記錄[MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fb653-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="fb653-112">在下列步驟 hello，您將建立索引上, 傳文件、 查詢 hello 索引，和取得服務資訊的查詢 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="fb653-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="fb653-113">toocomplete 這些步驟，您必須在 Azure 搜尋服務和`api-key`。</span><span class="sxs-lookup"><span data-stu-id="fb653-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="fb653-114">請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)如需有關如何啟動 tooget 指示。</span><span class="sxs-lookup"><span data-stu-id="fb653-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="fb653-115">建立索引</span><span class="sxs-lookup"><span data-stu-id="fb653-115">Create an index</span></span>
1. <span data-ttu-id="fb653-116">啟動 Fiddler。</span><span class="sxs-lookup"><span data-stu-id="fb653-116">Start Fiddler.</span></span> <span data-ttu-id="fb653-117">在 hello**檔案**功能表上，關閉**擷取的流量**toohide 多餘 HTTP 活動不相關的 toohello 目前的工作。</span><span class="sxs-lookup"><span data-stu-id="fb653-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="fb653-118">在 hello**編輯器**索引標籤上，您會編寫看起來像下列螢幕擷取畫面的 hello 的要求。</span><span class="sxs-lookup"><span data-stu-id="fb653-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="fb653-119">選取 [PUT] 。</span><span class="sxs-lookup"><span data-stu-id="fb653-119">Select **PUT**.</span></span>
4. <span data-ttu-id="fb653-120">輸入 URL 指定 hello 服務 URL、 要求屬性與 hello 的 api 版本。</span><span class="sxs-lookup"><span data-stu-id="fb653-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="fb653-121">請注意幾個指標 tookeep:</span><span class="sxs-lookup"><span data-stu-id="fb653-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="fb653-122">使用 HTTPS 做 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="fb653-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="fb653-123">要求屬性為 "/indexes/hotels"。</span><span class="sxs-lookup"><span data-stu-id="fb653-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="fb653-124">這會告知搜尋 toocreate 名為 '旅館' 的索引。</span><span class="sxs-lookup"><span data-stu-id="fb653-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="fb653-125">API 版本為小寫，並指定為 "?api-version=2016-09-01"。</span><span class="sxs-lookup"><span data-stu-id="fb653-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="fb653-126">API 版本十分重要，因為 Azure 搜尋服務會定期部署更新。</span><span class="sxs-lookup"><span data-stu-id="fb653-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="fb653-127">在少數情況下，服務更新可能會導入重大變更 toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="fb653-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="fb653-128">基於這個理由，Azure 搜尋服務在每個要求中都需要 API 版本，才能讓您完全控制使用的版本。</span><span class="sxs-lookup"><span data-stu-id="fb653-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="fb653-129">hello 完整的 URL 應該類似下列範例的 toohello。</span><span class="sxs-lookup"><span data-stu-id="fb653-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="fb653-130">指定 hello 要求標頭，以對服務有效的值取代 hello 主機和 api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="fb653-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="fb653-131">在要求主體中，貼上 hello 欄位組成 hello 索引定義中。</span><span class="sxs-lookup"><span data-stu-id="fb653-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="fb653-132">按一下 [Execute (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="fb653-132">Click **Execute**.</span></span>

<span data-ttu-id="fb653-133">在幾秒鐘，您應該會看見 hello 工作階段清單中的 HTTP 201 回應，指出 hello 索引已成功建立。</span><span class="sxs-lookup"><span data-stu-id="fb653-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="fb653-134">如果您收到 HTTP 504，請確認 hello URL 會指定 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="fb653-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="fb653-135">如果您看到 HTTP 400 或 404，請檢查 hello 要求有內文 tooverify 時沒有複製-貼上發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fb653-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="fb653-136">HTTP 403 通常表示有問題 hello api 金鑰 （金鑰無效或語法問題 hello api 金鑰的指定方式）。</span><span class="sxs-lookup"><span data-stu-id="fb653-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="fb653-137">載入文件</span><span class="sxs-lookup"><span data-stu-id="fb653-137">Load documents</span></span>
<span data-ttu-id="fb653-138">在 hello**編輯器**索引標籤上，您的要求 toopost 文件看起來像下列 hello。</span><span class="sxs-lookup"><span data-stu-id="fb653-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="fb653-139">hello hello 要求主體包含 4 旅館的 hello 搜尋資料。</span><span class="sxs-lookup"><span data-stu-id="fb653-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="fb653-140">選取 [POST] 。</span><span class="sxs-lookup"><span data-stu-id="fb653-140">Select **POST**.</span></span>
2. <span data-ttu-id="fb653-141">輸入以 HTTPS 開頭的 URL，並於後面依序加上服務 URL 和 "/indexes/<'indexname'>/docs/index?api-version=2016-09-01"。</span><span class="sxs-lookup"><span data-stu-id="fb653-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="fb653-142">hello 完整的 URL 應該類似下列範例的 toohello。</span><span class="sxs-lookup"><span data-stu-id="fb653-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="fb653-143">要求標頭應該是 hello 相同和以前一樣。</span><span class="sxs-lookup"><span data-stu-id="fb653-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="fb653-144">請記住，以對服務有效的值取代 hello 主機和 api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="fb653-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="fb653-145">hello 要求主體包含四個文件 toobe 加入的 toohello 旅館索引。</span><span class="sxs-lookup"><span data-stu-id="fb653-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="fb653-146">按一下 [Execute (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="fb653-146">Click **Execute**.</span></span>

<span data-ttu-id="fb653-147">在幾秒鐘，您應該會看到 HTTP 200 的回應 hello 工作階段清單中。</span><span class="sxs-lookup"><span data-stu-id="fb653-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="fb653-148">這表示已成功建立文件的 hello。</span><span class="sxs-lookup"><span data-stu-id="fb653-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="fb653-149">如果您收到 207，無法 tooupload 至少一個文件。</span><span class="sxs-lookup"><span data-stu-id="fb653-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="fb653-150">如果您收到 404 時，您會有 hello 標頭或 hello 要求主體中的有語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="fb653-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="fb653-151">查詢 hello 索引</span><span class="sxs-lookup"><span data-stu-id="fb653-151">Query hello index</span></span>
<span data-ttu-id="fb653-152">現在已載入索引和文件，您可以對其發出查詢。</span><span class="sxs-lookup"><span data-stu-id="fb653-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="fb653-153">在 hello**編輯器**索引標籤上，**取得**查詢您的服務的命令看起來類似 toohello 下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="fb653-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="fb653-154">選取 [GET] 。</span><span class="sxs-lookup"><span data-stu-id="fb653-154">Select **GET**.</span></span>
2. <span data-ttu-id="fb653-155">輸入以 HTTPS 開頭，並於後面依序加上服務 URL、"/indexes/<'indexname'>/docs?" 和查詢參數的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="fb653-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="fb653-156">範例中，透過使用下列 URL，使用適用於您的服務的其中一個取代 hello 範例主機名稱的 hello。</span><span class="sxs-lookup"><span data-stu-id="fb653-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="fb653-157">此查詢搜尋 hello 詞彙"motel"，並擷取 facet 評等的類別。</span><span class="sxs-lookup"><span data-stu-id="fb653-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="fb653-158">要求標頭應該是 hello 相同和以前一樣。</span><span class="sxs-lookup"><span data-stu-id="fb653-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="fb653-159">請記住，以對服務有效的值取代 hello 主機和 api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="fb653-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="fb653-160">hello 回應碼應為 200，和 hello 回應的輸出應該看起來類似 toohello 下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="fb653-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="fb653-161">hello 下列範例查詢是從 hello[搜尋索引作業 (Azure 搜尋 API)](http://msdn.microsoft.com/library/dn798927.aspx) MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="fb653-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="fb653-162">本主題中的 hello 範例查詢的許多包含空格、 Fiddler 中不允許。</span><span class="sxs-lookup"><span data-stu-id="fb653-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="fb653-163">每個空間與 + 字元之前 hello 貼到查詢字串，然後再嘗試 Fiddler 中的 hello 查詢取代。</span><span class="sxs-lookup"><span data-stu-id="fb653-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="fb653-164">**取代空格之前：**</span><span class="sxs-lookup"><span data-stu-id="fb653-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="fb653-165">**以 + 取代空格之後：**</span><span class="sxs-lookup"><span data-stu-id="fb653-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="fb653-166">查詢 hello 系統</span><span class="sxs-lookup"><span data-stu-id="fb653-166">Query hello system</span></span>
<span data-ttu-id="fb653-167">您也可以查詢 hello 系統 tooget 文件計數和儲存體耗用量。</span><span class="sxs-lookup"><span data-stu-id="fb653-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="fb653-168">在 hello**編輯器**索引標籤上，您的要求看起來類似 toohello 下列項目，而且 hello 回應會傳回文件和使用空間的 hello 數目的計數。</span><span class="sxs-lookup"><span data-stu-id="fb653-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="fb653-169">選取 [GET] 。</span><span class="sxs-lookup"><span data-stu-id="fb653-169">Select **GET**.</span></span>
2. <span data-ttu-id="fb653-170">輸入含有服務 URL 的 URL，並於後面加上 "/indexes/hotels/stats?api-version=2016-09-01"：</span><span class="sxs-lookup"><span data-stu-id="fb653-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="fb653-171">指定 hello 要求標頭，以對服務有效的值取代 hello 主機和 api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="fb653-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="fb653-172">將 hello 要求主體保留空白。</span><span class="sxs-lookup"><span data-stu-id="fb653-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="fb653-173">按一下 [Execute (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="fb653-173">Click **Execute**.</span></span> <span data-ttu-id="fb653-174">您應該會看到 hello 工作階段清單中的 HTTP 200 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="fb653-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="fb653-175">選取您的命令為公佈 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="fb653-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="fb653-176">按一下 hello**偵測器**索引標籤上，按一下 hello**標頭**索引標籤，然後再選取 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="fb653-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="fb653-177">您應該會看到 hello 文件計數和儲存體大小 （以 kb 為單位）。</span><span class="sxs-lookup"><span data-stu-id="fb653-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb653-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb653-178">Next steps</span></span>
<span data-ttu-id="fb653-179">請參閱[管理您的搜尋服務在 Azure 上](search-manage.md)沒有程式碼方法 toomanaging 及使用 Azure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="fb653-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
