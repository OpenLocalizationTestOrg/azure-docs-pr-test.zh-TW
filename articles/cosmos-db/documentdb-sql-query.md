---
title: "Azure Cosmos DB DocumentDB api aaaSQL 查詢 |Microsoft 文件"
description: "了解 Azure Cosmos DB 的 SQL 語法、資料庫概念及 SQL 查詢。 SQL 可作為 Azure Cosmos DB 中的 JSON 查詢語言。"
keywords: "sql 語法, sql 查詢, sql 查詢, json 查詢語言, 資料庫概念和 sql 查詢, 彙總函式"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="12279-105">適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="12279-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="12279-106">Microsoft Azure Cosmos DB 支援使用 SQL (結構化查詢語言) 作為 JSON 查詢語言來查詢文件。</span><span class="sxs-lookup"><span data-stu-id="12279-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="12279-107">Cosmos DB 確實無結構描述。</span><span class="sxs-lookup"><span data-stu-id="12279-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="12279-108">由於其承諾 toohello JSON 資料模型直接在 hello 資料庫引擎內，它會提供自動編製索引的 JSON 文件而不需要明確的結構描述或建立次要索引。</span><span class="sxs-lookup"><span data-stu-id="12279-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="12279-109">時設計 Cosmos DB hello 查詢語言，我們必須記住兩個目標：</span><span class="sxs-lookup"><span data-stu-id="12279-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="12279-110">而不是 ¬ 新的 JSON 查詢語言，我們想 toosupport SQL。</span><span class="sxs-lookup"><span data-stu-id="12279-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="12279-111">SQL 是一種 hello 最熟悉且常用查詢的語言。</span><span class="sxs-lookup"><span data-stu-id="12279-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="12279-112">Cosmos DB SQL 提供一個正式的程式設計模型，可在 JSON 文件上進行豐富的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="12279-113">做為能夠直接在 hello 資料庫引擎中執行 JavaScript 的 JSON 文件資料庫，我們想 toouse JavaScript 的程式設計模型為 hello 基礎的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="12279-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="12279-114">在 JavaScript 的型別系統、 運算式評估，以及函式引動過程根目錄為 hello DocumentDB API SQL。</span><span class="sxs-lookup"><span data-stu-id="12279-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="12279-115">這除了其他功能之外，還進而提供自然程式設計模型來進行關聯式投射、跨 JSON 文件的階層式導覽、自我聯結、空間查詢，以及叫用完全以 JavaScript 撰寫的使用者定義函式 (UDF)。</span><span class="sxs-lookup"><span data-stu-id="12279-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="12279-116">我們相信，這些功能 hello 應用程式與 hello 資料庫之間的索引鍵 tooreducing hello 人事而很重要的開發人員的生產力。</span><span class="sxs-lookup"><span data-stu-id="12279-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="12279-117">我們建議您藉由監看下列影片，其中 Aravind Ramachandran 顯示 Cosmos 資料庫 （linq） 功能，hello 和造訪開始使用我們[查詢遊樂場](http://www.documentdb.com/sql/demo)，其中您可以試用 Cosmos DB 而執行 SQL 查詢我們的資料集。</span><span class="sxs-lookup"><span data-stu-id="12279-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="12279-118">然後，傳回 toothis 文章中，我們開始使用 SQL 查詢教學課程會引導您進行一些簡單的 JSON 文件和 SQL 命令的位置。</span><span class="sxs-lookup"><span data-stu-id="12279-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="12279-119"><a id="GettingStarted"></a>開始在 Cosmos DB 中使用 SQL 命令</span><span class="sxs-lookup"><span data-stu-id="12279-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="12279-120">toosee Cosmos DB SQL 在運作，讓我們以幾個簡單的 JSON 文件開頭並逐步引導一些簡單的查詢，對它。</span><span class="sxs-lookup"><span data-stu-id="12279-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="12279-121">請考慮有關兩個家族的這兩份 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="12279-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="12279-122">以 Cosmos DB，我們不需要 toocreate 任何結構描述或次要索引明確。</span><span class="sxs-lookup"><span data-stu-id="12279-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="12279-123">我們只需要 tooinsert hello JSON 文件 tooa Cosmos DB 集合和後續查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="12279-124">這裡我們有簡單的 JSON 文件 hello Andersen 系列、 hello 父系、 子系 （和其寵物） 地址和註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="12279-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="12279-125">hello 文件具有字串、 數字、 布林值、 陣列和巢狀的屬性。</span><span class="sxs-lookup"><span data-stu-id="12279-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="12279-126">**文件**</span><span class="sxs-lookup"><span data-stu-id="12279-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="12279-127">以下是第二份具有些微差異的文件：使用 `givenName` 和 `familyName` 來取代 `firstName` 和 `lastName`。</span><span class="sxs-lookup"><span data-stu-id="12279-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="12279-128">**文件**</span><span class="sxs-lookup"><span data-stu-id="12279-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="12279-129">現在讓我們來試試幾個查詢針對此資料 toounderstand hello 的某些索引鍵 DocumentDB API SQL 層面。</span><span class="sxs-lookup"><span data-stu-id="12279-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="12279-130">Hello 下列查詢會傳回 hello 文件符合 hello 識別碼 欄位的位置，例如`AndersenFamily`。</span><span class="sxs-lookup"><span data-stu-id="12279-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="12279-131">因為它是`SELECT *`，hello 查詢的 hello 輸出是 hello 完整的 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="12279-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="12279-132">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-133">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="12279-134">現在請試想 hello 案例，我們需要 tooreformat hello 不同組織結構的 JSON 輸出的位置。</span><span class="sxs-lookup"><span data-stu-id="12279-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="12279-135">此專案的新 JSON 物件包含兩個選取的欄位，名稱與城市時 hello 地址的縣 （市） 名稱相同的 hello hello 狀態查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="12279-136">在此情況下，"NY, NY" 相符。</span><span class="sxs-lookup"><span data-stu-id="12279-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="12279-137">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="12279-138">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="12279-139">hello 下一個查詢會傳回所有 hello 指定名稱的子系中 hello 系列，其識別碼符合`WakefieldFamily`的居住地的 hello 縣 （市） 排序。</span><span class="sxs-lookup"><span data-stu-id="12279-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="12279-140">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="12279-141">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="12279-142">我們希望 toodraw 注意 tooa hello Cosmos DB 值得注意幾個層面查詢語言，瀏覽到目前為止，我們已看到 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="12279-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="12279-143">因為 DocumentDB API SQL 的處理對象是 JSON 值，所以它處理的是樹狀形式的實體，而不是資料列和資料行。</span><span class="sxs-lookup"><span data-stu-id="12279-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="12279-144">因此，hello 語言可讓您像參考 toonodes 任意深度，在 hello 樹狀結構的`Node1.Node2.Node3…..Nodem`，類似 toorelational SQL 參考 toohello 兩個組件參考的`<table>.<column>`。</span><span class="sxs-lookup"><span data-stu-id="12279-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="12279-145">hello 結構化查詢語言適用於無結構描述資料。</span><span class="sxs-lookup"><span data-stu-id="12279-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="12279-146">因此，動態 hello 類型系統的需求 toobe 繫結。</span><span class="sxs-lookup"><span data-stu-id="12279-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="12279-147">hello 相同的運算式可能會產生不同的文件上不同類型。</span><span class="sxs-lookup"><span data-stu-id="12279-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="12279-148">hello 查詢的結果是有效的 JSON 值，但不是保證 toobe 固定的結構描述。</span><span class="sxs-lookup"><span data-stu-id="12279-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="12279-149">Cosmos DB 只支援嚴謹的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="12279-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="12279-150">這表示 hello 類型系統和運算式都是受限制的 toodeal 只能使用 JSON 類型。</span><span class="sxs-lookup"><span data-stu-id="12279-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="12279-151">請參閱 toohello [JSON 規格](http://www.json.org/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="12279-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="12279-152">Cosmos DB 集合是 JSON 文件的無結構描述容器。</span><span class="sxs-lookup"><span data-stu-id="12279-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="12279-153">內含項目而不是主索引鍵和外部索引鍵的關聯，會隱含擷取內部與跨文件集合中的資料實體中的 hello 關聯。</span><span class="sxs-lookup"><span data-stu-id="12279-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="12279-154">這是值得按照本文件稍後所討論的 hello 文件內部聯結的重要層面。</span><span class="sxs-lookup"><span data-stu-id="12279-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="12279-155"><a id="Indexing"></a> Cosmos DB 索引編製</span><span class="sxs-lookup"><span data-stu-id="12279-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="12279-156">我們 hello DocumentDB API SQL 語法之前，值得瀏覽索引設計 Cosmos DB 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="12279-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="12279-157">資料庫索引 hello 用途是 tooserve 各種表單和 （如 CPU 和輸入/輸出） 的最小的資源耗用量的圖形中的查詢，同時提供良好的輸送量和低延遲。</span><span class="sxs-lookup"><span data-stu-id="12279-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="12279-158">通常，hello 所選擇的 hello 正確索引，來查詢資料庫需要許多規劃和試驗。</span><span class="sxs-lookup"><span data-stu-id="12279-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="12279-159">這個方法會造成無結構描述資料庫 hello 資料不符合 tooa 嚴格的結構描述和快速發展的其中一項挑戰。</span><span class="sxs-lookup"><span data-stu-id="12279-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="12279-160">因此，當我們設計 hello Cosmos DB 索引子系統，我們會設定 hello 下列目標：</span><span class="sxs-lookup"><span data-stu-id="12279-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="12279-161">索引文件，而不需要結構描述： hello 索引子系統不需要任何結構描述資訊或提出任何假設結構描述的 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="12279-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="12279-162">支援的有效率、 豐富的階層式，和關聯式查詢： hello 索引支援 hello Cosmos DB 查詢語言，包括支援階層式和關聯式投影。</span><span class="sxs-lookup"><span data-stu-id="12279-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="12279-163">支援持續性磁碟區的寫入 in face of 一致的查詢： 針對高寫入輸送量工作負載使用一致的查詢，hello 索引會以累加的方式，有效率，且在線上在更新持續的磁碟區的寫入 hello 字體。</span><span class="sxs-lookup"><span data-stu-id="12279-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="12279-164">hello 一致的索引更新為在 hello 一致性層級中的 hello 設定使用者 hello 文件服務的重要 tooserve hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="12279-165">多租用戶的支援： 跨租用戶中指定的資源控管 hello 保留為基礎的模型，索引不會執行更新的系統資源 （CPU、 記憶體和輸入/輸出作業每秒） 配置每個複本 hello 預算。</span><span class="sxs-lookup"><span data-stu-id="12279-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="12279-166">儲存體效率： 成本效益的 hello 磁碟上儲存額外負荷 hello 索引是限制與可預測。</span><span class="sxs-lookup"><span data-stu-id="12279-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="12279-167">這是非常重要，因為 Cosmos DB 讓 hello 開發人員 toomake 成本考量取捨索引關聯 toohello 查詢效能的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="12279-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="12279-168">請參閱 toohello [Azure Cosmos DB 範例](https://github.com/Azure/azure-documentdb-net)msdn 範例顯示如何 tooconfigure hello 集合的編製索引原則。</span><span class="sxs-lookup"><span data-stu-id="12279-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="12279-169">我們現在可以使用到 hello 的 hello Azure Cosmos DB SQL 語法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="12279-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="12279-170"><a id="Basics"></a>Azure Cosmos DB SQL 查詢的基本概念</span><span class="sxs-lookup"><span data-stu-id="12279-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="12279-171">根據 ANSI-SQL 標準，每個查詢都會包含 SELECT 子句以及選擇性的 FROM 和 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="12279-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="12279-172">一般而言，每個查詢，會列舉 hello FROM 子句中的 hello 來源。</span><span class="sxs-lookup"><span data-stu-id="12279-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="12279-173">然後 hello 篩選中的 WHERE 子句會套用至 hello 來源 tooretrieve hello JSON 文件的子集。</span><span class="sxs-lookup"><span data-stu-id="12279-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="12279-174">最後，使用 hello SELECT 子句 tooproject hello 要求 hello 中的 JSON 值選取清單。</span><span class="sxs-lookup"><span data-stu-id="12279-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="12279-175"><a id="FromClause"></a>FROM 子句</span><span class="sxs-lookup"><span data-stu-id="12279-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="12279-176">hello`FROM <from_specification>`子句是選擇性的除非 hello 來源經過篩選，或稍後在 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="12279-177">這個子句 hello 用途是查詢必須運作時的 hello toospecify hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="12279-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="12279-178">Hello 整個集合通常是 hello 來源，但其中一個可以改為指定 hello 集合的子集。</span><span class="sxs-lookup"><span data-stu-id="12279-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="12279-179">查詢類似`SELECT * FROM Families`表示 hello 整個系列集合是透過哪些 tooenumerate hello 來源。</span><span class="sxs-lookup"><span data-stu-id="12279-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="12279-180">根的特殊識別項可以是使用的 toorepresent hello 集合，而不是使用 hello 集合名稱。</span><span class="sxs-lookup"><span data-stu-id="12279-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="12279-181">hello 下列清單包含每個查詢會強制執行的 hello 規則：</span><span class="sxs-lookup"><span data-stu-id="12279-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="12279-182">hello 集合可以是別名，例如`SELECT f.id FROM Families AS f`或只是`SELECT f.id FROM Families f`。</span><span class="sxs-lookup"><span data-stu-id="12279-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="12279-183">這裡`f`hello 方法相當於`Families`。</span><span class="sxs-lookup"><span data-stu-id="12279-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="12279-184">`AS`這是選擇性的關鍵字 tooalias hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="12279-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="12279-185">一次別名 hello 原始來源無法繫結。</span><span class="sxs-lookup"><span data-stu-id="12279-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="12279-186">例如，`SELECT Families.id FROM Families f`的語法無效，因為無法再解析 hello 識別碼 」 系列 」。</span><span class="sxs-lookup"><span data-stu-id="12279-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="12279-187">需要 toobe 參考的所有屬性必須都是完整名稱。</span><span class="sxs-lookup"><span data-stu-id="12279-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="12279-188">在嚴格的結構描述是否遵循 hello 不存在，這是強制的 tooavoid 任何模稜兩可的繫結。</span><span class="sxs-lookup"><span data-stu-id="12279-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="12279-189">因此，`SELECT id FROM Families f`自 hello 屬性的語法無效`id`未繫結。</span><span class="sxs-lookup"><span data-stu-id="12279-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="12279-190">子文件</span><span class="sxs-lookup"><span data-stu-id="12279-190">Subdocuments</span></span>
<span data-ttu-id="12279-191">hello 來源也可以降低的 tooa 較小的子集。</span><span class="sxs-lookup"><span data-stu-id="12279-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="12279-192">比方說，tooenumerating 每份文件樹狀子目錄，hello subroot 無法再變成 hello 來源 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="12279-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="12279-193">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="12279-194">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="12279-195">雖然上述範例中的 hello 做 hello 來源使用陣列，物件也可用為 hello 來源，此為 hello 下列範例中所示： 任何有效的 JSON 值 （未定義），可以在 hello 來源考慮納入 hello 結果hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="12279-196">如果還沒有某些系列`address.state`值，會將它們排除 hello 查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="12279-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="12279-197">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="12279-198">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="12279-199"><a id="WhereClause"></a>WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="12279-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="12279-200">hello WHERE 子句 (**`WHERE <filter_condition>`**) 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="12279-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="12279-201">它會指定 hello 條件 hello hello 來源所提供的 JSON 文件必須符合在順序 toobe 納入 hello 結果的一部分。</span><span class="sxs-lookup"><span data-stu-id="12279-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="12279-202">任何 JSON 文件都必須評估 hello 指定條件太"true"toobe hello 結果列入考量。</span><span class="sxs-lookup"><span data-stu-id="12279-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="12279-203">hello 子句供順序 toodetermine hello 絕對最小的子集可以屬於 hello 結果的來源文件中的 hello 索引圖層的情況。</span><span class="sxs-lookup"><span data-stu-id="12279-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="12279-204">hello 下列查詢會要求包含一個 name 屬性，其值的文件`AndersenFamily`。</span><span class="sxs-lookup"><span data-stu-id="12279-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="12279-205">名稱屬性，沒有任何其他文件或 hello 值不符合`AndersenFamily`排除。</span><span class="sxs-lookup"><span data-stu-id="12279-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="12279-206">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-207">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="12279-208">hello 前一個範例示範簡單的等號查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="12279-209">DocumentDB API SQL 也支援各種純量運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="12279-210">hello 最常使用的是二進位和一元的運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="12279-211">從 hello 來源 JSON 物件的屬性參考也是有效的運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="12279-212">下列二元運算子的 hello 目前支援，並可用於查詢中 hello 遵循範例所示：</span><span class="sxs-lookup"><span data-stu-id="12279-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="12279-213">算術</span><span class="sxs-lookup"><span data-stu-id="12279-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="12279-214">+、-、*、/、%</span><span class="sxs-lookup"><span data-stu-id="12279-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="12279-215">位元</span><span class="sxs-lookup"><span data-stu-id="12279-215">Bitwise</span></span></td>    
<td><span data-ttu-id="12279-216">|、&、^、<<、>>、>>> (右移位並填滿零)</span><span class="sxs-lookup"><span data-stu-id="12279-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="12279-217">邏輯</span><span class="sxs-lookup"><span data-stu-id="12279-217">Logical</span></span></td>
<td><span data-ttu-id="12279-218">AND、OR、NOT</span><span class="sxs-lookup"><span data-stu-id="12279-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="12279-219">比較</span><span class="sxs-lookup"><span data-stu-id="12279-219">Comparison</span></span></td>    
<td><span data-ttu-id="12279-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="12279-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="12279-221">String</span><span class="sxs-lookup"><span data-stu-id="12279-221">String</span></span></td>    
<td><span data-ttu-id="12279-222">|| (串連)</span><span class="sxs-lookup"><span data-stu-id="12279-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="12279-223">讓我們了解一些使用二元運算子的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="12279-224">hello 一元運算子 +、-、 ~ 不會也支援，而且可以用於在查詢中 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="12279-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="12279-225">此外 toobinary 和一元運算子，屬性也允許的參考。</span><span class="sxs-lookup"><span data-stu-id="12279-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="12279-226">例如，`SELECT * FROM Families f WHERE f.isRegistered`傳回 hello 包含 hello 屬性的 JSON 文件`isRegistered`會 hello 屬性的值等於 toohello JSON`true`值。</span><span class="sxs-lookup"><span data-stu-id="12279-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="12279-227">任何其他值 (false、 null、 未定義， `<number>`， `<string>`， `<object>`，`<array>`等等) 會導致 hello 結果會排除 toohello 來源文件。</span><span class="sxs-lookup"><span data-stu-id="12279-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="12279-228">相等和比較運算子</span><span class="sxs-lookup"><span data-stu-id="12279-228">Equality and comparison operators</span></span>
<span data-ttu-id="12279-229">hello 下表顯示 hello 結果相等比較 DocumentDB API SQL 中任何兩個 JSON 類型。</span><span class="sxs-lookup"><span data-stu-id="12279-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="12279-230">
            <strong>運算子</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="12279-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="12279-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="12279-233">
            <strong>布林值</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="12279-234">
            <strong>數字</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="12279-235">
            <strong>字串</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="12279-236">
            <strong>物件</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="12279-237">
            <strong>陣列</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="12279-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="12279-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="12279-248">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="12279-254">
            <strong>布林值<strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="12279-257">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="12279-262">
            <strong>數字<strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="12279-266">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="12279-270">
            <strong>字串<strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="12279-275">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="12279-278">
            <strong>物件<strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="12279-284">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="12279-286">
            <strong>陣列<strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="12279-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="12279-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="12279-293">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="12279-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="12279-294">針對其他的比較運算子，例如 >，> =、 ！ =、 < 和 < =、 hello 適用下列規則：</span><span class="sxs-lookup"><span data-stu-id="12279-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="12279-295">不同類型的比較會導致 Undefined。</span><span class="sxs-lookup"><span data-stu-id="12279-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="12279-296">兩個物件或兩個陣列之間的比較會導致 Undefined。</span><span class="sxs-lookup"><span data-stu-id="12279-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="12279-297">如果 hello hello hello 篩選中的純量運算式的結果會是未定義，hello 對應文件就不會包含在 hello 結果，因為未定義不會以邏輯方式等同太"true"。</span><span class="sxs-lookup"><span data-stu-id="12279-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="12279-298">BETWEEN 關鍵字</span><span class="sxs-lookup"><span data-stu-id="12279-298">BETWEEN keyword</span></span>
<span data-ttu-id="12279-299">您也可以使用 ANSI SQL 中的 hello BETWEEN 關鍵字 tooexpress 查詢如值的範圍。</span><span class="sxs-lookup"><span data-stu-id="12279-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="12279-300">BETWEEN 可用於字串或數字。</span><span class="sxs-lookup"><span data-stu-id="12279-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="12279-301">例如，此查詢會傳回所有系列的文件中的 hello 第一個子系等級是 1-5 （兩者皆包含） 之間。</span><span class="sxs-lookup"><span data-stu-id="12279-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="12279-302">不同於在 ANSI SQL，您也可以使用 hello BETWEEN 子句類似 hello 下列範例中的 hello FROM 子句中。</span><span class="sxs-lookup"><span data-stu-id="12279-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="12279-303">更快的查詢執行時間，請記得 toocreate 會使用針對任何數值屬性/路徑篩選 hello BETWEEN 子句中的範圍索引類型編製索引原則。</span><span class="sxs-lookup"><span data-stu-id="12279-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="12279-304">hello 之間使用 BETWEEN DocumentDB API 和 ANSI SQL 中的主要差異是，你可以針對混合類型的屬性範圍查詢 – 例如，您可能必須是數字 (5) 「 等級 」，在某些文件和其他項目 (「 grade4") 中的字串。</span><span class="sxs-lookup"><span data-stu-id="12279-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="12279-305">在這些情況下，像是在 JavaScript 中，比較兩個不同類型結果，在 「 定義 」 和 hello 文件將會略過。</span><span class="sxs-lookup"><span data-stu-id="12279-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="12279-306">邏輯 (AND、OR 和 NOT) 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="12279-307">邏輯運算子的運算對象是布林值。</span><span class="sxs-lookup"><span data-stu-id="12279-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="12279-308">這些運算子 hello 邏輯事實資料表是以 hello 下表所示。</span><span class="sxs-lookup"><span data-stu-id="12279-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="12279-309">或</span><span class="sxs-lookup"><span data-stu-id="12279-309">OR</span></span> | <span data-ttu-id="12279-310">True</span><span class="sxs-lookup"><span data-stu-id="12279-310">True</span></span> | <span data-ttu-id="12279-311">False</span><span class="sxs-lookup"><span data-stu-id="12279-311">False</span></span> | <span data-ttu-id="12279-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12279-313">True</span><span class="sxs-lookup"><span data-stu-id="12279-313">True</span></span> |<span data-ttu-id="12279-314">True</span><span class="sxs-lookup"><span data-stu-id="12279-314">True</span></span> |<span data-ttu-id="12279-315">True</span><span class="sxs-lookup"><span data-stu-id="12279-315">True</span></span> |<span data-ttu-id="12279-316">True</span><span class="sxs-lookup"><span data-stu-id="12279-316">True</span></span> |
| <span data-ttu-id="12279-317">False</span><span class="sxs-lookup"><span data-stu-id="12279-317">False</span></span> |<span data-ttu-id="12279-318">True</span><span class="sxs-lookup"><span data-stu-id="12279-318">True</span></span> |<span data-ttu-id="12279-319">False</span><span class="sxs-lookup"><span data-stu-id="12279-319">False</span></span> |<span data-ttu-id="12279-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-320">Undefined</span></span> |
| <span data-ttu-id="12279-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-321">Undefined</span></span> |<span data-ttu-id="12279-322">True</span><span class="sxs-lookup"><span data-stu-id="12279-322">True</span></span> |<span data-ttu-id="12279-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-323">Undefined</span></span> |<span data-ttu-id="12279-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-324">Undefined</span></span> |

