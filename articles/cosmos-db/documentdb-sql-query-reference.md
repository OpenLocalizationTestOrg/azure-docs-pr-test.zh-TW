---
title: "Azure Cosmos DB DocumentDB API：SQL 語法 | Microsoft Docs"
description: "Azure Cosmos DB DocumentDB API SQL 查詢語言的參考文件。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="aef6a-103">Azure Cosmos DB DocumentDB API：SQL 語法參考</span><span class="sxs-lookup"><span data-stu-id="aef6a-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="aef6a-104">Azure Cosmos DB DocumentDB API 支援在階層式 JSON 文件上使用像是文法等熟悉的 SQL (結構式查詢語言) 查詢文件，無需明確的結構描述，也不用建立次要索引。</span><span class="sxs-lookup"><span data-stu-id="aef6a-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="aef6a-105">本主題提供 DocumentDB API SQL 查詢語言的參考文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="aef6a-106">如需 DocumentDB API SQL 查詢語言的逐步解說，請參閱 [適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="aef6a-107">我們也邀請您造訪 [Query Playground](http://www.documentdb.com/sql/demo)，您可以在此試用 Azure Cosmos DB 並針對我們的資料集執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="aef6a-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="aef6a-108">SELECT 查詢</span><span class="sxs-lookup"><span data-stu-id="aef6a-108">SELECT query</span></span>  
<span data-ttu-id="aef6a-109">從資料庫擷取 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="aef6a-110">支援運算式評估、規劃、篩選和聯結。</span><span class="sxs-lookup"><span data-stu-id="aef6a-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="aef6a-111">用來描述 SELECT 陳述式的慣例會在「語法」慣例一節中製成資料表。</span><span class="sxs-lookup"><span data-stu-id="aef6a-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="aef6a-112">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="aef6a-113">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-113">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-114">如需每個子句的詳細資料，請參閱下列各節：</span><span class="sxs-lookup"><span data-stu-id="aef6a-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="aef6a-115">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="aef6a-116">FROM 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="aef6a-117">WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="aef6a-118">ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="aef6a-119">SELECT 陳述式中的子句的順序必須如上所述。</span><span class="sxs-lookup"><span data-stu-id="aef6a-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="aef6a-120">您可以省略任一選用子句。</span><span class="sxs-lookup"><span data-stu-id="aef6a-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="aef6a-121">但是，若使用了選用子句，則這些子句必須以正確的順序出現。</span><span class="sxs-lookup"><span data-stu-id="aef6a-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="aef6a-122">**SELECT 陳述式的邏輯處理順序**</span><span class="sxs-lookup"><span data-stu-id="aef6a-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="aef6a-123">子句處理的順序為：</span><span class="sxs-lookup"><span data-stu-id="aef6a-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="aef6a-124">FROM 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="aef6a-125">WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="aef6a-126">ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="aef6a-127">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="aef6a-128">請注意，這裡的順序與語法中子句出現的順序不同。</span><span class="sxs-lookup"><span data-stu-id="aef6a-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="aef6a-129">您可以看到由已處理的子句所導入的所有新符號之順序，也能用於稍後要處理的子句。</span><span class="sxs-lookup"><span data-stu-id="aef6a-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="aef6a-130">例如，您可以在 WHERE 和 SELECT 子句中存取 FROM 子句中宣告的別名。</span><span class="sxs-lookup"><span data-stu-id="aef6a-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="aef6a-131">**空白字元和註解**</span><span class="sxs-lookup"><span data-stu-id="aef6a-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="aef6a-132">所有不屬於括號中的字串或引號識別項的空白字元都不是語言文法的一部分，而且會在剖析時忽略。</span><span class="sxs-lookup"><span data-stu-id="aef6a-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="aef6a-133">查詢語言支援 T-SQL 樣式的註解，例如</span><span class="sxs-lookup"><span data-stu-id="aef6a-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="aef6a-134">陳述式`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="aef6a-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="aef6a-135">若空白字元和註解在文法中不具備任何重要性，則必須用來分隔權杖。</span><span class="sxs-lookup"><span data-stu-id="aef6a-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="aef6a-136">例如：`-1e5` 是單一數字的權杖，而 `: – 1 e5` 則是加上減號的權杖，後面接著數字 1 和識別碼 e5。</span><span class="sxs-lookup"><span data-stu-id="aef6a-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="aef6a-137"><a name="bk_select_query"></a> SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="aef6a-138">SELECT 陳述式中的子句的順序必須如上所述。</span><span class="sxs-lookup"><span data-stu-id="aef6a-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="aef6a-139">您可以省略任一選用子句。</span><span class="sxs-lookup"><span data-stu-id="aef6a-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="aef6a-140">但是，若使用了選用子句，則這些子句必須以正確的順序出現。</span><span class="sxs-lookup"><span data-stu-id="aef6a-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="aef6a-141">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="aef6a-142">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="aef6a-143">要針對此結果集選取的屬性或值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="aef6a-144">指定應該在不做出任何變更的情況下指定該值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="aef6a-145">特別是若已處理的值是物件，則會擷取所有屬性。</span><span class="sxs-lookup"><span data-stu-id="aef6a-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="aef6a-146">指定要擷取的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="aef6a-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="aef6a-147">每個傳回的值都會是具備指定屬性的物件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="aef6a-148">指定應該擷取 JSON 值，而非擷取完整的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="aef6a-149">這與 `<property_list>` 不同，不會在物件中包裝預估的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="aef6a-150">表示要計算之值的運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="aef6a-151">請參閱[純量運算式](#bk_scalar_expressions)一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aef6a-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="aef6a-152">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-152">**Remarks**</span></span>  
  
<span data-ttu-id="aef6a-153">`SELECT *` 語法只有在 FROM 子句已明顯宣告一個別名時才會有效。</span><span class="sxs-lookup"><span data-stu-id="aef6a-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="aef6a-154">`SELECT *` 提供一個身分識別投影，在無需投影的情況下會非常實用。</span><span class="sxs-lookup"><span data-stu-id="aef6a-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="aef6a-155">SELECT * 只有在已指定 FROM 子句且只導入單一輸入來源時才有效。</span><span class="sxs-lookup"><span data-stu-id="aef6a-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="aef6a-156">請注意，`SELECT <select_list>` 和 `SELECT *` 為「語法捷徑」，可以使用如下所示的簡單 SELECT 陳述式另外表示。</span><span class="sxs-lookup"><span data-stu-id="aef6a-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="aef6a-157">相當於：</span><span class="sxs-lookup"><span data-stu-id="aef6a-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="aef6a-158">相當於：</span><span class="sxs-lookup"><span data-stu-id="aef6a-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="aef6a-159">**另請參閱**</span><span class="sxs-lookup"><span data-stu-id="aef6a-159">**See Also**</span></span>  
  
[<span data-ttu-id="aef6a-160">純量運算式</span><span class="sxs-lookup"><span data-stu-id="aef6a-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="aef6a-161">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="aef6a-162"><a name="bk_from_clause"></a>FROM 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="aef6a-163">指定來源或聯結的來源。</span><span class="sxs-lookup"><span data-stu-id="aef6a-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="aef6a-164">FROM 子句為選用子句。</span><span class="sxs-lookup"><span data-stu-id="aef6a-164">The FROM clause is optional.</span></span> <span data-ttu-id="aef6a-165">若未指定，系統仍然會在如同 FROM 子句提供了單一文件的情況下執行其他子句。</span><span class="sxs-lookup"><span data-stu-id="aef6a-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="aef6a-166">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-166">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="aef6a-167">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="aef6a-168">指定包含或不包含別名的資料來源。</span><span class="sxs-lookup"><span data-stu-id="aef6a-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="aef6a-169">若未指定別名，則會使用下列規則從 `<collection_expression>` 加以推斷：</span><span class="sxs-lookup"><span data-stu-id="aef6a-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="aef6a-170">如果運算式為 collection_name，則會使用 collection_name 作為別名。</span><span class="sxs-lookup"><span data-stu-id="aef6a-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="aef6a-171">如果運算式為 `<collection_expression>`，則會使用 property_name、 then property_name 作為別名。</span><span class="sxs-lookup"><span data-stu-id="aef6a-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="aef6a-172">如果運算式為 collection_name，則會使用 collection_name 作為別名。</span><span class="sxs-lookup"><span data-stu-id="aef6a-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="aef6a-173">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="aef6a-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="aef6a-174">指定 `input_alias` 為一組由基礎集合運算式傳回的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="aef6a-175">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="aef6a-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="aef6a-176">指定 `input_alias` 應該代表一組透過反覆計算所有陣列元素所取得的值，其中會依基礎集合運算式傳回每個陣列。</span><span class="sxs-lookup"><span data-stu-id="aef6a-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="aef6a-177">會忽略任何由基礎集合運算式傳回的任何非陣列的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="aef6a-178">指定要用來擷取文件的集合運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="aef6a-179">指定應該從預設、目前的連線集合中擷取文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="aef6a-180">指定應該從提供的連線集合中擷取文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="aef6a-181">集合名稱必須符合目前連線的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="aef6a-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="aef6a-182">指定應該從由提供的別名定義的其他來源擷取文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="aef6a-183">指定文件應該透過存取 `property_name` 屬性或 array_index 陣列元素加以擷取，其中所文件均依指定的集合運算式擷取。</span><span class="sxs-lookup"><span data-stu-id="aef6a-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="aef6a-184">指定文件應該透過存取 `property_name` 屬性或 array_index 陣列元素加以擷取，其中所文件均依指定的集合運算式擷取。</span><span class="sxs-lookup"><span data-stu-id="aef6a-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="aef6a-185">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-185">**Remarks**</span></span>  
  
<span data-ttu-id="aef6a-186">`<from_source>(`中提供的所有別名或推斷) 必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="aef6a-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="aef6a-187">語法 `<collection_expression>.`property_name 與 `<collection_expression>' ['"property_name"']'` 相同。</span><span class="sxs-lookup"><span data-stu-id="aef6a-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="aef6a-188">不過，若屬性名稱包含非識別碼字元，則可以使用後者的語法。</span><span class="sxs-lookup"><span data-stu-id="aef6a-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="aef6a-189">**遺漏的屬性、遺漏的陣列元素、未定義的值處理**</span><span class="sxs-lookup"><span data-stu-id="aef6a-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="aef6a-190">若集合運算式存取屬性或陣列元素，且該值不存在，則會忽略該值且不會進一步處理。</span><span class="sxs-lookup"><span data-stu-id="aef6a-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="aef6a-191">**集合運算式內容範圍**</span><span class="sxs-lookup"><span data-stu-id="aef6a-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="aef6a-192">集合運算方式可以是集合範圍或文件範圍：</span><span class="sxs-lookup"><span data-stu-id="aef6a-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="aef6a-193">若集合運算式的基礎來源為 ROOT 或 `collection_name`，則運算式為集合範圍。</span><span class="sxs-lookup"><span data-stu-id="aef6a-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="aef6a-194">這類運算式代表一組直接從集合中擷取的文件，並不會相依於其他集合運算式的處理。</span><span class="sxs-lookup"><span data-stu-id="aef6a-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="aef6a-195">若集合運算式的基礎來源為之前在查詢中導入的 `input_alias`，則運算式為文件範圍。</span><span class="sxs-lookup"><span data-stu-id="aef6a-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="aef6a-196">這類運算式代表一組文件，這組文件是透過評估屬於與別名集合相關聯之集的每個文件範圍的集合運算式而取得。</span><span class="sxs-lookup"><span data-stu-id="aef6a-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="aef6a-197">結果集會是透過評估基礎集中每個文件的集合運算式所獲得的聯集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="aef6a-198">**聯結**</span><span class="sxs-lookup"><span data-stu-id="aef6a-198">**Joins**</span></span>  
  
<span data-ttu-id="aef6a-199">在目前版本中，Azure Cosmos DB 支援內部聯結。</span><span class="sxs-lookup"><span data-stu-id="aef6a-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="aef6a-200">即將推出其他聯結功能。</span><span class="sxs-lookup"><span data-stu-id="aef6a-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="aef6a-201">內部聯結是參與聯結之集的完整交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="aef6a-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="aef6a-202">N 方聯結的結果為一組 N 元素 Tuple，其中 Tuple 中的每個值都與參與聯結的別名集相關聯，而且可以透過參考其他子句中的別名加以存取。</span><span class="sxs-lookup"><span data-stu-id="aef6a-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="aef6a-203">聯結的評估依參與集的內容範圍而定：</span><span class="sxs-lookup"><span data-stu-id="aef6a-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="aef6a-204">集合組 A 和集合範圍組 B 之間的聯結會產生集合 A 和 B 中所有元素的交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="aef6a-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="aef6a-205">集合組 A 和文件範圍組 B 之間的聯結會產生所有集合的聯集，是依評估集合 A 的每個文件的文件範圍集合 B 來取得。</span><span class="sxs-lookup"><span data-stu-id="aef6a-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="aef6a-206">在目前的版本中，查詢處理器支援集合範圍運算式的上限。</span><span class="sxs-lookup"><span data-stu-id="aef6a-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="aef6a-207">**聯結範例：**</span><span class="sxs-lookup"><span data-stu-id="aef6a-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="aef6a-208">我們來看看下面的 FROM 子句：`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="aef6a-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="aef6a-209">讓每個來源定義 `input_alias1, input_alias2, …, input_aliasN`。</span><span class="sxs-lookup"><span data-stu-id="aef6a-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="aef6a-210">這個 FROM 子句會傳回一組 N-Tuple (具有 N 個值的 Tuple)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="aef6a-211">每個 Tuple 所擁有的值，都是將所有集合別名在其個別集合上反覆運算所產生。</span><span class="sxs-lookup"><span data-stu-id="aef6a-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="aef6a-212">*JOIN 範例 1，搭配 2 個來源：*</span><span class="sxs-lookup"><span data-stu-id="aef6a-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="aef6a-213">讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="aef6a-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="aef6a-214">讓 `<from_source2>` 為參照 input_alias1 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="aef6a-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="aef6a-215">{1, 2} 為 `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="aef6a-216">{3} 為 `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="aef6a-217">{4, 5} 為 `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="aef6a-218">FROM 子句 `<from_source1> JOIN <from_source2>` 會產生下列 Tuple：</span><span class="sxs-lookup"><span data-stu-id="aef6a-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="aef6a-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="aef6a-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="aef6a-220">*JOIN 範例 2，搭配 3 個來源：*</span><span class="sxs-lookup"><span data-stu-id="aef6a-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="aef6a-221">讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="aef6a-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="aef6a-222">讓 `<from_source2>` 為參照 `input_alias1` 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="aef6a-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="aef6a-223">{1, 2} 為 `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="aef6a-224">{3} 為 `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="aef6a-225">{4, 5} 為 `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="aef6a-226">讓 `<from_source3>` 為參照 `input_alias2` 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="aef6a-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="aef6a-227">{100, 200} 為 `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="aef6a-228">{300}為 `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="aef6a-229">FROM 子句 `<from_source1> JOIN <from_source2> JOIN <from_source3>` 會產生下列 Tuple：</span><span class="sxs-lookup"><span data-stu-id="aef6a-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="aef6a-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="aef6a-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="aef6a-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="aef6a-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="aef6a-232">缺少 `input_alias1`、`input_alias2` 的其他值 Tuple，其中 `<from_source3>` 並未傳回任何值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="aef6a-233">*JOIN 範例 3，搭配 3 個來源：*</span><span class="sxs-lookup"><span data-stu-id="aef6a-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="aef6a-234">讓 <from_source1> 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="aef6a-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="aef6a-235">讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="aef6a-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="aef6a-236">讓 <from_source2> 為參照 input_alias1 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="aef6a-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="aef6a-237">{1, 2} 為 `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="aef6a-238">{3} 為 `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="aef6a-239">{4, 5} 為 `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="aef6a-240">讓 `<from_source3>` 將範圍設定為 `input_alias1` 並代表集：</span><span class="sxs-lookup"><span data-stu-id="aef6a-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="aef6a-241">{100, 200} 為 `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="aef6a-242">{300}為 `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="aef6a-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="aef6a-243">FROM 子句 `<from_source1> JOIN <from_source2> JOIN <from_source3>` 會產生下列 Tuple：</span><span class="sxs-lookup"><span data-stu-id="aef6a-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="aef6a-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="aef6a-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="aef6a-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="aef6a-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="aef6a-246">這會在 `<from_source2>` 和 `<from_source3>` 之間產生交叉乘積，因為兩者都只限於相同的 `<from_source1>` 範圍。</span><span class="sxs-lookup"><span data-stu-id="aef6a-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="aef6a-247">這會讓 4 (2x2) Tuple 具備值 A，0 Tuple 具備值 B (1x0) 而 2 (2x1) Tuple 具備值 C。</span><span class="sxs-lookup"><span data-stu-id="aef6a-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="aef6a-248">**另請參閱**</span><span class="sxs-lookup"><span data-stu-id="aef6a-248">**See also**</span></span>  
  
 [<span data-ttu-id="aef6a-249">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="aef6a-250"><a name="bk_where_clause"></a>WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="aef6a-251">指定查詢所傳回的文件之搜尋條件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="aef6a-252">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="aef6a-253">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="aef6a-254">指定要傳回的文件必須滿足的條件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="aef6a-255">表示要計算之值的運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="aef6a-256">請參閱[純量運算式](#bk_scalar_expressions)一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aef6a-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="aef6a-257">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-257">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-258">為了傳回文件，指定為篩選條件的運算式必須評估為 True。</span><span class="sxs-lookup"><span data-stu-id="aef6a-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="aef6a-259">只有在布林值為 True 的情況下才會滿足條件，任何其他值：未定義、Null、False、數字、陣列或物件都不會滿足條件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="aef6a-260"><a name="bk_orderby_clause"></a>ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="aef6a-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="aef6a-261">指定由查詢傳回之結果的排列順序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="aef6a-262">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="aef6a-263">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="aef6a-264">指定要排列查詢結果集的屬性或運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="aef6a-265">排序資料行可指定為名稱或資料行別名。</span><span class="sxs-lookup"><span data-stu-id="aef6a-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="aef6a-266">可以指定多個排序資料行。</span><span class="sxs-lookup"><span data-stu-id="aef6a-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="aef6a-267">資料行必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="aef6a-267">Column names must be unique.</span></span> <span data-ttu-id="aef6a-268">ORDER BY 子句中的排序資料行順序會定義已排序結果集的組織。</span><span class="sxs-lookup"><span data-stu-id="aef6a-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="aef6a-269">也就是說，結果集是依第一個屬性排序，而該排序清單會依次要屬性進行排序，以此類推。</span><span class="sxs-lookup"><span data-stu-id="aef6a-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="aef6a-270">ORDER BY 子句中參照的資料行名稱必須明確對應至選取清單中的資料行，或在 FROM 子句中指定之資料表中定義的資料行。</span><span class="sxs-lookup"><span data-stu-id="aef6a-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="aef6a-271">指定要排列查詢結果集的單一屬性或運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="aef6a-272">請參閱[純量運算式](#bk_scalar_expressions)一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aef6a-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="aef6a-273">指定特定之資料行中的值，應該以遞增或遞減順序排序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="aef6a-274">ASC 從最低值到最高值排序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="aef6a-275">DESC 從最高值到最低值排序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="aef6a-276">ASC 為預設排序順序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-276">ASC is the default sort order.</span></span> <span data-ttu-id="aef6a-277">NULL 值會被視為最低的可能值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="aef6a-278">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-278">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-279">即使查詢文法支援多個屬性順序，但 Azure Cosmos DB 查詢執行階段僅會支援單一屬性及屬性名稱的排序，例如不支援已計算屬性的排序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="aef6a-280">排序也需要索引原則，包括適用於屬性及指定類型的範圍索引，搭配最大有效位數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="aef6a-281">如需詳細資訊，請參閱索引原則文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="aef6a-282"><a name="bk_scalar_expressions"></a>純量運算式</span><span class="sxs-lookup"><span data-stu-id="aef6a-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="aef6a-283">純量運算式結合了符號及運算子，可以加以評估以取得單一值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="aef6a-284">簡單運算式可以是常數、屬性參考、陣列元素參考、別名參考或函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="aef6a-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="aef6a-285">簡單運算式可以透過使用運算子，與複雜運算式結合。</span><span class="sxs-lookup"><span data-stu-id="aef6a-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="aef6a-286">如需純量運算式具備哪些值的詳細資料，請參閱[常數](#bk_constants)一節。</span><span class="sxs-lookup"><span data-stu-id="aef6a-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="aef6a-287">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-287">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="aef6a-288">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="aef6a-289">代表常數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-289">Represents a constant value.</span></span> <span data-ttu-id="aef6a-290">如需詳細資料，請參閱[常數](#bk_constants)一節。</span><span class="sxs-lookup"><span data-stu-id="aef6a-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="aef6a-291">代表在 `FROM` 子句中導入，且由 `input_alias` 定義的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="aef6a-292">此值不保證為**未定義** – 輸入中的**未定義值**會略過。</span><span class="sxs-lookup"><span data-stu-id="aef6a-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="aef6a-293">代表物件屬性值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="aef6a-294">若屬性不存在或已在非物件的值中參考，則運算式會評估為**未定義的**值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="aef6a-295">代表具有名稱 `property_name` 的屬性值，或具有物件/陣列索引 `array_index` 的陣列元素。</span><span class="sxs-lookup"><span data-stu-id="aef6a-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="aef6a-296">若屬性不存在或屬性/陣列索引已在非物件/陣列的值中參考，則運算式會評估為未定義的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="aef6a-297">代表已套用至單一值的運算子。</span><span class="sxs-lookup"><span data-stu-id="aef6a-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="aef6a-298">如需詳細資料，請參閱[運算子](#bk_operators)一節。</span><span class="sxs-lookup"><span data-stu-id="aef6a-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="aef6a-299">代表已套用至兩個值的運算子。</span><span class="sxs-lookup"><span data-stu-id="aef6a-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="aef6a-300">如需詳細資料，請參閱[運算子](#bk_operators)一節。</span><span class="sxs-lookup"><span data-stu-id="aef6a-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="aef6a-301">代表由函式呼叫結果定義的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="aef6a-302">使用者定義純量值函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="aef6a-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="aef6a-303">內建純量值函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="aef6a-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="aef6a-304">代表搭配指定屬性及其值所建立之新物件取得的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="aef6a-305">代表搭配指定值作為元素所建立之新物件取得的值</span><span class="sxs-lookup"><span data-stu-id="aef6a-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="aef6a-306">代表指定參數名字的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="aef6a-307">參數名稱必須帶有單一 @ 作為第一個字元。</span><span class="sxs-lookup"><span data-stu-id="aef6a-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="aef6a-308">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-308">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-309">呼叫內建或使用者定義純量值函式時，必須定義所有引數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="aef6a-310">若有任何未定義的引數，則不會呼叫函式，同時會產生未定義的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="aef6a-311">建立物件時，會略過任何指派未定義值的屬性，且不會納入已建立的物件中。</span><span class="sxs-lookup"><span data-stu-id="aef6a-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="aef6a-312">建立陣列時，會略過任何指派**未定義**值的元素值，且不會納入已建立的物件中。</span><span class="sxs-lookup"><span data-stu-id="aef6a-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="aef6a-313">這會讓下一個定義的元素以相同方式取代其位置，而建立的陣列將不會具備已略過的索引。</span><span class="sxs-lookup"><span data-stu-id="aef6a-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="aef6a-314"><a name="bk_operators"></a> 運算子</span><span class="sxs-lookup"><span data-stu-id="aef6a-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="aef6a-315">本節說明支援的運算子。</span><span class="sxs-lookup"><span data-stu-id="aef6a-315">This section describes the supported operators.</span></span> <span data-ttu-id="aef6a-316">每個運算子只能指派給一個類別。</span><span class="sxs-lookup"><span data-stu-id="aef6a-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="aef6a-317">請參閱以下的**運算子類別**表格，如需處理**未定義**值的詳細資料，請輸入輸入值的需求，以及透過不相符的值處理值的需求。</span><span class="sxs-lookup"><span data-stu-id="aef6a-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="aef6a-318">**運算子類別：**</span><span class="sxs-lookup"><span data-stu-id="aef6a-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="aef6a-319">**類別**</span><span class="sxs-lookup"><span data-stu-id="aef6a-319">**Category**</span></span>|<span data-ttu-id="aef6a-320">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="aef6a-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="aef6a-321">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="aef6a-321">**arithmetic**</span></span>|<span data-ttu-id="aef6a-322">運算子預期的輸入為數字。</span><span class="sxs-lookup"><span data-stu-id="aef6a-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="aef6a-323">輸出也是數字。</span><span class="sxs-lookup"><span data-stu-id="aef6a-323">Output is also a Number.</span></span> <span data-ttu-id="aef6a-324">若有任何**未定義的**輸入，或輸入了數字以外的類型，則會產生**未定義**的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="aef6a-325">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="aef6a-325">**bitwise**</span></span>|<span data-ttu-id="aef6a-326">運算子預期的輸入為 32 位元的帶正負號整數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="aef6a-327">輸出也為 32 位元的帶正負號整數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="aef6a-328">任何非整數值均會進行四捨五入。</span><span class="sxs-lookup"><span data-stu-id="aef6a-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="aef6a-329">正值會無條件捨去，負值則會進位。</span><span class="sxs-lookup"><span data-stu-id="aef6a-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="aef6a-330">除了 32 位元整數範圍的任何值，都會以去掉其兩個元件標記法的最後 32 位元進行轉換。</span><span class="sxs-lookup"><span data-stu-id="aef6a-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="aef6a-331">若有任何**未定義的**輸入，或輸入了數字以外的類型，則會產生**未定義**的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="aef6a-332">**注意：**以上行為會與 JavaScript 位元運算子行為相容。</span><span class="sxs-lookup"><span data-stu-id="aef6a-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="aef6a-333">**logical**</span><span class="sxs-lookup"><span data-stu-id="aef6a-333">**logical**</span></span>|<span data-ttu-id="aef6a-334">運算子預期的輸入為布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="aef6a-335">輸出也是布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="aef6a-336">若有任何**未定義的**輸入，或輸入了布林值以外的類型，則會產生**未定義**的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="aef6a-337">**comparison**</span><span class="sxs-lookup"><span data-stu-id="aef6a-337">**comparison**</span></span>|<span data-ttu-id="aef6a-338">運算子預期的輸入具有相同的未定義類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="aef6a-339">輸出也是布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="aef6a-340">若有任何**未定義的**輸入，或是不同類型的輸入，則會產生**未定義**的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="aef6a-341">請參閱**比較值順序**表格以取得值順序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="aef6a-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="aef6a-342">**字串**</span><span class="sxs-lookup"><span data-stu-id="aef6a-342">**string**</span></span>|<span data-ttu-id="aef6a-343">運算子預期的輸入為字串。</span><span class="sxs-lookup"><span data-stu-id="aef6a-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="aef6a-344">輸出也是字串。</span><span class="sxs-lookup"><span data-stu-id="aef6a-344">Output is also a String.</span></span><br /><span data-ttu-id="aef6a-345">若有任何**未定義的**輸入，或輸入了字串以外的類型，則會產生**未定義**的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="aef6a-346">**一元運算子**</span><span class="sxs-lookup"><span data-stu-id="aef6a-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="aef6a-347">**名稱**</span><span class="sxs-lookup"><span data-stu-id="aef6a-347">**Name**</span></span>|<span data-ttu-id="aef6a-348">**運算子**</span><span class="sxs-lookup"><span data-stu-id="aef6a-348">**Operator**</span></span>|<span data-ttu-id="aef6a-349">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="aef6a-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="aef6a-350">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="aef6a-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="aef6a-351">傳回數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="aef6a-352">位元否定。</span><span class="sxs-lookup"><span data-stu-id="aef6a-352">Bitwise negation.</span></span> <span data-ttu-id="aef6a-353">傳回否定的數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="aef6a-354">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="aef6a-354">**bitwise**</span></span>|~|<span data-ttu-id="aef6a-355">1 的補數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-355">Ones' complement.</span></span> <span data-ttu-id="aef6a-356">傳回數值的補數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="aef6a-357">**Logical**</span><span class="sxs-lookup"><span data-stu-id="aef6a-357">**Logical**</span></span>|<span data-ttu-id="aef6a-358">**NOT**</span><span class="sxs-lookup"><span data-stu-id="aef6a-358">**NOT**</span></span>|<span data-ttu-id="aef6a-359">否定。</span><span class="sxs-lookup"><span data-stu-id="aef6a-359">Negation.</span></span> <span data-ttu-id="aef6a-360">傳回否定布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="aef6a-361">**二元運算子：**</span><span class="sxs-lookup"><span data-stu-id="aef6a-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="aef6a-362">**名稱**</span><span class="sxs-lookup"><span data-stu-id="aef6a-362">**Name**</span></span>|<span data-ttu-id="aef6a-363">**運算子**</span><span class="sxs-lookup"><span data-stu-id="aef6a-363">**Operator**</span></span>|<span data-ttu-id="aef6a-364">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="aef6a-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="aef6a-365">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="aef6a-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="aef6a-366">加法。</span><span class="sxs-lookup"><span data-stu-id="aef6a-366">Addition.</span></span><br /><br /> <span data-ttu-id="aef6a-367">減法。</span><span class="sxs-lookup"><span data-stu-id="aef6a-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="aef6a-368">乘法。</span><span class="sxs-lookup"><span data-stu-id="aef6a-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="aef6a-369">除法。</span><span class="sxs-lookup"><span data-stu-id="aef6a-369">Division.</span></span><br /><br /> <span data-ttu-id="aef6a-370">調節。</span><span class="sxs-lookup"><span data-stu-id="aef6a-370">Modulation.</span></span>|  
|<span data-ttu-id="aef6a-371">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="aef6a-371">**bitwise**</span></span>|<span data-ttu-id="aef6a-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="aef6a-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="aef6a-373">位元 OR。</span><span class="sxs-lookup"><span data-stu-id="aef6a-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="aef6a-374">位元 AND。</span><span class="sxs-lookup"><span data-stu-id="aef6a-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="aef6a-375">位元 XOR。</span><span class="sxs-lookup"><span data-stu-id="aef6a-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="aef6a-376">向左移位。</span><span class="sxs-lookup"><span data-stu-id="aef6a-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="aef6a-377">向右移位。</span><span class="sxs-lookup"><span data-stu-id="aef6a-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="aef6a-378">向右移位並填滿零。</span><span class="sxs-lookup"><span data-stu-id="aef6a-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="aef6a-379">**logical**</span><span class="sxs-lookup"><span data-stu-id="aef6a-379">**logical**</span></span>|<span data-ttu-id="aef6a-380">**AND**</span><span class="sxs-lookup"><span data-stu-id="aef6a-380">**AND**</span></span><br /><br /> <span data-ttu-id="aef6a-381">**或**</span><span class="sxs-lookup"><span data-stu-id="aef6a-381">**OR**</span></span>|<span data-ttu-id="aef6a-382">邏輯結合。</span><span class="sxs-lookup"><span data-stu-id="aef6a-382">Logical conjunction.</span></span> <span data-ttu-id="aef6a-383">若兩個引數都為 **True**，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="aef6a-384">邏輯結合。</span><span class="sxs-lookup"><span data-stu-id="aef6a-384">Logical conjunction.</span></span> <span data-ttu-id="aef6a-385">若兩個引數都為 **True**，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="aef6a-386">**comparison**</span><span class="sxs-lookup"><span data-stu-id="aef6a-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="aef6a-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="aef6a-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="aef6a-388">**??**</span><span class="sxs-lookup"><span data-stu-id="aef6a-388">**??**</span></span>|<span data-ttu-id="aef6a-389">等於。</span><span class="sxs-lookup"><span data-stu-id="aef6a-389">Equals.</span></span> <span data-ttu-id="aef6a-390">若引數相等，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="aef6a-391">不等於。</span><span class="sxs-lookup"><span data-stu-id="aef6a-391">Not equal to.</span></span> <span data-ttu-id="aef6a-392">若引數不相等，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="aef6a-393">大於。</span><span class="sxs-lookup"><span data-stu-id="aef6a-393">Greater Than.</span></span> <span data-ttu-id="aef6a-394">如果第一個引數大於第二個引數，則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="aef6a-395">大於或等於。</span><span class="sxs-lookup"><span data-stu-id="aef6a-395">Greater Than or Equal To.</span></span> <span data-ttu-id="aef6a-396">如果第一個引數大於或等於第二個引數，則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="aef6a-397">小於。</span><span class="sxs-lookup"><span data-stu-id="aef6a-397">Less Than.</span></span> <span data-ttu-id="aef6a-398">如果第一個引數小於第二個引數，則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="aef6a-399">小於或等於。</span><span class="sxs-lookup"><span data-stu-id="aef6a-399">Less Than or Equal To.</span></span> <span data-ttu-id="aef6a-400">如果第一個引數小於或等於第二個引數，則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="aef6a-401">聯合。</span><span class="sxs-lookup"><span data-stu-id="aef6a-401">Coalesce.</span></span> <span data-ttu-id="aef6a-402">若第一個引數為**未定義的**值，則會傳回第二個引數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="aef6a-403">**String**</span><span class="sxs-lookup"><span data-stu-id="aef6a-403">**String**</span></span>|<span data-ttu-id="aef6a-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="aef6a-404">**&#124;&#124;**</span></span>|<span data-ttu-id="aef6a-405">串連。</span><span class="sxs-lookup"><span data-stu-id="aef6a-405">Concatenation.</span></span> <span data-ttu-id="aef6a-406">傳回兩個引數的串連。</span><span class="sxs-lookup"><span data-stu-id="aef6a-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="aef6a-407">**三元運算子：** </span><span class="sxs-lookup"><span data-stu-id="aef6a-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="aef6a-408">三元運算子</span><span class="sxs-lookup"><span data-stu-id="aef6a-408">Ternary operator</span></span>|<span data-ttu-id="aef6a-409">?</span><span class="sxs-lookup"><span data-stu-id="aef6a-409">?</span></span>|<span data-ttu-id="aef6a-410">若第一個引數評估為 **True**；則會傳回第二個引數，否則會傳回第三個引數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="aef6a-411">**比較值順序**</span><span class="sxs-lookup"><span data-stu-id="aef6a-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="aef6a-412">**類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-412">**Type**</span></span>|<span data-ttu-id="aef6a-413">**值順序**</span><span class="sxs-lookup"><span data-stu-id="aef6a-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="aef6a-414">**未定義**</span><span class="sxs-lookup"><span data-stu-id="aef6a-414">**Undefined**</span></span>|<span data-ttu-id="aef6a-415">無法比較。</span><span class="sxs-lookup"><span data-stu-id="aef6a-415">Not comparable.</span></span>|  
|<span data-ttu-id="aef6a-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="aef6a-416">**Null**</span></span>|<span data-ttu-id="aef6a-417">單一值：**Null**</span><span class="sxs-lookup"><span data-stu-id="aef6a-417">Single value: **null**</span></span>|  
|<span data-ttu-id="aef6a-418">**Number**</span><span class="sxs-lookup"><span data-stu-id="aef6a-418">**Number**</span></span>|<span data-ttu-id="aef6a-419">自然實數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="aef6a-420">負的無限值小於其他任何數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="aef6a-421">正無限值大於其他任何數值。**NaN** 值無法比較。</span><span class="sxs-lookup"><span data-stu-id="aef6a-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="aef6a-422">與 **NaN** 比較會產生**未定義的**值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="aef6a-423">**String**</span><span class="sxs-lookup"><span data-stu-id="aef6a-423">**String**</span></span>|<span data-ttu-id="aef6a-424">詞彙編篡順序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="aef6a-425">**Array**</span><span class="sxs-lookup"><span data-stu-id="aef6a-425">**Array**</span></span>|<span data-ttu-id="aef6a-426">沒有順序，但合理。</span><span class="sxs-lookup"><span data-stu-id="aef6a-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="aef6a-427">**Object**</span><span class="sxs-lookup"><span data-stu-id="aef6a-427">**Object**</span></span>|<span data-ttu-id="aef6a-428">沒有順序，但合理。</span><span class="sxs-lookup"><span data-stu-id="aef6a-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="aef6a-429">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-429">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-430">在 Azure Cosmos DB 中，通常不會知道值的類型，除非實際從資料庫中擷取。</span><span class="sxs-lookup"><span data-stu-id="aef6a-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="aef6a-431">為了支援有效率的查詢執行，大部分的運算子都有嚴謹的類型需求。</span><span class="sxs-lookup"><span data-stu-id="aef6a-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="aef6a-432">此外，運算子本身並不會執行隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="aef6a-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="aef6a-433">這表示例如 SELECT * FROM ROOT r WHERE r.Age = 21 的查詢僅會傳回具有適當年齡為數字 21 的文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="aef6a-434">具有適當年齡為字串 "21" 或字串 "0021" 的文件並不相符，因為運算式 "21" = 21 評估為未定義。</span><span class="sxs-lookup"><span data-stu-id="aef6a-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="aef6a-435">由於查詢特定值 (例如數字 21) 比搜尋不限數量的可能相符項目更加快速 (例如數字 21 或字串 "21"、"021"、"21.0" 等)，因此可以利用索引進行。</span><span class="sxs-lookup"><span data-stu-id="aef6a-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="aef6a-436">這點不同於 JavaScript 評估不同類型運算子值的方式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="aef6a-437">**陣列和物件的相等和比較**</span><span class="sxs-lookup"><span data-stu-id="aef6a-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="aef6a-438">使用範圍運算子 (>, >=, <, <=) 比較陣列或物件值會產生未定義的結果，因為物件或陣列值未定義順序。</span><span class="sxs-lookup"><span data-stu-id="aef6a-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="aef6a-439">不過，支援使用等號/不等運算子 (=, !=, <>) 且會以結構化的方式進行比較。</span><span class="sxs-lookup"><span data-stu-id="aef6a-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="aef6a-440">若兩個陣列具有相同數目的元素，且位於相符位置的元素也相等，則陣列也會相等。</span><span class="sxs-lookup"><span data-stu-id="aef6a-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="aef6a-441">若比較任何元素配對對會產生未定義的結果，則陣列比較的結果為未定義。</span><span class="sxs-lookup"><span data-stu-id="aef6a-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="aef6a-442">若兩個物件均定義了相同的屬性，而且相符的屬性也相等，則物件會相等。</span><span class="sxs-lookup"><span data-stu-id="aef6a-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="aef6a-443">若比較任何屬性值配對會產生未定義的結果，則物件比較的結果為未定義。</span><span class="sxs-lookup"><span data-stu-id="aef6a-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="aef6a-444"><a name="bk_constants"></a> 常數</span><span class="sxs-lookup"><span data-stu-id="aef6a-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="aef6a-445">常數也稱為常值或純量值，是代表特定資料值的符號。</span><span class="sxs-lookup"><span data-stu-id="aef6a-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="aef6a-446">常數的格式會依其代表的值資料類型而定。</span><span class="sxs-lookup"><span data-stu-id="aef6a-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="aef6a-447">**支援的純量資料類型：**</span><span class="sxs-lookup"><span data-stu-id="aef6a-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="aef6a-448">**類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-448">**Type**</span></span>|<span data-ttu-id="aef6a-449">**值順序**</span><span class="sxs-lookup"><span data-stu-id="aef6a-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="aef6a-450">**未定義**</span><span class="sxs-lookup"><span data-stu-id="aef6a-450">**Undefined**</span></span>|<span data-ttu-id="aef6a-451">單一值： **未定義**</span><span class="sxs-lookup"><span data-stu-id="aef6a-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="aef6a-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="aef6a-452">**Null**</span></span>|<span data-ttu-id="aef6a-453">單一值：**Null**</span><span class="sxs-lookup"><span data-stu-id="aef6a-453">Single value: **null**</span></span>|  
|<span data-ttu-id="aef6a-454">**布林值**</span><span class="sxs-lookup"><span data-stu-id="aef6a-454">**Boolean**</span></span>|<span data-ttu-id="aef6a-455">值：**False**，**True**。</span><span class="sxs-lookup"><span data-stu-id="aef6a-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="aef6a-456">**Number**</span><span class="sxs-lookup"><span data-stu-id="aef6a-456">**Number**</span></span>|<span data-ttu-id="aef6a-457">雙精確度浮點數，符合 IEEE 754 標準。</span><span class="sxs-lookup"><span data-stu-id="aef6a-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="aef6a-458">**String**</span><span class="sxs-lookup"><span data-stu-id="aef6a-458">**String**</span></span>|<span data-ttu-id="aef6a-459">零或更多 Unicode 字元的序列。</span><span class="sxs-lookup"><span data-stu-id="aef6a-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="aef6a-460">字串必須以單引號或雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="aef6a-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="aef6a-461">**Array**</span><span class="sxs-lookup"><span data-stu-id="aef6a-461">**Array**</span></span>|<span data-ttu-id="aef6a-462">零或更多元素的序列。</span><span class="sxs-lookup"><span data-stu-id="aef6a-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="aef6a-463">除了未定義的類型，每個元素都可以是任何純量資料類型的值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="aef6a-464">**Object**</span><span class="sxs-lookup"><span data-stu-id="aef6a-464">**Object**</span></span>|<span data-ttu-id="aef6a-465">未排序的零或更多名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="aef6a-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="aef6a-466">名稱為 Unicode 字串；除了**未定義**的類型，值可以是任何純量資料類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="aef6a-467">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-467">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="aef6a-468">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="aef6a-469">代表未定義類型的未定義值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="aef6a-470">代表 **Null** 類型的 **Null** 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="aef6a-471">代表布林值類型的常數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="aef6a-472">代表布林值類型的 **False** 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="aef6a-473">代表布林值類型的 **True** 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="aef6a-474">代表常數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="aef6a-475">十進位常值是使用十進位表示法或科學記號標記法表示的數字。</span><span class="sxs-lookup"><span data-stu-id="aef6a-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="aef6a-476">十六進位常值是使用前置詞 '0x' 後面接著一或多個十六進位數字表示的數字。</span><span class="sxs-lookup"><span data-stu-id="aef6a-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="aef6a-477">代表字串類型的常數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="aef6a-478">字串常值是由零個或多個 Unicode 字元序列或逸出序列所表示的 Unicode 字串。</span><span class="sxs-lookup"><span data-stu-id="aef6a-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="aef6a-479">字串常值會以單引號 (所有格符號：') 或雙引號 (引號：") 括起來。</span><span class="sxs-lookup"><span data-stu-id="aef6a-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="aef6a-480">允許下列逸出序列：</span><span class="sxs-lookup"><span data-stu-id="aef6a-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="aef6a-481">**逸出序列**</span><span class="sxs-lookup"><span data-stu-id="aef6a-481">**Escape sequence**</span></span>|<span data-ttu-id="aef6a-482">**說明**</span><span class="sxs-lookup"><span data-stu-id="aef6a-482">**Description**</span></span>|<span data-ttu-id="aef6a-483">**Unicode 字元**</span><span class="sxs-lookup"><span data-stu-id="aef6a-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="aef6a-484">\\'</span><span class="sxs-lookup"><span data-stu-id="aef6a-484">\\'</span></span>|<span data-ttu-id="aef6a-485">apostrophe (')</span><span class="sxs-lookup"><span data-stu-id="aef6a-485">apostrophe (')</span></span>|<span data-ttu-id="aef6a-486">U+0027</span><span class="sxs-lookup"><span data-stu-id="aef6a-486">U+0027</span></span>|  
|<span data-ttu-id="aef6a-487">\\"</span><span class="sxs-lookup"><span data-stu-id="aef6a-487">\\"</span></span>|<span data-ttu-id="aef6a-488">引號 (")</span><span class="sxs-lookup"><span data-stu-id="aef6a-488">quotation mark (")</span></span>|<span data-ttu-id="aef6a-489">U+0022</span><span class="sxs-lookup"><span data-stu-id="aef6a-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="aef6a-490">反向斜線 (\\)</span><span class="sxs-lookup"><span data-stu-id="aef6a-490">reverse solidus (\\)</span></span>|<span data-ttu-id="aef6a-491">U+005C</span><span class="sxs-lookup"><span data-stu-id="aef6a-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="aef6a-492">斜線 (/)</span><span class="sxs-lookup"><span data-stu-id="aef6a-492">solidus (/)</span></span>|<span data-ttu-id="aef6a-493">U+002F</span><span class="sxs-lookup"><span data-stu-id="aef6a-493">U+002F</span></span>|  
|<span data-ttu-id="aef6a-494">\b</span><span class="sxs-lookup"><span data-stu-id="aef6a-494">\b</span></span>|<span data-ttu-id="aef6a-495">退格鍵</span><span class="sxs-lookup"><span data-stu-id="aef6a-495">backspace</span></span>|<span data-ttu-id="aef6a-496">U+0008</span><span class="sxs-lookup"><span data-stu-id="aef6a-496">U+0008</span></span>|  
|<span data-ttu-id="aef6a-497">\f</span><span class="sxs-lookup"><span data-stu-id="aef6a-497">\f</span></span>|<span data-ttu-id="aef6a-498">換頁字元</span><span class="sxs-lookup"><span data-stu-id="aef6a-498">form feed</span></span>|<span data-ttu-id="aef6a-499">U+000C</span><span class="sxs-lookup"><span data-stu-id="aef6a-499">U+000C</span></span>|  
|\n|<span data-ttu-id="aef6a-500">換行字元</span><span class="sxs-lookup"><span data-stu-id="aef6a-500">line feed</span></span>|<span data-ttu-id="aef6a-501">U+000A</span><span class="sxs-lookup"><span data-stu-id="aef6a-501">U+000A</span></span>|  
|<span data-ttu-id="aef6a-502">\r</span><span class="sxs-lookup"><span data-stu-id="aef6a-502">\r</span></span>|<span data-ttu-id="aef6a-503">歸位字元</span><span class="sxs-lookup"><span data-stu-id="aef6a-503">carriage return</span></span>|<span data-ttu-id="aef6a-504">U+000D</span><span class="sxs-lookup"><span data-stu-id="aef6a-504">U+000D</span></span>|  
|<span data-ttu-id="aef6a-505">\t</span><span class="sxs-lookup"><span data-stu-id="aef6a-505">\t</span></span>|<span data-ttu-id="aef6a-506">Tab 鍵</span><span class="sxs-lookup"><span data-stu-id="aef6a-506">tab</span></span>|<span data-ttu-id="aef6a-507">U+0009</span><span class="sxs-lookup"><span data-stu-id="aef6a-507">U+0009</span></span>|  
|<span data-ttu-id="aef6a-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="aef6a-508">\uXXXX</span></span>|<span data-ttu-id="aef6a-509">由 4 個十六進位數字所定義的 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="aef6a-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="aef6a-510">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="aef6a-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="aef6a-511"><a name="bk_query_perf_guidelines"></a> 查詢效能指導方針</span><span class="sxs-lookup"><span data-stu-id="aef6a-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="aef6a-512">為了讓查詢在大型集合中有效率的執行，應該使用可透過一或多個索引提供的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="aef6a-513">下列的篩選器會被視為索引查詢：</span><span class="sxs-lookup"><span data-stu-id="aef6a-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="aef6a-514">使用等號比較運算子 ( = ) 搭配文件路徑運算式和常數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="aef6a-515">使用範圍比較運算子 (<, \<=, >, >=) 搭配文件路徑運算式和數字常數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="aef6a-516">文件路徑運算式代表可識別受參考資料庫集合的文件中，常數路徑的任何運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="aef6a-517">**文件路徑運算式**</span><span class="sxs-lookup"><span data-stu-id="aef6a-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="aef6a-518">文件路徑運算式是一種運算式，會採取來自資料庫集合文件之文件上的屬性或陣列索引子的路徑。</span><span class="sxs-lookup"><span data-stu-id="aef6a-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="aef6a-519">這個路徑可以用來識別值的位置，而這些值會由篩選條件直接在資料庫集合中的文件參考。</span><span class="sxs-lookup"><span data-stu-id="aef6a-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="aef6a-520">對於被視為文件路徑運算式的運算式，它應該：</span><span class="sxs-lookup"><span data-stu-id="aef6a-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="aef6a-521">直接參考集合根。</span><span class="sxs-lookup"><span data-stu-id="aef6a-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="aef6a-522">參考某些文件路徑運算式的屬性或常數陣列索引子</span><span class="sxs-lookup"><span data-stu-id="aef6a-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="aef6a-523">參考代表某文件路徑運算式的別名。</span><span class="sxs-lookup"><span data-stu-id="aef6a-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="aef6a-524">**語法慣例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="aef6a-525">下列表格描述用來說明 DocumentDB API 查詢語言參考語法的慣例。</span><span class="sxs-lookup"><span data-stu-id="aef6a-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="aef6a-526">**慣例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-526">**Convention**</span></span>|<span data-ttu-id="aef6a-527">**用於**</span><span class="sxs-lookup"><span data-stu-id="aef6a-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="aef6a-528">大寫</span><span class="sxs-lookup"><span data-stu-id="aef6a-528">UPPERCASE</span></span>|<span data-ttu-id="aef6a-529">關鍵字不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="aef6a-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="aef6a-530">小寫</span><span class="sxs-lookup"><span data-stu-id="aef6a-530">lowercase</span></span>|<span data-ttu-id="aef6a-531">關鍵字區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="aef6a-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="aef6a-532">\<nonterminal></span><span class="sxs-lookup"><span data-stu-id="aef6a-532">\<nonterminal></span></span>|<span data-ttu-id="aef6a-533">非終端項，分別定義。</span><span class="sxs-lookup"><span data-stu-id="aef6a-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="aef6a-534">\<nonterminal> ::=</span><span class="sxs-lookup"><span data-stu-id="aef6a-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="aef6a-535">非終端項的語法定義。</span><span class="sxs-lookup"><span data-stu-id="aef6a-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="aef6a-536">other_terminal</span><span class="sxs-lookup"><span data-stu-id="aef6a-536">other_terminal</span></span>|<span data-ttu-id="aef6a-537">終端項 (權杖)，以文字詳細說明。</span><span class="sxs-lookup"><span data-stu-id="aef6a-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="aef6a-538">識別碼</span><span class="sxs-lookup"><span data-stu-id="aef6a-538">identifier</span></span>|<span data-ttu-id="aef6a-539">識別碼。</span><span class="sxs-lookup"><span data-stu-id="aef6a-539">Identifier.</span></span> <span data-ttu-id="aef6a-540">僅允許下列字元：a-z A-Z 0-9 _第一個字元不能為數字。</span><span class="sxs-lookup"><span data-stu-id="aef6a-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="aef6a-541">"字串"</span><span class="sxs-lookup"><span data-stu-id="aef6a-541">"string"</span></span>|<span data-ttu-id="aef6a-542">括號中的字串。</span><span class="sxs-lookup"><span data-stu-id="aef6a-542">Quoted string.</span></span> <span data-ttu-id="aef6a-543">允許任何有效字串。</span><span class="sxs-lookup"><span data-stu-id="aef6a-543">Allows any valid string.</span></span> <span data-ttu-id="aef6a-544">請參閱 string_literal 的描述。</span><span class="sxs-lookup"><span data-stu-id="aef6a-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="aef6a-545">'符號'</span><span class="sxs-lookup"><span data-stu-id="aef6a-545">'symbol'</span></span>|<span data-ttu-id="aef6a-546">常值符號，為語法的一部分。</span><span class="sxs-lookup"><span data-stu-id="aef6a-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="aef6a-547">&#124; (分隔號)</span><span class="sxs-lookup"><span data-stu-id="aef6a-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="aef6a-548">語法項目的替代項目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-548">Alternatives for syntax items.</span></span> <span data-ttu-id="aef6a-549">您僅可使用其中一個指定項目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="aef6a-550">[ ] /(方括號)</span><span class="sxs-lookup"><span data-stu-id="aef6a-550">[ ] /(brackets)</span></span>|<span data-ttu-id="aef6a-551">方括號會括住一或多個選用項目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="aef6a-552">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="aef6a-552">[ ,...n ]</span></span>|<span data-ttu-id="aef6a-553">指出先前項目可以重複 n 次。</span><span class="sxs-lookup"><span data-stu-id="aef6a-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="aef6a-554">以逗號分隔項目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="aef6a-555">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="aef6a-555">[ ...n ]</span></span>|<span data-ttu-id="aef6a-556">指出先前項目可以重複 n 次。</span><span class="sxs-lookup"><span data-stu-id="aef6a-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="aef6a-557">以空格分隔項目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="aef6a-558"><a name="bk_built_in_functions"></a>內建函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="aef6a-559">Azure Cosmos DB 提供許多內建 SQL 函式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="aef6a-560">內建函式的分類如下所示。</span><span class="sxs-lookup"><span data-stu-id="aef6a-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="aef6a-561">函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-561">Function</span></span>|<span data-ttu-id="aef6a-562">說明</span><span class="sxs-lookup"><span data-stu-id="aef6a-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="aef6a-563">數學函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="aef6a-564">每個數學函數都會執行計算，通常以提供做為引數的輸入值為基礎，並且會傳回數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="aef6a-565">類型檢查函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="aef6a-566">類型檢查函數可讓您檢查 SQL 查詢中的運算式類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="aef6a-567">字串函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="aef6a-568">下列字串函式會對字串輸入值執行作業，並傳回字串、數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="aef6a-569">陣列函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="aef6a-570">下列陣列函式會對陣列輸入值執行作業，並傳回數值、布林值或陣列值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="aef6a-571">空間函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="aef6a-572">下列空間函數會對空間物件輸入值執行作業，並傳回數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="aef6a-573"><a name="bk_mathematical_functions"></a>數學函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="aef6a-574">下列函式都會執行計算，通常以提供作為引數的輸入值為基礎，並且會傳回數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="aef6a-575">ABS</span><span class="sxs-lookup"><span data-stu-id="aef6a-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="aef6a-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="aef6a-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="aef6a-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="aef6a-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="aef6a-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="aef6a-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="aef6a-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="aef6a-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="aef6a-580">CEILING</span><span class="sxs-lookup"><span data-stu-id="aef6a-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="aef6a-581">COS</span><span class="sxs-lookup"><span data-stu-id="aef6a-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="aef6a-582">COT</span><span class="sxs-lookup"><span data-stu-id="aef6a-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="aef6a-583">DEGREES</span><span class="sxs-lookup"><span data-stu-id="aef6a-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="aef6a-584">EXP</span><span class="sxs-lookup"><span data-stu-id="aef6a-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="aef6a-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="aef6a-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="aef6a-586">LOG</span><span class="sxs-lookup"><span data-stu-id="aef6a-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="aef6a-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="aef6a-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="aef6a-588">PI</span><span class="sxs-lookup"><span data-stu-id="aef6a-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="aef6a-589">POWER</span><span class="sxs-lookup"><span data-stu-id="aef6a-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="aef6a-590">RADIANS</span><span class="sxs-lookup"><span data-stu-id="aef6a-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="aef6a-591">ROUND</span><span class="sxs-lookup"><span data-stu-id="aef6a-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="aef6a-592">SIN</span><span class="sxs-lookup"><span data-stu-id="aef6a-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="aef6a-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="aef6a-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="aef6a-594">SQUARE</span><span class="sxs-lookup"><span data-stu-id="aef6a-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="aef6a-595">SIGN</span><span class="sxs-lookup"><span data-stu-id="aef6a-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="aef6a-596">TAN</span><span class="sxs-lookup"><span data-stu-id="aef6a-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="aef6a-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="aef6a-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="aef6a-598"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="aef6a-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="aef6a-599">傳回指定之數值運算式的絕對 (正) 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-600">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-601">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-602">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-603">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-603">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-604">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-605">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-605">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-606">下列範例顯示在三個不同的數字上使用 ABS 函式的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="aef6a-607">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="aef6a-608"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="aef6a-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="aef6a-609">傳回角度，以弧度為單位，它的餘弦是指定的數值運算式；也稱為反餘弦值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="aef6a-610">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-611">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-612">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-613">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-613">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-614">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-615">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-615">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-616">下列範例會傳回 -1 的 ACOS。</span><span class="sxs-lookup"><span data-stu-id="aef6a-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="aef6a-617">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="aef6a-618"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="aef6a-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="aef6a-619">傳回角度，以弧度為單位，其正弦函數是指定的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="aef6a-620">這也稱為反正弦值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="aef6a-621">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-622">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-623">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-624">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-624">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-625">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-626">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-626">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-627">下列範例會傳回 -1 的 ASIN。</span><span class="sxs-lookup"><span data-stu-id="aef6a-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="aef6a-628">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="aef6a-629"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="aef6a-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="aef6a-630">傳回角度，以弧度為單位，其正切函數是指定的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="aef6a-631">這也稱為反正切值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="aef6a-632">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-633">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-634">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-635">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-635">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-636">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-637">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-637">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-638">下列範例會傳回指定值的 ATAN。</span><span class="sxs-lookup"><span data-stu-id="aef6a-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="aef6a-639">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="aef6a-640"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="aef6a-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="aef6a-641">傳回 y/x 有向徑正切函數的主體值，以弧度表示。</span><span class="sxs-lookup"><span data-stu-id="aef6a-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="aef6a-642">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-643">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-644">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-645">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-645">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-646">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-647">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-647">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-648">下列範例會計算指定 X 和 Y 元件的 ATN2 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="aef6a-649">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="aef6a-650"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="aef6a-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="aef6a-651">傳回大於或等於指定之數值運算式的最小整數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-652">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-653">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-654">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-655">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-655">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-656">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-657">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-657">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-658">下列範例顯示搭配 CEILING 函式的正數、負數和零值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="aef6a-659">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="aef6a-660"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="aef6a-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="aef6a-661">在指定運算式中傳回指定角度的三角餘弦函數，以弧度為單位。</span><span class="sxs-lookup"><span data-stu-id="aef6a-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="aef6a-662">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-663">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-664">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-665">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-665">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-666">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-667">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-667">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-668">下列範例會計算指定角度的 COS 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="aef6a-669">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="aef6a-670"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="aef6a-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="aef6a-671">在指定的數值運算式中傳回指定角度的三角餘切函數，以弧度為單位。</span><span class="sxs-lookup"><span data-stu-id="aef6a-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-672">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-673">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-674">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-675">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-675">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-676">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-677">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-677">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-678">下列範例會計算指定角度的 COS 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="aef6a-679">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="aef6a-680"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="aef6a-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="aef6a-681">針對以弧度指定的角度，傳回對應的角度 (以度為單位)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="aef6a-682">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-683">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-684">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-685">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-685">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-686">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-687">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-687">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-688">下列範例會傳回 PI/2 弧度的角度度數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="aef6a-689">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="aef6a-690"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="aef6a-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="aef6a-691">傳回小於或等於指定之數值運算式的最大整數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-692">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-693">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-694">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-695">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-695">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-696">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-697">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-697">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-698">下列範例顯示搭配 FLOOR 函式的正數、負數和零值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="aef6a-699">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="aef6a-700"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="aef6a-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="aef6a-701">傳回指定之數值運算式的指數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-702">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-703">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-704">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-705">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-705">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-706">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-707">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-707">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-708">常數 **e** (2.718281…)，為自然對數的基礎。</span><span class="sxs-lookup"><span data-stu-id="aef6a-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="aef6a-709">數字的指數是常數**e**的數字乘冪。</span><span class="sxs-lookup"><span data-stu-id="aef6a-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="aef6a-710">例如 EXP(1.0) = e^1.0 = 2.71828182845905 和 EXP(10) = e^10 = 22026.4657948067。</span><span class="sxs-lookup"><span data-stu-id="aef6a-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="aef6a-711">數字的自然對數之指數為數字本身：EXP (LOG (n)) = n。</span><span class="sxs-lookup"><span data-stu-id="aef6a-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="aef6a-712">而數字指數的自然對數則是該數值本身：LOG (EXP (n)) = n。</span><span class="sxs-lookup"><span data-stu-id="aef6a-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="aef6a-713">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-713">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-714">下列範例會宣告一個變數，並傳回指定變數 (10) 的指數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="aef6a-715">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="aef6a-716">下列範例會傳回自然對數的指數值 20，以及指數的自然對數 20。</span><span class="sxs-lookup"><span data-stu-id="aef6a-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="aef6a-717">因為這些函式是彼此的反向函數，傳回值以浮點數學計算，四捨五入之後在這兩種情況均為 20。</span><span class="sxs-lookup"><span data-stu-id="aef6a-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="aef6a-718">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="aef6a-719"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="aef6a-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="aef6a-720">傳回指定數值運算式的自然對數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-721">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="aef6a-722">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-723">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="aef6a-724">選用數值引數會設定對數基數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="aef6a-725">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-725">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-726">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-727">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-727">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-728">依預設，LOG() 會傳回自然對數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="aef6a-729">您可以使用選用基數參數，將對數基數變更為其他值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="aef6a-730">自然對數為基數 **e** 的對數，其中 **e** 為無理常數，大約等於 2.718281828。</span><span class="sxs-lookup"><span data-stu-id="aef6a-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="aef6a-731">數字指數的自然對數則是該數值本身：LOG( EXP( n ) ) = n。</span><span class="sxs-lookup"><span data-stu-id="aef6a-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="aef6a-732">而數字的自然對數之指數為數字本身：EXP( LOG( n ) ) = n。</span><span class="sxs-lookup"><span data-stu-id="aef6a-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="aef6a-733">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-733">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-734">下列範例會宣告一個變數，並傳回指定變數 (10) 的對數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="aef6a-735">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="aef6a-736">下列範例會計算數字指數的 LOG。</span><span class="sxs-lookup"><span data-stu-id="aef6a-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="aef6a-737">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="aef6a-738"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="aef6a-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="aef6a-739">傳回指定之數值運算式的以 10 為基底的對數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-740">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-741">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-742">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-743">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-743">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-744">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-745">**備註**</span><span class="sxs-lookup"><span data-stu-id="aef6a-745">**Remarks**</span></span>  
  
 <span data-ttu-id="aef6a-746">LOG10 和 POWER 函式彼此成反比相關。</span><span class="sxs-lookup"><span data-stu-id="aef6a-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="aef6a-747">例如，10 ^ LOG10(n) = n。</span><span class="sxs-lookup"><span data-stu-id="aef6a-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="aef6a-748">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-748">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-749">下列範例會宣告一個變數，並傳回指定變數 (100) 的 LOG10 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="aef6a-750">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="aef6a-751"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="aef6a-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="aef6a-752">傳回 PI 的常數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="aef6a-753">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="aef6a-754">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-755">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-756">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-756">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-757">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-758">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-758">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-759">下列範例會傳回 PI 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="aef6a-760">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="aef6a-761"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="aef6a-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="aef6a-762">將指定之運算式的值傳回給指定的乘冪。</span><span class="sxs-lookup"><span data-stu-id="aef6a-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="aef6a-763">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="aef6a-764">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-765">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="aef6a-766">為要提高至 `numeric_expression` 的乘冪。</span><span class="sxs-lookup"><span data-stu-id="aef6a-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="aef6a-767">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-767">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-768">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-769">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-769">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-770">下列範例示範如何將乘冪數字提高到 3 (數字立方體)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="aef6a-771">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="aef6a-772"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="aef6a-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="aef6a-773">當您輸入數值運算式 (以度為單位) 時，傳回弧度。</span><span class="sxs-lookup"><span data-stu-id="aef6a-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="aef6a-774">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-775">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-776">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-777">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-777">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-778">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-779">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-779">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-780">下列範例會使用幾個角度作為輸入，並傳回其對應的弧度值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="aef6a-781">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="aef6a-782"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="aef6a-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="aef6a-783">傳回數值，四捨五入到最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="aef6a-784">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-785">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-786">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-787">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-787">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-788">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-789">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-789">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-790">下列範例會將以下正數和負數數字四捨五入至最接近的整數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="aef6a-791">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="aef6a-792"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="aef6a-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="aef6a-793">傳回指定之數值運算式的正數 (+1)、零 (0) 或負數 (-1) 符號。</span><span class="sxs-lookup"><span data-stu-id="aef6a-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-794">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-795">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-796">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-797">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-797">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-798">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-799">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-799">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-800">下列範例會傳回從-2 到 2 的 SIGN 值數字。</span><span class="sxs-lookup"><span data-stu-id="aef6a-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="aef6a-801">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="aef6a-802"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="aef6a-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="aef6a-803">在指定運算式中傳回指定角度的三角正弦函數 (以弧度為單位)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="aef6a-804">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-805">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-806">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-807">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-807">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-808">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-809">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-809">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-810">下列範例會計算指定角度的 SIN 值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="aef6a-811">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="aef6a-812"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="aef6a-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="aef6a-813">傳回指定之數值的平方根。</span><span class="sxs-lookup"><span data-stu-id="aef6a-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="aef6a-814">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-815">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-816">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-817">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-817">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-818">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-819">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-819">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-820">下列範例會傳回數字 1 到 3 的平方根值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="aef6a-821">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="aef6a-822"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="aef6a-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="aef6a-823">傳回指定之數值的平方。</span><span class="sxs-lookup"><span data-stu-id="aef6a-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="aef6a-824">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-825">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-826">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-827">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-827">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-828">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-829">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-829">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-830">下列範例會傳回數字 1 到 3 的平方值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="aef6a-831">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="aef6a-832"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="aef6a-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="aef6a-833">在指定運算式中傳回指定角度的正切函式 (以弧度為單位)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="aef6a-834">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-835">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-836">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-837">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-837">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-838">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-839">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-839">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-840">下列範例會計算 PI()/2 的正切函數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="aef6a-841">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="aef6a-842"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="aef6a-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="aef6a-843">傳回數值，截斷至最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="aef6a-844">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="aef6a-845">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="aef6a-846">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-847">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-847">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-848">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-849">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-849">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-850">下列範例會將以下正數和負數數字截斷為最接近的整數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="aef6a-851">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="aef6a-852"><a name="bk_type_checking_functions"></a>類型檢查函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="aef6a-853">下列函式支援針對輸入值檢查類型，並且會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="aef6a-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="aef6a-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="aef6a-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="aef6a-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="aef6a-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="aef6a-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="aef6a-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="aef6a-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="aef6a-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="aef6a-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="aef6a-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="aef6a-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="aef6a-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="aef6a-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="aef6a-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="aef6a-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="aef6a-862"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="aef6a-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="aef6a-863">傳回布林值，表示指定之運算式的類型為陣列。</span><span class="sxs-lookup"><span data-stu-id="aef6a-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="aef6a-864">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="aef6a-865">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-866">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-867">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-867">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-868">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-869">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-869">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-870">下列範例會使用 IS_ARRAY 函式，檢查 JSON 布林值的物件、數字、字串、Null、物件、陣列以及未定義的類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="aef6a-871">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="aef6a-872"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="aef6a-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="aef6a-873">傳回布林值，表示指定之運算式的類型為布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="aef6a-874">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="aef6a-875">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-876">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-877">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-877">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-878">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-879">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-879">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-880">下列範例會使用 IS_BOOL 函式，檢查 JSON 布林值的物件、數字、字串、Null、物件、陣列以及未定義的類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="aef6a-881">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="aef6a-882"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="aef6a-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="aef6a-883">傳回布林值，表示屬性是否已經指派值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="aef6a-884">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="aef6a-885">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-886">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-887">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-887">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-888">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-889">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-889">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-890">下列範例會檢查指定的 JSON 文件內的屬性是否存在。</span><span class="sxs-lookup"><span data-stu-id="aef6a-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="aef6a-891">第一次會傳回 True，因為出現了 "a"，但第二次就會傳回 False 因為 "b" 不存在。</span><span class="sxs-lookup"><span data-stu-id="aef6a-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="aef6a-892">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="aef6a-893"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="aef6a-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="aef6a-894">傳回布林值，表示指定之運算式的類型為 null。</span><span class="sxs-lookup"><span data-stu-id="aef6a-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="aef6a-895">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="aef6a-896">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-897">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-898">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-898">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-899">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-900">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-900">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-901">下列範例會使用 IS_NULL 函式，檢查 JSON 布林值的物件、數字、字串、Null、物件、陣列以及未定義的類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="aef6a-902">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="aef6a-903"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="aef6a-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="aef6a-904">傳回布林值，表示指定之運算式的類型為數字。</span><span class="sxs-lookup"><span data-stu-id="aef6a-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="aef6a-905">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="aef6a-906">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-907">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-908">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-908">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-909">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-910">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-910">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-911">下列範例會使用 IS_NULL 函式，檢查 JSON 布林值的物件、數字、字串、Null、物件、陣列以及未定義的類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="aef6a-912">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="aef6a-913"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="aef6a-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="aef6a-914">傳回布林值，表示指定之運算式的類型為 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="aef6a-915">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="aef6a-916">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-917">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-918">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-918">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-919">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-920">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-920">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-921">下列範例會使用 IS_OBJECT 函式，檢查 JSON 布林值的物件、數字、字串、Null、物件、陣列以及未定義的類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="aef6a-922">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="aef6a-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="aef6a-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="aef6a-924">傳回布林值，表示指定之運算式的類型為基本類型 (字串、布林值、數值或 Null)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="aef6a-925">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="aef6a-926">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-927">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-928">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-928">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-929">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-930">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-930">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-931">下列範例會使用 IS_PRIMITIVE 函式，檢查 JSON 布林值的物件、數字、字串、Null、物件、陣列以及未定義的類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="aef6a-932">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="aef6a-933"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="aef6a-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="aef6a-934">傳回布林值，表示指定之運算式的類型為字串。</span><span class="sxs-lookup"><span data-stu-id="aef6a-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="aef6a-935">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="aef6a-936">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="aef6a-937">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-938">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-938">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-939">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-940">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-940">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-941">下列範例會使用 IS_STRING 函式，檢查 JSON 布林值的物件、數字、字串、Null、物件、陣列以及未定義的類型。</span><span class="sxs-lookup"><span data-stu-id="aef6a-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="aef6a-942">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="aef6a-943"><a name="bk_string_functions"></a> 字串函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="aef6a-944">下列純量函數會對字串輸入值執行作業，並傳回字串、數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="aef6a-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="aef6a-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="aef6a-946">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="aef6a-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="aef6a-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="aef6a-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="aef6a-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="aef6a-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="aef6a-949">LEFT</span><span class="sxs-lookup"><span data-stu-id="aef6a-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="aef6a-950">LENGTH</span><span class="sxs-lookup"><span data-stu-id="aef6a-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="aef6a-951">LOWER</span><span class="sxs-lookup"><span data-stu-id="aef6a-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="aef6a-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="aef6a-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="aef6a-953">REPLACE</span><span class="sxs-lookup"><span data-stu-id="aef6a-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="aef6a-954">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="aef6a-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="aef6a-955">REVERSE</span><span class="sxs-lookup"><span data-stu-id="aef6a-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="aef6a-956">RIGHT</span><span class="sxs-lookup"><span data-stu-id="aef6a-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="aef6a-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="aef6a-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="aef6a-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="aef6a-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="aef6a-959">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="aef6a-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="aef6a-960">UPPER</span><span class="sxs-lookup"><span data-stu-id="aef6a-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="aef6a-961"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="aef6a-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="aef6a-962">傳回字串，該字串是串連兩個或多個字串值的結果。</span><span class="sxs-lookup"><span data-stu-id="aef6a-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="aef6a-963">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="aef6a-964">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-965">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-966">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-966">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-967">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-968">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-968">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-969">下列範例會傳回指定值的串連字串。</span><span class="sxs-lookup"><span data-stu-id="aef6a-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="aef6a-970">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="aef6a-971"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="aef6a-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="aef6a-972">傳回布林值，表示第一個字串運算式是否包含第二個字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="aef6a-973">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="aef6a-974">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-975">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-976">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-976">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-977">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-978">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-978">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-979">下列範例會檢查 "abc" 是否包含 "ab" 及 "d"。</span><span class="sxs-lookup"><span data-stu-id="aef6a-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="aef6a-980">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="aef6a-981"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="aef6a-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="aef6a-982">傳回布林值，表示第一個字串運算式是否以第二個字串運算式結尾。</span><span class="sxs-lookup"><span data-stu-id="aef6a-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="aef6a-983">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="aef6a-984">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-985">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-986">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-986">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-987">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-988">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-988">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-989">下列範例會傳回以 "b" 或 "bc" 結尾的 "abc"。</span><span class="sxs-lookup"><span data-stu-id="aef6a-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="aef6a-990">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="aef6a-991"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="aef6a-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="aef6a-992">傳回第一個指定的字串運算式中，第二個字串運算式第一次出現的開始位置，或者如果找不到字串，則為 -1。</span><span class="sxs-lookup"><span data-stu-id="aef6a-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="aef6a-993">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="aef6a-994">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-995">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-996">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-996">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-997">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-998">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-998">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-999">下列範例會傳回 "abc" 內各種子字串的索引。</span><span class="sxs-lookup"><span data-stu-id="aef6a-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="aef6a-1000">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="aef6a-1001"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="aef6a-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="aef6a-1002">傳回具有指定字元數目的字串左側部分。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="aef6a-1003">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="aef6a-1004">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1005">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="aef6a-1006">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-1007">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1008">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1009">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1009">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1010">下列範例會傳回 "abc"左側部分的各種長度值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="aef6a-1011">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="aef6a-1012"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="aef6a-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="aef6a-1013">傳回指定字串運算式的字元數目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1014">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1015">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1016">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1017">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1018">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1019">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1019">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1020">下列範例會傳回字串的長度。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="aef6a-1021">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="aef6a-1022"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="aef6a-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="aef6a-1023">傳回將大寫字元資料轉換成小寫之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="aef6a-1024">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1025">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1026">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1027">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1028">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1029">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1029">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1030">下列範例示範如何在查詢中使用 LOWER。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="aef6a-1031">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="aef6a-1032"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="aef6a-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="aef6a-1033">傳回移除開頭空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="aef6a-1034">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1035">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1036">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1037">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1038">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1039">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1039">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1040">下列範例示範如何在查詢中使用 LTRIM。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="aef6a-1041">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="aef6a-1042"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="aef6a-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="aef6a-1043">使用其他字串值取代指定的字串值的所有項目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="aef6a-1044">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1045">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1046">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1047">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1048">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1049">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1049">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1050">下列範例示範如何在查詢中使用 REPLACE。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="aef6a-1051">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="aef6a-1052"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="aef6a-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="aef6a-1053">將字串值重複指定的次數。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="aef6a-1054">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="aef6a-1055">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1056">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="aef6a-1057">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-1058">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1059">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1060">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1060">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1061">下列範例示範如何在查詢中使用 REPLICATE。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="aef6a-1062">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="aef6a-1063"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="aef6a-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="aef6a-1064">傳回反向順序的字串值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="aef6a-1065">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1066">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1067">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1068">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1069">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1070">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1070">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1071">下列範例示範如何在查詢中使用 REVERSE。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="aef6a-1072">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="aef6a-1073"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="aef6a-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="aef6a-1074">傳回具有指定字元數目的字串右側部分。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="aef6a-1075">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="aef6a-1076">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1077">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="aef6a-1078">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-1079">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1080">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1081">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1081">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1082">下列範例會傳回 "abc"右側部分的各種長度值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="aef6a-1083">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="aef6a-1084"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="aef6a-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="aef6a-1085">傳回移除結尾空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="aef6a-1086">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1087">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1088">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1089">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1090">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1091">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1091">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1092">下列範例示範如何在查詢中使用 RTRIM。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="aef6a-1093">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="aef6a-1094"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="aef6a-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="aef6a-1095">傳回布林值，表示第一個字串運算式是否以第二個字串運算式開頭。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="aef6a-1096">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1097">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1098">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1099">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1100">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-1101">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1101">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1102">下列範例會檢查字串 "abc" 是否以 "b" 和 "a" 開頭。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="aef6a-1103">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="aef6a-1104"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="aef6a-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="aef6a-1105">傳回字串運算式的部分，從指定字元以零為起始的位置開始，直到指定的長度，或直到字串的結尾。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="aef6a-1106">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="aef6a-1107">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1108">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="aef6a-1109">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-1110">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1111">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1112">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1112">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1113">下列範例會傳回從 1 開始，且長度為 1 個字元的子字串 "abc"。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="aef6a-1114">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="aef6a-1115"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="aef6a-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="aef6a-1116">傳回將小寫字元資料轉換成大寫之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="aef6a-1117">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="aef6a-1118">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="aef6a-1119">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1120">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1121">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="aef6a-1122">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1122">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1123">下列範例示範如何在查詢中使用 UPPER</span><span class="sxs-lookup"><span data-stu-id="aef6a-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="aef6a-1124">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="aef6a-1125"><a name="bk_array_functions"></a> 陣列函陣列函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="aef6a-1126">下列純量值函式會對陣列輸入值執行作業，並傳回數值、布林值或陣列值</span><span class="sxs-lookup"><span data-stu-id="aef6a-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="aef6a-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="aef6a-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="aef6a-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="aef6a-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="aef6a-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="aef6a-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="aef6a-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="aef6a-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="aef6a-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="aef6a-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="aef6a-1132">傳回串連兩個或多個陣列值之結果的陣列。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="aef6a-1133">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="aef6a-1134">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="aef6a-1135">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="aef6a-1136">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1137">傳回陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="aef6a-1138">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1138">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1139">下列範例顯示如何串連兩個陣列。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="aef6a-1140">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="aef6a-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="aef6a-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="aef6a-1142">傳回布林值，表示陣列是否包含指定值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="aef6a-1143">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="aef6a-1144">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="aef6a-1145">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="aef6a-1146">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="aef6a-1147">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1148">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="aef6a-1149">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1149">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1150">下列範例說明如何使用 ARRAY_CONTAINS 檢查陣列中的成員資格。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="aef6a-1151">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="aef6a-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="aef6a-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="aef6a-1153">傳回指定陣列運算式的元素數目。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="aef6a-1154">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="aef6a-1155">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="aef6a-1156">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="aef6a-1157">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1158">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-1159">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1159">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1160">下列範例說明如何使用 ARRAY_LENGTH 取得陣列的長度。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="aef6a-1161">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="aef6a-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="aef6a-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="aef6a-1163">傳回陣列運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="aef6a-1164">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="aef6a-1165">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="aef6a-1166">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="aef6a-1167">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="aef6a-1168">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1169">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="aef6a-1170">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1170">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1171">下列範例說明如何使用 ARRAY_SLICE 取得陣列的一部分。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="aef6a-1172">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="aef6a-1173"><a name="bk_spatial_functions"></a> 空間函式</span><span class="sxs-lookup"><span data-stu-id="aef6a-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="aef6a-1174">下列純量值函式會對空間物件輸入值執行作業，並傳回數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="aef6a-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="aef6a-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="aef6a-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="aef6a-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="aef6a-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="aef6a-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="aef6a-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="aef6a-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="aef6a-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="aef6a-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="aef6a-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="aef6a-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="aef6a-1181">傳回兩個 GeoJSON Point、Polygon 或 LineString 運算式之間的距離。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="aef6a-1182">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="aef6a-1183">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="aef6a-1184">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="aef6a-1185">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1186">傳回數值運算式，其中包含距離。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="aef6a-1187">這在預設參照系統中以公尺表示。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="aef6a-1188">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1188">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1189">以下範例顯示如何使用ST_DISTANCE 內建函式傳回所有家族文件，且這些文件在 30 公里的指定位置內。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="aef6a-1190">。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="aef6a-1191">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="aef6a-1192"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="aef6a-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="aef6a-1193">傳回布林運算式，指出第一個引數中指定的 GeoJSON 物件 (Point、Polygon 或 LineString) 是否位在第二個引數中的 GeoJSON (Point、Polygon 或 LineString) 內。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="aef6a-1194">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="aef6a-1195">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="aef6a-1196">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="aef6a-1197">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="aef6a-1198">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1199">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="aef6a-1200">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1200">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1201">下列範例說明如何使用 ST_WITHIN 尋找多邊形內的所有家族文件。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="aef6a-1202">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="aef6a-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="aef6a-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="aef6a-1204">傳回布林運算式，指出第一個引數交集中指定的 GeoJSON 物件 (Point、Polygon 或 LineString) 是否位在第二個引數中的 GeoJSON (Point、Polygon 或 LineString) 內。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="aef6a-1205">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="aef6a-1206">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="aef6a-1207">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="aef6a-1208">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="aef6a-1209">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1210">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="aef6a-1211">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1211">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1212">下列範例說明如何尋找與給定的多邊形交集的所有區域。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="aef6a-1213">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="aef6a-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="aef6a-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="aef6a-1215">傳回布林值，指出指定的 GeoJSON Point、Polygon 或 LineString 運算式是否有效。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="aef6a-1216">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="aef6a-1217">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="aef6a-1218">為任何有效的 GeoJSON 點、Polygon 或 LineString 運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="aef6a-1219">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1220">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="aef6a-1221">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1221">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1222">下列範例說明如何使用 ST_VALID 檢查點是否有效。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="aef6a-1223">例如，此點的維度值不在數值 [-90, 90] 的有效範圍內，因此查詢會傳回 False。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="aef6a-1224">對於多邊形，GeoJSON 規格需要此資料；若要建立一個封閉的形狀，最後一個座標組應該與第一個座標組相同。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="aef6a-1225">多邊形內的點必須以逆時針順序指定。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="aef6a-1226">以順時針順序指定多邊形，代表區域內的反轉。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="aef6a-1227">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="aef6a-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="aef6a-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="aef6a-1229">如果指定的 GeoJSON Point、Polygon 或 LineString 運算式有效，就傳回包含布林值的 JSON 值；但如果是無效的，就會額外加上做為字串值的原因。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="aef6a-1230">**語法**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="aef6a-1231">**引數**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="aef6a-1232">為任何有效的 GeoJSON 點或多邊形運算式。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="aef6a-1233">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="aef6a-1234">如果指定的 GeoJSON 點或多邊形運算式是有效的，就會傳回包含布林值的 JSON 值；但如果是無效的，就會額外加上做為字串值的原因。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="aef6a-1235">**範例**</span><span class="sxs-lookup"><span data-stu-id="aef6a-1235">**Examples**</span></span>  
  
 <span data-ttu-id="aef6a-1236">下列範例說明如何使用 ST_ISVALIDDETAILED 檢查有效性 (包含詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="aef6a-1237">以下為結果集。</span><span class="sxs-lookup"><span data-stu-id="aef6a-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="aef6a-1238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aef6a-1238">Next steps</span></span>  
 <span data-ttu-id="aef6a-1239">[適用於Azure Cosmos DB 的 SQL 語法和 SQL 查詢](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="aef6a-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="aef6a-1240">Azure Cosmos DB 文件</span><span class="sxs-lookup"><span data-stu-id="aef6a-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
