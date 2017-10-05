---
title: "Azure CosmosDB︰每分鐘的要求單位 (RU/m) | Microsoft Docs"
description: "了解如何利用每分鐘的要求單位降低成本。"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="ec673-103">Azure Cosmos DB 之每分鐘的要求單位</span><span class="sxs-lookup"><span data-stu-id="ec673-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="ec673-104">Azure Cosmos DB 的設計可協助您達成快速且可預測的效能，並順暢地隨著應用程式的成長而調整規模。</span><span class="sxs-lookup"><span data-stu-id="ec673-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="ec673-105">您可以根據每秒和每分鐘 (RU/m) 的細微度，在 Cosmos DB 容器上佈建輸送量。</span><span class="sxs-lookup"><span data-stu-id="ec673-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="ec673-106">根據每分鐘細微度佈建的輸送量，用來管理發生在每秒細微度的非預期工作負載尖峰。</span><span class="sxs-lookup"><span data-stu-id="ec673-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="ec673-107">本文提供每分鐘的要求單位 (RU/m) 佈建如何運作的概觀。</span><span class="sxs-lookup"><span data-stu-id="ec673-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="ec673-108">RU/m 佈建的主要目標是針對無法預期的需求和尖峰工作負載，提供可預測的效能 (尤其是如果您需要在作業資料上執行分析時)。</span><span class="sxs-lookup"><span data-stu-id="ec673-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="ec673-109">我們希望客戶盡可能取用他們佈建的輸送量，以便安心地快速調整。</span><span class="sxs-lookup"><span data-stu-id="ec673-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="ec673-110">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="ec673-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="ec673-111">每分鐘的要求單位如何運作？</span><span class="sxs-lookup"><span data-stu-id="ec673-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="ec673-112">每分鐘的要求單位和每秒的要求單位有何差異？</span><span class="sxs-lookup"><span data-stu-id="ec673-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="ec673-113">如何佈建 RU/m？</span><span class="sxs-lookup"><span data-stu-id="ec673-113">How to provision RU/m?</span></span>
* <span data-ttu-id="ec673-114">在哪種情況下應該考慮佈建每分鐘的要求單位？</span><span class="sxs-lookup"><span data-stu-id="ec673-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="ec673-115">如何使用入口網站計量將成本和效能最佳化？</span><span class="sxs-lookup"><span data-stu-id="ec673-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="ec673-116">定義哪一種要求可能會耗用 RU/m 預算？</span><span class="sxs-lookup"><span data-stu-id="ec673-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="ec673-117">佈建每分鐘的要求單位 (RU/m)</span><span class="sxs-lookup"><span data-stu-id="ec673-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="ec673-118">根據每秒細微度 (RU/s) 佈建 Azure Cosmos DB 時，只要輸送量不超過該秒內佈建的容量，就能保證您的要求會在低延遲情況下成功。</span><span class="sxs-lookup"><span data-stu-id="ec673-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="ec673-119">使用 RU/m 時，細微度為分鐘，並保證您的要求在該分鐘內會成功。</span><span class="sxs-lookup"><span data-stu-id="ec673-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="ec673-120">相較於暴增的系統，我們可確保您會獲得可預測的效能，讓您做好規劃。</span><span class="sxs-lookup"><span data-stu-id="ec673-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="ec673-121">每分鐘佈建的運作方式很簡單︰</span><span class="sxs-lookup"><span data-stu-id="ec673-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="ec673-122">除了 RU/s 之外，RU/m 還會每小時計費。</span><span class="sxs-lookup"><span data-stu-id="ec673-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="ec673-123">如需詳細資訊，請瀏覽 Azure Cosmos DB [價格頁面](https://aka.ms/acdbpricing)。</span><span class="sxs-lookup"><span data-stu-id="ec673-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="ec673-124">您可以在集合等級啟用 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ec673-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="ec673-125">這可透過 SDK (Node.js、Java 或 .Net) 或入口網站 (也包括 MongoDB API 工作負載) 完成</span><span class="sxs-lookup"><span data-stu-id="ec673-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="ec673-126">RU/m 啟用時，佈建每 100 RU/s，也會佈建 1,000 RU/m (比率為 10 倍)</span><span class="sxs-lookup"><span data-stu-id="ec673-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="ec673-127">在某一秒內，只有當您在該秒內已超過您的每秒佈建時，要求單位才會取用您的 RU/m 佈建</span><span class="sxs-lookup"><span data-stu-id="ec673-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="ec673-128">當 60 秒期間 (UTC) 結束之後，就會再填滿每分鐘佈建</span><span class="sxs-lookup"><span data-stu-id="ec673-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="ec673-129">只有對每個資料分割最多佈建 5,000 RU/s 的集合，才能啟用 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ec673-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="ec673-130">如果您調整輸送量需求，而且每個資料分割達到如此高的佈建等級，您會收到警告訊息</span><span class="sxs-lookup"><span data-stu-id="ec673-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="ec673-131">以下是具體的範例，其中客戶可以佈建 10kRU/s 和 100kRU/m，在佈建 10,000 RU/s 和 100,000 RU/m 的集合上，90 秒期間的尖峰佈建 (50kRU/秒) 可節省 73% 的成本：</span><span class="sxs-lookup"><span data-stu-id="ec673-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="ec673-132">第 1 秒︰RU/m 預算設定在 100,000</span><span class="sxs-lookup"><span data-stu-id="ec673-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="ec673-133">第 3 秒︰在該秒內，取用的要求單位是 11,010 個 RU，比 RU/s 佈建多出 1,010 個 RU。</span><span class="sxs-lookup"><span data-stu-id="ec673-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="ec673-134">因此會從 RU/m 預算中扣除 1,010 個 RU。</span><span class="sxs-lookup"><span data-stu-id="ec673-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="ec673-135">在 RU/m 預算中，接下來 57 秒有 98,990 個 RU 可用</span><span class="sxs-lookup"><span data-stu-id="ec673-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="ec673-136">第 29 秒︰在該秒內，發生極高尖峰 (比每秒佈建高出 4 倍以上)，取用的要求單位是 46,920 個 RU。</span><span class="sxs-lookup"><span data-stu-id="ec673-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="ec673-137">RU/m 預算中會扣除 36,920 個 RU，從 92,323 個 RU (第 28 秒) 降到 55,403 個 RU (第 29 秒)</span><span class="sxs-lookup"><span data-stu-id="ec673-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="ec673-138">第 61 秒︰RU/m 預算重設回 100,000 個 RU。</span><span class="sxs-lookup"><span data-stu-id="ec673-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![此圖表顯示 Azure Cosmos DB 的取用和佈建](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="ec673-140">使用 RU/m 指定要求單位容量</span><span class="sxs-lookup"><span data-stu-id="ec673-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="ec673-141">建立 Azure Cosmos DB 集合時，您可以指定想要保留給集合的每秒要求單位數 (每秒 RU)。</span><span class="sxs-lookup"><span data-stu-id="ec673-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="ec673-142">您也可以決定是否要新增每分鐘的 RU。</span><span class="sxs-lookup"><span data-stu-id="ec673-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="ec673-143">這可以透過入口網站或 SDK 來完成。</span><span class="sxs-lookup"><span data-stu-id="ec673-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="ec673-144">透過入口網站</span><span class="sxs-lookup"><span data-stu-id="ec673-144">Through the Portal</span></span>

