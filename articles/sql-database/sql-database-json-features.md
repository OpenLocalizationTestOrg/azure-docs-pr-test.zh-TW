---
title: "Azure SQL Database JSON 功能 | Microsoft Docs"
description: "Azure SQL Database 可讓您剖析、查詢及格式化採用「JavaScript 物件標記法」(JSON) 的資料。"
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
ms.openlocfilehash: 883e661107dd838f5c381cdef2c7f891b9a9389c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="81a81-103">開始使用 Azure SQL Database 中的 JSON 功能</span><span class="sxs-lookup"><span data-stu-id="81a81-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="81a81-104">Azure SQL Database 可讓您剖析及查詢以「JavaScript 物件標記法」 [(JSON)](http://www.json.org/) 格式表示的資料，然後將您的關聯式資料匯出成 JSON 文字。</span><span class="sxs-lookup"><span data-stu-id="81a81-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="81a81-105">JSON 是一種用於在新式的 Web 與行動應用程式中交換資料的常用資料格式。</span><span class="sxs-lookup"><span data-stu-id="81a81-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="81a81-106">JSON 也用於將半結構化的資料儲存在記錄檔或 NoSQL 資料庫 (例如 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/)) 中。</span><span class="sxs-lookup"><span data-stu-id="81a81-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="81a81-107">許多 REST Web 服務都會傳回採用 JSON 文字格式的結果，或是接受採用 JSON 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="81a81-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="81a81-108">大多數 Azure 服務 (例如 [Azure 搜尋服務](https://azure.microsoft.com/services/search/)、[Azure 儲存體](https://azure.microsoft.com/services/storage/)、[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/)) 都有會傳回或取用 JSON 的 REST 端點。</span><span class="sxs-lookup"><span data-stu-id="81a81-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="81a81-109">Azure SQL Database 可讓您輕鬆使用 JSON 資料，並將資料庫與新式服務整合。</span><span class="sxs-lookup"><span data-stu-id="81a81-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="81a81-110">概觀</span><span class="sxs-lookup"><span data-stu-id="81a81-110">Overview</span></span>
<span data-ttu-id="81a81-111">Azure SQL Database 提供下列可與 JSON 資料搭配使用的函數：</span><span class="sxs-lookup"><span data-stu-id="81a81-111">Azure SQL Database provides the following functions for working with JSON data:</span></span>

