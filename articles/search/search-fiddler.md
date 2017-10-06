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
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>使用 Fiddler tooevaluate 和測試 Azure 搜尋 REST Api
> [!div class="op_single_selector"]
>
> * [概觀](search-query-overview.md)
> * [搜尋總管](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

這篇文章說明如何 toouse Fiddler，可做為[telerik 免費下載](http://www.telerik.com/fiddler)、 使用 hello Azure 搜尋 REST API，而不需要任何程式碼 toowrite tooissue HTTP 要求 tooand 檢視回應。 Azure 搜尋服務是 Microsoft Azure 上完整管理的雲端託管搜尋服務，可輕鬆地透過 .NET 和 REST API 程式化。 hello Azure 搜尋服務 REST Api 的記錄[MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx)。

在下列步驟 hello，您將建立索引上, 傳文件、 查詢 hello 索引，和取得服務資訊的查詢 hello 系統。

toocomplete 這些步驟，您必須在 Azure 搜尋服務和`api-key`。 請參閱[hello 入口網站中建立 Azure 搜尋服務](search-create-service-portal.md)如需有關如何啟動 tooget 指示。

## <a name="create-an-index"></a>建立索引
1. 啟動 Fiddler。 在 hello**檔案**功能表上，關閉**擷取的流量**toohide 多餘 HTTP 活動不相關的 toohello 目前的工作。
2. 在 hello**編輯器**索引標籤上，您會編寫看起來像下列螢幕擷取畫面的 hello 的要求。

      ![][1]
3. 選取 [PUT] 。
4. 輸入 URL 指定 hello 服務 URL、 要求屬性與 hello 的 api 版本。 請注意幾個指標 tookeep:

   * 使用 HTTPS 做 hello 前置詞。
   * 要求屬性為 "/indexes/hotels"。 這會告知搜尋 toocreate 名為 '旅館' 的索引。
   * API 版本為小寫，並指定為 "?api-version=2016-09-01"。 API 版本十分重要，因為 Azure 搜尋服務會定期部署更新。 在少數情況下，服務更新可能會導入重大變更 toohello 應用程式開發介面。 基於這個理由，Azure 搜尋服務在每個要求中都需要 API 版本，才能讓您完全控制使用的版本。

     hello 完整的 URL 應該類似下列範例的 toohello。

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. 指定 hello 要求標頭，以對服務有效的值取代 hello 主機和 api 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. 在要求主體中，貼上 hello 欄位組成 hello 索引定義中。

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

在幾秒鐘，您應該會看見 hello 工作階段清單中的 HTTP 201 回應，指出 hello 索引已成功建立。

如果您收到 HTTP 504，請確認 hello URL 會指定 HTTPS。 如果您看到 HTTP 400 或 404，請檢查 hello 要求有內文 tooverify 時沒有複製-貼上發生錯誤。 HTTP 403 通常表示有問題 hello api 金鑰 （金鑰無效或語法問題 hello api 金鑰的指定方式）。

## <a name="load-documents"></a>載入文件
在 hello**編輯器**索引標籤上，您的要求 toopost 文件看起來像下列 hello。 hello hello 要求主體包含 4 旅館的 hello 搜尋資料。

   ![][2]

1. 選取 [POST] 。
2. 輸入以 HTTPS 開頭的 URL，並於後面依序加上服務 URL 和 "/indexes/<'indexname'>/docs/index?api-version=2016-09-01"。 hello 完整的 URL 應該類似下列範例的 toohello。

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. 要求標頭應該是 hello 相同和以前一樣。 請記住，以對服務有效的值取代 hello 主機和 api 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. hello 要求主體包含四個文件 toobe 加入的 toohello 旅館索引。

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
5. 按一下 [Execute (執行)] 。

在幾秒鐘，您應該會看到 HTTP 200 的回應 hello 工作階段清單中。 這表示已成功建立文件的 hello。 如果您收到 207，無法 tooupload 至少一個文件。 如果您收到 404 時，您會有 hello 標頭或 hello 要求主體中的有語法錯誤。

## <a name="query-hello-index"></a>查詢 hello 索引
現在已載入索引和文件，您可以對其發出查詢。  在 hello**編輯器**索引標籤上，**取得**查詢您的服務的命令看起來類似 toohello 下列螢幕擷取畫面。

   ![][3]

1. 選取 [GET] 。
2. 輸入以 HTTPS 開頭，並於後面依序加上服務 URL、"/indexes/<'indexname'>/docs?" 和查詢參數的完整 URL。 範例中，透過使用下列 URL，使用適用於您的服務的其中一個取代 hello 範例主機名稱的 hello。

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   此查詢搜尋 hello 詞彙"motel"，並擷取 facet 評等的類別。
3. 要求標頭應該是 hello 相同和以前一樣。 請記住，以對服務有效的值取代 hello 主機和 api 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

hello 回應碼應為 200，和 hello 回應的輸出應該看起來類似 toohello 下列螢幕擷取畫面。

   ![][4]

hello 下列範例查詢是從 hello[搜尋索引作業 (Azure 搜尋 API)](http://msdn.microsoft.com/library/dn798927.aspx) MSDN 上。 本主題中的 hello 範例查詢的許多包含空格、 Fiddler 中不允許。 每個空間與 + 字元之前 hello 貼到查詢字串，然後再嘗試 Fiddler 中的 hello 查詢取代。

**取代空格之前：**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**以 + 取代空格之後：**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>查詢 hello 系統
您也可以查詢 hello 系統 tooget 文件計數和儲存體耗用量。 在 hello**編輯器**索引標籤上，您的要求看起來類似 toohello 下列項目，而且 hello 回應會傳回文件和使用空間的 hello 數目的計數。

 ![][5]

1. 選取 [GET] 。
2. 輸入含有服務 URL 的 URL，並於後面加上 "/indexes/hotels/stats?api-version=2016-09-01"：

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. 指定 hello 要求標頭，以對服務有效的值取代 hello 主機和 api 金鑰。

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. 將 hello 要求主體保留空白。
5. 按一下 [Execute (執行)] 。 您應該會看到 hello 工作階段清單中的 HTTP 200 狀態碼。 選取您的命令為公佈 hello 項目。
6. 按一下 hello**偵測器**索引標籤上，按一下 hello**標頭**索引標籤，然後再選取 hello JSON 格式。 您應該會看到 hello 文件計數和儲存體大小 （以 kb 為單位）。

## <a name="next-steps"></a>後續步驟
請參閱[管理您的搜尋服務在 Azure 上](search-manage.md)沒有程式碼方法 toomanaging 及使用 Azure 搜尋。

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