<span data-ttu-id="ec673-145">佈建集合時只需要按一下，即可啟用或停用每分鐘的 RU。</span><span class="sxs-lookup"><span data-stu-id="ec673-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![顯示如何在 Azure 入口網站中設定 RU/m 的螢幕擷取畫面](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="ec673-147">透過 SDK</span><span class="sxs-lookup"><span data-stu-id="ec673-147">Through the SDK</span></span>
<span data-ttu-id="ec673-148">首先，必須注意 RU/m 僅適用於下列 SDK：</span><span class="sxs-lookup"><span data-stu-id="ec673-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="ec673-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="ec673-149">.Net 1.14.0</span></span>
* <span data-ttu-id="ec673-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="ec673-150">Java 1.11.0</span></span>
* <span data-ttu-id="ec673-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="ec673-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="ec673-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="ec673-152">Python 2.2.0</span></span>

<span data-ttu-id="ec673-153">以下的程式碼片段使用 .NET SDK，建立包含每秒 3,000 個要求單位和每分鐘 30,000 個要求單位的集合：</span><span class="sxs-lookup"><span data-stu-id="ec673-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="ec673-154">以下的程式碼片段使用 .NET SDK，將集合的輸送量變更為每秒 5,000 個要求單位，且不佈建每分鐘 RU：</span><span class="sxs-lookup"><span data-stu-id="ec673-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="ec673-155">適合案例</span><span class="sxs-lookup"><span data-stu-id="ec673-155">Good fit scenarios</span></span>

