---
title: "Azure 搜尋服務的 Lucene 查詢範例 | Microsoft Docs"
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
ms.openlocfilehash: bfd044f333087d8e3e9526820196be6eaec2f18f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a><span data-ttu-id="e26dc-103">在 Azure 搜尋服務中建置查詢的 Lucene 查詢語法範例</span><span class="sxs-lookup"><span data-stu-id="e26dc-103">Lucene query syntax examples for building queries in Azure Search</span></span>
<span data-ttu-id="e26dc-104">建構 Azure 搜尋服務的查詢時，您可以使用預設的[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)或替代的 [Azure 搜尋服務 Lucene 查詢剖析器](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)。</span><span class="sxs-lookup"><span data-stu-id="e26dc-104">When constructing queries for Azure Search, you can use either the default [simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) or the alternative [Lucene Query Parser in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).</span></span> <span data-ttu-id="e26dc-105">Lucene 查詢剖析器支援更複雜的查詢建構，例如欄位範圍查詢、模糊搜尋、鄰近搜尋、詞彙提升，和規則運算式搜尋。</span><span class="sxs-lookup"><span data-stu-id="e26dc-105">The Lucene Query Parser supports more complex query constructs, such as field-scoped queries, fuzzy search, proximity search, term boosting, and regular expression search.</span></span>

<span data-ttu-id="e26dc-106">在本文中，您可以逐步執行範例，以示範使用完整語法時可用的查詢作業。</span><span class="sxs-lookup"><span data-stu-id="e26dc-106">In this article, you can step through examples demonstrating query operations available when using the full syntax.</span></span>

## <a name="viewing-the-examples-in-jsfiddle"></a><span data-ttu-id="e26dc-107">檢視 JSFiddle 中的範例</span><span class="sxs-lookup"><span data-stu-id="e26dc-107">Viewing the examples in JSFiddle</span></span>

