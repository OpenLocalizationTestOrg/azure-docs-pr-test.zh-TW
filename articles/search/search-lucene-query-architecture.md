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
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="852c4-103">全文檢索搜尋如何在 Azure 搜尋服務中運作</span><span class="sxs-lookup"><span data-stu-id="852c4-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="852c4-104">本文適用於需要更深入了解 Lucene 全文檢索搜尋在 Azure 搜尋服務中運作方式的開發人員。</span><span class="sxs-lookup"><span data-stu-id="852c4-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="852c4-105">針對文字查詢，Azure 搜尋服務在大部分情況下會順暢地提供預期的結果，但您偶爾可能會收到看起來像以某種方式「關閉」的結果。</span><span class="sxs-lookup"><span data-stu-id="852c4-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="852c4-106">在這些情況下，在具有背景 hello Lucene 查詢執行的四個階段 （查詢剖析語彙分析、 文件比對，計分） 可協助您識別特定變更 tooquery 參數或索引將會傳送 hello 的組態所要的結果。</span><span class="sxs-lookup"><span data-stu-id="852c4-106">In these situations, having a background in hello four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes tooquery parameters or index configuration that will deliver hello desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="852c4-107">Azure 搜尋服務會使用 Lucene 來進行全文檢索搜尋，但 Lucene 整合並不詳盡。</span><span class="sxs-lookup"><span data-stu-id="852c4-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="852c4-108">我們可以選擇性地公開 （expose） 和擴充 Lucene 功能 tooenable hello 案例重要 tooAzure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="852c4-108">We selectively expose and extend Lucene functionality tooenable hello scenarios important tooAzure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="852c4-109">架構概觀和圖表</span><span class="sxs-lookup"><span data-stu-id="852c4-109">Architecture overview and diagram</span></span>

<span data-ttu-id="852c4-110">處理全文檢索搜尋查詢以剖析 hello 查詢文字 tooextract 搜尋詞彙為開頭。</span><span class="sxs-lookup"><span data-stu-id="852c4-110">Processing a full text search query starts with parsing hello query text tooextract search terms.</span></span> <span data-ttu-id="852c4-111">hello 搜尋引擎會使用索引 tooretrieve 文件與比對的詞彙。</span><span class="sxs-lookup"><span data-stu-id="852c4-111">hello search engine uses an index tooretrieve documents with matching terms.</span></span> <span data-ttu-id="852c4-112">個別的查詢詞彙有時細分並重新組成新表單 toocast 到更廣泛的網路上項目可以視為可能的相符項目。</span><span class="sxs-lookup"><span data-stu-id="852c4-112">Individual query terms are sometimes broken down and reconstituted into new forms toocast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="852c4-113">依相關性分數指派的 tooeach 個別比對文件，然後進行排序結果集。</span><span class="sxs-lookup"><span data-stu-id="852c4-113">A result set is then sorted by a relevance score assigned tooeach individual matching document.</span></span> <span data-ttu-id="852c4-114">這些在 hello hello 排名清單最上方會傳回 toohello 呼叫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="852c4-114">Those at hello top of hello ranked list are returned toohello calling application.</span></span>

<span data-ttu-id="852c4-115">重新敘述的查詢執行有四個階段︰</span><span class="sxs-lookup"><span data-stu-id="852c4-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="852c4-116">查詢剖析</span><span class="sxs-lookup"><span data-stu-id="852c4-116">Query parsing</span></span> 
2. <span data-ttu-id="852c4-117">語彙分析</span><span class="sxs-lookup"><span data-stu-id="852c4-117">Lexical analysis</span></span> 
3. <span data-ttu-id="852c4-118">擷取文件</span><span class="sxs-lookup"><span data-stu-id="852c4-118">Document retrieval</span></span> 
4. <span data-ttu-id="852c4-119">評分</span><span class="sxs-lookup"><span data-stu-id="852c4-119">Scoring</span></span> 

<span data-ttu-id="852c4-120">hello 圖說明 hello 用元件 tooprocess 搜尋要求。</span><span class="sxs-lookup"><span data-stu-id="852c4-120">hello diagram below illustrates hello components used tooprocess a search request.</span></span> 

 ![Azure 搜尋服務中的 Lucene 查詢架構圖表][1]


| <span data-ttu-id="852c4-122">重要元件</span><span class="sxs-lookup"><span data-stu-id="852c4-122">Key components</span></span> | <span data-ttu-id="852c4-123">功能描述</span><span class="sxs-lookup"><span data-stu-id="852c4-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="852c4-124">**查詢剖析器**</span><span class="sxs-lookup"><span data-stu-id="852c4-124">**Query parsers**</span></span> | <span data-ttu-id="852c4-125">分開查詢運算子的查詢詞彙，並建立 hello 查詢結構 （查詢樹狀結構） 傳送 toobe toohello 搜尋引擎。</span><span class="sxs-lookup"><span data-stu-id="852c4-125">Separate query terms from query operators and create hello query structure (a query tree) toobe sent toohello search engine.</span></span> |
|<span data-ttu-id="852c4-126">**分析器**</span><span class="sxs-lookup"><span data-stu-id="852c4-126">**Analyzers**</span></span> | <span data-ttu-id="852c4-127">執行查詢詞彙的語彙分析。</span><span class="sxs-lookup"><span data-stu-id="852c4-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="852c4-128">此程序可能包含轉換、移除或展開查詢詞彙。</span><span class="sxs-lookup"><span data-stu-id="852c4-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="852c4-129">**Index**</span><span class="sxs-lookup"><span data-stu-id="852c4-129">**Index**</span></span> | <span data-ttu-id="852c4-130">有效率的資料結構使用 toostore 和組織可搜尋索引文件從擷取的詞彙。</span><span class="sxs-lookup"><span data-stu-id="852c4-130">An efficient data structure used toostore and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="852c4-131">**搜尋引擎**</span><span class="sxs-lookup"><span data-stu-id="852c4-131">**Search engine**</span></span> | <span data-ttu-id="852c4-132">擷取和比對的 hello hello 內容為基礎的文件的分數反向索引。</span><span class="sxs-lookup"><span data-stu-id="852c4-132">Retrieves and scores matching documents based on hello contents of hello inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="852c4-133">搜尋要求的剖析</span><span class="sxs-lookup"><span data-stu-id="852c4-133">Anatomy of a search request</span></span>

