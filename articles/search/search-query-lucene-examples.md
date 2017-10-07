---
title: "Azure 搜尋 aaaLucene 查詢範例 |Microsoft 文件"
description: "模糊搜尋、鄰近搜尋、詞彙提升、規則運算式搜尋與萬用字元搜尋的 Lucene 查詢語法。"
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>在 Azure 搜尋服務中建置查詢的 Lucene 查詢語法範例
當 Azure 搜尋建構查詢，您可以使用任一 hello 預設[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)或 hello 替代[Lucene 查詢剖析器，在 Azure 搜尋](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)。 hello Lucene 查詢剖析器支援更複雜的查詢建構，例如欄位範圍查詢、 模糊的搜尋、 鄰近搜尋、 詞彙來提升，和規則運算式搜尋。

在本文中，您可以逐步執行範例，示範可用的查詢作業時使用 hello 完整的語法。

## <a name="viewing-hello-examples-in-jsfiddle"></a>檢視 JSFiddle hello 範例

所有的這篇文章中的 hello 範例會針對預先載入的搜尋索引中執行的可執行查詢[JSFiddle](https://jsfiddle.net)，測試指令碼和 HTML 的線上的程式碼編輯器。 

toorun 它們，以滑鼠右鍵按一下 hello 查詢範例 Url tooopen JSFiddle 另一個瀏覽器視窗中。

> [!NOTE]
> hello 下列範例會利用根據 hello 所提供的資料集的可用工作所組成的搜尋索引[縣 （市） 的 New York 開放式資料](https://nycopendata.socrata.com/)開發案。 這項資料不應視為目前的或已完成。 hello 索引是在由 Microsoft 提供沙箱服務。 您不需要 Azure 訂用帳戶或 Azure 搜尋 tootry 這些查詢。
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Tooinvoke 完整 Lucene 剖析

所有的這篇文章中的 hello 範例指定 hello **queryType = 完整**搜尋參數，指出該 hello 完整語法，由 hello Lucene 查詢剖析器。 

**範例 1** --下列查詢程式碼片段 tooopen 在新的瀏覽器頁面上，以滑鼠右鍵按一下 hello 載入 JSFiddle 和執行 hello 查詢：

* [&queryType=full&search=*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

在 hello 新瀏覽器視窗中，會並排顯示 hello JavaScript 來源和 HTML 的輸出。 hello 指令碼參考完整的查詢 （不只是 hello 程式碼片段，hello 連結中所示）。 hello 完整查詢所示，每個範例 Url 的 hello。 

此查詢會從紐約市工作索引 (在沙箱服務上載入的 nycjobs) 傳回文件。 為求簡潔，hello 查詢會指定只有商務標題會傳回。 hello 完整的基礎查詢如下所示：

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

hello **searchFields**參數會限制 hello 搜尋 toojust hello 商務標題 欄位。 hello **queryType**設定得**完整**，它會指示此查詢的 Azure 搜尋 toouse hello Lucene 查詢剖析器。

> [!NOTE]
> 如需有關查詢處理的背景知識，請參閱[全文檢索搜尋如何在 Azure 搜尋服務中運作](search-lucene-query-architecture.md)。 如需搜尋參數的詳細資訊，請參閱 [Search Documents (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) (搜尋文件 (Azure 搜尋服務 REST API))。
>

### <a name="fielded-query-operation"></a>加入欄位的查詢作業
您可以修改本文中的 hello 範例藉由指定**fieldname:searchterm**建構 toodefine 擁有查詢作業，其中 hello 欄位是一個字使用，而 hello 搜尋詞彙也是一個單字或片語，選擇性地具有布林運算子。 一些範例包括 hello 下列：

* business_title:(senior NOT junior)
* state:("New York" AND "New Jersey")

如果您想要評估為單一實體，如同在此案例中搜尋 hello 位置 欄位中的兩個不同城市的這兩個字串 toobe，會確定 tooput 引號內的多個字串。 此外，請確定您看到使用 NOT 而大寫 hello 運算子和 and。

中指定的 hello 欄位**fieldname:searchterm**必須是可搜尋的欄位。 如需欄位定義中索引屬性使用方式的詳細資訊，請參閱 [建立索引 (Azure 搜尋服務 REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) 。

**範例 2** -以滑鼠右鍵按一下 hello 下列查詢的程式碼片段以 hello 的商務標題的搜尋詞彙資深，但不是資歷較淺這個查詢：

* [&queryType=full&search= business_title:senior NOT junior](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>模糊搜尋範例
模糊搜尋會尋找具有類似建構的相符項目。 在每個 [Lucene 文件](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html)中，模糊搜尋以 [Damerau-Levenshtein 距離](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance)為基礎。

toodo 模糊的搜尋，附加 hello 波狀符號"~"hello 與選擇性參數，指定 hello 編輯距離的值介於 0 到 2，單一文字的結尾處的符號。 比方說，"blue~" 或 "blue~1" 會傳回 blue、blues 和 glue。

**範例 3** -以滑鼠右鍵按一下 hello 下列查詢程式碼片段。 此查詢會搜尋具有 hello 詞彙關聯 （其中它拼字錯誤） 的工作：

* [&queryType=full&search= business_title:asosiate~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> 不會[分析](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis)模糊查詢，如果您預期詞幹分析或詞形歸併還原，可能會對此感到意外。 只能對完整詞彙執行語彙分析 (詞彙查詢或片語查詢)。 查詢類型不完整的條款 （前置詞的查詢、 萬用字元查詢、 regex 查詢、 模糊的查詢） 會加入直接 toohello 查詢樹狀目錄中，略過 hello 分析階段。 hello 對不完整的查詢詞彙的轉換為大寫。
>

## <a name="proximity-search-example"></a>鄰近搜尋範例
鄰近搜尋都是使用的 toofind 詞彙的文件中會彼此的附近。 插入波狀符號"~"片語的 hello 結尾符號後面建立 hello 相近界限的字組的 hello 數目。 例如，「 旅館機場"~ 5 會在文件中找到 hello 條款旅館和機場內彼此的 5 個字組。

**範例 4** -以滑鼠右鍵按一下 hello 查詢。 搜尋具有 hello 詞彙"資深分析師 」 工作分隔由不超過一個單字：

* [&queryType=full&search=business_title:"senior analyst"~1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**範例 5** -試試看吧再次移除 hello 詞彙"資深分析師 」 之間的 hello 文字。

* [&queryType=full&search=business_title:"senior analyst"~0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>提升詞彙範例
詞彙來提升是指的 tooranking 文件更高版本，如果它包含 hello 促進式相對 toodocuments 不含 hello 詞彙的詞彙。 這與評分設定檔的不同之處在於評分設定檔會提升特定欄位，而不是特定詞彙。 下列範例可協助說明 hello 差異 hello。

請考慮提升的計分設定檔符合的特定欄位中，例如**類型**hello musicstoreindex 範例中。 詞彙來提升可能是使用的 toofurther boost 特定搜尋詞彙高於其他人。 例如，"rock ^2 電子 」 將有助於提升包含 hello hello 搜尋詞彙的文件**內容類型**高於其他可搜尋的欄位 hello 索引中的欄位。 此外，文件包含 hello 搜尋詞彙"rock"排列次序 hello 高於其他搜尋詞彙"electronic"hello 詞彙增量值 (2) 的結果。

詞彙，使用 hello 插入號，tooboost"^"，在您要搜尋的 hello 詞彙的 hello 結尾處的提升係數 （數字） 使用符號。 hello 較高的 hello 提升係數，hello 更有相關性的 hello 詞彙會相對 tooother 搜尋詞彙。 根據預設，hello 提升係數是 1。 雖然 hello 提升係數必須是正數，它可能會小於 1 （例如 0.2）。

**範例 6** -以滑鼠右鍵按一下 hello 查詢。 搜尋具有 hello 詞彙 「 電腦分析師 」，我們看到沒有字電腦和分析師、 結果尚未分析師的工作會在 hello 結果 hello 最上方工作。

* [&queryType=full&search=business_title:computer analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**範例 7** -再試一次，此時間來提升結果與 hello 詞彙電腦透過 hello 詞彙分析師如果這兩個字都不存在。

* [&queryType=full&search=business_title:computer^2 analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>規則運算式範例
規則運算式搜尋會尋找相符項目根據 hello 內容之間正斜線"/"，為文件中的 hello [RegExp 類別](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html)。

**範例 8** -以滑鼠右鍵按一下 hello 查詢。 搜尋與 hello 詞彙資深或 Junior 的工作。

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

此範例中的 hello URL 不會正確呈現在 hello 頁面中。 因應措施，複製下列 hello URL 並將它貼到 hello 瀏覽器 URL 位址：`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>萬用字元搜尋範例
您可以使用一般辨識語法進行多個 (\*) 或單一 (?) 字元的萬用字元搜尋。 請注意 hello Lucene 查詢剖析器支援 hello 使用這些符號與單一詞彙，並不是一個片語。

**範例 9** -以滑鼠右鍵按一下 hello 查詢。 搜尋包含 hello 前置詞 'prog' 會包括商務標題程式設計的 hello 條款及程式設計師中的工作。

* [&queryType=full&$select=business_title&search=business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

您無法使用 * 或 ? hello 搜尋第一個字元的符號。

## <a name="next-steps"></a>後續步驟
請嘗試在程式碼中指定 hello Lucene 查詢剖析器。 下列連結查看 hello 說明適用於.NET 和 REST API hello tooset 增加搜尋查詢的方式。 hello 連結使用 hello 預設簡單的語法，因此，您必須從這個發行項 toospecify hello 學 tooapply **queryType**。

* [查詢您使用 hello.NET SDK 的 Azure 搜尋索引](search-query-dotnet.md)
* [查詢您使用 hello REST API 的 Azure 搜尋索引](search-query-rest-api.md)

## <a name="see-also"></a>另請參閱

 [全文檢索搜尋如何在 Azure 搜尋服務中運作](search-lucene-query-architecture.md)