| <span data-ttu-id="12279-325">AND</span><span class="sxs-lookup"><span data-stu-id="12279-325">AND</span></span> | <span data-ttu-id="12279-326">True</span><span class="sxs-lookup"><span data-stu-id="12279-326">True</span></span> | <span data-ttu-id="12279-327">False</span><span class="sxs-lookup"><span data-stu-id="12279-327">False</span></span> | <span data-ttu-id="12279-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12279-329">True</span><span class="sxs-lookup"><span data-stu-id="12279-329">True</span></span> |<span data-ttu-id="12279-330">True</span><span class="sxs-lookup"><span data-stu-id="12279-330">True</span></span> |<span data-ttu-id="12279-331">False</span><span class="sxs-lookup"><span data-stu-id="12279-331">False</span></span> |<span data-ttu-id="12279-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-332">Undefined</span></span> |
| <span data-ttu-id="12279-333">False</span><span class="sxs-lookup"><span data-stu-id="12279-333">False</span></span> |<span data-ttu-id="12279-334">False</span><span class="sxs-lookup"><span data-stu-id="12279-334">False</span></span> |<span data-ttu-id="12279-335">False</span><span class="sxs-lookup"><span data-stu-id="12279-335">False</span></span> |<span data-ttu-id="12279-336">False</span><span class="sxs-lookup"><span data-stu-id="12279-336">False</span></span> |
| <span data-ttu-id="12279-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-337">Undefined</span></span> |<span data-ttu-id="12279-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-338">Undefined</span></span> |<span data-ttu-id="12279-339">False</span><span class="sxs-lookup"><span data-stu-id="12279-339">False</span></span> |<span data-ttu-id="12279-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-340">Undefined</span></span> |

