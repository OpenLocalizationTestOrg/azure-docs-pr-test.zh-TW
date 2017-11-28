---
title: "aaaAzure Cosmos DB 做為索引鍵值存放區 – 成本概觀 |Microsoft 文件"
description: "深入了解 hello 很低成本使用 Azure Cosmos DB 做為索引鍵值存放區。"
keywords: "金鑰值存放區"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a><span data-ttu-id="376b5-104">Azure Cosmos DB 做為金鑰值存放區 – 成本概觀</span><span class="sxs-lookup"><span data-stu-id="376b5-104">Azure Cosmos DB as a key value store – Cost overview</span></span>

<span data-ttu-id="376b5-105">Azure Cosmos DB 是全域散發的多模型資料庫服務，可用來輕鬆建置具高可用性的大規模應用程式。</span><span class="sxs-lookup"><span data-stu-id="376b5-105">Azure Cosmos DB is a globally distributed, multi-model database service for building highly available, large scale applications easily.</span></span> <span data-ttu-id="376b5-106">根據預設，Azure Cosmos DB 會自動索引它內嵌，有效率地所有 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="376b5-106">By default, Azure Cosmos DB automatically indexes all hello data it ingests, efficiently.</span></span> <span data-ttu-id="376b5-107">這樣可在任何種類的資料上進行快速且一致的 [SQL](documentdb-sql-query.md) (和 [JavaScript](programming.md)) 查詢。</span><span class="sxs-lookup"><span data-stu-id="376b5-107">This enables fast and consistent [SQL](documentdb-sql-query.md) (and [JavaScript](programming.md)) queries on any kind of data.</span></span> 

<span data-ttu-id="376b5-108">本文章描述簡單寫入 Azure Cosmos DB hello 成本，並使用做為索引鍵/值存放區時，讀取作業。</span><span class="sxs-lookup"><span data-stu-id="376b5-108">This article describes hello cost of Azure Cosmos DB for simple write and read operations when it’s used as a key/value store.</span></span> <span data-ttu-id="376b5-109">寫入作業包括文件的插入、取代、刪除和更新插入。</span><span class="sxs-lookup"><span data-stu-id="376b5-109">Write operations include inserts, replaces, deletes, and upserts of documents.</span></span> <span data-ttu-id="376b5-110">除了保證 99.99%的高可用性，保證 Azure Cosmos DB 優惠 < 10 毫秒延遲讀取和 < hello （索引） 的 15 ms 延遲寫入分別在 hello 99th 百分位數。</span><span class="sxs-lookup"><span data-stu-id="376b5-110">Besides guaranteeing 99.99% high availability, Azure Cosmos DB offers guaranteed <10 ms latency for reads and <15 ms latency for hello (indexed) writes respectively, at hello 99th percentile.</span></span> 

## <a name="why-we-use-request-units-rus"></a><span data-ttu-id="376b5-111">為什麼我們要使用「要求單位」(RU)</span><span class="sxs-lookup"><span data-stu-id="376b5-111">Why we use Request Units (RUs)</span></span>

