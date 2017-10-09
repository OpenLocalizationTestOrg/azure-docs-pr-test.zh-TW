---
title: "aaaQuery Azure 搜尋索引 |Microsoft 文件"
description: "建置在 Azure 搜尋的搜尋查詢，並使用搜尋參數 toofilter 和排序搜尋結果。"
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>查詢 Azure 搜尋服務索引
> [!div class="op_single_selector"]
> * [概觀](search-query-overview.md)
> * [入口網站](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

提交時搜尋要求 tooAzure 搜尋，有幾個可以與 hello hello 應用程式的搜尋方塊中輸入的實際文字一起指定的參數。 這些查詢參數可讓您 tooachieve hello 某些更深入控制[全文檢索搜尋經驗](search-lucene-query-architecture.md)。

以下是簡短說明常見的用法，在 Azure 搜尋中的 hello 查詢參數的清單。 涵蓋的查詢參數和其行為的完整範圍，請參閱 hello 詳細 hello 頁面[REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)和[.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary)。

## <a name="types-of-queries"></a>查詢類型
Azure 搜尋會提供許多選項 toocreate 極為強大的查詢。 hello 兩個主要的查詢將使用的類型是`search`和`filter`。 A`search`查詢中所有的一或多個詞彙搜尋*可搜尋*在索引中，欄位 hello 方式與您希望像 Google 或 Bing toowork 搜尋引擎。 `filter` 查詢可跨索引的所有可篩選欄位評估布林運算式。 不同於`search`查詢`filter`查詢比對欄位，這表示它們會區分大小寫的字串欄位的 hello 確切內容。

您可以同時或個別使用搜尋和篩選。 如果您同時使用它們，則 hello 篩選套用第一個 toohello 整個索引，而且然後 hello 搜尋 hello hello 篩選結果上。 篩選因此可能會很有用的技巧 tooimprove 查詢效能，因為會減低 hello 組 hello 搜尋查詢需求 tooprocess 的文件。

hello 的篩選條件運算式的語法是 hello 子集[OData 篩選器語言](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)。 搜尋查詢中，您可以使用任一 hello[簡化語法](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)或 hello [Lucene 的查詢語法](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search)下面會討論。

### <a name="simple-query-syntax"></a>簡單查詢語法
hello[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)hello Azure 搜尋中所使用的預設查詢語言。 hello 簡單查詢語法支援許多常用的搜尋運算子包括 hello AND、 OR、 NOT、 片語、 後置詞，以及優先順序運算子。

### <a name="lucene-query-syntax"></a>Lucene 查詢語法
hello [Lucene 的查詢語法](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search)廣為採用 toouse hello 和表示查詢語言開發的一部分，可讓您[Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html)。

使用此查詢語法可讓您 tooeasily 達到 hello 下列功能：[欄位範圍查詢](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields)，[模糊搜尋](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy)，[鄰近搜尋](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity)， [詞彙提升](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost)，[規則運算式搜尋](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex)，[萬用字元搜尋](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard)，[語法基礎](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax)，和[查詢使用布林運算子](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean)。

## <a name="ordering-results"></a>排序結果
在接收時搜尋查詢的結果，您可以要求 Azure 搜尋做 hello 結果依特定欄位中的值。 根據預設，Azure 搜尋訂單 hello 搜尋結果，根據每份文件的搜尋分數衍生自 hello 陣序[TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)。

如果您希望 Azure 搜尋 tooreturn hello 搜尋分數以外的值來排序您的結果，您可以使用 hello`orderby`搜尋參數。 您可以指定 hello hello 值`orderby`參數 tooinclude 欄位名稱，並呼叫 toohello [ `geo.distance()`函式](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)地理空間值。 每個運算式後面可以接著`asc`tooindicate 結果會以遞增順序，要求並`desc`tooindicate 結果會以遞減順序要求。 hello 預設排名遞增的順序。

## <a name="paging"></a>分頁
Azure 搜尋可讓您輕鬆 tooimplement 搜尋結果的分頁。 使用 hello`top`和`skip`參數，您可以順暢地發出搜尋要求，可讓您 tooreceive hello 一整組搜尋結果中輕鬆地啟用良好搜尋 UI 作法的可管理、 已排序的子集。 當接收這些結果的較小的子集，也可以在收到 hello 的文件計數的搜尋結果的 hello 總集合中。

您可以進一步了解分頁 hello 文件中的搜尋結果[toopage 搜尋在 Azure 搜尋的結果如何](search-pagination-page-layout.md)。

## <a name="hit-highlighting"></a>搜尋結果醒目提示
在 Azure 搜尋中，強調 hello 確切部分符合 hello 搜尋查詢的搜尋結果更容易使用 hello `highlight`， `highlightPreTag`，和`highlightPostTag`參數。 您可以指定哪些*可搜尋*欄位應該有其相符的文字，以及指定傳回正確字串標記 tooappend toohello 開始及結尾 hello 比對文字 Azure 搜尋的 hello 反白。

## <a name="try-out-query-syntax"></a>嘗試執行查詢語法

hello 最佳方式 toounderstand 語法差異是所送出查詢並檢視結果。

+ 使用[搜尋總管](search-explorer.md)hello Azure 入口網站中。 藉由部署[hello 範例索引](search-get-started-portal.md)，您可以查詢 hello 索引以分鐘為單位使用 hello 入口網站中的工具。

+ 使用[Fiddler](search-fiddler.md)或 Chrome 郵差 toosubmit 查詢 tooan 索引已上傳 tooyour 搜尋服務。 這兩個工具支援 REST 呼叫 tooan HTTP 端點。 
