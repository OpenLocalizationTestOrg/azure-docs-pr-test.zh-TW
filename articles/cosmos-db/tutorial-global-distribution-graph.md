---
title: "Graph API 的 aaaAzure Cosmos DB 全域發佈教學課程 |Microsoft 文件"
description: "了解如何使用全域發佈 toosetup Azure Cosmos DB hello Graph API。"
services: cosmos-db
keywords: "全域散發, 圖形, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="db91f-104">如何使用全域發佈 toosetup Azure Cosmos DB hello Graph API</span><span class="sxs-lookup"><span data-stu-id="db91f-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="db91f-105">在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello Graph API （預覽） 連接。</span><span class="sxs-lookup"><span data-stu-id="db91f-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="db91f-106">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="db91f-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="db91f-107">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="db91f-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="db91f-108">設定全域發佈使用 hello [Graph Api](graph-introduction.md) （預覽）</span><span class="sxs-lookup"><span data-stu-id="db91f-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="db91f-109">連接 tooa 慣用的區域使用 hello Graph API 使用 hello.NET SDK</span><span class="sxs-lookup"><span data-stu-id="db91f-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="db91f-110">hello Graph API 會公開為之上 hello DocumentDB SDK 延伸模組程式庫。</span><span class="sxs-lookup"><span data-stu-id="db91f-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="db91f-111">中的順序 tootake 優點[全域發佈](distribute-data-globally.md)，用戶端應用程式可以指定 hello 排序喜好設定清單中的區域 toobe 用 tooperform 文件的作業。</span><span class="sxs-lookup"><span data-stu-id="db91f-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="db91f-112">設定 hello 連線原則可以完成此作業。</span><span class="sxs-lookup"><span data-stu-id="db91f-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="db91f-113">根據 hello Azure Cosmos DB 帳戶設定，目前的地區可用性和 hello 喜好設定清單中指定，hello 會選擇 hello SDK tooperform 寫入和讀取作業大部分最佳端點。</span><span class="sxs-lookup"><span data-stu-id="db91f-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="db91f-114">當使用 hello Sdk 初始化連線時，會指定此喜好設定清單。</span><span class="sxs-lookup"><span data-stu-id="db91f-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="db91f-115">hello Sdk 接受選擇性參數 」 PreferredLocations"也就是 Azure 區域的排序的清單。</span><span class="sxs-lookup"><span data-stu-id="db91f-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="db91f-116">**寫入**: hello SDK 將會自動傳送所有寫入 toohello 目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="db91f-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="db91f-117">**讀取**： 所有讀取將會都傳送 toohello 第一個可用的地區 hello PreferredLocations 清單中。</span><span class="sxs-lookup"><span data-stu-id="db91f-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="db91f-118">如果 hello 要求失敗，hello 用戶端會向 hello 清單 toohello 下一個區域，失敗等等。</span><span class="sxs-lookup"><span data-stu-id="db91f-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="db91f-119">hello Sdk 將只會嘗試 tooread hello PreferredLocations 中指定的區域。</span><span class="sxs-lookup"><span data-stu-id="db91f-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="db91f-120">因此，比方說，如果 hello Cosmos DB 帳戶位在三個區域，但是 hello 用戶端只會指定兩個 hello 非寫入區域 PreferredLocations 的然後讀取會是由提供服務 hello 寫入區域，即使在 hello 的容錯移轉的情況下。</span><span class="sxs-lookup"><span data-stu-id="db91f-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="db91f-121">hello 應用程式可以確認 hello 目前寫入端點，以及讀取 hello SDK 所檢查的兩個屬性，WriteEndpoint 和 ReadEndpoint 可用 SDK 1.8 版和更新版本所選的端點。</span><span class="sxs-lookup"><span data-stu-id="db91f-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="db91f-122">如果未設定 hello PreferredLocations 屬性，將會 hello 目前寫入區域從服務的所有要求。</span><span class="sxs-lookup"><span data-stu-id="db91f-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="db91f-123">使用 hello SDK</span><span class="sxs-lookup"><span data-stu-id="db91f-123">Using hello SDK</span></span>

<span data-ttu-id="db91f-124">例如，在 hello.NET SDK，hello `ConnectionPolicy` hello 參數`DocumentClient`建構函式具有名`PreferredLocations`。</span><span class="sxs-lookup"><span data-stu-id="db91f-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="db91f-125">這個屬性可以設定區域名稱 tooa 的清單。</span><span class="sxs-lookup"><span data-stu-id="db91f-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="db91f-126">hello 顯示名稱[Azure 區域][ regions]可以指定一部分`PreferredLocations`。</span><span class="sxs-lookup"><span data-stu-id="db91f-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="db91f-127">hello hello 端點的 Url 不應視為長時間執行的常數。</span><span class="sxs-lookup"><span data-stu-id="db91f-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="db91f-128">hello 服務可能會更新這些在任何時間點。</span><span class="sxs-lookup"><span data-stu-id="db91f-128">hello service may update these at any point.</span></span> <span data-ttu-id="db91f-129">hello SDK 自動處理這項變更。</span><span class="sxs-lookup"><span data-stu-id="db91f-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="db91f-130">就這麼簡單，這樣便已完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="db91f-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="db91f-131">您可以了解如何 toomanage hello 所讀取的一致性，您的全球複寫帳戶[Azure Cosmos DB 中的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="db91f-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="db91f-132">如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="db91f-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db91f-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db91f-133">Next steps</span></span>

<span data-ttu-id="db91f-134">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="db91f-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db91f-135">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="db91f-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="db91f-136">設定全域發佈使用 hello DocumentDB Api</span><span class="sxs-lookup"><span data-stu-id="db91f-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="db91f-137">您可以現在繼續 toohello 下一個教學課程 toolearn 如何使用在本機的 toodevelop hello Azure Cosmos DB 本機模擬器。</span><span class="sxs-lookup"><span data-stu-id="db91f-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db91f-138">與 hello 模擬器在本機開發</span><span class="sxs-lookup"><span data-stu-id="db91f-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

