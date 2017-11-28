---
<span data-ttu-id="7e8bb-101">標題： aaa"Azure Cosmos DB DocumentDB API: SQL 語法 |Microsoft 文件"描述： 參考文件以 hello Azure Cosmos DB DocumentDB API SQL 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="7e8bb-102">服務： cosmos db 作者： mimig1 管理員： jhubbard 編輯器： mimig documentationcenter: '</span><span class="sxs-lookup"><span data-stu-id="7e8bb-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="7e8bb-103">ms.assetid: ms.service: cosmos db ms.workload： 資料服務 ms.tgt_pltfrm: na ms.devlang: na ms.topic： 參考 ms.date: 06/13/2017 ms.author: mimig</span><span class="sxs-lookup"><span data-stu-id="7e8bb-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="7e8bb-104">Azure Cosmos DB DocumentDB API：SQL 語法參考</span><span class="sxs-lookup"><span data-stu-id="7e8bb-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="7e8bb-105">hello Azure Cosmos DB DocumentDB API 像文法，透過階層式 JSON 而不需要明確的結構描述或建立次要索引，支援使用熟悉的 SQL （結構化查詢語言） 查詢文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="7e8bb-106">本主題提供 hello DocumentDB API SQL 查詢語言參考文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="7e8bb-107">逐步解說中的 hello DocumentDB API SQL 查詢語言，請參閱[SQL 查詢 Azure Cosmos DB DocumentDB api](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="7e8bb-108">我們也邀請您 toovisit hello[查詢遊樂場](http://www.documentdb.com/sql/demo)您可以在此 Azure Cosmos DB 再試一次，並對我們的資料集執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="7e8bb-109">SELECT 查詢</span><span class="sxs-lookup"><span data-stu-id="7e8bb-109">SELECT query</span></span>  
<span data-ttu-id="7e8bb-110">從 hello 資料庫擷取 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="7e8bb-111">支援運算式評估、規劃、篩選和聯結。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="7e8bb-112">hello 慣例用來描述 hello SELECT 陳述式會在 hello 語法慣例 > 一節中製成資料表。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="7e8bb-113">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="7e8bb-114">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-114">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-115">如需每個子句的詳細資料，請參閱下列各節：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="7e8bb-116">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="7e8bb-117">FROM 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="7e8bb-118">WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="7e8bb-119">ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="7e8bb-120">hello SELECT 陳述式中的 hello 子句的順序必須如上所示。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="7e8bb-121">可以省略任何一個 hello 選擇性子句。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="7e8bb-122">但是，當使用選擇性的子句時，它們必須顯示 hello 正確的順序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="7e8bb-123">**Hello SELECT 陳述式的邏輯處理順序**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="7e8bb-124">子句的處理 hello 順序為：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="7e8bb-125">FROM 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="7e8bb-126">WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="7e8bb-127">ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="7e8bb-128">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="7e8bb-129">請注意，這不同於在 hello hello 語法中出現的順序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="7e8bb-130">hello 排序，這類處理的子句所導入的所有新符號是可見和可在稍後處理的子句。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="7e8bb-131">例如，您可以在 WHERE 和 SELECT 子句中存取 FROM 子句中宣告的別名。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="7e8bb-132">**空白字元和註解**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="7e8bb-133">所有空白字元不屬於引號的字串或引號識別項不 hello 語言文法的一部分，而且會在剖析期間忽略。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="7e8bb-134">hello 查詢語言支援 T-SQL 樣式的註解類似</span><span class="sxs-lookup"><span data-stu-id="7e8bb-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="7e8bb-135">陳述式`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="7e8bb-136">雖然空白字元和註解沒有任何重要性 hello 文法中，它們必須使用的 tooseparate 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="7e8bb-137">例如：`-1e5` 是單一數字的權杖，而 `: – 1 e5` 則是加上減號的權杖，後面接著數字 1 和識別碼 e5。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="7e8bb-138"><a name="bk_select_query"></a> SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="7e8bb-139">hello SELECT 陳述式中的 hello 子句的順序必須如上所示。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="7e8bb-140">可以省略任何一個 hello 選擇性子句。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="7e8bb-141">但是，當使用選擇性的子句時，它們必須顯示 hello 正確的順序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="7e8bb-142">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="7e8bb-143">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="7e8bb-144">設定屬性或值 toobe 選取 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="7e8bb-145">指定應該擷取 hello 值，而不進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="7e8bb-146">特別是如果處理 hello 值是物件，將會擷取所有屬性。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="7e8bb-147">指定擷取的屬性 toobe hello 清單。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="7e8bb-148">每個傳回的值將是具有 hello 屬性指定的物件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="7e8bb-149">指定應該擷取 hello JSON 值，而不是 hello 完整的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="7e8bb-150">這不同的是`<property_list>`不會換行投射的 hello 值物件中。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="7e8bb-151">代表 hello 值 toobe 運算式計算。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="7e8bb-152">請參閱[純量運算式](#bk_scalar_expressions)一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="7e8bb-153">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-153">**Remarks**</span></span>  
  
<span data-ttu-id="7e8bb-154">hello`SELECT *`語法才會有效 FROM 子句已宣告一個別名。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="7e8bb-155">`SELECT *` 提供一個身分識別投影，在無需投影的情況下會非常實用。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="7e8bb-156">SELECT * 只有在已指定 FROM 子句且只導入單一輸入來源時才有效。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="7e8bb-157">請注意，`SELECT <select_list>` 和 `SELECT *` 為「語法捷徑」，可以使用如下所示的簡單 SELECT 陳述式另外表示。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="7e8bb-158">相當於：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="7e8bb-159">相當於：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="7e8bb-160">**另請參閱**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-160">**See Also**</span></span>  
  
[<span data-ttu-id="7e8bb-161">純量運算式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="7e8bb-162">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="7e8bb-163"><a name="bk_from_clause"></a>FROM 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="7e8bb-164">指定 hello 來源或聯結的來源。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="7e8bb-165">hello FROM 子句是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-165">hello FROM clause is optional.</span></span> <span data-ttu-id="7e8bb-166">若未指定，系統仍然會在如同 FROM 子句提供了單一文件的情況下執行其他子句。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="7e8bb-167">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="7e8bb-168">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="7e8bb-169">指定包含或不包含別名的資料來源。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="7e8bb-170">如果未指定別名，它會從推斷 hello`<collection_expression>`使用下列規則：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="7e8bb-171">如果 hello 運算式是 collection_name，collection_name 將使用做為別名。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="7e8bb-172">如果 hello 運算式`<collection_expression>`，則 property_name 會作為別名。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="7e8bb-173">如果 hello 運算式是 collection_name，collection_name 將使用做為別名。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="7e8bb-174">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="7e8bb-175">指定該 hello`input_alias`是一組 hello 基礎集合運算式所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="7e8bb-176">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="7e8bb-177">指定該 hello`input_alias`應該代表 hello 組來逐一查看每個陣列 hello 基礎集合運算式所傳回的所有陣列項目取得的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="7e8bb-178">會忽略任何由基礎集合運算式傳回的任何非陣列的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="7e8bb-179">指定 hello 集合運算式 toobe 使用 tooretrieve hello 文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="7e8bb-180">指定應該從 hello 預設，目前連接的集合中擷取該文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="7e8bb-181">指定應該從提供的 hello 集合中擷取該文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="7e8bb-182">hello hello 集合名稱必須符合目前已連線到 hello 集合 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="7e8bb-183">指定應該從 hello 擷取該文件以 hello 提供別名定義其他來源。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="7e8bb-184">指定應該擷取該文件，藉由存取 hello`property_name`屬性或 array_index 陣列元素的所有文件，來擷取指定之集合運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="7e8bb-185">指定應該擷取該文件，藉由存取 hello`property_name`屬性或 array_index 陣列元素的所有文件，來擷取指定之集合運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="7e8bb-186">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-186">**Remarks**</span></span>  
  
<span data-ttu-id="7e8bb-187">所有的別名中提供或推斷 hello `<from_source>(`s) 必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="7e8bb-188">hello 語法`<collection_expression>.`property_name 是 hello 與相同`<collection_expression>' ['"property_name"']'`。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="7e8bb-189">不過，如果屬性名稱包含非識別碼字元，可以使用 hello 後者的語法。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="7e8bb-190">**遺漏的屬性、遺漏的陣列元素、未定義的值處理**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="7e8bb-191">若集合運算式存取屬性或陣列元素，且該值不存在，則會忽略該值且不會進一步處理。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="7e8bb-192">**集合運算式內容範圍**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="7e8bb-193">集合運算方式可以是集合範圍或文件範圍：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="7e8bb-194">運算式是集合範圍，如果 hello hello 集合運算式的基礎來源為 ROOT 或`collection_name`。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="7e8bb-195">這類運算式代表一組直接從 hello 集合中擷取的文件，並不會相依於其他集合運算式的 hello 處理。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="7e8bb-196">運算式是文件範圍，如果 hello hello 集合運算式的基礎來源是`input_alias`早導入 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="7e8bb-197">這類運算式表示一組藉由評估 hello 範圍中的每個屬於 toohello 組與 hello 別名集合相關聯的文件的 hello 集合運算式取得的文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="7e8bb-198">hello 結果集將會取得藉由評估 hello 集合運算式，針對每個 hello 基礎集合中的 hello 文件集的聯集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="7e8bb-199">**聯結**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-199">**Joins**</span></span>  
  