<span data-ttu-id="852c4-134">搜尋要求是結果集所需傳回的完整規格。</span><span class="sxs-lookup"><span data-stu-id="852c4-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="852c4-135">最簡單的形式中，它是不設任何類型之條件的空查詢。</span><span class="sxs-lookup"><span data-stu-id="852c4-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="852c4-136">更真實的範例包含參數，數個查詢詞彙中，可能是已設定領域的 toocertain 欄位，可能是篩選條件運算式和排序規則。</span><span class="sxs-lookup"><span data-stu-id="852c4-136">A more realistic example includes parameters, several query terms, perhaps scoped toocertain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="852c4-137">hello 下列範例會搜尋要求，您可能會傳送 tooAzure 搜尋使用 hello [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)。</span><span class="sxs-lookup"><span data-stu-id="852c4-137">hello following example is a search request you might send tooAzure Search using hello [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

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

<span data-ttu-id="852c4-138">此要求，hello 搜尋引擎沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="852c4-138">For this request, hello search engine does hello following:</span></span>

1. <span data-ttu-id="852c4-139">篩選出 hello 價格為至少 $60 和小於 $300 文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-139">Filters out documents where hello price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="852c4-140">執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="852c4-140">Executes hello query.</span></span> <span data-ttu-id="852c4-141">在此範例中，hello 搜尋查詢所組成片語和詞彙： `"Spacious, air-condition* +\"Ocean view\""` (使用者通常不輸入標點符號，但是包含在 hello 範例可讓我們 tooexplain 分析器如何處理它)。</span><span class="sxs-lookup"><span data-stu-id="852c4-141">In this example, hello search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in hello example allows us tooexplain how analyzers handle it).</span></span> <span data-ttu-id="852c4-142">對於此查詢，hello 搜尋引擎掃描 hello 描述，並在指定的標題欄位`searchFields`包含 「 Ocean 檢視 」 的文件和此外 hello 詞彙"寬廣"，或在以 hello 前置詞開頭的項目上 「 air-condition"。</span><span class="sxs-lookup"><span data-stu-id="852c4-142">For this query, hello search engine scans hello description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on hello term "spacious", or on terms that start with hello prefix "air-condition".</span></span> <span data-ttu-id="852c4-143">hello`searchMode`參數 （預設值） 的任何詞彙或所有項目，其中詞彙是不需要明確的案例是使用的 toomatch (`+`)。</span><span class="sxs-lookup"><span data-stu-id="852c4-143">hello `searchMode` parameter is used toomatch on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="852c4-144">訂單所指定的地理位置，然後傳回 toohello 呼叫的應用程式的鄰近 tooa hello 旅館的結果集。</span><span class="sxs-lookup"><span data-stu-id="852c4-144">Orders hello resulting set of hotels by proximity tooa given geography location, and then returned toohello calling application.</span></span> 

<span data-ttu-id="852c4-145">hello 大部分的這篇文章是關於處理 hello*搜尋查詢*: `"Spacious, air-condition* +\"Ocean view\""`。</span><span class="sxs-lookup"><span data-stu-id="852c4-145">hello majority of this article is about processing of hello *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="852c4-146">篩選和排序不在範圍內。</span><span class="sxs-lookup"><span data-stu-id="852c4-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="852c4-147">如需詳細資訊，請參閱 hello[搜尋 API 參考文件](https://docs.microsoft.com/rest/api/searchservice/search-documents)。</span><span class="sxs-lookup"><span data-stu-id="852c4-147">For more information, see hello [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="852c4-148">第 1 階段︰查詢剖析</span><span class="sxs-lookup"><span data-stu-id="852c4-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="852c4-149">如前所述，hello 查詢字串，則 hello hello 要求第一行：</span><span class="sxs-lookup"><span data-stu-id="852c4-149">As noted, hello query string is hello first line of hello request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="852c4-150">hello 查詢剖析器分隔運算子 (例如`*`和`+`hello 範例中) 從搜尋詞彙，並將解構 hello 搜尋查詢*子查詢*支援的類型：</span><span class="sxs-lookup"><span data-stu-id="852c4-150">hello query parser separates operators (such as `*` and `+` in hello example) from search terms, and deconstructs hello search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="852c4-151">詞彙查詢適用於獨立詞彙 (例如 spacious)</span><span class="sxs-lookup"><span data-stu-id="852c4-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="852c4-152">片語查詢適用於引號括住的詞彙 (例如 ocean view)</span><span class="sxs-lookup"><span data-stu-id="852c4-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="852c4-153">前置詞查詢適用於前置詞運算子後面的詞彙 `*` (例如 air-condition)</span><span class="sxs-lookup"><span data-stu-id="852c4-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="852c4-154">如需支援的查詢類型完整清單，請參閱 [Lucene 查詢語法](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span><span class="sxs-lookup"><span data-stu-id="852c4-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="852c4-155">子查詢相關聯的運算子決定 hello 查詢 「 必須 」 或 「 應該 」 文件順序滿足 toobe 視為相符。</span><span class="sxs-lookup"><span data-stu-id="852c4-155">Operators associated with a subquery determine whether hello query "must be" or "should be" satisfied in order for a document toobe considered a match.</span></span> <span data-ttu-id="852c4-156">例如， `+"Ocean view"` 「 必須 」 到期 toohello`+`運算子。</span><span class="sxs-lookup"><span data-stu-id="852c4-156">For example, `+"Ocean view"` is "must" due toohello `+` operator.</span></span> 

<span data-ttu-id="852c4-157">hello 查詢剖析器的重建 hello 子查詢至*查詢樹狀結構*toohello 搜尋引擎上傳遞 （代表 hello 查詢的內部結構）。</span><span class="sxs-lookup"><span data-stu-id="852c4-157">hello query parser restructures hello subqueries into a *query tree* (an internal structure representing hello query) it passes on toohello search engine.</span></span> <span data-ttu-id="852c4-158">在剖析查詢的第一個階段中 hello，hello 查詢樹狀結構看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="852c4-158">In hello first stage of query parsing, hello query tree looks like this.</span></span>  

 ![Boolean query searchmode any][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="852c4-160">支援的剖析器︰簡單和完整的 Lucene</span><span class="sxs-lookup"><span data-stu-id="852c4-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="852c4-161">Azure 搜尋服務會公開兩種不同的查詢語言，`simple` (預設值) 和 `full`。</span><span class="sxs-lookup"><span data-stu-id="852c4-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="852c4-162">所設定的 hello`queryType`參數與您的搜尋要求，您可告知 hello 查詢剖析器的查詢語言您選擇，讓它知道如何 toointerpret hello 運算子和語法。</span><span class="sxs-lookup"><span data-stu-id="852c4-162">By setting hello `queryType` parameter with your search request, you tell hello query parser which query language you choose so that it knows how toointerpret hello operators and syntax.</span></span> <span data-ttu-id="852c4-163">hello[簡單的查詢語言](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)憑直覺強固、 通常適合 toointerpret 使用者輸入為-沒有用戶端處理。</span><span class="sxs-lookup"><span data-stu-id="852c4-163">hello [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable toointerpret user input as-is without client-side processing.</span></span> <span data-ttu-id="852c4-164">它支援 web 搜尋引擎熟悉的查詢運算子。</span><span class="sxs-lookup"><span data-stu-id="852c4-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="852c4-165">hello[完整 Lucene 的查詢語言](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)，您會取得藉由設定`queryType=full`，藉由新增更多的運算子與類萬用字元，模糊的查詢類型，regex 和欄位範圍查詢的支援延伸 hello 預設簡單的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="852c4-165">hello [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends hello default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="852c4-166">例如，簡單查詢語法傳入的規則運算式會解譯為查詢字串而非運算式。</span><span class="sxs-lookup"><span data-stu-id="852c4-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="852c4-167">本文章中的 hello 範例要求會使用 hello 完整 Lucene 的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="852c4-167">hello example request in this article uses hello Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-hello-parser"></a><span data-ttu-id="852c4-168">受 searchMode hello 剖析器上的影響</span><span class="sxs-lookup"><span data-stu-id="852c4-168">Impact of searchMode on hello parser</span></span> 

<span data-ttu-id="852c4-169">另一個搜尋要求參數，會影響剖析為 hello`searchMode`參數。</span><span class="sxs-lookup"><span data-stu-id="852c4-169">Another search request parameter that affects parsing is hello `searchMode` parameter.</span></span> <span data-ttu-id="852c4-170">它所控制的布林值的查詢 hello 預設運算子： 任何 （預設值），或全部。</span><span class="sxs-lookup"><span data-stu-id="852c4-170">It controls hello default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="852c4-171">當`searchMode=any`，是 hello 預設，hello 空間分隔符號之間寬廣，air-condition 為或者 (`||`)，讓文字 hello 範例查詢相當於：</span><span class="sxs-lookup"><span data-stu-id="852c4-171">When `searchMode=any`, which is hello default, hello space delimiter between spacious and air-condition is OR (`||`), making hello sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="852c4-172">明確運算子，例如`+`中`+"Ocean view"`，會在布林查詢建構模稜兩可 (hello 詞彙*必須*符合)。</span><span class="sxs-lookup"><span data-stu-id="852c4-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (hello term *must* match).</span></span> <span data-ttu-id="852c4-173">較不明顯是 toointerpret hello 剩餘如何條款： 寬廣和 air-condition。</span><span class="sxs-lookup"><span data-stu-id="852c4-173">Less obvious is how toointerpret hello remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="852c4-174">應該 hello 搜尋引擎尋找相符項目上海景*和*寬廣*和*air-condition 嗎？</span><span class="sxs-lookup"><span data-stu-id="852c4-174">Should hello search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="852c4-175">它應該會發現海景或加上*其中一個*的 hello 剩餘條款？</span><span class="sxs-lookup"><span data-stu-id="852c4-175">Or should it find ocean view plus *either one* of hello remaining terms?</span></span> 

<span data-ttu-id="852c4-176">根據預設 (`searchMode=any`)，hello 搜尋引擎假設 hello 更廣泛的解譯方式。</span><span class="sxs-lookup"><span data-stu-id="852c4-176">By default (`searchMode=any`), hello search engine assumes hello broader interpretation.</span></span> <span data-ttu-id="852c4-177">任一個欄位應該相符，反映「或」語意。</span><span class="sxs-lookup"><span data-stu-id="852c4-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="852c4-178">hello 初始查詢樹狀結構之前，使用說明 hello 兩個 「 應該 」 作業，會顯示 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="852c4-178">hello initial query tree illustrated previously, with hello two "should" operations, shows hello default.</span></span>  

<span data-ttu-id="852c4-179">假設我們現在設定 `searchMode=all`。</span><span class="sxs-lookup"><span data-stu-id="852c4-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="852c4-180">在此情況下，hello 空格會解譯為 「 和 」 作業。</span><span class="sxs-lookup"><span data-stu-id="852c4-180">In this case, hello space is interpreted as an "and" operation.</span></span> <span data-ttu-id="852c4-181">每個 hello 其餘條款必須同時出現在 hello 文件 tooqualify 為相符項目。</span><span class="sxs-lookup"><span data-stu-id="852c4-181">Each of hello remaining terms must both be present in hello document tooqualify as a match.</span></span> <span data-ttu-id="852c4-182">hello 產生的範例查詢會解譯，如下所示：</span><span class="sxs-lookup"><span data-stu-id="852c4-182">hello resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="852c4-183">修改過的查詢樹狀結構，此查詢會，如下所示，比對文件所在的所有三個的子查詢的 hello 交集：</span><span class="sxs-lookup"><span data-stu-id="852c4-183">A modified query tree for this query would be as follows, where a matching document is hello intersection of all three subqueries:</span></span> 

 ![Boolean query searchmode all][3]

> [!Note] 
> <span data-ttu-id="852c4-185">透過 `searchMode=all` 選擇 `searchMode=any` 是藉由執行具代表性之查詢所得出的最佳決策。</span><span class="sxs-lookup"><span data-stu-id="852c4-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="852c4-186">可能的 tooinclude 運算子 （一般搜尋文件會儲存時） 的使用者可能會發現結果更具直覺性如果`searchMode=all`通知布林查詢建構。</span><span class="sxs-lookup"><span data-stu-id="852c4-186">Users who are likely tooinclude operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="852c4-187">如需詳細資訊之間的 hello 相互作用`searchMode`和運算子，請參閱[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)。</span><span class="sxs-lookup"><span data-stu-id="852c4-187">For more about hello interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="852c4-188">第 2 階段：語彙分析</span><span class="sxs-lookup"><span data-stu-id="852c4-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="852c4-189">語彙分析器程序*詞彙查詢*和*片語查詢*hello 查詢樹狀結構的結構之後。</span><span class="sxs-lookup"><span data-stu-id="852c4-189">Lexical analyzers process *term queries* and *phrase queries* after hello query tree is structured.</span></span> <span data-ttu-id="852c4-190">分析器接受 hello 文字輸入指定 tooit hello 剖析器、 處理序 hello 文字，並再傳送回語彙基元化的詞彙 toobe 併入 hello 查詢樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="852c4-190">An analyzer accepts hello text inputs given tooit by hello parser, processes hello text, and then sends back tokenized terms toobe incorporated into hello query tree.</span></span> 

<span data-ttu-id="852c4-191">hello 語彙分析最常見形式是*語言分析*的轉換規則的特定 tooa 給定語言為基礎的查詢字詞：</span><span class="sxs-lookup"><span data-stu-id="852c4-191">hello most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific tooa given language:</span></span> 

* <span data-ttu-id="852c4-192">減少查詢詞彙 toohello 根形式的文字</span><span class="sxs-lookup"><span data-stu-id="852c4-192">Reducing a query term toohello root form of a word</span></span> 
* <span data-ttu-id="852c4-193">移除不必要的字 (停用字詞，例如英文的 "the" 或 "and")</span><span class="sxs-lookup"><span data-stu-id="852c4-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="852c4-194">將複合字分成多個組件元件</span><span class="sxs-lookup"><span data-stu-id="852c4-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="852c4-195">將大寫的字改成小寫</span><span class="sxs-lookup"><span data-stu-id="852c4-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="852c4-196">所有這些作業通常 tooerase hello 使用者與 hello 詞彙儲存在 hello 索引所提供的 hello 文字輸入之間的差異。</span><span class="sxs-lookup"><span data-stu-id="852c4-196">All of these operations tend tooerase differences between hello text input provided by hello user and hello terms stored in hello index.</span></span> <span data-ttu-id="852c4-197">這類作業超出文字處理，而且需要深入了解 hello 語言本身。</span><span class="sxs-lookup"><span data-stu-id="852c4-197">Such operations go beyond text processing and require in-depth knowledge of hello language itself.</span></span> <span data-ttu-id="852c4-198">tooadd 這層的語言感知，Azure 搜尋支援一長串[語言分析器](https://docs.microsoft.com/rest/api/searchservice/language-support)Lucene 和 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="852c4-198">tooadd this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="852c4-199">分析需求的範圍從最小 tooelaborate 根據您的案例。</span><span class="sxs-lookup"><span data-stu-id="852c4-199">Analysis requirements can range from minimal tooelaborate depending on your scenario.</span></span> <span data-ttu-id="852c4-200">您可以控制語彙分析的複雜性，選取其中一個預先定義的 hello 分析器 hello 或建立您自己[自訂分析器](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search)。</span><span class="sxs-lookup"><span data-stu-id="852c4-200">You can control complexity of lexical analysis by hello selecting one of hello predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="852c4-201">分析器是已設定領域的 toosearchable 欄位和欄位定義中指定。</span><span class="sxs-lookup"><span data-stu-id="852c4-201">Analyzers are scoped toosearchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="852c4-202">這可讓您 toovary 語彙分析每個欄位為基礎。</span><span class="sxs-lookup"><span data-stu-id="852c4-202">This allows you toovary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="852c4-203">未指定，hello*標準*Lucene 分析器 的用途。</span><span class="sxs-lookup"><span data-stu-id="852c4-203">Unspecified, hello *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="852c4-204">在我們的範例，先前的 tooanalysis hello 初始查詢樹狀結構有 hello 詞彙"Spacious，「 以大寫的"S"和逗號的 hello 查詢剖析器會解譯為 hello 查詢字詞 （逗號不被視為查詢語言運算子） 的一部分。</span><span class="sxs-lookup"><span data-stu-id="852c4-204">In our example, prior tooanalysis, hello initial query tree has hello term "Spacious," with an uppercase "S" and a comma that hello query parser interprets as a part of hello query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="852c4-205">Hello 預設分析器處理 hello 詞彙時，它將小寫"海景"和"寬廣 」，並移除 hello 逗號字元。</span><span class="sxs-lookup"><span data-stu-id="852c4-205">When hello default analyzer processes hello term, it will lowercase "ocean view" and "spacious", and remove hello comma character.</span></span> <span data-ttu-id="852c4-206">hello 修改過的查詢樹狀結構會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="852c4-206">hello modified query tree will look as follows:</span></span> 

 ![包含分析過詞彙的布林值查詢][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="852c4-208">測試分析器的行為</span><span class="sxs-lookup"><span data-stu-id="852c4-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="852c4-209">可以使用 hello 測試分析器的 hello 行為[分析 API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer)。</span><span class="sxs-lookup"><span data-stu-id="852c4-209">hello behavior of an analyzer can be tested using hello [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="852c4-210">提供您想要指定分析器哪些詞彙將會產生 tooanalyze toosee 的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="852c4-210">Provide hello text you want tooanalyze toosee what terms given analyzer will generate.</span></span> <span data-ttu-id="852c4-211">例如，toosee hello 標準分析器會處理如何 hello 文字"air-condition 」，您可以發出下列要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="852c4-211">For example, toosee how hello standard analyzer would process hello text "air-condition", you can issue hello following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="852c4-212">hello 標準分析器會分成下列兩個語彙基元，這些註解的屬性，例如開始和結束位移 （用來叫用的反白顯示），以及它們的位置 （用來比對片語） hello hello 輸入的文字：</span><span class="sxs-lookup"><span data-stu-id="852c4-212">hello standard analyzer breaks hello input text into hello following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

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

### <a name="exceptions-toolexical-analysis"></a><span data-ttu-id="852c4-213">例外狀況 toolexical 分析</span><span class="sxs-lookup"><span data-stu-id="852c4-213">Exceptions toolexical analysis</span></span> 

<span data-ttu-id="852c4-214">語彙分析適用於需要完整條款 – 查詢詞彙或片語查詢 tooquery 型別。</span><span class="sxs-lookup"><span data-stu-id="852c4-214">Lexical analysis applies only tooquery types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="852c4-215">它不會套用 tooquery 類型不完整的條款-前置詞的查詢、 萬用字元查詢、 regex 查詢或 tooa 模糊查詢。</span><span class="sxs-lookup"><span data-stu-id="852c4-215">It doesn’t apply tooquery types with incomplete terms – prefix query, wildcard query, regex query – or tooa fuzzy query.</span></span> <span data-ttu-id="852c4-216">這些查詢類型，包括 hello 與詞彙的前置詞查詢*air-condition\** 在本例中，加入直接 toohello 查詢樹狀目錄中，略過 hello 分析階段。</span><span class="sxs-lookup"><span data-stu-id="852c4-216">Those query types, including hello prefix query with term *air-condition\** in our example, are added directly toohello query tree, bypassing hello analysis stage.</span></span> <span data-ttu-id="852c4-217">hello 對這些類型的查詢詞彙的轉換為大寫。</span><span class="sxs-lookup"><span data-stu-id="852c4-217">hello only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="852c4-218">第 3 階段：擷取文件</span><span class="sxs-lookup"><span data-stu-id="852c4-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="852c4-219">文件擷取指的是 toofinding hello 索引中的相符詞彙的文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-219">Document retrieval refers toofinding documents with matching terms in hello index.</span></span> <span data-ttu-id="852c4-220">了解這個階段的最佳方式就是範例。</span><span class="sxs-lookup"><span data-stu-id="852c4-220">This stage is understood best through an example.</span></span> <span data-ttu-id="852c4-221">讓我們開始與旅館索引具有下列簡單的結構描述的 hello:</span><span class="sxs-lookup"><span data-stu-id="852c4-221">Let's start with a hotels index having hello following simple schema:</span></span> 

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

<span data-ttu-id="852c4-222">進一步假設這個索引包含下列四個文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="852c4-222">Further assume that this index contains hello following four documents:</span></span> 

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

<span data-ttu-id="852c4-223">**詞彙編製索引的方式**</span><span class="sxs-lookup"><span data-stu-id="852c4-223">**How terms are indexed**</span></span>

<span data-ttu-id="852c4-224">它可協助 tooknow toounderstand 擷取有關編製索引的幾個基本概念。</span><span class="sxs-lookup"><span data-stu-id="852c4-224">toounderstand retrieval, it helps tooknow a few basics about indexing.</span></span> <span data-ttu-id="852c4-225">儲存體 hello 單位是反向的索引，一個用於每個可搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="852c4-225">hello unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="852c4-226">反向索引內會有所有文件中所有詞彙的排序清單。</span><span class="sxs-lookup"><span data-stu-id="852c4-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="852c4-227">每個詞彙對應 toohello 發生，以下的 hello 範例中為明顯的文件清單。</span><span class="sxs-lookup"><span data-stu-id="852c4-227">Each term maps toohello list of documents in which it occurs, as evident in hello example below.</span></span>

<span data-ttu-id="852c4-228">tooproduce hello 詞彙在反向索引中，hello 搜尋引擎執行語彙分析 hello 文件內容，透過類似 toowhat 查詢處理期間進行的作業。</span><span class="sxs-lookup"><span data-stu-id="852c4-228">tooproduce hello terms in an inverted index, hello search engine performs lexical analysis over hello content of documents, similar toowhat happens during query processing.</span></span> <span data-ttu-id="852c4-229">文字輸入傳遞 tooan 分析器 中，較低的大小寫慣例，除去標點符號及其他等等，根據 hello 的分析器組態。</span><span class="sxs-lookup"><span data-stu-id="852c4-229">Text inputs are passed tooan analyzer, lower-cased, stripped of punctuation, and so forth, depending on hello analyzer configuration.</span></span> <span data-ttu-id="852c4-230">它是不常見，但並非必要，toouse hello 相同分析器搜尋和索引作業，讓查詢詞彙起來更 hello 索引內的詞彙。</span><span class="sxs-lookup"><span data-stu-id="852c4-230">It's common, but not required, toouse hello same analyzers for search and indexing operations so that query terms look more like terms inside hello index.</span></span>

> [!Note]
> <span data-ttu-id="852c4-231">Azure 搜尋服務可讓您指定不同的分析器來編製索引，並透過其他的 `indexAnalyzer` 和 `searchAnalyzer` 欄位參數進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="852c4-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="852c4-232">如果未指定，hello 分析器設定以 hello`analyzer`屬性用於索引和搜尋。</span><span class="sxs-lookup"><span data-stu-id="852c4-232">If unspecified, hello analyzer set with hello `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="852c4-233">**範例文件的反向索引**</span><span class="sxs-lookup"><span data-stu-id="852c4-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="852c4-234">傳回 tooour 範例中的，針對 hello**標題** 欄位中，反轉 hello 索引看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="852c4-234">Returning tooour example, for hello **title** field, hello inverted index looks like this:</span></span>

| <span data-ttu-id="852c4-235">詞彙</span><span class="sxs-lookup"><span data-stu-id="852c4-235">Term</span></span> | <span data-ttu-id="852c4-236">文件清單</span><span class="sxs-lookup"><span data-stu-id="852c4-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="852c4-237">atman</span><span class="sxs-lookup"><span data-stu-id="852c4-237">atman</span></span> | <span data-ttu-id="852c4-238">1</span><span class="sxs-lookup"><span data-stu-id="852c4-238">1</span></span> |
| <span data-ttu-id="852c4-239">beach</span><span class="sxs-lookup"><span data-stu-id="852c4-239">beach</span></span> | <span data-ttu-id="852c4-240">2</span><span class="sxs-lookup"><span data-stu-id="852c4-240">2</span></span> |
| <span data-ttu-id="852c4-241">hotel</span><span class="sxs-lookup"><span data-stu-id="852c4-241">hotel</span></span> | <span data-ttu-id="852c4-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="852c4-242">1, 3</span></span> |
| <span data-ttu-id="852c4-243">ocean</span><span class="sxs-lookup"><span data-stu-id="852c4-243">ocean</span></span> | <span data-ttu-id="852c4-244">4</span><span class="sxs-lookup"><span data-stu-id="852c4-244">4</span></span>  |
| <span data-ttu-id="852c4-245">playa</span><span class="sxs-lookup"><span data-stu-id="852c4-245">playa</span></span> | <span data-ttu-id="852c4-246">3</span><span class="sxs-lookup"><span data-stu-id="852c4-246">3</span></span> |
| <span data-ttu-id="852c4-247">resort</span><span class="sxs-lookup"><span data-stu-id="852c4-247">resort</span></span> | <span data-ttu-id="852c4-248">3</span><span class="sxs-lookup"><span data-stu-id="852c4-248">3</span></span> |
| <span data-ttu-id="852c4-249">retreat</span><span class="sxs-lookup"><span data-stu-id="852c4-249">retreat</span></span> | <span data-ttu-id="852c4-250">4</span><span class="sxs-lookup"><span data-stu-id="852c4-250">4</span></span> |

<span data-ttu-id="852c4-251">Hello 標題 欄位中，只有*旅館*出現兩份文件： 1、 3。</span><span class="sxs-lookup"><span data-stu-id="852c4-251">In hello title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="852c4-252">Hello**描述** 欄位中，hello 索引如下所示：</span><span class="sxs-lookup"><span data-stu-id="852c4-252">For hello **description** field, hello index is as follows:</span></span>

| <span data-ttu-id="852c4-253">詞彙</span><span class="sxs-lookup"><span data-stu-id="852c4-253">Term</span></span> | <span data-ttu-id="852c4-254">文件清單</span><span class="sxs-lookup"><span data-stu-id="852c4-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="852c4-255">air</span><span class="sxs-lookup"><span data-stu-id="852c4-255">air</span></span> | <span data-ttu-id="852c4-256">3</span><span class="sxs-lookup"><span data-stu-id="852c4-256">3</span></span>
| <span data-ttu-id="852c4-257">和</span><span class="sxs-lookup"><span data-stu-id="852c4-257">and</span></span> | <span data-ttu-id="852c4-258">4</span><span class="sxs-lookup"><span data-stu-id="852c4-258">4</span></span>
| <span data-ttu-id="852c4-259">beach</span><span class="sxs-lookup"><span data-stu-id="852c4-259">beach</span></span> | <span data-ttu-id="852c4-260">1</span><span class="sxs-lookup"><span data-stu-id="852c4-260">1</span></span>
| <span data-ttu-id="852c4-261">conditioned</span><span class="sxs-lookup"><span data-stu-id="852c4-261">conditioned</span></span> | <span data-ttu-id="852c4-262">3</span><span class="sxs-lookup"><span data-stu-id="852c4-262">3</span></span>
| <span data-ttu-id="852c4-263">comfortable</span><span class="sxs-lookup"><span data-stu-id="852c4-263">comfortable</span></span> | <span data-ttu-id="852c4-264">3</span><span class="sxs-lookup"><span data-stu-id="852c4-264">3</span></span>
| <span data-ttu-id="852c4-265">distance</span><span class="sxs-lookup"><span data-stu-id="852c4-265">distance</span></span> | <span data-ttu-id="852c4-266">1</span><span class="sxs-lookup"><span data-stu-id="852c4-266">1</span></span>
| <span data-ttu-id="852c4-267">island</span><span class="sxs-lookup"><span data-stu-id="852c4-267">island</span></span> | <span data-ttu-id="852c4-268">2</span><span class="sxs-lookup"><span data-stu-id="852c4-268">2</span></span>
| <span data-ttu-id="852c4-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="852c4-269">kauaʻi</span></span> | <span data-ttu-id="852c4-270">2</span><span class="sxs-lookup"><span data-stu-id="852c4-270">2</span></span>
| <span data-ttu-id="852c4-271">located</span><span class="sxs-lookup"><span data-stu-id="852c4-271">located</span></span> | <span data-ttu-id="852c4-272">2</span><span class="sxs-lookup"><span data-stu-id="852c4-272">2</span></span>
| <span data-ttu-id="852c4-273">north</span><span class="sxs-lookup"><span data-stu-id="852c4-273">north</span></span> | <span data-ttu-id="852c4-274">2</span><span class="sxs-lookup"><span data-stu-id="852c4-274">2</span></span>
| <span data-ttu-id="852c4-275">ocean</span><span class="sxs-lookup"><span data-stu-id="852c4-275">ocean</span></span> | <span data-ttu-id="852c4-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="852c4-276">1, 2, 3</span></span>
| <span data-ttu-id="852c4-277">of</span><span class="sxs-lookup"><span data-stu-id="852c4-277">of</span></span> | <span data-ttu-id="852c4-278">2</span><span class="sxs-lookup"><span data-stu-id="852c4-278">2</span></span>
| <span data-ttu-id="852c4-279">on</span><span class="sxs-lookup"><span data-stu-id="852c4-279">on</span></span> |<span data-ttu-id="852c4-280">2</span><span class="sxs-lookup"><span data-stu-id="852c4-280">2</span></span>
| <span data-ttu-id="852c4-281">quiet</span><span class="sxs-lookup"><span data-stu-id="852c4-281">quiet</span></span> | <span data-ttu-id="852c4-282">4</span><span class="sxs-lookup"><span data-stu-id="852c4-282">4</span></span>
| <span data-ttu-id="852c4-283">rooms</span><span class="sxs-lookup"><span data-stu-id="852c4-283">rooms</span></span>  | <span data-ttu-id="852c4-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="852c4-284">1, 3</span></span>
| <span data-ttu-id="852c4-285">secluded</span><span class="sxs-lookup"><span data-stu-id="852c4-285">secluded</span></span> | <span data-ttu-id="852c4-286">4</span><span class="sxs-lookup"><span data-stu-id="852c4-286">4</span></span>
| <span data-ttu-id="852c4-287">shore</span><span class="sxs-lookup"><span data-stu-id="852c4-287">shore</span></span> | <span data-ttu-id="852c4-288">2</span><span class="sxs-lookup"><span data-stu-id="852c4-288">2</span></span>
| <span data-ttu-id="852c4-289">spacious</span><span class="sxs-lookup"><span data-stu-id="852c4-289">spacious</span></span> | <span data-ttu-id="852c4-290">1</span><span class="sxs-lookup"><span data-stu-id="852c4-290">1</span></span>
| <span data-ttu-id="852c4-291">hello</span><span class="sxs-lookup"><span data-stu-id="852c4-291">hello</span></span> | <span data-ttu-id="852c4-292">1、2</span><span class="sxs-lookup"><span data-stu-id="852c4-292">1, 2</span></span>
| <span data-ttu-id="852c4-293">太</span><span class="sxs-lookup"><span data-stu-id="852c4-293">too</span></span>| <span data-ttu-id="852c4-294">1</span><span class="sxs-lookup"><span data-stu-id="852c4-294">1</span></span>
| <span data-ttu-id="852c4-295">view</span><span class="sxs-lookup"><span data-stu-id="852c4-295">view</span></span> | <span data-ttu-id="852c4-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="852c4-296">1, 2, 3</span></span>
| <span data-ttu-id="852c4-297">walking</span><span class="sxs-lookup"><span data-stu-id="852c4-297">walking</span></span> | <span data-ttu-id="852c4-298">1</span><span class="sxs-lookup"><span data-stu-id="852c4-298">1</span></span>
| <span data-ttu-id="852c4-299">取代為</span><span class="sxs-lookup"><span data-stu-id="852c4-299">with</span></span> | <span data-ttu-id="852c4-300">3</span><span class="sxs-lookup"><span data-stu-id="852c4-300">3</span></span>


<span data-ttu-id="852c4-301">**比對查詢詞彙與索引的詞彙**</span><span class="sxs-lookup"><span data-stu-id="852c4-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="852c4-302">指定上述 hello 反轉索引，讓我們傳回 toohello 範例查詢並查看如何比對文件找到範例查詢。</span><span class="sxs-lookup"><span data-stu-id="852c4-302">Given hello inverted indices above, let’s return toohello sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="852c4-303">前文提過該 hello 最終查詢樹狀結構看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="852c4-303">Recall that hello final query tree looks like this:</span></span> 

 ![包含分析過詞彙的布林值查詢][4]

<span data-ttu-id="852c4-305">執行查詢時，個別的查詢會針對執行 hello 可搜尋的欄位獨立。</span><span class="sxs-lookup"><span data-stu-id="852c4-305">During query execution, individual queries are executed against hello searchable fields independently.</span></span> 

+ <span data-ttu-id="852c4-306">hello TermQuery"寬廣"會比對文件 1 (旅館 Atman)。</span><span class="sxs-lookup"><span data-stu-id="852c4-306">hello TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="852c4-307">hello PrefixQuery，"air-condition *"，不符合任何文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-307">hello PrefixQuery, "air-condition*", doesn't match any documents.</span></span> 

  <span data-ttu-id="852c4-308">這個行為有時候會混淆開發人員。</span><span class="sxs-lookup"><span data-stu-id="852c4-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="852c4-309">雖然 air-conditioned hello 詞彙存在 hello 文件中，它是分割成兩個詞彙 hello 預設解析程式。</span><span class="sxs-lookup"><span data-stu-id="852c4-309">Although hello term air-conditioned exists in hello document, it is split into two terms by hello default analyzer.</span></span> <span data-ttu-id="852c4-310">還記得包含部分詞彙的前置詞查詢不會進行分析。</span><span class="sxs-lookup"><span data-stu-id="852c4-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="852c4-311">因此具有前置詞"air-condition 」 中查閱 hello 條款反向索引，但找不到。</span><span class="sxs-lookup"><span data-stu-id="852c4-311">Therefore terms with prefix "air-condition" are looked up in hello inverted index and not found.</span></span>

+ <span data-ttu-id="852c4-312">hello PhraseQuery 「 ocean 檢視 」 查閱 hello 條款 」 ocean 」 和 「 檢視 」，並檢查 hello 相近的 hello 原始文件中的詞彙。</span><span class="sxs-lookup"><span data-stu-id="852c4-312">hello PhraseQuery, "ocean view", looks up hello terms "ocean" and "view" and checks hello proximity of terms in hello original document.</span></span> <span data-ttu-id="852c4-313">文件 1、 2 和 3 符合這個 hello 描述欄位中的查詢。</span><span class="sxs-lookup"><span data-stu-id="852c4-313">Documents 1, 2 and 3 match this query in hello description field.</span></span> <span data-ttu-id="852c4-314">請注意文件 4 有 hello 標題中的 hello 詞彙 ocean，但不視為相符項目，因為我們想要尋求 hello"海景"片語，而不是個別文字。</span><span class="sxs-lookup"><span data-stu-id="852c4-314">Notice document 4 has hello term ocean in hello title but isn’t considered a match, as we're looking for hello "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="852c4-315">搜尋查詢針對 hello Azure 搜尋索引，除非您限制設定以 hello hello 欄位中的所有可搜尋欄位單獨執行`searchFields`參數 hello 範例搜尋要求中所示。</span><span class="sxs-lookup"><span data-stu-id="852c4-315">A search query is executed independently against all searchable fields in hello Azure Search index unless you limit hello fields set with hello `searchFields` parameter, as illustrated in hello example search request.</span></span> <span data-ttu-id="852c4-316">傳回符合任何選取的 hello 欄位中的文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-316">Documents that match in any of hello selected fields are returned.</span></span> 

<span data-ttu-id="852c4-317">Hello 整個 hello 查詢有問題，在比對的 hello 文件會是 1、 2、 3。</span><span class="sxs-lookup"><span data-stu-id="852c4-317">On hello whole, for hello query in question, hello documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="852c4-318">第 4 階段︰評分</span><span class="sxs-lookup"><span data-stu-id="852c4-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="852c4-319">會將相關性分數指派給搜尋結果集中的每個文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="852c4-320">hello 相關性分數的 hello 函式是 toorank 更高版本，這些文件最佳回答使用者問題所表示的 hello 搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="852c4-320">hello function of hello relevance score is toorank higher those documents that best answer a user question as expressed by hello search query.</span></span> <span data-ttu-id="852c4-321">hello 分數會根據比對的詞彙的統計屬性來計算的。</span><span class="sxs-lookup"><span data-stu-id="852c4-321">hello score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="852c4-322">Hello hello 計分公式的核心是[TF IDF （「 詞彙頻率反向的文件頻率）](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)。</span><span class="sxs-lookup"><span data-stu-id="852c4-322">At hello core of hello scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="852c4-323">在查詢中包含少數且常見的詞彙，TF/IDF 升級包含 hello 罕見詞彙的結果。</span><span class="sxs-lookup"><span data-stu-id="852c4-323">In queries containing rare and common terms, TF/IDF promotes results containing hello rare term.</span></span> <span data-ttu-id="852c4-324">例如，在所有的維基百科文章假設索引中，從文件相符的 hello 查詢*hello 總統*、 比對文件*總統*會被視為比更有相關性比對文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched hello query *hello president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="852c4-325">評分範例</span><span class="sxs-lookup"><span data-stu-id="852c4-325">Scoring example</span></span>

<span data-ttu-id="852c4-326">前文提過 hello 三份文件符合我們的範例查詢：</span><span class="sxs-lookup"><span data-stu-id="852c4-326">Recall hello three documents that matched our example query:</span></span>
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

<span data-ttu-id="852c4-327">最佳記錄 1 個相符的 hello 查詢，因為兩者 hello 詞彙*寬廣*與 hello 必要的片語*海景*發生 hello 描述欄位中。</span><span class="sxs-lookup"><span data-stu-id="852c4-327">Document 1 matched hello query best because both hello term *spacious* and hello required phrase *ocean view* occur in hello description field.</span></span> <span data-ttu-id="852c4-328">hello 下面兩個文件符合只 hello 片語*海景*。</span><span class="sxs-lookup"><span data-stu-id="852c4-328">hello next two documents match only hello phrase *ocean view*.</span></span> <span data-ttu-id="852c4-329">它可能會意外該 hello 相關性分數 2 和 3 的文件的不同，即使它們符合 hello 中的 hello 查詢相同的方式。</span><span class="sxs-lookup"><span data-stu-id="852c4-329">It might be surprising that hello relevance score for document 2 and 3 is different even though they matched hello query in hello same way.</span></span> <span data-ttu-id="852c4-330">這是因為 hello 計分公式有比只 TF/IDF 的多個元件。</span><span class="sxs-lookup"><span data-stu-id="852c4-330">It's because hello scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="852c4-331">在此情況下，已將較高的分數指派給文件 3，因為它的說明較短。</span><span class="sxs-lookup"><span data-stu-id="852c4-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="852c4-332">深入了解[Lucene 的實際計分公式](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html)toounderstand 欄位長度和其他因素會影響 hello 相關性分數。</span><span class="sxs-lookup"><span data-stu-id="852c4-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand how field length and other factors can influence hello relevance score.</span></span>

<span data-ttu-id="852c4-333">某些查詢類型 （萬用字元、 前置詞、 regex） 一律參與常數分數 toohello 整體文件的分數。</span><span class="sxs-lookup"><span data-stu-id="852c4-333">Some query types (wildcard, prefix, regex) always contribute a constant score toohello overall document score.</span></span> <span data-ttu-id="852c4-334">這可讓透過查詢擴充 toobe 包含在 hello 結果中，但不會影響 hello 排名找到的相符項目。</span><span class="sxs-lookup"><span data-stu-id="852c4-334">This allows matches found through query expansion toobe included in hello results, but without affecting hello ranking.</span></span> 

<span data-ttu-id="852c4-335">範例會說明這很重要的原因。</span><span class="sxs-lookup"><span data-stu-id="852c4-335">An example illustrates why this matters.</span></span> <span data-ttu-id="852c4-336">萬用字元搜尋，包括前置詞搜尋會模稜兩可根據定義，因為 hello 輸入位於非常大量的不同詞彙可能符合的部分字串 ("tours and techniques"，"tourettes"上找到的相符項目與考量 」 教學課程 *，"的輸入，以及"tourmaline")。</span><span class="sxs-lookup"><span data-stu-id="852c4-336">Wildcard searches, including prefix searches, are ambiguous by definition because hello input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="852c4-337">提供這些結果的 hello 性質，所以 tooreasonably 推斷哪些詞彙會比其他更有價值。</span><span class="sxs-lookup"><span data-stu-id="852c4-337">Given hello nature of these results, there is no way tooreasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="852c4-338">基於這個理由，當評分導致萬用字元、前置詞和 Rregex 的查詢類型時，我們會忽略詞彙頻率。</span><span class="sxs-lookup"><span data-stu-id="852c4-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="852c4-339">在多部分的搜尋要求，其中包含部分或完全詞彙中，從 hello 部分輸入的結果會合併與常數評分 tooavoid 偏差朝向可能未預期的相符項目。</span><span class="sxs-lookup"><span data-stu-id="852c4-339">In a multi-part search request that includes partial and complete terms, results from hello partial input are incorporated with a constant score tooavoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="852c4-340">微調分數</span><span class="sxs-lookup"><span data-stu-id="852c4-340">Score tuning</span></span>

<span data-ttu-id="852c4-341">有兩種方式 tootune 相關性分數 Azure 搜尋中：</span><span class="sxs-lookup"><span data-stu-id="852c4-341">There are two ways tootune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="852c4-342">**計分設定檔**升級 hello 排名根據一組規則結果清單中的文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-342">**Scoring profiles** promote documents in hello ranked list of results based on a set of rules.</span></span> <span data-ttu-id="852c4-343">在本例中，我們可以考慮在 hello 標題 欄位相關比 hello 描述欄位中比對的文件中比對的文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-343">In our example, we could consider documents that matched in hello title field more relevant than documents that matched in hello description field.</span></span> <span data-ttu-id="852c4-344">此外，如果索引有每家旅館的價格欄位，我們便可以提升包含較低價格的文件。</span><span class="sxs-lookup"><span data-stu-id="852c4-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="852c4-345">進一步了解如何太[新增評分設定檔 tooa 搜尋索引。](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="852c4-345">Learn more how too[add Scoring Profiles tooa search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="852c4-346">**詞彙提升**（僅適用於 hello 完整 Lucene 的查詢語法） 提供提升運算子`^`可以套用 tooany hello 查詢樹狀結構的一部分。</span><span class="sxs-lookup"><span data-stu-id="852c4-346">**Term boosting** (available only in hello Full Lucene query syntax) provides a boosting operator `^` that can be applied tooany part of hello query tree.</span></span> <span data-ttu-id="852c4-347">在本例中，而不是根據 hello 前置詞搜尋*air-condition*\*，其中一個可以搜尋與任一 hello 精確的詞彙*air-condition*或 hello 前置詞，但比對確切的 hello 的文件詞彙次序比它高藉由套用 boost toohello 詞彙查詢：*空中條件 ^2 | |air-condition**。</span><span class="sxs-lookup"><span data-stu-id="852c4-347">In our example, instead of searching on hello prefix *air-condition*\*, one could search for either hello exact term *air-condition* or hello prefix, but documents that match on hello exact term are ranked higher by applying boost toohello term query: *air-condition^2||air-condition**.</span></span> <span data-ttu-id="852c4-348">深入了解[詞彙提升](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost)。</span><span class="sxs-lookup"><span data-stu-id="852c4-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="852c4-349">分散式索引中的評分</span><span class="sxs-lookup"><span data-stu-id="852c4-349">Scoring in a distributed index</span></span>

<span data-ttu-id="852c4-350">Azure 搜尋中的所有索引都會自動分割成多個分區，讓我們 tooquickly 分散多部 hello 索引服務規模期間節點向上或向下調整。</span><span class="sxs-lookup"><span data-stu-id="852c4-350">All indexes in Azure Search are automatically split into multiple shards, allowing us tooquickly distribute hello index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="852c4-351">當發出搜尋要求時，它會針對每個分區獨立發行。</span><span class="sxs-lookup"><span data-stu-id="852c4-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="852c4-352">hello 從每個分區的結果會合併，然後依分數排序 （如果沒有其他順序會定義）。</span><span class="sxs-lookup"><span data-stu-id="852c4-352">hello results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="852c4-353">它是不在所有分區間 hello 計分函式加權查詢 「 詞彙頻率對它的反向的文件頻率 hello 分區內的所有文件中的重要 tooknow ！</span><span class="sxs-lookup"><span data-stu-id="852c4-353">It is important tooknow that hello scoring function weights query term frequency against its inverse document frequency in all documents within hello shard, not across all shards!</span></span>

<span data-ttu-id="852c4-354">這表示如果相同的文件位於不同的分區，則相同文件的相關性分數可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="852c4-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="852c4-355">幸運的是，這類差異會因為 toomore 甚至詞彙發佈 hello hello 索引的文件數目隨著通常 toodisappear。</span><span class="sxs-lookup"><span data-stu-id="852c4-355">Fortunately, such differences tend toodisappear as hello number of documents in hello index grows due toomore even term distribution.</span></span> <span data-ttu-id="852c4-356">不可能 tooassume 任何給定的文件將會放在哪一個分區。</span><span class="sxs-lookup"><span data-stu-id="852c4-356">It’s not possible tooassume on which shard any given document will be placed.</span></span> <span data-ttu-id="852c4-357">不過，假設不會變更文件索引鍵，則會一律指派 toohello 相同分區。</span><span class="sxs-lookup"><span data-stu-id="852c4-357">However, assuming a document key doesn't change, it will always be assigned toohello same shard.</span></span>

<span data-ttu-id="852c4-358">一般情況下，文件分數不 hello 最佳屬性來排序文件，如果穩定性順序很重要。</span><span class="sxs-lookup"><span data-stu-id="852c4-358">In general, document score is not hello best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="852c4-359">例如，假設分數完全相同的兩個文件，並不保證哪一項會先出現在後續的執行中的 hello 相同的查詢。</span><span class="sxs-lookup"><span data-stu-id="852c4-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of hello same query.</span></span> <span data-ttu-id="852c4-360">文件分數應該只授與一般的意義上，文件相關性的相對 tooother 文件 hello 結果集中。</span><span class="sxs-lookup"><span data-stu-id="852c4-360">Document score should only give a general sense of document relevance relative tooother documents in hello results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="852c4-361">結論</span><span class="sxs-lookup"><span data-stu-id="852c4-361">Conclusion</span></span>

<span data-ttu-id="852c4-362">hello 成功網際網路搜尋引擎的私用資料透過引發全文檢索搜尋的期望。</span><span class="sxs-lookup"><span data-stu-id="852c4-362">hello success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="852c4-363">幾乎所有種類的搜尋經驗，我們現在預期 hello 引擎 toounderstand 我們的目的，即使條款拼字錯誤或不完整。</span><span class="sxs-lookup"><span data-stu-id="852c4-363">For almost any kind of search experience, we now expect hello engine toounderstand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="852c4-364">我們甚至可能會根據接近對等的詞彙，或從來不會實際指定的同義字來預期相符項目。</span><span class="sxs-lookup"><span data-stu-id="852c4-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="852c4-365">從技術觀點來看，全文檢索搜尋是相當複雜，需要複雜的語言分析和系統化的方法 tooprocessing 抽出，展開並轉換查詢詞彙 toodeliver 相關結果的方式。</span><span class="sxs-lookup"><span data-stu-id="852c4-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach tooprocessing in ways that distill, expand, and transform query terms toodeliver a relevant result.</span></span> <span data-ttu-id="852c4-366">指定 hello 固有的複雜性，有許多因素可能會影響查詢的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="852c4-366">Given hello inherent complexities, there are a lot of factors that can affect hello outcome of a query.</span></span> <span data-ttu-id="852c4-367">基於這個理由，投資 hello 時間 toounderstand hello 機制全文檢索搜尋的優點是實際 toowork 透過非預期的結果時。</span><span class="sxs-lookup"><span data-stu-id="852c4-367">For this reason, investing hello time toounderstand hello mechanics of full text search offers tangible benefits when trying toowork through unexpected results.</span></span>  

<span data-ttu-id="852c4-368">這篇文章探討 hello Azure 搜尋內容中的全文檢索搜尋。</span><span class="sxs-lookup"><span data-stu-id="852c4-368">This article explored full text search in hello context of Azure Search.</span></span> <span data-ttu-id="852c4-369">我們希望您提供了足夠的背景 toorecognize 可能原因和解決方式解決常見的查詢問題。</span><span class="sxs-lookup"><span data-stu-id="852c4-369">We hope it gives you sufficient background toorecognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="852c4-370">後續步驟</span><span class="sxs-lookup"><span data-stu-id="852c4-370">Next steps</span></span>

+ <span data-ttu-id="852c4-371">建立 hello 範例索引，請嘗試掉不同的查詢，檢閱結果。</span><span class="sxs-lookup"><span data-stu-id="852c4-371">Build hello sample index, try out different queries and review results.</span></span> <span data-ttu-id="852c4-372">如需指示，請參閱[建置及查詢 hello 入口網站中的索引](search-get-started-portal.md#query-index)。</span><span class="sxs-lookup"><span data-stu-id="852c4-372">For instructions, see [Build and query an index in hello portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="852c4-373">請嘗試其他查詢語法，從 hello[搜尋文件](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples)範例 > 一節或從[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)hello 入口網站中的搜尋總管 中。</span><span class="sxs-lookup"><span data-stu-id="852c4-373">Try additional query syntax from hello [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in hello portal.</span></span>

+ <span data-ttu-id="852c4-374">檢閱[計分設定檔](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)如果您想 tootune 排名搜尋應用程式中。</span><span class="sxs-lookup"><span data-stu-id="852c4-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want tootune ranking in your search application.</span></span>

+ <span data-ttu-id="852c4-375">深入了解如何 tooapply[特定語言的語彙分析器](https://docs.microsoft.com/rest/api/searchservice/language-support)。</span><span class="sxs-lookup"><span data-stu-id="852c4-375">Learn how tooapply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="852c4-376">[設定自訂分析器](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search)以進行最少的處理，或是在特定欄位上進行特殊的處理。</span><span class="sxs-lookup"><span data-stu-id="852c4-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

+ <span data-ttu-id="852c4-377">在這個示範網站上同時[比較標準和英文分析器](http://alice.unearth.ai/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="852c4-377">[Compare standard and English analyzers](http://alice.unearth.ai/)) side-by-side on this demo web site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="852c4-378">另請參閱</span><span class="sxs-lookup"><span data-stu-id="852c4-378">See also</span></span>

[<span data-ttu-id="852c4-379">搜尋文件 REST API</span><span class="sxs-lookup"><span data-stu-id="852c4-379">Search Documents REST API</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[<span data-ttu-id="852c4-380">簡單查詢語法</span><span class="sxs-lookup"><span data-stu-id="852c4-380">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[<span data-ttu-id="852c4-381">完整的 Lucene 查詢語法</span><span class="sxs-lookup"><span data-stu-id="852c4-381">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[<span data-ttu-id="852c4-382">處理搜尋結果</span><span class="sxs-lookup"><span data-stu-id="852c4-382">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
