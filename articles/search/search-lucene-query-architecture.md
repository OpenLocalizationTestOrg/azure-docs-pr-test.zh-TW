---
title: "在 Azure 搜尋 aaaFull 文字搜尋引擎 (Lucene) 架構 |Microsoft 文件"
description: "說明 Lucene 查詢處理和文件擷取概念的全文檢索搜尋中，為相關 tooAzure 搜尋。"
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>全文檢索搜尋如何在 Azure 搜尋服務中運作

本文適用於需要更深入了解 Lucene 全文檢索搜尋在 Azure 搜尋服務中運作方式的開發人員。 針對文字查詢，Azure 搜尋服務在大部分情況下會順暢地提供預期的結果，但您偶爾可能會收到看起來像以某種方式「關閉」的結果。 在這些情況下，在具有背景 hello Lucene 查詢執行的四個階段 （查詢剖析語彙分析、 文件比對，計分） 可協助您識別特定變更 tooquery 參數或索引將會傳送 hello 的組態所要的結果。 

> [!Note] 
> Azure 搜尋服務會使用 Lucene 來進行全文檢索搜尋，但 Lucene 整合並不詳盡。 我們可以選擇性地公開 （expose） 和擴充 Lucene 功能 tooenable hello 案例重要 tooAzure 搜尋。 

## <a name="architecture-overview-and-diagram"></a>架構概觀和圖表

處理全文檢索搜尋查詢以剖析 hello 查詢文字 tooextract 搜尋詞彙為開頭。 hello 搜尋引擎會使用索引 tooretrieve 文件與比對的詞彙。 個別的查詢詞彙有時細分並重新組成新表單 toocast 到更廣泛的網路上項目可以視為可能的相符項目。 依相關性分數指派的 tooeach 個別比對文件，然後進行排序結果集。 這些在 hello hello 排名清單最上方會傳回 toohello 呼叫的應用程式。

重新敘述的查詢執行有四個階段︰ 

1. 查詢剖析 
2. 語彙分析 
3. 擷取文件 
4. 評分 

hello 圖說明 hello 用元件 tooprocess 搜尋要求。 

 ![Azure 搜尋服務中的 Lucene 查詢架構圖表][1]


| 重要元件 | 功能描述 | 
|----------------|------------------------|
|**查詢剖析器** | 分開查詢運算子的查詢詞彙，並建立 hello 查詢結構 （查詢樹狀結構） 傳送 toobe toohello 搜尋引擎。 |
|**分析器** | 執行查詢詞彙的語彙分析。 此程序可能包含轉換、移除或展開查詢詞彙。 |
|**Index** | 有效率的資料結構使用 toostore 和組織可搜尋索引文件從擷取的詞彙。 |
|**搜尋引擎** | 擷取和比對的 hello hello 內容為基礎的文件的分數反向索引。 |

## <a name="anatomy-of-a-search-request"></a>搜尋要求的剖析

搜尋要求是結果集所需傳回的完整規格。 最簡單的形式中，它是不設任何類型之條件的空查詢。 更真實的範例包含參數，數個查詢詞彙中，可能是已設定領域的 toocertain 欄位，可能是篩選條件運算式和排序規則。  

hello 下列範例會搜尋要求，您可能會傳送 tooAzure 搜尋使用 hello [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)。  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

此要求，hello 搜尋引擎沒有 hello 遵循：

1. 篩選出 hello 價格為至少 $60 和小於 $300 文件。
2. 執行 hello 查詢。 在此範例中，hello 搜尋查詢所組成片語和詞彙： `"Spacious, air-condition* +\"Ocean view\""` (使用者通常不輸入標點符號，但是包含在 hello 範例可讓我們 tooexplain 分析器如何處理它)。 對於此查詢，hello 搜尋引擎掃描 hello 描述，並在指定的標題欄位`searchFields`包含 「 Ocean 檢視 」 的文件和此外 hello 詞彙"寬廣"，或在以 hello 前置詞開頭的項目上 「 air-condition"。 hello`searchMode`參數 （預設值） 的任何詞彙或所有項目，其中詞彙是不需要明確的案例是使用的 toomatch (`+`)。
3. 訂單所指定的地理位置，然後傳回 toohello 呼叫的應用程式的鄰近 tooa hello 旅館的結果集。 