<span data-ttu-id="e26dc-108">本文中的所有範例是針對在 [JSFiddle](https://jsfiddle.net) 中預先載入的搜尋索引執行的可執行檔查詢，JSFiddle 是測試指令碼和 HTML 的線上程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="e26dc-108">All of the examples in this article are executable queries that run against a pre-loaded Search index in [JSFiddle](https://jsfiddle.net), an online code editor for testing script and HTML.</span></span> 

<span data-ttu-id="e26dc-109">若要執行這些範例，請以滑鼠右鍵按一下查詢範例 URL，以在個別瀏覽器視窗中開啟 JSFiddle。</span><span class="sxs-lookup"><span data-stu-id="e26dc-109">To run them, right-click on the query example URLs to open JSFiddle in a separate browser window.</span></span>

> [!NOTE]
> <span data-ttu-id="e26dc-110">下列範例會根據 [紐約市 OpenData](https://nycopendata.socrata.com/) 計劃所提供的資料集，利用由可用工作所組成的搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="e26dc-110">The following examples leverage a search index consisting of jobs available based on a dataset provided by the [City of New York OpenData](https://nycopendata.socrata.com/) initiative.</span></span> <span data-ttu-id="e26dc-111">這項資料不應視為目前的或已完成。</span><span class="sxs-lookup"><span data-stu-id="e26dc-111">This data should not be considered current or complete.</span></span> <span data-ttu-id="e26dc-112">索引位於由 Microsoft 提供的沙箱服務上。</span><span class="sxs-lookup"><span data-stu-id="e26dc-112">The index is on a sandbox service provided by Microsoft.</span></span> <span data-ttu-id="e26dc-113">您不需要 Azure 訂用帳戶或 Azure 搜尋服務即可嘗試這些查詢。</span><span class="sxs-lookup"><span data-stu-id="e26dc-113">You do not need an Azure subscription or Azure Search to try these queries.</span></span>
>


## <a name="how-to-invoke-full-lucene-parsing"></a><span data-ttu-id="e26dc-114">如何叫用完整 Lucene 剖析</span><span class="sxs-lookup"><span data-stu-id="e26dc-114">How to invoke full Lucene parsing</span></span>

<span data-ttu-id="e26dc-115">本文中的所有範例會指定 **queryType=full** 搜尋參數，表示 Lucene 查詢剖析器所處理的完整語法。</span><span class="sxs-lookup"><span data-stu-id="e26dc-115">All of the examples in this article specify the **queryType=full** search parameter, indicating that the full syntax, handled by the Lucene Query Parser.</span></span> 

<span data-ttu-id="e26dc-116">**範例 1** -- 以滑鼠右鍵按一下下列查詢程式碼片段，以在載入 JSFiddle 及執行查詢的新瀏覽器頁面上將其開啟：</span><span class="sxs-lookup"><span data-stu-id="e26dc-116">**Example 1** -- Right-click the following query snippet to open it in a new browser page that loads JSFiddle and runs the query:</span></span>

* [<span data-ttu-id="e26dc-117">&queryType=full&search=*</span><span class="sxs-lookup"><span data-stu-id="e26dc-117">&queryType=full&search=*</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

<span data-ttu-id="e26dc-118">在新的瀏覽器視窗中，JavaScript 來源和 HTML 輸出並排顯示。</span><span class="sxs-lookup"><span data-stu-id="e26dc-118">In the new browser window, the JavaScript source and HTML output are presented side by side.</span></span> <span data-ttu-id="e26dc-119">指令碼會參考完整查詢 (而不只是連結中所示的程式碼片段)。</span><span class="sxs-lookup"><span data-stu-id="e26dc-119">The script references a full query (not just the snippet, as shown in the link).</span></span> <span data-ttu-id="e26dc-120">每個範例的 URL 中會顯示完整查詢。</span><span class="sxs-lookup"><span data-stu-id="e26dc-120">The full query is shown in the URLs for each example.</span></span> 

<span data-ttu-id="e26dc-121">此查詢會從紐約市工作索引 (在沙箱服務上載入的 nycjobs) 傳回文件。</span><span class="sxs-lookup"><span data-stu-id="e26dc-121">This query returns documents from our New York City Jobs index (nycjobs, loaded on a sandbox service).</span></span> <span data-ttu-id="e26dc-122">為求簡潔，查詢會指定僅傳回公司職稱。</span><span class="sxs-lookup"><span data-stu-id="e26dc-122">For brevity, the query specifies only business titles are returned.</span></span> <span data-ttu-id="e26dc-123">完整基礎查詢如下所示：</span><span class="sxs-lookup"><span data-stu-id="e26dc-123">The full underlying query is as follows:</span></span>

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

<span data-ttu-id="e26dc-124">**searchFields** 參數會將搜尋限制在商務標題欄位。</span><span class="sxs-lookup"><span data-stu-id="e26dc-124">The **searchFields** parameter restricts the search to just the business title field.</span></span> <span data-ttu-id="e26dc-125">**queryType** 設為 **full**，指示 Azure 搜尋服務對這個查詢使用 Lucene 查詢剖析器。</span><span class="sxs-lookup"><span data-stu-id="e26dc-125">The **queryType** is set to **full**, which instructs Azure Search to use the Lucene Query Parser for this query.</span></span>

> [!NOTE]
> <span data-ttu-id="e26dc-126">如需有關查詢處理的背景知識，請參閱[全文檢索搜尋如何在 Azure 搜尋服務中運作](search-lucene-query-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="e26dc-126">For background on query processing, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span> <span data-ttu-id="e26dc-127">如需搜尋參數的詳細資訊，請參閱 [Search Documents (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) (搜尋文件 (Azure 搜尋服務 REST API))。</span><span class="sxs-lookup"><span data-stu-id="e26dc-127">For more information on search parameters, see [Search Documents (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span>
>

### <a name="fielded-query-operation"></a><span data-ttu-id="e26dc-128">加入欄位的查詢作業</span><span class="sxs-lookup"><span data-stu-id="e26dc-128">Fielded query operation</span></span>
<span data-ttu-id="e26dc-129">您可以修改本文中的範例：指定 **fieldname:searchterm** 建構來定義加入欄位的查詢作業，其中欄位是單一文字，而搜尋詞彙也是一個單一文字或片語，選擇性使用布林運算子。</span><span class="sxs-lookup"><span data-stu-id="e26dc-129">You can modify the examples in this article by specifying a **fieldname:searchterm** construction to define a fielded query operation, where the field is a single word, and the search term is also a single word or a phrase, optionally with Boolean operators.</span></span> <span data-ttu-id="e26dc-130">某些範例包括以下內容：</span><span class="sxs-lookup"><span data-stu-id="e26dc-130">Some examples include the following:</span></span>

* <span data-ttu-id="e26dc-131">business_title:(senior NOT junior)</span><span class="sxs-lookup"><span data-stu-id="e26dc-131">business_title:(senior NOT junior)</span></span>
* <span data-ttu-id="e26dc-132">state:("New York" AND "New Jersey")</span><span class="sxs-lookup"><span data-stu-id="e26dc-132">state:("New York" AND "New Jersey")</span></span>

<span data-ttu-id="e26dc-133">如果您想要將字串視為單一實體評估，請務必將多個字串放在引號中，例如搜尋 [位置] 欄位中兩個不同城市的情況。</span><span class="sxs-lookup"><span data-stu-id="e26dc-133">Be sure to put multiple strings within quotation marks if you want both strings to be evaluated as a single entity, as in this case searching for two distinct cities in the location field.</span></span> <span data-ttu-id="e26dc-134">此外，請確定運算子是大寫，如同您看到的 NOT 和 AND。</span><span class="sxs-lookup"><span data-stu-id="e26dc-134">Also, ensure the operator is capitalized as you see with NOT and AND.</span></span>

<span data-ttu-id="e26dc-135">**fieldname:searchterm** 中指定的欄位必須是可搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="e26dc-135">The field specified in **fieldname:searchterm** must be a searchable field.</span></span> <span data-ttu-id="e26dc-136">如需欄位定義中索引屬性使用方式的詳細資訊，請參閱 [建立索引 (Azure 搜尋服務 REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) 。</span><span class="sxs-lookup"><span data-stu-id="e26dc-136">See [Create Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) for details on how index attributes are used in field definitions.</span></span>

<span data-ttu-id="e26dc-137">**範例 2** -- 以滑鼠右鍵按一下下列查詢程式碼片段。此查詢會搜尋包含 senior 詞彙的公司職稱，而不是包含 junior：</span><span class="sxs-lookup"><span data-stu-id="e26dc-137">**Example 2** -- Right-click the following query snippet This query searches for business titles with the term senior in them, but not junior:</span></span>

* [<span data-ttu-id="e26dc-138">&queryType=full&search= business_title:senior NOT junior</span><span class="sxs-lookup"><span data-stu-id="e26dc-138">&queryType=full&search= business_title:senior NOT junior</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a><span data-ttu-id="e26dc-139">模糊搜尋範例</span><span class="sxs-lookup"><span data-stu-id="e26dc-139">Fuzzy search example</span></span>
<span data-ttu-id="e26dc-140">模糊搜尋會尋找具有類似建構的相符項目。</span><span class="sxs-lookup"><span data-stu-id="e26dc-140">A fuzzy search finds matches in terms that have a similar construction.</span></span> <span data-ttu-id="e26dc-141">在每個 [Lucene 文件](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html)中，模糊搜尋以 [Damerau-Levenshtein 距離](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance)為基礎。</span><span class="sxs-lookup"><span data-stu-id="e26dc-141">Per [Lucene documentation](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), fuzzy searches are based on [Damerau-Levenshtein Distance](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).</span></span>

<span data-ttu-id="e26dc-142">若要執行模糊搜尋，請在單一文字結尾附加波狀符號 "~"，加上選擇性參數，介於 0 和 2 之間且指定編輯距離的值。</span><span class="sxs-lookup"><span data-stu-id="e26dc-142">To do a fuzzy search, append the tilde "~" symbol at the end of a single word with an optional parameter, a value between 0 and 2, that specifies the edit distance.</span></span> <span data-ttu-id="e26dc-143">比方說，"blue~" 或 "blue~1" 會傳回 blue、blues 和 glue。</span><span class="sxs-lookup"><span data-stu-id="e26dc-143">For example, "blue~" or "blue~1" would return blue, blues, and glue.</span></span>

<span data-ttu-id="e26dc-144">**範例 3** -- 以滑鼠右鍵按一下下列查詢程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e26dc-144">**Example 3** -- Right-click the following query snippet.</span></span> <span data-ttu-id="e26dc-145">此查詢會搜尋具有詞彙關聯的工作 (其中有拼字錯誤)︰</span><span class="sxs-lookup"><span data-stu-id="e26dc-145">This query searches for jobs with the term associate (where it is misspelled):</span></span>

* [<span data-ttu-id="e26dc-146">&queryType=full&search= business_title:asosiate~</span><span class="sxs-lookup"><span data-stu-id="e26dc-146">&queryType=full&search= business_title:asosiate~</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> <span data-ttu-id="e26dc-147">不會[分析](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis)模糊查詢，如果您預期詞幹分析或詞形歸併還原，可能會對此感到意外。</span><span class="sxs-lookup"><span data-stu-id="e26dc-147">Fuzzy queries are not [analyzed](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), which can be surprising if you expect stemming or lemmatization.</span></span> <span data-ttu-id="e26dc-148">只能對完整詞彙執行語彙分析 (詞彙查詢或片語查詢)。</span><span class="sxs-lookup"><span data-stu-id="e26dc-148">Lexical analysis is only performed on complete terms (a term query or phrase query).</span></span> <span data-ttu-id="e26dc-149">不完整詞彙的查詢類型 (前置詞查詢、萬用字元查詢、Regex 查詢、模糊查詢) 會直接新增至查詢樹狀結構，並略過分析階段。</span><span class="sxs-lookup"><span data-stu-id="e26dc-149">Query types with incomplete terms (prefix query, wildcard query, regex query, fuzzy query) are added directly to the query tree, bypassing the analysis stage.</span></span> <span data-ttu-id="e26dc-150">只能對不完整的查詢詞彙執行小寫轉換。</span><span class="sxs-lookup"><span data-stu-id="e26dc-150">The only transformation performed on incomplete query terms is lowercasing.</span></span>
>

## <a name="proximity-search-example"></a><span data-ttu-id="e26dc-151">鄰近搜尋範例</span><span class="sxs-lookup"><span data-stu-id="e26dc-151">Proximity search example</span></span>
<span data-ttu-id="e26dc-152">鄰近搜尋可用來尋找文件中彼此相近的詞彙。</span><span class="sxs-lookup"><span data-stu-id="e26dc-152">Proximity searches are used to find terms that are near each other in a document.</span></span> <span data-ttu-id="e26dc-153">在片語的結尾插入波狀符號 "~"，後面加上建立鄰近界限的字數。</span><span class="sxs-lookup"><span data-stu-id="e26dc-153">Insert a tilde "~" symbol at the end of a phrase followed by the number of words that create the proximity boundary.</span></span> <span data-ttu-id="e26dc-154">例如，"hotel airport"~5 會在文件中每 5 個字內尋找旅館和機場等詞彙。</span><span class="sxs-lookup"><span data-stu-id="e26dc-154">For example, "hotel airport"~5 will find the terms hotel and airport within 5 words of each other in a document.</span></span>

<span data-ttu-id="e26dc-155">**範例 4** -- 以滑鼠右鍵按一下查詢。</span><span class="sxs-lookup"><span data-stu-id="e26dc-155">**Example 4** -- Right-click the query.</span></span> <span data-ttu-id="e26dc-156">搜尋詞彙 "senior analyst"，且其中將其分隔的字數不得超過一個字︰</span><span class="sxs-lookup"><span data-stu-id="e26dc-156">Search for jobs with the term "senior analyst" where it is separated by no more than one word:</span></span>

* [<span data-ttu-id="e26dc-157">&queryType=full&search=business_title:"senior analyst"~1</span><span class="sxs-lookup"><span data-stu-id="e26dc-157">&queryType=full&search=business_title:"senior analyst"~1</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

<span data-ttu-id="e26dc-158">**範例 5** -- 再試一次，移除 "senior analyst" 一詞之間的單字。</span><span class="sxs-lookup"><span data-stu-id="e26dc-158">**Example 5** -- Try it again removing the words between the term "senior analyst".</span></span>

* [<span data-ttu-id="e26dc-159">&queryType=full&search=business_title:"senior analyst"~0</span><span class="sxs-lookup"><span data-stu-id="e26dc-159">&queryType=full&search=business_title:"senior analyst"~0</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a><span data-ttu-id="e26dc-160">提升詞彙範例</span><span class="sxs-lookup"><span data-stu-id="e26dc-160">Term boosting examples</span></span>
<span data-ttu-id="e26dc-161">提升一詞指的是如果文件包含提升詞彙，則將其評等提高，高於不包含該詞彙的文件。</span><span class="sxs-lookup"><span data-stu-id="e26dc-161">Term boosting refers to ranking a document higher if it contains the boosted term, relative to documents that do not contain the term.</span></span> <span data-ttu-id="e26dc-162">這與評分設定檔的不同之處在於評分設定檔會提升特定欄位，而不是特定詞彙。</span><span class="sxs-lookup"><span data-stu-id="e26dc-162">This differs from scoring profiles in that scoring profiles boost certain fields, rather than specific terms.</span></span> <span data-ttu-id="e26dc-163">下列範例可協助說明差異。</span><span class="sxs-lookup"><span data-stu-id="e26dc-163">The following example helps illustrate the differences.</span></span>

<span data-ttu-id="e26dc-164">請考慮使用評分設定檔，可提高特定欄位中的相符項目，例如 musicstoreindex 範例中的 **genre** 。</span><span class="sxs-lookup"><span data-stu-id="e26dc-164">Consider a scoring profile that boosts matches in a certain field, such as **genre** in the musicstoreindex example.</span></span> <span data-ttu-id="e26dc-165">詞彙提升可用來進一步提升某些搜尋詞彙，使其高於其他詞彙。</span><span class="sxs-lookup"><span data-stu-id="e26dc-165">Term boosting could be used to further boost certain search terms higher than others.</span></span> <span data-ttu-id="e26dc-166">比方說，"rock^2 electronic" 可提升包含搜尋詞彙的文件﹐使其在 [genre]  欄位中高於索引中的其他可搜尋欄位。</span><span class="sxs-lookup"><span data-stu-id="e26dc-166">For example, "rock^2 electronic" will boost documents that contain the search terms in the **genre** field higher than other searchable fields in the index.</span></span> <span data-ttu-id="e26dc-167">此外，包含搜尋詞彙 "rock" 的文件排名會比另一個搜尋詞彙 "electronic" 還高，此為詞彙提升值 (2) 的結果。</span><span class="sxs-lookup"><span data-stu-id="e26dc-167">Furthermore, documents that contain the search term "rock" will be ranked higher than the other search term "electronic" as a result of the term boost value (2).</span></span>

<span data-ttu-id="e26dc-168">若要提升詞彙，請使用插入號 "^"，並在搜尋詞彙的結尾加上提升係數 (數字)。</span><span class="sxs-lookup"><span data-stu-id="e26dc-168">To boost a term, use the caret, "^", symbol with a boost factor (a number) at the end of the term you are searching.</span></span> <span data-ttu-id="e26dc-169">提升係數越高，該詞彙相對於其他搜尋詞彙的關聯性也越高。</span><span class="sxs-lookup"><span data-stu-id="e26dc-169">The higher the boost factor, the more relevant the term will be relative to other search terms.</span></span> <span data-ttu-id="e26dc-170">根據預設，提升係數為 1。</span><span class="sxs-lookup"><span data-stu-id="e26dc-170">By default, the boost factor is 1.</span></span> <span data-ttu-id="e26dc-171">雖然提升係數必須是正數，但是它可能會小於 1 (例如，0.2)。</span><span class="sxs-lookup"><span data-stu-id="e26dc-171">Although the boost factor must be positive, it can be less than 1 (for example, 0.2).</span></span>

<span data-ttu-id="e26dc-172">**範例 6** -- 以滑鼠右鍵按一下查詢。</span><span class="sxs-lookup"><span data-stu-id="e26dc-172">**Example 6**  -- Right-click the query.</span></span> <span data-ttu-id="e26dc-173">搜尋包含詞彙「電腦分析師 (computer analyst)」的工作時，我們會發現包含電腦和分析師兩個單字的搜尋沒有結果，但是分析師工作會顯示在結果的頂端。</span><span class="sxs-lookup"><span data-stu-id="e26dc-173">Search for jobs with the term "computer analyst" where we see there are no results with both words computer and analyst, yet analyst jobs are at the top of the results.</span></span>

* [<span data-ttu-id="e26dc-174">&queryType=full&search=business_title:computer analyst</span><span class="sxs-lookup"><span data-stu-id="e26dc-174">&queryType=full&search=business_title:computer analyst</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

<span data-ttu-id="e26dc-175">**範例 7** -- 再試一次，在兩個單字並沒有同時存在的情況下，這一次提升包含電腦一詞的結果，高於包含分析師一詞。</span><span class="sxs-lookup"><span data-stu-id="e26dc-175">**Example 7**  --  Try it again, this time boosting results with the term computer over the term analyst if both words do not exist.</span></span>

* [<span data-ttu-id="e26dc-176">&queryType=full&search=business_title:computer^2 analyst</span><span class="sxs-lookup"><span data-stu-id="e26dc-176">&queryType=full&search=business_title:computer^2 analyst</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a><span data-ttu-id="e26dc-177">規則運算式範例</span><span class="sxs-lookup"><span data-stu-id="e26dc-177">Regular expression example</span></span>
<span data-ttu-id="e26dc-178">規則運算式搜尋會根據正斜線 "/" 之間的內容尋找相符項目，如 [RegExp 類別](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html)中所記錄。</span><span class="sxs-lookup"><span data-stu-id="e26dc-178">A regular expression search finds a match based on the contents between forward slashes "/", as documented in the [RegExp class](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).</span></span>

<span data-ttu-id="e26dc-179">**範例 8** -- 以滑鼠右鍵按一下查詢。</span><span class="sxs-lookup"><span data-stu-id="e26dc-179">**Example 8** -- Right-click the query.</span></span> <span data-ttu-id="e26dc-180">搜尋包含 Senior 或 Junior 詞彙的工作。</span><span class="sxs-lookup"><span data-stu-id="e26dc-180">Search for jobs with either the term Senior or Junior.</span></span>

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

<span data-ttu-id="e26dc-181">在頁面中，此範例的 URL 將無法正確轉譯。</span><span class="sxs-lookup"><span data-stu-id="e26dc-181">The URL for this example will not render properly in the page.</span></span> <span data-ttu-id="e26dc-182">解決的方法是複製下列 URL 並將它貼到瀏覽器 URL 位址︰`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`</span><span class="sxs-lookup"><span data-stu-id="e26dc-182">As a workaround, copy the URL below and paste it into the browser URL address: `http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`</span></span>

## <a name="wildcard-search-example"></a><span data-ttu-id="e26dc-183">萬用字元搜尋範例</span><span class="sxs-lookup"><span data-stu-id="e26dc-183">Wildcard search example</span></span>
<span data-ttu-id="e26dc-184">您可以使用一般辨識語法進行多個 (\*) 或單一 (?) 字元的萬用字元搜尋。</span><span class="sxs-lookup"><span data-stu-id="e26dc-184">You can use generally recognized syntax for multiple (\*) or single (?) character wildcard searches.</span></span> <span data-ttu-id="e26dc-185">請注意，Lucene 查詢剖析器支援搭配使用這些符號與單一詞彙，而不是片語。</span><span class="sxs-lookup"><span data-stu-id="e26dc-185">Note the Lucene query parser supports the use of these symbols with a single term, and not a phrase.</span></span>

<span data-ttu-id="e26dc-186">**範例 9** -- 以滑鼠右鍵按一下查詢。</span><span class="sxs-lookup"><span data-stu-id="e26dc-186">**Example 9** -- Right-click the  query.</span></span> <span data-ttu-id="e26dc-187">搜尋包含前置詞 'prog' 的工作，其中包括內含程式設計 (programming) 與程式設計人員 (programmer) 的職稱。</span><span class="sxs-lookup"><span data-stu-id="e26dc-187">Search for jobs that contain the prefix 'prog' which would include business titles with the terms programming and programmer in it.</span></span>

* [<span data-ttu-id="e26dc-188">&queryType=full&$select=business_title&search=business_title:prog*</span><span class="sxs-lookup"><span data-stu-id="e26dc-188">&queryType=full&$select=business_title&search=business_title:prog*</span></span>](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

<span data-ttu-id="e26dc-189">您無法使用 * 或 ?</span><span class="sxs-lookup"><span data-stu-id="e26dc-189">You cannot use a * or ?</span></span> <span data-ttu-id="e26dc-190">符號做為搜尋的第一個字元。</span><span class="sxs-lookup"><span data-stu-id="e26dc-190">symbol as the first character of a search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26dc-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e26dc-191">Next steps</span></span>
<span data-ttu-id="e26dc-192">請在您的程式碼中嘗試指定 Lucene 查詢剖析器。</span><span class="sxs-lookup"><span data-stu-id="e26dc-192">Try specifying the Lucene Query Parser in your code.</span></span> <span data-ttu-id="e26dc-193">下列連結說明如何設定 .NET 和 REST API 的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="e26dc-193">The following links explain how to set up search queries for both .NET and the REST API.</span></span> <span data-ttu-id="e26dc-194">這些連結會使用預設的簡單語法，因此您必須套用您從本文了解的內容來指定 **queryType**。</span><span class="sxs-lookup"><span data-stu-id="e26dc-194">The links use the default simple syntax so you will need to apply what you learned from this article to specify the **queryType**.</span></span>

* [<span data-ttu-id="e26dc-195">使用 .NET SDK 查詢 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="e26dc-195">Query your Azure Search Index using the .NET SDK</span></span>](search-query-dotnet.md)
* [<span data-ttu-id="e26dc-196">使用 REST API 查詢 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="e26dc-196">Query your Azure Search Index using the REST API</span></span>](search-query-rest-api.md)

## <a name="see-also"></a><span data-ttu-id="e26dc-197">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e26dc-197">See also</span></span>

 [<span data-ttu-id="e26dc-198">全文檢索搜尋如何在 Azure 搜尋服務中運作</span><span class="sxs-lookup"><span data-stu-id="e26dc-198">How full text search works in Azure Search</span></span>](search-lucene-query-architecture.md)