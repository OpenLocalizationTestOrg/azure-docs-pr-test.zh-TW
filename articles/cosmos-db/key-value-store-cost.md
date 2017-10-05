---
title: "Azure Cosmos DB 做為金鑰值存放區 – 成本概觀 | Microsoft Docs"
description: "了解使用 Azure Cosmos DB 做為金鑰值存放區的低成本。"
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
ms.openlocfilehash: 33eef1b51a5ee00b0fa67096030ed9ce92cf768e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a><span data-ttu-id="81345-104">Azure Cosmos DB 做為金鑰值存放區 – 成本概觀</span><span class="sxs-lookup"><span data-stu-id="81345-104">Azure Cosmos DB as a key value store – Cost overview</span></span>

<span data-ttu-id="81345-105">Azure Cosmos DB 是全域散發的多模型資料庫服務，可用來輕鬆建置具高可用性的大規模應用程式。</span><span class="sxs-lookup"><span data-stu-id="81345-105">Azure Cosmos DB is a globally distributed, multi-model database service for building highly available, large scale applications easily.</span></span> <span data-ttu-id="81345-106">根據預設，Azure Cosmos DB 會自動有效率地編製它內嵌之所有資料的索引。</span><span class="sxs-lookup"><span data-stu-id="81345-106">By default, Azure Cosmos DB automatically indexes all the data it ingests, efficiently.</span></span> <span data-ttu-id="81345-107">這樣可在任何種類的資料上進行快速且一致的 [SQL](documentdb-sql-query.md) (和 [JavaScript](programming.md)) 查詢。</span><span class="sxs-lookup"><span data-stu-id="81345-107">This enables fast and consistent [SQL](documentdb-sql-query.md) (and [JavaScript](programming.md)) queries on any kind of data.</span></span> 

<span data-ttu-id="81345-108">本文說明 Azure Cosmos DB 做為金鑰值存放區時，進行簡單寫入與讀取作業的成本。</span><span class="sxs-lookup"><span data-stu-id="81345-108">This article describes the cost of Azure Cosmos DB for simple write and read operations when it’s used as a key/value store.</span></span> <span data-ttu-id="81345-109">寫入作業包括文件的插入、取代、刪除和更新插入。</span><span class="sxs-lookup"><span data-stu-id="81345-109">Write operations include inserts, replaces, deletes, and upserts of documents.</span></span> <span data-ttu-id="81345-110">除了保證 99.99% 的高可用性，Azure Cosmos DB 還分別提供保證低於 10 毫秒延遲的讀取，以及低於 15 毫秒延遲的 (索引) 寫入 (99 百分位數)。</span><span class="sxs-lookup"><span data-stu-id="81345-110">Besides guaranteeing 99.99% high availability, Azure Cosmos DB offers guaranteed <10 ms latency for reads and <15 ms latency for the (indexed) writes respectively, at the 99th percentile.</span></span> 

## <a name="why-we-use-request-units-rus"></a><span data-ttu-id="81345-111">為什麼我們要使用「要求單位」(RU)</span><span class="sxs-lookup"><span data-stu-id="81345-111">Why we use Request Units (RUs)</span></span>

