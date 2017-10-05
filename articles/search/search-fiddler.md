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
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a>使用 Fiddler 評估及測試 Azure 搜尋 REST API
> [!div class="op_single_selector"]
>
> * [概觀](search-query-overview.md)
> * [搜尋總管](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

本文說明如何使用 Fiddler ( [可從 Telerik 免費下載](http://www.telerik.com/fiddler))，以在不必撰寫任何程式碼的情況下，透過 Azure 搜尋服務 REST API 發送 HTTP 要求以及檢視回應。 Azure 搜尋服務是 Microsoft Azure 上完整管理的雲端託管搜尋服務，可輕鬆地透過 .NET 和 REST API 程式化。 [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx)中記載了 Azure 搜尋服務 REST API。

在下列步驟中，您將建立索引、上傳文件、查詢索引，然後查詢系統以取得服務資訊。

若要完成這些步驟，您將需要 Azure 搜尋服務和 `api-key`。 如需起始步驟的指示，請參閱 [在入口網站中建立 Azure 搜尋服務](search-create-service-portal.md) 。

## <a name="create-an-index"></a>建立索引
1. 啟動 Fiddler。 在 [File (檔案)] 功能表上，關閉 [Capture Traffic (擷取流量)] 以隱藏與目前工作無關的 HTTP 活動。
2. 在 [編寫器]  索引標籤上，您可以制訂如下列螢幕擷取畫面所示的要求：

      ![][1]
3. 選取 [PUT] 。
4. 輸入可指定服務 URL、要求屬性和 API 版本的 URL。 請留意以下幾點：

   * 使用 HTTPS 做為首碼。
   * 要求屬性為 "/indexes/hotels"。 這可告知「搜尋」建立名為 'hotels' 的索引。
   * API 版本為小寫，並指定為 "?api-version=2016-09-01"。 API 版本十分重要，因為 Azure 搜尋服務會定期部署更新。 在極少數情況下，更新服務可能會對 API 造成中斷變更。 基於這個理由，Azure 搜尋服務在每個要求中都需要 API 版本，才能讓您完全控制使用的版本。

     完整 URL 應該會類似下列範例。

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. 指定要求標頭，使用服務的有效值取代主機和 API 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. 在 [Request Body (要求本文)] 中，貼上構成索引定義的欄位。

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
7. 按一下 [Execute (執行)] 。

幾秒鐘後，您應該就會在工作階段清單中看見 HTTP 201 的回應，指出已成功建立索引。

如果您收到 HTTP 504，請確認 URL 所指定的是 HTTPS。 如果您看見 HTTP 400 或 404，請查看要求本文以確認並沒有「複製-貼上」錯誤。 HTTP 403 通常表示 API 金鑰有問題 (可能是金鑰無效或是用來指定 API 金鑰的語法有問題)。

## <a name="load-documents"></a>載入文件
在 [編寫器]  索引標籤上，張貼文件的要求會類似如下。 要求本文包含 4 間飯店的搜尋資料。

   ![][2]

1. 選取 [POST] 。
2. 輸入以 HTTPS 開頭的 URL，並於後面依序加上服務 URL 和 "/indexes/<'indexname'>/docs/index?api-version=2016-09-01"。 完整 URL 應該會類似下列範例。

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. 要求標頭應與之前的相同。 請記住，您已使用您服務的有效值取代主機和 API 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. [Request Body (要求本文)] 包含 4 個要新增到飯店索引的文件。

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
5. 按一下 [Execute (執行)] 。

幾秒鐘後，您應該就會在工作階段清單中看見 HTTP 200 的回應。 這表示已成功建立文件。 如果您收到 207，表示至少有一個文件上傳失敗。 如果您收到 404，則表示要求的標頭或本文有語法錯誤。

## <a name="query-the-index"></a>查詢索引
現在已載入索引和文件，您可以對其發出查詢。  在 [編寫器] 索引標籤上，查詢服務的 **GET** 命令會類似下列螢幕擷取畫面。

   ![][3]

1. 選取 [GET] 。
2. 輸入以 HTTPS 開頭，並於後面依序加上服務 URL、"/indexes/<'indexname'>/docs?" 和查詢參數的完整 URL。 舉例來說，使用下列 URL，並以服務的有效值取代範例主機名稱。

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   此查詢會搜尋「motel」一字，並擷取評等的 Facet 類別。
3. 要求標頭應與之前的相同。 請記住，您已使用您服務的有效值取代主機和 API 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

回應碼應為 200，而回應輸出應該會類似下列螢幕擷取畫面。

   ![][4]

下列範例查詢來自 MSDN 上的 [搜尋索引作業 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/dn798927.aspx) (英文)。 此主題中有許多範例查詢包含空格，這在 Fiddler 中是不允許的。 因此，請先使用 + 字元取代空格，再貼到查詢字串中，然後再於 Fiddler 中嘗試該查詢：

**取代空格之前：**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**以 + 取代空格之後：**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a>查詢系統
您也可以查詢系統以取得文件計數和儲存體用量。 在 [編寫器]  索引標籤上，您的要求會類似如下，且回應會傳回文件計數和空間使用量。

 ![][5]

1. 選取 [GET] 。
2. 輸入含有服務 URL 的 URL，並於後面加上 "/indexes/hotels/stats?api-version=2016-09-01"：

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. 指定要求標頭，使用服務的有效值取代主機和 API 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. 讓要求本文保持空白。
5. 按一下 [Execute (執行)] 。 您應該會在工作階段清單中看到 HTTP 200 的狀態碼。 選取為命令張貼的項目。
6. 依序按一下 [檢測器] 索引標籤和 [標頭] 索引標籤，然後選取 JSON 格式。 您應該會看到文件計數和儲存體大小 (以 KB計算)。

## <a name="next-steps"></a>後續步驟
請參閱 [管理 Azure 上的搜尋服務](search-manage.md) ，了解以不使用程式碼的方式管理和使用 Azure 搜尋服務。

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
