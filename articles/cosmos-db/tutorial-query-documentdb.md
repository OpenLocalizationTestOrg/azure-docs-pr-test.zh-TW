---
title: "如何在 Azure Cosmos DB 中使用 SQL 進行查詢？ | Microsoft Docs"
description: "了解如何在 Azure Cosmos DB 中使用 SQL 進行 DocumentDB 資料查詢"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="62071-104">Azure Cosmos DB：如何使用 SQL 來進行查詢？</span><span class="sxs-lookup"><span data-stu-id="62071-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="62071-105">Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) 支援使用 SQL 來查詢文件。</span><span class="sxs-lookup"><span data-stu-id="62071-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="62071-106">本文提供一個範例文件及兩個範例 SQL 查詢和結果。</span><span class="sxs-lookup"><span data-stu-id="62071-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="62071-107">本文涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="62071-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="62071-108">使用 SQL 來查詢資料</span><span class="sxs-lookup"><span data-stu-id="62071-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="62071-109">範例文件</span><span class="sxs-lookup"><span data-stu-id="62071-109">Sample document</span></span>

<span data-ttu-id="62071-110">本文中的 SQL 查詢使用下列範例文件。</span><span class="sxs-lookup"><span data-stu-id="62071-110">The SQL queries in this article use the following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="62071-111">我可以在哪裡執行 SQL 查詢？</span><span class="sxs-lookup"><span data-stu-id="62071-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="62071-112">您可以使用 Azure 入口網站中的 [資料總管]、透過 [REST API 和 SDK](documentdb-sdk-dotnet.md)，甚至是 [Query Playground](https://www.documentdb.com/sql/demo) (在一組現有的範例資料上執行查詢)，來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="62071-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="62071-113">如需有關 SQL 查詢的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="62071-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="62071-114">SQL 查詢和 SQL 語法</span><span class="sxs-lookup"><span data-stu-id="62071-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="62071-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="62071-115">Prerequisites</span></span>

<span data-ttu-id="62071-116">本教學課程會假設您具備 Azure Cosmos DB 帳戶和集合。</span><span class="sxs-lookup"><span data-stu-id="62071-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="62071-117">不符合上述其中任何一項條件嗎？</span><span class="sxs-lookup"><span data-stu-id="62071-117">Don't have any of those?</span></span> <span data-ttu-id="62071-118">請完成 [5 分鐘快速入門](create-mongodb-nodejs.md)或[開發人員教學課程](tutorial-develop-mongodb.md)，以建立帳戶和集合。</span><span class="sxs-lookup"><span data-stu-id="62071-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="62071-119">範例查詢 1</span><span class="sxs-lookup"><span data-stu-id="62071-119">Example query 1</span></span>

<span data-ttu-id="62071-120">在提供上述範例家族文件的情況下，下列 SQL 查詢會傳回識別碼欄位符合 `WakefieldFamily` 的文件。</span><span class="sxs-lookup"><span data-stu-id="62071-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="62071-121">由於它是一個 `SELECT *` 陳述式，因為查詢的輸出是完整的 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="62071-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="62071-122">**查詢**</span><span class="sxs-lookup"><span data-stu-id="62071-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="62071-123">**結果**</span><span class="sxs-lookup"><span data-stu-id="62071-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="62071-124">範例查詢 2</span><span class="sxs-lookup"><span data-stu-id="62071-124">Example query 2</span></span>

<span data-ttu-id="62071-125">下一個查詢會傳回家族中識別碼符合 `WakefieldFamily` 的小孩名字，並依年級排序。</span><span class="sxs-lookup"><span data-stu-id="62071-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="62071-126">**查詢**</span><span class="sxs-lookup"><span data-stu-id="62071-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="62071-127">**結果**</span><span class="sxs-lookup"><span data-stu-id="62071-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="62071-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62071-128">Next steps</span></span>

<span data-ttu-id="62071-129">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="62071-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="62071-130">了解如何使用 SQL 來進行查詢</span><span class="sxs-lookup"><span data-stu-id="62071-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="62071-131">您現在可以繼續進行到下一個教學課程，以了解如何全域散發您的資料。</span><span class="sxs-lookup"><span data-stu-id="62071-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62071-132">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="62071-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

