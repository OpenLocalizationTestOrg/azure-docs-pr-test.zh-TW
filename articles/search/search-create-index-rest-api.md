---
title: "aaa\"建立索引 (REST API 的 Azure 搜尋) |Microsoft 文件 」"
description: "使用 hello Azure 搜尋 HTTP 的 REST API 的程式碼中建立索引。"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>建立 Azure 搜尋索引使用 hello REST API
> [!div class="op_single_selector"]
>
> * [概觀](search-what-is-an-index.md)
> * [入口網站](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

本文將逐步引導您建立 Azure 搜尋的 hello 程序[索引](https://docs.microsoft.com/rest/api/searchservice/Create-Index)使用 hello Azure 搜尋 REST API。

在按照本指南進行並建立索引錢，請先 [建立好 Azure 搜尋服務](search-create-service-portal.md)。

toocreate Azure 搜尋索引，使用 hello REST API，您將發行單一 HTTP POST 要求 tooyour Azure 搜尋服務的 URL 端點。 索引定義會包含在 hello 要求主體中，做為格式正確的 JSON 內容。

## <a name="identify-your-azure-search-services-admin-api-key"></a>識別 Azure 搜尋服務的系統管理 API 金鑰
既然您已佈建 Azure 搜尋服務，您可以發出對使用 hello REST API 服務的 URL 端點的 HTTP 要求。 *所有*API 要求中必須包含 hello api 金鑰 hello 您佈建的搜尋服務所產生。 擁有有效的索引鍵建立信任關係，針對每個要求，hello 應用程式正在傳送嗨要求和處理它的 hello 服務之間。

1. toofind 服務的 api 金鑰您必須登入 hello [Azure 入口網站](https://portal.azure.com/)
2. 移 tooyour Azure 搜尋服務的刀鋒視窗
3. 按一下 hello 「 金鑰 」 圖示

服務會有系統管理金鑰和查詢金鑰。

* 您的主要和次要*系統管理金鑰*tooall 作業，包括 hello 能力 toomanage hello 服務授與的完整權限、 建立和刪除索引、 索引子和資料來源。 有兩個索引鍵，讓您可以繼續 toouse hello 次要索引鍵，如果您決定 tooregenerate hello 主索引鍵，反之亦然。
* 您*查詢索引鍵*授與唯讀存取 tooindexes 和文件，並發出搜尋要求的 tooclient 通常分散式應用程式。

基於 hello 建立索引，您可以使用主要或次要管理金鑰。

## <a name="define-your-azure-search-index-using-well-formed-json"></a>使用正確格式的 JSON 定義 Azure 搜尋服務索引
單一 HTTP POST 要求 tooyour 服務將建立您的索引。 hello HTTP POST 要求主體會包含單一 JSON 物件，定義您的 Azure 搜尋索引。

1. hello 這個 JSON 物件的第一個屬性是 hello 索引名稱。
2. hello 這個 JSON 物件的第二個屬性是名為 JSON 陣列`fields`，其中包含您的索引中每個欄位個別的 JSON 物件。 每個 JSON 物件包含多個名稱/值組的 hello 欄位屬性，包括 「 名稱 」、 「 類型 」，每個等等。

很重要時，設計您的索引，因為每個欄位必須指派 hello 您搜尋的使用者經驗和商務需求謹記在心[適當屬性](https://docs.microsoft.com/rest/api/searchservice/Create-Index)。 這些屬性控制的搜尋功能 （篩選、 排序等全文檢索搜尋的 faceting） 套用 toowhich 欄位。 您沒有指定任何屬性，hello 預設值將是 tooenable hello 對應搜尋功能，除非您明確停用。

在我們的範例中，我們已將索引命名為 "hotels"，並將欄位定義如下：

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

我們已仔細選擇根據我們認為將用於應用程式的方式每個欄位的 hello 索引屬性。 例如，`hotelId`是唯一的索引鍵搜尋飯店可能不會知道，因此我們停用該欄位的全文檢索搜尋設定該人員`searchable`太`false`，以節省空間 hello 索引中。

請注意在類型的索引中剛好只有一個欄位`Edm.String`必須 hello 指定為 hello 'key' 欄位。

上述的 hello 索引定義會使用語言分析器 hello`description_fr`欄位，因為它是預定的 toostore 法文文字。 請參閱[hello 語言支援主題](https://docs.microsoft.com/rest/api/searchservice/Language-support)以及 hello 對應[部落格文章](https://azure.microsoft.com/blog/language-support-in-azure-search/)如需語言分析器的詳細資訊。

## <a name="issue-hello-http-request"></a>問題 hello HTTP 要求
1. 使用索引定義以 hello 要求主體，發出 HTTP POST 要求 tooyour Azure 搜尋服務端點 URL。 Hello URL 中是確定 toouse hello 主機名稱，為您的服務名稱，並將適當的 hello`api-version`做為查詢字串參數 (hello 目前的 API 版本是`2016-09-01`次發行本文件的 hello)。
2. 在 hello 要求標頭，指定 hello`Content-Type`為`application/json`。 您也需要 tooprovide 您的服務管理金鑰，您在步驟 1 所識別在 hello`api-key`標頭。

您必須 tooprovide 自己服務名稱和 api 金鑰 tooissue hello 要求如下：

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


若要求成功，您應該會看到狀態碼 201 (已建立)。 如需有關建立 hello REST API 透過索引的詳細資訊，請瀏覽 hello[這裡 API 參考](https://docs.microsoft.com/rest/api/searchservice/Create-Index)。 如需失敗時可能傳回的其他 HTTP 狀態碼詳細資訊，請參閱 [HTTP 狀態碼 (Azure 搜尋服務)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes)。

當您完成時具有索引，且想 toodelete 它時，就會發出 HTTP DELETE 要求。 比方說，這是我們會 delete hello 「 旅館"索引的方式：

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>後續步驟
建立 Azure 搜尋索引之後, 您就可以開始太[將內容上傳到 hello 索引](search-what-is-data-import.md)這樣就可以搜尋您的資料。
