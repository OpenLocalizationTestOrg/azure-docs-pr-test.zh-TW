---
title: "Azure Cosmos DB： 如何使用 tooquery hello DocumentDB API 嗎？ | Microsoft Docs"
description: "了解 Azure Cosmos DB tooquery 以 hello DocumentDB API"
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
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="22618-104">Azure Cosmos DB： 如何使用 MongoDB 的 API tooquery 嗎？</span><span class="sxs-lookup"><span data-stu-id="22618-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="22618-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md)支援[MongoDB 殼層查詢](https://docs.mongodb.com/manual/tutorial/query-documents/)。</span><span class="sxs-lookup"><span data-stu-id="22618-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="22618-106">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="22618-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="22618-107">使用 MongoDB 來查詢資料</span><span class="sxs-lookup"><span data-stu-id="22618-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="22618-108">範例文件</span><span class="sxs-lookup"><span data-stu-id="22618-108">Sample document</span></span>

<span data-ttu-id="22618-109">本文章中的 hello 查詢使用 hello 遵循範例文件。</span><span class="sxs-lookup"><span data-stu-id="22618-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="22618-110"><a id="examplequery1"></a> 範例查詢 1</span><span class="sxs-lookup"><span data-stu-id="22618-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="22618-111">指定 hello 範例系列文件上方，hello 下列查詢會傳回 hello 文件，其中 hello 識別碼] 欄位必須符合`WakefieldFamily`。</span><span class="sxs-lookup"><span data-stu-id="22618-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="22618-112">**查詢**</span><span class="sxs-lookup"><span data-stu-id="22618-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="22618-113">**結果**</span><span class="sxs-lookup"><span data-stu-id="22618-113">**Results**</span></span>

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

## <span data-ttu-id="22618-114"><a id="examplequery2"></a>範例查詢 2</span><span class="sxs-lookup"><span data-stu-id="22618-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="22618-115">hello 下一個查詢會傳回 hello 系列中的 hello 子系。</span><span class="sxs-lookup"><span data-stu-id="22618-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="22618-116">**查詢**</span><span class="sxs-lookup"><span data-stu-id="22618-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="22618-117">**結果**</span><span class="sxs-lookup"><span data-stu-id="22618-117">**Results**</span></span>

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


## <span data-ttu-id="22618-118"><a id="examplequery3"></a>範例查詢 3</span><span class="sxs-lookup"><span data-stu-id="22618-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="22618-119">hello 下一個查詢會傳回所有 hello 系列註冊。</span><span class="sxs-lookup"><span data-stu-id="22618-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="22618-120">**查詢**</span><span class="sxs-lookup"><span data-stu-id="22618-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="22618-121">**結果**會傳回任何文件。</span><span class="sxs-lookup"><span data-stu-id="22618-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="22618-122"><a id="examplequery4"></a>範例查詢 4</span><span class="sxs-lookup"><span data-stu-id="22618-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="22618-123">hello 下一個查詢會傳回所有 hello 系列未註冊。</span><span class="sxs-lookup"><span data-stu-id="22618-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="22618-124">**查詢**</span><span class="sxs-lookup"><span data-stu-id="22618-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="22618-125">**結果**</span><span class="sxs-lookup"><span data-stu-id="22618-125">**Results**</span></span>

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
<span data-ttu-id="22618-126">}</span><span class="sxs-lookup"><span data-stu-id="22618-126">}</span></span>

## <span data-ttu-id="22618-127"><a id="examplequery5"></a>範例查詢 5</span><span class="sxs-lookup"><span data-stu-id="22618-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="22618-128">hello 下一個查詢會傳回所有尚未註冊 hello 系列和狀態是開頭為 NY。</span><span class="sxs-lookup"><span data-stu-id="22618-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="22618-129">**查詢**</span><span class="sxs-lookup"><span data-stu-id="22618-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="22618-130">**結果**</span><span class="sxs-lookup"><span data-stu-id="22618-130">**Results**</span></span>

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
<span data-ttu-id="22618-131">}</span><span class="sxs-lookup"><span data-stu-id="22618-131">}</span></span>


## <span data-ttu-id="22618-132"><a id="examplequery6"></a>範例查詢 6</span><span class="sxs-lookup"><span data-stu-id="22618-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="22618-133">hello 下一個查詢會傳回所有 hello 系列其中子系等級是 8。</span><span class="sxs-lookup"><span data-stu-id="22618-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="22618-134">**查詢**</span><span class="sxs-lookup"><span data-stu-id="22618-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="22618-135">**結果**</span><span class="sxs-lookup"><span data-stu-id="22618-135">**Results**</span></span>

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
<span data-ttu-id="22618-136">}</span><span class="sxs-lookup"><span data-stu-id="22618-136">}</span></span>

## <span data-ttu-id="22618-137"><a id="examplequery7"></a>範例查詢 7</span><span class="sxs-lookup"><span data-stu-id="22618-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="22618-138">hello 下一個查詢會傳回所有 hello 系列其中的子陣列的大小是 3。</span><span class="sxs-lookup"><span data-stu-id="22618-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="22618-139">**查詢**</span><span class="sxs-lookup"><span data-stu-id="22618-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="22618-140">**結果**</span><span class="sxs-lookup"><span data-stu-id="22618-140">**Results**</span></span>

<span data-ttu-id="22618-141">不會傳回任何結果，因為小孩數目不超過 2 個。</span><span class="sxs-lookup"><span data-stu-id="22618-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="22618-142">只有當參數為 2 時此查詢會成功，而傳回 hello 完整的文件。</span><span class="sxs-lookup"><span data-stu-id="22618-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22618-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22618-143">Next steps</span></span>

<span data-ttu-id="22618-144">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="22618-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="22618-145">了解如何使用 MongoDB tooquery</span><span class="sxs-lookup"><span data-stu-id="22618-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="22618-146">您現在可以如何繼續 toohello 下一個教學課程 toolearn toodistribute 資料全域。</span><span class="sxs-lookup"><span data-stu-id="22618-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="22618-147">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="22618-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