![JSON 函數](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="81a81-113">如果您有 JSON 文字，您可以透過使用內建的函式 [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx)、[JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx) 及 [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx)，從 JSON 擷取資料或確認 JSON 的格式是否正確。</span><span class="sxs-lookup"><span data-stu-id="81a81-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using the built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="81a81-114">[JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) 函式可讓您更新 JSON 文字內的值。</span><span class="sxs-lookup"><span data-stu-id="81a81-114">The [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="81a81-115">針對更進階的查詢和分析， [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) 函數可以將 JSON 物件陣列轉換成一組資料列。</span><span class="sxs-lookup"><span data-stu-id="81a81-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="81a81-116">您可以在傳回的結果集上執行任何 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="81a81-116">Any SQL query can be executed on the returned result set.</span></span> <span data-ttu-id="81a81-117">最後，還有 [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) 子句，此子句可讓您將儲存在關聯式資料表中的資料格式化為 JSON 文字。</span><span class="sxs-lookup"><span data-stu-id="81a81-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="81a81-118">以 JSON 格式將關聯式資料格式化</span><span class="sxs-lookup"><span data-stu-id="81a81-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="81a81-119">如果您有會從資料庫層擷取資料並以 JSON 格式提供回應的 Web 服務，或是有會接受以 JSON 格式化之資料的用戶端 JavaScript 架構或程式庫，您就可以直接在 SQL 查詢中將資料庫內容格式化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="81a81-119">If you have a web service that takes data from the database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="81a81-120">您不再需要撰寫應用程式程式碼以將來自 Azure SQL Database 的結果格式化為 JSON，或包含一些 JSON 序列化程式庫來轉換表格式查詢結果，然後將物件序列化為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="81a81-120">You no longer have to write application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library to convert tabular query results and then serialize objects to JSON format.</span></span> <span data-ttu-id="81a81-121">取得代之的是，您可以在 Azure SQL Database 中使用 FOR JSON 子句將 SQL 查詢結果格式化為 JSON，然後直接在您的應用程式中使用它。</span><span class="sxs-lookup"><span data-stu-id="81a81-121">Instead, you can use the FOR JSON clause to format SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="81a81-122">在下列範例中，會透過使用 FOR JSON 子句，將來自 Sales.Customer 資料表的資料列格式化為 JSON：</span><span class="sxs-lookup"><span data-stu-id="81a81-122">In the following example, rows from the Sales.Customer table are formatted as JSON by using the FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="81a81-123">FOR JSON PATH 子句會將查詢的結果格式化為 JSON 文字。</span><span class="sxs-lookup"><span data-stu-id="81a81-123">The FOR JSON PATH clause formats the results of the query as JSON text.</span></span> <span data-ttu-id="81a81-124">資料行名稱會作為索引鍵，而儲存格值則會以 JSON 值的形式產生︰</span><span class="sxs-lookup"><span data-stu-id="81a81-124">Column names are used as keys, while the cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="81a81-125">結果集會格式化為 JSON 陣列，其中每個資料列皆格式化為個別的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="81a81-125">The result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="81a81-126">PATH 表示您可以在資料行別名中使用點標記法來自訂 JSON 結果的輸出格式。</span><span class="sxs-lookup"><span data-stu-id="81a81-126">PATH indicates that you can customize the output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="81a81-127">下列查詢會變更輸出 JSON 格式中 "CustomerName" 索引鍵的名稱 ，並將電話及傳真號碼放入 "Contact" 子物件中︰</span><span class="sxs-lookup"><span data-stu-id="81a81-127">The following query changes the name of the "CustomerName" key in the output JSON format, and puts phone and fax numbers in the "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="81a81-128">此查詢的輸出看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="81a81-128">The output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="81a81-129">在此範例中，我們透過指定 [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) 選項，傳回了單一 JSON 物件而不是陣列。</span><span class="sxs-lookup"><span data-stu-id="81a81-129">In this example we returned a single JSON object instead of an array by specifying the [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="81a81-130">如果您知道您要傳回單一物件來作為查詢結果，就可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="81a81-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="81a81-131">FOR JSON 子句的主要價值在於，它可讓您從資料庫傳回格式化為巢狀 JSON 物件或陣列的複雜階層式資料。</span><span class="sxs-lookup"><span data-stu-id="81a81-131">The main value of the FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="81a81-132">下列範例說明如何將屬於 Customer 的 Orders 納入成為巢狀 Orders 陣列：</span><span class="sxs-lookup"><span data-stu-id="81a81-132">The following example shows how to include Orders that belong to the Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="81a81-133">您可以不傳送個別查詢來取得 Customer 資料，然後再擷取相關 Orders 清單，而是透過單一查詢來取得所有必要的資料，如下列範例輸出所示：</span><span class="sxs-lookup"><span data-stu-id="81a81-133">Instead of sending separate queries to get Customer data and then to fetch a list of related Orders, you can get all the necessary data with a single query, as shown in the following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="81a81-134">使用 JSON 資料</span><span class="sxs-lookup"><span data-stu-id="81a81-134">Working with JSON data</span></span>
<span data-ttu-id="81a81-135">如果您沒有嚴格結構化的資料，如果您有複雜的子物件、陣列或階層式資料，或如果您的資料結構會隨時間演變，則 JSON 格式可協助您表現任何複雜的資料結構。</span><span class="sxs-lookup"><span data-stu-id="81a81-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, the JSON format can help you to represent any complex data structure.</span></span>

<span data-ttu-id="81a81-136">JSON 是一種文字格式，您可以在 Azure SQL Database 中使用它，就像使用任何其他字串類型一樣。</span><span class="sxs-lookup"><span data-stu-id="81a81-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="81a81-137">您可以用標準 NVARCHAR 形式來傳送或儲存 JSON 資料：</span><span class="sxs-lookup"><span data-stu-id="81a81-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="81a81-138">在此範例中，是透過使用 NVARCHAR(MAX) 類型來表現所使用的 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="81a81-138">The JSON data used in this example is represented by using the NVARCHAR(MAX) type.</span></span> <span data-ttu-id="81a81-139">您可以使用標準 Transact-SQL 語法，將 JSON 插入此資料表中或提供來作為預存程序的引數，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="81a81-139">JSON can be inserted into this table or provided as an argument of the stored procedure using standard Transact-SQL syntax as shown in the following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="81a81-140">任何可以與 Azure SQL Database 中的字串資料搭配運作的用戶端語言或程式庫，也將可以與 JSON 資料搭配運作。</span><span class="sxs-lookup"><span data-stu-id="81a81-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="81a81-141">JSON 可以儲存在任何支援 NVARCHAR 類型的資料表中，例如記憶體最佳化資料表或由系統控制版本的資料表。</span><span class="sxs-lookup"><span data-stu-id="81a81-141">JSON can be stored in any table that supports the NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="81a81-142">JSON 不會導入任何條件約束，不論是用戶端程式碼中還是在資料庫層中的條件約束。</span><span class="sxs-lookup"><span data-stu-id="81a81-142">JSON does not introduce any constraint either in the client-side code or in the database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="81a81-143">查詢 JSON 資料</span><span class="sxs-lookup"><span data-stu-id="81a81-143">Querying JSON data</span></span>
<span data-ttu-id="81a81-144">如果您有格式化為 JSON 的資料儲存在 Azure SQL 資料表中，JSON 函數可讓您在任何 SQL 查詢中使用此資料。</span><span class="sxs-lookup"><span data-stu-id="81a81-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="81a81-145">Azure SQL Database 中可用的 JSON 函數可讓您將格式化為 JSON 的資料視為任何其他 SQL 資料類型。</span><span class="sxs-lookup"><span data-stu-id="81a81-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="81a81-146">您可以輕鬆地從 JSON 文字中擷取值，然後在任何查詢中使用 JSON 資料︰</span><span class="sxs-lookup"><span data-stu-id="81a81-146">You can easily extract values from the JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="81a81-147">JSON_VALUE 函數會從儲存在 Data 資料行的 JSON 文字中擷取值。</span><span class="sxs-lookup"><span data-stu-id="81a81-147">The JSON_VALUE function extracts a value from JSON text stored in the Data column.</span></span> <span data-ttu-id="81a81-148">此函數會使用類似 JavaScript 的路徑來參考所要擷取的 JSON 文字中的值。</span><span class="sxs-lookup"><span data-stu-id="81a81-148">This function uses a JavaScript-like path to reference a value in JSON text to extract.</span></span> <span data-ttu-id="81a81-149">所擷取的值可以在 SQL 查詢的任何部分中使用。</span><span class="sxs-lookup"><span data-stu-id="81a81-149">The extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="81a81-150">JSON_QUERY 函數類似於 JSON_VALUE。</span><span class="sxs-lookup"><span data-stu-id="81a81-150">The JSON_QUERY function is similar to JSON_VALUE.</span></span> <span data-ttu-id="81a81-151">與 JSON_VALUE 不同，此函數會擷取複雜的子物件，例如置於 JSON 文字中的陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="81a81-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="81a81-152">JSON_MODIFY 函數可讓您指定 JSON 文字中應更新的值路徑，以及將覆寫舊值的新值。</span><span class="sxs-lookup"><span data-stu-id="81a81-152">The JSON_MODIFY function lets you specify the path of the value in the JSON text that should be updated, as well as a new value that will overwrite the old one.</span></span> <span data-ttu-id="81a81-153">如此一來，您便可以輕鬆更新 JSON 文字，而不需重新剖析整個結構。</span><span class="sxs-lookup"><span data-stu-id="81a81-153">This way you can easily update JSON text without reparsing the entire structure.</span></span>

<span data-ttu-id="81a81-154">由於 JSON 是以標準文字儲存，因此無法保證儲存在文字資料行中的值格式會正確。</span><span class="sxs-lookup"><span data-stu-id="81a81-154">Since JSON is stored in a standard text, there are no guarantees that the values stored in text columns are properly formatted.</span></span> <span data-ttu-id="81a81-155">您可以使用標準的 Azure SQL Database 檢查條件約束和 ISJSON 函數，來確認儲存在 JSON 資料行中的文字是否格式正確︰</span><span class="sxs-lookup"><span data-stu-id="81a81-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and the ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="81a81-156">如果輸入的文字是格式正確的 JSON，ISJSON 函數就會傳回值 1。</span><span class="sxs-lookup"><span data-stu-id="81a81-156">If the input text is properly formatted JSON, the ISJSON function returns the value 1.</span></span> <span data-ttu-id="81a81-157">在每次插入或更新 JSON 資料行時，這個條件約束都會確認新的文字值不是格式錯誤的 JSON。</span><span class="sxs-lookup"><span data-stu-id="81a81-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="81a81-158">將 JSON 轉換成表格式格式</span><span class="sxs-lookup"><span data-stu-id="81a81-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="81a81-159">Azure SQL Database 也可讓您將 JSON 集合轉換成表格式格式，然後再載入或查詢 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="81a81-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="81a81-160">OPENJSON 是一個資料表值函數，可剖析 JSON 文字、找出 JSON 物件陣列、逐一查看陣列的元素，然後在輸出結果中為每個陣列元素傳回一個資料列。</span><span class="sxs-lookup"><span data-stu-id="81a81-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through the elements of the array, and returns one row in the output result for each element of the array.</span></span>

![JSON 表格式](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="81a81-162">在上述範例中，我們可以指定要在哪裡尋找應該開啟的 JSON 陣列 (在 $.Orders 路徑中)、應該傳回哪些資料行作為結果，以及要在哪裡尋找將以資料格形式傳回的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="81a81-162">In the example above, we can specify where to locate the JSON array that should be opened (in the $.Orders path), what columns should be returned as result, and where to find the JSON values that will be returned as cells.</span></span>

<span data-ttu-id="81a81-163">我們可以將 @orders 變數中的 JSON 陣列轉換成一組資料列、分析此結果集，或將資料列插入標準資料表中︰</span><span class="sxs-lookup"><span data-stu-id="81a81-163">We can transform a JSON array in the @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="81a81-164">我們可以剖析採用 JSON 陣列格式並作為參數提供給預存程序的訂單集合，然後將它插入 Orders 資料表中。</span><span class="sxs-lookup"><span data-stu-id="81a81-164">The collection of orders formatted as a JSON array and provided as a parameter to the stored procedure can be parsed and inserted into the Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81a81-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81a81-165">Next steps</span></span>
<span data-ttu-id="81a81-166">若要了解如何將 JSON 整合到您的應用程式中，請參閱下列資源︰</span><span class="sxs-lookup"><span data-stu-id="81a81-166">To learn how to integrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="81a81-167">TechNet 部落格</span><span class="sxs-lookup"><span data-stu-id="81a81-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="81a81-168">MSDN 文件</span><span class="sxs-lookup"><span data-stu-id="81a81-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="81a81-169">Channel 9 影片</span><span class="sxs-lookup"><span data-stu-id="81a81-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="81a81-170">若要了解將 JSON 整合到您應用程式中的各種案例，請參閱這段 [Channel 9 影片](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)中的示範，或從 [JSON 部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)中尋找符合您使用案例的情況。</span><span class="sxs-lookup"><span data-stu-id="81a81-170">To learn about various scenarios for integrating JSON into your application, see the demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

