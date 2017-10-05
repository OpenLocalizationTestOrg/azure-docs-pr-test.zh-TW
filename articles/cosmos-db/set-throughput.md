---
title: "Azure Cosmos DB 的佈建輸送量 | Microsoft Docs"
description: "了解如何設定 Azure Cosmos DB 容器、集合、圖表和資料表的佈建輸送量。"
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="d053b-103">設定 Azure Cosmos DB 容器的輸送量</span><span class="sxs-lookup"><span data-stu-id="d053b-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="d053b-104">您可以在 Azure 入口網站，或是使用用戶端 SDK，設定 Azure Cosmos DB 容器的輸送量。</span><span class="sxs-lookup"><span data-stu-id="d053b-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="d053b-105">下表列出容器可使用的輸送量：</span><span class="sxs-lookup"><span data-stu-id="d053b-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="d053b-106"><strong>單一資料分割容器</strong></span><span class="sxs-lookup"><span data-stu-id="d053b-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d053b-107"><strong>已資料分割的容器</strong></span><span class="sxs-lookup"><span data-stu-id="d053b-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d053b-108">輸送量下限</span><span class="sxs-lookup"><span data-stu-id="d053b-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d053b-109">每秒 400 個要求單位</span><span class="sxs-lookup"><span data-stu-id="d053b-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d053b-110">每秒 2,500 個要求單位</span><span class="sxs-lookup"><span data-stu-id="d053b-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d053b-111">輸送量上限</span><span class="sxs-lookup"><span data-stu-id="d053b-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d053b-112">每秒 10,000 個要求單位</span><span class="sxs-lookup"><span data-stu-id="d053b-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d053b-113">無限</span><span class="sxs-lookup"><span data-stu-id="d053b-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="d053b-114">使用 Azure 入口網站設定輸送量</span><span class="sxs-lookup"><span data-stu-id="d053b-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="d053b-115">在新的視窗中，開啟 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d053b-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d053b-116">按一下左側的 [Azure Cosmos DB]，或按一下底部的 [更多服務]，捲動至 [資料庫]，然後按一下 [Azure Cosmos DB]。</span><span class="sxs-lookup"><span data-stu-id="d053b-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="d053b-117">選取您的 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d053b-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="d053b-118">在新視窗中，按一下導覽功能表中的 [資料總管 (預覽)]。</span><span class="sxs-lookup"><span data-stu-id="d053b-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="d053b-119">在新視窗中，展開您的資料庫和容器，然後按一下 [規模與設定]。</span><span class="sxs-lookup"><span data-stu-id="d053b-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="d053b-120">在新視窗中，在 [輸送量] 方塊中輸入新的輸送量，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d053b-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="d053b-121">使用 DocumentDB API for .NET 設定輸送量</span><span class="sxs-lookup"><span data-stu-id="d053b-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="d053b-122">輸送量常見問題集</span><span class="sxs-lookup"><span data-stu-id="d053b-122">Throughput FAQ</span></span>

<span data-ttu-id="d053b-123">**我可以將輸送量設定為小於 400 RU/s 嗎？**</span><span class="sxs-lookup"><span data-stu-id="d053b-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="d053b-124">400 RU/s 是 Cosmos DB 單一資料分割集合上可用的最小輸送量 (2500 RU/s 是資料分割集合的最小值)。</span><span class="sxs-lookup"><span data-stu-id="d053b-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="d053b-125">要求單位是設定為 100 RU/s 時間間隔，但不能將輸送量設定為 100 RU/s 或任何小於 400 RU/s 的值。</span><span class="sxs-lookup"><span data-stu-id="d053b-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="d053b-126">如果您正在尋找符合成本效益的方法來開發和測試 Cosmos DB，您可以使用免費的 [Cosmos DB 模擬器](local-emulator.md)，於本機免費部署此模擬器。</span><span class="sxs-lookup"><span data-stu-id="d053b-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="d053b-127">**如何使用 MongoDB API 設定輸送量？**</span><span class="sxs-lookup"><span data-stu-id="d053b-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="d053b-128">MongoDB API 沒有可以設定輸送量的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d053b-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="d053b-129">建議使用 DocumentDB API，如[使用 DocumentDB API for .NET 設定輸送量](#set-throughput-sdk)中所述。</span><span class="sxs-lookup"><span data-stu-id="d053b-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d053b-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d053b-130">Next steps</span></span>

<span data-ttu-id="d053b-131">若要深入了解 Cosmos DB 的佈建和全球規模化，請參閱 [Cosmos DB 的資料分割和規模調整](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d053b-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
