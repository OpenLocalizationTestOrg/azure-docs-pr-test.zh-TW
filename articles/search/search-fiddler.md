---
title: "如何使用 Fiddler 評估及測試 Azure 搜尋服務 REST API | Microsoft Docs"
description: "使用 Fiddler 以無程式碼的方式驗證 Azure 搜尋服務的可用性，並試用 REST API。"
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
ms.openlocfilehash: c38b73fa69bee34ce2434c6274cb017c99ef3c35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="ad7ea-103">使用 Fiddler 評估及測試 Azure 搜尋 REST API</span><span class="sxs-lookup"><span data-stu-id="ad7ea-103">Use Fiddler to evaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="ad7ea-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ad7ea-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="ad7ea-105">搜尋總管</span><span class="sxs-lookup"><span data-stu-id="ad7ea-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="ad7ea-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="ad7ea-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="ad7ea-107">.NET</span><span class="sxs-lookup"><span data-stu-id="ad7ea-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="ad7ea-108">REST</span><span class="sxs-lookup"><span data-stu-id="ad7ea-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="ad7ea-109">本文說明如何使用 Fiddler ( [可從 Telerik 免費下載](http://www.telerik.com/fiddler))，以在不必撰寫任何程式碼的情況下，透過 Azure 搜尋服務 REST API 發送 HTTP 要求以及檢視回應。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span></span> <span data-ttu-id="ad7ea-110">Azure 搜尋服務是 Microsoft Azure 上完整管理的雲端託管搜尋服務，可輕鬆地透過 .NET 和 REST API 程式化。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="ad7ea-111">[MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx)中記載了 Azure 搜尋服務 REST API。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="ad7ea-112">在下列步驟中，您將建立索引、上傳文件、查詢索引，然後查詢系統以取得服務資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span></span>

<span data-ttu-id="ad7ea-113">若要完成這些步驟，您將需要 Azure 搜尋服務和 `api-key`。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-113">To complete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="ad7ea-114">如需起始步驟的指示，請參閱 [在入口網站中建立 Azure 搜尋服務](search-create-service-portal.md) 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="ad7ea-115">建立索引</span><span class="sxs-lookup"><span data-stu-id="ad7ea-115">Create an index</span></span>
1. <span data-ttu-id="ad7ea-116">啟動 Fiddler。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-116">Start Fiddler.</span></span> <span data-ttu-id="ad7ea-117">在 [File (檔案)] 功能表上，關閉 [Capture Traffic (擷取流量)] 以隱藏與目前工作無關的 HTTP 活動。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span></span>
2. <span data-ttu-id="ad7ea-118">在 [編寫器]  索引標籤上，您可以制訂如下列螢幕擷取畫面所示的要求：</span><span class="sxs-lookup"><span data-stu-id="ad7ea-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="ad7ea-119">選取 [PUT] 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-119">Select **PUT**.</span></span>
4. <span data-ttu-id="ad7ea-120">輸入可指定服務 URL、要求屬性和 API 版本的 URL。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span></span> <span data-ttu-id="ad7ea-121">請留意以下幾點：</span><span class="sxs-lookup"><span data-stu-id="ad7ea-121">A few pointers to keep in mind:</span></span>

   * <span data-ttu-id="ad7ea-122">使用 HTTPS 做為首碼。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-122">Use HTTPS as the prefix.</span></span>
   * <span data-ttu-id="ad7ea-123">要求屬性為 "/indexes/hotels"。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="ad7ea-124">這可告知「搜尋」建立名為 'hotels' 的索引。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-124">This tells Search to create an index named 'hotels'.</span></span>
   * <span data-ttu-id="ad7ea-125">API 版本為小寫，並指定為 "?api-version=2016-09-01"。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="ad7ea-126">API 版本十分重要，因為 Azure 搜尋服務會定期部署更新。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="ad7ea-127">在極少數情況下，更新服務可能會對 API 造成中斷變更。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-127">On rare occasions, a service update may introduce a breaking change to the API.</span></span> <span data-ttu-id="ad7ea-128">基於這個理由，Azure 搜尋服務在每個要求中都需要 API 版本，才能讓您完全控制使用的版本。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="ad7ea-129">完整 URL 應該會類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-129">The full URL should look similar to the following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="ad7ea-130">指定要求標頭，使用服務的有效值取代主機和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="ad7ea-131">在 [Request Body (要求本文)] 中，貼上構成索引定義的欄位。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-131">In Request Body, paste in the fields that make up the index definition.</span></span>

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
7. <span data-ttu-id="ad7ea-132">按一下 [Execute (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-132">Click **Execute**.</span></span>

<span data-ttu-id="ad7ea-133">幾秒鐘後，您應該就會在工作階段清單中看見 HTTP 201 的回應，指出已成功建立索引。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span></span>

<span data-ttu-id="ad7ea-134">如果您收到 HTTP 504，請確認 URL 所指定的是 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-134">If you get HTTP 504, verify the URL specifies HTTPS.</span></span> <span data-ttu-id="ad7ea-135">如果您看見 HTTP 400 或 404，請查看要求本文以確認並沒有「複製-貼上」錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span></span> <span data-ttu-id="ad7ea-136">HTTP 403 通常表示 API 金鑰有問題 (可能是金鑰無效或是用來指定 API 金鑰的語法有問題)。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="ad7ea-137">載入文件</span><span class="sxs-lookup"><span data-stu-id="ad7ea-137">Load documents</span></span>
<span data-ttu-id="ad7ea-138">在 [編寫器]  索引標籤上，張貼文件的要求會類似如下。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-138">On the **Composer** tab, your request to post documents will look like the following.</span></span> <span data-ttu-id="ad7ea-139">要求本文包含 4 間飯店的搜尋資料。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-139">The body of the request contains the search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="ad7ea-140">選取 [POST] 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-140">Select **POST**.</span></span>
2. <span data-ttu-id="ad7ea-141">輸入以 HTTPS 開頭的 URL，並於後面依序加上服務 URL 和 "/indexes/<'indexname'>/docs/index?api-version=2016-09-01"。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="ad7ea-142">完整 URL 應該會類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-142">The full URL should look similar to the following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="ad7ea-143">要求標頭應與之前的相同。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-143">Request Header should be the same as before.</span></span> <span data-ttu-id="ad7ea-144">請記住，您已使用您服務的有效值取代主機和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-144">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="ad7ea-145">[Request Body (要求本文)] 包含 4 個要新增到飯店索引的文件。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-145">The Request Body contains four documents to be added to the hotels index.</span></span>

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
             "description": "This could be the one",
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
5. <span data-ttu-id="ad7ea-146">按一下 [Execute (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-146">Click **Execute**.</span></span>

<span data-ttu-id="ad7ea-147">幾秒鐘後，您應該就會在工作階段清單中看見 HTTP 200 的回應。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-147">In a few seconds, you should see an HTTP 200 response in the session list.</span></span> <span data-ttu-id="ad7ea-148">這表示已成功建立文件。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-148">This indicates the documents were created successfully.</span></span> <span data-ttu-id="ad7ea-149">如果您收到 207，表示至少有一個文件上傳失敗。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-149">If you get a 207, at least one document failed to upload.</span></span> <span data-ttu-id="ad7ea-150">如果您收到 404，則表示要求的標頭或本文有語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-150">If you get a 404, you have a syntax error in either the header or body of the request.</span></span>

## <a name="query-the-index"></a><span data-ttu-id="ad7ea-151">查詢索引</span><span class="sxs-lookup"><span data-stu-id="ad7ea-151">Query the index</span></span>
<span data-ttu-id="ad7ea-152">現在已載入索引和文件，您可以對其發出查詢。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="ad7ea-153">在 [編寫器] 索引標籤上，查詢服務的 **GET** 命令會類似下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="ad7ea-154">選取 [GET] 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-154">Select **GET**.</span></span>
2. <span data-ttu-id="ad7ea-155">輸入以 HTTPS 開頭，並於後面依序加上服務 URL、"/indexes/<'indexname'>/docs?" 和查詢參數的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="ad7ea-156">舉例來說，使用下列 URL，並以服務的有效值取代範例主機名稱。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="ad7ea-157">此查詢會搜尋「motel」一字，並擷取評等的 Facet 類別。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="ad7ea-158">要求標頭應與之前的相同。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-158">Request Header should be the same as before.</span></span> <span data-ttu-id="ad7ea-159">請記住，您已使用您服務的有效值取代主機和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-159">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="ad7ea-160">回應碼應為 200，而回應輸出應該會類似下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-160">The response code should be 200, and the response output should look similar to the following screen shot.</span></span>

   ![][4]

<span data-ttu-id="ad7ea-161">下列範例查詢來自 MSDN 上的 [搜尋索引作業 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/dn798927.aspx) (英文)。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="ad7ea-162">此主題中有許多範例查詢包含空格，這在 Fiddler 中是不允許的。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="ad7ea-163">因此，請先使用 + 字元取代空格，再貼到查詢字串中，然後再於 Fiddler 中嘗試該查詢：</span><span class="sxs-lookup"><span data-stu-id="ad7ea-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span></span>

<span data-ttu-id="ad7ea-164">**取代空格之前：**</span><span class="sxs-lookup"><span data-stu-id="ad7ea-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="ad7ea-165">**以 + 取代空格之後：**</span><span class="sxs-lookup"><span data-stu-id="ad7ea-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a><span data-ttu-id="ad7ea-166">查詢系統</span><span class="sxs-lookup"><span data-stu-id="ad7ea-166">Query the system</span></span>
<span data-ttu-id="ad7ea-167">您也可以查詢系統以取得文件計數和儲存體用量。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-167">You can also query the system to get document counts and storage consumption.</span></span> <span data-ttu-id="ad7ea-168">在 [編寫器]  索引標籤上，您的要求會類似如下，且回應會傳回文件計數和空間使用量。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="ad7ea-169">選取 [GET] 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-169">Select **GET**.</span></span>
2. <span data-ttu-id="ad7ea-170">輸入含有服務 URL 的 URL，並於後面加上 "/indexes/hotels/stats?api-version=2016-09-01"：</span><span class="sxs-lookup"><span data-stu-id="ad7ea-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="ad7ea-171">指定要求標頭，使用服務的有效值取代主機和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="ad7ea-172">讓要求本文保持空白。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-172">Leave the request body empty.</span></span>
5. <span data-ttu-id="ad7ea-173">按一下 [Execute (執行)] 。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-173">Click **Execute**.</span></span> <span data-ttu-id="ad7ea-174">您應該會在工作階段清單中看到 HTTP 200 的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-174">You should see an HTTP 200 status code in the session list.</span></span> <span data-ttu-id="ad7ea-175">選取為命令張貼的項目。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-175">Select the entry posted for your command.</span></span>
6. <span data-ttu-id="ad7ea-176">依序按一下 [檢測器] 索引標籤和 [標頭] 索引標籤，然後選取 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span></span> <span data-ttu-id="ad7ea-177">您應該會看到文件計數和儲存體大小 (以 KB計算)。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-177">You should see the document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad7ea-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad7ea-178">Next steps</span></span>
<span data-ttu-id="ad7ea-179">請參閱 [管理 Azure 上的搜尋服務](search-manage.md) ，了解以不使用程式碼的方式管理和使用 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="ad7ea-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
