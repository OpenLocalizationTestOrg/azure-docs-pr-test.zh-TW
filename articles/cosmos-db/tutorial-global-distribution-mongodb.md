---
title: "適用於 MongoDB API 的 Azure Cosmos DB 全域散發教學課程 | Microsoft Docs"
description: "了解如何使用 MongoDB API 來設定 Azure Cosmos DB 全域散發。"
services: cosmos-db
keywords: "全域散發, MongoDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="61643-104">如何使用 MongoDB API 來設定 Azure Cosmos DB 全域散發</span><span class="sxs-lookup"><span data-stu-id="61643-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="61643-105">在本文中，我們會說明如何使用 Azure 入口網站來設定 Azure Cosmos DB 全域散發，然後使用 MongoDB API 來進行連線。</span><span class="sxs-lookup"><span data-stu-id="61643-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="61643-106">本文涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="61643-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="61643-107">使用 Azure 入口網站來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="61643-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="61643-108">使用 [MongoDB API](mongodb-introduction.md) 來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="61643-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="61643-109">使用 MongoDB API 來確認您的區域設定</span><span class="sxs-lookup"><span data-stu-id="61643-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="61643-110">若要在 API for MongoDB 內仔細檢查檢查您的全球組態，最簡單的方法就是從 Mongo 殼層執行 *isMaster()* 命令。</span><span class="sxs-lookup"><span data-stu-id="61643-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="61643-111">從您的 Mongo 殼層︰</span><span class="sxs-lookup"><span data-stu-id="61643-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="61643-112">範例結果︰</span><span class="sxs-lookup"><span data-stu-id="61643-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="61643-113">使用 MongoDB API 來連線到慣用的區域</span><span class="sxs-lookup"><span data-stu-id="61643-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="61643-114">MongoDB API 可讓您針對全域分散式資料庫，指定集合的讀取喜好設定。</span><span class="sxs-lookup"><span data-stu-id="61643-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="61643-115">為了兼顧低延遲讀取和全球高可用性，建議將集合的讀取喜好設定設為 [最接近]。</span><span class="sxs-lookup"><span data-stu-id="61643-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="61643-116">[最接近] 讀取喜好設定會設定為從最近的區域讀取。</span><span class="sxs-lookup"><span data-stu-id="61643-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="61643-117">如果應用程式具有主要讀取/寫入區域和次要地區來因應災害復原 (DR) 情況，我們建議將集合的讀取喜好設定設為 [慣用次要]。</span><span class="sxs-lookup"><span data-stu-id="61643-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="61643-118">[慣用次要] 讀取喜好設定會設定當主要區域無法使用時，從次要地區讀取。</span><span class="sxs-lookup"><span data-stu-id="61643-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="61643-119">最後，如果您想要手動指定讀取區域，</span><span class="sxs-lookup"><span data-stu-id="61643-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="61643-120">您可以在讀取喜好設定內設定區域標記。</span><span class="sxs-lookup"><span data-stu-id="61643-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="61643-121">就這麼簡單，這樣便已完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="61643-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="61643-122">您可以透過閱讀 [Azure Cosmos DB 中的一致性層級](consistency-levels.md)，來了解如何管理全域複寫帳戶的一致性。</span><span class="sxs-lookup"><span data-stu-id="61643-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="61643-123">如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="61643-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="61643-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61643-124">Next steps</span></span>

<span data-ttu-id="61643-125">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="61643-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61643-126">使用 Azure 入口網站來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="61643-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="61643-127">使用 DocumentDB API 來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="61643-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="61643-128">您現在可以繼續進行到下一個教學課程，以了解如何使用 Azure Cosmos DB 本機模擬器在本機進行開發。</span><span class="sxs-lookup"><span data-stu-id="61643-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61643-129">使用模擬器在本機進行開發</span><span class="sxs-lookup"><span data-stu-id="61643-129">Develop locally with the emulator</span></span>](local-emulator.md)