<span data-ttu-id="376b5-112">Azure DB Cosmos 效能根據 hello 金額佈建[要求單位](request-units.md)(RU) hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="376b5-112">Azure Cosmos DB performance is based on hello amount of provisioned [Request Units](request-units.md) (RU) for hello partition.</span></span> <span data-ttu-id="376b5-113">hello 佈建第二個資料粒度是和購買的俄文/sec] 與 [RUs/分鐘 ([不 toobe hello 每小時計費的問題感到困惑](https://azure.microsoft.com/pricing/details/cosmos-db/))。</span><span class="sxs-lookup"><span data-stu-id="376b5-113">hello provisioning is at a second granularity and is purchased in RUs/sec and RUs/min ([not toobe confused with hello hourly billing](https://azure.microsoft.com/pricing/details/cosmos-db/)).</span></span> <span data-ttu-id="376b5-114">RUs 應視為貨幣，可簡化 hello 佈建的 hello 應用程式所需的輸送量。</span><span class="sxs-lookup"><span data-stu-id="376b5-114">RUs should be considered as a currency that simplifies hello provisioning of required throughput for hello application.</span></span> <span data-ttu-id="376b5-115">我們的客戶不需要 toothink 區別的讀取和寫入容量單位。</span><span class="sxs-lookup"><span data-stu-id="376b5-115">Our customers do not have toothink of differentiating between read and write capacity units.</span></span> <span data-ttu-id="376b5-116">RUs hello 單一貨幣模型建立效率 tooshare 佈建的 hello 容量之間讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="376b5-116">hello single currency model of RUs creates efficiencies tooshare hello provisioned capacity between reads and writes.</span></span> <span data-ttu-id="376b5-117">此模型中佈建的容量可讓 hello 服務 tooprovide 可預測且一致的輸送量、 低延遲及高可用性保證。</span><span class="sxs-lookup"><span data-stu-id="376b5-117">This provisioned capacity model enables hello service tooprovide a predictable and consistent throughput, guaranteed low latency, and high availability.</span></span> <span data-ttu-id="376b5-118">最後，我們使用 RU toomodel 輸送量，但每個已佈建的 RU 也有定義的資源 （記憶體、 核心） 量。</span><span class="sxs-lookup"><span data-stu-id="376b5-118">Finally, we use RU toomodel throughput but each provisioned RU has also a defined amount of resources (Memory, Core).</span></span> <span data-ttu-id="376b5-119">RU/秒不只是 IOPS。</span><span class="sxs-lookup"><span data-stu-id="376b5-119">RU/sec is not only IOPS.</span></span>

<span data-ttu-id="376b5-120">做為全域分散式的資料庫系統，Cosmos DB 是 hello 加法 toohigh 可用性中提供 SLA 延遲、 輸送量和一致性，只有 Azure 的服務。</span><span class="sxs-lookup"><span data-stu-id="376b5-120">As a globally distributed database system, Cosmos DB is hello only Azure service that provides an SLA on latency, throughput, and consistency in addition toohigh availability.</span></span> <span data-ttu-id="376b5-121">您佈建的 hello 輸送量為套用的 tooeach 的 hello 與您的 Cosmos DB 資料庫帳戶相關聯的區域。</span><span class="sxs-lookup"><span data-stu-id="376b5-121">hello throughput you provision is applied tooeach of hello regions associated with your Cosmos DB database account.</span></span> <span data-ttu-id="376b5-122">Cosmos DB 針對讀取，提供多個定義完善[一致性層級](consistency-levels.md)toochoose 從的。</span><span class="sxs-lookup"><span data-stu-id="376b5-122">For reads, Cosmos DB offers multiple, well-defined [consistency levels](consistency-levels.md) for you toochoose from.</span></span> 

<span data-ttu-id="376b5-123">hello 下表顯示 hello 數目 RUs 必要的 tooperform 讀取和寫入根據文件大小 1 KB 到 100KBs 的交易。</span><span class="sxs-lookup"><span data-stu-id="376b5-123">hello following table shows hello number of RUs required tooperform read and write transactions based on document size of 1KB and 100KBs.</span></span>

|<span data-ttu-id="376b5-124">項目大小</span><span class="sxs-lookup"><span data-stu-id="376b5-124">Item Size</span></span>|<span data-ttu-id="376b5-125">1 次讀取</span><span class="sxs-lookup"><span data-stu-id="376b5-125">1 Read</span></span>|<span data-ttu-id="376b5-126">1 次寫入</span><span class="sxs-lookup"><span data-stu-id="376b5-126">1 Write</span></span>|
|-------------|------|-------|
|<span data-ttu-id="376b5-127">1 KB</span><span class="sxs-lookup"><span data-stu-id="376b5-127">1 KB</span></span>|<span data-ttu-id="376b5-128">1 RU</span><span class="sxs-lookup"><span data-stu-id="376b5-128">1 RU</span></span>|<span data-ttu-id="376b5-129">5 RU</span><span class="sxs-lookup"><span data-stu-id="376b5-129">5 RUs</span></span>|
|<span data-ttu-id="376b5-130">100 KB</span><span class="sxs-lookup"><span data-stu-id="376b5-130">100 KB</span></span>|<span data-ttu-id="376b5-131">10 RU</span><span class="sxs-lookup"><span data-stu-id="376b5-131">10 RUs</span></span>|<span data-ttu-id="376b5-132">50 RU</span><span class="sxs-lookup"><span data-stu-id="376b5-132">50 RUs</span></span>|

## <a name="cost-of-reads-and-writes"></a><span data-ttu-id="376b5-133">讀取和寫入的成本</span><span class="sxs-lookup"><span data-stu-id="376b5-133">Cost of Reads and writes</span></span>

<span data-ttu-id="376b5-134">如果您佈建 1,000 RU/秒，這數量 too3.6m RU/小時，並需要成本 $0.08 hello 小時 （在 hello 美國和歐洲）。</span><span class="sxs-lookup"><span data-stu-id="376b5-134">If you provision 1,000 RU/sec, this amounts too3.6m RU/hour and will cost $0.08 for hello hour (in hello US and Europe).</span></span> <span data-ttu-id="376b5-135">針對 1KB 大小的文件，這表示以您的佈建輸送量，您將會使用 3.6 百萬次讀取或 0.72 百萬次寫入 (3.6 百萬 RU / 5)。</span><span class="sxs-lookup"><span data-stu-id="376b5-135">For a 1KB size document, this means that you can consume 3.6m reads or 0.72m writes (3.6mRU / 5) using your provisioned throughput.</span></span> <span data-ttu-id="376b5-136">正規化的 toomillion 讀取和寫入，hello 成本是 $0.022 /m 讀取 ($0.08 / 3.6) 和 m $0.111/寫入 ($0.08 / 0.72)。</span><span class="sxs-lookup"><span data-stu-id="376b5-136">Normalized toomillion reads and writes, hello cost would be $0.022 /m reads ($0.08 / 3.6) and $0.111/m writes ($0.08 / 0.72).</span></span> <span data-ttu-id="376b5-137">每次成本 hello 1 千萬會變成最少 hello 下表所示。</span><span class="sxs-lookup"><span data-stu-id="376b5-137">hello cost per million becomes minimal as shown in hello table below.</span></span>

|<span data-ttu-id="376b5-138">項目大小</span><span class="sxs-lookup"><span data-stu-id="376b5-138">Item Size</span></span>|<span data-ttu-id="376b5-139">1 百萬次讀取</span><span class="sxs-lookup"><span data-stu-id="376b5-139">1m Read</span></span>|<span data-ttu-id="376b5-140">1 百萬次寫入</span><span class="sxs-lookup"><span data-stu-id="376b5-140">1m Write</span></span>|
|-------------|-------|--------|
|<span data-ttu-id="376b5-141">1 KB</span><span class="sxs-lookup"><span data-stu-id="376b5-141">1 KB</span></span>|<span data-ttu-id="376b5-142">$0.022</span><span class="sxs-lookup"><span data-stu-id="376b5-142">$0.022</span></span>|<span data-ttu-id="376b5-143">$0.111</span><span class="sxs-lookup"><span data-stu-id="376b5-143">$0.111</span></span>|
|<span data-ttu-id="376b5-144">100 KB</span><span class="sxs-lookup"><span data-stu-id="376b5-144">100 KB</span></span>|<span data-ttu-id="376b5-145">$0.222</span><span class="sxs-lookup"><span data-stu-id="376b5-145">$0.222</span></span>|<span data-ttu-id="376b5-146">$1.111</span><span class="sxs-lookup"><span data-stu-id="376b5-146">$1.111</span></span>|


<span data-ttu-id="376b5-147">大部分的 hello 基本 blob 或物件儲存區服務費用 $0.40 每百萬個的讀取的交易和 $5 每百萬個寫入交易。</span><span class="sxs-lookup"><span data-stu-id="376b5-147">Most of hello basic blob or object stores services charge $0.40 per million read transaction and $5 per million write transaction.</span></span> <span data-ttu-id="376b5-148">如果使用以最佳方式，Cosmos DB 可以 too98%成本比這些其他解決方案 （如 1 KB 的交易）。</span><span class="sxs-lookup"><span data-stu-id="376b5-148">If used optimally, Cosmos DB can be up too98% cheaper than these other solutions (for 1KB transactions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="376b5-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="376b5-149">Next steps</span></span>

<span data-ttu-id="376b5-150">敬請期待最佳化 Azure Cosmos DB 資源佈建的新文章。</span><span class="sxs-lookup"><span data-stu-id="376b5-150">Stay tuned for new articles on optimizing Azure Cosmos DB resource provisioning.</span></span> <span data-ttu-id="376b5-151">在同時，hello 覺得可用 toouse 我們[RU 計算機](https://www.documentdb.com/capacityplanner)。</span><span class="sxs-lookup"><span data-stu-id="376b5-151">In hello meantime, feel free toouse our [RU calculator](https://www.documentdb.com/capacityplanner).</span></span>