<span data-ttu-id="81345-112">Azure Cosmos DB 效能是以分割區已佈建的[要求單位](request-units.md) (RU) 數量為基礎。</span><span class="sxs-lookup"><span data-stu-id="81345-112">Azure Cosmos DB performance is based on the amount of provisioned [Request Units](request-units.md) (RU) for the partition.</span></span> <span data-ttu-id="81345-113">佈建為第二個資料粒度，且以 RU/秒和 RU/分為單位購買 ([不應該與每小時計費混淆](https://azure.microsoft.com/pricing/details/cosmos-db/))。</span><span class="sxs-lookup"><span data-stu-id="81345-113">The provisioning is at a second granularity and is purchased in RUs/sec and RUs/min ([not to be confused with the hourly billing](https://azure.microsoft.com/pricing/details/cosmos-db/)).</span></span> <span data-ttu-id="81345-114">RU 應該被視為可簡化佈建應用程式必要輸送量的貨幣。</span><span class="sxs-lookup"><span data-stu-id="81345-114">RUs should be considered as a currency that simplifies the provisioning of required throughput for the application.</span></span> <span data-ttu-id="81345-115">我們的客戶不必去區別讀取和寫入容量單位。</span><span class="sxs-lookup"><span data-stu-id="81345-115">Our customers do not have to think of differentiating between read and write capacity units.</span></span> <span data-ttu-id="81345-116">RU 的單一貨幣模型可有效率地共用讀取和寫入之間已佈建的容量。</span><span class="sxs-lookup"><span data-stu-id="81345-116">The single currency model of RUs creates efficiencies to share the provisioned capacity between reads and writes.</span></span> <span data-ttu-id="81345-117">此佈建容量模型可讓服務提供可預測且一致的輸送量、保證低延遲以及高可用性。</span><span class="sxs-lookup"><span data-stu-id="81345-117">This provisioned capacity model enables the service to provide a predictable and consistent throughput, guaranteed low latency, and high availability.</span></span> <span data-ttu-id="81345-118">最後，我們使用 RU 來建立輸送量的模型，但每個佈建的 RU 也會有定義的資源數量 (記憶體、核心)。</span><span class="sxs-lookup"><span data-stu-id="81345-118">Finally, we use RU to model throughput but each provisioned RU has also a defined amount of resources (Memory, Core).</span></span> <span data-ttu-id="81345-119">RU/秒不只是 IOPS。</span><span class="sxs-lookup"><span data-stu-id="81345-119">RU/sec is not only IOPS.</span></span>

<span data-ttu-id="81345-120">做為全域散發的資料庫系統，Cosmos DB 是除了高可用性以外，唯一就延遲、輸送量和一致性提供 SLA 的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="81345-120">As a globally distributed database system, Cosmos DB is the only Azure service that provides an SLA on latency, throughput, and consistency in addition to high availability.</span></span> <span data-ttu-id="81345-121">您所佈建的輸送量會套用到與您 Cosmos DB 資料庫帳戶相關聯的每一個區域。</span><span class="sxs-lookup"><span data-stu-id="81345-121">The throughput you provision is applied to each of the regions associated with your Cosmos DB database account.</span></span> <span data-ttu-id="81345-122">針對讀取，Cosmos DB 提供多個定義完善的[一致性層級](consistency-levels.md)，以供您選擇。</span><span class="sxs-lookup"><span data-stu-id="81345-122">For reads, Cosmos DB offers multiple, well-defined [consistency levels](consistency-levels.md) for you to choose from.</span></span> 

<span data-ttu-id="81345-123">下表顯示根據 1KB 和 100KB 的文件大小，執行讀取和寫入交易所需要的 RU 數目。</span><span class="sxs-lookup"><span data-stu-id="81345-123">The following table shows the number of RUs required to perform read and write transactions based on document size of 1KB and 100KBs.</span></span>

|<span data-ttu-id="81345-124">項目大小</span><span class="sxs-lookup"><span data-stu-id="81345-124">Item Size</span></span>|<span data-ttu-id="81345-125">1 次讀取</span><span class="sxs-lookup"><span data-stu-id="81345-125">1 Read</span></span>|<span data-ttu-id="81345-126">1 次寫入</span><span class="sxs-lookup"><span data-stu-id="81345-126">1 Write</span></span>|
|-------------|------|-------|
|<span data-ttu-id="81345-127">1 KB</span><span class="sxs-lookup"><span data-stu-id="81345-127">1 KB</span></span>|<span data-ttu-id="81345-128">1 RU</span><span class="sxs-lookup"><span data-stu-id="81345-128">1 RU</span></span>|<span data-ttu-id="81345-129">5 RU</span><span class="sxs-lookup"><span data-stu-id="81345-129">5 RUs</span></span>|
|<span data-ttu-id="81345-130">100 KB</span><span class="sxs-lookup"><span data-stu-id="81345-130">100 KB</span></span>|<span data-ttu-id="81345-131">10 RU</span><span class="sxs-lookup"><span data-stu-id="81345-131">10 RUs</span></span>|<span data-ttu-id="81345-132">50 RU</span><span class="sxs-lookup"><span data-stu-id="81345-132">50 RUs</span></span>|

## <a name="cost-of-reads-and-writes"></a><span data-ttu-id="81345-133">讀取和寫入的成本</span><span class="sxs-lookup"><span data-stu-id="81345-133">Cost of Reads and writes</span></span>

<span data-ttu-id="81345-134">如果您佈建 1,000 RU/每秒，數量會達 3.6 百萬 RU/每小時，且該小時將會花費 $0.08 (美國和歐洲)。</span><span class="sxs-lookup"><span data-stu-id="81345-134">If you provision 1,000 RU/sec, this amounts to 3.6m RU/hour and will cost $0.08 for the hour (in the US and Europe).</span></span> <span data-ttu-id="81345-135">針對 1KB 大小的文件，這表示以您的佈建輸送量，您將會使用 3.6 百萬次讀取或 0.72 百萬次寫入 (3.6 百萬 RU / 5)。</span><span class="sxs-lookup"><span data-stu-id="81345-135">For a 1KB size document, this means that you can consume 3.6m reads or 0.72m writes (3.6mRU / 5) using your provisioned throughput.</span></span> <span data-ttu-id="81345-136">標準化至百萬讀取和寫入，成本會是 $0.022/每百萬次讀取 ($0.08 / 3.6) 和 $0.111/每百萬次寫入 ($0.08 / 0.72)。</span><span class="sxs-lookup"><span data-stu-id="81345-136">Normalized to million reads and writes, the cost would be $0.022 /m reads ($0.08 / 3.6) and $0.111/m writes ($0.08 / 0.72).</span></span> <span data-ttu-id="81345-137">每百萬成本會變成最小值，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="81345-137">The cost per million becomes minimal as shown in the table below.</span></span>

|<span data-ttu-id="81345-138">項目大小</span><span class="sxs-lookup"><span data-stu-id="81345-138">Item Size</span></span>|<span data-ttu-id="81345-139">1 百萬次讀取</span><span class="sxs-lookup"><span data-stu-id="81345-139">1m Read</span></span>|<span data-ttu-id="81345-140">1 百萬次寫入</span><span class="sxs-lookup"><span data-stu-id="81345-140">1m Write</span></span>|
|-------------|-------|--------|
|<span data-ttu-id="81345-141">1 KB</span><span class="sxs-lookup"><span data-stu-id="81345-141">1 KB</span></span>|<span data-ttu-id="81345-142">$0.022</span><span class="sxs-lookup"><span data-stu-id="81345-142">$0.022</span></span>|<span data-ttu-id="81345-143">$0.111</span><span class="sxs-lookup"><span data-stu-id="81345-143">$0.111</span></span>|
|<span data-ttu-id="81345-144">100 KB</span><span class="sxs-lookup"><span data-stu-id="81345-144">100 KB</span></span>|<span data-ttu-id="81345-145">$0.222</span><span class="sxs-lookup"><span data-stu-id="81345-145">$0.222</span></span>|<span data-ttu-id="81345-146">$1.111</span><span class="sxs-lookup"><span data-stu-id="81345-146">$1.111</span></span>|


<span data-ttu-id="81345-147">大部分基本的 Blob 或物件存放區的服務收費，為每百萬次讀取交易 $0.40，以及每百萬次寫入交易 $5。</span><span class="sxs-lookup"><span data-stu-id="81345-147">Most of the basic blob or object stores services charge $0.40 per million read transaction and $5 per million write transaction.</span></span> <span data-ttu-id="81345-148">如果以最佳方式使用，Cosmos DB 可以比其他的解決方案節省多達 98% 的成本 (針對 1KB 交易)。</span><span class="sxs-lookup"><span data-stu-id="81345-148">If used optimally, Cosmos DB can be up to 98% cheaper than these other solutions (for 1KB transactions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="81345-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81345-149">Next steps</span></span>

<span data-ttu-id="81345-150">敬請期待最佳化 Azure Cosmos DB 資源佈建的新文章。</span><span class="sxs-lookup"><span data-stu-id="81345-150">Stay tuned for new articles on optimizing Azure Cosmos DB resource provisioning.</span></span> <span data-ttu-id="81345-151">在此同時，歡迎使用我們的 [RU 計算機 (英文)](https://www.documentdb.com/capacityplanner)。</span><span class="sxs-lookup"><span data-stu-id="81345-151">In the meantime, feel free to use our [RU calculator](https://www.documentdb.com/capacityplanner).</span></span>