| <span data-ttu-id="12279-341">NOT</span><span class="sxs-lookup"><span data-stu-id="12279-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="12279-342">True</span><span class="sxs-lookup"><span data-stu-id="12279-342">True</span></span> |<span data-ttu-id="12279-343">False</span><span class="sxs-lookup"><span data-stu-id="12279-343">False</span></span> |
| <span data-ttu-id="12279-344">False</span><span class="sxs-lookup"><span data-stu-id="12279-344">False</span></span> |<span data-ttu-id="12279-345">True</span><span class="sxs-lookup"><span data-stu-id="12279-345">True</span></span> |
| <span data-ttu-id="12279-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-346">Undefined</span></span> |<span data-ttu-id="12279-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="12279-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="12279-348">IN 關鍵字</span><span class="sxs-lookup"><span data-stu-id="12279-348">IN keyword</span></span>
<span data-ttu-id="12279-349">可以使用的 toocheck hello IN 關鍵字，是否指定的值符合清單中的任何值。</span><span class="sxs-lookup"><span data-stu-id="12279-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="12279-350">比方說，此查詢會傳回所有系列的文件識別碼 hello 其中是其中一個"WakefieldFamily"或"AndersenFamily"。</span><span class="sxs-lookup"><span data-stu-id="12279-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="12279-351">這個範例會傳回所有文件位置 hello 狀態可以是任何 hello 指定值。</span><span class="sxs-lookup"><span data-stu-id="12279-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="12279-352">三元 (?) 和聯合 (??) 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="12279-353">hello 三元和 Coalesce 運算子可以是使用的 toobuild 條件運算式，類似 toopopular 程式設計語言，例如 C# 和 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="12279-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="12279-354">時建構新 JSON 屬性上 hello 飛 hello 三元 （？） 運算子可以是非常實用。</span><span class="sxs-lookup"><span data-stu-id="12279-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="12279-355">比方說，現在您可以撰寫查詢 tooclassify hello 類別層級到人類可讀取的格式，例如初學者/中繼/進階如下所示。</span><span class="sxs-lookup"><span data-stu-id="12279-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="12279-356">您也可以巢狀 hello 呼叫 toohello 運算子類似下列的 hello 查詢中。</span><span class="sxs-lookup"><span data-stu-id="12279-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="12279-357">做為與其他查詢運算子，如果 hello hello 條件運算式中參考的屬性已遺失在任何文件，或如果要比較的 hello 類型不同，則這些文件會排除 hello 查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="12279-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="12279-358">hello Coalesce （？） 運算子可以是 （也稱為 tooefficiently 核取用於 hello 是否有屬性</span><span class="sxs-lookup"><span data-stu-id="12279-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="12279-359">已定義) 於文件中。</span><span class="sxs-lookup"><span data-stu-id="12279-359">is defined) in a document.</span></span> <span data-ttu-id="12279-360">針對半結構化或混合類型的資料執行查詢時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="12279-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="12279-361">例如，此查詢傳回 hello"lastName"如果存在或使用 「 姓氏 」 hello 如果它不存在。</span><span class="sxs-lookup"><span data-stu-id="12279-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="12279-362"><a id="EscapingReservedKeywords"></a>加上引號的屬性存取子</span><span class="sxs-lookup"><span data-stu-id="12279-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="12279-363">您也可以存取屬性使用 hello 加上引號的屬性運算子`[]`。</span><span class="sxs-lookup"><span data-stu-id="12279-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="12279-364">例如， `SELECT c.grade` and `SELECT c["grade"]` 是相等的。</span><span class="sxs-lookup"><span data-stu-id="12279-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="12279-365">這個語法時，您需要 tooescape 屬性，可包含空格、 特殊字元，或發生 tooshare hello 相同的名稱，以 SQL 關鍵字或保留的字。</span><span class="sxs-lookup"><span data-stu-id="12279-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="12279-366"><a id="SelectClause"></a>SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="12279-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="12279-367">hello SELECT 子句 (**`SELECT <select_list>`**) 是必要項，指定哪些值會從擷取 hello 查詢一樣在 ANSI SQL。</span><span class="sxs-lookup"><span data-stu-id="12279-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="12279-368">已篩選之上 hello 來源文件的 hello 子集會傳遞到 hello 投影階段中，其中 hello 指定擷取 JSON 值，並建構新的 JSON 物件時，針對每個輸入傳遞至其本身。</span><span class="sxs-lookup"><span data-stu-id="12279-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="12279-369">下列範例中的 hello 顯示一般的 SELECT 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="12279-370">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-371">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="12279-372">巢狀屬性</span><span class="sxs-lookup"><span data-stu-id="12279-372">Nested properties</span></span>
<span data-ttu-id="12279-373">在下列範例的 hello，我們會將兩個巢狀的屬性投射`f.address.state`和`f.address.city`。</span><span class="sxs-lookup"><span data-stu-id="12279-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="12279-374">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-375">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="12279-376">投影也支援 JSON 運算式 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="12279-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="12279-377">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-378">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="12279-379">讓我們看看 hello 角色`$1`這裡。</span><span class="sxs-lookup"><span data-stu-id="12279-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="12279-380">hello`SELECT`子句需要 toocreate JSON 物件，但由於未不提供任何索引鍵，則我們會使用隱含引數的變數名稱開頭為`$1`。</span><span class="sxs-lookup"><span data-stu-id="12279-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="12279-381">例如，此查詢會傳回兩個隱含引數變數，名稱為 `$1` 和 `$2`。</span><span class="sxs-lookup"><span data-stu-id="12279-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="12279-382">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-383">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="12279-384">別名</span><span class="sxs-lookup"><span data-stu-id="12279-384">Aliasing</span></span>
<span data-ttu-id="12279-385">現在讓我們來擴充 hello 上述範例與明確的別名的值。</span><span class="sxs-lookup"><span data-stu-id="12279-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="12279-386">因為是 hello 關鍵字用於別名。</span><span class="sxs-lookup"><span data-stu-id="12279-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="12279-387">它是選擇性的投影出 hello 做為第二個值時顯示`NameInfo`。</span><span class="sxs-lookup"><span data-stu-id="12279-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="12279-388">萬一查詢有兩個屬性，以 hello 相同的名稱，別名必須是一或兩個 hello 屬性，因此它們會明確地區分 hello 投影中使用的 toorename 結果。</span><span class="sxs-lookup"><span data-stu-id="12279-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="12279-389">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-390">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="12279-391">純量運算式</span><span class="sxs-lookup"><span data-stu-id="12279-391">Scalar expressions</span></span>
<span data-ttu-id="12279-392">此外 tooproperty 參考、 hello SELECT 子句也支援純量運算式，例如常數、 算術運算式、 邏輯運算式等等。例如，以下是簡單 "Hello World" 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="12279-393">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="12279-394">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="12279-395">以下是使用純量運算式的較複雜範例。</span><span class="sxs-lookup"><span data-stu-id="12279-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="12279-396">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="12279-397">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="12279-398">在下列範例的 hello，hello hello 純量運算式的結果會是布林值。</span><span class="sxs-lookup"><span data-stu-id="12279-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="12279-399">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="12279-400">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="12279-401">物件和陣列建立</span><span class="sxs-lookup"><span data-stu-id="12279-401">Object and array creation</span></span>
<span data-ttu-id="12279-402">DocumentDB API SQL 的另一個重要功能是建立陣列/物件。</span><span class="sxs-lookup"><span data-stu-id="12279-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="12279-403">在 hello 前一個範例中，請注意，我們會建立新的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="12279-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="12279-404">同樣地，其中也可以建構陣列 hello 遵循範例所示：</span><span class="sxs-lookup"><span data-stu-id="12279-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="12279-405">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="12279-406">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="12279-407"><a id="ValueKeyword"></a>VALUE 關鍵字</span><span class="sxs-lookup"><span data-stu-id="12279-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="12279-408">hello**值**關鍵字，可提供方式 tooreturn JSON 值。</span><span class="sxs-lookup"><span data-stu-id="12279-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="12279-409">例如，如下所示傳回 hello 純量 hello 查詢`"Hello World"`而不是`{$1: "Hello World"}`。</span><span class="sxs-lookup"><span data-stu-id="12279-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="12279-410">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="12279-411">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="12279-412">hello 下列查詢會傳回不使用 hello hello JSON 值`"address"`hello 結果中的標籤。</span><span class="sxs-lookup"><span data-stu-id="12279-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="12279-413">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="12279-414">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="12279-415">hello 下列範例將擴充此 tooshow 如何 tooreturn JSON 基本值 （hello JSON 樹狀結構的 hello 分葉層級）。</span><span class="sxs-lookup"><span data-stu-id="12279-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="12279-416">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="12279-417">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="12279-418">* 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-418">* Operator</span></span>
<span data-ttu-id="12279-419">hello 特殊運算子 （*） 是支援的 tooproject hello 文件集是。</span><span class="sxs-lookup"><span data-stu-id="12279-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="12279-420">使用時，它必須只 hello 投射的欄位。</span><span class="sxs-lookup"><span data-stu-id="12279-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="12279-421">`SELECT * FROM Families f` 之類的查詢有效，`SELECT VALUE * FROM Families f ` 和 `SELECT *, f.id FROM Families f ` 則無效。</span><span class="sxs-lookup"><span data-stu-id="12279-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="12279-422">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="12279-423">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="12279-424"><a id="TopKeyword"></a>TOP 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="12279-425">hello TOP 關鍵字可以用 toolimit hello 數目查詢的值。</span><span class="sxs-lookup"><span data-stu-id="12279-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="12279-426">當 TOP 與 hello ORDER BY 子句一起使用時，hello 結果集是有限的 toohello 第 n 個已排序的值;否則，它會傳回 hello 第 n 個結果中未定義的順序。</span><span class="sxs-lookup"><span data-stu-id="12279-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="12279-427">最佳做法，在 SELECT 陳述式，一律使用 ORDER BY 子句與 hello TOP 子句。</span><span class="sxs-lookup"><span data-stu-id="12279-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="12279-428">這是 hello toopredictably 指出哪些資料列受到 TOP 的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="12279-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="12279-429">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="12279-430">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="12279-431">TOP 可以與常數值 (如上所示) 或使用參數化查詢的變數值搭配使用 。</span><span class="sxs-lookup"><span data-stu-id="12279-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="12279-432">如需詳細資訊，請參閱下方的參數化查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="12279-433"><a id="Aggregates"></a>彙總函式</span><span class="sxs-lookup"><span data-stu-id="12279-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="12279-434">您也可以執行彙總中 hello`SELECT`子句。</span><span class="sxs-lookup"><span data-stu-id="12279-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="12279-435">彙總函式會執行一組值的計算，然後傳回單一值。</span><span class="sxs-lookup"><span data-stu-id="12279-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="12279-436">例如，hello 下列查詢會傳回 hello 集合內的家族文件的 hello 的計數。</span><span class="sxs-lookup"><span data-stu-id="12279-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="12279-437">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="12279-438">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="12279-439">您也可以傳回 hello hello 純量值彙總使用 hello`VALUE`關鍵字。</span><span class="sxs-lookup"><span data-stu-id="12279-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="12279-440">比方說，hello 下列查詢會傳回值的 hello 計數以單一數字：</span><span class="sxs-lookup"><span data-stu-id="12279-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="12279-441">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="12279-442">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="12279-443">您也可以搭配篩選器執行彙總。</span><span class="sxs-lookup"><span data-stu-id="12279-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="12279-444">例如，hello 下列查詢會傳回文件以 hello 位址 hello 的計數 hello 華盛頓州。</span><span class="sxs-lookup"><span data-stu-id="12279-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="12279-445">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="12279-446">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="12279-447">hello 下表顯示 hello 清單支援的彙總函式在 DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="12279-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="12279-448">`SUM` 和 `AVG` 是對數值執行，而 `COUNT`、`MIN`和 `MAX` 則可對數字、字串、布林值和 null 執行。</span><span class="sxs-lookup"><span data-stu-id="12279-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="12279-449">使用量</span><span class="sxs-lookup"><span data-stu-id="12279-449">Usage</span></span> | <span data-ttu-id="12279-450">說明</span><span class="sxs-lookup"><span data-stu-id="12279-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="12279-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="12279-451">COUNT</span></span> | <span data-ttu-id="12279-452">傳回 hello hello 運算式中的項目數。</span><span class="sxs-lookup"><span data-stu-id="12279-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="12279-453">SUM</span><span class="sxs-lookup"><span data-stu-id="12279-453">SUM</span></span>   | <span data-ttu-id="12279-454">傳回 hello hello 運算式中的所有 hello 值的總和。</span><span class="sxs-lookup"><span data-stu-id="12279-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="12279-455">最小值</span><span class="sxs-lookup"><span data-stu-id="12279-455">MIN</span></span>   | <span data-ttu-id="12279-456">傳回 hello hello 運算式中的最小值。</span><span class="sxs-lookup"><span data-stu-id="12279-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="12279-457">最大值</span><span class="sxs-lookup"><span data-stu-id="12279-457">MAX</span></span>   | <span data-ttu-id="12279-458">傳回 hello hello 運算式中的最大值。</span><span class="sxs-lookup"><span data-stu-id="12279-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="12279-459">平均</span><span class="sxs-lookup"><span data-stu-id="12279-459">AVG</span></span>   | <span data-ttu-id="12279-460">傳回 hello hello 運算式中的 hello 值的平均值。</span><span class="sxs-lookup"><span data-stu-id="12279-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="12279-461">也可在 hello 結果陣列反覆項目上執行彙總。</span><span class="sxs-lookup"><span data-stu-id="12279-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="12279-462">如需詳細資訊，請參閱[查詢中的陣列反覆運算](#Iteration)。</span><span class="sxs-lookup"><span data-stu-id="12279-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="12279-463">當使用 hello Azure 入口網站查詢總管時，請注意，彙總查詢中可能傳回 hello 部分彙總的結果查詢 頁面。</span><span class="sxs-lookup"><span data-stu-id="12279-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="12279-464">hello Sdk 會產生單一的累計值，所有頁面。</span><span class="sxs-lookup"><span data-stu-id="12279-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="12279-465">為了 tooperform 彙總查詢，使用程式碼，您需要.NET SDK 1.12.0、.NET Core SDK 1.1.0 或 Java SDK 1.9.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="12279-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="12279-466"><a id="OrderByClause"></a>ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="12279-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="12279-467">像是在 ANSI SQL 中，您可以在查詢時包含選擇性的 Order By 子句。</span><span class="sxs-lookup"><span data-stu-id="12279-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="12279-468">hello 子句可以包含選擇性 ASC/DESC 引數 toospecify hello 訂單結果必須擷取。</span><span class="sxs-lookup"><span data-stu-id="12279-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="12279-469">例如，以下是擷取系列中的 hello 常駐城市名稱順序的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="12279-470">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="12279-471">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="12279-472">以下是系列中的建立日期以數字代表 hello epoch 時間，也就是，經過時間 1970 年 1 月 1，以秒為單位儲存的順序會擷取的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="12279-473">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="12279-474">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="12279-475"><a id="Advanced"></a>進階資料庫概念和 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="12279-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="12279-476"><a id="Iteration"></a>反覆運算</span><span class="sxs-lookup"><span data-stu-id="12279-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="12279-477">新建構加入透過 hello **IN** DocumentDB API SQL tooprovide 支援逐一查看 JSON 陣列中的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="12279-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="12279-478">hello FROM 來源反覆項目提供支援。</span><span class="sxs-lookup"><span data-stu-id="12279-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="12279-479">讓我們開始 hello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="12279-479">Let's start with hello following example:</span></span>

<span data-ttu-id="12279-480">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="12279-481">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="12279-482">現在讓我們看看另一個查詢，透過 hello 集合中的子系執行反覆項目。</span><span class="sxs-lookup"><span data-stu-id="12279-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="12279-483">請注意 hello 輸出陣列中的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="12279-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="12279-484">此範例會將`children`和 hello 結果扁平化單一陣列。</span><span class="sxs-lookup"><span data-stu-id="12279-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="12279-485">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="12279-486">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="12279-487">這可以進一步使用的 toofilter hello 陣列 hello 下列範例所示的每個個別項目：</span><span class="sxs-lookup"><span data-stu-id="12279-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="12279-488">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="12279-489">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="12279-490">您也可以透過 hello 結果陣列反覆項目執行彙總。</span><span class="sxs-lookup"><span data-stu-id="12279-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="12279-491">例如，hello 下列查詢會計算 hello 子系之間的所有家族數目。</span><span class="sxs-lookup"><span data-stu-id="12279-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="12279-492">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="12279-493">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="12279-494"><a id="Joins"></a>聯結</span><span class="sxs-lookup"><span data-stu-id="12279-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="12279-495">在關聯式資料庫中，在資料表之間的 hello 需要 toojoin 很重要。</span><span class="sxs-lookup"><span data-stu-id="12279-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="12279-496">它的 hello 正規化的推論 toodesigning 邏輯結構描述。</span><span class="sxs-lookup"><span data-stu-id="12279-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="12279-497">反對 toothis，DocumentDB API 處理 hello 非正規化的資料模型的無結構描述的文件。</span><span class="sxs-lookup"><span data-stu-id="12279-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="12279-498">這是 hello 的邏輯對等的 「 自我聯結 」。</span><span class="sxs-lookup"><span data-stu-id="12279-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="12279-499">hello 語言支援的 hello 語法為 < from_source1 > 聯結 < from_source2 > 聯結...JOIN <from_sourceN>。</span><span class="sxs-lookup"><span data-stu-id="12279-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="12279-500">整體而言，這會傳回一組 **N**-Tuple (具有 **N** 個值的 Tuple)。</span><span class="sxs-lookup"><span data-stu-id="12279-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="12279-501">每個 Tuple 所擁有的值，都是將所有集合別名在其個別集合上反覆運算所產生。</span><span class="sxs-lookup"><span data-stu-id="12279-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="12279-502">換句話說，這是參與 hello 聯結 hello 集合的完整交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="12279-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="12279-503">hello 下列範例顯示 hello JOIN 子句的運作方式。</span><span class="sxs-lookup"><span data-stu-id="12279-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="12279-504">在下列範例的 hello，hello 結果是空的因為 hello 交叉乘積，每份文件從來源和空的集合是空的。</span><span class="sxs-lookup"><span data-stu-id="12279-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="12279-505">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="12279-506">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="12279-507">在下列範例的 hello，hello 聯結是 hello 文件根與 hello 之間`children`subroot。</span><span class="sxs-lookup"><span data-stu-id="12279-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="12279-508">它是兩個 JSON 物件之間的交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="12279-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="12279-509">因為我們處理 hello 子陣列的單一根節點，便無法生效 hello 聯結中子系是陣列的 hello 事實。</span><span class="sxs-lookup"><span data-stu-id="12279-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="12279-510">因此 hello 結果會包含只有兩個結果，因為 hello 交叉乘積，每份文件以 hello 陣列會產生剛好只有一個文件。</span><span class="sxs-lookup"><span data-stu-id="12279-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="12279-511">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="12279-512">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="12279-513">下列範例中的 hello 顯示傳統聯結：</span><span class="sxs-lookup"><span data-stu-id="12279-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="12279-514">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="12279-515">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="12279-516">hello 首先 toonote 為該 hello`from_source`的 hello**聯結**子句是迭代器。</span><span class="sxs-lookup"><span data-stu-id="12279-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="12279-517">因此，hello 流程在此情況下，如下所示如下：</span><span class="sxs-lookup"><span data-stu-id="12279-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="12279-518">展開每一個子項目**c** hello 陣列中。</span><span class="sxs-lookup"><span data-stu-id="12279-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="12279-519">套用 hello 根 hello 文件的交叉乘積**f**每個子項目與**c** ，已扁平化 hello 第一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="12279-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="12279-520">最後，專案 hello 根物件**f** name 單獨的屬性。</span><span class="sxs-lookup"><span data-stu-id="12279-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="12279-521">hello 第一個文件 (`AndersenFamily`) 只包含一個子元素，所以 hello 結果集包含只有單一物件對應 toothis 文件。</span><span class="sxs-lookup"><span data-stu-id="12279-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="12279-522">hello 第二個文件 (`WakefieldFamily`) 包含兩個子系。</span><span class="sxs-lookup"><span data-stu-id="12279-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="12279-523">因此，hello 交叉乘積會產生不同的物件供每個子系，藉此產生兩個物件，其中每個子對應 toothis 文件中。</span><span class="sxs-lookup"><span data-stu-id="12279-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="12279-524">在這些文件中的欄位 hello 根 hello 相同，就像您會預期中的交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="12279-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="12279-525">hello hello 聯結的實際公用程式是從 hello 交叉乘積中的圖形，否則為 tooform tuple tooproject 困難。</span><span class="sxs-lookup"><span data-stu-id="12279-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="12279-526">此外，我們看到在 hello 面範例中，您可以篩選的 tuple 的 hello 組合 hello，可讓使用者選擇整體的 hello tuple 符合條件。</span><span class="sxs-lookup"><span data-stu-id="12279-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="12279-527">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="12279-528">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="12279-529">這個範例是前面範例中，hello 的自然擴充功能，並執行兩個聯結。</span><span class="sxs-lookup"><span data-stu-id="12279-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="12279-530">因此，hello 交叉乘積可視為 hello 下列虛擬程式碼：</span><span class="sxs-lookup"><span data-stu-id="12279-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="12279-531">`AndersenFamily` 有一個小孩養了一隻寵物。</span><span class="sxs-lookup"><span data-stu-id="12279-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="12279-532">因此，hello 交叉乘積會產生一個資料列 (1\*1\*1) 從這一系列。</span><span class="sxs-lookup"><span data-stu-id="12279-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="12279-533">不過，WakefieldFamily 有兩個小孩，但只有一個小孩 "Jesse" 養了多隻寵物。</span><span class="sxs-lookup"><span data-stu-id="12279-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="12279-534">Jesse 有兩隻寵物。</span><span class="sxs-lookup"><span data-stu-id="12279-534">Jesse has two pets though.</span></span> <span data-ttu-id="12279-535">因此 hello 交叉乘積產生 1\*1\*2 = 2 此系列中的資料列。</span><span class="sxs-lookup"><span data-stu-id="12279-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="12279-536">在 hello 下一個範例中，沒有額外的篩選`pet`。</span><span class="sxs-lookup"><span data-stu-id="12279-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="12279-537">這不包括所有 hello tuple hello 隻寵物的名字不 「 陰影 」。</span><span class="sxs-lookup"><span data-stu-id="12279-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="12279-538">請注意，我們會從陣列中，任何 hello tuple 的 hello 項篩選無法 toobuild tuple，以及專案 hello 項目的任何組合。</span><span class="sxs-lookup"><span data-stu-id="12279-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="12279-539">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="12279-540">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="12279-541"><a id="JavaScriptIntegration"></a>JavaScript 整合</span><span class="sxs-lookup"><span data-stu-id="12279-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="12279-542">Azure Cosmos DB 預存程序和觸發程序方面的 hello 集合上直接執行 JavaScript 為基礎的應用程式邏輯提供程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="12279-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="12279-543">這允許：</span><span class="sxs-lookup"><span data-stu-id="12279-543">This allows for both:</span></span>

* <span data-ttu-id="12279-544">查詢中的 JavaScript 執行階段，直接在 hello 資料庫引擎內的 hello 深層整合必定集合的文件和能力 toodo 高效能交易 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="12279-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="12279-545">將控制流程、變數範圍限制、指派以及例外狀況處理基本類型與資料庫交易的整合自然模型化。</span><span class="sxs-lookup"><span data-stu-id="12279-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="12279-546">如需 Azure Cosmos DB 支援 JavaScript 整合的詳細資訊，請參閱 toohello JavaScript 伺服器端程式設計文件。</span><span class="sxs-lookup"><span data-stu-id="12279-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="12279-547"><a id="UserDefinedFunctions"></a>使用者定義函式 (UDF)</span><span class="sxs-lookup"><span data-stu-id="12279-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="12279-548">Hello 已在這份文件中定義的型別，以及 DocumentDB API SQL 支援使用者定義函數 (UDF)。</span><span class="sxs-lookup"><span data-stu-id="12279-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="12279-549">特別是，純量 Udf 支援 hello 開發人員可以傳入零或多個引數並傳回單一引數結果回其中。</span><span class="sxs-lookup"><span data-stu-id="12279-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="12279-550">系統會檢查所有這些引數是否為合法的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="12279-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="12279-551">hello DocumentDB API SQL 語法已擴充，使用這些使用者定義函式的 toosupport 自訂應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="12279-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="12279-552">您可以向 DocumentDB API 註冊 UDF，然後在 SQL 查詢中參照它。</span><span class="sxs-lookup"><span data-stu-id="12279-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="12279-553">事實上，Udf 是 exquisitely hello 設計 toobe 查詢所叫用。</span><span class="sxs-lookup"><span data-stu-id="12279-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="12279-554">做為推論 toothis 的選擇，Udf 不含存取 toohello 內容物件的 hello 其他 JavaScript 有型別 （預存程序和觸發程序）。</span><span class="sxs-lookup"><span data-stu-id="12279-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="12279-555">因為查詢是以唯讀形式執行，所以可以在主要或次要複本上執行。</span><span class="sxs-lookup"><span data-stu-id="12279-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="12279-556">因此，Udf 是設計的 toorun 不像其他的 JavaScript 類型的次要複本上。</span><span class="sxs-lookup"><span data-stu-id="12279-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="12279-557">以下是如何在 hello Cosmos DB 之下的資料庫，特別是文件集合可以註冊 UDF 的範例。</span><span class="sxs-lookup"><span data-stu-id="12279-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="12279-558">hello 上述範例會建立的 UDF，其名稱是`REGEX_MATCH`。</span><span class="sxs-lookup"><span data-stu-id="12279-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="12279-559">它接受兩個的 JSON 字串值`input`和`pattern`和檢查，如果第二個 hello hello 模式中指定 hello 第一個相符項目使用 JavaScript 的 string.match() 函式。</span><span class="sxs-lookup"><span data-stu-id="12279-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="12279-560">我們現在可以在投射的查詢中使用此 UDF。</span><span class="sxs-lookup"><span data-stu-id="12279-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="12279-561">Udf 必須限定 hello 區分大小寫的前置詞"udf。 」</span><span class="sxs-lookup"><span data-stu-id="12279-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="12279-562">(當從查詢內呼叫時)。</span><span class="sxs-lookup"><span data-stu-id="12279-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="12279-563">先前 too3/17/2015，Cosmos DB 支援 UDF 呼叫沒有 hello"udf。 」</span><span class="sxs-lookup"><span data-stu-id="12279-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="12279-564">例如 SELECT REGEX_MATCH()。</span><span class="sxs-lookup"><span data-stu-id="12279-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="12279-565">這種呼叫模式已被取代。</span><span class="sxs-lookup"><span data-stu-id="12279-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="12279-566">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="12279-567">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="12279-568">hello UDF 也可以用在篩選內 hello 面範例中，也限定 hello"udf。 」 中所示</span><span class="sxs-lookup"><span data-stu-id="12279-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="12279-569">前置詞來限定：</span><span class="sxs-lookup"><span data-stu-id="12279-569">prefix:</span></span>

<span data-ttu-id="12279-570">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="12279-571">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="12279-572">在本質上，UDF 是有效的純量運算式，而且可以用於投射和篩選。</span><span class="sxs-lookup"><span data-stu-id="12279-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="12279-573">tooexpand hello 電源的 Udf 時，讓我們看看另一個範例使用條件式邏輯：</span><span class="sxs-lookup"><span data-stu-id="12279-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="12279-574">以下是範例，練習 hello UDF。</span><span class="sxs-lookup"><span data-stu-id="12279-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="12279-575">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="12279-576">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="12279-577">如 hello 上述範例展示，Udf 整合 hello 電源的 JavaScript 語言 hello DocumentDB API SQL tooprovide 非常豐富的可程式化介面 toodo 複雜程序、 條件式邏輯與 hello 的內建 JavaScript 執行階段的說明功能。</span><span class="sxs-lookup"><span data-stu-id="12279-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="12279-578">DocumentDB API SQL 提供 hello 引數 toohello Udf hello 來源中的每份文件在 hello 目前 （WHERE 子句或 SELECT 子句） 的階段處理 hello UDF。</span><span class="sxs-lookup"><span data-stu-id="12279-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="12279-579">hello 結果就會合併在順暢地 hello 整體執行管線。</span><span class="sxs-lookup"><span data-stu-id="12279-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="12279-580">如果 hello 屬性參照的 tooby hello UDF 參數不適用於 hello JSON 值 hello 參數會被視為未定義，並因此 hello UDF 引動過程會完全略過。</span><span class="sxs-lookup"><span data-stu-id="12279-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="12279-581">同樣地 hello hello UDF 未定義的結果，如果它不是包含 hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="12279-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="12279-582">總而言之，Udf 是 hello 查詢一部分的絕佳工具 toodo 複雜的商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="12279-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="12279-583">運算子評估</span><span class="sxs-lookup"><span data-stu-id="12279-583">Operator evaluation</span></span>
<span data-ttu-id="12279-584">Cosmos DB hello virtue 的 JSON 資料庫所繪製 parallels 與 JavaScript 運算子和評估語意。</span><span class="sxs-lookup"><span data-stu-id="12279-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="12279-585">雖然 Cosmos DB 嘗試 toopreserve JavaScript 語意 JSON 支援方面，hello 作業評估偏差在某些情況下。</span><span class="sxs-lookup"><span data-stu-id="12279-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="12279-586">在 DocumentDB API SQL 中，不同於傳統的 SQL 中 hello 類型的值通常之前，無法得知會從資料庫擷取 hello 值。</span><span class="sxs-lookup"><span data-stu-id="12279-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="12279-587">順序 tooefficiently 中執行查詢，大部分的 hello 運算子有嚴格的型別需求。</span><span class="sxs-lookup"><span data-stu-id="12279-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="12279-588">與 JavaScript 不同，DocumentDB API SQL 並不會執行隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="12279-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="12279-589">例如，類似 `SELECT * FROM Person p WHERE p.Age = 21` 的查詢會針對包含 Age 屬性且值為 21 的文件進行比對。</span><span class="sxs-lookup"><span data-stu-id="12279-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="12279-590">任何其他 Age 屬性符合字串 "21" 或其他可能之無限制變化 (例如 "021"、"21.0"、"0021"、"00021" 等等) 的文件，則不會成為比對的結果。</span><span class="sxs-lookup"><span data-stu-id="12279-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="12279-591">相反地，這是 toohello JavaScript hello 字串值的隱含轉換 toonumbers (根據運算子，例如: = =)。</span><span class="sxs-lookup"><span data-stu-id="12279-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="12279-592">這項選擇對 DocumentDB API SQL 中有效率的索引比對十分重要。</span><span class="sxs-lookup"><span data-stu-id="12279-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="12279-593">參數化 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="12279-593">Parameterized SQL queries</span></span>
<span data-ttu-id="12279-594">Cosmos DB 支援查詢參數以 hello 熟悉 @ 表示法來表示。</span><span class="sxs-lookup"><span data-stu-id="12279-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="12279-595">參數化 SQL 提供使用者輸入的健全處理和逸出，防止透過 SQL 插入式意外洩露資料。</span><span class="sxs-lookup"><span data-stu-id="12279-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="12279-596">比方說，您可以撰寫查詢，將姓氏和地址 (州) 做為參數，然後根據使用者輸入，使用各種不同姓氏和地址 (州) 的值執行查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="12279-597">此要求可以傳送 tooCosmos DB 做為參數化的 JSON 查詢類似如下所示。</span><span class="sxs-lookup"><span data-stu-id="12279-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="12279-598">hello 引數 tooTOP 可以設定使用參數化的查詢類似如下所示。</span><span class="sxs-lookup"><span data-stu-id="12279-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="12279-599">參數值可以是任何有效的 JSON (字串、數字、布林值、null，甚至是陣列或巢狀 JSON)。</span><span class="sxs-lookup"><span data-stu-id="12279-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="12279-600">此外，由於 Cosmos DB 並無結構描述，因此系統不會對照任何類型來驗證參數。</span><span class="sxs-lookup"><span data-stu-id="12279-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="12279-601"><a id="BuiltinFunctions"></a>內建函數</span><span class="sxs-lookup"><span data-stu-id="12279-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="12279-602">Cosmos DB 也支援一些適用於一般作業的內建函式，這些函式可在像是使用者定義函式 (UDF) 之類的查詢內使用。</span><span class="sxs-lookup"><span data-stu-id="12279-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="12279-603">函式群組</span><span class="sxs-lookup"><span data-stu-id="12279-603">Function group</span></span>          | <span data-ttu-id="12279-604">作業</span><span class="sxs-lookup"><span data-stu-id="12279-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="12279-605">數學函數</span><span class="sxs-lookup"><span data-stu-id="12279-605">Mathematical functions</span></span>  | <span data-ttu-id="12279-606">ABS、CEILING、EXP、FLOOR、LOG、LOG10、POWER、ROUND、SIGN、SQRT、SQUARE、TRUNC、ACOS、ASIN、ATAN、ATN2、COS、COT、DEGREES、PI、RADIANS、SIN 和 TAN</span><span class="sxs-lookup"><span data-stu-id="12279-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="12279-607">類型檢查函數</span><span class="sxs-lookup"><span data-stu-id="12279-607">Type checking functions</span></span> | <span data-ttu-id="12279-608">IS_ARRAY、IS_BOOL、IS_NULL、IS_NUMBER、IS_OBJECT、IS_STRING、IS_DEFINED 和 IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="12279-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="12279-609">字串函數</span><span class="sxs-lookup"><span data-stu-id="12279-609">String functions</span></span>        | <span data-ttu-id="12279-610">CONCAT、CONTAINS、ENDSWITH、INDEX_OF、LEFT、LENGTH、LOWER、LTRIM、REPLACE、REPLICATE、REVERSE、RIGHT、RTRIM、STARTSWITH、SUBSTRING 和 UPPER</span><span class="sxs-lookup"><span data-stu-id="12279-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="12279-611">陣列函數</span><span class="sxs-lookup"><span data-stu-id="12279-611">Array functions</span></span>         | <span data-ttu-id="12279-612">ARRAY_CONCAT、ARRAY_CONTAINS、ARRAY_LENGTH 和 ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="12279-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="12279-613">空間函數</span><span class="sxs-lookup"><span data-stu-id="12279-613">Spatial functions</span></span>       | <span data-ttu-id="12279-614">ST_DISTANCE、ST_WITHIN、ST_INTERSECTS、ST_ISVALID 和 ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="12279-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="12279-615">如果您目前使用的使用者定義的函數 (UDF) 已可使用內建函式，您就應該使用 hello 對應內建函式，為即將 toobe 快速 toorun 以及其他更多有效。</span><span class="sxs-lookup"><span data-stu-id="12279-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="12279-616">數學函數</span><span class="sxs-lookup"><span data-stu-id="12279-616">Mathematical functions</span></span>
<span data-ttu-id="12279-617">hello 數學函數會執行計算，根據輸入值會作為引數，且傳回數字的值。</span><span class="sxs-lookup"><span data-stu-id="12279-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="12279-618">以下是支援的內建數學函數資料表。</span><span class="sxs-lookup"><span data-stu-id="12279-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="12279-619">使用量</span><span class="sxs-lookup"><span data-stu-id="12279-619">Usage</span></span> | <span data-ttu-id="12279-620">說明</span><span class="sxs-lookup"><span data-stu-id="12279-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="12279-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="12279-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="12279-622">傳回 hello 絕對 （正） 值 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="12279-624">傳回 hello 最小整數值大於或等於，hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="12279-626">傳回小於 hello 最大整數 toohello 或等於指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="12279-628">傳回 hello 指數的 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="12279-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="12279-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="12279-630">傳回 hello 自然對數的 hello 指定數值運算式，或是使用 hello hello 對數指定基底</span><span class="sxs-lookup"><span data-stu-id="12279-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="12279-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="12279-632">傳回 hello 基底 10 對數值 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="12279-634">傳回數值，捨入的 toohello 最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="12279-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="12279-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="12279-636">傳回數值，截斷的 toohello 最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="12279-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="12279-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="12279-638">傳回 hello 平方根 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="12279-640">傳回 hello 方形的 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="12279-642">指定了數值運算式 toohello 值指定傳回 hello 冪 hello。</span><span class="sxs-lookup"><span data-stu-id="12279-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="12279-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="12279-644">傳回 hello 號 （-1，0，1） 的值 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="12279-646">傳回 hello 的角度，以弧度為單位，它的餘弦為 hello 指定數值運算式。也稱為反餘弦值。</span><span class="sxs-lookup"><span data-stu-id="12279-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="12279-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="12279-648">傳回 hello 的角度，以弧度為單位，其正弦值為 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="12279-649">這也稱為反正弦值。</span><span class="sxs-lookup"><span data-stu-id="12279-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="12279-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="12279-651">傳回 hello 的角度，以弧度為單位，其正切為 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="12279-652">這也稱為反正切值。</span><span class="sxs-lookup"><span data-stu-id="12279-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="12279-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="12279-654">傳回 hello hello 正數 x 軸與 hello 光線從 hello toohello 原點 （y，x） 之間，弧度的角度，其中 x 和 y 是兩個指定的浮點運算式的 hello hello 值。</span><span class="sxs-lookup"><span data-stu-id="12279-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="12279-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="12279-656">傳回 hello 三角餘弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="12279-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="12279-658">傳回 hello 三角餘切函數 hello 指定旋轉的角度，以弧度為單位，在 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="12279-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="12279-660">傳回 hello 以度為單位的角度以弧度為單位指定的對應角度。</span><span class="sxs-lookup"><span data-stu-id="12279-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="12279-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="12279-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="12279-662">傳回 hello PI 的常數值。</span><span class="sxs-lookup"><span data-stu-id="12279-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="12279-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="12279-664">當您輸入數值運算式 (以度為單位) 時，傳回弧度。</span><span class="sxs-lookup"><span data-stu-id="12279-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="12279-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="12279-666">傳回 hello 三角正弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="12279-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="12279-668">傳回 hello 正切 hello 輸入運算式，hello 中指定的運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="12279-669">例如，您現在可以執行類似 hello 下列查詢：</span><span class="sxs-lookup"><span data-stu-id="12279-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="12279-670">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="12279-671">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-671">**Results**</span></span>

    [4]

<span data-ttu-id="12279-672">hello Cosmos DB 函式比較 tooANSI SQL 之間的主要差異在於它們是設計的 toowork 與無結構描述和混合的結構描述資料。</span><span class="sxs-lookup"><span data-stu-id="12279-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="12279-673">比方說，如果您有的文件，其中 hello 大小屬性遺漏，或非數值像 「 不明 」，然後 hello 文件會透過，略過而不是傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="12279-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="12279-674">類型檢查函數</span><span class="sxs-lookup"><span data-stu-id="12279-674">Type checking functions</span></span>
<span data-ttu-id="12279-675">hello 類型檢查函數可讓您 toocheck hello SQL 查詢中運算式型別。</span><span class="sxs-lookup"><span data-stu-id="12279-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="12279-676">類型檢查函數可以在變數或未知時，使用 hello 立即 toodetermine hello 類型的文件內的屬性。</span><span class="sxs-lookup"><span data-stu-id="12279-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="12279-677">以下是支援的內建類型檢查函數資料表。</span><span class="sxs-lookup"><span data-stu-id="12279-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="12279-678"><strong>用法</strong></span><span class="sxs-lookup"><span data-stu-id="12279-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="12279-679"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="12279-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-681">傳回布林值，指出是否 hello hello 值型別陣列。</span><span class="sxs-lookup"><span data-stu-id="12279-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-683">傳回布林值，指出是否 hello hello 值型別布林值。</span><span class="sxs-lookup"><span data-stu-id="12279-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-685">傳回布林值，指出 hello hello 值型別是否為 null。</span><span class="sxs-lookup"><span data-stu-id="12279-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-687">傳回布林值，指出是否 hello hello 值型別數字。</span><span class="sxs-lookup"><span data-stu-id="12279-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-689">傳回布林值，指出是否 hello hello 值型別一個 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="12279-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-691">傳回布林值，指出是否 hello hello 值型別為字串。</span><span class="sxs-lookup"><span data-stu-id="12279-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-693">傳回布林值，指出如果 hello 尚未指派屬性值。</span><span class="sxs-lookup"><span data-stu-id="12279-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="12279-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="12279-695">傳回布林值，指出是否 hello hello 值類型字串、 數字、 布林值或 null。</span><span class="sxs-lookup"><span data-stu-id="12279-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="12279-696">使用這些函式，您現在可以執行類似 hello 下列查詢：</span><span class="sxs-lookup"><span data-stu-id="12279-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="12279-697">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="12279-698">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="12279-699">字串函數</span><span class="sxs-lookup"><span data-stu-id="12279-699">String functions</span></span>
<span data-ttu-id="12279-700">hello 下列純量函數的字串輸入值來執行作業並傳回字串、 數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="12279-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="12279-701">以下是內建字串函數的資料表：</span><span class="sxs-lookup"><span data-stu-id="12279-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="12279-702">使用量</span><span class="sxs-lookup"><span data-stu-id="12279-702">Usage</span></span> | <span data-ttu-id="12279-703">說明</span><span class="sxs-lookup"><span data-stu-id="12279-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="12279-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="12279-705">指定字串運算式的字元為單位的 hello 傳回 hello 數目</span><span class="sxs-lookup"><span data-stu-id="12279-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="12279-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="12279-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="12279-707">傳回字串 hello 因產生的串連兩個或多個字串值。</span><span class="sxs-lookup"><span data-stu-id="12279-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="12279-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="12279-709">傳回字串運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="12279-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="12279-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="12279-711">傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個</span><span class="sxs-lookup"><span data-stu-id="12279-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="12279-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="12279-713">傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個</span><span class="sxs-lookup"><span data-stu-id="12279-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="12279-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="12279-715">傳回布林值，指出是否 hello 第一個字串運算式中第二個包含 hello。</span><span class="sxs-lookup"><span data-stu-id="12279-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="12279-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="12279-717">傳回開始 hello 內 hello 第一個指定的字串運算式，則為-1 hello 第二個字串運算式的第一次出現的位置，如果找不到 hello 字串 hello。</span><span class="sxs-lookup"><span data-stu-id="12279-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="12279-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="12279-719">傳回 hello 字串的左側的組件以 hello 指定字元數。</span><span class="sxs-lookup"><span data-stu-id="12279-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="12279-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="12279-721">傳回 hello 權限屬於字串 hello 與指定字元的數。</span><span class="sxs-lookup"><span data-stu-id="12279-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="12279-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="12279-723">傳回移除開頭空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="12279-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="12279-725">傳回截斷所有結尾空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="12279-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="12279-727">傳回將大寫字元資料 toolowercase 轉換後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="12279-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="12279-729">傳回將小寫字元資料 toouppercase 轉換後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="12279-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="12279-731">使用其他字串值取代指定的字串值的所有項目。</span><span class="sxs-lookup"><span data-stu-id="12279-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="12279-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="12279-733">將字串值重複指定的次數。</span><span class="sxs-lookup"><span data-stu-id="12279-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="12279-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="12279-735">傳回字串值的 hello 反向順序。</span><span class="sxs-lookup"><span data-stu-id="12279-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="12279-736">使用這些函式，您現在可以執行類似 hello 下列查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="12279-737">例如，您可以傳回 hello 系列名稱以大寫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="12279-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="12279-738">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="12279-739">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="12279-740">或串連字串，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="12279-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="12279-741">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="12279-742">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="12279-743">字串函式也可用在 hello 其中子句 toofilter 結果，如同下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="12279-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="12279-744">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="12279-745">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="12279-746">陣列函數</span><span class="sxs-lookup"><span data-stu-id="12279-746">Array functions</span></span>
<span data-ttu-id="12279-747">下列純量函數的 hello 執行作業陣列輸入的值和傳回數值、 布林值或陣列值。</span><span class="sxs-lookup"><span data-stu-id="12279-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="12279-748">以下是內建陣列函數的資料表：</span><span class="sxs-lookup"><span data-stu-id="12279-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="12279-749">使用量</span><span class="sxs-lookup"><span data-stu-id="12279-749">Usage</span></span> | <span data-ttu-id="12279-750">說明</span><span class="sxs-lookup"><span data-stu-id="12279-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="12279-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="12279-752">傳回 hello 項目數的 hello 指定陣列運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="12279-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="12279-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="12279-754">傳回陣列，其中是 hello 結果串連兩個以上陣列值。</span><span class="sxs-lookup"><span data-stu-id="12279-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="12279-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="12279-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="12279-756">傳回布林值，指出 hello 陣列中是否包含 hello 指定的值。</span><span class="sxs-lookup"><span data-stu-id="12279-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="12279-757">可以指定完整或部分，是否才 hello 比對。</span><span class="sxs-lookup"><span data-stu-id="12279-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="12279-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="12279-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="12279-759">傳回陣列運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="12279-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="12279-760">陣列的函式可使用的 toomanipulate 陣列在 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="12279-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="12279-761">例如，以下是其中 hello 父系的其中一個是 「 循環配置資源 Wakefield"會傳回所有文件的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="12279-762">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="12279-763">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="12279-764">您可以指定相符的項目 hello 陣列中的部分片段。</span><span class="sxs-lookup"><span data-stu-id="12279-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="12279-765">hello 下列查詢會尋找所有父系使用 hello`givenName`的`Robin`。</span><span class="sxs-lookup"><span data-stu-id="12279-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="12279-766">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="12279-767">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="12279-768">以下是另一個範例，其使用 ARRAY_LENGTH tooget hello 每個系列的子系數目。</span><span class="sxs-lookup"><span data-stu-id="12279-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="12279-769">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="12279-770">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="12279-771">空間函數</span><span class="sxs-lookup"><span data-stu-id="12279-771">Spatial functions</span></span>
<span data-ttu-id="12279-772">Cosmos DB 支援 hello 下列開放式地理空間協會 (OGC) 的地理空間查詢內建函式。</span><span class="sxs-lookup"><span data-stu-id="12279-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="12279-773"><strong>用法</strong></span><span class="sxs-lookup"><span data-stu-id="12279-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="12279-774"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="12279-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-775">ST_DISTANCE (point_expr、point_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="12279-776">傳回兩個 hello GeoJSON 點、 多邊形或 LineString 運算式之間的 hello 距離。</span><span class="sxs-lookup"><span data-stu-id="12279-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-777">ST_WITHIN (point_expr、polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="12279-778">傳回指示 hello 第一個 GeoJSON 物件 （點、 多邊形或 LineString） 是否在 hello 第二個 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="12279-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="12279-780">傳回指出是否要交叉 hello 兩個指定的 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="12279-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="12279-782">傳回布林值，指出 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式是否有效。</span><span class="sxs-lookup"><span data-stu-id="12279-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="12279-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="12279-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="12279-784">傳回包含布林值，如果 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式的 JSON 值有效，而且如果無效，此外 hello 原因，表示為字串值。</span><span class="sxs-lookup"><span data-stu-id="12279-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="12279-785">空間函式可使用的 tooperform 鄰近查詢空間資料。</span><span class="sxs-lookup"><span data-stu-id="12279-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="12279-786">例如，以下是 hello 的可傳回所有的系列文件，30 公里內指定的位置使用 hello ST_DISTANCE 內建函式的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="12279-787">**查詢**</span><span class="sxs-lookup"><span data-stu-id="12279-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="12279-788">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="12279-789">如需有關 Cosmos DB 中的地理空間支援詳細資料，請參閱[使用 Azure Cosmos DB 中的地理空間資料](geospatial.md)。</span><span class="sxs-lookup"><span data-stu-id="12279-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="12279-790">Cosmos db 包裝空間的函式和 hello SQL 語法。</span><span class="sxs-lookup"><span data-stu-id="12279-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="12279-791">現在讓我們看看如何 LINQ 查詢的運作方式以及它如何與 hello 語法互動我們看到了到目前為止。</span><span class="sxs-lookup"><span data-stu-id="12279-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="12279-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="12279-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="12279-793">LINQ 是一種 .NET 程式設計模型，此模型會將運算表示為對物件串流的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="12279-794">Cosmos DB 藉由使用 LINQ 的用戶端程式庫 toointerface 促進 JSON 和.NET 物件之間的轉換，並從 LINQ 子集的對應查詢 tooCosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="12279-795">hello 下圖顯示 hello 架構支援使用 Cosmos DB LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="12279-796">使用 hello Cosmos DB 用戶端，開發人員可以建立**IQueryable**物件直接查詢 hello Cosmos DB 查詢提供者，然後會將 hello LINQ 查詢轉譯成 Cosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="12279-797">hello 查詢然後會以 JSON 格式傳遞 toohello Cosmos DB 伺服器 tooretrieve 一組結果。</span><span class="sxs-lookup"><span data-stu-id="12279-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="12279-798">hello 傳回結果為已還原序列化成資料流，hello 用戶端上的.NET 物件。</span><span class="sxs-lookup"><span data-stu-id="12279-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![使用 DocumentDB API 來支援 LINQ 查詢的架構：SQL 語法、JSON 查詢語言、資料庫概念及 SQL 查詢][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="12279-800">.NET 和 JSON 對應</span><span class="sxs-lookup"><span data-stu-id="12279-800">.NET and JSON mapping</span></span>
<span data-ttu-id="12279-801">為自然階層 hello.NET 物件和 JSON 文件之間的對應-對應每個資料成員欄位 tooa JSON 物件，其中是 hello 欄位名稱對應 toohello 「 金鑰 」 部分 hello 物件和 hello 「 值 」 組件是以遞迴方式對應 toohello 值 hello 物件一部分。</span><span class="sxs-lookup"><span data-stu-id="12279-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="12279-802">請考慮下列範例中的 hello: hello 系列物件建立對應的 toohello JSON 文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="12279-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="12279-803">且反之亦然，hello JSON 文件對應的反向 tooa.NET 物件。</span><span class="sxs-lookup"><span data-stu-id="12279-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="12279-804">**C# 類別**</span><span class="sxs-lookup"><span data-stu-id="12279-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="12279-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="12279-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a><span data-ttu-id="12279-806">LINQ tooSQL 轉譯</span><span class="sxs-lookup"><span data-stu-id="12279-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="12279-807">hello Cosmos DB 查詢提供者從 LINQ 查詢執行最佳的投入時間對應到 Cosmos DB SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="12279-808">在下列描述 hello，我們假設 hello 讀者具備 「 基本的認識 LINQ。</span><span class="sxs-lookup"><span data-stu-id="12279-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="12279-809">首先，hello 型別系統，我們支援所有 JSON 基本型別 – 數值類型、 布林值、 字串和 null。</span><span class="sxs-lookup"><span data-stu-id="12279-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="12279-810">只支援這些 JSON 類型。</span><span class="sxs-lookup"><span data-stu-id="12279-810">Only these JSON types are supported.</span></span> <span data-ttu-id="12279-811">下列純量運算式的 hello 支援。</span><span class="sxs-lookup"><span data-stu-id="12279-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="12279-812">常值-將常數值的 hello 基本資料類型包括次 hello hello 查詢都會進行評估。</span><span class="sxs-lookup"><span data-stu-id="12279-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="12279-813">屬性/陣列索引運算式 – 這些運算式參考物件或陣列元素 toohello 的屬性。</span><span class="sxs-lookup"><span data-stu-id="12279-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="12279-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span><span class="sxs-lookup"><span data-stu-id="12279-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="12279-815">算術運算式：這些包括數值和布林值的一般算術運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="12279-816">Hello 完整清單，請參閱 toohello SQL 規格。</span><span class="sxs-lookup"><span data-stu-id="12279-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="12279-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="12279-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="12279-818">字串比較運算式-這些包括比較字串值 toosome 常數字串值。</span><span class="sxs-lookup"><span data-stu-id="12279-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="12279-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span><span class="sxs-lookup"><span data-stu-id="12279-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="12279-820">物件/陣列建立運算式：這些運算式傳回複合值類型或匿名類型的物件，或是這類物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="12279-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="12279-821">這些值可以是巢狀值。</span><span class="sxs-lookup"><span data-stu-id="12279-821">These values can be nested.</span></span>
  
     <span data-ttu-id="12279-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //含有兩個欄位的匿名類型</span><span class="sxs-lookup"><span data-stu-id="12279-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="12279-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="12279-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="12279-824"><a id="SupportedLinqOperators"></a>支援的 LINQ 運算子清單</span><span class="sxs-lookup"><span data-stu-id="12279-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="12279-825">以下是支援的 LINQ 運算子 hello LINQ 提供者隨附 hello DocumentDB.NET SDK 中的清單。</span><span class="sxs-lookup"><span data-stu-id="12279-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="12279-826">**選取**： 投影轉譯 toohello SQL SELECT 包括物件建構</span><span class="sxs-lookup"><span data-stu-id="12279-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="12279-827">**其中**： 轉譯 toohello SQL WHERE，篩選器，並支援之間轉譯 & &、 | | 和 ！</span><span class="sxs-lookup"><span data-stu-id="12279-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="12279-828">toohello SQL 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-828">toohello SQL operators</span></span>
* <span data-ttu-id="12279-829">**SelectMany**： 可讓陣列 toohello SQL JOIN 子句的回溯。</span><span class="sxs-lookup"><span data-stu-id="12279-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="12279-830">可以是陣列項目上的使用的 toochain/巢狀運算式 toofilter</span><span class="sxs-lookup"><span data-stu-id="12279-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="12279-831">**OrderBy 和 OrderByDescending**： 轉譯 tooORDER BY 遞增/遞減</span><span class="sxs-lookup"><span data-stu-id="12279-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="12279-832">彙總的 **Count**、**Sum**、**Min**、**Max** 與 **Average** 運算子，以及其非同步對應項 **CountAsync**、**SumAsync**、**MinAsync**、**MaxAsync** 與 **AverageAsync**。</span><span class="sxs-lookup"><span data-stu-id="12279-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="12279-833">**CompareTo**： 轉譯 toorange 比較。</span><span class="sxs-lookup"><span data-stu-id="12279-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="12279-834">通常用於字串，因為字串在 .NET 中是無法比較的</span><span class="sxs-lookup"><span data-stu-id="12279-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="12279-835">**採取**： 轉譯 toohello SQL TOP 來限制查詢結果</span><span class="sxs-lookup"><span data-stu-id="12279-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="12279-836">**數學函式**： 支援從轉譯。網路的 Abs，Acos、 Asin、 Atan、 Ceiling、 Cos、 Exp、 Floor、 記錄、 Log10、 Pow、 循、 符號、 Sin、 Sqrt、 Tan、 截斷 toohello 對等 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="12279-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="12279-837">**字串函數**： 支援從轉譯。網路的 Concat、 Contains、 EndsWith、 IndexOf、 計數、 ToLower、 TrimStart、 取代、 反向、 TrimEnd、 StartsWith、 子字串，ToUpper toohello 對等 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="12279-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="12279-838">**陣列函數**： 支援從轉譯。網路的 Concat、 Contains 和計數 toohello 對等 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="12279-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="12279-839">**Geospatial 擴充函式**： 支援從虛設常式方法距離內 IsValid、 轉譯和 IsValidDetailed toohello 對等 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="12279-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="12279-840">**使用者定義函式延伸模組函數**： 支援轉譯 hello 從虛設常式方法 UserDefinedFunctionProvider.Invoke toohello 對應使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="12279-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="12279-841">**其他**: hello 的轉譯聯合的支援和條件式運算子。</span><span class="sxs-lookup"><span data-stu-id="12279-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="12279-842">可以翻譯 Contains tooString CONTAINS、 ARRAY_CONTAINS 或 hello SQL 中的，視內容而定。</span><span class="sxs-lookup"><span data-stu-id="12279-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="12279-843">SQL 查詢運算子</span><span class="sxs-lookup"><span data-stu-id="12279-843">SQL query operators</span></span>
<span data-ttu-id="12279-844">以下是一些範例，說明如何某些 hello 標準 LINQ 查詢運算子轉譯 tooCosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="12279-845">Select 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-845">Select Operator</span></span>
<span data-ttu-id="12279-846">hello 語法`input.Select(x => f(x))`，其中`f`是純量運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="12279-847">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="12279-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="12279-849">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="12279-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="12279-851">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="12279-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="12279-853">SelectMany 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-853">SelectMany operator</span></span>
<span data-ttu-id="12279-854">hello 語法`input.SelectMany(x => f(x))`，其中`f`是傳回的集合類型的純量運算式。</span><span class="sxs-lookup"><span data-stu-id="12279-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="12279-855">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="12279-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="12279-857">Where 運算子</span><span class="sxs-lookup"><span data-stu-id="12279-857">Where operator</span></span>
<span data-ttu-id="12279-858">hello 語法`input.Where(x => f(x))`，其中`f`是純量運算式，它會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="12279-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="12279-859">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="12279-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="12279-861">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="12279-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="12279-863">複合 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="12279-863">Composite SQL queries</span></span>
<span data-ttu-id="12279-864">hello 上方運算子可以是組成的 tooform 功能更強大的查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="12279-865">由於 Cosmos DB 支援巢狀的集合，hello 組合可以串連或巢狀。</span><span class="sxs-lookup"><span data-stu-id="12279-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="12279-866">串連</span><span class="sxs-lookup"><span data-stu-id="12279-866">Concatenation</span></span>
<span data-ttu-id="12279-867">hello 語法`input(.|.SelectMany())(.Select()|.Where())*`。</span><span class="sxs-lookup"><span data-stu-id="12279-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="12279-868">串連查詢的開頭可以是選用的 `SelectMany` 查詢，其後接著多個 `Select` 或 `Where` 運算子。</span><span class="sxs-lookup"><span data-stu-id="12279-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="12279-869">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="12279-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="12279-871">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="12279-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="12279-873">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="12279-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="12279-875">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="12279-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="12279-877">巢狀</span><span class="sxs-lookup"><span data-stu-id="12279-877">Nesting</span></span>
<span data-ttu-id="12279-878">hello 語法`input.SelectMany(x=>x.Q())`其中 Q 是`Select`， `SelectMany`，或`Where`運算子。</span><span class="sxs-lookup"><span data-stu-id="12279-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="12279-879">在巢狀查詢中，hello 內部查詢是套用的 tooeach hello 外部集合項目。</span><span class="sxs-lookup"><span data-stu-id="12279-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="12279-880">有一個重要功能是該 hello 內部查詢可以參考 toohello 欄位 hello 集合中的元素 hello 外部像自我聯結。</span><span class="sxs-lookup"><span data-stu-id="12279-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="12279-881">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="12279-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="12279-883">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="12279-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="12279-885">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="12279-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="12279-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="12279-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="12279-887"><a id="ExecutingSqlQueries"></a>執行 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="12279-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="12279-888">Cosmos DB 公開資源的方式是透過 REST API，任何能夠發出 HTTP/HTTPS 要求的語言都可呼叫此 API。</span><span class="sxs-lookup"><span data-stu-id="12279-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="12279-889">此外，Cosmos DB 還為數種熱門語言 (例如 .NET、Node.js、JavaScript 和 Python) 提供程式設計程式庫。</span><span class="sxs-lookup"><span data-stu-id="12279-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="12279-890">hello REST API 和 hello 所有的各種程式庫支援透過 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="12279-891">hello.NET SDK 支援 LINQ 查詢此外 tooSQL。</span><span class="sxs-lookup"><span data-stu-id="12279-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="12279-892">hello 下列範例顯示如何 toocreate 查詢並將它送出針對 Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="12279-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="12279-893"><a id="RestAPI"></a>REST API</span><span class="sxs-lookup"><span data-stu-id="12279-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="12279-894">Cosmos DB 提供透過 HTTP 的開放 RESTful 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="12279-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="12279-895">可以使用 Azure 訂用帳戶佈建資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="12279-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="12279-896">hello Cosmos DB 資源模型包含一組帳戶資料庫，每一個都是可使用的邏輯與穩定 URI 定址的資源。</span><span class="sxs-lookup"><span data-stu-id="12279-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="12279-897">一組資源是參照的 tooas 本文件摘要。</span><span class="sxs-lookup"><span data-stu-id="12279-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="12279-898">資料庫帳戶包含一組資料庫，而每個資料庫都包含多個集合，且各集合因此會包含文件、UDF 和其他資源類型。</span><span class="sxs-lookup"><span data-stu-id="12279-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="12279-899">hello 基本互動模型，這些資源是透過 hello HTTP 動詞命令 GET、 PUT、 POST 和 DELETE 與標準解譯。</span><span class="sxs-lookup"><span data-stu-id="12279-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="12279-900">hello POST 動詞命令用來建立新的資源、 執行預存程序或發出 Cosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="12279-901">查詢一律是唯讀作業，而且沒有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="12279-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="12279-902">hello 下列範例顯示 DocumentDB API 查詢對集合，其中包含 hello 兩份範例文件到目前為止已檢閱過的文章。</span><span class="sxs-lookup"><span data-stu-id="12279-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="12279-903">hello 查詢會有一個簡單的篩選 hello JSON 名稱屬性上。</span><span class="sxs-lookup"><span data-stu-id="12279-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="12279-904">請記下的 hello hello 使用`x-ms-documentdb-isquery`和內容類型： `application/query+json` hello 作業的標頭 toodenote 是查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="12279-905">**要求**</span><span class="sxs-lookup"><span data-stu-id="12279-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="12279-906">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="12279-907">hello 第二個範例示範更複雜的查詢會傳回從 hello 聯結的多個結果。</span><span class="sxs-lookup"><span data-stu-id="12279-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="12279-908">**要求**</span><span class="sxs-lookup"><span data-stu-id="12279-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="12279-909">**結果**</span><span class="sxs-lookup"><span data-stu-id="12279-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="12279-910">如果查詢的結果無法納入單一頁面的結果，則 hello REST API 會傳回接續 token，透過 hello`x-ms-continuation-token`回應標頭。</span><span class="sxs-lookup"><span data-stu-id="12279-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="12279-911">用戶端可以對結果分頁中後續的結果包含 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="12279-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="12279-912">每個分頁結果的 hello 數目也可以透過 hello`x-ms-max-item-count`標頭。</span><span class="sxs-lookup"><span data-stu-id="12279-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="12279-913">如果 hello 指定的查詢的彙總函式類似`COUNT`，然後 hello 查詢頁面可能傳回的結果 hello 頁面部分彙總的值。</span><span class="sxs-lookup"><span data-stu-id="12279-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="12279-914">hello 用戶端必須透過這些結果 tooproduce hello 最終結果，例如執行第二個層級彙總、 加總 hello 傳回 hello 個別頁面 tooreturn hello 總計數的計數。</span><span class="sxs-lookup"><span data-stu-id="12279-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="12279-915">查詢，使用 hello toomanage hello 資料一致性原則`x-ms-consistency-level`REST API 的所有要求標頭。</span><span class="sxs-lookup"><span data-stu-id="12279-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="12279-916">工作階段一致性，就需要的 tooalso 回應 hello 最新`x-ms-session-token`hello 查詢要求的 Cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="12279-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="12279-917">hello 查詢的集合的編製索引原則可能也會影響查詢結果的 hello 一致性。</span><span class="sxs-lookup"><span data-stu-id="12279-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="12279-918">Hello 預設檢索原則設定，針對集合 hello 索引一定是目前與 hello 文件內容和查詢結果符合 hello 選擇資料的一致性。</span><span class="sxs-lookup"><span data-stu-id="12279-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="12279-919">如果 hello 檢索原則是比較不嚴謹的 tooLazy，查詢可以傳回過時的結果。</span><span class="sxs-lookup"><span data-stu-id="12279-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="12279-920">如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級][consistency-levels]。</span><span class="sxs-lookup"><span data-stu-id="12279-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="12279-921">如果設定的 hello hello 集合上的編製索引原則無法支援 hello 指定的查詢，hello Azure Cosmos DB 伺服器就會傳回 400 「 不正確的要求 」。</span><span class="sxs-lookup"><span data-stu-id="12279-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="12279-922">針對範圍查詢 (針對雜湊 (相等) 查閱所設定的路徑) 以及明確地排除不進行編製索引的路徑，會傳回此訊息。</span><span class="sxs-lookup"><span data-stu-id="12279-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="12279-923">hello`x-ms-documentdb-query-enable-scan`標頭無法使用索引時，可以是指定的 tooallow hello 查詢 tooperform 掃描。</span><span class="sxs-lookup"><span data-stu-id="12279-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="12279-924">您也可以設定於查詢執行取得詳細的度量`x-ms-documentdb-populatequerymetrics`標頭太`True`。</span><span class="sxs-lookup"><span data-stu-id="12279-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="12279-925">如需詳細資訊，請參閱[適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢計量](documentdb-sql-query-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="12279-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="12279-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="12279-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="12279-927">hello.NET SDK 支援 LINQ 和 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="12279-928">hello 下列範例顯示如何 tooperform hello 簡單的篩選條件查詢早導入這份文件。</span><span class="sxs-lookup"><span data-stu-id="12279-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="12279-929">此範例會比較每個文件內的兩個屬性是否相等，以及使用匿名投射。</span><span class="sxs-lookup"><span data-stu-id="12279-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="12279-930">hello 下一個範例顯示聯結，透過 LINQ SelectMany 表示。</span><span class="sxs-lookup"><span data-stu-id="12279-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="12279-931">hello.NET 用戶端自動逐一查看查詢結果，如上所示的 hello foreach 區塊中的所有 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="12279-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="12279-932">hello 查詢 hello REST API > 一節中導入的選項也會出現在 hello.NET SDK 使用 hello`FeedOptions`和`FeedResponse`hello CreateDocumentQuery 方法中的類別。</span><span class="sxs-lookup"><span data-stu-id="12279-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="12279-933">可以使用 hello 控制 hello 頁數`MaxItemCount`設定。</span><span class="sxs-lookup"><span data-stu-id="12279-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="12279-934">您可以建立，以同時也可以明確控制分頁`IDocumentQueryable`使用 hello`IQueryable`物件，然後藉由讀取` ResponseContinuationToken`值並將其傳遞回為`RequestContinuationToken`中`FeedOptions`。</span><span class="sxs-lookup"><span data-stu-id="12279-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="12279-935">`EnableScanInQuery`可設定 tooenable 掃描 hello 查詢無法支援所設定的 hello 編製索引原則時。</span><span class="sxs-lookup"><span data-stu-id="12279-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="12279-936">對於資料分割的集合，您可以使用`PartitionKey`toorun hello 查詢針對單一資料分割 （雖然 Cosmos DB 可以自動擷取此從 hello 查詢文字），和`EnableCrossPartitionQuery`toorun 查詢可能需要 toobe 執行多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="12279-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="12279-937">請參閱太[Azure Cosmos DB 的.NET 範例](https://github.com/Azure/azure-documentdb-net)如需其他範例包含查詢。</span><span class="sxs-lookup"><span data-stu-id="12279-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="12279-938"><a id="JavaScriptServerSideApi"></a>JavaScript 伺服器端 API</span><span class="sxs-lookup"><span data-stu-id="12279-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="12279-939">Cosmos DB 提供程式設計模型使用預存程序和觸發程序的 hello 集合上直接執行 JavaScript 為基礎的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="12279-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="12279-940">hello JavaScript 邏輯在集合層級註冊可以再發出 hello 文件的指定集合的 hello hello 作業的資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="12279-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="12279-941">這些作業會包裝在環境 ACID 交易中。</span><span class="sxs-lookup"><span data-stu-id="12279-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="12279-942">hello 下列範例示範如何在 hello JavaScript 伺服器 API toomake toouse hello queryDocuments 查詢從內部預存程序和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="12279-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="12279-943"><a id="References"></a>參考</span><span class="sxs-lookup"><span data-stu-id="12279-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="12279-944">[簡介 tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="12279-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="12279-945">Azure Cosmos DB SQL 規格</span><span class="sxs-lookup"><span data-stu-id="12279-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="12279-946">Azure Cosmos DB .NET 範例</span><span class="sxs-lookup"><span data-stu-id="12279-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="12279-947">[Azure Cosmos DB 一致性層級][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="12279-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="12279-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="12279-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="12279-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="12279-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="12279-950">Javascript 規格 [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="12279-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="12279-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="12279-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="12279-952">大型資料庫的查詢評估技術 [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="12279-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="12279-953">平行關聯式資料庫系統中的查詢處理 (IEEE Computer Society Press，1994 年)</span><span class="sxs-lookup"><span data-stu-id="12279-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="12279-954">Lu, Ooi, Tan, 平行關聯式資料庫系統中的查詢處理 (IEEE Computer Society Press，1994 年)。</span><span class="sxs-lookup"><span data-stu-id="12279-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="12279-955">Christopher Olston、Benjamin Reed、Utkarsh Srivastava、Ravi Kumar、Andrew Tomkins：Pig Latin：資料處理的 Not-So-Foreign 語言，SIGMOD 2008。</span><span class="sxs-lookup"><span data-stu-id="12279-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="12279-956">G.</span><span class="sxs-lookup"><span data-stu-id="12279-956">G.</span></span> <span data-ttu-id="12279-957">Graefe。</span><span class="sxs-lookup"><span data-stu-id="12279-957">Graefe.</span></span> <span data-ttu-id="12279-958">hello 串聯，聯集的架構，會在查詢最佳化。</span><span class="sxs-lookup"><span data-stu-id="12279-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="12279-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="12279-959">IEEE Data Eng.</span></span> <span data-ttu-id="12279-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="12279-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md