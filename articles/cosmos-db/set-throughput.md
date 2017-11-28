---
title: "Azure Cosmos DB aaaProvision 輸送量 |Microsoft 文件"
description: "了解如何 tooset 佈建 Azure Cosmos DB containsers、 集合、 圖表和資料表的輸送量。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="8105c-103">設定 Azure Cosmos DB 容器的輸送量</span><span class="sxs-lookup"><span data-stu-id="8105c-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="8105c-104">您可以為您的 Azure Cosmos DB 容器 hello Azure 入口網站中設定輸送量或使用 hello 的用戶端 Sdk。</span><span class="sxs-lookup"><span data-stu-id="8105c-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="8105c-105">hello 下表列出適用於容器的 hello 輸送量：</span><span class="sxs-lookup"><span data-stu-id="8105c-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="8105c-106"><strong>單一資料分割容器</strong></span><span class="sxs-lookup"><span data-stu-id="8105c-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="8105c-107"><strong>已資料分割的容器</strong></span><span class="sxs-lookup"><span data-stu-id="8105c-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="8105c-108">輸送量下限</span><span class="sxs-lookup"><span data-stu-id="8105c-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="8105c-109">每秒 400 個要求單位</span><span class="sxs-lookup"><span data-stu-id="8105c-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="8105c-110">每秒 2,500 個要求單位</span><span class="sxs-lookup"><span data-stu-id="8105c-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="8105c-111">輸送量上限</span><span class="sxs-lookup"><span data-stu-id="8105c-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="8105c-112">每秒 10,000 個要求單位</span><span class="sxs-lookup"><span data-stu-id="8105c-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="8105c-113">無限</span><span class="sxs-lookup"><span data-stu-id="8105c-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="8105c-114">使用 Azure 入口網站 hello tooset hello 輸送量</span><span class="sxs-lookup"><span data-stu-id="8105c-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="8105c-115">在新視窗中，開啟 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8105c-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8105c-116">Hello 左列上，按一下**Azure Cosmos DB**，或按一下**更服務**hello 底部，然後捲動太**資料庫**，然後按一下 **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="8105c-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="8105c-117">選取您的 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8105c-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="8105c-118">在 hello 新視窗中，按一下 **資料總管 （預覽）** hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="8105c-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="8105c-119">在 hello 新視窗中，展開您的資料庫和容器，然後按一下**小數位數 （& s) 設定**。</span><span class="sxs-lookup"><span data-stu-id="8105c-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="8105c-120">在 hello 新視窗中，輸入 hello 新處理量值在 hello**輸送量**方塊，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="8105c-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="8105c-121">使用適用於.NET 的 hello DocumentDB API tooset hello 輸送量</span><span class="sxs-lookup"><span data-stu-id="8105c-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="8105c-122">輸送量常見問題集</span><span class="sxs-lookup"><span data-stu-id="8105c-122">Throughput FAQ</span></span>

<span data-ttu-id="8105c-123">**可以設定我比 400 RU/秒的輸送量 tooless 嗎？**</span><span class="sxs-lookup"><span data-stu-id="8105c-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="8105c-124">400 RU/秒是 hello Cosmos DB 單一資料分割的集合 （2500 RU/秒 hello 的分割區集合最小值） 上可用的最小輸送量。</span><span class="sxs-lookup"><span data-stu-id="8105c-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="8105c-125">要求單位設定以 100 RU/秒間隔，但輸送量無法設定 too100 RU/秒或任何值小於 400 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="8105c-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="8105c-126">如果您要尋找符合成本效益的方法 toodevelop 和測試 Cosmos DB 時，您可以使用可用的 hello [Azure Cosmos DB 模擬器](local-emulator.md)，其中您可以在本機部署不花一毛錢。</span><span class="sxs-lookup"><span data-stu-id="8105c-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="8105c-127">**如何設定使用 hello MongoDB API througput？**</span><span class="sxs-lookup"><span data-stu-id="8105c-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="8105c-128">沒有任何 MongoDB API 延伸模組 tooset 輸送量。</span><span class="sxs-lookup"><span data-stu-id="8105c-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="8105c-129">hello 建議 toouse hello DocumentDB API 中所示[hello DocumentDB API 使用適用於.NET 的 tooset hello 輸送量](#set-throughput-sdk)。</span><span class="sxs-lookup"><span data-stu-id="8105c-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8105c-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8105c-130">Next steps</span></span>

<span data-ttu-id="8105c-131">請參閱深入了解佈建和持續地球位小數位數以 Cosmos DB toolearn[資料分割和調整以 Cosmos DB](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="8105c-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
