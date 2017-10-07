---
title: "資料表 api aaaAzure Cosmos DB 全域發佈教學課程 |Microsoft 文件"
description: "了解如何使用全域發佈 toosetup Azure Cosmos DB hello 表格 API。"
services: cosmos-db
keywords: "全域散發, 資料表"
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="e067e-104">如何使用全域發佈 toosetup Azure Cosmos DB hello 表格 API</span><span class="sxs-lookup"><span data-stu-id="e067e-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="e067e-105">在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello 表格 API （預覽） 連接。</span><span class="sxs-lookup"><span data-stu-id="e067e-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="e067e-106">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="e067e-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e067e-107">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e067e-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="e067e-108">設定全域發佈使用 hello[表格 API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e067e-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="e067e-109">連接使用 hello 表格 API tooa 慣用的區域</span><span class="sxs-lookup"><span data-stu-id="e067e-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="e067e-110">中的順序 tootake 優點[全域發佈](distribute-data-globally.md)，用戶端應用程式可以指定 hello 排序喜好設定清單中的區域 toobe 用 tooperform 文件的作業。</span><span class="sxs-lookup"><span data-stu-id="e067e-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="e067e-111">這可藉由設定 hello `TablePreferredLocations` hello hello 預覽 Azure 儲存體 SDK 的應用程式組態中的組態值。</span><span class="sxs-lookup"><span data-stu-id="e067e-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="e067e-112">根據 hello Azure Cosmos DB 帳戶設定，目前的地區可用性與 hello 喜好設定指定的清單，大部分的最佳端點將會選擇的 hello Azure 儲存體 SDK tooperform hello 寫入和讀取作業。</span><span class="sxs-lookup"><span data-stu-id="e067e-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="e067e-113">hello`TablePreferredLocations`應包含以逗號分隔清單的慣用 （多路連接） 的位置供讀取。</span><span class="sxs-lookup"><span data-stu-id="e067e-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="e067e-114">每個用戶端執行個體可以針對低度延遲讀取 hello 慣用順序指定這些區域的子集。</span><span class="sxs-lookup"><span data-stu-id="e067e-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="e067e-115">必須使用命名 hello 區及其[顯示名稱](https://msdn.microsoft.com/library/azure/gg441293.aspx)，例如`West US`。</span><span class="sxs-lookup"><span data-stu-id="e067e-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="e067e-116">所有的讀取將會傳送 toohello 第一個可用的地區中 hello`TablePreferredLocations`清單。</span><span class="sxs-lookup"><span data-stu-id="e067e-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="e067e-117">如果 hello 要求失敗，hello 用戶端會向 hello 清單 toohello 下一個區域，失敗等等。</span><span class="sxs-lookup"><span data-stu-id="e067e-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="e067e-118">hello SDK 只會嘗試從 hello 區域中指定 tooread `TablePreferredLocations`。</span><span class="sxs-lookup"><span data-stu-id="e067e-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="e067e-119">因此，比方說，如果 hello 資料庫帳戶有三個區域，但是 hello 用戶端只會指定兩個 hello 非寫入區域`TablePreferredLocations`，然後讀取將會由 hello 寫入區域，即使在 hello 的容錯移轉的情況下提供服務。</span><span class="sxs-lookup"><span data-stu-id="e067e-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="e067e-120">hello SDK 都會自動傳送所有寫入 toohello 目前寫入的區域。</span><span class="sxs-lookup"><span data-stu-id="e067e-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="e067e-121">如果 hello`TablePreferredLocations`屬性未設定，所有的要求將由 hello 目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="e067e-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="e067e-122">就這麼簡單，這樣便已完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="e067e-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="e067e-123">您可以了解如何 toomanage hello 所讀取的一致性，您的全球複寫帳戶[Azure Cosmos DB 中的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="e067e-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="e067e-124">如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="e067e-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e067e-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e067e-125">Next steps</span></span>

<span data-ttu-id="e067e-126">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e067e-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e067e-127">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e067e-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="e067e-128">設定全域發佈使用 hello DocumentDB Api</span><span class="sxs-lookup"><span data-stu-id="e067e-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="e067e-129">您可以現在繼續 toohello 下一個教學課程 toolearn 如何使用在本機的 toodevelop hello Azure Cosmos DB 本機模擬器。</span><span class="sxs-lookup"><span data-stu-id="e067e-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e067e-130">與 hello 模擬器在本機開發</span><span class="sxs-lookup"><span data-stu-id="e067e-130">Develop locally with hello emulator</span></span>](local-emulator.md)