<span data-ttu-id="7e8bb-200">在 hello 目前版本中，Azure Cosmos DB 支援內部聯結。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="7e8bb-201">即將推出其他聯結功能。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="7e8bb-202">在完整的交叉乘積的 hello 的內部聯結結果設定參與 hello 聯結。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="7e8bb-203">hello N 方聯結結果是一組 N 元素 tuple，其中 hello tuple 中的每個值都與 hello 別名 hello 聯結中設定 參與關聯，而可以參考其他子句中的該別名來存取。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="7e8bb-204">hello 聯結的 hello 評估 hello 參與集 hello 內容範圍而定：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="7e8bb-205">集合組 A 和集合範圍組 B 之間的聯結會產生集合 A 和 B 中所有元素的交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="7e8bb-206">集合組 A 和文件範圍組 B 之間的聯結會產生所有集合的聯集，是依評估集合 A 的每個文件的文件範圍集合 B 來取得。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="7e8bb-207">在 hello 目前版本中，一個集合範圍運算式最多可支援由 hello 查詢處理器。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="7e8bb-208">**聯結範例：**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="7e8bb-209">讓我們看看下列 FROM 子句的 hello:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="7e8bb-210">讓每個來源定義 `input_alias1, input_alias2, …, input_aliasN`。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="7e8bb-211">這個 FROM 子句會傳回一組 N-Tuple (具有 N 個值的 Tuple)。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="7e8bb-212">每個 Tuple 所擁有的值，都是將所有集合別名在其個別集合上反覆運算所產生。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="7e8bb-213">*JOIN 範例 1，搭配 2 個來源：*</span><span class="sxs-lookup"><span data-stu-id="7e8bb-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="7e8bb-214">讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="7e8bb-215">讓 `<from_source2>` 為參照 input_alias1 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="7e8bb-216">{1, 2} 為 `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="7e8bb-217">{3} 為 `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="7e8bb-218">{4, 5} 為 `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="7e8bb-219">FROM 子句 hello`<from_source1> JOIN <from_source2>`會導致下列 tuple 的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e8bb-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="7e8bb-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="7e8bb-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="7e8bb-221">*JOIN 範例 2，搭配 3 個來源：*</span><span class="sxs-lookup"><span data-stu-id="7e8bb-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="7e8bb-222">讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="7e8bb-223">讓 `<from_source2>` 為參照 `input_alias1` 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="7e8bb-224">{1, 2} 為 `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="7e8bb-225">{3} 為 `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="7e8bb-226">{4, 5} 為 `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="7e8bb-227">讓 `<from_source3>` 為參照 `input_alias2` 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="7e8bb-228">{100, 200} 為 `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="7e8bb-229">{300}為 `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="7e8bb-230">FROM 子句 hello`<from_source1> JOIN <from_source2> JOIN <from_source3>`會導致下列 tuple 的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e8bb-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="7e8bb-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="7e8bb-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="7e8bb-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="7e8bb-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7e8bb-233">缺乏的其他值的 tuple `input_alias1`， `input_alias2`，哪些 hello`<from_source3>`未傳回任何值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="7e8bb-234">*JOIN 範例 3，搭配 3 個來源：*</span><span class="sxs-lookup"><span data-stu-id="7e8bb-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="7e8bb-235">讓 <from_source1> 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="7e8bb-236">讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="7e8bb-237">讓 <from_source2> 為參照 input_alias1 的文件範圍，並代表以下集：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="7e8bb-238">{1, 2} 為 `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="7e8bb-239">{3} 為 `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="7e8bb-240">{4, 5} 為 `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="7e8bb-241">可讓`<from_source3>`太範圍`input_alias1`，而且代表集：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="7e8bb-242">{100, 200} 為 `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="7e8bb-243">{300}為 `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="7e8bb-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="7e8bb-244">FROM 子句 hello`<from_source1> JOIN <from_source2> JOIN <from_source3>`會導致下列 tuple 的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e8bb-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="7e8bb-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="7e8bb-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="7e8bb-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="7e8bb-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7e8bb-247">這會導致之間的交叉乘積`<from_source2>`和`<from_source3>`因為兩者都已設定領域的 toohello 相同`<from_source1>`。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="7e8bb-248">這會讓 4 (2x2) Tuple 具備值 A，0 Tuple 具備值 B (1x0) 而 2 (2x1) Tuple 具備值 C。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="7e8bb-249">**另請參閱**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-249">**See also**</span></span>  
  
 [<span data-ttu-id="7e8bb-250">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="7e8bb-251"><a name="bk_where_clause"></a>WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="7e8bb-252">指定 hello hello hello 查詢所傳回的文件的搜尋條件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="7e8bb-253">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="7e8bb-254">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="7e8bb-255">指定符合的傳回 hello 文件 toobe hello 條件 toobe。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="7e8bb-256">代表 hello 值 toobe 運算式計算。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="7e8bb-257">請參閱 hello[純量運算式](#bk_scalar_expressions)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="7e8bb-258">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-258">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-259">為了讓 hello 文件 toobe 會傳回指定為篩選條件必須評估 tootrue 的運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="7e8bb-260">只有布林值 true 會滿足 hello 條件，任何其他值： 未定義、 null、 false、 數字、 陣列或物件並不符合 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="7e8bb-261"><a name="bk_orderby_clause"></a>ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="7e8bb-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="7e8bb-262">指定排序次序 hello 查詢所傳回結果的 hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="7e8bb-263">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="7e8bb-264">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="7e8bb-265">指定屬性或在其設定 toosort hello 查詢結果的運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="7e8bb-266">排序資料行可指定為名稱或資料行別名。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="7e8bb-267">可以指定多個排序資料行。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="7e8bb-268">資料行必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-268">Column names must be unique.</span></span> <span data-ttu-id="7e8bb-269">hello hello ORDER BY 子句中的 hello 排序資料行的順序定義 hello 組織 hello 排序結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="7e8bb-270">也就是說，hello 結果集依照 hello 第一個屬性，然後該排序的清單依照 hello 第二個屬性，依此類推。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="7e8bb-271">hello hello ORDER BY 子句中參考的資料行名稱必須對應的 tooeither hello 中的資料行選取清單或 tooa 中沒有任何模稜兩可的 hello FROM 子句中指定的資料表定義的資料行。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="7e8bb-272">指定哪些 toosort hello 查詢結果集上的單一屬性或運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="7e8bb-273">請參閱 hello[純量運算式](#bk_scalar_expressions)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="7e8bb-274">指定的 hello 指定資料行中的 hello 值應該以遞增或遞減順序排序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="7e8bb-275">ASC 從最低值 toohighest 值 hello 進行排序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="7e8bb-276">DESC 從最高值 toolowest 值進行排序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="7e8bb-277">ASC 是 hello 預設排序順序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-277">ASC is hello default sort order.</span></span> <span data-ttu-id="7e8bb-278">Null 值會視為 hello 最低的可能值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="7e8bb-279">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-279">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-280">即使 hello 查詢文法支援多個順序屬性，但是 hello Azure Cosmos DB 查詢執行階段會支援排序只針對單一屬性，並只對屬性名稱，亦即，不是針對計算的屬性。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="7e8bb-281">排序也需要編製索引原則該 hello 包含 hello 屬性與 hello 指定範圍的索引類型，含 hello 最大有效位數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="7e8bb-282">Toohello 編製索引原則文件，如需詳細資訊，請參閱。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="7e8bb-283"><a name="bk_scalar_expressions"></a>純量運算式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="7e8bb-284">純量運算式是符號的組合，而且可運算子評估 tooobtain 單一值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="7e8bb-285">簡單運算式可以是常數、屬性參考、陣列元素參考、別名參考或函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="7e8bb-286">簡單運算式可以透過使用運算子，與複雜運算式結合。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="7e8bb-287">如需純量運算式具備哪些值的詳細資料，請參閱[常數](#bk_constants)一節。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="7e8bb-288">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-289">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="7e8bb-290">代表常數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-290">Represents a constant value.</span></span> <span data-ttu-id="7e8bb-291">如需詳細資料，請參閱[常數](#bk_constants)一節。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="7e8bb-292">代表 hello 所定義的值`input_alias`hello 中導入`FROM`子句。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="7e8bb-293">這個值保證 toonot 是**未定義**–**未定義**hello 輸入中的值會略過。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="7e8bb-294">代表物件的 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="7e8bb-295">如果 hello 屬性不存在，或參考屬性的值不是物件，則 hello 運算式的評估太**未定義**值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="7e8bb-296">代表 hello 屬性名稱與值`property_name`或具有索引的陣列元素`array_index`的物件/陣列。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="7e8bb-297">如果 hello 屬性/陣列索引不存在或 hello 屬性/陣列索引參考的值不是物件/陣列，接著 hello 運算式會評估 tooundefined 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="7e8bb-298">表示的運算子所套用的 tooa 的單一值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="7e8bb-299">如需詳細資料，請參閱[運算子](#bk_operators)一節。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="7e8bb-300">表示已套用的 tootwo 值的運算子。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="7e8bb-301">如需詳細資料，請參閱[運算子](#bk_operators)一節。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="7e8bb-302">代表由函式呼叫結果定義的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="7e8bb-303">定義純量函數 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="7e8bb-304">Hello 內建的純量函數的名稱。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="7e8bb-305">代表搭配指定屬性及其值所建立之新物件取得的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="7e8bb-306">代表搭配指定值作為元素所建立之新物件取得的值</span><span class="sxs-lookup"><span data-stu-id="7e8bb-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="7e8bb-307">代表 hello 指定的參數名稱的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="7e8bb-308">參數名稱必須帶有單一 @ 作為 hello 第一個字元。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="7e8bb-309">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-309">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-310">呼叫內建或使用者定義純量值函式時，必須定義所有引數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="7e8bb-311">如果未定義任何 hello 引數，將不會呼叫 hello 函式和 hello 結果會是未定義。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="7e8bb-312">建立物件時，將略過不包含在建立物件的 hello 獲派值未定義任何屬性。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="7e8bb-313">當建立陣列的任何項目值可指派**未定義**將略過不包含在 hello 建立物件的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="7e8bb-314">這會導致 hello 接著定義項目 tootake 其所在位置的方式建立 hello 陣列將沒有略過索引。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="7e8bb-315"><a name="bk_operators"></a> 運算子</span><span class="sxs-lookup"><span data-stu-id="7e8bb-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="7e8bb-316">本章節描述支援的 hello 運算子。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-316">This section describes hello supported operators.</span></span> <span data-ttu-id="7e8bb-317">每個運算子可以是指派的 tooexactly 一個類別目錄。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="7e8bb-318">請參閱以下的**運算子類別**表格，如需處理**未定義**值的詳細資料，請輸入輸入值的需求，以及透過不相符的值處理值的需求。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="7e8bb-319">**運算子類別：**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="7e8bb-320">**類別**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-320">**Category**</span></span>|<span data-ttu-id="7e8bb-321">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="7e8bb-322">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-322">**arithmetic**</span></span>|<span data-ttu-id="7e8bb-323">運算子預期輸入 toobe 號碼。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="7e8bb-324">輸出也是數字。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-324">Output is also a Number.</span></span> <span data-ttu-id="7e8bb-325">如果任一 hello 輸入**未定義**或數字則 hello 結果以外的型別為**未定義**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="7e8bb-326">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-326">**bitwise**</span></span>|<span data-ttu-id="7e8bb-327">運算子預期輸入 toobe 32 位元帶正負號的正負號的整數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="7e8bb-328">輸出也為 32 位元的帶正負號整數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="7e8bb-329">任何非整數值均會進行四捨五入。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="7e8bb-330">正值會無條件捨去，負值則會進位。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="7e8bb-331">取得最後 32 位元的它的補數標記法，將轉換 hello 32 位元整數範圍以外的任何值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="7e8bb-332">如果任一 hello 輸入**未定義**或 hello 結果是，請輸入數字，以外**未定義**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="7e8bb-333">**注意：** hello 上述行為會與 JavaScript 位元運算子行為相容。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="7e8bb-334">**logical**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-334">**logical**</span></span>|<span data-ttu-id="7e8bb-335">運算子預期輸入 toobe 布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="7e8bb-336">輸出也是布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="7e8bb-337">如果任一 hello 輸入**未定義**hello 結果將會輸入而不是布林值，或**未定義**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="7e8bb-338">**comparison**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-338">**comparison**</span></span>|<span data-ttu-id="7e8bb-339">運算子預期輸入 toohave hello 相同類型，而且不是 未定義。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="7e8bb-340">輸出也是布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="7e8bb-341">如果任一 hello 輸入**未定義**hello 輸入或是不同的類型，則 hello 結果是**未定義**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="7e8bb-342">請參閱**比較值順序**表格以取得值順序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="7e8bb-343">**字串**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-343">**string**</span></span>|<span data-ttu-id="7e8bb-344">運算子預期輸入 toobe 字串。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="7e8bb-345">輸出也是字串。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-345">Output is also a String.</span></span><br /><span data-ttu-id="7e8bb-346">如果任一 hello 輸入**未定義**或字串，然後 hello 結果以外的型別為**未定義**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="7e8bb-347">**一元運算子**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="7e8bb-348">**名稱**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-348">**Name**</span></span>|<span data-ttu-id="7e8bb-349">**運算子**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-349">**Operator**</span></span>|<span data-ttu-id="7e8bb-350">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="7e8bb-351">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="7e8bb-352">傳回 hello 數字值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="7e8bb-353">位元否定。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-353">Bitwise negation.</span></span> <span data-ttu-id="7e8bb-354">傳回否定的數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="7e8bb-355">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-355">**bitwise**</span></span>|~|<span data-ttu-id="7e8bb-356">1 的補數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-356">Ones' complement.</span></span> <span data-ttu-id="7e8bb-357">傳回數值的補數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="7e8bb-358">**Logical**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-358">**Logical**</span></span>|<span data-ttu-id="7e8bb-359">**NOT**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-359">**NOT**</span></span>|<span data-ttu-id="7e8bb-360">否定。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-360">Negation.</span></span> <span data-ttu-id="7e8bb-361">傳回否定布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="7e8bb-362">**二元運算子：**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="7e8bb-363">**名稱**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-363">**Name**</span></span>|<span data-ttu-id="7e8bb-364">**運算子**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-364">**Operator**</span></span>|<span data-ttu-id="7e8bb-365">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="7e8bb-366">**arithmetic**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="7e8bb-367">加法。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-367">Addition.</span></span><br /><br /> <span data-ttu-id="7e8bb-368">減法。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="7e8bb-369">乘法。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="7e8bb-370">除法。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-370">Division.</span></span><br /><br /> <span data-ttu-id="7e8bb-371">調節。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-371">Modulation.</span></span>|  
|<span data-ttu-id="7e8bb-372">**bitwise**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-372">**bitwise**</span></span>|<span data-ttu-id="7e8bb-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="7e8bb-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="7e8bb-374">位元 OR。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="7e8bb-375">位元 AND。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="7e8bb-376">位元 XOR。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="7e8bb-377">向左移位。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="7e8bb-378">向右移位。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="7e8bb-379">向右移位並填滿零。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="7e8bb-380">**logical**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-380">**logical**</span></span>|<span data-ttu-id="7e8bb-381">**AND**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-381">**AND**</span></span><br /><br /> <span data-ttu-id="7e8bb-382">**或**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-382">**OR**</span></span>|<span data-ttu-id="7e8bb-383">邏輯結合。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-383">Logical conjunction.</span></span> <span data-ttu-id="7e8bb-384">若兩個引數都為 **True**，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="7e8bb-385">邏輯結合。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-385">Logical conjunction.</span></span> <span data-ttu-id="7e8bb-386">若兩個引數都為 **True**，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="7e8bb-387">**comparison**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="7e8bb-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="7e8bb-389">**??**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-389">**??**</span></span>|<span data-ttu-id="7e8bb-390">等於。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-390">Equals.</span></span> <span data-ttu-id="7e8bb-391">若引數相等，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="7e8bb-392">不等於。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-392">Not equal to.</span></span> <span data-ttu-id="7e8bb-393">若引數不相等，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="7e8bb-394">大於。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-394">Greater Than.</span></span> <span data-ttu-id="7e8bb-395">傳回**true**如果第一個引數為大於 hello 第二個項目，傳回**false**否則。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="7e8bb-396">大於或等於。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-396">Greater Than or Equal To.</span></span> <span data-ttu-id="7e8bb-397">傳回**true**如果第一個引數大於或等於第二個 toohello，傳回**false**否則。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="7e8bb-398">小於。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-398">Less Than.</span></span> <span data-ttu-id="7e8bb-399">傳回**true**如果第一個引數小於 hello 第二個，傳回**false**否則。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="7e8bb-400">小於或等於。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-400">Less Than or Equal To.</span></span> <span data-ttu-id="7e8bb-401">傳回**true**如果第一個引數小於或等於 toohello 第二個其中一個，傳回**false**否則。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="7e8bb-402">聯合。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-402">Coalesce.</span></span> <span data-ttu-id="7e8bb-403">傳回 hello 第二個引數，如果第一個引數 hello**未定義**值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="7e8bb-404">**String**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-404">**String**</span></span>|<span data-ttu-id="7e8bb-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-405">**&#124;&#124;**</span></span>|<span data-ttu-id="7e8bb-406">串連。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-406">Concatenation.</span></span> <span data-ttu-id="7e8bb-407">傳回兩個引數的串連。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="7e8bb-408">**三元運算子：** </span><span class="sxs-lookup"><span data-stu-id="7e8bb-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="7e8bb-409">三元運算子</span><span class="sxs-lookup"><span data-stu-id="7e8bb-409">Ternary operator</span></span>|<span data-ttu-id="7e8bb-410">?</span><span class="sxs-lookup"><span data-stu-id="7e8bb-410">?</span></span>|<span data-ttu-id="7e8bb-411">傳回 hello 第二個引數，如果 hello 第一個引數的評估太**true**; 否則傳回 hello 第三個引數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="7e8bb-412">**比較值順序**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="7e8bb-413">**類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-413">**Type**</span></span>|<span data-ttu-id="7e8bb-414">**值順序**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="7e8bb-415">**未定義**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-415">**Undefined**</span></span>|<span data-ttu-id="7e8bb-416">無法比較。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-416">Not comparable.</span></span>|  
|<span data-ttu-id="7e8bb-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-417">**Null**</span></span>|<span data-ttu-id="7e8bb-418">單一值：**Null**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-418">Single value: **null**</span></span>|  
|<span data-ttu-id="7e8bb-419">**Number**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-419">**Number**</span></span>|<span data-ttu-id="7e8bb-420">自然實數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="7e8bb-421">負的無限值小於其他任何數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="7e8bb-422">正無限值大於其他任何數值。**NaN** 值無法比較。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="7e8bb-423">與 **NaN** 比較會產生**未定義的**值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="7e8bb-424">**String**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-424">**String**</span></span>|<span data-ttu-id="7e8bb-425">詞彙編篡順序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="7e8bb-426">**Array**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-426">**Array**</span></span>|<span data-ttu-id="7e8bb-427">沒有順序，但合理。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="7e8bb-428">**Object**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-428">**Object**</span></span>|<span data-ttu-id="7e8bb-429">沒有順序，但合理。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="7e8bb-430">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-430">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-431">在 Azure Cosmos DB，hello 類型的值通常之前，無法得知它們實際從 hello 資料庫中擷取。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="7e8bb-432">順序 toosupport 能夠有效率地執行查詢，在大部分的 hello 運算子會有嚴格的型別需求。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="7e8bb-433">此外，運算子本身並不會執行隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="7e8bb-434">這表示查詢喜歡： 選取 * FROM ROOT r WHERE r.Age = 21 只會傳回屬性 Age 等於 toohello 數字 21 的文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="7e8bb-435">不符合屬性 Age 等於 toohello 字串"21"或 hello 字串"0021"的文件，與 hello 運算式"21"= 21 會評估 tooundefined。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="7e8bb-436">這樣可以利用索引，因為 hello 查閱特定值 （也就是數字 21） 的速度比搜尋不限數目的可能相符項目 （也就是數字 21 或字串"21"、"021"、"21.0"...）。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="7e8bb-437">這點不同於 JavaScript 評估不同類型運算子值的方式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="7e8bb-438">**陣列和物件的相等和比較**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="7e8bb-439">使用範圍運算子 (>, >=, <, <=) 比較陣列或物件值會產生未定義的結果，因為物件或陣列值未定義順序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="7e8bb-440">不過，支援使用等號/不等運算子 (=, !=, <>) 且會以結構化的方式進行比較。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="7e8bb-441">若兩個陣列具有相同數目的元素，且位於相符位置的元素也相等，則陣列也會相等。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="7e8bb-442">如果比較任何元素配對會導致未定義，hello 比較結果的陣列是未定義。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="7e8bb-443">若兩個物件均定義了相同的屬性，而且相符的屬性也相等，則物件會相等。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="7e8bb-444">如果比較任何屬性值的配對會導致未定義，hello 比較結果的物件未定義。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="7e8bb-445"><a name="bk_constants"></a> 常數</span><span class="sxs-lookup"><span data-stu-id="7e8bb-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="7e8bb-446">常數也稱為常值或純量值，是代表特定資料值的符號。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="7e8bb-447">hello 常數的格式取決於其所代表的 hello 數值 hello 資料型別。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="7e8bb-448">**支援的純量資料類型：**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="7e8bb-449">**類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-449">**Type**</span></span>|<span data-ttu-id="7e8bb-450">**值順序**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="7e8bb-451">**未定義**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-451">**Undefined**</span></span>|<span data-ttu-id="7e8bb-452">單一值： **未定義**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="7e8bb-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-453">**Null**</span></span>|<span data-ttu-id="7e8bb-454">單一值：**Null**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-454">Single value: **null**</span></span>|  
|<span data-ttu-id="7e8bb-455">**布林值**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-455">**Boolean**</span></span>|<span data-ttu-id="7e8bb-456">值：**False**，**True**。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="7e8bb-457">**Number**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-457">**Number**</span></span>|<span data-ttu-id="7e8bb-458">雙精確度浮點數，符合 IEEE 754 標準。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="7e8bb-459">**String**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-459">**String**</span></span>|<span data-ttu-id="7e8bb-460">零或更多 Unicode 字元的序列。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="7e8bb-461">字串必須以單引號或雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="7e8bb-462">**Array**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-462">**Array**</span></span>|<span data-ttu-id="7e8bb-463">零或更多元素的序列。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="7e8bb-464">除了未定義的類型，每個元素都可以是任何純量資料類型的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="7e8bb-465">**Object**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-465">**Object**</span></span>|<span data-ttu-id="7e8bb-466">未排序的零或更多名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="7e8bb-467">名稱為 Unicode 字串；除了**未定義**的類型，值可以是任何純量資料類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="7e8bb-468">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-469">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="7e8bb-470">代表未定義類型的未定義值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="7e8bb-471">代表 **Null** 類型的 **Null** 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="7e8bb-472">代表布林值類型的常數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="7e8bb-473">代表布林值類型的 **False** 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="7e8bb-474">代表布林值類型的 **True** 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="7e8bb-475">代表常數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="7e8bb-476">十進位常值是使用十進位表示法或科學記號標記法表示的數字。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="7e8bb-477">十六進位常值是使用前置詞 '0x' 後面接著一或多個十六進位數字表示的數字。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="7e8bb-478">代表字串類型的常數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="7e8bb-479">字串常值是由零個或多個 Unicode 字元序列或逸出序列所表示的 Unicode 字串。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="7e8bb-480">字串常值會以單引號 (所有格符號：') 或雙引號 (引號：") 括起來。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="7e8bb-481">允許下列逸出序列：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="7e8bb-482">**逸出序列**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-482">**Escape sequence**</span></span>|<span data-ttu-id="7e8bb-483">**說明**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-483">**Description**</span></span>|<span data-ttu-id="7e8bb-484">**Unicode 字元**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="7e8bb-485">\\'</span><span class="sxs-lookup"><span data-stu-id="7e8bb-485">\\'</span></span>|<span data-ttu-id="7e8bb-486">apostrophe (')</span><span class="sxs-lookup"><span data-stu-id="7e8bb-486">apostrophe (')</span></span>|<span data-ttu-id="7e8bb-487">U+0027</span><span class="sxs-lookup"><span data-stu-id="7e8bb-487">U+0027</span></span>|  
|<span data-ttu-id="7e8bb-488">\\"</span><span class="sxs-lookup"><span data-stu-id="7e8bb-488">\\"</span></span>|<span data-ttu-id="7e8bb-489">引號 (")</span><span class="sxs-lookup"><span data-stu-id="7e8bb-489">quotation mark (")</span></span>|<span data-ttu-id="7e8bb-490">U+0022</span><span class="sxs-lookup"><span data-stu-id="7e8bb-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="7e8bb-491">反向斜線 (\\)</span><span class="sxs-lookup"><span data-stu-id="7e8bb-491">reverse solidus (\\)</span></span>|<span data-ttu-id="7e8bb-492">U+005C</span><span class="sxs-lookup"><span data-stu-id="7e8bb-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="7e8bb-493">斜線 (/)</span><span class="sxs-lookup"><span data-stu-id="7e8bb-493">solidus (/)</span></span>|<span data-ttu-id="7e8bb-494">U+002F</span><span class="sxs-lookup"><span data-stu-id="7e8bb-494">U+002F</span></span>|  
|<span data-ttu-id="7e8bb-495">\b</span><span class="sxs-lookup"><span data-stu-id="7e8bb-495">\b</span></span>|<span data-ttu-id="7e8bb-496">退格鍵</span><span class="sxs-lookup"><span data-stu-id="7e8bb-496">backspace</span></span>|<span data-ttu-id="7e8bb-497">U+0008</span><span class="sxs-lookup"><span data-stu-id="7e8bb-497">U+0008</span></span>|  
|<span data-ttu-id="7e8bb-498">\f</span><span class="sxs-lookup"><span data-stu-id="7e8bb-498">\f</span></span>|<span data-ttu-id="7e8bb-499">換頁字元</span><span class="sxs-lookup"><span data-stu-id="7e8bb-499">form feed</span></span>|<span data-ttu-id="7e8bb-500">U+000C</span><span class="sxs-lookup"><span data-stu-id="7e8bb-500">U+000C</span></span>|  
|\n|<span data-ttu-id="7e8bb-501">換行字元</span><span class="sxs-lookup"><span data-stu-id="7e8bb-501">line feed</span></span>|<span data-ttu-id="7e8bb-502">U+000A</span><span class="sxs-lookup"><span data-stu-id="7e8bb-502">U+000A</span></span>|  
|<span data-ttu-id="7e8bb-503">\r</span><span class="sxs-lookup"><span data-stu-id="7e8bb-503">\r</span></span>|<span data-ttu-id="7e8bb-504">歸位字元</span><span class="sxs-lookup"><span data-stu-id="7e8bb-504">carriage return</span></span>|<span data-ttu-id="7e8bb-505">U+000D</span><span class="sxs-lookup"><span data-stu-id="7e8bb-505">U+000D</span></span>|  
|<span data-ttu-id="7e8bb-506">\t</span><span class="sxs-lookup"><span data-stu-id="7e8bb-506">\t</span></span>|<span data-ttu-id="7e8bb-507">Tab 鍵</span><span class="sxs-lookup"><span data-stu-id="7e8bb-507">tab</span></span>|<span data-ttu-id="7e8bb-508">U+0009</span><span class="sxs-lookup"><span data-stu-id="7e8bb-508">U+0009</span></span>|  
|<span data-ttu-id="7e8bb-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="7e8bb-509">\uXXXX</span></span>|<span data-ttu-id="7e8bb-510">由 4 個十六進位數字所定義的 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="7e8bb-511">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="7e8bb-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="7e8bb-512"><a name="bk_query_perf_guidelines"></a> 查詢效能指導方針</span><span class="sxs-lookup"><span data-stu-id="7e8bb-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="7e8bb-513">為了讓大型集合有效執行查詢 toobe，它應該使用可提供透過一或多個索引的篩選器。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="7e8bb-514">hello 下列篩選會被視為索引查詢：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="7e8bb-515">使用等號比較運算子 ( = ) 搭配文件路徑運算式和常數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="7e8bb-516">使用範圍比較運算子 (<, \<=, >, >=) 搭配文件路徑運算式和數字常數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="7e8bb-517">文件路徑運算式代表識別 hello 參考資料庫集合中的 hello 文件中常數路徑的任何運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="7e8bb-518">**文件路徑運算式**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="7e8bb-519">文件路徑運算式是一種運算式，會採取來自資料庫集合文件之文件上的屬性或陣列索引子的路徑。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="7e8bb-520">這個路徑可以是使用的 tooidentify hello 位置，直接在 hello 資料庫集合中的 hello 文件內的篩選中所參考的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="7e8bb-521">對於文件路徑運算式會被視為運算式 toobe，它應該：</span><span class="sxs-lookup"><span data-stu-id="7e8bb-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="7e8bb-522">參考 hello 集合根直接。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="7e8bb-523">參考某些文件路徑運算式的屬性或常數陣列索引子</span><span class="sxs-lookup"><span data-stu-id="7e8bb-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="7e8bb-524">參考代表某文件路徑運算式的別名。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="7e8bb-525">**語法慣例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="7e8bb-526">hello 下表描述 hello DocumentDB API 查詢語言參考中的 hello 所使用的慣例 toodescribe 語法。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="7e8bb-527">**慣例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-527">**Convention**</span></span>|<span data-ttu-id="7e8bb-528">**用於**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="7e8bb-529">大寫</span><span class="sxs-lookup"><span data-stu-id="7e8bb-529">UPPERCASE</span></span>|<span data-ttu-id="7e8bb-530">關鍵字不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="7e8bb-531">小寫</span><span class="sxs-lookup"><span data-stu-id="7e8bb-531">lowercase</span></span>|<span data-ttu-id="7e8bb-532">關鍵字區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="7e8bb-533">\<nonterminal></span><span class="sxs-lookup"><span data-stu-id="7e8bb-533">\<nonterminal></span></span>|<span data-ttu-id="7e8bb-534">非終端項，分別定義。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="7e8bb-535">\<nonterminal> ::=</span><span class="sxs-lookup"><span data-stu-id="7e8bb-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="7e8bb-536">Hello 非終端項的語法定義。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="7e8bb-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="7e8bb-537">other_terminal</span></span>|<span data-ttu-id="7e8bb-538">終端項 (權杖)，以文字詳細說明。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="7e8bb-539">識別碼</span><span class="sxs-lookup"><span data-stu-id="7e8bb-539">identifier</span></span>|<span data-ttu-id="7e8bb-540">識別碼。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-540">Identifier.</span></span> <span data-ttu-id="7e8bb-541">僅允許下列字元：a-z A-Z 0-9 _第一個字元不能為數字。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="7e8bb-542">"字串"</span><span class="sxs-lookup"><span data-stu-id="7e8bb-542">"string"</span></span>|<span data-ttu-id="7e8bb-543">括號中的字串。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-543">Quoted string.</span></span> <span data-ttu-id="7e8bb-544">允許任何有效字串。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-544">Allows any valid string.</span></span> <span data-ttu-id="7e8bb-545">請參閱 string_literal 的描述。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="7e8bb-546">'符號'</span><span class="sxs-lookup"><span data-stu-id="7e8bb-546">'symbol'</span></span>|<span data-ttu-id="7e8bb-547">這是 hello 語法的一部分的常值符號。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="7e8bb-548">&#124; (分隔號)</span><span class="sxs-lookup"><span data-stu-id="7e8bb-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="7e8bb-549">語法項目的替代項目。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-549">Alternatives for syntax items.</span></span> <span data-ttu-id="7e8bb-550">您可以使用其中一個指定的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="7e8bb-551">[ ] /(方括號)</span><span class="sxs-lookup"><span data-stu-id="7e8bb-551">[ ] /(brackets)</span></span>|<span data-ttu-id="7e8bb-552">方括號會括住一或多個選用項目。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="7e8bb-553">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="7e8bb-553">[ ,...n ]</span></span>|<span data-ttu-id="7e8bb-554">指出 hello 上述項目可以重複的 n 次。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="7e8bb-555">hello 相符項目會以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="7e8bb-556">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="7e8bb-556">[ ...n ]</span></span>|<span data-ttu-id="7e8bb-557">指出 hello 上述項目可以重複的 n 次。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="7e8bb-558">以空白分開 hello 相符項目。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="7e8bb-559"><a name="bk_built_in_functions"></a>內建函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="7e8bb-560">Azure Cosmos DB 提供許多內建 SQL 函式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="7e8bb-561">內建函式的 hello 類別如下所示。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="7e8bb-562">函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-562">Function</span></span>|<span data-ttu-id="7e8bb-563">說明</span><span class="sxs-lookup"><span data-stu-id="7e8bb-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="7e8bb-564">數學函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="7e8bb-565">hello 數學函數會執行計算，通常取決於輸入的值會作為引數，且傳回數字的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="7e8bb-566">類型檢查函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="7e8bb-567">hello 類型檢查函數可讓您 toocheck hello SQL 查詢中運算式型別。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="7e8bb-568">字串函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="7e8bb-569">hello 字串函數的字串輸入值來執行作業，並且傳回字串、 數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="7e8bb-570">陣列函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="7e8bb-571">hello 陣列函數會執行作業陣列輸入的值，並且傳回數值、 布林值或陣列值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="7e8bb-572">空間函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="7e8bb-573">hello 空間函式上的空間物件的輸入值執行作業，並傳回數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="7e8bb-574"><a name="bk_mathematical_functions"></a>數學函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="7e8bb-575">hello 下列各個函式執行計算，通常取決於輸入的值會作為引數，且傳回數字的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="7e8bb-576">ABS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="7e8bb-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="7e8bb-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="7e8bb-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="7e8bb-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="7e8bb-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="7e8bb-581">CEILING</span><span class="sxs-lookup"><span data-stu-id="7e8bb-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="7e8bb-582">COS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="7e8bb-583">COT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="7e8bb-584">DEGREES</span><span class="sxs-lookup"><span data-stu-id="7e8bb-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="7e8bb-585">EXP</span><span class="sxs-lookup"><span data-stu-id="7e8bb-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="7e8bb-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="7e8bb-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="7e8bb-587">LOG</span><span class="sxs-lookup"><span data-stu-id="7e8bb-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="7e8bb-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="7e8bb-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="7e8bb-589">PI</span><span class="sxs-lookup"><span data-stu-id="7e8bb-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="7e8bb-590">POWER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="7e8bb-591">RADIANS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="7e8bb-592">ROUND</span><span class="sxs-lookup"><span data-stu-id="7e8bb-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="7e8bb-593">SIN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="7e8bb-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="7e8bb-595">SQUARE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="7e8bb-596">SIGN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="7e8bb-597">TAN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="7e8bb-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="7e8bb-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="7e8bb-599"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="7e8bb-600">傳回 hello 絕對 （正） 值 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-601">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-602">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-603">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-604">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-604">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-605">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-606">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-606">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-607">hello 下列範例顯示三個不同的數字上使用 hello ABS 函數的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="7e8bb-608">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="7e8bb-609"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="7e8bb-610">傳回 hello 的角度，以弧度為單位，它的餘弦為 hello 指定數值運算式。也稱為反餘弦值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="7e8bb-611">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-612">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-613">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-614">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-614">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-615">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-616">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-616">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-617">hello 下列範例會傳回-1 的 ACOS hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="7e8bb-618">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="7e8bb-619"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="7e8bb-620">傳回 hello 的角度，以弧度為單位，其正弦值為 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="7e8bb-621">這也稱為反正弦值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="7e8bb-622">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-623">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-624">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-625">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-625">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-626">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-627">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-627">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-628">hello 下列範例會傳回-1 的 ASIN hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="7e8bb-629">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="7e8bb-630"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="7e8bb-631">傳回 hello 的角度，以弧度為單位，其正切為 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="7e8bb-632">這也稱為反正切值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="7e8bb-633">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-634">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-635">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-636">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-636">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-637">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-638">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-638">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-639">下列範例傳回 hello 的 hello ATAN hello 指定的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="7e8bb-640">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="7e8bb-641"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="7e8bb-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="7e8bb-642">傳回 hello hello 反正切值 y / x，以弧度表示主體值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="7e8bb-643">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-644">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-645">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-646">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-646">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-647">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-648">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-648">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-649">hello 下列範例會計算指定的 hello ATN2 x 和 y 元件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="7e8bb-650">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="7e8bb-651"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="7e8bb-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="7e8bb-652">傳回 hello 最小整數值大於或等於，hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-653">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-654">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-655">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-656">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-656">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-657">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-658">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-658">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-659">hello 下列範例顯示正數、 負數和零值與 hello CEILING 函數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="7e8bb-660">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="7e8bb-661"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="7e8bb-662">傳回 hello 三角餘弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="7e8bb-663">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-664">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-665">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-666">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-666">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-667">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-668">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-668">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-669">下列範例中的 hello 計算 hello hello 的指定角度的 COS。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="7e8bb-670">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="7e8bb-671"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="7e8bb-672">傳回 hello 三角餘切函數 hello 指定旋轉的角度，以弧度為單位，在 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-673">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-674">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-675">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-676">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-676">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-677">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-678">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-678">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-679">下列範例中的 hello 計算 hello hello 指定角度的 COT。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="7e8bb-680">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="7e8bb-681"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="7e8bb-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="7e8bb-682">傳回 hello 以度為單位的角度以弧度為單位指定的對應角度。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="7e8bb-683">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-684">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-685">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-686">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-686">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-687">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-688">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-688">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-689">hello 下列範例會傳回 hello 掠的度數 PI/2 弧度的角度。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="7e8bb-690">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="7e8bb-691"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="7e8bb-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="7e8bb-692">傳回小於 hello 最大整數 toohello 或等於指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-693">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-694">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-695">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-696">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-696">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-697">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-698">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-698">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-699">hello 下列範例顯示正數、 負數和零值與 hello FLOOR 函式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="7e8bb-700">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="7e8bb-701"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="7e8bb-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="7e8bb-702">傳回的 hello hello 指數值指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-703">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-704">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-705">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-706">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-706">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-707">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-708">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-708">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-709">hello 常數**e** (2.718281...) 是 hello 自然對數的基底。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="7e8bb-710">hello 數字的指數是 hello 常數**e**引發 toohello hello 數字乘冪。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="7e8bb-711">例如 EXP(1.0) = e^1.0 = 2.71828182845905 和 EXP(10) = e^10 = 22026.4657948067。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="7e8bb-712">hello hello 數字的自然對數的指數是 hello 數本身： EXP (LOG (n)) = n。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="7e8bb-713">而 hello hello 指數的自然對數是 hello 數值本身： LOG (EXP (n)) = n。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="7e8bb-714">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-714">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-715">hello 下列範例會宣告一個變數並傳回 hello hello 指定變數 (10) 的指數的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="7e8bb-716">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="7e8bb-717">hello 下列範例會傳回 hello hello 自然對數 20 和 hello hello 自然對數的指數值 20 的指數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="7e8bb-718">因為這些函式是反向函數彼此 hello 傳回值捨入為浮點數學之兩種情況下為 20。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="7e8bb-719">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="7e8bb-720"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="7e8bb-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="7e8bb-721">傳回 hello 自然對數的 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-722">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="7e8bb-723">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-724">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="7e8bb-725">選擇性數值引數，以設定 hello hello 對數基底。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="7e8bb-726">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-726">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-727">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-728">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-728">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-729">根據預設，log （） 會傳回 hello 自然對數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="7e8bb-730">您可以使用 hello 選擇性底數參數，以變更 hello 基底的 hello 對數 tooanother 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="7e8bb-731">hello 自然對數是 hello 基底的對數 toohello **e**，其中**e**是無理常數大約等於 too2.718281828。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="7e8bb-732">hello hello 指數的自然對數是 hello 數本身： LOG (EXP (n)) = n。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="7e8bb-733">而 hello hello 數字的自然對數的指數是 hello 數值本身： EXP (LOG (n)) = n。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="7e8bb-734">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-734">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-735">hello 下列範例會宣告一個變數並傳回 hello 對數值 hello 指定變數 (10)。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="7e8bb-736">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="7e8bb-737">hello 下列範例會計算數字的 hello 指數 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="7e8bb-738">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="7e8bb-739"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="7e8bb-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="7e8bb-740">傳回 hello 基底 10 對數 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-741">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-742">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-743">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-744">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-744">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-745">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-746">**備註**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-746">**Remarks**</span></span>  
  
 <span data-ttu-id="7e8bb-747">hello LOG10 和 POWER 函數是反比相關的 tooone 另一個。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="7e8bb-748">例如，10 ^ LOG10(n) = n。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="7e8bb-749">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-749">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-750">hello 下列範例會宣告一個變數並傳回 hello 的 hello 指定的變數 (100) 的 LOG10 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="7e8bb-751">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="7e8bb-752"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="7e8bb-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="7e8bb-753">傳回 hello PI 的常數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="7e8bb-754">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="7e8bb-755">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-756">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-757">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-757">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-758">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-759">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-759">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-760">hello 下列範例會傳回 PI 的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="7e8bb-761">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="7e8bb-762"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="7e8bb-763">傳回 hello hello 指定的值運算式 toohello 指定的冪。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="7e8bb-764">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="7e8bb-765">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-766">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="7e8bb-767">是 hello 電源 toowhich tooraise `numeric_expression`。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="7e8bb-768">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-768">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-769">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-770">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-770">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-771">hello 下列範例示範如何引發數字 toohello 3 的乘冪 (數字 hello hello cube)。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="7e8bb-772">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="7e8bb-773"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="7e8bb-774">當您輸入數值運算式 (以度為單位) 時，傳回弧度。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="7e8bb-775">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-776">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-777">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-778">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-778">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-779">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-780">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-780">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-781">hello 下列範例使用幾個角度做為輸入並傳回其對應的弧度值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="7e8bb-782">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="7e8bb-783"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="7e8bb-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="7e8bb-784">傳回數值，捨入的 toohello 最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="7e8bb-785">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-786">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-787">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-788">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-788">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-789">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-790">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-790">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-791">hello 下列範例會將下列正數和負數 toohello 接近的整數的 hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="7e8bb-792">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="7e8bb-793"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="7e8bb-794">傳回 hello 正 (+ 1)、 零 (0)，或 hello 負 (-1) 號指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-795">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-796">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-797">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-798">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-798">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-799">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-800">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-800">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-801">hello 下列範例會傳回 hello 的數字的 SIGN 值從-2 too2。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="7e8bb-802">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="7e8bb-803"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="7e8bb-804">傳回 hello 三角正弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="7e8bb-805">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-806">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-807">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-808">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-808">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-809">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-810">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-810">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-811">下列範例中的 hello 計算 hello 指定角度的 SIN hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="7e8bb-812">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="7e8bb-813"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="7e8bb-814">傳回 hello 平方根 hello 指定數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="7e8bb-815">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-816">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-817">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-818">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-818">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-819">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-820">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-820">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-821">hello 下列範例會傳回 hello 平方根的數字 1-3。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="7e8bb-822">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="7e8bb-823"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="7e8bb-824">傳回 hello 正方形 hello 的指定數字值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="7e8bb-825">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-826">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-827">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-828">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-828">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-829">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-830">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-830">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-831">hello 下列範例會傳回數字 1-3 的 hello 平方。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="7e8bb-832">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="7e8bb-833"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="7e8bb-834">Hello 傳回 hello 正切函數指定的角度，以弧度為單位，hello 中指定的運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="7e8bb-835">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-836">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-837">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-838">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-838">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-839">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-840">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-840">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-841">hello 下列範例計算 hello 正切 PI （） / 2。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="7e8bb-842">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="7e8bb-843"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="7e8bb-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="7e8bb-844">傳回數值，截斷的 toohello 最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="7e8bb-845">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="7e8bb-846">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="7e8bb-847">為數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-848">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-848">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-849">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-850">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-850">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-851">下列範例中的 hello 截斷 hello 下列正數和負數 toohello 最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="7e8bb-852">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="7e8bb-853"><a name="bk_type_checking_functions"></a>類型檢查函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="7e8bb-854">hello 下列函數支援類型檢查輸入的值，而且每個傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="7e8bb-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="7e8bb-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="7e8bb-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="7e8bb-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="7e8bb-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="7e8bb-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="7e8bb-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="7e8bb-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="7e8bb-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="7e8bb-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="7e8bb-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="7e8bb-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="7e8bb-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="7e8bb-863"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="7e8bb-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="7e8bb-864">傳回布林值，指出是否指定運算式的 hello hello 類型是陣列。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="7e8bb-865">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-866">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-867">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-868">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-868">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-869">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-870">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-870">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-871">hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_ARRAY 函式的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-872">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="7e8bb-873"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="7e8bb-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="7e8bb-874">傳回布林值，指出是否 hello hello 類型指定的運算式是布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="7e8bb-875">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-876">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-877">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-878">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-878">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-879">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-880">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-880">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-881">hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_BOOL 函數的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-882">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="7e8bb-883"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="7e8bb-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="7e8bb-884">傳回布林值，指出如果 hello 尚未指派屬性值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="7e8bb-885">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-886">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-887">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-888">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-888">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-889">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-890">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-890">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-891">下列範例會檢查 hello hello 內的屬性存在的 hello 指定 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="7e8bb-892">hello 第一次，則為 true，因此傳回"a"，但 hello 第二個則為 false，因此會傳回"b"不存在。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="7e8bb-893">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="7e8bb-894"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="7e8bb-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="7e8bb-895">傳回布林值，指出是否 hello hello 類型指定的運算式為 null。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="7e8bb-896">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-897">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-898">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-899">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-899">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-900">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-901">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-901">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-902">hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_NULL 函數的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-903">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="7e8bb-904"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="7e8bb-905">傳回布林值，指出是否 hello hello 類型指定的運算式是一個數字。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="7e8bb-906">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-907">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-908">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-909">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-909">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-910">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-911">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-911">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-912">hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_NULL 函數的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-913">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="7e8bb-914"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="7e8bb-915">傳回布林值，指出是否 hello hello 類型指定的運算式是一個 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="7e8bb-916">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-917">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-918">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-919">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-919">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-920">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-921">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-921">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-922">hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_OBJECT 函式的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-923">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="7e8bb-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="7e8bb-925">傳回布林值，指出是否 hello hello 類型指定運算式是基本型別 （字串、 布林值、 數值或 null）。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="7e8bb-926">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-927">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-928">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-929">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-929">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-930">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-931">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-931">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-932">hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_PRIMITIVE 函數的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-933">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="7e8bb-934"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="7e8bb-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="7e8bb-935">傳回布林值，指出是否 hello hello 類型指定的運算式是字串。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="7e8bb-936">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="7e8bb-937">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="7e8bb-938">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-939">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-939">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-940">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-941">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-941">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-942">hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_STRING 函數的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="7e8bb-943">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="7e8bb-944"><a name="bk_string_functions"></a> 字串函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="7e8bb-945">hello 下列純量函數的字串輸入值來執行作業並傳回字串、 數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="7e8bb-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="7e8bb-947">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="7e8bb-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="7e8bb-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="7e8bb-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="7e8bb-950">LEFT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="7e8bb-951">LENGTH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="7e8bb-952">LOWER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="7e8bb-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="7e8bb-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="7e8bb-954">REPLACE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="7e8bb-955">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="7e8bb-956">REVERSE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="7e8bb-957">RIGHT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="7e8bb-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="7e8bb-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="7e8bb-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="7e8bb-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="7e8bb-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="7e8bb-961">UPPER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="7e8bb-962"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="7e8bb-963">傳回字串 hello 因產生的串連兩個或多個字串值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="7e8bb-964">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="7e8bb-965">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-966">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-967">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-967">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-968">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-969">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-969">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-970">下列範例傳回 hello 串連字串 hello hello 指定值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="7e8bb-971">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="7e8bb-972"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="7e8bb-973">傳回布林值，指出是否 hello 第一個字串運算式中第二個包含 hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="7e8bb-974">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-975">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-976">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-977">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-977">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-978">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-979">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-979">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-980">hello 下列範例會檢查是否"abc"包含"ab"，且包含"d"。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="7e8bb-981">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="7e8bb-982"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="7e8bb-983">傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="7e8bb-984">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-985">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-986">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-987">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-987">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-988">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-989">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-989">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-990">hello 下列範例會傳回"abc"的結尾是"b"和"bc"hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="7e8bb-991">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="7e8bb-992"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="7e8bb-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="7e8bb-993">傳回開始 hello 內 hello 第一個指定的字串運算式，則為-1 hello 第二個字串運算式的第一次出現的位置，如果找不到 hello 字串 hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="7e8bb-994">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-995">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-996">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-997">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-997">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-998">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-999">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-999">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1000">hello 下列範例會傳回"abc"內各種子字串 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="7e8bb-1001">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="7e8bb-1002"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="7e8bb-1003">傳回 hello 字串的左側的組件以 hello 指定字元數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="7e8bb-1004">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1005">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1006">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="7e8bb-1007">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1008">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1009">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1010">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1010">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1011">hello 下列範例會傳回 hello 左"abc"各種長度值的一部分。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="7e8bb-1012">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="7e8bb-1013"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="7e8bb-1014">傳回 hello 數目的 hello 字元指定的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1015">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1016">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1017">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1018">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1019">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1020">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1020">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1021">hello 下列範例會傳回字串 hello 長度。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="7e8bb-1022">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="7e8bb-1023"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="7e8bb-1024">傳回將大寫字元資料 toolowercase 轉換後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="7e8bb-1025">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1026">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1027">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1028">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1029">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1030">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1030">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1031">下列範例會示範如何 hello toouse 較低的查詢中。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="7e8bb-1032">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="7e8bb-1033"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="7e8bb-1034">傳回移除開頭空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="7e8bb-1035">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1036">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1037">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1038">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1039">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1040">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1040">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1041">下列範例會示範如何 hello toouse LTRIM 查詢內。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="7e8bb-1042">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="7e8bb-1043"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="7e8bb-1044">使用其他字串值取代指定的字串值的所有項目。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="7e8bb-1045">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1046">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1047">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1048">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1049">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1050">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1050">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1051">hello 下列範例顯示如何 toouse 取代查詢中。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="7e8bb-1052">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="7e8bb-1053"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="7e8bb-1054">將字串值重複指定的次數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="7e8bb-1055">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1056">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1057">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="7e8bb-1058">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1059">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1060">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1061">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1061">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1062">hello 下列範例顯示如何 toouse 複寫在查詢中。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="7e8bb-1063">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="7e8bb-1064"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="7e8bb-1065">傳回字串值的 hello 反向順序。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="7e8bb-1066">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1067">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1068">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1069">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1070">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1071">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1071">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1072">hello 下列範例顯示如何 toouse 反向查詢中。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="7e8bb-1073">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="7e8bb-1074"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="7e8bb-1075">傳回 hello 權限屬於字串 hello 與指定字元的數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="7e8bb-1076">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1077">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1078">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="7e8bb-1079">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1080">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1081">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1082">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1082">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1083">hello 下列範例會傳回 hello 的右側部分"abc"各種長度值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="7e8bb-1084">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="7e8bb-1085"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="7e8bb-1086">傳回移除結尾空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="7e8bb-1087">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1088">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1089">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1090">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1091">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1092">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1092">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1093">下列範例會示範如何 hello toouse RTRIM 查詢內。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="7e8bb-1094">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="7e8bb-1095"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="7e8bb-1096">傳回布林值，指出 hello 第一個字串運算式的開頭是否 hello 第二個。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="7e8bb-1097">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1098">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1099">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1100">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1101">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1102">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1102">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1103">hello 下列範例會檢查有 hello 字串"abc"開頭為"b"和"a"。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="7e8bb-1104">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="7e8bb-1105"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="7e8bb-1106">Hello 處開始的字串運算式的傳回屬於指定的字元以零為起始的位置，並繼續 toohello 指定長度或 toohello hello 字串的結尾。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="7e8bb-1107">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="7e8bb-1108">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1109">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="7e8bb-1110">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1111">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1112">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1113">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1113">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1114">hello 下列範例會傳回"abc"hello 子字串開始在 1 和 1 個字元的長度。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="7e8bb-1115">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="7e8bb-1116"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="7e8bb-1117">傳回將小寫字元資料 toouppercase 轉換後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="7e8bb-1118">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1119">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="7e8bb-1120">為任何有效的字運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1121">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1122">傳回字串運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1123">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1123">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1124">下列範例會示範如何 hello toouse 上限，在查詢中</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="7e8bb-1125">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="7e8bb-1126"><a name="bk_array_functions"></a> 陣列函陣列函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="7e8bb-1127">下列純量函數的 hello 執行陣列輸入的值和傳回數值、 布林值或陣列值的作業</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="7e8bb-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="7e8bb-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="7e8bb-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="7e8bb-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="7e8bb-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="7e8bb-1133">傳回陣列，其中是 hello 結果串連兩個以上陣列值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="7e8bb-1134">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="7e8bb-1135">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="7e8bb-1136">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1137">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1138">傳回陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1139">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1139">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1140">下列範例如何 tooconcatenate 兩個陣列 hello。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="7e8bb-1141">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="7e8bb-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="7e8bb-1143">傳回布林值，指出 hello 陣列中是否包含 hello 指定的值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="7e8bb-1144">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="7e8bb-1145">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="7e8bb-1146">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="7e8bb-1147">為任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1148">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1149">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="7e8bb-1150">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1150">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1151">下列範例如何 hello toocheck 使用 ARRAY_CONTAINS 陣列中的成員資格。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="7e8bb-1152">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="7e8bb-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="7e8bb-1154">傳回 hello 項目數的 hello 指定陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1155">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1156">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="7e8bb-1157">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1158">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1159">傳回數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1160">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1160">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1161">下列範例 hello tooget 如何 hello 使用 ARRAY_LENGTH 陣列的長度。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="7e8bb-1162">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="7e8bb-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="7e8bb-1164">傳回陣列運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="7e8bb-1165">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="7e8bb-1166">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="7e8bb-1167">為任何有效陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="7e8bb-1168">為任何有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1169">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1170">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="7e8bb-1171">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1171">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1172">下列範例如何 hello tooget 使用 ARRAY_SLICE 陣列的一部分。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="7e8bb-1173">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="7e8bb-1174"><a name="bk_spatial_functions"></a> 空間函式</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="7e8bb-1175">hello 下列純量函數的空間物件的輸入值上執行作業並傳回數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="7e8bb-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="7e8bb-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="7e8bb-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="7e8bb-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="7e8bb-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="7e8bb-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="7e8bb-1182">傳回兩個 hello GeoJSON 點、 多邊形或 LineString 運算式之間的 hello 距離。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="7e8bb-1183">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1184">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="7e8bb-1185">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1186">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1187">傳回數值運算式，其中包含 hello 距離。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="7e8bb-1188">這表示以公尺為單位 hello 預設參照系統。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="7e8bb-1189">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1189">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1190">下列範例會示範如何 hello tooreturn 所有系列的文件內的 hello 30 金鑰管理，則會指定使用 hello ST_DISTANCE 內建函式的位置。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="7e8bb-1191">.</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="7e8bb-1192">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="7e8bb-1193"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="7e8bb-1194">傳回布林運算式，指出 hello GeoJSON 物件 （點、 多邊形或 LineString） hello 第一個引數中指定處於 hello GeoJSON （點、 多邊形或 LineString） 內 hello 第二個引數。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="7e8bb-1195">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1196">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="7e8bb-1197">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="7e8bb-1198">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1199">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1200">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="7e8bb-1201">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1201">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1202">hello 下列範例顯示如何 toofind 所有系列文都件內使用 ST_WITHIN 多邊形。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="7e8bb-1203">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="7e8bb-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="7e8bb-1205">傳回表示 hello GeoJSON （點、 多邊形或 LineString） 中指定的物件 hello 第一個引數是否相交 hello 第二個引數中的 hello GeoJSON （點、 多邊形或 LineString） 的布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="7e8bb-1206">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1207">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="7e8bb-1208">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="7e8bb-1209">為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1210">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1211">傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="7e8bb-1212">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1212">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1213">下列範例會示範如何 hello toofind 給定的多邊形 hello 與交集的所有區域。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="7e8bb-1214">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="7e8bb-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="7e8bb-1216">傳回布林值，指出 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式是否有效。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="7e8bb-1217">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1218">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="7e8bb-1219">為任何有效的 GeoJSON 點、Polygon 或 LineString 運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1220">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1221">傳回布林運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1222">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1222">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1223">下列範例會示範如何 hello toocheck 是否有效使用 ST_VALID 點。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="7e8bb-1224">比方說，此點的緯度值不在 hello [-90，90] 值的有效範圍內，因此 hello 查詢會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="7e8bb-1225">若是多邊形，hello 規格要求應該是最後一個 hello 提供座標組的 GeoJSON hello 相同 hello 第一次，toocreate 為封閉的圖形。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="7e8bb-1226">多邊形內的點必須以逆時針順序指定。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="7e8bb-1227">順時針旋轉的順序指定的多邊形代表 hello 反 hello 區域內。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="7e8bb-1228">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="7e8bb-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="7e8bb-1230">傳回包含布林值，如果 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式的 JSON 值有效，而且如果無效，此外 hello 原因，表示為字串值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="7e8bb-1231">**語法**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="7e8bb-1232">**引數**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="7e8bb-1233">為任何有效的 GeoJSON 點或多邊形運算式。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="7e8bb-1234">**傳回類型**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="7e8bb-1235">傳回包含布林值，如果 hello 指定 GeoJSON 點或多邊形運算式有效，而且如果無效，此外 hello 原因，表示為字串值的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="7e8bb-1236">**範例**</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1236">**Examples**</span></span>  
  
 <span data-ttu-id="7e8bb-1237">下列範例如何 hello toocheck 使用 ST_ISVALIDDETAILED （與詳細資料） 有效。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="7e8bb-1238">以下是 hello 結果集。</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="7e8bb-1239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1239">Next steps</span></span>  
 <span data-ttu-id="7e8bb-1240">[適用於Azure Cosmos DB 的 SQL 語法和 SQL 查詢](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="7e8bb-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="7e8bb-1241">Azure Cosmos DB 文件</span><span class="sxs-lookup"><span data-stu-id="7e8bb-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