<span data-ttu-id="ec673-156">在本節中，我們提供一些案例的概觀，這些案例適合啟用每分鐘的要求單位。</span><span class="sxs-lookup"><span data-stu-id="ec673-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="ec673-157">**開發/測試環境：**適合。</span><span class="sxs-lookup"><span data-stu-id="ec673-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="ec673-158">在開發階段，如果您以不同的工作負載測試您的應用程式，RU/m 在這個階段會很有彈性。</span><span class="sxs-lookup"><span data-stu-id="ec673-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="ec673-159">[模擬器](local-emulator.md)是適合用來測試 Azure Cosmos DB 的免費工具。</span><span class="sxs-lookup"><span data-stu-id="ec673-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="ec673-160">不過，如果您想要從雲端環境開始，RU/m 可針對您的特殊效能需求而發揮很大的彈性。</span><span class="sxs-lookup"><span data-stu-id="ec673-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="ec673-161">您會有更多時間進行開發，不必一開始就擔心效能需求。</span><span class="sxs-lookup"><span data-stu-id="ec673-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="ec673-162">我們建議從最小的 RU/s 佈建開始，並啟用 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ec673-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="ec673-163">**無法預測、尖峰、每分鐘細微度的需求︰**適合 – 節省︰25-75%。</span><span class="sxs-lookup"><span data-stu-id="ec673-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="ec673-164">我們看到 RU/m 提供明顯的改善，且大部分的實際執行案例都屬於這一類。</span><span class="sxs-lookup"><span data-stu-id="ec673-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="ec673-165">如果您的 IoT 工作負載在一分鐘內出現幾次尖峰，且當您在系統同時進行大量插入時執行查詢，就需要更多容量來處理尖峰需求。</span><span class="sxs-lookup"><span data-stu-id="ec673-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="ec673-166">建議您套用以下的逐步方法，將您的資源需求最佳化。</span><span class="sxs-lookup"><span data-stu-id="ec673-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![此圖表顯示 5 分鐘細微度的要求耗用量](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="ec673-168">*圖 - RU 耗用量基準測試*</span><span class="sxs-lookup"><span data-stu-id="ec673-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="ec673-169">**安心使用︰**適合 – 節省︰10-20%。</span><span class="sxs-lookup"><span data-stu-id="ec673-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="ec673-170">有時候，您只希望安心使用，而不擔心潛在的尖峰和節流。</span><span class="sxs-lookup"><span data-stu-id="ec673-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="ec673-171">此功能非常適合您。</span><span class="sxs-lookup"><span data-stu-id="ec673-171">This feature is the right one for you.</span></span> <span data-ttu-id="ec673-172">在此情況下，我們建議啟用 RU/m，並稍微降低每秒佈建。</span><span class="sxs-lookup"><span data-stu-id="ec673-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="ec673-173">此案例中不同於上述情況，您將不會嘗試積極將佈建最佳化。</span><span class="sxs-lookup"><span data-stu-id="ec673-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="ec673-174">這比較傾向於「零節流」的心態。</span><span class="sxs-lookup"><span data-stu-id="ec673-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="ec673-175">具有特殊需求的重要作業︰有時候，我們建議只讓重要的作業取用 RU/m 預算，而不要讓特殊或不重要的作業消耗預算。</span><span class="sxs-lookup"><span data-stu-id="ec673-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="ec673-176">這可以在下一節輕鬆定義。</span><span class="sxs-lookup"><span data-stu-id="ec673-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="ec673-177">使用入口網站計量將成本和效能最佳化</span><span class="sxs-lookup"><span data-stu-id="ec673-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="ec673-178">**接下來的幾週，我們將進一步開發內容來監視 RU 分鐘耗用量，以最佳化您的輸送量需求。**</span><span class="sxs-lookup"><span data-stu-id="ec673-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="ec673-179">透過入口網站計量，您可以比較取用的一般 RU 秒數和 RU 分鐘數。</span><span class="sxs-lookup"><span data-stu-id="ec673-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="ec673-180">監視這些計量應該可以協助您將佈建最佳化。</span><span class="sxs-lookup"><span data-stu-id="ec673-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="ec673-181">我們建議採取逐步方法來決定適合您的 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ec673-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="ec673-182">針對每個步驟，您應該可以看出代表工作負載完整週期 (可能是小時、天，甚至是週) 的整體 RU 耗用量，並深入了解您佈建之項目的使用量。</span><span class="sxs-lookup"><span data-stu-id="ec673-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="ec673-183">這個方法背後的原則是讓您的輸送量佈建，盡可能接近符合下列效能準則的佈建點。</span><span class="sxs-lookup"><span data-stu-id="ec673-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![此圖表顯示 5 分鐘細微度的要求耗用量](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="ec673-185">若要了解工作負載的最佳佈建點，您需要了解︰</span><span class="sxs-lookup"><span data-stu-id="ec673-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="ec673-186">取用模式︰沒有、不頻繁或持續性的尖峰？</span><span class="sxs-lookup"><span data-stu-id="ec673-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="ec673-187">小 (平均 2 倍)、中、大 (平均大於 10 倍) 尖峰？</span><span class="sxs-lookup"><span data-stu-id="ec673-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="ec673-188">節流要求的百分比︰您是否覺得稍微節流也沒有關係？</span><span class="sxs-lookup"><span data-stu-id="ec673-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="ec673-189">如果是的話，多少才適合？</span><span class="sxs-lookup"><span data-stu-id="ec673-189">If so, by how much?</span></span> 

<span data-ttu-id="ec673-190">只要確定您的目標，就更能夠接近最佳佈建。</span><span class="sxs-lookup"><span data-stu-id="ec673-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="ec673-191">為了協助您，我們提供整體指引，讓您根據 RU/m 耗用量將佈建最佳化。</span><span class="sxs-lookup"><span data-stu-id="ec673-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="ec673-192">本指引並不適用於所有種類的工作負載，而是以私人預覽知識為主。</span><span class="sxs-lookup"><span data-stu-id="ec673-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="ec673-193">我們可能隨著更多經驗而變更這些基準︰</span><span class="sxs-lookup"><span data-stu-id="ec673-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="ec673-194">RU/m % 使用率</span><span class="sxs-lookup"><span data-stu-id="ec673-194">RU/m % utilization</span></span>|<span data-ttu-id="ec673-195">RU/m 的使用程度</span><span class="sxs-lookup"><span data-stu-id="ec673-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="ec673-196">建議的佈建動作</span><span class="sxs-lookup"><span data-stu-id="ec673-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="ec673-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="ec673-197">0-1%</span></span>|<span data-ttu-id="ec673-198">使用率不足</span><span class="sxs-lookup"><span data-stu-id="ec673-198">Under utilization</span></span>|<span data-ttu-id="ec673-199">降低 RU/s 以取用更多 RU/m</span><span class="sxs-lookup"><span data-stu-id="ec673-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="ec673-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="ec673-200">1-10%</span></span>|<span data-ttu-id="ec673-201">使用情況良好</span><span class="sxs-lookup"><span data-stu-id="ec673-201">Healthy use</span></span>|<span data-ttu-id="ec673-202">保持相同的佈建等級</span><span class="sxs-lookup"><span data-stu-id="ec673-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="ec673-203">10% 以上</span><span class="sxs-lookup"><span data-stu-id="ec673-203">Above 10%</span></span>|<span data-ttu-id="ec673-204">過度使用</span><span class="sxs-lookup"><span data-stu-id="ec673-204">Over utilization</span></span>|<span data-ttu-id="ec673-205">增加 RU/s 以減少依賴 RU/m</span><span class="sxs-lookup"><span data-stu-id="ec673-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="ec673-206">選取哪些作業可以取用 RU/m 預算</span><span class="sxs-lookup"><span data-stu-id="ec673-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="ec673-207">在要求等級上，您也可以啟用/停用 RU/m 預算來支應要求，而不分作業類型。</span><span class="sxs-lookup"><span data-stu-id="ec673-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="ec673-208">如果取用一般佈建的 RU/秒預算，但要求無法取用 RU/m 預算，將會節流處理此要求。</span><span class="sxs-lookup"><span data-stu-id="ec673-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="ec673-209">根據預設，如果啟動 RU/m 輸送量預算，則由 RU/m 預算支應任何要求。</span><span class="sxs-lookup"><span data-stu-id="ec673-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="ec673-210">以下的程式碼片段使用 DocumentDB API，停用 CRUD 和查詢作業的 RU/m 預算。</span><span class="sxs-lookup"><span data-stu-id="ec673-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="ec673-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec673-211">Next steps</span></span>

<span data-ttu-id="ec673-212">在本文中，我們已描述了 Azure Cosmos DB 中的資料分割運作方式、如何建立分割集合，以及如何為您的應用程式挑選適當的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ec673-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="ec673-213">使用 Azure Cosmos DB 執行規模和效能測試。</span><span class="sxs-lookup"><span data-stu-id="ec673-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="ec673-214">如需範例，請參閱[使用 Azure Cosmos DB 執行效能和規模測試](performance-testing.md)。</span><span class="sxs-lookup"><span data-stu-id="ec673-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="ec673-215">使用 [SDK](documentdb-sdk-dotnet.md) 或 [REST API](/rest/api/documentdb/) 開始撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="ec673-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="ec673-216">了解 Azure Cosmos DB 中[佈建的輸送量](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="ec673-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

