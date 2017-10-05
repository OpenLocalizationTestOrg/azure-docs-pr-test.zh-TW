---
title: "Azure Cosmos DB：如何使用 DocumentDB API 來進行查詢？ | Microsoft Docs"
description: "了解如何使用適用於 Azure Cosmos DB 的 DocumentDB API 來進行查詢"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: feffc553a9aa931d96cec71c101674fce08a466b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-with-api-for-mongodb"></a><span data-ttu-id="4e7b9-104">Azure Cosmos DB：如何使用適用於 MongoDB 的 API 來進行查詢？</span><span class="sxs-lookup"><span data-stu-id="4e7b9-104">Azure Cosmos DB: How to query with API for MongoDB?</span></span>

<span data-ttu-id="4e7b9-105">Azure Cosmos DB [適用於 MongoDB 的 API](mongodb-introduction.md) 支援 [MongoDB 殼層查詢](https://docs.mongodb.com/manual/tutorial/query-documents/)。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="4e7b9-106">本文涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="4e7b9-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4e7b9-107">使用 MongoDB 來查詢資料</span><span class="sxs-lookup"><span data-stu-id="4e7b9-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="4e7b9-108">範例文件</span><span class="sxs-lookup"><span data-stu-id="4e7b9-108">Sample document</span></span>

<span data-ttu-id="4e7b9-109">本文中的查詢使用下列範例文件。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-109">The queries in this article use the following sample document.</span></span>

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
## <span data-ttu-id="4e7b9-110"><a id="examplequery1"></a> 範例查詢 1</span><span class="sxs-lookup"><span data-stu-id="4e7b9-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="4e7b9-111">在提供上述範例家族文件的情況下，下列查詢會傳回識別碼欄位符合 `WakefieldFamily` 的文件。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-111">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="4e7b9-112">**查詢**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="4e7b9-113">**結果**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
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
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="4e7b9-114"><a id="examplequery2"></a>範例查詢 2</span><span class="sxs-lookup"><span data-stu-id="4e7b9-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="4e7b9-115">下一個查詢會傳回家族中的所有小孩。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-115">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="4e7b9-116">**查詢**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="4e7b9-117">**結果**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
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
    ]
    }


## <span data-ttu-id="4e7b9-118"><a id="examplequery3"></a>範例查詢 3</span><span class="sxs-lookup"><span data-stu-id="4e7b9-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="4e7b9-119">下一個查詢會傳回已註冊的所有家族。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-119">The next query returns all the families which are registered.</span></span> 

<span data-ttu-id="4e7b9-120">**查詢**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="4e7b9-121">**結果**會傳回任何文件。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="4e7b9-122"><a id="examplequery4"></a>範例查詢 4</span><span class="sxs-lookup"><span data-stu-id="4e7b9-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="4e7b9-123">下一個查詢會傳回未註冊的所有家族。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-123">The next query returns all the families which are not registered.</span></span> 

<span data-ttu-id="4e7b9-124">**查詢**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="4e7b9-125">**結果**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="4e7b9-126">}</span><span class="sxs-lookup"><span data-stu-id="4e7b9-126">}</span></span>

## <span data-ttu-id="4e7b9-127"><a id="examplequery5"></a>範例查詢 5</span><span class="sxs-lookup"><span data-stu-id="4e7b9-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="4e7b9-128">下一個查詢會傳回未註冊且州別為 NY 的所有家族。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-128">The next query returns all the families which are not registered and state is NY.</span></span> 

<span data-ttu-id="4e7b9-129">**查詢**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="4e7b9-130">**結果**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="4e7b9-131">}</span><span class="sxs-lookup"><span data-stu-id="4e7b9-131">}</span></span>


## <span data-ttu-id="4e7b9-132"><a id="examplequery6"></a>範例查詢 6</span><span class="sxs-lookup"><span data-stu-id="4e7b9-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="4e7b9-133">下一個查詢會傳回小孩年級為 8 的所有家族。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-133">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="4e7b9-134">**查詢**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="4e7b9-135">**結果**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="4e7b9-136">}</span><span class="sxs-lookup"><span data-stu-id="4e7b9-136">}</span></span>

## <span data-ttu-id="4e7b9-137"><a id="examplequery7"></a>範例查詢 7</span><span class="sxs-lookup"><span data-stu-id="4e7b9-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="4e7b9-138">下一個查詢會傳回小孩陣列大小為 3 的所有家族。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-138">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="4e7b9-139">**查詢**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="4e7b9-140">**結果**</span><span class="sxs-lookup"><span data-stu-id="4e7b9-140">**Results**</span></span>

<span data-ttu-id="4e7b9-141">不會傳回任何結果，因為小孩數目不超過 2 個。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="4e7b9-142">只有當參數為 2 時，此查詢才會成功並傳回整個文件。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-142">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e7b9-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e7b9-143">Next steps</span></span>

<span data-ttu-id="4e7b9-144">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="4e7b9-144">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4e7b9-145">了解如何使用 MongoDB 來進行查詢</span><span class="sxs-lookup"><span data-stu-id="4e7b9-145">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="4e7b9-146">您現在可以繼續進行到下一個教學課程，以了解如何全域散發您的資料。</span><span class="sxs-lookup"><span data-stu-id="4e7b9-146">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e7b9-147">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="4e7b9-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

