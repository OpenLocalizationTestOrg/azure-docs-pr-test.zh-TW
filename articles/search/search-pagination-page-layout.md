---
title: "在 Azure 搜尋的 aaaHow toopage 搜尋結果 |Microsoft 文件"
description: "Azure 搜尋服務 (Microsoft Azure 上之託管的雲端搜尋服務) 中的分頁方式。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>在 Azure 搜尋 toopage 搜尋結果的方式
這篇文章會提供有關如何 toouse hello Azure 搜尋服務 REST API tooimplement 標準的項目搜尋結果頁面上，例如的總次數、 文件擷取、 排序次序和瀏覽的指引。

在每個案例中，如下所述，提供資料或資訊 tooyour 搜尋結果頁面的頁面的相關選項透過 hello 指定[搜尋文件](http://msdn.microsoft.com/library/azure/dn798927.aspx)傳送要求 tooyour Azure 搜尋服務。 要求包含 GET 命令、 路徑和 hello 服務要求功能，就會通知的查詢參數和 tooformulate hello 回應的方式。

> [!NOTE]
> 有效的要求包含一些項目，例如服務 URL 及路徑、HTTP 動詞命令、`api-version` 等。 為求簡單明瞭，我們會修剪 hello 範例 toohighlight 只 hello 語法相關 toopagination。 請參閱 hello [Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx)要求語法的詳細文件。
> 
> 

## <a name="total-hits-and-page-counts"></a>總點擊數和頁面計數
顯示 hello 總查詢，傳回的結果數目，然後傳回結果較小的區塊，是基本 toovirtually 所有搜尋頁面。

![][1]

在 Azure 搜尋中，您可以使用 hello `$count`， `$top`，和`$skip`參數 tooreturn 這些值。 hello 下列範例顯示的範例要求的總叫用，以傳回`@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

擷取 15，群組中的文件，也會顯示 hello 的點擊總數，開始 hello 第一頁：

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

分頁結果同時需要`$top`和`$skip`，其中`$top`批次中指定數目的項目 tooreturn 和`$skip`指定數目的項目 tooskip。 在 hello 遵循範例中，每一頁會顯示 hello 接下來 15 的項目，以表示 hello 累加式跳躍點在 hello`$skip`參數。

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>版面配置
在搜尋結果 頁面中，您可能想 tooshow 縮圖影像、 欄位、 的子集，以及連結 tooa 完整產品頁面。

 ![][2]

在 Azure 搜尋中，您會使用`$select`和查閱命令 tooimplement 這項體驗。

tooreturn 子集並排顯示版面配置的欄位：

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

映像和媒體檔案不是直接搜尋，並應該儲存在另一個存放裝置平台，例如 Azure Blob 儲存體，tooreduce 成本。 在 hello 索引和文件中，定義會儲存 hello hello 外部內容的 URL 地址的欄位。 您接著可以使用 hello 欄位做為映像的參照。 hello URL toohello 映像應該 hello 文件中。

產品說明頁面的 tooretrieve **onClick**事件時，使用[查閱文件](http://msdn.microsoft.com/library/azure/dn798929.aspx)toopass hello 文件 tooretrieve hello 索引鍵中的。 hello hello 索引鍵資料類型是`Edm.String`。 在此範例中為 *246810*。 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>根據相關性、評等或價格排序
排序通常順序預設 toorelevance，但它是一般 toomake 替代排序次序便於使用，讓客戶可以快速地為不同的次序順序 reshuffle 現有的結果。

 ![][3]

在 Azure 搜尋中，會根據排序 hello`$orderby`運算式，會與編製索引的所有欄位`"Sortable": true.`

相關性和評分設定檔密切相關。 您可以使用預設計分 hello，它會依賴文字分析和統計資料 toorank 順序所有結果，使用較高 toodocuments 的更多或更強的相符項目進行的搜尋詞彙的分數。

替代的排序順序通常與相關聯**onClick**回 tooa 方法會呼叫的事件建立 hello 排序順序。 例如指定頁面項目如下：

 ![][4]

您會建立接受 hello 選取排序選項做為輸入，並傳回該選項相關聯的 hello 準則的已排序的清單的方法。

 ![][5]

> [!NOTE]
> 雖然 hello 預設計分足以適用許多情況，我們建議您改為基礎的自訂計分設定檔的相關性。 自訂的計分設定檔可讓您更有幫助 tooyour 商務方式 tooboost 項目。 如需詳細資訊，請參閱 [新增評分設定檔](http://msdn.microsoft.com/library/azure/dn798928.aspx) 。 
> 
> 

## <a name="faceted-navigation"></a>多面向導覽
在 [結果] 頁面中，通常位於 hello 側邊或上方頁面上搜尋巡覽常會。 在 Azure 搜尋服務中，多面向導覽會根據預先定義的篩選器提供自我導向的搜尋。 如需詳細資訊，請參閱 [Azure 搜尋服務中的多面向導覽](search-faceted-navigation.md) 。

## <a name="filters-at-hello-page-level"></a>Hello 頁面層級篩選
如果您解決方案設計包含特定類型的內容 （例如，線上零售應用程式已列在 hello hello 頁面頂端的部門） 的專用的搜尋頁面中，您可以插入旁邊的篩選條件運算式**onClick**事件 tooopen 預先狀態中的頁面。 

您可以傳送篩選器，但不一定要有搜尋運算式。 例如，hello 下列要求會篩選品牌名稱，傳回符合這些文件。

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

如需 `$filter` 運算式的詳細資訊，請參閱[搜尋文件 (Azure 搜尋服務 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)。

## <a name="see-also"></a>另請參閱
* [Azure 搜尋服務 REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [索引作業](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [文件作業](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Azure 搜尋服務的影片和教學課程](search-video-demo-tutorial-list.md)
* [Azure 搜尋服務中的多面向導覽](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
