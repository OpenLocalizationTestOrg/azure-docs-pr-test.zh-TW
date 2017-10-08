---
title: "aaaAzure MongoDB api Cosmos DB 全域發佈教學課程 |Microsoft 文件"
description: "了解如何使用全域發佈 toosetup Azure Cosmos DB hello MongoDB API。"
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="c126f-104">如何使用全域發佈 toosetup Azure Cosmos DB hello MongoDB 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="c126f-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="c126f-105">在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello MongoDB API 連接。</span><span class="sxs-lookup"><span data-stu-id="c126f-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="c126f-106">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="c126f-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c126f-107">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c126f-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c126f-108">設定全域發佈使用 hello [MongoDB 應用程式開發介面](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c126f-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="c126f-109">確認您的地區設定使用 hello MongoDB 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="c126f-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="c126f-110">hello 雙 MongoDB 為 toorun hello 檢查您的全域組態 API 內的最簡單的方式*isMaster()* hello Mongo 殼層命令。</span><span class="sxs-lookup"><span data-stu-id="c126f-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="c126f-111">從您的 Mongo 殼層︰</span><span class="sxs-lookup"><span data-stu-id="c126f-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="c126f-112">範例結果︰</span><span class="sxs-lookup"><span data-stu-id="c126f-112">Example results:</span></span>

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="c126f-113">連接 tooa 慣用的區域使用 hello MongoDB 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="c126f-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="c126f-114">hello MongoDB API 可讓您 toospecify 集合的全域散發資料庫的讀取喜好設定。</span><span class="sxs-lookup"><span data-stu-id="c126f-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="c126f-115">針對兩者低延遲讀取和通用的高可用性，建議您設定集合的唯讀喜好設定太*接近*。</span><span class="sxs-lookup"><span data-stu-id="c126f-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="c126f-116">讀取的喜好設定的*接近*是設定的 tooread 從 hello 最接近的區域。</span><span class="sxs-lookup"><span data-stu-id="c126f-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="c126f-117">針對，主要的應用程式讀取/寫入區域與次要區域進行災害復原 (DR) 情況下，我們建議您設定您的集合讀取喜好設定太*慣用次要*。</span><span class="sxs-lookup"><span data-stu-id="c126f-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="c126f-118">讀取的喜好設定的*慣用次要*hello 主要區域無法使用時，會設定的 tooread 從 hello 次要區域。</span><span class="sxs-lookup"><span data-stu-id="c126f-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="c126f-119">最後，如果您將像是 toomanually 指定您讀取的區域。</span><span class="sxs-lookup"><span data-stu-id="c126f-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="c126f-120">您可以設定 hello 區域標記內讀取喜好設定。</span><span class="sxs-lookup"><span data-stu-id="c126f-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="c126f-121">就這麼簡單，這樣便已完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="c126f-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="c126f-122">您可以了解如何 toomanage hello 所讀取的一致性，您的全球複寫帳戶[Azure Cosmos DB 中的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="c126f-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="c126f-123">如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="c126f-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c126f-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c126f-124">Next steps</span></span>

<span data-ttu-id="c126f-125">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="c126f-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c126f-126">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c126f-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c126f-127">設定全域發佈使用 hello DocumentDB Api</span><span class="sxs-lookup"><span data-stu-id="c126f-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="c126f-128">您可以現在繼續 toohello 下一個教學課程 toolearn 如何使用在本機的 toodevelop hello Azure Cosmos DB 本機模擬器。</span><span class="sxs-lookup"><span data-stu-id="c126f-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c126f-129">與 hello 模擬器在本機開發</span><span class="sxs-lookup"><span data-stu-id="c126f-129">Develop locally with hello emulator</span></span>](local-emulator.md)
