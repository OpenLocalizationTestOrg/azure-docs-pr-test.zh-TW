---
標題： aaa"Azure Cosmos DB DocumentDB API: SQL 語法 |Microsoft 文件"描述： 參考文件以 hello Azure Cosmos DB DocumentDB API SQL 查詢語言。
服務： cosmos db 作者： mimig1 管理員： jhubbard 編輯器： mimig documentationcenter: '

ms.assetid: ms.service: cosmos db ms.workload： 資料服務 ms.tgt_pltfrm: na ms.devlang: na ms.topic： 參考 ms.date: 06/13/2017 ms.author: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>Azure Cosmos DB DocumentDB API：SQL 語法參考

hello Azure Cosmos DB DocumentDB API 像文法，透過階層式 JSON 而不需要明確的結構描述或建立次要索引，支援使用熟悉的 SQL （結構化查詢語言） 查詢文件。 本主題提供 hello DocumentDB API SQL 查詢語言參考文件。

逐步解說中的 hello DocumentDB API SQL 查詢語言，請參閱[SQL 查詢 Azure Cosmos DB DocumentDB api](documentdb-sql-query.md)。  
  
我們也邀請您 toovisit hello[查詢遊樂場](http://www.documentdb.com/sql/demo)您可以在此 Azure Cosmos DB 再試一次，並對我們的資料集執行 SQL 查詢。  
  
## <a name="select-query"></a>SELECT 查詢  
從 hello 資料庫擷取 JSON 文件。 支援運算式評估、規劃、篩選和聯結。  hello 慣例用來描述 hello SELECT 陳述式會在 hello 語法慣例 > 一節中製成資料表。  
  
**語法**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **備註**  
  
 如需每個子句的詳細資料，請參閱下列各節：  
  
-   [SELECT 子句](#bk_select_query)  
  
-   [FROM 子句](#bk_from_clause)  
  
-   [WHERE 子句](#bk_where_clause)  
  
-   [ORDER BY 子句](#bk_orderby_clause)  
  
hello SELECT 陳述式中的 hello 子句的順序必須如上所示。 可以省略任何一個 hello 選擇性子句。 但是，當使用選擇性的子句時，它們必須顯示 hello 正確的順序。  
  
**Hello SELECT 陳述式的邏輯處理順序**  
  
子句的處理 hello 順序為：  

1.  [FROM 子句](#bk_from_clause)  
2.  [WHERE 子句](#bk_where_clause)  
3.  [ORDER BY 子句](#bk_orderby_clause)  
4.  [SELECT 子句](#bk_select_query)  

請注意，這不同於在 hello hello 語法中出現的順序。 hello 排序，這類處理的子句所導入的所有新符號是可見和可在稍後處理的子句。 例如，您可以在 WHERE 和 SELECT 子句中存取 FROM 子句中宣告的別名。  

**空白字元和註解**  

所有空白字元不屬於引號的字串或引號識別項不 hello 語言文法的一部分，而且會在剖析期間忽略。  

hello 查詢語言支援 T-SQL 樣式的註解類似  

-   陳述式`-- comment text [newline]`  

雖然空白字元和註解沒有任何重要性 hello 文法中，它們必須使用的 tooseparate 語彙基元。 例如：`-1e5` 是單一數字的權杖，而 `: – 1 e5` 則是加上減號的權杖，後面接著數字 1 和識別碼 e5。  

##  <a name="bk_select_query"></a> SELECT 子句  
hello SELECT 陳述式中的 hello 子句的順序必須如上所示。 可以省略任何一個 hello 選擇性子句。 但是，當使用選擇性的子句時，它們必須顯示 hello 正確的順序。  

**語法**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **引數**  
  
 `<select_specification>`  
  
 設定屬性或值 toobe 選取 hello 結果。  
  
 `'*'`  
  
指定應該擷取 hello 值，而不進行任何變更。 特別是如果處理 hello 值是物件，將會擷取所有屬性。  
  
 `<object_property_list>`  
  
指定擷取的屬性 toobe hello 清單。 每個傳回的值將是具有 hello 屬性指定的物件。  
  
`VALUE`  
  
指定應該擷取 hello JSON 值，而不是 hello 完整的 JSON 物件。 這不同的是`<property_list>`不會換行投射的 hello 值物件中。  
  
`<scalar_expression>`  
  
代表 hello 值 toobe 運算式計算。 請參閱[純量運算式](#bk_scalar_expressions)一節以取得詳細資料。  
  
**備註**  
  
hello`SELECT *`語法才會有效 FROM 子句已宣告一個別名。 `SELECT *` 提供一個身分識別投影，在無需投影的情況下會非常實用。 SELECT * 只有在已指定 FROM 子句且只導入單一輸入來源時才有效。  
  
請注意，`SELECT <select_list>` 和 `SELECT *` 為「語法捷徑」，可以使用如下所示的簡單 SELECT 陳述式另外表示。  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     相當於：  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     相當於：  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**另請參閱**  
  
[純量運算式](#bk_scalar_expressions)  
[SELECT 子句](#bk_select_query)  
  
##  <a name="bk_from_clause"></a>FROM 子句  
指定 hello 來源或聯結的來源。 hello FROM 子句是選擇性的。 若未指定，系統仍然會在如同 FROM 子句提供了單一文件的情況下執行其他子句。  
  
**語法**  
  
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
  
**引數**  
  
`<from_source>`  
  
指定包含或不包含別名的資料來源。 如果未指定別名，它會從推斷 hello`<collection_expression>`使用下列規則：  
  
-   如果 hello 運算式是 collection_name，collection_name 將使用做為別名。  
  
-   如果 hello 運算式`<collection_expression>`，則 property_name 會作為別名。 如果 hello 運算式是 collection_name，collection_name 將使用做為別名。  
  
AS `input_alias`  
  
指定該 hello`input_alias`是一組 hello 基礎集合運算式所傳回的值。  
 
`input_alias` IN  
  
指定該 hello`input_alias`應該代表 hello 組來逐一查看每個陣列 hello 基礎集合運算式所傳回的所有陣列項目取得的值。 會忽略任何由基礎集合運算式傳回的任何非陣列的值。  
  
`<collection_expression>`  
  
指定 hello 集合運算式 toobe 使用 tooretrieve hello 文件。  
  
`ROOT`  
  
指定應該從 hello 預設，目前連接的集合中擷取該文件。  
  
`collection_name`  
  
指定應該從提供的 hello 集合中擷取該文件。 hello hello 集合名稱必須符合目前已連線到 hello 集合 hello 名稱。  
  
`input_alias`  
  
指定應該從 hello 擷取該文件以 hello 提供別名定義其他來源。  
  
`<collection_expression> '.' property_`  
  
指定應該擷取該文件，藉由存取 hello`property_name`屬性或 array_index 陣列元素的所有文件，來擷取指定之集合運算式。  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
指定應該擷取該文件，藉由存取 hello`property_name`屬性或 array_index 陣列元素的所有文件，來擷取指定之集合運算式。  
  
**備註**  
  
所有的別名中提供或推斷 hello `<from_source>(`s) 必須是唯一的。 hello 語法`<collection_expression>.`property_name 是 hello 與相同`<collection_expression>' ['"property_name"']'`。 不過，如果屬性名稱包含非識別碼字元，可以使用 hello 後者的語法。  
  
**遺漏的屬性、遺漏的陣列元素、未定義的值處理**  
  
若集合運算式存取屬性或陣列元素，且該值不存在，則會忽略該值且不會進一步處理。  
  
**集合運算式內容範圍**  
  
集合運算方式可以是集合範圍或文件範圍：  
  
-   運算式是集合範圍，如果 hello hello 集合運算式的基礎來源為 ROOT 或`collection_name`。 這類運算式代表一組直接從 hello 集合中擷取的文件，並不會相依於其他集合運算式的 hello 處理。  
  
-   運算式是文件範圍，如果 hello hello 集合運算式的基礎來源是`input_alias`早導入 hello 查詢。 這類運算式表示一組藉由評估 hello 範圍中的每個屬於 toohello 組與 hello 別名集合相關聯的文件的 hello 集合運算式取得的文件。  hello 結果集將會取得藉由評估 hello 集合運算式，針對每個 hello 基礎集合中的 hello 文件集的聯集。  
  
**聯結**  
  
在 hello 目前版本中，Azure Cosmos DB 支援內部聯結。 即將推出其他聯結功能。

在完整的交叉乘積的 hello 的內部聯結結果設定參與 hello 聯結。 hello N 方聯結結果是一組 N 元素 tuple，其中 hello tuple 中的每個值都與 hello 別名 hello 聯結中設定 參與關聯，而可以參考其他子句中的該別名來存取。  
  
hello 聯結的 hello 評估 hello 參與集 hello 內容範圍而定：  
  
-  集合組 A 和集合範圍組 B 之間的聯結會產生集合 A 和 B 中所有元素的交叉乘積。
  
-   集合組 A 和文件範圍組 B 之間的聯結會產生所有集合的聯集，是依評估集合 A 的每個文件的文件範圍集合 B 來取得。  
  
 在 hello 目前版本中，一個集合範圍運算式最多可支援由 hello 查詢處理器。  
  
**聯結範例：**  
  
讓我們看看下列 FROM 子句的 hello:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 讓每個來源定義 `input_alias1, input_alias2, …, input_aliasN`。 這個 FROM 子句會傳回一組 N-Tuple (具有 N 個值的 Tuple)。 每個 Tuple 所擁有的值，都是將所有集合別名在其個別集合上反覆運算所產生。  
  
*JOIN 範例 1，搭配 2 個來源：*  
  
- 讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。  
  
- 讓 `<from_source2>` 為參照 input_alias1 的文件範圍，並代表以下集：  
  
    {1, 2} 為 `input_alias1 = A,`  
  
    {3} 為 `input_alias1 = B,`  
  
    {4, 5} 為 `input_alias1 = C,`  
  
- FROM 子句 hello`<from_source1> JOIN <from_source2>`會導致下列 tuple 的 hello:  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*JOIN 範例 2，搭配 3 個來源：*  
  
- 讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。  
  
- 讓 `<from_source2>` 為參照 `input_alias1` 的文件範圍，並代表以下集：  
  
    {1, 2} 為 `input_alias1 = A,`  
  
    {3} 為 `input_alias1 = B,`  
  
    {4, 5} 為 `input_alias1 = C,`  
  
- 讓 `<from_source3>` 為參照 `input_alias2` 的文件範圍，並代表以下集：  
  
    {100, 200} 為 `input_alias2 = 1,`  
  
    {300}為 `input_alias2 = 3,`  
  
- FROM 子句 hello`<from_source1> JOIN <from_source2> JOIN <from_source3>`會導致下列 tuple 的 hello:  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> 缺乏的其他值的 tuple `input_alias1`， `input_alias2`，哪些 hello`<from_source3>`未傳回任何值。  
  
*JOIN 範例 3，搭配 3 個來源：*  
  
- 讓 <from_source1> 為集合範圍並代表集 {A, B, C}。  
  
- 讓 `<from_source1>` 為集合範圍並代表集 {A, B, C}。  
  
- 讓 <from_source2> 為參照 input_alias1 的文件範圍，並代表以下集：  
  
    {1, 2} 為 `input_alias1 = A,`  
  
    {3} 為 `input_alias1 = B,`  
  
    {4, 5} 為 `input_alias1 = C,`  
  
- 可讓`<from_source3>`太範圍`input_alias1`，而且代表集：  
  
    {100, 200} 為 `input_alias2 = A,`  
  
    {300}為 `input_alias2 = C,`  
  
- FROM 子句 hello`<from_source1> JOIN <from_source2> JOIN <from_source3>`會導致下列 tuple 的 hello:  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)  
  
> [!NOTE]
> 這會導致之間的交叉乘積`<from_source2>`和`<from_source3>`因為兩者都已設定領域的 toohello 相同`<from_source1>`。  這會讓 4 (2x2) Tuple 具備值 A，0 Tuple 具備值 B (1x0) 而 2 (2x1) Tuple 具備值 C。  
  
**另請參閱**  
  
 [SELECT 子句](#bk_select_query)  
  
##  <a name="bk_where_clause"></a>WHERE 子句  
 指定 hello hello hello 查詢所傳回的文件的搜尋條件。  
  
 **語法**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **引數**  
  
-   `<filter_condition>`  
  
     指定符合的傳回 hello 文件 toobe hello 條件 toobe。  
  
-   `<scalar_expression>`  
  
     代表 hello 值 toobe 運算式計算。 請參閱 hello[純量運算式](#bk_scalar_expressions)如需詳細資訊。  
  
 **備註**  
  
 為了讓 hello 文件 toobe 會傳回指定為篩選條件必須評估 tootrue 的運算式。 只有布林值 true 會滿足 hello 條件，任何其他值： 未定義、 null、 false、 數字、 陣列或物件並不符合 hello 條件。  
  
##  <a name="bk_orderby_clause"></a>ORDER BY 子句  
 指定排序次序 hello 查詢所傳回結果的 hello。  
  
 **語法**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **引數**  
  
-   `<sort_specification>`  
  
     指定屬性或在其設定 toosort hello 查詢結果的運算式。 排序資料行可指定為名稱或資料行別名。  
  
     可以指定多個排序資料行。 資料行必須是唯一的。 hello hello ORDER BY 子句中的 hello 排序資料行的順序定義 hello 組織 hello 排序結果集。 也就是說，hello 結果集依照 hello 第一個屬性，然後該排序的清單依照 hello 第二個屬性，依此類推。  
  
     hello hello ORDER BY 子句中參考的資料行名稱必須對應的 tooeither hello 中的資料行選取清單或 tooa 中沒有任何模稜兩可的 hello FROM 子句中指定的資料表定義的資料行。  
  
-   `<sort_expression>`  
  
     指定哪些 toosort hello 查詢結果集上的單一屬性或運算式。  
  
-   `<scalar_expression>`  
  
     請參閱 hello[純量運算式](#bk_scalar_expressions)如需詳細資訊。  
  
-   `ASC | DESC`  
  
     指定的 hello 指定資料行中的 hello 值應該以遞增或遞減順序排序。 ASC 從最低值 toohighest 值 hello 進行排序。 DESC 從最高值 toolowest 值進行排序。 ASC 是 hello 預設排序順序。 Null 值會視為 hello 最低的可能值。  
  
 **備註**  
  
 即使 hello 查詢文法支援多個順序屬性，但是 hello Azure Cosmos DB 查詢執行階段會支援排序只針對單一屬性，並只對屬性名稱，亦即，不是針對計算的屬性。 排序也需要編製索引原則該 hello 包含 hello 屬性與 hello 指定範圍的索引類型，含 hello 最大有效位數。 Toohello 編製索引原則文件，如需詳細資訊，請參閱。  
  
##  <a name="bk_scalar_expressions"></a>純量運算式  
 純量運算式是符號的組合，而且可運算子評估 tooobtain 單一值。 簡單運算式可以是常數、屬性參考、陣列元素參考、別名參考或函式呼叫。 簡單運算式可以透過使用運算子，與複雜運算式結合。  
  
 如需純量運算式具備哪些值的詳細資料，請參閱[常數](#bk_constants)一節。  
  
 **語法**  
  
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
  
 **引數**  
  
-   `<constant>`  
  
     代表常數值。 如需詳細資料，請參閱[常數](#bk_constants)一節。  
  
-   `input_alias`  
  
     代表 hello 所定義的值`input_alias`hello 中導入`FROM`子句。  
    這個值保證 toonot 是**未定義**–**未定義**hello 輸入中的值會略過。  
  
-   `<scalar_expression>.property_name`  
  
     代表物件的 hello 屬性值。 如果 hello 屬性不存在，或參考屬性的值不是物件，則 hello 運算式的評估太**未定義**值。  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     代表 hello 屬性名稱與值`property_name`或具有索引的陣列元素`array_index`的物件/陣列。 如果 hello 屬性/陣列索引不存在或 hello 屬性/陣列索引參考的值不是物件/陣列，接著 hello 運算式會評估 tooundefined 值。  
  
-   `unary_operator <scalar_expression>`  
  
     表示的運算子所套用的 tooa 的單一值。 如需詳細資料，請參閱[運算子](#bk_operators)一節。  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     表示已套用的 tootwo 值的運算子。 如需詳細資料，請參閱[運算子](#bk_operators)一節。  
  
-   `<scalar_function_expression>`  
  
     代表由函式呼叫結果定義的值。  
  
-   `udf_scalar_function`  
  
     定義純量函數 hello 使用者名稱。  
  
-   `builtin_scalar_function`  
  
     Hello 內建的純量函數的名稱。  
  
-   `<create_object_expression>`  
  
     代表搭配指定屬性及其值所建立之新物件取得的值。  
  
-   `<create_array_expression>`  
  
     代表搭配指定值作為元素所建立之新物件取得的值  
  
-   `parameter_name`  
  
     代表 hello 指定的參數名稱的值。 參數名稱必須帶有單一 @ 作為 hello 第一個字元。  
  
 **備註**  
  
 呼叫內建或使用者定義純量值函式時，必須定義所有引數。 如果未定義任何 hello 引數，將不會呼叫 hello 函式和 hello 結果會是未定義。  
  
 建立物件時，將略過不包含在建立物件的 hello 獲派值未定義任何屬性。  
  
 當建立陣列的任何項目值可指派**未定義**將略過不包含在 hello 建立物件的值。 這會導致 hello 接著定義項目 tootake 其所在位置的方式建立 hello 陣列將沒有略過索引。  
  
##  <a name="bk_operators"></a> 運算子  
 本章節描述支援的 hello 運算子。 每個運算子可以是指派的 tooexactly 一個類別目錄。  
  
 請參閱以下的**運算子類別**表格，如需處理**未定義**值的詳細資料，請輸入輸入值的需求，以及透過不相符的值處理值的需求。  
  
 **運算子類別：**  
  
|**類別**|**詳細資料**|  
|-|-|  
|**arithmetic**|運算子預期輸入 toobe 號碼。 輸出也是數字。 如果任一 hello 輸入**未定義**或數字則 hello 結果以外的型別為**未定義**。|  
|**bitwise**|運算子預期輸入 toobe 32 位元帶正負號的正負號的整數。 輸出也為 32 位元的帶正負號整數。<br /><br /> 任何非整數值均會進行四捨五入。 正值會無條件捨去，負值則會進位。<br /><br /> 取得最後 32 位元的它的補數標記法，將轉換 hello 32 位元整數範圍以外的任何值。<br /><br /> 如果任一 hello 輸入**未定義**或 hello 結果是，請輸入數字，以外**未定義**。<br /><br /> **注意：** hello 上述行為會與 JavaScript 位元運算子行為相容。|  
|**logical**|運算子預期輸入 toobe 布林值。 輸出也是布林值。<br />如果任一 hello 輸入**未定義**hello 結果將會輸入而不是布林值，或**未定義**。|  
|**comparison**|運算子預期輸入 toohave hello 相同類型，而且不是 未定義。 輸出也是布林值。<br /><br /> 如果任一 hello 輸入**未定義**hello 輸入或是不同的類型，則 hello 結果是**未定義**。<br /><br /> 請參閱**比較值順序**表格以取得值順序的詳細資料。|  
|**字串**|運算子預期輸入 toobe 字串。 輸出也是字串。<br />如果任一 hello 輸入**未定義**或字串，然後 hello 結果以外的型別為**未定義**。|  
  
 **一元運算子**  
  
|**名稱**|**運算子**|**詳細資料**|  
|-|-|-|  
|**arithmetic**|+<br /><br /> -|傳回 hello 數字值。<br /><br /> 位元否定。 傳回否定的數值。|  
|**bitwise**|~|1 的補數。 傳回數值的補數。|  
|**Logical**|**NOT**|否定。 傳回否定布林值。|  
  
 **二元運算子：**  
  
|**名稱**|**運算子**|**詳細資料**|  
|-|-|-|  
|**arithmetic**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|加法。<br /><br /> 減法。<br /><br /> 乘法。<br /><br /> 除法。<br /><br /> 調節。|  
|**bitwise**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|位元 OR。<br /><br /> 位元 AND。<br /><br /> 位元 XOR。<br /><br /> 向左移位。<br /><br /> 向右移位。<br /><br /> 向右移位並填滿零。|  
|**logical**|**AND**<br /><br /> **或**|邏輯結合。 若兩個引數都為 **True**，則傳回 **True**，否則會傳回 **False**。<br /><br /> 邏輯結合。 若兩個引數都為 **True**，則傳回 **True**，否則會傳回 **False**。|  
|**comparison**|**=**<br /><br /> **!=, <>**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|等於。 若引數相等，則傳回 **True**，否則會傳回 **False**。<br /><br /> 不等於。 若引數不相等，則傳回 **True**，否則會傳回 **False**。<br /><br /> 大於。 傳回**true**如果第一個引數為大於 hello 第二個項目，傳回**false**否則。<br /><br /> 大於或等於。 傳回**true**如果第一個引數大於或等於第二個 toohello，傳回**false**否則。<br /><br /> 小於。 傳回**true**如果第一個引數小於 hello 第二個，傳回**false**否則。<br /><br /> 小於或等於。 傳回**true**如果第一個引數小於或等於 toohello 第二個其中一個，傳回**false**否則。<br /><br /> 聯合。 傳回 hello 第二個引數，如果第一個引數 hello**未定義**值。|  
|**String**|**&#124;&#124;**|串連。 傳回兩個引數的串連。|  
  
 **三元運算子：**   
  
|三元運算子|?|傳回 hello 第二個引數，如果 hello 第一個引數的評估太**true**; 否則傳回 hello 第三個引數。|  
|-|-|-|  
  
 **比較值順序**  
  
|**類型**|**值順序**|  
|-|-|  
|**未定義**|無法比較。|  
|**Null**|單一值：**Null**|  
|**Number**|自然實數。<br /><br /> 負的無限值小於其他任何數值。<br /><br /> 正無限值大於其他任何數值。**NaN** 值無法比較。 與 **NaN** 比較會產生**未定義的**值。|  
|**String**|詞彙編篡順序。|  
|**Array**|沒有順序，但合理。|  
|**Object**|沒有順序，但合理。|  
  
 **備註**  
  
 在 Azure Cosmos DB，hello 類型的值通常之前，無法得知它們實際從 hello 資料庫中擷取。 順序 toosupport 能夠有效率地執行查詢，在大部分的 hello 運算子會有嚴格的型別需求。 此外，運算子本身並不會執行隱含轉換。  
  
 這表示查詢喜歡： 選取 * FROM ROOT r WHERE r.Age = 21 只會傳回屬性 Age 等於 toohello 數字 21 的文件。 不符合屬性 Age 等於 toohello 字串"21"或 hello 字串"0021"的文件，與 hello 運算式"21"= 21 會評估 tooundefined。 這樣可以利用索引，因為 hello 查閱特定值 （也就是數字 21） 的速度比搜尋不限數目的可能相符項目 （也就是數字 21 或字串"21"、"021"、"21.0"...）。 這點不同於 JavaScript 評估不同類型運算子值的方式。  
  
 **陣列和物件的相等和比較**  
  
 使用範圍運算子 (>, >=, <, <=) 比較陣列或物件值會產生未定義的結果，因為物件或陣列值未定義順序。 不過，支援使用等號/不等運算子 (=, !=, <>) 且會以結構化的方式進行比較。  
  
 若兩個陣列具有相同數目的元素，且位於相符位置的元素也相等，則陣列也會相等。 如果比較任何元素配對會導致未定義，hello 比較結果的陣列是未定義。  
  
 若兩個物件均定義了相同的屬性，而且相符的屬性也相等，則物件會相等。 如果比較任何屬性值的配對會導致未定義，hello 比較結果的物件未定義。  
  
##  <a name="bk_constants"></a> 常數  
 常數也稱為常值或純量值，是代表特定資料值的符號。 hello 常數的格式取決於其所代表的 hello 數值 hello 資料型別。  
  
 **支援的純量資料類型：**  
  
|**類型**|**值順序**|  
|-|-|  
|**未定義**|單一值： **未定義**|  
|**Null**|單一值：**Null**|  
|**布林值**|值：**False**，**True**。|  
|**Number**|雙精確度浮點數，符合 IEEE 754 標準。|  
|**String**|零或更多 Unicode 字元的序列。 字串必須以單引號或雙引號括住。|  
|**Array**|零或更多元素的序列。 除了未定義的類型，每個元素都可以是任何純量資料類型的值。|  
|**Object**|未排序的零或更多名稱/值組。 名稱為 Unicode 字串；除了**未定義**的類型，值可以是任何純量資料類型。|  
  
 **語法**  
  
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
  
 **引數**  
  
1.  `<undefined_constant>; undefined`  
  
     代表未定義類型的未定義值。  
  
2.  `<null_constant>; null`  
  
     代表 **Null** 類型的 **Null** 值。  
  
3.  `<boolean_constant>`  
  
     代表布林值類型的常數。  
  
4.  `false`  
  
     代表布林值類型的 **False** 值。  
  
5.  `true`  
  
     代表布林值類型的 **True** 值。  
  
6.  `<number_constant>`  
  
     代表常數值。  
  
7.  `decimal_literal`  
  
     十進位常值是使用十進位表示法或科學記號標記法表示的數字。  
  
8.  `hexadecimal_literal`  
  
     十六進位常值是使用前置詞 '0x' 後面接著一或多個十六進位數字表示的數字。  
  
9. `<string_constant>`  
  
     代表字串類型的常數。  
  
10. `string _literal`  
  
     字串常值是由零個或多個 Unicode 字元序列或逸出序列所表示的 Unicode 字串。 字串常值會以單引號 (所有格符號：') 或雙引號 (引號：") 括起來。  
  
 允許下列逸出序列：  
  
|**逸出序列**|**說明**|**Unicode 字元**|  
|-|-|-|  
|\\'|apostrophe (')|U+0027|  
|\\"|引號 (")|U+0022|  
|\\\|反向斜線 (\\)|U+005C|  
|\\/|斜線 (/)|U+002F|  
|\b|退格鍵|U+0008|  
|\f|換頁字元|U+000C|  
|\n|換行字元|U+000A|  
|\r|歸位字元|U+000D|  
|\t|Tab 鍵|U+0009|  
|\uXXXX|由 4 個十六進位數字所定義的 Unicode 字元。|U+XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a> 查詢效能指導方針  
 為了讓大型集合有效執行查詢 toobe，它應該使用可提供透過一或多個索引的篩選器。  
  
 hello 下列篩選會被視為索引查詢：  
  
-   使用等號比較運算子 ( = ) 搭配文件路徑運算式和常數。  
  
-   使用範圍比較運算子 (<, \<=, >, >=) 搭配文件路徑運算式和數字常數。  
  
-   文件路徑運算式代表識別 hello 參考資料庫集合中的 hello 文件中常數路徑的任何運算式。  
  
 **文件路徑運算式**  
  
 文件路徑運算式是一種運算式，會採取來自資料庫集合文件之文件上的屬性或陣列索引子的路徑。 這個路徑可以是使用的 tooidentify hello 位置，直接在 hello 資料庫集合中的 hello 文件內的篩選中所參考的值。  
  
 對於文件路徑運算式會被視為運算式 toobe，它應該：  
  
1.  參考 hello 集合根直接。  
  
2.  參考某些文件路徑運算式的屬性或常數陣列索引子  
  
3.  參考代表某文件路徑運算式的別名。  
  
     **語法慣例**  
  
     hello 下表描述 hello DocumentDB API 查詢語言參考中的 hello 所使用的慣例 toodescribe 語法。  
  
    |**慣例**|**用於**|  
    |-|-|    
    |大寫|關鍵字不區分大小寫。|  
    |小寫|關鍵字區分大小寫。|  
    |\<nonterminal>|非終端項，分別定義。|  
    |\<nonterminal> ::=|Hello 非終端項的語法定義。|  
    |other_terminal|終端項 (權杖)，以文字詳細說明。|  
    |識別碼|識別碼。 僅允許下列字元：a-z A-Z 0-9 _第一個字元不能為數字。|  
    |"字串"|括號中的字串。 允許任何有效字串。 請參閱 string_literal 的描述。|  
    |'符號'|這是 hello 語法的一部分的常值符號。|  
    |&#124; (分隔號)|語法項目的替代項目。 您可以使用其中一個指定的 hello 項目。|  
    |[ ] /(方括號)|方括號會括住一或多個選用項目。|  
    |[ ,...n ]|指出 hello 上述項目可以重複的 n 次。 hello 相符項目會以逗號分隔。|  
    |[ ...n ]|指出 hello 上述項目可以重複的 n 次。 以空白分開 hello 相符項目。|  
  
##  <a name="bk_built_in_functions"></a>內建函式  
 Azure Cosmos DB 提供許多內建 SQL 函式。 內建函式的 hello 類別如下所示。  
  
|函式|說明|  
|--------------|-----------------|  
|[數學函式](#bk_mathematical_functions)|hello 數學函數會執行計算，通常取決於輸入的值會作為引數，且傳回數字的值。|  
|[類型檢查函式](#bk_type_checking_functions)|hello 類型檢查函數可讓您 toocheck hello SQL 查詢中運算式型別。|  
|[字串函式](#bk_string_functions)|hello 字串函數的字串輸入值來執行作業，並且傳回字串、 數值或布林值。|  
|[陣列函式](#bk_array_functions)|hello 陣列函數會執行作業陣列輸入的值，並且傳回數值、 布林值或陣列值。|  
|[空間函式](#bk_spatial_functions)|hello 空間函式上的空間物件的輸入值執行作業，並傳回數值或布林值。|  
  
###  <a name="bk_mathematical_functions"></a>數學函式  
 hello 下列各個函式執行計算，通常取決於輸入的值會作為引數，且傳回數字的值。  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[CEILING](#bk_ceiling)|  
|[COS](#bk_cos)|[COT](#bk_cot)|[DEGREES](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[LOG](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[POWER](#bk_power)|  
|[RADIANS](#bk_radians)|[ROUND](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[SQUARE](#bk_square)|[SIGN](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC](#bk_trunc)||  
  
####  <a name="bk_abs"></a> ABS  
 傳回 hello 絕對 （正） 值 hello 指定數值運算式。  
  
 **語法**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例顯示三個不同的數字上使用 hello ABS 函數的 hello 結果。  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a> ACOS  
 傳回 hello 的角度，以弧度為單位，它的餘弦為 hello 指定數值運算式。也稱為反餘弦值。  
  
 **語法**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回-1 的 ACOS hello。  
  
```  
SELECT ACOS(-1)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a> ASIN  
 傳回 hello 的角度，以弧度為單位，其正弦值為 hello 指定數值運算式。 這也稱為反正弦值。  
  
 **語法**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回-1 的 ASIN hello。  
  
```  
SELECT ASIN(-1)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a> ATAN  
 傳回 hello 的角度，以弧度為單位，其正切為 hello 指定數值運算式。 這也稱為反正切值。  
  
 **語法**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 下列範例傳回 hello 的 hello ATAN hello 指定的值。  
  
```  
SELECT ATAN(-45.01)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a> ATN2  
 傳回 hello hello 反正切值 y / x，以弧度表示主體值。  
  
 **語法**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會計算指定的 hello ATN2 x 和 y 元件。  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a> CEILING  
 傳回 hello 最小整數值大於或等於，hello 指定數值運算式。  
  
 **語法**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例顯示正數、 負數和零值與 hello CEILING 函數。  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a> COS  
 傳回 hello 三角餘弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。  
  
 **語法**  
  
```  
COS(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 下列範例中的 hello 計算 hello hello 的指定角度的 COS。  
  
```  
SELECT COS(14.78)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a> COT  
 傳回 hello 三角餘切函數 hello 指定旋轉的角度，以弧度為單位，在 hello 指定數值運算式。  
  
 **語法**  
  
```  
COT(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 下列範例中的 hello 計算 hello hello 指定角度的 COT。  
  
```  
SELECT COT(124.1332)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a> DEGREES  
 傳回 hello 以度為單位的角度以弧度為單位指定的對應角度。  
  
 **語法**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回 hello 掠的度數 PI/2 弧度的角度。  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a> FLOOR  
 傳回小於 hello 最大整數 toohello 或等於指定數值運算式。  
  
 **語法**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例顯示正數、 負數和零值與 hello FLOOR 函式。  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a> EXP  
 傳回的 hello hello 指數值指定數值運算式。  
  
 **語法**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **備註**  
  
 hello 常數**e** (2.718281...) 是 hello 自然對數的基底。  
  
 hello 數字的指數是 hello 常數**e**引發 toohello hello 數字乘冪。 例如 EXP(1.0) = e^1.0 = 2.71828182845905 和 EXP(10) = e^10 = 22026.4657948067。  
  
 hello hello 數字的自然對數的指數是 hello 數本身： EXP (LOG (n)) = n。 而 hello hello 指數的自然對數是 hello 數值本身： LOG (EXP (n)) = n。  
  
 **範例**  
  
 hello 下列範例會宣告一個變數並傳回 hello hello 指定變數 (10) 的指數的值。  
  
```  
SELECT EXP(10)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 hello 下列範例會傳回 hello hello 自然對數 20 和 hello hello 自然對數的指數值 20 的指數。 因為這些函式是反向函數彼此 hello 傳回值捨入為浮點數學之兩種情況下為 20。  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a> LOG  
 傳回 hello 自然對數的 hello 指定數值運算式。  
  
 **語法**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
-   `base`  
  
     選擇性數值引數，以設定 hello hello 對數基底。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **備註**  
  
 根據預設，log （） 會傳回 hello 自然對數。 您可以使用 hello 選擇性底數參數，以變更 hello 基底的 hello 對數 tooanother 值。  
  
 hello 自然對數是 hello 基底的對數 toohello **e**，其中**e**是無理常數大約等於 too2.718281828。  
  
 hello hello 指數的自然對數是 hello 數本身： LOG (EXP (n)) = n。 而 hello hello 數字的自然對數的指數是 hello 數值本身： EXP (LOG (n)) = n。  
  
 **範例**  
  
 hello 下列範例會宣告一個變數並傳回 hello 對數值 hello 指定變數 (10)。  
  
```  
SELECT LOG(10)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 hello 下列範例會計算數字的 hello 指數 hello 記錄檔。  
  
```  
SELECT EXP(LOG(10))  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a> LOG10  
 傳回 hello 基底 10 對數 hello 指定數值運算式。  
  
 **語法**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **備註**  
  
 hello LOG10 和 POWER 函數是反比相關的 tooone 另一個。 例如，10 ^ LOG10(n) = n。  
  
 **範例**  
  
 hello 下列範例會宣告一個變數並傳回 hello 的 hello 指定的變數 (100) 的 LOG10 值。  
  
```  
SELECT LOG10(100)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a> PI  
 傳回 hello PI 的常數值。  
  
 **語法**  
  
```  
PI ()  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回 PI 的 hello 值。  
  
```  
SELECT PI()  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a> POWER  
 傳回 hello hello 指定的值運算式 toohello 指定的冪。  
  
 **語法**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
-   `y`  
  
     是 hello 電源 toowhich tooraise `numeric_expression`。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例示範如何引發數字 toohello 3 的乘冪 (數字 hello hello cube)。  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a> RADIANS  
 當您輸入數值運算式 (以度為單位) 時，傳回弧度。  
  
 **語法**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例使用幾個角度做為輸入並傳回其對應的弧度值。  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 以下是 hello 結果集。  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a> ROUND  
 傳回數值，捨入的 toohello 最接近的整數值。  
  
 **語法**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會將下列正數和負數 toohello 接近的整數的 hello。  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a> SIGN  
 傳回 hello 正 (+ 1)、 零 (0)，或 hello 負 (-1) 號指定數值運算式。  
  
 **語法**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回 hello 的數字的 SIGN 值從-2 too2。  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a> SIN  
 傳回 hello 三角正弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。  
  
 **語法**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 下列範例中的 hello 計算 hello 指定角度的 SIN hello。  
  
```  
SELECT SIN(45.175643)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a> SQRT  
 傳回 hello 平方根 hello 指定數值。  
  
 **語法**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回 hello 平方根的數字 1-3。  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a> SQUARE  
 傳回 hello 正方形 hello 的指定數字值。  
  
 **語法**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回數字 1-3 的 hello 平方。  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a> TAN  
 Hello 傳回 hello 正切函數指定的角度，以弧度為單位，hello 中指定的運算式。  
  
 **語法**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例計算 hello 正切 PI （） / 2。  
  
```  
SELECT TAN(PI()/2);  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a> TRUNC  
 傳回數值，截斷的 toohello 最接近的整數值。  
  
 **語法**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **引數**  
  
-   `numeric_expression`  
  
     為數值運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 下列範例中的 hello 截斷 hello 下列正數和負數 toohello 最接近的整數值。  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 以下是 hello 結果集。  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a>類型檢查函式  
 hello 下列函數支援類型檢查輸入的值，而且每個傳回布林值。  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a> IS_ARRAY  
 傳回布林值，指出是否指定運算式的 hello hello 類型是陣列。  
  
 **語法**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_ARRAY 函式的類型。  
  
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
  
 以下是 hello 結果集。  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a> IS_BOOL  
 傳回布林值，指出是否 hello hello 類型指定的運算式是布林值。  
  
 **語法**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_BOOL 函數的類型。  
  
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
  
 以下是 hello 結果集。  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a> IS_DEFINED  
 傳回布林值，指出如果 hello 尚未指派屬性值。  
  
 **語法**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 下列範例會檢查 hello hello 內的屬性存在的 hello 指定 JSON 文件。 hello 第一次，則為 true，因此傳回"a"，但 hello 第二個則為 false，因此會傳回"b"不存在。  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 以下是 hello 結果集。  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a> IS_NULL  
 傳回布林值，指出是否 hello hello 類型指定的運算式為 null。  
  
 **語法**  
  
```  
IS_NULL(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_NULL 函數的類型。  
  
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
  
 以下是 hello 結果集。  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a> IS_NUMBER  
 傳回布林值，指出是否 hello hello 類型指定的運算式是一個數字。  
  
 **語法**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_NULL 函數的類型。  
  
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
  
 以下是 hello 結果集。  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a> IS_OBJECT  
 傳回布林值，指出是否 hello hello 類型指定的運算式是一個 JSON 物件。  
  
 **語法**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_OBJECT 函式的類型。  
  
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
  
 以下是 hello 結果集。  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a> IS_PRIMITIVE  
 傳回布林值，指出是否 hello hello 類型指定運算式是基本型別 （字串、 布林值、 數值或 null）。  
  
 **語法**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_PRIMITIVE 函數的類型。  
  
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
  
 以下是 hello 結果集。  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a> IS_STRING  
 傳回布林值，指出是否 hello hello 類型指定的運算式是字串。  
  
 **語法**  
  
```  
IS_STRING(<expression>)  
```  
  
 **引數**  
  
-   `expression`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查物件的 JSON 布林、 數字、 字串、 null、 物件、 陣列和未定義使用 hello IS_STRING 函數的類型。  
  
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
  
 以下是 hello 結果集。  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a> 字串函式  
 hello 下列純量函數的字串輸入值來執行作業並傳回字串、 數值或布林值。  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[CONTAINS](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[LEFT](#bk_left)|[LENGTH](#bk_length)|  
|[LOWER](#bk_lower)|[LTRIM](#bk_ltrim)|[REPLACE](#bk_replace)|  
|[REPLICATE](#bk_replicate)|[REVERSE](#bk_reverse)|[RIGHT](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[SUBSTRING](#bk_substring)|  
|[UPPER](#bk_upper)|||  
  
####  <a name="bk_concat"></a> CONCAT  
 傳回字串 hello 因產生的串連兩個或多個字串值。  
  
 **語法**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 下列範例傳回 hello 串連字串 hello hello 指定值。  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a> CONTAINS  
 傳回布林值，指出是否 hello 第一個字串運算式中第二個包含 hello。  
  
 **語法**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查是否"abc"包含"ab"，且包含"d"。  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a> ENDSWITH  
 傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個。  
  
 **語法**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會傳回"abc"的結尾是"b"和"bc"hello。  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a> INDEX_OF  
 傳回開始 hello 內 hello 第一個指定的字串運算式，則為-1 hello 第二個字串運算式的第一次出現的位置，如果找不到 hello 字串 hello。  
  
 **語法**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 hello 下列範例會傳回"abc"內各種子字串 hello 索引。  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a> LEFT  
 傳回 hello 字串的左側的組件以 hello 指定字元數。  
  
 **語法**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
-   `num_expr`  
  
     為任何有效的數值運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 hello 下列範例會傳回 hello 左"abc"各種長度值的一部分。  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a> LENGTH  
 傳回 hello 數目的 hello 字元指定的字串運算式。  
  
 **語法**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 hello 下列範例會傳回字串 hello 長度。  
  
```  
SELECT LENGTH("abc")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a> LOWER  
 傳回將大寫字元資料 toolowercase 轉換後的字串運算式。  
  
 **語法**  
  
```  
LOWER(<str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 下列範例會示範如何 hello toouse 較低的查詢中。  
  
```  
SELECT LOWER("Abc")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a> LTRIM  
 傳回移除開頭空白之後的字串運算式。  
  
 **語法**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 下列範例會示範如何 hello toouse LTRIM 查詢內。  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a> REPLACE  
 使用其他字串值取代指定的字串值的所有項目。  
  
 **語法**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 hello 下列範例顯示如何 toouse 取代查詢中。  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a> REPLICATE  
 將字串值重複指定的次數。  
  
 **語法**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
-   `num_expr`  
  
     為任何有效的數值運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 hello 下列範例顯示如何 toouse 複寫在查詢中。  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a> REVERSE  
 傳回字串值的 hello 反向順序。  
  
 **語法**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 hello 下列範例顯示如何 toouse 反向查詢中。  
  
```  
SELECT REVERSE("Abc")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a> RIGHT  
 傳回 hello 權限屬於字串 hello 與指定字元的數。  
  
 **語法**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
-   `num_expr`  
  
     為任何有效的數值運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 hello 下列範例會傳回 hello 的右側部分"abc"各種長度值。  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a> RTRIM  
 傳回移除結尾空白之後的字串運算式。  
  
 **語法**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 下列範例會示範如何 hello toouse RTRIM 查詢內。  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a> STARTSWITH  
 傳回布林值，指出 hello 第一個字串運算式的開頭是否 hello 第二個。  
  
 **語法**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 hello 下列範例會檢查有 hello 字串"abc"開頭為"b"和"a"。  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a> SUBSTRING  
 Hello 處開始的字串運算式的傳回屬於指定的字元以零為起始的位置，並繼續 toohello 指定長度或 toohello hello 字串的結尾。  
  
 **語法**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
-   `num_expr`  
  
     為任何有效的數值運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 hello 下列範例會傳回"abc"hello 子字串開始在 1 和 1 個字元的長度。  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a> UPPER  
 傳回將小寫字元資料 toouppercase 轉換後的字串運算式。  
  
 **語法**  
  
```  
UPPER(<str_expr>)  
```  
  
 **引數**  
  
-   `str_expr`  
  
     為任何有效的字運算式。  
  
 **傳回類型**  
  
 傳回字串運算式。  
  
 **範例**  
  
 下列範例會示範如何 hello toouse 上限，在查詢中  
  
```  
SELECT UPPER("Abc")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a> 陣列函陣列函式  
 下列純量函數的 hello 執行陣列輸入的值和傳回數值、 布林值或陣列值的作業  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a> ARRAY_CONCAT  
 傳回陣列，其中是 hello 結果串連兩個以上陣列值。  
  
 **語法**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **引數**  
  
-   `arr_expr`  
  
     為任何有效陣列運算式。  
  
 **傳回類型**  
  
 傳回陣列運算式。  
  
 **範例**  
  
 下列範例如何 tooconcatenate 兩個陣列 hello。  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a> ARRAY_CONTAINS  
 傳回布林值，指出 hello 陣列中是否包含 hello 指定的值。  
  
 **語法**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **引數**  
  
-   `arr_expr`  
  
     為任何有效陣列運算式。  
  
-   `expr`  
  
     為任何有效運算式。  
  
 **傳回類型**  
  
 傳回布林值。  
  
 **範例**  
  
 下列範例如何 hello toocheck 使用 ARRAY_CONTAINS 陣列中的成員資格。  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a> ARRAY_LENGTH  
 傳回 hello 項目數的 hello 指定陣列運算式。  
  
 **語法**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **引數**  
  
-   `arr_expr`  
  
     為任何有效陣列運算式。  
  
 **傳回類型**  
  
 傳回數值運算式。  
  
 **範例**  
  
 下列範例 hello tooget 如何 hello 使用 ARRAY_LENGTH 陣列的長度。  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 以下是 hello 結果集。  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a> ARRAY_SLICE  
 傳回陣列運算式的一部分。
  
 **語法**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **引數**  
  
-   `arr_expr`  
  
     為任何有效陣列運算式。  
  
-   `num_expr`  
  
     為任何有效的數值運算式。  
  
 **傳回類型**  
  
 傳回布林值。  
  
 **範例**  
  
 下列範例如何 hello tooget 使用 ARRAY_SLICE 陣列的一部分。  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 以下是 hello 結果集。  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a> 空間函式  
 hello 下列純量函數的空間物件的輸入值上執行作業並傳回數值或布林值。  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a> ST_DISTANCE  
 傳回兩個 hello GeoJSON 點、 多邊形或 LineString 運算式之間的 hello 距離。  
  
 **語法**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **引數**  
  
-   `spatial_expr`  
  
     為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。  
  
 **傳回類型**  
  
 傳回數值運算式，其中包含 hello 距離。 這表示以公尺為單位 hello 預設參照系統。  
  
 **範例**  
  
 下列範例會示範如何 hello tooreturn 所有系列的文件內的 hello 30 金鑰管理，則會指定使用 hello ST_DISTANCE 內建函式的位置。 .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 以下是 hello 結果集。  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a> ST_WITHIN  
 傳回布林運算式，指出 hello GeoJSON 物件 （點、 多邊形或 LineString） hello 第一個引數中指定處於 hello GeoJSON （點、 多邊形或 LineString） 內 hello 第二個引數。  
  
 **語法**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **引數**  
  
-   `spatial_expr`  
  
     為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。  
 
-   `spatial_expr`  
  
     為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。  
  
 **傳回類型**  
  
 傳回布林值。  
  
 **範例**  
  
 hello 下列範例顯示如何 toofind 所有系列文都件內使用 ST_WITHIN 多邊形。  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 以下是 hello 結果集。  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a> ST_INTERSECTS  
 傳回表示 hello GeoJSON （點、 多邊形或 LineString） 中指定的物件 hello 第一個引數是否相交 hello 第二個引數中的 hello GeoJSON （點、 多邊形或 LineString） 的布林運算式。  
  
 **語法**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **引數**  
  
-   `spatial_expr`  
  
     為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。  
 
-   `spatial_expr`  
  
     為任何有效的 GeoJSON 點、Polygon 或 LineString 物件運算式。  
  
 **傳回類型**  
  
 傳回布林值。  
  
 **範例**  
  
 下列範例會示範如何 hello toofind 給定的多邊形 hello 與交集的所有區域。  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 以下是 hello 結果集。  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a> ST_ISVALID  
 傳回布林值，指出 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式是否有效。  
  
 **語法**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **引數**  
  
-   `spatial_expr`  
  
     為任何有效的 GeoJSON 點、Polygon 或 LineString 運算式。  
  
 **傳回類型**  
  
 傳回布林運算式。  
  
 **範例**  
  
 下列範例會示範如何 hello toocheck 是否有效使用 ST_VALID 點。  
  
 比方說，此點的緯度值不在 hello [-90，90] 值的有效範圍內，因此 hello 查詢會傳回 false。  
  
 若是多邊形，hello 規格要求應該是最後一個 hello 提供座標組的 GeoJSON hello 相同 hello 第一次，toocreate 為封閉的圖形。 多邊形內的點必須以逆時針順序指定。 順時針旋轉的順序指定的多邊形代表 hello 反 hello 區域內。  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 以下是 hello 結果集。  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED  
 傳回包含布林值，如果 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式的 JSON 值有效，而且如果無效，此外 hello 原因，表示為字串值。  
  
 **語法**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **引數**  
  
-   `spatial_expr`  
  
     為任何有效的 GeoJSON 點或多邊形運算式。  
  
 **傳回類型**  
  
 傳回包含布林值，如果 hello 指定 GeoJSON 點或多邊形運算式有效，而且如果無效，此外 hello 原因，表示為字串值的 JSON 值。  
  
 **範例**  
  
 下列範例如何 hello toocheck 使用 ST_ISVALIDDETAILED （與詳細資料） 有效。  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 以下是 hello 結果集。  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>後續步驟  
 [適用於Azure Cosmos DB 的 SQL 語法和 SQL 查詢](documentdb-sql-query.md)   
 [Azure Cosmos DB 文件](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
