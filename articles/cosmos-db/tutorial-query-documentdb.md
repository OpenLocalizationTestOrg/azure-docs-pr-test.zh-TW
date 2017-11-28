---
title: "Azure Cosmos DB 中的 SQL aaaHow tooquery 嗎？ | Microsoft Docs"
description: "了解 tooquery DocumentDB SQL Azure Cosmos DB 中的資料"
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
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="7e27b-104">Azure Cosmos DB： 如何使用 SQL tooquery 嗎？</span><span class="sxs-lookup"><span data-stu-id="7e27b-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="7e27b-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md)查詢使用 SQL 的文件的支援。</span><span class="sxs-lookup"><span data-stu-id="7e27b-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="7e27b-106">本文提供一個範例文件及兩個範例 SQL 查詢和結果。</span><span class="sxs-lookup"><span data-stu-id="7e27b-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="7e27b-107">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e27b-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7e27b-108">使用 SQL 來查詢資料</span><span class="sxs-lookup"><span data-stu-id="7e27b-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="7e27b-109">範例文件</span><span class="sxs-lookup"><span data-stu-id="7e27b-109">Sample document</span></span>

<span data-ttu-id="7e27b-110">本文章中的 hello SQL 查詢使用 hello 遵循範例文件。</span><span class="sxs-lookup"><span data-stu-id="7e27b-110">hello SQL queries in this article use hello following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="7e27b-111">我可以在哪裡執行 SQL 查詢？</span><span class="sxs-lookup"><span data-stu-id="7e27b-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="7e27b-112">您可以使用執行查詢 hello hello 透過 Azure 入口網站中的 hello 資料總管[REST API 和 Sdk](documentdb-sdk-dotnet.md)，甚至 hello 和[查詢遊樂場](https://www.documentdb.com/sql/demo)，現有的範例資料集上執行查詢。</span><span class="sxs-lookup"><span data-stu-id="7e27b-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="7e27b-113">如需有關 SQL 查詢的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7e27b-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="7e27b-114">SQL 查詢和 SQL 語法</span><span class="sxs-lookup"><span data-stu-id="7e27b-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="7e27b-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="7e27b-115">Prerequisites</span></span>

<span data-ttu-id="7e27b-116">本教學課程會假設您具備 Azure Cosmos DB 帳戶和集合。</span><span class="sxs-lookup"><span data-stu-id="7e27b-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="7e27b-117">不符合上述其中任何一項條件嗎？</span><span class="sxs-lookup"><span data-stu-id="7e27b-117">Don't have any of those?</span></span> <span data-ttu-id="7e27b-118">完整的 hello [5 分鐘快速入門](create-mongodb-nodejs.md)或 hello[開發人員教學課程](tutorial-develop-mongodb.md)toocreate 帳戶和集合。</span><span class="sxs-lookup"><span data-stu-id="7e27b-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="7e27b-119">範例查詢 1</span><span class="sxs-lookup"><span data-stu-id="7e27b-119">Example query 1</span></span>

<span data-ttu-id="7e27b-120">給定 hello 範例系列文件上方，下列 SQL 查詢會傳回 hello 文件符合 hello 識別碼 欄位的位置`WakefieldFamily`。</span><span class="sxs-lookup"><span data-stu-id="7e27b-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="7e27b-121">因為它是`SELECT *`陳述式，hello 查詢的 hello 輸出是 hello 完整的 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="7e27b-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="7e27b-122">**查詢**</span><span class="sxs-lookup"><span data-stu-id="7e27b-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="7e27b-123">**結果**</span><span class="sxs-lookup"><span data-stu-id="7e27b-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="7e27b-124">範例查詢 2</span><span class="sxs-lookup"><span data-stu-id="7e27b-124">Example query 2</span></span>

<span data-ttu-id="7e27b-125">hello 下一個查詢會傳回所有 hello 指定名稱的子系中 hello 系列，其識別碼符合`WakefieldFamily`依其等級。</span><span class="sxs-lookup"><span data-stu-id="7e27b-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="7e27b-126">**查詢**</span><span class="sxs-lookup"><span data-stu-id="7e27b-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="7e27b-127">**結果**</span><span class="sxs-lookup"><span data-stu-id="7e27b-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="7e27b-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e27b-128">Next steps</span></span>

<span data-ttu-id="7e27b-129">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7e27b-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7e27b-130">了解如何使用 SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="7e27b-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="7e27b-131">您現在可以如何繼續 toohello 下一個教學課程 toolearn toodistribute 資料全域。</span><span class="sxs-lookup"><span data-stu-id="7e27b-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7e27b-132">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="7e27b-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