hello 大部分的這篇文章是關於處理 hello*搜尋查詢*: `"Spacious, air-condition* +\"Ocean view\""`。 篩選和排序不在範圍內。 如需詳細資訊，請參閱 hello[搜尋 API 參考文件](https://docs.microsoft.com/rest/api/searchservice/search-documents)。

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>第 1 階段︰查詢剖析 

如前所述，hello 查詢字串，則 hello hello 要求第一行： 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

hello 查詢剖析器分隔運算子 (例如`*`和`+`hello 範例中) 從搜尋詞彙，並將解構 hello 搜尋查詢*子查詢*支援的類型： 

+ 詞彙查詢適用於獨立詞彙 (例如 spacious)
+ 片語查詢適用於引號括住的詞彙 (例如 ocean view)
+ 前置詞查詢適用於前置詞運算子後面的詞彙 `*` (例如 air-condition)

如需支援的查詢類型完整清單，請參閱 [Lucene 查詢語法](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

子查詢相關聯的運算子決定 hello 查詢 「 必須 」 或 「 應該 」 文件順序滿足 toobe 視為相符。 例如， `+"Ocean view"` 「 必須 」 到期 toohello`+`運算子。 

hello 查詢剖析器的重建 hello 子查詢至*查詢樹狀結構*toohello 搜尋引擎上傳遞 （代表 hello 查詢的內部結構）。 在剖析查詢的第一個階段中 hello，hello 查詢樹狀結構看起來像這樣。  

 ![Boolean query searchmode any][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>支援的剖析器︰簡單和完整的 Lucene 

 Azure 搜尋服務會公開兩種不同的查詢語言，`simple` (預設值) 和 `full`。 所設定的 hello`queryType`參數與您的搜尋要求，您可告知 hello 查詢剖析器的查詢語言您選擇，讓它知道如何 toointerpret hello 運算子和語法。 hello[簡單的查詢語言](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)憑直覺強固、 通常適合 toointerpret 使用者輸入為-沒有用戶端處理。 它支援 web 搜尋引擎熟悉的查詢運算子。 hello[完整 Lucene 的查詢語言](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)，您會取得藉由設定`queryType=full`，藉由新增更多的運算子與類萬用字元，模糊的查詢類型，regex 和欄位範圍查詢的支援延伸 hello 預設簡單的查詢語言。 例如，簡單查詢語法傳入的規則運算式會解譯為查詢字串而非運算式。 本文章中的 hello 範例要求會使用 hello 完整 Lucene 的查詢語言。

### <a name="impact-of-searchmode-on-hello-parser"></a>受 searchMode hello 剖析器上的影響 

另一個搜尋要求參數，會影響剖析為 hello`searchMode`參數。 它所控制的布林值的查詢 hello 預設運算子： 任何 （預設值），或全部。  

當`searchMode=any`，是 hello 預設，hello 空間分隔符號之間寬廣，air-condition 為或者 (`||`)，讓文字 hello 範例查詢相當於： 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

明確運算子，例如`+`中`+"Ocean view"`，會在布林查詢建構模稜兩可 (hello 詞彙*必須*符合)。 較不明顯是 toointerpret hello 剩餘如何條款： 寬廣和 air-condition。 應該 hello 搜尋引擎尋找相符項目上海景*和*寬廣*和*air-condition 嗎？ 它應該會發現海景或加上*其中一個*的 hello 剩餘條款？ 

根據預設 (`searchMode=any`)，hello 搜尋引擎假設 hello 更廣泛的解譯方式。 任一個欄位應該相符，反映「或」語意。 hello 初始查詢樹狀結構之前，使用說明 hello 兩個 「 應該 」 作業，會顯示 hello 預設值。  

假設我們現在設定 `searchMode=all`。 在此情況下，hello 空格會解譯為 「 和 」 作業。 每個 hello 其餘條款必須同時出現在 hello 文件 tooqualify 為相符項目。 hello 產生的範例查詢會解譯，如下所示： 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

修改過的查詢樹狀結構，此查詢會，如下所示，比對文件所在的所有三個的子查詢的 hello 交集： 

 ![Boolean query searchmode all][3]

> [!Note] 
> 透過 `searchMode=all` 選擇 `searchMode=any` 是藉由執行具代表性之查詢所得出的最佳決策。 可能的 tooinclude 運算子 （一般搜尋文件會儲存時） 的使用者可能會發現結果更具直覺性如果`searchMode=all`通知布林查詢建構。 如需詳細資訊之間的 hello 相互作用`searchMode`和運算子，請參閱[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)。

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>第 2 階段：語彙分析 

語彙分析器程序*詞彙查詢*和*片語查詢*hello 查詢樹狀結構的結構之後。 分析器接受 hello 文字輸入指定 tooit hello 剖析器、 處理序 hello 文字，並再傳送回語彙基元化的詞彙 toobe 併入 hello 查詢樹狀結構。 

hello 語彙分析最常見形式是*語言分析*的轉換規則的特定 tooa 給定語言為基礎的查詢字詞： 

* 減少查詢詞彙 toohello 根形式的文字 
* 移除不必要的字 (停用字詞，例如英文的 "the" 或 "and") 
* 將複合字分成多個組件元件 
* 將大寫的字改成小寫 

所有這些作業通常 tooerase hello 使用者與 hello 詞彙儲存在 hello 索引所提供的 hello 文字輸入之間的差異。 這類作業超出文字處理，而且需要深入了解 hello 語言本身。 tooadd 這層的語言感知，Azure 搜尋支援一長串[語言分析器](https://docs.microsoft.com/rest/api/searchservice/language-support)Lucene 和 Microsoft。

> [!Note]
> 分析需求的範圍從最小 tooelaborate 根據您的案例。 您可以控制語彙分析的複雜性，選取其中一個預先定義的 hello 分析器 hello 或建立您自己[自訂分析器](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search)。 分析器是已設定領域的 toosearchable 欄位和欄位定義中指定。 這可讓您 toovary 語彙分析每個欄位為基礎。 未指定，hello*標準*Lucene 分析器 的用途。

在我們的範例，先前的 tooanalysis hello 初始查詢樹狀結構有 hello 詞彙"Spacious，「 以大寫的"S"和逗號的 hello 查詢剖析器會解譯為 hello 查詢字詞 （逗號不被視為查詢語言運算子） 的一部分。  

Hello 預設分析器處理 hello 詞彙時，它將小寫"海景"和"寬廣 」，並移除 hello 逗號字元。 hello 修改過的查詢樹狀結構會看起來像這樣： 

 ![包含分析過詞彙的布林值查詢][4]

### <a name="testing-analyzer-behaviors"></a>測試分析器的行為 

可以使用 hello 測試分析器的 hello 行為[分析 API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer)。 提供您想要指定分析器哪些詞彙將會產生 tooanalyze toosee 的 hello 文字。 例如，toosee hello 標準分析器會處理如何 hello 文字"air-condition 」，您可以發出下列要求的 hello:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

hello 標準分析器會分成下列兩個語彙基元，這些註解的屬性，例如開始和結束位移 （用來叫用的反白顯示），以及它們的位置 （用來比對片語） hello hello 輸入的文字：

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>例外狀況 toolexical 分析 

語彙分析適用於需要完整條款 – 查詢詞彙或片語查詢 tooquery 型別。 它不會套用 tooquery 類型不完整的條款-前置詞的查詢、 萬用字元查詢、 regex 查詢或 tooa 模糊查詢。 這些查詢類型，包括 hello 與詞彙的前置詞查詢*air-condition\** 在本例中，加入直接 toohello 查詢樹狀目錄中，略過 hello 分析階段。 hello 對這些類型的查詢詞彙的轉換為大寫。

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>第 3 階段：擷取文件 

文件擷取指的是 toofinding hello 索引中的相符詞彙的文件。 了解這個階段的最佳方式就是範例。 讓我們開始與旅館索引具有下列簡單的結構描述的 hello: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

進一步假設這個索引包含下列四個文件的 hello: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**詞彙編製索引的方式**

它可協助 tooknow toounderstand 擷取有關編製索引的幾個基本概念。 儲存體 hello 單位是反向的索引，一個用於每個可搜尋的欄位。 反向索引內會有所有文件中所有詞彙的排序清單。 每個詞彙對應 toohello 發生，以下的 hello 範例中為明顯的文件清單。

tooproduce hello 詞彙在反向索引中，hello 搜尋引擎執行語彙分析 hello 文件內容，透過類似 toowhat 查詢處理期間進行的作業。 文字輸入傳遞 tooan 分析器 中，較低的大小寫慣例，除去標點符號及其他等等，根據 hello 的分析器組態。 它是不常見，但並非必要，toouse hello 相同分析器搜尋和索引作業，讓查詢詞彙起來更 hello 索引內的詞彙。

> [!Note]
> Azure 搜尋服務可讓您指定不同的分析器來編製索引，並透過其他的 `indexAnalyzer` 和 `searchAnalyzer` 欄位參數進行搜尋。 如果未指定，hello 分析器設定以 hello`analyzer`屬性用於索引和搜尋。  

**範例文件的反向索引**

傳回 tooour 範例中的，針對 hello**標題** 欄位中，反轉 hello 索引看起來像這樣：

| 詞彙 | 文件清單 |
|------|---------------|
| atman | 1 |
| beach | 2 |
| hotel | 1, 3 |
| ocean | 4  |
| playa | 3 |
| resort | 3 |
| retreat | 4 |

Hello 標題 欄位中，只有*旅館*出現兩份文件： 1、 3。

Hello**描述** 欄位中，hello 索引如下所示：

| 詞彙 | 文件清單 |
|------|---------------|
| air | 3
| 和 | 4
| beach | 1
| conditioned | 3
| comfortable | 3
| distance | 1
| island | 2
| kauaʻi | 2
| located | 2
| north | 2
| ocean | 1, 2, 3
| of | 2
| on |2
| quiet | 4
| rooms  | 1, 3
| secluded | 4
| shore | 2
| spacious | 1
| hello | 1、2
| 太| 1
| view | 1, 2, 3
| walking | 1
| 取代為 | 3


**比對查詢詞彙與索引的詞彙**

指定上述 hello 反轉索引，讓我們傳回 toohello 範例查詢並查看如何比對文件找到範例查詢。 前文提過該 hello 最終查詢樹狀結構看起來像這樣： 

 ![包含分析過詞彙的布林值查詢][4]

執行查詢時，個別的查詢會針對執行 hello 可搜尋的欄位獨立。 

+ hello TermQuery"寬廣"會比對文件 1 (旅館 Atman)。 

+ hello PrefixQuery，"air-condition *"，不符合任何文件。 

  這個行為有時候會混淆開發人員。 雖然 air-conditioned hello 詞彙存在 hello 文件中，它是分割成兩個詞彙 hello 預設解析程式。 還記得包含部分詞彙的前置詞查詢不會進行分析。 因此具有前置詞"air-condition 」 中查閱 hello 條款反向索引，但找不到。

+ hello PhraseQuery 「 ocean 檢視 」 查閱 hello 條款 」 ocean 」 和 「 檢視 」，並檢查 hello 相近的 hello 原始文件中的詞彙。 文件 1、 2 和 3 符合這個 hello 描述欄位中的查詢。 請注意文件 4 有 hello 標題中的 hello 詞彙 ocean，但不視為相符項目，因為我們想要尋求 hello"海景"片語，而不是個別文字。 

> [!Note]
> 搜尋查詢針對 hello Azure 搜尋索引，除非您限制設定以 hello hello 欄位中的所有可搜尋欄位單獨執行`searchFields`參數 hello 範例搜尋要求中所示。 傳回符合任何選取的 hello 欄位中的文件。 

Hello 整個 hello 查詢有問題，在比對的 hello 文件會是 1、 2、 3。 

## <a name="stage-4-scoring"></a>第 4 階段︰評分  

會將相關性分數指派給搜尋結果集中的每個文件。 hello 相關性分數的 hello 函式是 toorank 更高版本，這些文件最佳回答使用者問題所表示的 hello 搜尋查詢。 hello 分數會根據比對的詞彙的統計屬性來計算的。 Hello hello 計分公式的核心是[TF IDF （「 詞彙頻率反向的文件頻率）](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)。 在查詢中包含少數且常見的詞彙，TF/IDF 升級包含 hello 罕見詞彙的結果。 例如，在所有的維基百科文章假設索引中，從文件相符的 hello 查詢*hello 總統*、 比對文件*總統*會被視為比更有相關性比對文件。


### <a name="scoring-example"></a>評分範例

前文提過 hello 三份文件符合我們的範例查詢：
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

最佳記錄 1 個相符的 hello 查詢，因為兩者 hello 詞彙*寬廣*與 hello 必要的片語*海景*發生 hello 描述欄位中。 hello 下面兩個文件符合只 hello 片語*海景*。 它可能會意外該 hello 相關性分數 2 和 3 的文件的不同，即使它們符合 hello 中的 hello 查詢相同的方式。 這是因為 hello 計分公式有比只 TF/IDF 的多個元件。 在此情況下，已將較高的分數指派給文件 3，因為它的說明較短。 深入了解[Lucene 的實際計分公式](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html)toounderstand 欄位長度和其他因素會影響 hello 相關性分數。

某些查詢類型 （萬用字元、 前置詞、 regex） 一律參與常數分數 toohello 整體文件的分數。 這可讓透過查詢擴充 toobe 包含在 hello 結果中，但不會影響 hello 排名找到的相符項目。 

範例會說明這很重要的原因。 萬用字元搜尋，包括前置詞搜尋會模稜兩可根據定義，因為 hello 輸入位於非常大量的不同詞彙可能符合的部分字串 ("tours and techniques"，"tourettes"上找到的相符項目與考量 」 教學課程 *，"的輸入，以及"tourmaline")。 提供這些結果的 hello 性質，所以 tooreasonably 推斷哪些詞彙會比其他更有價值。 基於這個理由，當評分導致萬用字元、前置詞和 Rregex 的查詢類型時，我們會忽略詞彙頻率。 在多部分的搜尋要求，其中包含部分或完全詞彙中，從 hello 部分輸入的結果會合併與常數評分 tooavoid 偏差朝向可能未預期的相符項目。

### <a name="score-tuning"></a>微調分數

有兩種方式 tootune 相關性分數 Azure 搜尋中：

1. **計分設定檔**升級 hello 排名根據一組規則結果清單中的文件。 在本例中，我們可以考慮在 hello 標題 欄位相關比 hello 描述欄位中比對的文件中比對的文件。 此外，如果索引有每家旅館的價格欄位，我們便可以提升包含較低價格的文件。 進一步了解如何太[新增評分設定檔 tooa 搜尋索引。](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **詞彙提升**（僅適用於 hello 完整 Lucene 的查詢語法） 提供提升運算子`^`可以套用 tooany hello 查詢樹狀結構的一部分。 在本例中，而不是根據 hello 前置詞搜尋*air-condition*\*，其中一個可以搜尋與任一 hello 精確的詞彙*air-condition*或 hello 前置詞，但比對確切的 hello 的文件詞彙次序比它高藉由套用 boost toohello 詞彙查詢：*空中條件 ^2 | |air-condition**。 深入了解[詞彙提升](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost)。


### <a name="scoring-in-a-distributed-index"></a>分散式索引中的評分

Azure 搜尋中的所有索引都會自動分割成多個分區，讓我們 tooquickly 分散多部 hello 索引服務規模期間節點向上或向下調整。 當發出搜尋要求時，它會針對每個分區獨立發行。 hello 從每個分區的結果會合併，然後依分數排序 （如果沒有其他順序會定義）。 它是不在所有分區間 hello 計分函式加權查詢 「 詞彙頻率對它的反向的文件頻率 hello 分區內的所有文件中的重要 tooknow ！

這表示如果相同的文件位於不同的分區，則相同文件的相關性分數可能會有所不同。 幸運的是，這類差異會因為 toomore 甚至詞彙發佈 hello hello 索引的文件數目隨著通常 toodisappear。 不可能 tooassume 任何給定的文件將會放在哪一個分區。 不過，假設不會變更文件索引鍵，則會一律指派 toohello 相同分區。

一般情況下，文件分數不 hello 最佳屬性來排序文件，如果穩定性順序很重要。 例如，假設分數完全相同的兩個文件，並不保證哪一項會先出現在後續的執行中的 hello 相同的查詢。 文件分數應該只授與一般的意義上，文件相關性的相對 tooother 文件 hello 結果集中。

## <a name="conclusion"></a>結論

hello 成功網際網路搜尋引擎的私用資料透過引發全文檢索搜尋的期望。 幾乎所有種類的搜尋經驗，我們現在預期 hello 引擎 toounderstand 我們的目的，即使條款拼字錯誤或不完整。 我們甚至可能會根據接近對等的詞彙，或從來不會實際指定的同義字來預期相符項目。

從技術觀點來看，全文檢索搜尋是相當複雜，需要複雜的語言分析和系統化的方法 tooprocessing 抽出，展開並轉換查詢詞彙 toodeliver 相關結果的方式。 指定 hello 固有的複雜性，有許多因素可能會影響查詢的 hello 結果。 基於這個理由，投資 hello 時間 toounderstand hello 機制全文檢索搜尋的優點是實際 toowork 透過非預期的結果時。  

這篇文章探討 hello Azure 搜尋內容中的全文檢索搜尋。 我們希望您提供了足夠的背景 toorecognize 可能原因和解決方式解決常見的查詢問題。 

## <a name="next-steps"></a>後續步驟

+ 建立 hello 範例索引，請嘗試掉不同的查詢，檢閱結果。 如需指示，請參閱[建置及查詢 hello 入口網站中的索引](search-get-started-portal.md#query-index)。

+ 請嘗試其他查詢語法，從 hello[搜尋文件](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples)範例 > 一節或從[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)hello 入口網站中的搜尋總管 中。

+ 檢閱[計分設定檔](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)如果您想 tootune 排名搜尋應用程式中。

+ 深入了解如何 tooapply[特定語言的語彙分析器](https://docs.microsoft.com/rest/api/searchservice/language-support)。

+ [設定自訂分析器](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search)以進行最少的處理，或是在特定欄位上進行特殊的處理。

+ 在這個示範網站上同時[比較標準和英文分析器](http://alice.unearth.ai/) \(英文\)。 

## <a name="see-also"></a>另請參閱

[搜尋文件 REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[完整的 Lucene 查詢語法](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[處理搜尋結果](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
