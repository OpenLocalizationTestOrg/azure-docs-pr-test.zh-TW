---
title: "Azure CosmosDB︰每分鐘的要求單位 (RU/m) | Microsoft Docs"
description: "了解如何藉由使用 tooreduce 成本要求每分鐘的單位。"
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
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="ac9ea-103">Azure Cosmos DB 之每分鐘的要求單位</span><span class="sxs-lookup"><span data-stu-id="ac9ea-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="ac9ea-104">Azure 的 Cosmos DB 是設計的 toohelp 您得到快速、 可預測的效能和順暢地連同您的應用程式成長的小數位數。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="ac9ea-105">您可以根據每秒和每分鐘 (RU/m) 的細微度，在 Cosmos DB 容器上佈建輸送量。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="ac9ea-106">hello 每分鐘的資料粒度的佈建的輸送量為使用的 toomanage hello 工作負載發生在每秒的資料粒度的非預期的激增。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="ac9ea-107">本文章提供 hello 佈建每分鐘 (RU/m) 的要求單位的運作方式的概觀。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="ac9ea-108">請注意，佈建 RU/m 的 hello 目標是 tooprovide 周圍預期需求 （特別是如果您需要 toorun 分析操作的資料之上） 和 spiky 工作負載的效能預測性。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="ac9ea-109">我們想要的 toohave 我們的客戶使用他們佈建，使快速調整與安心詳細 hello 輸送量。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="ac9ea-110">閱讀這篇文章之後, 您將無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="ac9ea-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="ac9ea-111">每分鐘的要求單位如何運作？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="ac9ea-112">Hello 要求單位每分鐘和秒的要求單位之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="ac9ea-113">如何 tooprovision RU/m 嗎？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="ac9ea-114">在哪種情況下應該考慮佈建每分鐘的要求單位？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="ac9ea-115">如何 toouse hello 入口網站的度量 toooptimize，我的成本和效能？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="ac9ea-116">定義哪一種要求可能會耗用 RU/m 預算？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="ac9ea-117">佈建每分鐘的要求單位 (RU/m)</span><span class="sxs-lookup"><span data-stu-id="ac9ea-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="ac9ea-118">時您提供 Azure Cosmos DB 在 hello 第二個資料粒度 （RU/秒），您會收到 hello 保證您的要求成功在低延遲，如果您的輸送量尚未超過 hello 該秒內佈建的容量。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="ac9ea-119">RU/m hello 資料粒度是在與您的要求會在該分鐘內成功的 hello 保證 hello 分鐘。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="ac9ea-120">比較 toobursting 系統中，我們會先確認您所取得的 hello 效能可預測，而您可以規劃。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="ac9ea-121">每分鐘的佈建運作方式的 hello 方式很簡單：</span><span class="sxs-lookup"><span data-stu-id="ac9ea-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="ac9ea-122">每小時及新增 tooRU/s 計費 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="ac9ea-123">如需詳細資訊，請瀏覽 Azure Cosmos DB [價格頁面](https://aka.ms/acdbpricing)。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="ac9ea-124">您可以在集合等級啟用 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="ac9ea-125">即可透過 hello Sdk （Node.js、 Java 或.Net） 或透過 hello 入口網站 （也包括 MongoDB API 工作負載）</span><span class="sxs-lookup"><span data-stu-id="ac9ea-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="ac9ea-126">當啟用 RU/m 時，針對每個 100 RU/秒佈建，您也可以取得 1000 RU/m 佈建 （hello 比率會是 10 倍）</span><span class="sxs-lookup"><span data-stu-id="ac9ea-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="ac9ea-127">在某一秒內，只有當您在該秒內已超過您的每秒佈建時，要求單位才會取用您的 RU/m 佈建</span><span class="sxs-lookup"><span data-stu-id="ac9ea-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="ac9ea-128">一次 hello 60 秒的期間內 (UTC) 結束，要每分鐘的佈建的 hello</span><span class="sxs-lookup"><span data-stu-id="ac9ea-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="ac9ea-129">只有對每個資料分割最多佈建 5,000 RU/s 的集合，才能啟用 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="ac9ea-130">如果您調整輸送量需求，而且每個資料分割達到如此高的佈建等級，您會收到警告訊息</span><span class="sxs-lookup"><span data-stu-id="ac9ea-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="ac9ea-131">以下是具體的範例，其中客戶可以佈建 10kRU/s 和 100kRU/m，在佈建 10,000 RU/s 和 100,000 RU/m 的集合上，90 秒期間的尖峰佈建 (50kRU/秒) 可節省 73% 的成本：</span><span class="sxs-lookup"><span data-stu-id="ac9ea-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="ac9ea-132">第 1 個第二個： hello RU/m 預算設定 100000</span><span class="sxs-lookup"><span data-stu-id="ac9ea-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="ac9ea-133">第 3 秒： 要求單位的耗用量已 11,010 RUs、 1,010 RUs 上方 hello RU/秒佈建期間，第二個 hello。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="ac9ea-134">因此，1,010 RUs 被扣除 hello RU/m 預算。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="ac9ea-135">98,990 RUs 可供 hello hello RU/m 預算的下一個 57 秒數</span><span class="sxs-lookup"><span data-stu-id="ac9ea-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="ac9ea-136">第 29 秒： 期間的第二個大型高峰發生 (> 高於佈建每秒 4 x) 的要求單位的 hello 耗用量，46,920 俄文。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="ac9ea-137">36,920 RUs 被扣除 92,323 RUs （28 秒） too55，403 RUs （第 29 秒） 從卸除的 hello RU/m 預算</span><span class="sxs-lookup"><span data-stu-id="ac9ea-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="ac9ea-138">61st 第二個： RU/m 預算設回 too100，000 俄文。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![圖形顯示 hello 耗用量，以及佈建 Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="ac9ea-140">使用 RU/m 指定要求單位容量</span><span class="sxs-lookup"><span data-stu-id="ac9ea-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="ac9ea-141">建立 Azure Cosmos DB 集合時，您會指定 hello 號碼的要求單位 (RU 每秒) 秒您想保留 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="ac9ea-142">您也可以決定是否要讓 tooadd RU 每分鐘。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="ac9ea-143">這可以透過 hello 入口網站或 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="ac9ea-144">透過 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="ac9ea-144">Through hello Portal</span></span>

<span data-ttu-id="ac9ea-145">佈建集合時只需要按一下，即可啟用或停用每分鐘的 RU。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![螢幕擷取畫面顯示如何在 Azure 入口網站 hello tooset RU/m](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="ac9ea-147">透過 hello SDK</span><span class="sxs-lookup"><span data-stu-id="ac9ea-147">Through hello SDK</span></span>
<span data-ttu-id="ac9ea-148">首先，這是重要 toonote RU/m 」 僅適用於下列 Sdk hello:</span><span class="sxs-lookup"><span data-stu-id="ac9ea-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="ac9ea-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="ac9ea-149">.Net 1.14.0</span></span>
* <span data-ttu-id="ac9ea-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="ac9ea-150">Java 1.11.0</span></span>
* <span data-ttu-id="ac9ea-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="ac9ea-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="ac9ea-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="ac9ea-152">Python 2.2.0</span></span>

<span data-ttu-id="ac9ea-153">以下是用來建立集合與每分鐘使用 hello.NET SDK 的第二個和 30000 要求單位每 3000 的要求單位的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="ac9ea-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="ac9ea-154">以下是變更集合 too5 hello 輸送量的程式碼片段，000 要求每秒單位數不會每分鐘使用佈建 RU hello.NET SDK:</span><span class="sxs-lookup"><span data-stu-id="ac9ea-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="ac9ea-155">適合案例</span><span class="sxs-lookup"><span data-stu-id="ac9ea-155">Good fit scenarios</span></span>

<span data-ttu-id="ac9ea-156">在本節中，我們提供一些案例的概觀，這些案例適合啟用每分鐘的要求單位。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="ac9ea-157">**開發/測試環境：**適合。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="ac9ea-158">在 hello 開發階段中，如果您要測試您的應用程式使用不同的工作負載，RU/m 可提供 hello 彈性在這個階段。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="ac9ea-159">Hello 時[模擬器](local-emulator.md)是很好的免費工具 tootest Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="ac9ea-160">不過如果您想 toostart 雲端環境中的，您將會有很大的彈性與 RU/m 臨機操作效能需求。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="ac9ea-161">您會有更多時間進行開發，不必一開始就擔心效能需求。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="ac9ea-162">我們建議您從 hello 最小 RU/秒佈建並啟用 RU/m。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="ac9ea-163">**無法預測、尖峰、每分鐘細微度的需求︰**適合 – 節省︰25-75%。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="ac9ea-164">我們看到 RU/m 提供明顯的改善，且大部分的實際執行案例都屬於這一類。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="ac9ea-165">如果您有幾次在一分鐘中具有特殊圖文集 IoT 工作負載執行的查詢時系統發出大量插入 hello 相同 time、 spiky 處理需求，您將需要額外容量。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="ac9ea-166">建議您套用以下的逐步方法，將您的資源需求最佳化。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![此圖表顯示 5 分鐘細微度的要求耗用量](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="ac9ea-168">*圖 - RU 耗用量基準測試*</span><span class="sxs-lookup"><span data-stu-id="ac9ea-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="ac9ea-169">**安心使用︰**適合 – 節省︰10-20%。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="ac9ea-170">有時候，您只想 toohave 安心，而不必擔心潛在尖峰流量和節流。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="ac9ea-171">這個功能會為您的 hello 右移一個。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-171">This feature is hello right one for you.</span></span> <span data-ttu-id="ac9ea-172">在此情況下，我們建議啟用 RU/m，並稍微降低每秒佈建。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="ac9ea-173">當您將不會嘗試 toooptimize 積極您佈建，此情況下與不同 hello 上方。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="ac9ea-174">這比較傾向於「零節流」的心態。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="ac9ea-175">重要的作業，以臨機操作的需求： 我們有時建議 tooonly 讓重要的作業存取 RU/m 預算，因此不會發生 hello 預算取用臨機操作或較不重要的作業。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="ac9ea-176">可以輕鬆地定義於 hello 一節。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="ac9ea-177">使用 hello 入口網站的度量 toooptimize 成本和效能</span><span class="sxs-lookup"><span data-stu-id="ac9ea-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="ac9ea-178">**在未來幾週 hello，我們將進一步開發監視您的輸送需求之俄文分鐘耗用量 toooptimize hello 內容。**</span><span class="sxs-lookup"><span data-stu-id="ac9ea-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="ac9ea-179">透過 hello 入口網站的度量，您可以看到您使用與 RU 規則 RU 秒中有多少分鐘。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="ac9ea-180">監視這些計量應該可以協助您將佈建最佳化。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="ac9ea-181">我們建議您如何以逐步方法 toouse RU/m tooyour 優點。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="ac9ea-182">針對每個步驟中，您應該代表您的工作負載 （它可能是小時、 天，或甚至數週） 的完整循環的 hello RU 耗用量的概觀及深入 hello 善用您佈建。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="ac9ea-183">這種方式背後的 hello 原則是的 toomake 做為您提供的輸送量可能 tooa 佈建符合您的下列效能條件的點為關閉。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![此圖表顯示 5 分鐘細微度的要求耗用量](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="ac9ea-185">toounderstand hello 最佳佈建點為您的工作負載，您需要 toounderstand:</span><span class="sxs-lookup"><span data-stu-id="ac9ea-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="ac9ea-186">取用模式︰沒有、不頻繁或持續性的尖峰？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="ac9ea-187">小 (平均 2 倍)、中、大 (平均大於 10 倍) 尖峰？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="ac9ea-188">節流要求的百分比︰您是否覺得稍微節流也沒有關係？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="ac9ea-189">如果是的話，多少才適合？</span><span class="sxs-lookup"><span data-stu-id="ac9ea-189">If so, by how much?</span></span> 

<span data-ttu-id="ac9ea-190">一旦您已識別您的目標是什麼，您將無法 tooget 接近 toohello 最佳佈建。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="ac9ea-191">tooassist，我們想 tooprovide toooptimize 您佈建方式根據 RU/m 耗用整體的指引。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="ac9ea-192">本指南不會套用 tooall 種類的工作負載，但 hello 私人預覽中的知識為基礎。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="ac9ea-193">我們可能隨著更多經驗而變更這些基準︰</span><span class="sxs-lookup"><span data-stu-id="ac9ea-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="ac9ea-194">RU/m % 使用率</span><span class="sxs-lookup"><span data-stu-id="ac9ea-194">RU/m % utilization</span></span>|<span data-ttu-id="ac9ea-195">RU/m 的使用程度</span><span class="sxs-lookup"><span data-stu-id="ac9ea-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="ac9ea-196">建議的佈建動作</span><span class="sxs-lookup"><span data-stu-id="ac9ea-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="ac9ea-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="ac9ea-197">0-1%</span></span>|<span data-ttu-id="ac9ea-198">使用率不足</span><span class="sxs-lookup"><span data-stu-id="ac9ea-198">Under utilization</span></span>|<span data-ttu-id="ac9ea-199">降低 RU/秒 tooconsume 詳細 RU/m</span><span class="sxs-lookup"><span data-stu-id="ac9ea-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="ac9ea-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="ac9ea-200">1-10%</span></span>|<span data-ttu-id="ac9ea-201">使用情況良好</span><span class="sxs-lookup"><span data-stu-id="ac9ea-201">Healthy use</span></span>|<span data-ttu-id="ac9ea-202">持續 hello 相同佈建層級嗎</span><span class="sxs-lookup"><span data-stu-id="ac9ea-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="ac9ea-203">10% 以上</span><span class="sxs-lookup"><span data-stu-id="ac9ea-203">Above 10%</span></span>|<span data-ttu-id="ac9ea-204">過度使用</span><span class="sxs-lookup"><span data-stu-id="ac9ea-204">Over utilization</span></span>|<span data-ttu-id="ac9ea-205">增加 RU/秒 toorely 較少的 RU/m</span><span class="sxs-lookup"><span data-stu-id="ac9ea-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="ac9ea-206">選取的作業可能會耗用 hello RU/m 預算</span><span class="sxs-lookup"><span data-stu-id="ac9ea-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="ac9ea-207">在要求層級，您可以也啟用/停用 RU/m 預算 tooserve hello 要求無論作業類型。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="ac9ea-208">如果規則的佈建的 Ru/秒預算一經 hello 要求無法取用 hello RU/m 預算，此要求會被調整。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="ac9ea-209">根據預設，如果啟動 RU/m 輸送量預算，則由 RU/m 預算支應任何要求。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="ac9ea-210">以下是用來停用 RU/m 預算 CRUD 和查詢作業使用 hello DocumentDB API 的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="ac9ea-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac9ea-211">Next steps</span></span>

<span data-ttu-id="ac9ea-212">在本文中，我們已描述了 Azure Cosmos DB 中的資料分割運作方式、如何建立分割集合，以及如何為您的應用程式挑選適當的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="ac9ea-213">使用 Azure Cosmos DB 執行規模和效能測試。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="ac9ea-214">如需範例，請參閱 [Azure Cosmos DB 的效能和規模測試](performance-testing.md)。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="ac9ea-215">開始撰寫程式碼以 hello [Sdk](documentdb-sdk-dotnet.md)或 hello [REST API](/rest/api/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="ac9ea-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="ac9ea-216">了解 Azure Cosmos DB 中[佈建的輸送量](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="ac9ea-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

