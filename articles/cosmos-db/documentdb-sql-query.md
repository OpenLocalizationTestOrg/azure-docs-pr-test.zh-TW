---
title: "適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢 | Microsoft Docs"
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
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="67eef-105">適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="67eef-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="67eef-106">Microsoft Azure Cosmos DB 支援使用 SQL (結構化查詢語言) 作為 JSON 查詢語言來查詢文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="67eef-107">Cosmos DB 確實無結構描述。</span><span class="sxs-lookup"><span data-stu-id="67eef-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="67eef-108">由於它是直接在資料庫引擎內使用 JSON 資料模型，因此它提供不需明確的結構描述或建立次要索引，即可自動編製 JSON 文件索引的功能。</span><span class="sxs-lookup"><span data-stu-id="67eef-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="67eef-109">為 Cosmos DB 設計查詢語言時，我們心中懷有兩個目標：</span><span class="sxs-lookup"><span data-stu-id="67eef-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="67eef-110">我們想要支援 SQL，而不是發明新的 JSON 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="67eef-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="67eef-111">SQL 是一種最熟悉且熱門的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="67eef-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="67eef-112">Cosmos DB SQL 提供一個正式的程式設計模型，可在 JSON 文件上進行豐富的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="67eef-113">由於 JSON 文件資料庫可以直接在資料庫引擎中執行 JavaScript，因此，我們想要使用 JavaScript 的程式設計模型做為查詢語言的基礎。</span><span class="sxs-lookup"><span data-stu-id="67eef-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="67eef-114">DocumentDB API SQL 是以 JavaScript 的類型系統、運算式評估和函數叫用為基礎。</span><span class="sxs-lookup"><span data-stu-id="67eef-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="67eef-115">這除了其他功能之外，還進而提供自然程式設計模型來進行關聯式投射、跨 JSON 文件的階層式導覽、自我聯結、空間查詢，以及叫用完全以 JavaScript 撰寫的使用者定義函式 (UDF)。</span><span class="sxs-lookup"><span data-stu-id="67eef-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="67eef-116">我們相信這些功能的重點是減少應用程式與資料庫之間的摩擦，而且對開發人員的生產力而言十分重要。</span><span class="sxs-lookup"><span data-stu-id="67eef-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="67eef-117">建議您透過觀看下列影片 (影片中 Aravind Ramachandran 會示範 Cosmos DB 的查詢功能)，以及瀏覽我們的 [Query Playground (查詢遊樂場)](http://www.documentdb.com/sql/demo) (您可以在其中試試 Cosmos DB，並對我們的資料集執行 SQL 查詢)，來開始著手。</span><span class="sxs-lookup"><span data-stu-id="67eef-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="67eef-118">接著再回到本文，我們會從 SQL 查詢教學課程開始，帶領您演練一些簡易的 JSON 文件和 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="67eef-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="67eef-119"><a id="GettingStarted"></a>開始在 Cosmos DB 中使用 SQL 命令</span><span class="sxs-lookup"><span data-stu-id="67eef-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="67eef-120">為了查看 Cosmos DB SQL 如何運作，讓我們從一些簡單的 JSON 文件開始著手，然後對其逐步執行一些簡單的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="67eef-121">請考慮有關兩個家族的這兩份 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="67eef-122">使用 Cosmos DB 時，我們不需要明確地建立任何結構描述或次要索引。</span><span class="sxs-lookup"><span data-stu-id="67eef-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="67eef-123">我們只需要將 JSON 文件插入到 Cosmos DB 集合中，再接著進行查詢即可。</span><span class="sxs-lookup"><span data-stu-id="67eef-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="67eef-124">這裡有 Andersen 一家的簡單 JSON 文件，包括這一家的父母、孩子 (以及寵物)、地址及註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="67eef-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="67eef-125">這份文件包含字串、數字、布林值、陣列和巢狀屬性。</span><span class="sxs-lookup"><span data-stu-id="67eef-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="67eef-126">**文件**</span><span class="sxs-lookup"><span data-stu-id="67eef-126">**Document**</span></span>  

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

<span data-ttu-id="67eef-127">以下是第二份具有些微差異的文件：使用 `givenName` 和 `familyName` 來取代 `firstName` 和 `lastName`。</span><span class="sxs-lookup"><span data-stu-id="67eef-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="67eef-128">**文件**</span><span class="sxs-lookup"><span data-stu-id="67eef-128">**Document**</span></span>  

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

<span data-ttu-id="67eef-129">現在，讓我們嘗試對此資料執行一些查詢，以了解 DocumentDB API SQL 的一些重要部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="67eef-130">例如，下列查詢會傳回 id 欄位符合 `AndersenFamily` 的文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="67eef-131">因為它是 `SELECT *`，所以查詢的輸出是完整 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="67eef-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="67eef-132">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-133">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-133">**Results**</span></span>

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


<span data-ttu-id="67eef-134">現在，請考慮我們需要以不同形式來重新格式化 JSON 輸出的情況。</span><span class="sxs-lookup"><span data-stu-id="67eef-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="67eef-135">當地址所在城市的名稱與省/市的名稱相同時，此查詢會投射具有兩個所選欄位 (Name 和 City) 的新 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="67eef-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="67eef-136">在此情況下，"NY, NY" 相符。</span><span class="sxs-lookup"><span data-stu-id="67eef-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="67eef-137">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="67eef-138">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="67eef-139">下一個查詢會傳回家族中所有指定小孩的名稱，該家族的 id 符合依據居住城市所排序的 `WakefieldFamily` 。</span><span class="sxs-lookup"><span data-stu-id="67eef-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="67eef-140">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="67eef-141">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="67eef-142">我們想要透過目前所看到的範例來指出 Cosmos DB 查詢語言的一些重要部分：</span><span class="sxs-lookup"><span data-stu-id="67eef-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="67eef-143">因為 DocumentDB API SQL 的處理對象是 JSON 值，所以它處理的是樹狀形式的實體，而不是資料列和資料行。</span><span class="sxs-lookup"><span data-stu-id="67eef-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="67eef-144">因此，此語言可讓您參考樹狀目錄中任意深度的節點 (例如 `Node1.Node2.Node3…..Nodem`)，該節點與參考 `<table>.<column>` 之兩個部分參考的關聯式 SQL 類似。</span><span class="sxs-lookup"><span data-stu-id="67eef-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="67eef-145">結構化查詢語言可處理無結構描述資料。</span><span class="sxs-lookup"><span data-stu-id="67eef-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="67eef-146">因此，需要動態繫結類型系統。</span><span class="sxs-lookup"><span data-stu-id="67eef-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="67eef-147">相同的運算式可能會對不同的文件產生不同的類型。</span><span class="sxs-lookup"><span data-stu-id="67eef-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="67eef-148">查詢的結果會是有效的 JSON 值，但不保證會是固定的結構描述。</span><span class="sxs-lookup"><span data-stu-id="67eef-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="67eef-149">Cosmos DB 只支援嚴謹的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="67eef-150">這表示類型系統和運算式只能處理 JSON 類型。</span><span class="sxs-lookup"><span data-stu-id="67eef-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="67eef-151">如需詳細資料，請參閱 [JSON 規格](http://www.json.org/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="67eef-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="67eef-152">Cosmos DB 集合是 JSON 文件的無結構描述容器。</span><span class="sxs-lookup"><span data-stu-id="67eef-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="67eef-153">集合中文件內及跨文件之資料實體中的關係，會由內含項目以隱含方式擷取，而不是由主索引鍵和外部索引鍵關係擷取。</span><span class="sxs-lookup"><span data-stu-id="67eef-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="67eef-154">這是本文稍後討論之文件內聯結中值得指出的重要部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="67eef-155"><a id="Indexing"></a> Cosmos DB 索引編製</span><span class="sxs-lookup"><span data-stu-id="67eef-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="67eef-156">進入 DocumentDB API SQL 語法之前，有必要先探索 Cosmos DB 的索引設計。</span><span class="sxs-lookup"><span data-stu-id="67eef-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="67eef-157">資料庫索引的目的是要在使用最少資源 (例如 CPU、輸入/輸出) 的情況下，以各種方式提供查詢，同時兼顧良好的輸送量和低延遲。</span><span class="sxs-lookup"><span data-stu-id="67eef-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="67eef-158">通常，選擇適用於資料庫查詢的正確索引需要經過相當的規劃和實驗。</span><span class="sxs-lookup"><span data-stu-id="67eef-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="67eef-159">此方式對資料不符合嚴謹結構描述的無結構描述資料庫而言是種挑戰，而且發展十分迅速。</span><span class="sxs-lookup"><span data-stu-id="67eef-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="67eef-160">因此，我們在設計 Cosmos DB 索引子系統時，設定了下列目標：</span><span class="sxs-lookup"><span data-stu-id="67eef-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="67eef-161">在不需要結構描述的情況下，對文件編製索引：索引子系統不需要任何結構描述資訊，或提出任何文件結構描述的相關假設。</span><span class="sxs-lookup"><span data-stu-id="67eef-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="67eef-162">支援有效率、豐富階層式及關聯式查詢：索引可有效率地支援 Cosmos DB 查詢語言，包括支援階層式和關聯式投射。</span><span class="sxs-lookup"><span data-stu-id="67eef-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="67eef-163">支援在面對持續大量寫入時進行一致查詢：在面對持續大量寫入時，針對具有一致查詢的高寫入輸送量工作負載，會以累加、有效率及線上方式更新索引。</span><span class="sxs-lookup"><span data-stu-id="67eef-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="67eef-164">一致的索引更新對於提供一致性層級的查詢十分重要，在此層級中是由使用者設定文件服務。</span><span class="sxs-lookup"><span data-stu-id="67eef-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="67eef-165">支援多重租用：由於是使用保留型模型進行跨租用戶的資源控管，因此會在為每一複本配置的系統資源 (CPU、記憶體，以及每秒的輸入/輸出作業) 預算內執行索引更新。</span><span class="sxs-lookup"><span data-stu-id="67eef-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="67eef-166">儲存體效率：基於成本效益，索引的磁碟儲存體額外負荷有所限制且可預測。</span><span class="sxs-lookup"><span data-stu-id="67eef-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="67eef-167">這十分重要，因為 Cosmos DB 允許開發人員在索引額外負荷與查詢效能之間做出成本取捨。</span><span class="sxs-lookup"><span data-stu-id="67eef-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="67eef-168">如需示範如何為集合設定索引編製原則的範例，請參閱 MSDN 上的 [Azure Cosmos DB 範例 (英文)](https://github.com/Azure/azure-documentdb-net)。</span><span class="sxs-lookup"><span data-stu-id="67eef-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="67eef-169">現在，讓我們深入討論 Azure Cosmos DB SQL 語法。</span><span class="sxs-lookup"><span data-stu-id="67eef-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="67eef-170"><a id="Basics"></a>Azure Cosmos DB SQL 查詢的基本概念</span><span class="sxs-lookup"><span data-stu-id="67eef-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="67eef-171">根據 ANSI-SQL 標準，每個查詢都會包含 SELECT 子句以及選擇性的 FROM 和 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="67eef-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="67eef-172">針對每個查詢，通常都會列舉 FROM 子句中的來源。</span><span class="sxs-lookup"><span data-stu-id="67eef-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="67eef-173">接著，會對來源套用 WHERE 子句中的篩選，以擷取 JSON 文件的子集。</span><span class="sxs-lookup"><span data-stu-id="67eef-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="67eef-174">最後，使用 SELECT 子句來投射選取清單中所要求的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="67eef-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="67eef-175"><a id="FromClause"></a>FROM 子句</span><span class="sxs-lookup"><span data-stu-id="67eef-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="67eef-176">除非稍後會在查詢中篩選或投射來源，否則 `FROM <from_specification>` 子句為選用子句。</span><span class="sxs-lookup"><span data-stu-id="67eef-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="67eef-177">此子句的目的是指定查詢必須操作的資料來源。</span><span class="sxs-lookup"><span data-stu-id="67eef-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="67eef-178">整個集合通常是來源，但是您可以改為指定集合的子集。</span><span class="sxs-lookup"><span data-stu-id="67eef-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="67eef-179">類似 `SELECT * FROM Families` 的查詢指出整個 Families 集合是要列舉的來源。</span><span class="sxs-lookup"><span data-stu-id="67eef-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="67eef-180">可使用特殊識別碼 ROOT 來代表此集合，而不使用集合名稱。</span><span class="sxs-lookup"><span data-stu-id="67eef-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="67eef-181">下列清單包含會針對每個查詢強制執行的規則：</span><span class="sxs-lookup"><span data-stu-id="67eef-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="67eef-182">集合可以進行別名處理，例如 `SELECT f.id FROM Families AS f` 或只是 `SELECT f.id FROM Families f`。</span><span class="sxs-lookup"><span data-stu-id="67eef-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="67eef-183">此處的 `f` 即等於 `Families`。</span><span class="sxs-lookup"><span data-stu-id="67eef-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="67eef-184">`AS` 是對識別碼進行別名處理的選用關鍵字。</span><span class="sxs-lookup"><span data-stu-id="67eef-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="67eef-185">進行別名處理之後，就無法繫結原始來源。</span><span class="sxs-lookup"><span data-stu-id="67eef-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="67eef-186">例如， `SELECT Families.id FROM Families f` 在語句構造上無效，因為無法再解析識別碼 "Families"。</span><span class="sxs-lookup"><span data-stu-id="67eef-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="67eef-187">所有需要參照的屬性都必須是完整的。</span><span class="sxs-lookup"><span data-stu-id="67eef-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="67eef-188">如果未遵循嚴謹的結構描述，則會強制執行以避免任何模糊的繫結。</span><span class="sxs-lookup"><span data-stu-id="67eef-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="67eef-189">因此，`SELECT id FROM Families f` 在語句構造上無效，因為不會繫結屬性 `id`。</span><span class="sxs-lookup"><span data-stu-id="67eef-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="67eef-190">子文件</span><span class="sxs-lookup"><span data-stu-id="67eef-190">Subdocuments</span></span>
<span data-ttu-id="67eef-191">來源也可以減少為更小的子集。</span><span class="sxs-lookup"><span data-stu-id="67eef-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="67eef-192">例如，若只要列舉每份文件中的樹狀子目錄，則子根目錄可能會變成來源 (如下列範例所示)：</span><span class="sxs-lookup"><span data-stu-id="67eef-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="67eef-193">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="67eef-194">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-194">**Results**</span></span>  

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

<span data-ttu-id="67eef-195">雖然上述範例使用陣列作為來源，但物件也可用來作為來源，即下列範例中顯示的內容：可在來源中找到的任何有效的 JSON 值 (已定義的)，均會被視為查詢結果中的包含項目。</span><span class="sxs-lookup"><span data-stu-id="67eef-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="67eef-196">如果有些家族沒有 `address.state` 值，則會在查詢結果中予以排除。</span><span class="sxs-lookup"><span data-stu-id="67eef-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="67eef-197">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="67eef-198">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="67eef-199"><a id="WhereClause"></a>WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="67eef-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="67eef-200">WHERE 子句 (**`WHERE <filter_condition>`**) 是選用的。</span><span class="sxs-lookup"><span data-stu-id="67eef-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="67eef-201">它會指定條件，而且來源所提供的 JSON 文件必須滿足這些條件才能併入為結果的一部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="67eef-202">任何 JSON 文件都必須將指定的條件評估為 "true"，才能視為結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="67eef-203">索引層使用 WHERE 子句，來判斷可為結果一部分的來源文件的絕對最小子集。</span><span class="sxs-lookup"><span data-stu-id="67eef-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="67eef-204">下列查詢會要求包含名稱屬性且其值為 `AndersenFamily`的文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="67eef-205">沒有名稱屬性或值不符合 `AndersenFamily` 的任何其他文件都會予以排除。</span><span class="sxs-lookup"><span data-stu-id="67eef-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="67eef-206">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-207">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="67eef-208">前一個範例已顯示簡單的相等查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="67eef-209">DocumentDB API SQL 也支援各種純量運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="67eef-210">最常用的是二元和一元運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="67eef-211">來源 JSON 物件中的屬性參考也是有效的運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="67eef-212">下列是目前支援的二元運算式，而且可以用於查詢中 (如下列範例所示)：</span><span class="sxs-lookup"><span data-stu-id="67eef-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="67eef-213">算術</span><span class="sxs-lookup"><span data-stu-id="67eef-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="67eef-214">+、-、*、/、%</span><span class="sxs-lookup"><span data-stu-id="67eef-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="67eef-215">位元</span><span class="sxs-lookup"><span data-stu-id="67eef-215">Bitwise</span></span></td>    
<td><span data-ttu-id="67eef-216">|、&、^、<<、>>、>>> (右移位並填滿零)</span><span class="sxs-lookup"><span data-stu-id="67eef-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="67eef-217">邏輯</span><span class="sxs-lookup"><span data-stu-id="67eef-217">Logical</span></span></td>
<td><span data-ttu-id="67eef-218">AND、OR、NOT</span><span class="sxs-lookup"><span data-stu-id="67eef-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="67eef-219">比較</span><span class="sxs-lookup"><span data-stu-id="67eef-219">Comparison</span></span></td>    
<td><span data-ttu-id="67eef-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="67eef-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="67eef-221">String</span><span class="sxs-lookup"><span data-stu-id="67eef-221">String</span></span></td>    
<td><span data-ttu-id="67eef-222">|| (串連)</span><span class="sxs-lookup"><span data-stu-id="67eef-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="67eef-223">讓我們了解一些使用二元運算子的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="67eef-224">一元運算子 +、-、~ 及 NOT 也是支援的運算子，可在查詢內使用 (如下列範例所示)：</span><span class="sxs-lookup"><span data-stu-id="67eef-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="67eef-225">除了二元和一元運算子之外，還允許屬性參照。</span><span class="sxs-lookup"><span data-stu-id="67eef-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="67eef-226">例如，`SELECT * FROM Families f WHERE f.isRegistered` 所傳回的 JSON 文件包含屬性 `isRegistered` 且屬性值等於 JSON `true` 值。</span><span class="sxs-lookup"><span data-stu-id="67eef-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="67eef-227">任何其他值 (false、null、Undefined、`<number>`、`<string>`、`<object>`、`<array>` 等) 則會導致從結果中排除來源文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="67eef-228">相等和比較運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-228">Equality and comparison operators</span></span>
<span data-ttu-id="67eef-229">下表顯示 DocumentDB API SQL 中任何兩個 JSON 類型之間的相等比較結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-230">
            <strong>運算子</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="67eef-231">
            <strong>Undefined</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="67eef-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="67eef-233">
            <strong>布林值</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="67eef-234">
            <strong>數字</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="67eef-235">
            <strong>字串</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="67eef-236">
            <strong>物件</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="67eef-237">
            <strong>陣列</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-238">
            <strong>Undefined<strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-239">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-240">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-241">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-242">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-243">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-244">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-245">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-247">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="67eef-248">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-249">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-250">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-251">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-252">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-253">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-254">
            <strong>布林值<strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-255">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-256">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="67eef-257">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-258">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-259">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-260">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-261">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-262">
            <strong>數字<strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-263">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-264">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-265">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="67eef-266">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-267">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-268">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-269">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-270">
            <strong>字串<strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-271">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-272">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-273">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-274">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="67eef-275">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-276">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-277">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-278">
            <strong>物件<strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-279">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-280">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-281">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-282">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-283">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="67eef-284">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-285">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="67eef-286">
            <strong>陣列<strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="67eef-287">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-288">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-289">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-290">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-291">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="67eef-292">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="67eef-293">
            <strong>正常</strong>
         </span><span class="sxs-lookup"><span data-stu-id="67eef-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="67eef-294">其他比較運算子 (例如 >、>=、!=、< 及 <=) 則適用下列規則：</span><span class="sxs-lookup"><span data-stu-id="67eef-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="67eef-295">不同類型的比較會導致 Undefined。</span><span class="sxs-lookup"><span data-stu-id="67eef-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="67eef-296">兩個物件或兩個陣列之間的比較會導致 Undefined。</span><span class="sxs-lookup"><span data-stu-id="67eef-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="67eef-297">如果篩選中純量運算式的結果是 Undefined，則不會將對應的文件併入結果中，因為 Undefined 邏輯上不會等於 "true"。</span><span class="sxs-lookup"><span data-stu-id="67eef-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="67eef-298">BETWEEN 關鍵字</span><span class="sxs-lookup"><span data-stu-id="67eef-298">BETWEEN keyword</span></span>
<span data-ttu-id="67eef-299">您也可以使用 BETWEEN 關鍵字來表示像對 ANSI SQL 中的值範圍執行查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="67eef-300">BETWEEN 可用於字串或數字。</span><span class="sxs-lookup"><span data-stu-id="67eef-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="67eef-301">例如，此查詢會傳回其長子的成績介於 1-5 (兩者皆含) 之間的所有家族文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="67eef-302">不同於 ANSI SQL，您也可以在 FROM 子句中使用 BETWEEN 子句，如下列範例所示 。</span><span class="sxs-lookup"><span data-stu-id="67eef-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="67eef-303">如需更快速的查詢執行時間，請記得針對經過 BETWEEN 子句篩選的任何數值屬性/路徑，建立使用範圍索引類型的檢索原則。</span><span class="sxs-lookup"><span data-stu-id="67eef-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="67eef-304">在 DocumentDB API 和 ANSI SQL 中使用 BETWEEN 的主要差異在於，您可以表示針對混合類型屬性的範圍查詢，比方說，在某些文件中 "grade" 可能是數字 (5) ，而在其他文件中可能會是字串 ("grade4")。</span><span class="sxs-lookup"><span data-stu-id="67eef-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="67eef-305">在這些情況下 (像在 JavaScript 中)，這兩種不同類型之間的比較會產生 「 未定義 」，並略過文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="67eef-306">邏輯 (AND、OR 和 NOT) 運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="67eef-307">邏輯運算子的運算對象是布林值。</span><span class="sxs-lookup"><span data-stu-id="67eef-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="67eef-308">下表顯示這些運算子的邏輯真值表。</span><span class="sxs-lookup"><span data-stu-id="67eef-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="67eef-309">或</span><span class="sxs-lookup"><span data-stu-id="67eef-309">OR</span></span> | <span data-ttu-id="67eef-310">True</span><span class="sxs-lookup"><span data-stu-id="67eef-310">True</span></span> | <span data-ttu-id="67eef-311">False</span><span class="sxs-lookup"><span data-stu-id="67eef-311">False</span></span> | <span data-ttu-id="67eef-312">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="67eef-313">True</span><span class="sxs-lookup"><span data-stu-id="67eef-313">True</span></span> |<span data-ttu-id="67eef-314">True</span><span class="sxs-lookup"><span data-stu-id="67eef-314">True</span></span> |<span data-ttu-id="67eef-315">True</span><span class="sxs-lookup"><span data-stu-id="67eef-315">True</span></span> |<span data-ttu-id="67eef-316">True</span><span class="sxs-lookup"><span data-stu-id="67eef-316">True</span></span> |
| <span data-ttu-id="67eef-317">False</span><span class="sxs-lookup"><span data-stu-id="67eef-317">False</span></span> |<span data-ttu-id="67eef-318">True</span><span class="sxs-lookup"><span data-stu-id="67eef-318">True</span></span> |<span data-ttu-id="67eef-319">False</span><span class="sxs-lookup"><span data-stu-id="67eef-319">False</span></span> |<span data-ttu-id="67eef-320">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-320">Undefined</span></span> |
| <span data-ttu-id="67eef-321">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-321">Undefined</span></span> |<span data-ttu-id="67eef-322">True</span><span class="sxs-lookup"><span data-stu-id="67eef-322">True</span></span> |<span data-ttu-id="67eef-323">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-323">Undefined</span></span> |<span data-ttu-id="67eef-324">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-324">Undefined</span></span> |

| <span data-ttu-id="67eef-325">AND</span><span class="sxs-lookup"><span data-stu-id="67eef-325">AND</span></span> | <span data-ttu-id="67eef-326">True</span><span class="sxs-lookup"><span data-stu-id="67eef-326">True</span></span> | <span data-ttu-id="67eef-327">False</span><span class="sxs-lookup"><span data-stu-id="67eef-327">False</span></span> | <span data-ttu-id="67eef-328">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="67eef-329">True</span><span class="sxs-lookup"><span data-stu-id="67eef-329">True</span></span> |<span data-ttu-id="67eef-330">True</span><span class="sxs-lookup"><span data-stu-id="67eef-330">True</span></span> |<span data-ttu-id="67eef-331">False</span><span class="sxs-lookup"><span data-stu-id="67eef-331">False</span></span> |<span data-ttu-id="67eef-332">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-332">Undefined</span></span> |
| <span data-ttu-id="67eef-333">False</span><span class="sxs-lookup"><span data-stu-id="67eef-333">False</span></span> |<span data-ttu-id="67eef-334">False</span><span class="sxs-lookup"><span data-stu-id="67eef-334">False</span></span> |<span data-ttu-id="67eef-335">False</span><span class="sxs-lookup"><span data-stu-id="67eef-335">False</span></span> |<span data-ttu-id="67eef-336">False</span><span class="sxs-lookup"><span data-stu-id="67eef-336">False</span></span> |
| <span data-ttu-id="67eef-337">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-337">Undefined</span></span> |<span data-ttu-id="67eef-338">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-338">Undefined</span></span> |<span data-ttu-id="67eef-339">False</span><span class="sxs-lookup"><span data-stu-id="67eef-339">False</span></span> |<span data-ttu-id="67eef-340">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-340">Undefined</span></span> |

| <span data-ttu-id="67eef-341">NOT</span><span class="sxs-lookup"><span data-stu-id="67eef-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="67eef-342">True</span><span class="sxs-lookup"><span data-stu-id="67eef-342">True</span></span> |<span data-ttu-id="67eef-343">False</span><span class="sxs-lookup"><span data-stu-id="67eef-343">False</span></span> |
| <span data-ttu-id="67eef-344">False</span><span class="sxs-lookup"><span data-stu-id="67eef-344">False</span></span> |<span data-ttu-id="67eef-345">True</span><span class="sxs-lookup"><span data-stu-id="67eef-345">True</span></span> |
| <span data-ttu-id="67eef-346">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-346">Undefined</span></span> |<span data-ttu-id="67eef-347">Undefined</span><span class="sxs-lookup"><span data-stu-id="67eef-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="67eef-348">IN 關鍵字</span><span class="sxs-lookup"><span data-stu-id="67eef-348">IN keyword</span></span>
<span data-ttu-id="67eef-349">IN 關鍵字可用來檢查指定的值是否符合清單中的任何值。</span><span class="sxs-lookup"><span data-stu-id="67eef-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="67eef-350">例如，此查詢會傳回所有的家族文件，其中 id 是 "WakefieldFamily" 或 "AndersenFamily" 其中一個。</span><span class="sxs-lookup"><span data-stu-id="67eef-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="67eef-351">這個範例會傳回其狀態是任何一個指定值的所有文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="67eef-352">三元 (?) 和聯合 (??) 運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="67eef-353">三元和聯合運算子可用來建立條件運算式，與熱門程式設計語言 (如 C# 和 JavaScript) 類似。</span><span class="sxs-lookup"><span data-stu-id="67eef-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="67eef-354">快速建構新的 JSON 屬性時，三元 (?) 運算子可以說非常好用。</span><span class="sxs-lookup"><span data-stu-id="67eef-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="67eef-355">比方說，您現在可以撰寫查詢將類別層級分類為一般人可判讀的格式 (例如初級/中級/進階)，如下所示。</span><span class="sxs-lookup"><span data-stu-id="67eef-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="67eef-356">您也可以巢狀運算子的呼叫，如下方查詢所示。</span><span class="sxs-lookup"><span data-stu-id="67eef-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="67eef-357">和其他查詢運算子一樣，如果任何文件中的條件運算式遺漏了參考屬性，或者要比較的類型不同，則查詢結果會將那些文件排除在外。</span><span class="sxs-lookup"><span data-stu-id="67eef-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="67eef-358">聯合 (??) 運算子可用來有效率地檢查屬性是否存在 (也稱為</span><span class="sxs-lookup"><span data-stu-id="67eef-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="67eef-359">已定義) 於文件中。</span><span class="sxs-lookup"><span data-stu-id="67eef-359">is defined) in a document.</span></span> <span data-ttu-id="67eef-360">針對半結構化或混合類型的資料執行查詢時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="67eef-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="67eef-361">例如，此查詢會傳回 "lastName" (如果存在) 或 "surname" (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="67eef-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="67eef-362"><a id="EscapingReservedKeywords"></a>加上引號的屬性存取子</span><span class="sxs-lookup"><span data-stu-id="67eef-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="67eef-363">您也可以使用加上引號的屬性運算子 `[]`存取屬性。</span><span class="sxs-lookup"><span data-stu-id="67eef-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="67eef-364">例如， `SELECT c.grade` and `SELECT c["grade"]` 是相等的。</span><span class="sxs-lookup"><span data-stu-id="67eef-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="67eef-365">當您需要逸出包含空格、特殊字元的屬性，或剛好要共用和 SQL 關鍵字或保留字相同的名稱時，此語法很有用。</span><span class="sxs-lookup"><span data-stu-id="67eef-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="67eef-366"><a id="SelectClause"></a>SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="67eef-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="67eef-367">SELECT 子句 (**`SELECT <select_list>`**) 是必要項目，並指定要從查詢中擷取的值 (就像在 ANSI-SQL 中)。</span><span class="sxs-lookup"><span data-stu-id="67eef-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="67eef-368">在來源文件上篩選出來的子集會傳遞給投射階段，而在此階段中，會擷取指定的 JSON 值並建構新的 JSON 物件 (針對每個傳遞給它的輸入)。</span><span class="sxs-lookup"><span data-stu-id="67eef-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="67eef-369">下列範例示範一般的 SELECT 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="67eef-370">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-371">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="67eef-372">巢狀屬性</span><span class="sxs-lookup"><span data-stu-id="67eef-372">Nested properties</span></span>
<span data-ttu-id="67eef-373">在下列範例中，我們將投射兩個巢狀屬性 `f.address.state` and `f.address.city`。</span><span class="sxs-lookup"><span data-stu-id="67eef-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="67eef-374">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-375">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="67eef-376">投射也支援 JSON 運算式 (如下列範例所示)：</span><span class="sxs-lookup"><span data-stu-id="67eef-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="67eef-377">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-378">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="67eef-379">讓我們在這裡查看 `$1` 角色。</span><span class="sxs-lookup"><span data-stu-id="67eef-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="67eef-380">`SELECT` 子句需要建立 JSON 物件，且因為未提供任何索引鍵，所以我們將使用以 `$1` 開頭的隱含引數變數名稱。</span><span class="sxs-lookup"><span data-stu-id="67eef-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="67eef-381">例如，此查詢會傳回兩個隱含引數變數，名稱為 `$1` 和 `$2`。</span><span class="sxs-lookup"><span data-stu-id="67eef-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="67eef-382">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-383">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="67eef-384">別名</span><span class="sxs-lookup"><span data-stu-id="67eef-384">Aliasing</span></span>
<span data-ttu-id="67eef-385">現在，讓我們使用值的明確別名處理來擴充上面的範例。</span><span class="sxs-lookup"><span data-stu-id="67eef-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="67eef-386">AS 是用來加上別名的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="67eef-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="67eef-387">它在將第二個值投射為 `NameInfo` 時是選用項目 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="67eef-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="67eef-388">如果查詢具有兩個同名的屬性，則必須使用別名處理來重新命名一或兩個屬性，使其在投射的結果中變得更為明確。</span><span class="sxs-lookup"><span data-stu-id="67eef-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="67eef-389">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-390">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="67eef-391">純量運算式</span><span class="sxs-lookup"><span data-stu-id="67eef-391">Scalar expressions</span></span>
<span data-ttu-id="67eef-392">除了屬性參考之外，SELECT 子句也支援純量運算式 (例如常數、算術運算式、邏輯運算式等)。例如，以下是簡單 "Hello World" 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="67eef-393">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="67eef-394">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="67eef-395">以下是使用純量運算式的較複雜範例。</span><span class="sxs-lookup"><span data-stu-id="67eef-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="67eef-396">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="67eef-397">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="67eef-398">在下列範例中，純量運算式結果是布林值。</span><span class="sxs-lookup"><span data-stu-id="67eef-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="67eef-399">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="67eef-400">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="67eef-401">物件和陣列建立</span><span class="sxs-lookup"><span data-stu-id="67eef-401">Object and array creation</span></span>
<span data-ttu-id="67eef-402">DocumentDB API SQL 的另一個重要功能是建立陣列/物件。</span><span class="sxs-lookup"><span data-stu-id="67eef-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="67eef-403">在前一個範例中，請注意，我們已建立新的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="67eef-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="67eef-404">同樣地，您也可以建構陣列 (如下列範例所示)：</span><span class="sxs-lookup"><span data-stu-id="67eef-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="67eef-405">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="67eef-406">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-406">**Results**</span></span>  

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

### <span data-ttu-id="67eef-407"><a id="ValueKeyword"></a>VALUE 關鍵字</span><span class="sxs-lookup"><span data-stu-id="67eef-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="67eef-408">**VALUE** 關鍵字提供可傳回 JSON 值的方法。</span><span class="sxs-lookup"><span data-stu-id="67eef-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="67eef-409">例如，下面顯示的查詢會傳回純量 `"Hello World"` 而非 `{$1: "Hello World"}`。</span><span class="sxs-lookup"><span data-stu-id="67eef-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="67eef-410">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="67eef-411">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="67eef-412">下列查詢會在結果中傳回不含 `"address"` 標籤的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="67eef-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="67eef-413">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="67eef-414">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-414">**Results**</span></span>  

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

<span data-ttu-id="67eef-415">下列範例會延伸此程式碼，以示範如何傳回 JSON 基本值 (JSON 樹狀目錄的分葉層級)。</span><span class="sxs-lookup"><span data-stu-id="67eef-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="67eef-416">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="67eef-417">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="67eef-418">* 運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-418">* Operator</span></span>
<span data-ttu-id="67eef-419">支援使用特殊運算子 (*) 來依原樣投射文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="67eef-420">使用時，它必須是唯一投射的欄位。</span><span class="sxs-lookup"><span data-stu-id="67eef-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="67eef-421">`SELECT * FROM Families f` 之類的查詢有效，`SELECT VALUE * FROM Families f ` 和 `SELECT *, f.id FROM Families f ` 則無效。</span><span class="sxs-lookup"><span data-stu-id="67eef-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="67eef-422">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="67eef-423">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-423">**Results**</span></span>

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

### <span data-ttu-id="67eef-424"><a id="TopKeyword"></a>TOP 運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="67eef-425">TOP 關鍵字可以用來限制來自查詢的值數目。</span><span class="sxs-lookup"><span data-stu-id="67eef-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="67eef-426">當 TOP 與 ORDER BY 子句一起使用時，結果集會限制於前 N 個已排序的值。否則，它會以未定義的順序傳回前 N 個結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="67eef-427">最佳做法是在 SELECT 陳述式中，一律搭配 TOP 子句來使用 ORDER BY 子句。</span><span class="sxs-lookup"><span data-stu-id="67eef-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="67eef-428">這是唯一能如預期般指出哪些資料列會受到 TOP 影響的方式。</span><span class="sxs-lookup"><span data-stu-id="67eef-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="67eef-429">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="67eef-430">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-430">**Results**</span></span>

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

<span data-ttu-id="67eef-431">TOP 可以與常數值 (如上所示) 或使用參數化查詢的變數值搭配使用 。</span><span class="sxs-lookup"><span data-stu-id="67eef-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="67eef-432">如需詳細資訊，請參閱下方的參數化查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="67eef-433"><a id="Aggregates"></a>彙總函式</span><span class="sxs-lookup"><span data-stu-id="67eef-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="67eef-434">您也可以在 `SELECT` 子句中執行彙總。</span><span class="sxs-lookup"><span data-stu-id="67eef-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="67eef-435">彙總函式會執行一組值的計算，然後傳回單一值。</span><span class="sxs-lookup"><span data-stu-id="67eef-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="67eef-436">例如，下列查詢會傳回集合內的系列文件計數。</span><span class="sxs-lookup"><span data-stu-id="67eef-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="67eef-437">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="67eef-438">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="67eef-439">您也可以使用 `VALUE` 關鍵字來傳回彙總的純量值。</span><span class="sxs-lookup"><span data-stu-id="67eef-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="67eef-440">例如，下列查詢會以單一數字傳回值的計數：</span><span class="sxs-lookup"><span data-stu-id="67eef-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="67eef-441">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="67eef-442">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="67eef-443">您也可以搭配篩選器執行彙總。</span><span class="sxs-lookup"><span data-stu-id="67eef-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="67eef-444">例如，下列查詢會傳回位址在華盛頓州的文件計數。</span><span class="sxs-lookup"><span data-stu-id="67eef-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="67eef-445">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="67eef-446">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="67eef-447">下表顯示 DocumentDB API 中支援的彙總函式清單。</span><span class="sxs-lookup"><span data-stu-id="67eef-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="67eef-448">`SUM` 和 `AVG` 是對數值執行，而 `COUNT`、`MIN`和 `MAX` 則可對數字、字串、布林值和 null 執行。</span><span class="sxs-lookup"><span data-stu-id="67eef-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="67eef-449">使用量</span><span class="sxs-lookup"><span data-stu-id="67eef-449">Usage</span></span> | <span data-ttu-id="67eef-450">說明</span><span class="sxs-lookup"><span data-stu-id="67eef-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="67eef-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="67eef-451">COUNT</span></span> | <span data-ttu-id="67eef-452">以運算式傳回項目的數目。</span><span class="sxs-lookup"><span data-stu-id="67eef-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="67eef-453">SUM</span><span class="sxs-lookup"><span data-stu-id="67eef-453">SUM</span></span>   | <span data-ttu-id="67eef-454">以運算式傳回所有值的總和。</span><span class="sxs-lookup"><span data-stu-id="67eef-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="67eef-455">最小值</span><span class="sxs-lookup"><span data-stu-id="67eef-455">MIN</span></span>   | <span data-ttu-id="67eef-456">以運算式傳回最小值。</span><span class="sxs-lookup"><span data-stu-id="67eef-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="67eef-457">最大值</span><span class="sxs-lookup"><span data-stu-id="67eef-457">MAX</span></span>   | <span data-ttu-id="67eef-458">以運算式傳回最大值。</span><span class="sxs-lookup"><span data-stu-id="67eef-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="67eef-459">平均</span><span class="sxs-lookup"><span data-stu-id="67eef-459">AVG</span></span>   | <span data-ttu-id="67eef-460">以運算式傳回值的平均。</span><span class="sxs-lookup"><span data-stu-id="67eef-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="67eef-461">彙總也可以對陣列反覆運算的結果執行。</span><span class="sxs-lookup"><span data-stu-id="67eef-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="67eef-462">如需詳細資訊，請參閱[查詢中的陣列反覆運算](#Iteration)。</span><span class="sxs-lookup"><span data-stu-id="67eef-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="67eef-463">使用 Azure 入口網站的 [查詢總管] 時，請注意彙總查詢可能會對查詢頁面傳回部分彙總的結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="67eef-464">SDK 會產生所有頁面的單一累計值。</span><span class="sxs-lookup"><span data-stu-id="67eef-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="67eef-465">若要使用程式碼執行彙總查詢，您需要 .NET SDK 1.12.0、.NET Core SDK 1.1.0 或 Java SDK 1.9.5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="67eef-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="67eef-466"><a id="OrderByClause"></a>ORDER BY 子句</span><span class="sxs-lookup"><span data-stu-id="67eef-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="67eef-467">像是在 ANSI SQL 中，您可以在查詢時包含選擇性的 Order By 子句。</span><span class="sxs-lookup"><span data-stu-id="67eef-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="67eef-468">子句可以包含選擇性 ASC/DESC 引數，利用它來指定擷取結果時必須依循的順序。</span><span class="sxs-lookup"><span data-stu-id="67eef-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="67eef-469">例如，以下是依據居住城市名稱的順序擷取家族的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="67eef-470">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="67eef-471">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-471">**Results**</span></span>

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

<span data-ttu-id="67eef-472">以下是依據建立日期擷取家族的查詢，儲存為代表 epoch 時間的數字，也就是，自 1970 年 1 月 1 日之後經過的時間 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="67eef-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="67eef-473">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="67eef-474">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-474">**Results**</span></span>

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

## <span data-ttu-id="67eef-475"><a id="Advanced"></a>進階資料庫概念和 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="67eef-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="67eef-476"><a id="Iteration"></a>反覆運算</span><span class="sxs-lookup"><span data-stu-id="67eef-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="67eef-477">在 DocumentDB API SQL 中已透過 **IN** 關鍵字加入新的建構，以支援對 JSON 陣列的反覆查看。</span><span class="sxs-lookup"><span data-stu-id="67eef-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="67eef-478">FROM 來源支援反覆運算。</span><span class="sxs-lookup"><span data-stu-id="67eef-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="67eef-479">讓我們從下列範例開始：</span><span class="sxs-lookup"><span data-stu-id="67eef-479">Let's start with the following example:</span></span>

<span data-ttu-id="67eef-480">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="67eef-481">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-481">**Results**</span></span>  

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

<span data-ttu-id="67eef-482">現在，讓我們查看另一個查詢，以執行反覆運算集合中的子系。</span><span class="sxs-lookup"><span data-stu-id="67eef-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="67eef-483">請注意輸出陣列中的差異。</span><span class="sxs-lookup"><span data-stu-id="67eef-483">Note the difference in the output array.</span></span> <span data-ttu-id="67eef-484">此範例會分割 `children` ，並將結果簡維成單一陣列。</span><span class="sxs-lookup"><span data-stu-id="67eef-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="67eef-485">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="67eef-486">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-486">**Results**</span></span>  

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

<span data-ttu-id="67eef-487">這可以進一步用來篩選陣列的每個個別項目 (如下列範例所示)：</span><span class="sxs-lookup"><span data-stu-id="67eef-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="67eef-488">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="67eef-489">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="67eef-490">您也可以對陣列反覆運算的結果執行彙總。</span><span class="sxs-lookup"><span data-stu-id="67eef-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="67eef-491">例如，下列查詢會計算所有系列的子系數目。</span><span class="sxs-lookup"><span data-stu-id="67eef-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="67eef-492">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="67eef-493">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="67eef-494"><a id="Joins"></a>聯結</span><span class="sxs-lookup"><span data-stu-id="67eef-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="67eef-495">在關聯式資料庫中，跨資料表的聯結需求很重要。</span><span class="sxs-lookup"><span data-stu-id="67eef-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="67eef-496">就設計正規化結構描述而言，邏輯上需要它。</span><span class="sxs-lookup"><span data-stu-id="67eef-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="67eef-497">與此相反的是，DocumentDB API 會處理無結構描述文件的反正規化資料模型。</span><span class="sxs-lookup"><span data-stu-id="67eef-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="67eef-498">這在邏輯上等同於「自我聯結」。</span><span class="sxs-lookup"><span data-stu-id="67eef-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="67eef-499">語言支援的語法是 <from_source1> JOIN <from_source2> JOIN ...JOIN <from_sourceN>。</span><span class="sxs-lookup"><span data-stu-id="67eef-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="67eef-500">整體而言，這會傳回一組 **N**-Tuple (具有 **N** 個值的 Tuple)。</span><span class="sxs-lookup"><span data-stu-id="67eef-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="67eef-501">每個 Tuple 所擁有的值，都是將所有集合別名在其個別集合上反覆運算所產生。</span><span class="sxs-lookup"><span data-stu-id="67eef-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="67eef-502">換句話說，這是參與聯結之集的完整交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="67eef-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="67eef-503">下列範例示範 JOIN 子句的運作方式。</span><span class="sxs-lookup"><span data-stu-id="67eef-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="67eef-504">在下列範例中，結果是空的，因為來源中每個文件與空集合的交叉乘積是空的。</span><span class="sxs-lookup"><span data-stu-id="67eef-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="67eef-505">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="67eef-506">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="67eef-507">在下列範例中，聯結會介於文件根目錄與 `children` 子根目錄之間。</span><span class="sxs-lookup"><span data-stu-id="67eef-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="67eef-508">它是兩個 JSON 物件之間的交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="67eef-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="67eef-509">子系是陣列的事實不會影響 JOIN，因為我們是處理為子陣列的單一根目錄。</span><span class="sxs-lookup"><span data-stu-id="67eef-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="67eef-510">因此，結果只會包含兩個結果，因為每個含有陣列之文件的交叉乘積都只會產生一個文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="67eef-511">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="67eef-512">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="67eef-513">下列範例示範較傳統的聯結：</span><span class="sxs-lookup"><span data-stu-id="67eef-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="67eef-514">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="67eef-515">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-515">**Results**</span></span>

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



<span data-ttu-id="67eef-516">第一件要注意的事是 **JOIN** 子句的 `from_source` 是迭代器。</span><span class="sxs-lookup"><span data-stu-id="67eef-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="67eef-517">因此，此案例中的流程如下：</span><span class="sxs-lookup"><span data-stu-id="67eef-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="67eef-518">展開陣列中的每個子項目 **c** 。</span><span class="sxs-lookup"><span data-stu-id="67eef-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="67eef-519">套用文件 **f** 的根目錄與第一個步驟中所簡維之每個子項目 **c** 的交叉乘積。</span><span class="sxs-lookup"><span data-stu-id="67eef-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="67eef-520">最後，單獨投射根物件 **f** 名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="67eef-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="67eef-521">第一份文件 (`AndersenFamily`) 只包含一個子項目，因此結果集只會包含與此文件相對應的單一物件。</span><span class="sxs-lookup"><span data-stu-id="67eef-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="67eef-522">第二份文件 (`WakefieldFamily`) 包含兩個子系。</span><span class="sxs-lookup"><span data-stu-id="67eef-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="67eef-523">因此，交叉乘積會產生每個子系的個別物件，進而導致兩個物件 (一個對應至此文件的子系一個)。</span><span class="sxs-lookup"><span data-stu-id="67eef-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="67eef-524">這兩份文件中的根欄位相同，就像您在交叉乘積中預期地一樣。</span><span class="sxs-lookup"><span data-stu-id="67eef-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="67eef-525">JOIN 的實際作用是透過圖形中很難投射的交叉乘積來形成 Tuple。</span><span class="sxs-lookup"><span data-stu-id="67eef-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="67eef-526">此外，如下面範例所示，您可以根據 Tuple 的組合進行篩選，讓使用者選擇全部 Tuple 都符合的條件。</span><span class="sxs-lookup"><span data-stu-id="67eef-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="67eef-527">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="67eef-528">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-528">**Results**</span></span>

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



<span data-ttu-id="67eef-529">此範例是上述範例的自然延伸，用來執行雙重聯結。</span><span class="sxs-lookup"><span data-stu-id="67eef-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="67eef-530">因此，交叉乘積可被視為下列虛擬程式碼：</span><span class="sxs-lookup"><span data-stu-id="67eef-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

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

<span data-ttu-id="67eef-531">`AndersenFamily` 有一個小孩養了一隻寵物。</span><span class="sxs-lookup"><span data-stu-id="67eef-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="67eef-532">因此，交叉乘積會從此家族產生 1 個資料列 (1\*1\*1)。</span><span class="sxs-lookup"><span data-stu-id="67eef-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="67eef-533">不過，WakefieldFamily 有兩個小孩，但只有一個小孩 "Jesse" 養了多隻寵物。</span><span class="sxs-lookup"><span data-stu-id="67eef-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="67eef-534">Jesse 有兩隻寵物。</span><span class="sxs-lookup"><span data-stu-id="67eef-534">Jesse has two pets though.</span></span> <span data-ttu-id="67eef-535">因此，交叉乘積會從此家族產生 1\*1\*2 = 2 個資料列。</span><span class="sxs-lookup"><span data-stu-id="67eef-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="67eef-536">在下一個範例中，對 `pet`有一個額外的篩選。</span><span class="sxs-lookup"><span data-stu-id="67eef-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="67eef-537">這會排除寵物名稱不是 "Shadow" 的所有 Tuple。</span><span class="sxs-lookup"><span data-stu-id="67eef-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="67eef-538">請注意，我們可以從陣列建置 Tuple、根據 Tuple 的任何元素進行篩選，以及投射元素的任何組合。</span><span class="sxs-lookup"><span data-stu-id="67eef-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="67eef-539">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="67eef-540">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="67eef-541"><a id="JavaScriptIntegration"></a>JavaScript 整合</span><span class="sxs-lookup"><span data-stu-id="67eef-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="67eef-542">Azure Cosmos DB 提供一個程式設計模型，可藉由預存程序和觸發程序，直接對集合執行 JavaScript 型應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="67eef-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="67eef-543">這允許：</span><span class="sxs-lookup"><span data-stu-id="67eef-543">This allows for both:</span></span>

* <span data-ttu-id="67eef-544">藉由直接在資料庫引擎內深入整合 JavaScript 執行階段，對集合中的文件執行高效能交易式 CRUD 操作和查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="67eef-545">將控制流程、變數範圍限制、指派以及例外狀況處理基本類型與資料庫交易的整合自然模型化。</span><span class="sxs-lookup"><span data-stu-id="67eef-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="67eef-546">如需有關 JavaScript 整合之 Azure Cosmos DB 支援的詳細資料，請參閱 JavaScript 伺服器端程式設計文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="67eef-547"><a id="UserDefinedFunctions"></a>使用者定義函式 (UDF)</span><span class="sxs-lookup"><span data-stu-id="67eef-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="67eef-548">除了本文中已定義的類型之外，DocumentDB API SQL 還支援「使用者定義函數」(UDF)。</span><span class="sxs-lookup"><span data-stu-id="67eef-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="67eef-549">特別的是，如果開發人員可以傳入零個或多個引數並傳回單一引數結果，則支援純量 UDF。</span><span class="sxs-lookup"><span data-stu-id="67eef-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="67eef-550">系統會檢查所有這些引數是否為合法的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="67eef-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="67eef-551">DocumentDB API SQL 語法已延伸，可支援使用這些使用者定義函式的自訂應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="67eef-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="67eef-552">您可以向 DocumentDB API 註冊 UDF，然後在 SQL 查詢中參照它。</span><span class="sxs-lookup"><span data-stu-id="67eef-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="67eef-553">實際上，UDF 是特別設計來透過查詢進行叫用。</span><span class="sxs-lookup"><span data-stu-id="67eef-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="67eef-554">這項選擇的必然結果，就是 UDF 無法存取其他 JavaScript 類型 (預存程序和觸發程序) 擁有的內容物件。</span><span class="sxs-lookup"><span data-stu-id="67eef-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="67eef-555">因為查詢是以唯讀形式執行，所以可以在主要或次要複本上執行。</span><span class="sxs-lookup"><span data-stu-id="67eef-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="67eef-556">因此，與其他 JavaScript 類型不同，UDF 是設計成在次要複本上執行。</span><span class="sxs-lookup"><span data-stu-id="67eef-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="67eef-557">以下是如何在 Cosmos DB 資料庫 (更明確地說是在文件集合下) 註冊 UDF 的範例。</span><span class="sxs-lookup"><span data-stu-id="67eef-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="67eef-558">上述範例會建立名為 `REGEX_MATCH`的 UDF。</span><span class="sxs-lookup"><span data-stu-id="67eef-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="67eef-559">它接受兩個 JSON 字串值 `input` and `pattern` ，並使用 JavaScript 的 string.match() 函式來檢查第一個項目是否符合第二個項目中指定的模式。</span><span class="sxs-lookup"><span data-stu-id="67eef-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="67eef-560">我們現在可以在投射的查詢中使用此 UDF。</span><span class="sxs-lookup"><span data-stu-id="67eef-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="67eef-561">必須以區分大小寫的前置詞 "udf." 來限定 UDF</span><span class="sxs-lookup"><span data-stu-id="67eef-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="67eef-562">(當從查詢內呼叫時)。</span><span class="sxs-lookup"><span data-stu-id="67eef-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="67eef-563">在 2015 年 3 月 17 日以前，Cosmos DB 支援無 "udf." 前置詞的 UDF 呼叫，</span><span class="sxs-lookup"><span data-stu-id="67eef-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="67eef-564">例如 SELECT REGEX_MATCH()。</span><span class="sxs-lookup"><span data-stu-id="67eef-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="67eef-565">這種呼叫模式已被取代。</span><span class="sxs-lookup"><span data-stu-id="67eef-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="67eef-566">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="67eef-567">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="67eef-568">UDF 也可以用於篩選內 (如下面範例所示)，同樣是以 "udf."</span><span class="sxs-lookup"><span data-stu-id="67eef-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="67eef-569">前置詞來限定：</span><span class="sxs-lookup"><span data-stu-id="67eef-569">prefix:</span></span>

<span data-ttu-id="67eef-570">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="67eef-571">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="67eef-572">在本質上，UDF 是有效的純量運算式，而且可以用於投射和篩選。</span><span class="sxs-lookup"><span data-stu-id="67eef-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="67eef-573">為了擴展 UDF 的能力，請查看另一個含有條件式邏輯的範例：</span><span class="sxs-lookup"><span data-stu-id="67eef-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="67eef-574">以下是執行 UDF 的範例。</span><span class="sxs-lookup"><span data-stu-id="67eef-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="67eef-575">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="67eef-576">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-576">**Results**</span></span>

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


<span data-ttu-id="67eef-577">如上述範例所示，UDF 會將 JavaScript 語言的強大功能與 DocumentDB API SQL 整合來提供可進行程式設計的豐富介面，以在內建的 JavaScript 執行階段功能協助下，執行複雜的程序性、條件式邏輯。</span><span class="sxs-lookup"><span data-stu-id="67eef-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="67eef-578">在處理 UDF 的目前階段 (WHERE 子句或 SELECT 子句) 中，DocumentDB API SQL 會針對來源中的每個文件提供 UDF 的引數。</span><span class="sxs-lookup"><span data-stu-id="67eef-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="67eef-579">結果會緊密整合至整體執行管線。</span><span class="sxs-lookup"><span data-stu-id="67eef-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="67eef-580">如果 JSON 值中沒有 UDF 參數所參照的屬性，則會將參數視為 undefined，因此，而整個略過 UDF 叫用。</span><span class="sxs-lookup"><span data-stu-id="67eef-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="67eef-581">同樣地，如果 UDF 的結果為未定義，便不會被納入結果中。</span><span class="sxs-lookup"><span data-stu-id="67eef-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="67eef-582">簡言之，UDF 是在進行查詢時執行複雜商務邏輯的不錯工具。</span><span class="sxs-lookup"><span data-stu-id="67eef-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="67eef-583">運算子評估</span><span class="sxs-lookup"><span data-stu-id="67eef-583">Operator evaluation</span></span>
<span data-ttu-id="67eef-584">Cosmos DB 藉由作為 JSON 資料庫，可將 JavaScript 運算子與其評估語意做比較。</span><span class="sxs-lookup"><span data-stu-id="67eef-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="67eef-585">雖然 Cosmos DB 嘗試以 JSON 支援的形式保留 JavaScript 語意，但是在部分執行個體中，作業評估還是會偏離。</span><span class="sxs-lookup"><span data-stu-id="67eef-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="67eef-586">與傳統 SQL 不同，在 DocumentDB API SQL 中，通常要等到從資料庫擷取值，才會知道值的類型。</span><span class="sxs-lookup"><span data-stu-id="67eef-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="67eef-587">為了有效率地執行查詢，大部分的運算子都有嚴謹的類型需求。</span><span class="sxs-lookup"><span data-stu-id="67eef-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="67eef-588">與 JavaScript 不同，DocumentDB API SQL 並不會執行隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="67eef-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="67eef-589">例如，類似 `SELECT * FROM Person p WHERE p.Age = 21` 的查詢會針對包含 Age 屬性且值為 21 的文件進行比對。</span><span class="sxs-lookup"><span data-stu-id="67eef-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="67eef-590">任何其他 Age 屬性符合字串 "21" 或其他可能之無限制變化 (例如 "021"、"21.0"、"0021"、"00021" 等等) 的文件，則不會成為比對的結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="67eef-591">這與 JavaScript 形成對比，在 JavaScript 中，會將字串值隱含地轉換成數字 (根據運算子，例如：==)。</span><span class="sxs-lookup"><span data-stu-id="67eef-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="67eef-592">這項選擇對 DocumentDB API SQL 中有效率的索引比對十分重要。</span><span class="sxs-lookup"><span data-stu-id="67eef-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="67eef-593">參數化 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="67eef-593">Parameterized SQL queries</span></span>
<span data-ttu-id="67eef-594">Cosmos DB 支援含有以常見的 @ 標記法表示之參數的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="67eef-595">參數化 SQL 提供使用者輸入的健全處理和逸出，防止透過 SQL 插入式意外洩露資料。</span><span class="sxs-lookup"><span data-stu-id="67eef-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="67eef-596">比方說，您可以撰寫查詢，將姓氏和地址 (州) 做為參數，然後根據使用者輸入，使用各種不同姓氏和地址 (州) 的值執行查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="67eef-597">您可以接著將此要求傳送給 Cosmos DB 作為參數化 JSON 查詢，如下所示。</span><span class="sxs-lookup"><span data-stu-id="67eef-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="67eef-598">您可以使用參數化查詢來設定 TOP 的引數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="67eef-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="67eef-599">參數值可以是任何有效的 JSON (字串、數字、布林值、null，甚至是陣列或巢狀 JSON)。</span><span class="sxs-lookup"><span data-stu-id="67eef-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="67eef-600">此外，由於 Cosmos DB 並無結構描述，因此系統不會對照任何類型來驗證參數。</span><span class="sxs-lookup"><span data-stu-id="67eef-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="67eef-601"><a id="BuiltinFunctions"></a>內建函數</span><span class="sxs-lookup"><span data-stu-id="67eef-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="67eef-602">Cosmos DB 也支援一些適用於一般作業的內建函式，這些函式可在像是使用者定義函式 (UDF) 之類的查詢內使用。</span><span class="sxs-lookup"><span data-stu-id="67eef-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="67eef-603">函式群組</span><span class="sxs-lookup"><span data-stu-id="67eef-603">Function group</span></span>          | <span data-ttu-id="67eef-604">作業</span><span class="sxs-lookup"><span data-stu-id="67eef-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="67eef-605">數學函數</span><span class="sxs-lookup"><span data-stu-id="67eef-605">Mathematical functions</span></span>  | <span data-ttu-id="67eef-606">ABS、CEILING、EXP、FLOOR、LOG、LOG10、POWER、ROUND、SIGN、SQRT、SQUARE、TRUNC、ACOS、ASIN、ATAN、ATN2、COS、COT、DEGREES、PI、RADIANS、SIN 和 TAN</span><span class="sxs-lookup"><span data-stu-id="67eef-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="67eef-607">類型檢查函數</span><span class="sxs-lookup"><span data-stu-id="67eef-607">Type checking functions</span></span> | <span data-ttu-id="67eef-608">IS_ARRAY、IS_BOOL、IS_NULL、IS_NUMBER、IS_OBJECT、IS_STRING、IS_DEFINED 和 IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="67eef-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="67eef-609">字串函數</span><span class="sxs-lookup"><span data-stu-id="67eef-609">String functions</span></span>        | <span data-ttu-id="67eef-610">CONCAT、CONTAINS、ENDSWITH、INDEX_OF、LEFT、LENGTH、LOWER、LTRIM、REPLACE、REPLICATE、REVERSE、RIGHT、RTRIM、STARTSWITH、SUBSTRING 和 UPPER</span><span class="sxs-lookup"><span data-stu-id="67eef-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="67eef-611">陣列函數</span><span class="sxs-lookup"><span data-stu-id="67eef-611">Array functions</span></span>         | <span data-ttu-id="67eef-612">ARRAY_CONCAT、ARRAY_CONTAINS、ARRAY_LENGTH 和 ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="67eef-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="67eef-613">空間函數</span><span class="sxs-lookup"><span data-stu-id="67eef-613">Spatial functions</span></span>       | <span data-ttu-id="67eef-614">ST_DISTANCE、ST_WITHIN、ST_INTERSECTS、ST_ISVALID 和 ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="67eef-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="67eef-615">如果您目前使用的使用者定義函式 (UDF) 已提供內建函式，則應該使用相對應的內建函式，因為這樣會加快執行速度且更有效率。</span><span class="sxs-lookup"><span data-stu-id="67eef-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="67eef-616">數學函數</span><span class="sxs-lookup"><span data-stu-id="67eef-616">Mathematical functions</span></span>
<span data-ttu-id="67eef-617">每個數學函式都會執行計算，通常以提供來作為引數的輸入值為基礎，並傳回數值。</span><span class="sxs-lookup"><span data-stu-id="67eef-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="67eef-618">以下是支援的內建數學函數資料表。</span><span class="sxs-lookup"><span data-stu-id="67eef-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="67eef-619">使用量</span><span class="sxs-lookup"><span data-stu-id="67eef-619">Usage</span></span> | <span data-ttu-id="67eef-620">說明</span><span class="sxs-lookup"><span data-stu-id="67eef-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="67eef-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="67eef-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="67eef-622">傳回指定之數值運算式的絕對 (正) 值。</span><span class="sxs-lookup"><span data-stu-id="67eef-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="67eef-624">傳回大於或等於指定之數值運算式的最小整數值。</span><span class="sxs-lookup"><span data-stu-id="67eef-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="67eef-626">傳回小於或等於指定之數值運算式的最大整數。</span><span class="sxs-lookup"><span data-stu-id="67eef-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="67eef-628">傳回指定之數值運算式的指數。</span><span class="sxs-lookup"><span data-stu-id="67eef-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="67eef-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="67eef-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="67eef-630">傳回指定之數值運算式的自然對數，或使用指定之基底的對數</span><span class="sxs-lookup"><span data-stu-id="67eef-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="67eef-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="67eef-632">傳回指定之數值運算式的以 10 為基底的對數值。</span><span class="sxs-lookup"><span data-stu-id="67eef-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="67eef-634">傳回數值，四捨五入到最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="67eef-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="67eef-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="67eef-636">傳回數值，截斷至最接近的整數值。</span><span class="sxs-lookup"><span data-stu-id="67eef-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="67eef-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="67eef-638">傳回指定之數值運算式的平方根。</span><span class="sxs-lookup"><span data-stu-id="67eef-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="67eef-640">傳回指定之數值運算式的平方。</span><span class="sxs-lookup"><span data-stu-id="67eef-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="67eef-642">將指定數值運算式的乘冪傳回給指定的值。</span><span class="sxs-lookup"><span data-stu-id="67eef-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="67eef-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="67eef-644">傳回指定之數值運算式的正負號值 (-1、0、1)。</span><span class="sxs-lookup"><span data-stu-id="67eef-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="67eef-646">傳回角度，以弧度為單位，它的餘弦是指定的數值運算式；也稱為反餘弦值。</span><span class="sxs-lookup"><span data-stu-id="67eef-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="67eef-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="67eef-648">傳回角度，以弧度為單位，其正弦函數是指定的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="67eef-649">這也稱為反正弦值。</span><span class="sxs-lookup"><span data-stu-id="67eef-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="67eef-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="67eef-651">傳回角度，以弧度為單位，其正切函數是指定的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="67eef-652">這也稱為反正切值。</span><span class="sxs-lookup"><span data-stu-id="67eef-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="67eef-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="67eef-654">傳回角度，以弧度為單位，正 x 軸和從原點 (y、x) 點的切線之間，其中 x 和 y 是兩個指定之浮點運算式的值。</span><span class="sxs-lookup"><span data-stu-id="67eef-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="67eef-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="67eef-656">在指定運算式中傳回指定角度的三角餘弦函數，以弧度為單位。</span><span class="sxs-lookup"><span data-stu-id="67eef-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="67eef-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="67eef-658">在指定的數值運算式中傳回指定角度的三角餘切函數，以弧度為單位。</span><span class="sxs-lookup"><span data-stu-id="67eef-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="67eef-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="67eef-660">針對以弧度指定的角度，傳回對應的角度 (以度為單位)。</span><span class="sxs-lookup"><span data-stu-id="67eef-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="67eef-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="67eef-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="67eef-662">傳回 PI 的常數值。</span><span class="sxs-lookup"><span data-stu-id="67eef-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="67eef-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="67eef-664">當您輸入數值運算式 (以度為單位) 時，傳回弧度。</span><span class="sxs-lookup"><span data-stu-id="67eef-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="67eef-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="67eef-666">在指定運算式中傳回指定角度的三角正弦函數 (以弧度為單位)。</span><span class="sxs-lookup"><span data-stu-id="67eef-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="67eef-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="67eef-668">在指定運算式中傳回輸入運算式的正切函數。</span><span class="sxs-lookup"><span data-stu-id="67eef-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="67eef-669">例如，您現在可以執行下列的查詢：</span><span class="sxs-lookup"><span data-stu-id="67eef-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="67eef-670">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="67eef-671">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-671">**Results**</span></span>

    [4]

<span data-ttu-id="67eef-672">相較於 ANSI SQL，Cosmos DB 函數的主要差異在於，其設計目的是要與無結構描述資料及混合的結構描述資料有效搭配運作。</span><span class="sxs-lookup"><span data-stu-id="67eef-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="67eef-673">例如，如果您有一個文件的 [大小] 屬性已遺失，或具有非數值的值 (例如 "unknown")，該文件就會被略過而不會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="67eef-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="67eef-674">類型檢查函數</span><span class="sxs-lookup"><span data-stu-id="67eef-674">Type checking functions</span></span>
<span data-ttu-id="67eef-675">類型檢查函數可讓您檢查 SQL 查詢中的運算式類型。</span><span class="sxs-lookup"><span data-stu-id="67eef-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="67eef-676">類型檢查函數可在屬性類型為變數或未知時，用來快速判斷文件中的屬性類型。</span><span class="sxs-lookup"><span data-stu-id="67eef-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="67eef-677">以下是支援的內建類型檢查函數資料表。</span><span class="sxs-lookup"><span data-stu-id="67eef-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="67eef-678"><strong>用法</strong></span><span class="sxs-lookup"><span data-stu-id="67eef-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="67eef-679"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="67eef-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-681">傳回布林值，表示值的類型是否為陣列。</span><span class="sxs-lookup"><span data-stu-id="67eef-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-683">傳回布林值，表示值的類型是否為布林值。</span><span class="sxs-lookup"><span data-stu-id="67eef-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-685">傳回布林值，表示值的類型是否為 null。</span><span class="sxs-lookup"><span data-stu-id="67eef-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-687">傳回布林值，表示值的類型是否為數字。</span><span class="sxs-lookup"><span data-stu-id="67eef-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-689">傳回布林值，表示值的類型是否為 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="67eef-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-691">傳回布林值，表示值的類型是否為字串。</span><span class="sxs-lookup"><span data-stu-id="67eef-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-693">傳回布林值，表示屬性是否已經指派值。</span><span class="sxs-lookup"><span data-stu-id="67eef-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="67eef-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="67eef-695">傳回布林值，表示值的類型是字串、數字、布林值或 Null。</span><span class="sxs-lookup"><span data-stu-id="67eef-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="67eef-696">藉由使用這些函數，您現在可以執行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="67eef-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="67eef-697">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="67eef-698">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="67eef-699">字串函數</span><span class="sxs-lookup"><span data-stu-id="67eef-699">String functions</span></span>
<span data-ttu-id="67eef-700">下列純量函數會對字串輸入值執行作業，並傳回字串、數值或布林值。</span><span class="sxs-lookup"><span data-stu-id="67eef-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="67eef-701">以下是內建字串函數的資料表：</span><span class="sxs-lookup"><span data-stu-id="67eef-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="67eef-702">使用量</span><span class="sxs-lookup"><span data-stu-id="67eef-702">Usage</span></span> | <span data-ttu-id="67eef-703">說明</span><span class="sxs-lookup"><span data-stu-id="67eef-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="67eef-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="67eef-705">傳回指定字串運算式的字元數目</span><span class="sxs-lookup"><span data-stu-id="67eef-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="67eef-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="67eef-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="67eef-707">傳回字串，該字串是串連兩個或多個字串值的結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="67eef-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="67eef-709">傳回字串運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="67eef-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="67eef-711">傳回布林值，表示第一個字串運算式是否以第二個結束字串運算式做為結束</span><span class="sxs-lookup"><span data-stu-id="67eef-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="67eef-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="67eef-713">傳回布林值，表示第一個字串運算式是否以第二個結束字串運算式做為結束</span><span class="sxs-lookup"><span data-stu-id="67eef-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="67eef-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="67eef-715">傳回布林值，表示第一個字串運算式是否包含第二個字串運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="67eef-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="67eef-717">傳回第一個指定的字串運算式中，第二個字串運算式第一次出現的開始位置，或者如果找不到字串，則為 -1。</span><span class="sxs-lookup"><span data-stu-id="67eef-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="67eef-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="67eef-719">傳回具有指定字元數目的字串左側部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="67eef-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="67eef-721">傳回具有指定字元數目的字串右側部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="67eef-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="67eef-723">傳回移除開頭空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="67eef-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="67eef-725">傳回截斷所有結尾空白之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="67eef-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="67eef-727">傳回將大寫字元資料轉換成小寫之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="67eef-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="67eef-729">傳回將小寫字元資料轉換成大寫之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="67eef-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="67eef-731">使用其他字串值取代指定的字串值的所有項目。</span><span class="sxs-lookup"><span data-stu-id="67eef-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="67eef-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="67eef-733">將字串值重複指定的次數。</span><span class="sxs-lookup"><span data-stu-id="67eef-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="67eef-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="67eef-735">傳回反向順序的字串值。</span><span class="sxs-lookup"><span data-stu-id="67eef-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="67eef-736">藉由使用這些函數，您現在可以執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="67eef-737">例如，您可以傳回大寫的家族名稱，如下所示：</span><span class="sxs-lookup"><span data-stu-id="67eef-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="67eef-738">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="67eef-739">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="67eef-740">或串連字串，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="67eef-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="67eef-741">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="67eef-742">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="67eef-743">字串函數也可用於 WHERE 子句中以篩選結果，例如下列範例：</span><span class="sxs-lookup"><span data-stu-id="67eef-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="67eef-744">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="67eef-745">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="67eef-746">陣列函數</span><span class="sxs-lookup"><span data-stu-id="67eef-746">Array functions</span></span>
<span data-ttu-id="67eef-747">下列純量函數會對陣列輸入值執行作業，並傳回數值、布林值或陣列值。</span><span class="sxs-lookup"><span data-stu-id="67eef-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="67eef-748">以下是內建陣列函數的資料表：</span><span class="sxs-lookup"><span data-stu-id="67eef-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="67eef-749">使用量</span><span class="sxs-lookup"><span data-stu-id="67eef-749">Usage</span></span> | <span data-ttu-id="67eef-750">說明</span><span class="sxs-lookup"><span data-stu-id="67eef-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="67eef-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="67eef-752">傳回指定陣列運算式的元素數目。</span><span class="sxs-lookup"><span data-stu-id="67eef-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="67eef-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="67eef-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="67eef-754">傳回串連兩個或多個陣列值之結果的陣列。</span><span class="sxs-lookup"><span data-stu-id="67eef-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="67eef-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="67eef-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="67eef-756">傳回布林值，表示陣列是否包含指定值。</span><span class="sxs-lookup"><span data-stu-id="67eef-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="67eef-757">可以指定要進行完整或部分比對。</span><span class="sxs-lookup"><span data-stu-id="67eef-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="67eef-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="67eef-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="67eef-759">傳回陣列運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="67eef-760">陣列函數可用來管理 JSON 中的陣列。</span><span class="sxs-lookup"><span data-stu-id="67eef-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="67eef-761">例如，以下是傳回其中一位父母是 "Robin Wakefield" 之所有文件的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="67eef-762">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="67eef-763">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="67eef-764">您可以指定部分片段來比對陣列內的元素。</span><span class="sxs-lookup"><span data-stu-id="67eef-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="67eef-765">下列查詢會尋找 `givenName` 為 `Robin` 的所有父母。</span><span class="sxs-lookup"><span data-stu-id="67eef-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="67eef-766">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="67eef-767">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="67eef-768">以下是另一個例子，會使用 ARRAY_LENGTH 取得每個家族的子女數目。</span><span class="sxs-lookup"><span data-stu-id="67eef-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="67eef-769">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="67eef-770">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="67eef-771">空間函數</span><span class="sxs-lookup"><span data-stu-id="67eef-771">Spatial functions</span></span>
<span data-ttu-id="67eef-772">Cosmos DB 支援下列「開放地理空間協會」(OGC) 內建地理空間查詢函數。</span><span class="sxs-lookup"><span data-stu-id="67eef-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="67eef-773"><strong>用法</strong></span><span class="sxs-lookup"><span data-stu-id="67eef-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="67eef-774"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="67eef-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-775">ST_DISTANCE (point_expr、point_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="67eef-776">傳回兩個 GeoJSON Point、Polygon 或 LineString 運算式之間的距離。</span><span class="sxs-lookup"><span data-stu-id="67eef-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-777">ST_WITHIN (point_expr、polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="67eef-778">傳回布林運算式，指出第一個 GeoJSON 物件 (Point、Polygon 或 LineString) 是否位在第二個 GeoJSON 物件 (Point、Polygon 或 LineString) 內。</span><span class="sxs-lookup"><span data-stu-id="67eef-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="67eef-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="67eef-780">傳回布林運算式，指出兩個指定的 GeoJSON 物件 (Point、Polygon 或 LineString) 是否相交。</span><span class="sxs-lookup"><span data-stu-id="67eef-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="67eef-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="67eef-782">傳回布林值，指出指定的 GeoJSON Point、Polygon 或 LineString 運算式是否有效。</span><span class="sxs-lookup"><span data-stu-id="67eef-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="67eef-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="67eef-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="67eef-784">如果指定的 GeoJSON Point、Polygon 或 LineString 運算式有效，就傳回包含布林值的 JSON 值；但如果是無效的，就會額外加上做為字串值的原因。</span><span class="sxs-lookup"><span data-stu-id="67eef-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="67eef-785">空間函數可以用來對空間資料執行鄰近性查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="67eef-786">例如，以下查詢使用 ST_DISTANCE 內建函數傳回所有家族文件，且這些文件在 30 公里指定位置內。</span><span class="sxs-lookup"><span data-stu-id="67eef-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="67eef-787">**查詢**</span><span class="sxs-lookup"><span data-stu-id="67eef-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="67eef-788">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="67eef-789">如需有關 Cosmos DB 中的地理空間支援詳細資料，請參閱[使用 Azure Cosmos DB 中的地理空間資料](geospatial.md)。</span><span class="sxs-lookup"><span data-stu-id="67eef-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="67eef-790">其中提供 Cosmos DB 之空間函數及 SQL 語法的概要。</span><span class="sxs-lookup"><span data-stu-id="67eef-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="67eef-791">現在讓我們看看 LINQ 查詢如何運作，以及它如何與我們到目前為止所見到的語法互動。</span><span class="sxs-lookup"><span data-stu-id="67eef-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="67eef-792"><a id="Linq"></a>LINQ 到 DocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="67eef-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="67eef-793">LINQ 是一種 .NET 程式設計模型，此模型會將運算表示為對物件串流的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="67eef-794">Cosmos DB 提供一個用戶端程式庫，可透過協助 JSON 與 .NET 物件之間的轉換，以及 LINQ 查詢子集與 Cosmos DB 查詢的對應，來與 LINQ 互動。</span><span class="sxs-lookup"><span data-stu-id="67eef-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="67eef-795">下圖顯示使用 Cosmos DB 來支援 LINQ 查詢的架構。</span><span class="sxs-lookup"><span data-stu-id="67eef-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="67eef-796">開發人員可以使用 Cosmos DB 用戶端來建立 **IQueryable** 物件，以直接查詢 Cosmos DB 查詢提供者，而此查詢提供者會接著將 LINQ 查詢轉譯成 Cosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="67eef-797">然後，將此查詢傳遞給 Cosmos DB 伺服器，以擷取一組以 JSON 格式表示的結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="67eef-798">傳回的結果會在用戶端進行還原序列化，變成 .NET 物件的串流。</span><span class="sxs-lookup"><span data-stu-id="67eef-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![使用 DocumentDB API 來支援 LINQ 查詢的架構：SQL 語法、JSON 查詢語言、資料庫概念及 SQL 查詢][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="67eef-800">.NET 和 JSON 對應</span><span class="sxs-lookup"><span data-stu-id="67eef-800">.NET and JSON mapping</span></span>
<span data-ttu-id="67eef-801">.NET 物件與 JSON 文件之間的對應是自然的，亦即每個資料成員欄位都會對應至 JSON 物件，其中欄位名稱對應至物件的「索引鍵」部分，而「值」部分則遞迴地對應至物件的值部分。</span><span class="sxs-lookup"><span data-stu-id="67eef-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="67eef-802">請考量下列範例：建立的 Family 物件會對應至 JSON 文件 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="67eef-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="67eef-803">而反之亦然，JSON 文件會對應回 .NET 物件。</span><span class="sxs-lookup"><span data-stu-id="67eef-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="67eef-804">**C# 類別**</span><span class="sxs-lookup"><span data-stu-id="67eef-804">**C# Class**</span></span>

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


<span data-ttu-id="67eef-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="67eef-805">**JSON**</span></span>  

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



### <a name="linq-to-sql-translation"></a><span data-ttu-id="67eef-806">LINQ 至 SQL 轉譯</span><span class="sxs-lookup"><span data-stu-id="67eef-806">LINQ to SQL translation</span></span>
<span data-ttu-id="67eef-807">Cosmos DB 查詢提供者會盡力將 LINQ 查詢對應至 Cosmos DB SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="67eef-808">在下列描述中，我們假設讀者對 LINQ 有基本的認識。</span><span class="sxs-lookup"><span data-stu-id="67eef-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="67eef-809">首先，針對類型系統，我們支援所有 JSON 基本類型：數值類型、布林值、字串及 null。</span><span class="sxs-lookup"><span data-stu-id="67eef-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="67eef-810">只支援這些 JSON 類型。</span><span class="sxs-lookup"><span data-stu-id="67eef-810">Only these JSON types are supported.</span></span> <span data-ttu-id="67eef-811">下列是支援的純量運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="67eef-812">常數值：這些包括評估查詢時之基本資料類型的常數值。</span><span class="sxs-lookup"><span data-stu-id="67eef-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="67eef-813">屬性/陣列索引運算式：這些運算式參照物件或陣列項目的屬性。</span><span class="sxs-lookup"><span data-stu-id="67eef-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="67eef-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span><span class="sxs-lookup"><span data-stu-id="67eef-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="67eef-815">算術運算式：這些包括數值和布林值的一般算術運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="67eef-816">如需完整清單，請參閱 SQL 規格。</span><span class="sxs-lookup"><span data-stu-id="67eef-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="67eef-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="67eef-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="67eef-818">字串比較運算式：這些包括比較字串值與某個常數字串值。</span><span class="sxs-lookup"><span data-stu-id="67eef-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="67eef-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span><span class="sxs-lookup"><span data-stu-id="67eef-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="67eef-820">物件/陣列建立運算式：這些運算式傳回複合值類型或匿名類型的物件，或是這類物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="67eef-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="67eef-821">這些值可以是巢狀值。</span><span class="sxs-lookup"><span data-stu-id="67eef-821">These values can be nested.</span></span>
  
     <span data-ttu-id="67eef-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //含有兩個欄位的匿名類型</span><span class="sxs-lookup"><span data-stu-id="67eef-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="67eef-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="67eef-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="67eef-824"><a id="SupportedLinqOperators"></a>支援的 LINQ 運算子清單</span><span class="sxs-lookup"><span data-stu-id="67eef-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="67eef-825">以下是隨附於 DocumentDB.NET SDK 之 LINQ 提供者中支援的 LINQ 運算子清單。</span><span class="sxs-lookup"><span data-stu-id="67eef-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="67eef-826">**Select**：投影會轉譯為包括物件建構的 SQL SELECT</span><span class="sxs-lookup"><span data-stu-id="67eef-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="67eef-827">**Where**：篩選會轉譯為 SQL WHERE，並支援 &&、|| 及 ! 之間的轉譯</span><span class="sxs-lookup"><span data-stu-id="67eef-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="67eef-828">到 SQL 運算子之間的轉譯</span><span class="sxs-lookup"><span data-stu-id="67eef-828">to the SQL operators</span></span>
* <span data-ttu-id="67eef-829">**SelectMany**：可讓陣列回溯到 SQL JOIN 子句。</span><span class="sxs-lookup"><span data-stu-id="67eef-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="67eef-830">可用來鏈結/巢串運算式來篩選陣列元素</span><span class="sxs-lookup"><span data-stu-id="67eef-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="67eef-831">**OrderBy 和 OrderByDescending**：轉譯為 ORDER BY 遞增/遞減順序</span><span class="sxs-lookup"><span data-stu-id="67eef-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="67eef-832">彙總的 **Count**、**Sum**、**Min**、**Max** 與 **Average** 運算子，以及其非同步對應項 **CountAsync**、**SumAsync**、**MinAsync**、**MaxAsync** 與 **AverageAsync**。</span><span class="sxs-lookup"><span data-stu-id="67eef-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="67eef-833">**CompareTo**：轉譯為範圍比較。</span><span class="sxs-lookup"><span data-stu-id="67eef-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="67eef-834">通常用於字串，因為字串在 .NET 中是無法比較的</span><span class="sxs-lookup"><span data-stu-id="67eef-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="67eef-835">**Take**：轉譯為 SQL TOP，以限制查詢的結果</span><span class="sxs-lookup"><span data-stu-id="67eef-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="67eef-836">**數學函數**：支援從 .NET 的 Abs、Acos、Asin、Atan、Ceiling、Cos、Exp、Floor、Log、Log10、Pow、Round、Sign、Sin、Sqrt、Tan、Truncate 轉譯為對等的 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="67eef-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="67eef-837">**字串函數**：支援從 .NET 的 Concat、Contains、EndsWith、IndexOf、Count、ToLower、TrimStart、Replace、Reverse、TrimEnd、StartsWith、SubString、ToUpper 轉譯為對等的 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="67eef-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="67eef-838">**陣列函數**：支援從 .NET 的 Concat、Contains 和 Count 轉譯為對等的 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="67eef-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="67eef-839">**地理空間擴充函數**：支援從虛設常式方法 Distance、Within、IsValid 及 IsValidDetailed 轉譯為對等的 SQL 內建函式。</span><span class="sxs-lookup"><span data-stu-id="67eef-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="67eef-840">**使用者定義函式的擴充函式**：支援從 Stub 方法 UserDefinedFunctionProvider.Invoke 轉譯為對應的使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="67eef-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="67eef-841">**其他**：支援聯合和條件式運算子的轉譯。</span><span class="sxs-lookup"><span data-stu-id="67eef-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="67eef-842">可根據內容將 Contains 轉譯為字串 CONTAINS、ARRAY_CONTAINS 或 SQL IN。</span><span class="sxs-lookup"><span data-stu-id="67eef-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="67eef-843">SQL 查詢運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-843">SQL query operators</span></span>
<span data-ttu-id="67eef-844">以下是一些範例，說明如何將一些標準 LINQ 查詢運算子一路轉譯成 Cosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="67eef-845">Select 運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-845">Select Operator</span></span>
<span data-ttu-id="67eef-846">語法為 `input.Select(x => f(x))`，其中 `f` 是純量運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="67eef-847">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="67eef-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="67eef-849">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="67eef-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="67eef-851">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="67eef-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="67eef-853">SelectMany 運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-853">SelectMany operator</span></span>
<span data-ttu-id="67eef-854">語法為 `input.SelectMany(x => f(x))`，其中 `f` 是傳回集合類型的純量運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="67eef-855">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="67eef-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="67eef-857">Where 運算子</span><span class="sxs-lookup"><span data-stu-id="67eef-857">Where operator</span></span>
<span data-ttu-id="67eef-858">語法為 `input.Where(x => f(x))`，其中 `f` 是傳回布林值的純量運算式。</span><span class="sxs-lookup"><span data-stu-id="67eef-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="67eef-859">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="67eef-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="67eef-861">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="67eef-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="67eef-863">複合 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="67eef-863">Composite SQL queries</span></span>
<span data-ttu-id="67eef-864">您可以包含上述的運算子，以形成功能更強大的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="67eef-865">由於 Cosmos DB 支援巢狀集合，因此這個組合可以採用串連或巢狀的形式。</span><span class="sxs-lookup"><span data-stu-id="67eef-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="67eef-866">串連</span><span class="sxs-lookup"><span data-stu-id="67eef-866">Concatenation</span></span>
<span data-ttu-id="67eef-867">語法為 `input(.|.SelectMany())(.Select()|.Where())*`。</span><span class="sxs-lookup"><span data-stu-id="67eef-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="67eef-868">串連查詢的開頭可以是選用的 `SelectMany` 查詢，其後接著多個 `Select` 或 `Where` 運算子。</span><span class="sxs-lookup"><span data-stu-id="67eef-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="67eef-869">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="67eef-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="67eef-871">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="67eef-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="67eef-873">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="67eef-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="67eef-875">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="67eef-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="67eef-877">巢狀</span><span class="sxs-lookup"><span data-stu-id="67eef-877">Nesting</span></span>
<span data-ttu-id="67eef-878">語法為 `input.SelectMany(x=>x.Q())`，其中 Q 是 `Select`、`SelectMany` 或 `Where` 運算子。</span><span class="sxs-lookup"><span data-stu-id="67eef-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="67eef-879">在巢狀查詢中，會將內部查詢套用至外部集合的每個項目。</span><span class="sxs-lookup"><span data-stu-id="67eef-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="67eef-880">其中一個重要功能是內部查詢可以參照外部集合中項目的欄位 (例如自我聯結)。</span><span class="sxs-lookup"><span data-stu-id="67eef-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="67eef-881">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="67eef-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="67eef-883">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="67eef-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="67eef-885">**LINQ Lambda 運算式**</span><span class="sxs-lookup"><span data-stu-id="67eef-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="67eef-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="67eef-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="67eef-887"><a id="ExecutingSqlQueries"></a>執行 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="67eef-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="67eef-888">Cosmos DB 公開資源的方式是透過 REST API，任何能夠發出 HTTP/HTTPS 要求的語言都可呼叫此 API。</span><span class="sxs-lookup"><span data-stu-id="67eef-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="67eef-889">此外，Cosmos DB 還為數種熱門語言 (例如 .NET、Node.js、JavaScript 和 Python) 提供程式設計程式庫。</span><span class="sxs-lookup"><span data-stu-id="67eef-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="67eef-890">REST API 和各種程式庫都支援透過 SQL 進行查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="67eef-891">.NET SDK 除了 SQL 之外，也支援 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="67eef-892">下列範例顯示如何建立查詢，並針對 Cosmos DB 資料庫帳戶提交它。</span><span class="sxs-lookup"><span data-stu-id="67eef-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="67eef-893"><a id="RestAPI"></a>REST API</span><span class="sxs-lookup"><span data-stu-id="67eef-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="67eef-894">Cosmos DB 提供透過 HTTP 的開放 RESTful 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="67eef-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="67eef-895">可以使用 Azure 訂用帳戶佈建資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="67eef-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="67eef-896">Cosmos DB 資源模型包含某個資料庫帳戶下的一組資源，其中每個資源都可透過邏輯和穩定 URI 來定址。</span><span class="sxs-lookup"><span data-stu-id="67eef-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="67eef-897">在本文件中，一組資源稱為摘要。</span><span class="sxs-lookup"><span data-stu-id="67eef-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="67eef-898">資料庫帳戶包含一組資料庫，而每個資料庫都包含多個集合，且各集合因此會包含文件、UDF 和其他資源類型。</span><span class="sxs-lookup"><span data-stu-id="67eef-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="67eef-899">與這些資源的基本互動模型是透過具有其標準解譯的 HTTP 動詞命令 GET、PUT、POST 和 DELETE。</span><span class="sxs-lookup"><span data-stu-id="67eef-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="67eef-900">POST 動詞命令可用於建立新的資源、執行預存程序或發出 Cosmos DB 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="67eef-901">查詢一律是唯讀作業，而且沒有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="67eef-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="67eef-902">下列範例示範針對集合進行之 DocumentDB API 查詢的 POST，此集合包含我們到目前為止檢閱過的兩個範例文件。</span><span class="sxs-lookup"><span data-stu-id="67eef-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="67eef-903">查詢具有 JSON 名稱屬性的簡單篩選。</span><span class="sxs-lookup"><span data-stu-id="67eef-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="67eef-904">請注意 `x-ms-documentdb-isquery` 和內容類型的用法：`application/query+json` 標頭表示該作業是一項查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="67eef-905">**要求**</span><span class="sxs-lookup"><span data-stu-id="67eef-905">**Request**</span></span>

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


<span data-ttu-id="67eef-906">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-906">**Results**</span></span>

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


<span data-ttu-id="67eef-907">第二個範例顯示透過聯結傳回多個結果的較複雜查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="67eef-908">**要求**</span><span class="sxs-lookup"><span data-stu-id="67eef-908">**Request**</span></span>

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


<span data-ttu-id="67eef-909">**結果**</span><span class="sxs-lookup"><span data-stu-id="67eef-909">**Results**</span></span>

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


<span data-ttu-id="67eef-910">如果查詢的結果無法放入結果的單一頁面內，則 REST API 會透過 `x-ms-continuation-token` 傳回接續 Token。</span><span class="sxs-lookup"><span data-stu-id="67eef-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="67eef-911">用戶端可以透過在後續結果中包括標頭，以將結果分頁。</span><span class="sxs-lookup"><span data-stu-id="67eef-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="67eef-912">每頁的結果數目也可以透過 `x-ms-max-item-count` 數字標頭來控制。</span><span class="sxs-lookup"><span data-stu-id="67eef-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="67eef-913">如果指定的查詢有一個彙總函數 (如 `COUNT`)，則查詢頁面可對結果頁面傳回部分彙總的值。</span><span class="sxs-lookup"><span data-stu-id="67eef-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="67eef-914">用戶端必須對這些結果執行第二層彙總以產生最終結果，例如，對個別頁面中傳回的計數執行加總以傳回總計數。</span><span class="sxs-lookup"><span data-stu-id="67eef-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="67eef-915">若要管理查詢的資料一致性原則，請使用 `x-ms-consistency-level` 標頭 (例如，所有 REST API 要求)。</span><span class="sxs-lookup"><span data-stu-id="67eef-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="67eef-916">針對工作階段一致性，也需要在查詢要求中回應最新的 `x-ms-session-token` Cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="67eef-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="67eef-917">所查詢集合的索引原則也可能影響查詢結果的一致性。</span><span class="sxs-lookup"><span data-stu-id="67eef-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="67eef-918">運用預設的索引原則設定，集合的索引一律具有最新文件內容，而且查詢結果會符合針對資料所選擇的一致性。</span><span class="sxs-lookup"><span data-stu-id="67eef-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="67eef-919">如果編索引原則放寬為 Lazy，則查詢可能會傳回過時的結果。</span><span class="sxs-lookup"><span data-stu-id="67eef-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="67eef-920">如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級][consistency-levels]。</span><span class="sxs-lookup"><span data-stu-id="67eef-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="67eef-921">如果集合上所設定的索引原則無法支援指定的查詢，Azure Cosmos DB 伺服器就會傳回 400「錯誤的要求」。</span><span class="sxs-lookup"><span data-stu-id="67eef-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="67eef-922">針對範圍查詢 (針對雜湊 (相等) 查閱所設定的路徑) 以及明確地排除不進行編製索引的路徑，會傳回此訊息。</span><span class="sxs-lookup"><span data-stu-id="67eef-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="67eef-923">`x-ms-documentdb-query-enable-scan` 標頭可以指定成允許查詢在無法使用索引時執行掃描。</span><span class="sxs-lookup"><span data-stu-id="67eef-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="67eef-924">您也可以藉由將 `x-ms-documentdb-populatequerymetrics` 標頭設為 `True`，在查詢執行期間取得詳細的計量。</span><span class="sxs-lookup"><span data-stu-id="67eef-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="67eef-925">如需詳細資訊，請參閱[適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢計量](documentdb-sql-query-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="67eef-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="67eef-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="67eef-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="67eef-927">.NET SDK 支援 LINQ 和 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="67eef-928">下列範例顯示如何執行稍早在本文件中介紹的簡單篩選查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="67eef-929">此範例會比較每個文件內的兩個屬性是否相等，以及使用匿名投射。</span><span class="sxs-lookup"><span data-stu-id="67eef-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="67eef-930">下一個範例顯示聯結 (透過 LINQ SelectMany 表示)。</span><span class="sxs-lookup"><span data-stu-id="67eef-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="67eef-931">.NET 用戶端會在 foreach 區塊中自動逐一查看查詢結果的所有頁面 (如上所示)。</span><span class="sxs-lookup"><span data-stu-id="67eef-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="67eef-932">.NET SDK 中也提供 REST API 小節所介紹的查詢選項，方法是在 CreateDocumentQuery 方法中使用 `FeedOptions` and `FeedResponse` 類別。</span><span class="sxs-lookup"><span data-stu-id="67eef-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="67eef-933">頁數可以透過 `MaxItemCount` 設定來控制。</span><span class="sxs-lookup"><span data-stu-id="67eef-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="67eef-934">您也可以明確地控制分頁，方法是使用 `IQueryable` 物件來建立 `IDocumentQueryable`，然後讀取 ` ResponseContinuationToken` 值，並將它們以 `RequestContinuationToken` 的形式在 `FeedOptions` 中傳回。</span><span class="sxs-lookup"><span data-stu-id="67eef-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="67eef-935">`EnableScanInQuery` 可以設定為在設定的索引編製原則不支援查詢時啟用掃描。</span><span class="sxs-lookup"><span data-stu-id="67eef-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="67eef-936">對於已分割的集合，您可以使用 `PartitionKey` 來針對單一分割區執行查詢 (雖然 Cosmos DB 可以從查詢文字自動擷取)，以及使用 `EnableCrossPartitionQuery` 以執行可能需要針對多個分割區執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="67eef-937">如需更多包含查詢的範例，請參閱 [Azure Cosmos DB .NET 範例](https://github.com/Azure/azure-documentdb-net)。</span><span class="sxs-lookup"><span data-stu-id="67eef-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="67eef-938"><a id="JavaScriptServerSideApi"></a>JavaScript 伺服器端 API</span><span class="sxs-lookup"><span data-stu-id="67eef-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="67eef-939">Cosmos DB 提供一個程式設計模型，可使用預存程序和觸發程序，直接對集合執行 JavaScript 型應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="67eef-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="67eef-940">在集合層級註冊的 JavaScript 邏輯接著可以對給定集合之文件的作業發出資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="67eef-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="67eef-941">這些作業會包裝在環境 ACID 交易中。</span><span class="sxs-lookup"><span data-stu-id="67eef-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="67eef-942">下列範例示範如何在 JavaScript 伺服器 API 中使用 queryDocuments，從預存程序和觸發程序內發出查詢。</span><span class="sxs-lookup"><span data-stu-id="67eef-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

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

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="67eef-943"><a id="References"></a>參考</span><span class="sxs-lookup"><span data-stu-id="67eef-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="67eef-944">[Azure Cosmos DB 簡介][introduction]</span><span class="sxs-lookup"><span data-stu-id="67eef-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="67eef-945">Azure Cosmos DB SQL 規格</span><span class="sxs-lookup"><span data-stu-id="67eef-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="67eef-946">Azure Cosmos DB .NET 範例</span><span class="sxs-lookup"><span data-stu-id="67eef-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="67eef-947">[Azure Cosmos DB 一致性層級][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="67eef-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="67eef-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="67eef-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="67eef-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="67eef-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="67eef-950">Javascript 規格 [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="67eef-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="67eef-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="67eef-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="67eef-952">大型資料庫的查詢評估技術 [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="67eef-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="67eef-953">平行關聯式資料庫系統中的查詢處理 (IEEE Computer Society Press，1994 年)</span><span class="sxs-lookup"><span data-stu-id="67eef-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="67eef-954">Lu, Ooi, Tan, 平行關聯式資料庫系統中的查詢處理 (IEEE Computer Society Press，1994 年)。</span><span class="sxs-lookup"><span data-stu-id="67eef-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="67eef-955">Christopher Olston、Benjamin Reed、Utkarsh Srivastava、Ravi Kumar、Andrew Tomkins：Pig Latin：資料處理的 Not-So-Foreign 語言，SIGMOD 2008。</span><span class="sxs-lookup"><span data-stu-id="67eef-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="67eef-956">G.</span><span class="sxs-lookup"><span data-stu-id="67eef-956">G.</span></span> <span data-ttu-id="67eef-957">Graefe。</span><span class="sxs-lookup"><span data-stu-id="67eef-957">Graefe.</span></span> <span data-ttu-id="67eef-958">The Cascades framework for query optimization.</span><span class="sxs-lookup"><span data-stu-id="67eef-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="67eef-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="67eef-959">IEEE Data Eng.</span></span> <span data-ttu-id="67eef-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="67eef-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md