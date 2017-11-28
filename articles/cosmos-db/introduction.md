---
title: "aaaIntroduction tooAzure Cosmos DB |Microsoft 文件"
description: "了解 Azure Cosmos DB。 這個全球散發的多模型資料庫是針對低延遲、彈性的延展性和高可用性所建置。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a><span data-ttu-id="8dd65-104">歡迎使用 tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8dd65-104">Welcome tooAzure Cosmos DB</span></span>

<span data-ttu-id="8dd65-105">Azure Cosmos DB 是 Microsoft 的全球散發多模型資料庫。</span><span class="sxs-lookup"><span data-stu-id="8dd65-105">Azure Cosmos DB is Microsoft's globally distributed, multi-model database.</span></span> <span data-ttu-id="8dd65-106">Hello 按一下按鈕，使用 Azure Cosmos DB 可讓您 tooelastically 和獨立延展輸送量與儲存體在任意數目的 Azure 地理區域。</span><span class="sxs-lookup"><span data-stu-id="8dd65-106">With hello click of a button, Azure Cosmos DB enables you tooelastically and independently scale throughput and storage across any number of Azure's geographic regions.</span></span> <span data-ttu-id="8dd65-107">它利用完整的[服務等級協定](https://aka.ms/acdbsla) (SLA) 提供了輸送量、延遲、可用性和一致性的保證，這是其他資料庫服務無法提供的。</span><span class="sxs-lookup"><span data-stu-id="8dd65-107">It offers throughput, latency, availability, and consistency guarantees with comprehensive [service level agreements](https://aka.ms/acdbsla) (SLAs), something no other database service can offer.</span></span>

![Azure Cosmos DB 是 Microsoft 的全球散發資料庫服務，包含彈性的相應放大、低延遲保證、五個一致性模型，以及完整保證的 SLA](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a><span data-ttu-id="8dd65-109">受益於 Azure Cosmos DB 的解決方案</span><span class="sxs-lookup"><span data-stu-id="8dd65-109">Solutions that benefit from Azure Cosmos DB</span></span>

<span data-ttu-id="8dd65-110">任何[web、 行動裝置、 遊戲和 IoT 應用程式](use-cases.md)上需要的 toohandle 大量的讀取和寫入[全域](distribute-data-globally.md)的各種不同的資料將受益於 Azure Cosmos DB 的低回應時間調整[保證](https://azure.microsoft.com/support/legal/sla/cosmos-db/)可用性、 高輸送量、 低延遲度及可微調的一致性。</span><span class="sxs-lookup"><span data-stu-id="8dd65-110">Any [web, mobile, gaming, and IoT applications](use-cases.md) that need toohandle massive amounts of reads and writes on a [global](distribute-data-globally.md) scale with low response times for a variety of data will benefit from Azure Cosmos DB's [guaranteed](https://azure.microsoft.com/support/legal/sla/cosmos-db/) availability, high throughput, low latency, and tunable consistency.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="8dd65-111">主要功能</span><span class="sxs-lookup"><span data-stu-id="8dd65-111">Key capabilities</span></span>
<span data-ttu-id="8dd65-112">為全域分散式的資料庫服務，Azure Cosmos DB 會提供下列功能 toohelp 建置可擴充、 高回應性的應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="8dd65-112">As a globally distributed database service, Azure Cosmos DB provides hello following capabilities toohelp you build scalable, highly responsive applications:</span></span>

* <span data-ttu-id="8dd65-113">**周全且立即可用的全域分散式資料庫**</span><span class="sxs-lookup"><span data-stu-id="8dd65-113">**Turnkey global distribution**</span></span>
    * <span data-ttu-id="8dd65-114">您可以[散發資料](distribute-data-globally.md)tooany 數目[Azure 區域](https://azure.microsoft.com/regions/)，以 hello[按鈕的按一下](tutorial-global-distribution-documentdb.md)。</span><span class="sxs-lookup"><span data-stu-id="8dd65-114">You can [distribute your data](distribute-data-globally.md) tooany number of [Azure regions](https://azure.microsoft.com/regions/), with hello [click of a button](tutorial-global-distribution-documentdb.md).</span></span> <span data-ttu-id="8dd65-115">這可讓您 tooput 其中您的使用者，請確保 hello 最低可能延遲 tooyour 客戶資料。</span><span class="sxs-lookup"><span data-stu-id="8dd65-115">This enables you tooput your data where your users are, ensuring hello lowest possible latency tooyour customers.</span></span> 
    * <span data-ttu-id="8dd65-116">使用 Azure Cosmos DB 的多路連接的 Api，hello 應用程式一定會知道其中是 hello 最接近的區域，而將會傳送要求 toohello 最接近的資料中心。</span><span class="sxs-lookup"><span data-stu-id="8dd65-116">Using Azure Cosmos DB's multi-homing APIs, hello app always knows where hello nearest region is and will send requests toohello nearest data center.</span></span> <span data-ttu-id="8dd65-117">這可能會有任何組態變更、 設定寫入區域和 rest 會為您處理許多讀取並 hello 的區域。</span><span class="sxs-lookup"><span data-stu-id="8dd65-117">All of this is possible with no config changes, you set your write region and as many read regions as you want and hello rest is handled for you.</span></span>

* <span data-ttu-id="8dd65-118">**存取和查詢資料的多重資料模型與常用 API**</span><span class="sxs-lookup"><span data-stu-id="8dd65-118">**Multiple data models and popular APIs for accessing and querying data**</span></span>
    * <span data-ttu-id="8dd65-119">hello Azure Cosmos DB 上建立原生 atom 記錄順序 (ARS) 型的資料模型支援多個資料模型，包括但不是限於的 toodocument、 圖形、 索引鍵-值、 資料表和單欄式資料模型。</span><span class="sxs-lookup"><span data-stu-id="8dd65-119">hello atom-record-sequence (ARS) based data model that Azure Cosmos DB is built on natively supports multiple data models, including but not limited toodocument, graph, key-value, table, and columnar data models.</span></span>
    * <span data-ttu-id="8dd65-120">Sdk 提供多種語言支援下列資料模型的 hello 的 Api:</span><span class="sxs-lookup"><span data-stu-id="8dd65-120">APIs for hello following data models are supported with SDKs available in multiple languages:</span></span>
        * [<span data-ttu-id="8dd65-121">DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="8dd65-121">DocumentDB API</span></span>](documentdb-introduction.md)
        * [<span data-ttu-id="8dd65-122">MongoDB API</span><span class="sxs-lookup"><span data-stu-id="8dd65-122">MongoDB API</span></span>](mongodb-introduction.md)
        * [<span data-ttu-id="8dd65-123">資料表 API</span><span class="sxs-lookup"><span data-stu-id="8dd65-123">Table API</span></span>](table-introduction.md)
        * [<span data-ttu-id="8dd65-124">Graph (Gremlin) API</span><span class="sxs-lookup"><span data-stu-id="8dd65-124">Graph (Gremlin) API</span></span>](graph-introduction.md)
        * <span data-ttu-id="8dd65-125">其他資料模型即將登場</span><span class="sxs-lookup"><span data-stu-id="8dd65-125">Additional data models coming soon</span></span> 

* <span data-ttu-id="8dd65-126">**全球性依需求彈性調整輸送量和儲存體**</span><span class="sxs-lookup"><span data-stu-id="8dd65-126">**Elastically scale throughput and storage on demand, worldwide**</span></span>
    * <span data-ttu-id="8dd65-127">輕鬆地以[每秒](request-units.md)的細微度調整資料庫輸送量，並隨時依需求變更。</span><span class="sxs-lookup"><span data-stu-id="8dd65-127">Easily scale database throughput at a [per second](request-units.md) granularity, and change it anytime you want.</span></span> 
    * <span data-ttu-id="8dd65-128">調整儲存體大小[以透明且自動](partition-data.md)toohandle now 及永遠您大小需求。</span><span class="sxs-lookup"><span data-stu-id="8dd65-128">Scale storage size [transparently and automatically](partition-data.md) toohandle your size requirements now and forever.</span></span>

* <span data-ttu-id="8dd65-129">**建置回應速度快和關鍵任務應用程式**</span><span class="sxs-lookup"><span data-stu-id="8dd65-129">**Build highly responsive and mission-critical applications**</span></span>
    * <span data-ttu-id="8dd65-130">Azure Cosmos DB 可保證在 hello 的端對端低度延遲 99th 百分位數 tooits 客戶。</span><span class="sxs-lookup"><span data-stu-id="8dd65-130">Azure Cosmos DB guarantees end-to-end low latency at hello 99th percentile tooits customers.</span></span> 
    * <span data-ttu-id="8dd65-131">典型 1 KB 的項目，如 Cosmos DB 的讀取端對端延遲低於 10 毫秒與保證索引的寫入在 hello 99th 百分位數 底下 15 毫秒內 hello 相同 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="8dd65-131">For a typical 1 KB item, Cosmos DB guarantees end-to-end latency of reads under 10 ms and indexed writes under 15 ms at hello 99th percentile, within hello same Azure region.</span></span> <span data-ttu-id="8dd65-132">hello 中間延遲會大幅降低 （下 5 毫秒）。</span><span class="sxs-lookup"><span data-stu-id="8dd65-132">hello median latencies are significantly lower (under 5 ms).</span></span>

* <span data-ttu-id="8dd65-133">**確保「永遠可用」可用性**</span><span class="sxs-lookup"><span data-stu-id="8dd65-133">**Ensure "always on" availability**</span></span>
    * <span data-ttu-id="8dd65-134">單一區域內的 99.99% 可用性。</span><span class="sxs-lookup"><span data-stu-id="8dd65-134">99.99% availability within a single region.</span></span>
    * <span data-ttu-id="8dd65-135">部署 tooany 數目[Azure 區域](https://azure.microsoft.com/regions)提高可用性。</span><span class="sxs-lookup"><span data-stu-id="8dd65-135">Deploy tooany number of [Azure regions](https://azure.microsoft.com/regions) for higher availability.</span></span>
    * <span data-ttu-id="8dd65-136">透過資料零遺失保證來[模擬一或多個區域的錯誤](regional-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="8dd65-136">[Simulate a failure](regional-failover.md) of one or more regions with zero-data loss guarantees.</span></span> 

* <span data-ttu-id="8dd65-137">**撰寫全域散發的應用程式，hello 以滑鼠右鍵的方式**</span><span class="sxs-lookup"><span data-stu-id="8dd65-137">**Write globally distributed applications, hello right way**</span></span>
    * <span data-ttu-id="8dd65-138">五個[一致性模型](consistency-levels.md)模型提供廣泛的強式所有 hello 類似方式 tooNoSQL 的最終一致性，而且每個兩者之間的類似 SQL 的一致性。</span><span class="sxs-lookup"><span data-stu-id="8dd65-138">Five [consistency models](consistency-levels.md) models provide a spectrum of strong SQL-like consistency all hello way tooNoSQL-like eventual consistency, and every thing in between.</span></span> 
  
* <span data-ttu-id="8dd65-139">**退款保證**</span><span class="sxs-lookup"><span data-stu-id="8dd65-139">**Money back guarantees**</span></span>
    * <span data-ttu-id="8dd65-140">保證快速取得您的資料，否則退款。</span><span class="sxs-lookup"><span data-stu-id="8dd65-140">Your data gets there fast, or your money back.</span></span> 
    * <span data-ttu-id="8dd65-141">可用性、延遲、輸送量和一致性的[服務等級協定](https://aka.ms/acdbsla)。</span><span class="sxs-lookup"><span data-stu-id="8dd65-141">[Service level agreements](https://aka.ms/acdbsla) for availability, latency, throughput, and consistency.</span></span> 

* <span data-ttu-id="8dd65-142">**無資料庫結構描述/索引管理**</span><span class="sxs-lookup"><span data-stu-id="8dd65-142">**No database schema/index management**</span></span>
    * <span data-ttu-id="8dd65-143">不用再擔心維持您的資料庫結構描述和索引與您的應用程式結構描述之間的同步處理了。</span><span class="sxs-lookup"><span data-stu-id="8dd65-143">Stop worrying about keeping your database schema and indexes in-sync with your application’s schema.</span></span> <span data-ttu-id="8dd65-144">我們完全不需要結構描述。</span><span class="sxs-lookup"><span data-stu-id="8dd65-144">We're schema-free.</span></span> 
    * <span data-ttu-id="8dd65-145">Azure Cosmos 資料庫的資料庫引擎是完整的結構描述無關，因為它內嵌，而不需要任何結構描述或索引，並提供服務效能穩定的快速查詢的所有 hello 資料自動編製都索引。</span><span class="sxs-lookup"><span data-stu-id="8dd65-145">Azure Cosmos DB’s database engine is fully schema-agnostic – it automatically indexes all hello data it ingests without requiring any schema or indexes and serves blazing fast queries.</span></span> 

* <span data-ttu-id="8dd65-146">**降低擁有權成本**</span><span class="sxs-lookup"><span data-stu-id="8dd65-146">**Low cost of ownership**</span></span>
    * <span data-ttu-id="8dd65-147">五 tooten 次[更符合成本效益](https://aka.ms/cosmos-db-tco-paper)與未受管理的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8dd65-147">Five tooten times [more cost effective](https://aka.ms/cosmos-db-tco-paper) than a non-managed solution.</span></span>
    * <span data-ttu-id="8dd65-148">比 DynamoDB 便宜三倍。</span><span class="sxs-lookup"><span data-stu-id="8dd65-148">Three times cheaper than DynamoDB.</span></span>

## <a name="capability-comparison"></a><span data-ttu-id="8dd65-149">功能比較</span><span class="sxs-lookup"><span data-stu-id="8dd65-149">Capability comparison</span></span>

<span data-ttu-id="8dd65-150">Azure 的 Cosmos DB 會提供 hello 的關聯式和非關聯式資料庫的最佳功能。</span><span class="sxs-lookup"><span data-stu-id="8dd65-150">Azure Cosmos DB provides hello best capabilities of relational and non-relational databases.</span></span>

| <span data-ttu-id="8dd65-151">功能</span><span class="sxs-lookup"><span data-stu-id="8dd65-151">Capabilities</span></span> | <span data-ttu-id="8dd65-152">關聯式資料庫</span><span class="sxs-lookup"><span data-stu-id="8dd65-152">Relational databases</span></span>   | <span data-ttu-id="8dd65-153">非關聯式 (NoSQL) 資料庫</span><span class="sxs-lookup"><span data-stu-id="8dd65-153">Non-relational (NoSQL) databases</span></span> |    <span data-ttu-id="8dd65-154">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8dd65-154">Azure Cosmos DB</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8dd65-155">全球發佈</span><span class="sxs-lookup"><span data-stu-id="8dd65-155">Global distribution</span></span> | <span data-ttu-id="8dd65-156">否</span><span class="sxs-lookup"><span data-stu-id="8dd65-156">No</span></span> | <span data-ttu-id="8dd65-157">否</span><span class="sxs-lookup"><span data-stu-id="8dd65-157">No</span></span> | <span data-ttu-id="8dd65-158">是，在 30 個以上的區域中周全且立即可用的散發，具有多路連接的 API</span><span class="sxs-lookup"><span data-stu-id="8dd65-158">Yes, turnkey distribution in 30+ regions, with multi-homing APIs</span></span>|
| <span data-ttu-id="8dd65-159">水平調整</span><span class="sxs-lookup"><span data-stu-id="8dd65-159">Horizontal scale</span></span> | <span data-ttu-id="8dd65-160">否</span><span class="sxs-lookup"><span data-stu-id="8dd65-160">No</span></span> | <span data-ttu-id="8dd65-161">是</span><span class="sxs-lookup"><span data-stu-id="8dd65-161">Yes</span></span> | <span data-ttu-id="8dd65-162">是，您可以獨立調整儲存體和輸送量</span><span class="sxs-lookup"><span data-stu-id="8dd65-162">Yes, you can independently scale storage and throughput</span></span> | 
| <span data-ttu-id="8dd65-163">延遲保證</span><span class="sxs-lookup"><span data-stu-id="8dd65-163">Latency guarantees</span></span> | <span data-ttu-id="8dd65-164">否</span><span class="sxs-lookup"><span data-stu-id="8dd65-164">No</span></span> | <span data-ttu-id="8dd65-165">是</span><span class="sxs-lookup"><span data-stu-id="8dd65-165">Yes</span></span> | <span data-ttu-id="8dd65-166">是，99% 的讀取 <10 毫秒和寫入 <15 毫秒</span><span class="sxs-lookup"><span data-stu-id="8dd65-166">Yes, 99% of reads in <10 ms and writes in <15 ms</span></span> | 
| <span data-ttu-id="8dd65-167">高可用性</span><span class="sxs-lookup"><span data-stu-id="8dd65-167">High availability</span></span> | <span data-ttu-id="8dd65-168">否</span><span class="sxs-lookup"><span data-stu-id="8dd65-168">No</span></span> | <span data-ttu-id="8dd65-169">是</span><span class="sxs-lookup"><span data-stu-id="8dd65-169">Yes</span></span> | <span data-ttu-id="8dd65-170">是，Cosmos DB 一律可用，具有 PACELC 取捨，並提供自動和手動容錯移轉選項</span><span class="sxs-lookup"><span data-stu-id="8dd65-170">Yes, Cosmos DB is always on, has PACELC tradeoffs, and provides automatic & manual failover options</span></span>|
| <span data-ttu-id="8dd65-171">資料模型 + API</span><span class="sxs-lookup"><span data-stu-id="8dd65-171">Data model + API</span></span> | <span data-ttu-id="8dd65-172">關聯式 + SQL</span><span class="sxs-lookup"><span data-stu-id="8dd65-172">Relational + SQL</span></span> | <span data-ttu-id="8dd65-173">多模型 + OSS API</span><span class="sxs-lookup"><span data-stu-id="8dd65-173">Multi-model + OSS API</span></span> | <span data-ttu-id="8dd65-174">多模型 + SQL + OSS API (更多即將推出)</span><span class="sxs-lookup"><span data-stu-id="8dd65-174">Multi-model + SQL + OSS API (more coming soon)</span></span> |
| <span data-ttu-id="8dd65-175">SLA</span><span class="sxs-lookup"><span data-stu-id="8dd65-175">SLAs</span></span> | <span data-ttu-id="8dd65-176">是</span><span class="sxs-lookup"><span data-stu-id="8dd65-176">Yes</span></span> | <span data-ttu-id="8dd65-177">否</span><span class="sxs-lookup"><span data-stu-id="8dd65-177">No</span></span> | <span data-ttu-id="8dd65-178">是，延遲、輸送量、一致性、可用性的完整 SLA</span><span class="sxs-lookup"><span data-stu-id="8dd65-178">Yes, comprehensive SLAs for latency, throughput, consistency, availability</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8dd65-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8dd65-179">Next steps</span></span>
<span data-ttu-id="8dd65-180">透過下列其中一個快速入門開始使用 Azure Cosmos DB：</span><span class="sxs-lookup"><span data-stu-id="8dd65-180">Get started with Azure Cosmos DB with one of our quickstarts:</span></span>

* [<span data-ttu-id="8dd65-181">開始使用 Azure Cosmos DB 的 DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="8dd65-181">Get started with Azure Cosmos DB's DocumentDB API</span></span>](create-documentdb-dotnet.md)
* [<span data-ttu-id="8dd65-182">開始使用 Azure Cosmos DB 的 MongoDB API</span><span class="sxs-lookup"><span data-stu-id="8dd65-182">Get started with Azure Cosmos DB's MongoDB API</span></span>](create-mongodb-nodejs.md)
* [<span data-ttu-id="8dd65-183">開始使用 Azure Cosmos DB 的圖形 API</span><span class="sxs-lookup"><span data-stu-id="8dd65-183">Get started with Azure Cosmos DB's Graph API</span></span>](create-graph-dotnet.md)
* [<span data-ttu-id="8dd65-184">開始使用 Azure Cosmos DB 的資料表 API</span><span class="sxs-lookup"><span data-stu-id="8dd65-184">Get started with Azure Cosmos DB's Table API</span></span>](create-table-dotnet.md)
