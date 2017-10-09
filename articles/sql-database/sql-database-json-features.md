---
title: "aaaAzure SQL 資料庫 JSON 功能 |Microsoft 文件"
description: "Azure SQL Database 可讓您 tooparse、 查詢和格式化 JavaScript Object Notation (JSON) 表示法中的資料。"
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="9d277-103">開始使用 Azure SQL Database 中的 JSON 功能</span><span class="sxs-lookup"><span data-stu-id="9d277-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="9d277-104">Azure SQL Database 可讓您剖析及查詢以「JavaScript 物件標記法」 [(JSON)](http://www.json.org/) 格式表示的資料，然後將您的關聯式資料匯出成 JSON 文字。</span><span class="sxs-lookup"><span data-stu-id="9d277-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="9d277-105">JSON 是一種用於在新式的 Web 與行動應用程式中交換資料的常用資料格式。</span><span class="sxs-lookup"><span data-stu-id="9d277-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="9d277-106">JSON 也用於將半結構化的資料儲存在記錄檔或 NoSQL 資料庫 (例如 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/)) 中。</span><span class="sxs-lookup"><span data-stu-id="9d277-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="9d277-107">許多 REST Web 服務都會傳回採用 JSON 文字格式的結果，或是接受採用 JSON 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="9d277-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="9d277-108">大多數 Azure 服務 (例如 [Azure 搜尋服務](https://azure.microsoft.com/services/search/)、[Azure 儲存體](https://azure.microsoft.com/services/storage/)、[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/)) 都有會傳回或取用 JSON 的 REST 端點。</span><span class="sxs-lookup"><span data-stu-id="9d277-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="9d277-109">Azure SQL Database 可讓您輕鬆使用 JSON 資料，並將資料庫與新式服務整合。</span><span class="sxs-lookup"><span data-stu-id="9d277-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="9d277-110">概觀</span><span class="sxs-lookup"><span data-stu-id="9d277-110">Overview</span></span>
<span data-ttu-id="9d277-111">Azure SQL Database 提供 hello 遵循使用 JSON 資料的功能：</span><span class="sxs-lookup"><span data-stu-id="9d277-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![JSON 函數](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="9d277-113">如果您已將 JSON 文字，您可以擷取從 JSON 資料，或確認使用 hello 內建函式已正確格式化 JSON [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx)， [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx)，和[ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d277-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="9d277-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx)函式可讓您更新 JSON 文字內的值。</span><span class="sxs-lookup"><span data-stu-id="9d277-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="9d277-115">針對更進階的查詢和分析， [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) 函數可以將 JSON 物件陣列轉換成一組資料列。</span><span class="sxs-lookup"><span data-stu-id="9d277-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="9d277-116">任何 SQL 查詢可以傳回的結果集的 hello 上執行。</span><span class="sxs-lookup"><span data-stu-id="9d277-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="9d277-117">最後，還有 [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) 子句，此子句可讓您將儲存在關聯式資料表中的資料格式化為 JSON 文字。</span><span class="sxs-lookup"><span data-stu-id="9d277-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="9d277-118">以 JSON 格式將關聯式資料格式化</span><span class="sxs-lookup"><span data-stu-id="9d277-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="9d277-119">如果您有 web 服務，會採用 hello 資料庫資料的圖層，並提供 JSON 中的回應格式，或用戶端的 JavaScript 架構或程式庫可接受資料格式化為 JSON，您可以直接在 SQL 查詢中的資料庫內容格式化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="9d277-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="9d277-120">您不再有格式化為 JSON，Azure SQL 資料庫的結果的 toowrite 應用程式程式碼或包含一些 JSON 序列化程式庫 tooconvert 表格式查詢結果，然後將序列化物件 tooJSON 格式。</span><span class="sxs-lookup"><span data-stu-id="9d277-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="9d277-121">相反地，您可以使用 FOR JSON 子句 tooformat SQL 查詢結果的 hello 為 Azure SQL Database 中的 JSON，並直接在您的應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="9d277-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="9d277-122">在下列範例的 hello，hello Sales.Customer 資料表中的資料列來使用 hello FOR JSON 子句格式化為 JSON 的：</span><span class="sxs-lookup"><span data-stu-id="9d277-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="9d277-123">hello FOR JSON PATH 子句會將 hello hello 查詢結果格式化為 JSON 文字。</span><span class="sxs-lookup"><span data-stu-id="9d277-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="9d277-124">Hello 儲存格的值會產生為 JSON 值時，會使用做為索引鍵，資料行名稱：</span><span class="sxs-lookup"><span data-stu-id="9d277-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="9d277-125">hello 結果集會格式化為 JSON 陣列，其中每個資料列會格式化為個別的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="9d277-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="9d277-126">路徑會指出可以使用點標記法中資料行別名，以自訂 hello 的 JSON 結果的輸出格式。</span><span class="sxs-lookup"><span data-stu-id="9d277-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="9d277-127">下列查詢的 hello 變更 hello hello 輸出 JSON 格式，hello"CustomerName"索引鍵名稱，然後將電話及傳真號碼放入 hello"Contact"的子物件：</span><span class="sxs-lookup"><span data-stu-id="9d277-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="9d277-128">這個查詢的 hello 輸出看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="9d277-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="9d277-129">在此範例中傳回單一 JSON 物件而非陣列藉由指定 hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx)選項。</span><span class="sxs-lookup"><span data-stu-id="9d277-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="9d277-130">如果您知道您要傳回單一物件來作為查詢結果，就可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="9d277-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="9d277-131">hello 主要價值 hello FOR JSON 子句是它可讓您從您格式化為巢狀的 JSON 物件或陣列的資料庫傳回複雜的階層式資料。</span><span class="sxs-lookup"><span data-stu-id="9d277-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="9d277-132">下列範例所示 tooinclude 的訂單屬於 toohello 客戶訂單的巢狀陣列為 hello:</span><span class="sxs-lookup"><span data-stu-id="9d277-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="9d277-133">而不是傳送個別查詢 tooget 客戶資料，然後 toofetch 相關訂單的清單，您可以取得所有 hello 必要的資料使用單一查詢，hello 下列範例輸出所示：</span><span class="sxs-lookup"><span data-stu-id="9d277-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="9d277-134">使用 JSON 資料</span><span class="sxs-lookup"><span data-stu-id="9d277-134">Working with JSON data</span></span>
<span data-ttu-id="9d277-135">如果您不需要嚴格結構化的資料，如果您有複雜的子物件、 陣列或階層式資料，或如果您的資料結構會隨著時間發展，hello JSON 格式可協助您 toorepresent 任何複雜資料結構。</span><span class="sxs-lookup"><span data-stu-id="9d277-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="9d277-136">JSON 是一種文字格式，您可以在 Azure SQL Database 中使用它，就像使用任何其他字串類型一樣。</span><span class="sxs-lookup"><span data-stu-id="9d277-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="9d277-137">您可以用標準 NVARCHAR 形式來傳送或儲存 JSON 資料：</span><span class="sxs-lookup"><span data-stu-id="9d277-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="9d277-138">hello 這個範例中使用的 JSON 資料是由使用 hello nvarchar （max） 類型表示。</span><span class="sxs-lookup"><span data-stu-id="9d277-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="9d277-139">JSON 可以插入此資料表，或提供做為引數的 hello 預存程序中使用標準的 TRANSACT-SQL 語法 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="9d277-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="9d277-140">任何可以與 Azure SQL Database 中的字串資料搭配運作的用戶端語言或程式庫，也將可以與 JSON 資料搭配運作。</span><span class="sxs-lookup"><span data-stu-id="9d277-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="9d277-141">JSON 可儲存在任何支援 hello NVARCHAR 類型，例如記憶體最佳化的資料表或系統建立版本資料表的資料表中。</span><span class="sxs-lookup"><span data-stu-id="9d277-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="9d277-142">JSON 不會產生任何 hello 用戶端程式碼中或在 hello 資料庫層級的條件約束。</span><span class="sxs-lookup"><span data-stu-id="9d277-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="9d277-143">查詢 JSON 資料</span><span class="sxs-lookup"><span data-stu-id="9d277-143">Querying JSON data</span></span>
<span data-ttu-id="9d277-144">如果您有格式化為 JSON 的資料儲存在 Azure SQL 資料表中，JSON 函數可讓您在任何 SQL 查詢中使用此資料。</span><span class="sxs-lookup"><span data-stu-id="9d277-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="9d277-145">Azure SQL Database 中可用的 JSON 函數可讓您將格式化為 JSON 的資料視為任何其他 SQL 資料類型。</span><span class="sxs-lookup"><span data-stu-id="9d277-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="9d277-146">您可輕鬆地從 hello JSON 文字擷取值並用 JSON 資料在任何查詢中：</span><span class="sxs-lookup"><span data-stu-id="9d277-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="9d277-147">hello JSON_VALUE 函數從 JSON 文字儲存 hello 資料行中擷取值。</span><span class="sxs-lookup"><span data-stu-id="9d277-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="9d277-148">這個函式在 JSON 文字 tooextract 中使用類似 JavaScript 路徑 tooreference 值。</span><span class="sxs-lookup"><span data-stu-id="9d277-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="9d277-149">在 SQL 查詢的任何部分可用 hello 擷取值。</span><span class="sxs-lookup"><span data-stu-id="9d277-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="9d277-150">hello JSON_QUERY 函數是類似 tooJSON_VALUE。</span><span class="sxs-lookup"><span data-stu-id="9d277-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="9d277-151">與 JSON_VALUE 不同，此函數會擷取複雜的子物件，例如置於 JSON 文字中的陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="9d277-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="9d277-152">hello JSON_MODIFY 函數可讓您指定應更新的 hello JSON 文字，以及新的值將會覆寫舊 hello hello 值 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="9d277-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="9d277-153">如此一來您可以輕鬆地更新 JSON 文字而不重新剖析 hello 整個結構。</span><span class="sxs-lookup"><span data-stu-id="9d277-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="9d277-154">JSON 中標準文字儲存，因此沒有儲存文字資料行中的 hello 值正確地格式化任何保證。</span><span class="sxs-lookup"><span data-stu-id="9d277-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="9d277-155">您可以確認文字儲存於 JSON 資料行已正確格式化使用的標準 Azure SQL Database check 條件約束和 hello ISJSON 函數：</span><span class="sxs-lookup"><span data-stu-id="9d277-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="9d277-156">如果已正確格式化 hello 輸入的文字 JSON，hello ISJSON 函數傳回 hello 值 1。</span><span class="sxs-lookup"><span data-stu-id="9d277-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="9d277-157">在每次插入或更新 JSON 資料行時，這個條件約束都會確認新的文字值不是格式錯誤的 JSON。</span><span class="sxs-lookup"><span data-stu-id="9d277-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="9d277-158">將 JSON 轉換成表格式格式</span><span class="sxs-lookup"><span data-stu-id="9d277-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="9d277-159">Azure SQL Database 也可讓您將 JSON 集合轉換成表格式格式，然後再載入或查詢 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="9d277-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="9d277-160">OPENJSON 是資料表值函式會剖析 JSON 文字，找出的 JSON 物件陣列，逐一 hello hello 陣列項目的並 hello 陣列的每個元素的 hello 輸出結果中傳回一個資料列。</span><span class="sxs-lookup"><span data-stu-id="9d277-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![JSON 表格式](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="9d277-162">在 hello 上述範例中，我們可以指定其中 toolocate hello （在 hello $ 應開啟 JSON 陣列。訂單路徑），應該當做結果，傳回的資料行，而且其中 toofind hello 將傳回的 JSON 值做為資料格。</span><span class="sxs-lookup"><span data-stu-id="9d277-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="9d277-163">我們可以將轉換的 JSON 陣列，在 hello@orders成一組資料列，變數分析此結果集中，或將資料列插入標準的資料表：</span><span class="sxs-lookup"><span data-stu-id="9d277-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="9d277-164">訂單的 hello 集合格式化為 JSON 陣列，並提供為參數 toohello 預存程序，可以剖析和插入至 hello Orders 資料表。</span><span class="sxs-lookup"><span data-stu-id="9d277-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d277-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d277-165">Next steps</span></span>
<span data-ttu-id="9d277-166">toolearn toointegrate JSON 應用程式時，請參閱這些資源的方式：</span><span class="sxs-lookup"><span data-stu-id="9d277-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="9d277-167">TechNet 部落格</span><span class="sxs-lookup"><span data-stu-id="9d277-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="9d277-168">MSDN 文件</span><span class="sxs-lookup"><span data-stu-id="9d277-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="9d277-169">Channel 9 影片</span><span class="sxs-lookup"><span data-stu-id="9d277-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="9d277-170">toolearn 有關將 JSON 整合到您的應用程式的各種案例，請參閱 「 hello 示範此[Channel 9 影片](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)或找不到符合您的使用案例中的案例[JSON 部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。</span><span class="sxs-lookup"><span data-stu-id="9d277-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

