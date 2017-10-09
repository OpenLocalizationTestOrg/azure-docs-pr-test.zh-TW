---
title: "aaaDocumentDB API 效能層級 |Microsoft 文件"
description: "深入了解如何 DocumentDB API 效能層級可讓您以每個容器基礎 tooreserve 輸送量。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="727db-103">淘汰 hello S1、 S2 和 S3 效能層級</span><span class="sxs-lookup"><span data-stu-id="727db-103">Retiring hello S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="727db-104">hello S1、 S2 和 S3 效能層級本文所討論的淘汰過程，便無法再使用新的 DocumentDB API 帳戶。</span><span class="sxs-lookup"><span data-stu-id="727db-104">hello S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="727db-105">本文提供 S1、 S2 和 S3 效能層級的概觀，並討論如何使用這些效能層級的 hello 集合時，會在 2017 年 8 月 1 日，是移轉的 toosingle 分割區集合。</span><span class="sxs-lookup"><span data-stu-id="727db-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how hello collections that use these performance levels will be migrated toosingle partition collections on August 1st, 2017.</span></span> <span data-ttu-id="727db-106">閱讀這篇文章之後, 您將會無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="727db-106">After reading this article, you'll be able tooanswer hello following questions:</span></span>

- [<span data-ttu-id="727db-107">為何 hello S1、 S2 和 S3 效能層級停用嗎？</span><span class="sxs-lookup"><span data-stu-id="727db-107">Why are hello S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="727db-108">如何單一分割區集合和資料分割的集合比較 toohello S1、 S2、 S3 效能層級？</span><span class="sxs-lookup"><span data-stu-id="727db-108">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="727db-109">我要如何需要 toodo tooensure 不會中斷存取 toomy 資料嗎？</span><span class="sxs-lookup"><span data-stu-id="727db-109">What do I need toodo tooensure uninterrupted access toomy data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="727db-110">Hello 移轉之後如何變更我的集合？</span><span class="sxs-lookup"><span data-stu-id="727db-110">How will my collection change after hello migration?</span></span>](#collection-change)
- [<span data-ttu-id="727db-111">如何將我的帳單之後變更我已移轉的 toosingle 分割區集合？</span><span class="sxs-lookup"><span data-stu-id="727db-111">How will my billing change after I’m migrated toosingle partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="727db-112">如果我需要超過 10 GB 的儲存體會如何？</span><span class="sxs-lookup"><span data-stu-id="727db-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="727db-113">我可以變更 hello S1、 S2 和 S3 效能層級，2017 年 8 月 1 之前, 之間嗎？</span><span class="sxs-lookup"><span data-stu-id="727db-113">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="727db-114">如何得知我的收藏何時已移轉？</span><span class="sxs-lookup"><span data-stu-id="727db-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="727db-115">如何將從 hello S1、 S2 或 S3 效能層級 toosingle 分割區集合自己移轉？</span><span class="sxs-lookup"><span data-stu-id="727db-115">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="727db-116">如果我是 EA 客戶會受到什麼影響？</span><span class="sxs-lookup"><span data-stu-id="727db-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="727db-117">為何 hello S1、 S2 和 S3 效能層級停用嗎？</span><span class="sxs-lookup"><span data-stu-id="727db-117">Why are hello S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="727db-118">hello S1、 S2 和 S3 效能層級執行無法提供 hello 彈性 DocumentDB API 集合所提供。</span><span class="sxs-lookup"><span data-stu-id="727db-118">hello S1, S2, and S3 performance levels do not offer hello flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="727db-119">以 hello S1、 S2 或 S3 效能層級，這兩個 hello 輸送量與儲存體容量已預先設定，並不會提供彈性。</span><span class="sxs-lookup"><span data-stu-id="727db-119">With hello S1, S2, S3 performance levels, both hello throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="727db-120">Azure Cosmos DB 現在提供 hello 能力 toocustomize 您輸送量與儲存體，提供您更大的彈性能力 tooscale 中隨著需求的變更。</span><span class="sxs-lookup"><span data-stu-id="727db-120">Azure Cosmos DB now offers hello ability toocustomize your throughput and storage, offering you much more flexibility in your ability tooscale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a><span data-ttu-id="727db-121">如何單一分割區集合和資料分割的集合比較 toohello S1、 S2、 S3 效能層級？</span><span class="sxs-lookup"><span data-stu-id="727db-121">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="727db-122">下表中的 hello 比較 hello 輸送量與儲存體的可用選項中單一分割區集合、 資料分割的集合和 S1、 S2 或 S3 效能層級。</span><span class="sxs-lookup"><span data-stu-id="727db-122">hello following table compares hello throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="727db-123">美國東部 2 區域的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="727db-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="727db-124">資料分割的集合</span><span class="sxs-lookup"><span data-stu-id="727db-124">Partitioned collection</span></span>|<span data-ttu-id="727db-125">單一資料分割集合</span><span class="sxs-lookup"><span data-stu-id="727db-125">Single partition collection</span></span>|<span data-ttu-id="727db-126">S1</span><span class="sxs-lookup"><span data-stu-id="727db-126">S1</span></span>|<span data-ttu-id="727db-127">S2</span><span class="sxs-lookup"><span data-stu-id="727db-127">S2</span></span>|<span data-ttu-id="727db-128">S3</span><span class="sxs-lookup"><span data-stu-id="727db-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="727db-129">最大輸送量</span><span class="sxs-lookup"><span data-stu-id="727db-129">Maximum throughput</span></span>|<span data-ttu-id="727db-130">無限制</span><span class="sxs-lookup"><span data-stu-id="727db-130">Unlimited</span></span>|<span data-ttu-id="727db-131">10K RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-131">10K RU/s</span></span>|<span data-ttu-id="727db-132">250 RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-132">250 RU/s</span></span>|<span data-ttu-id="727db-133">1 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-133">1 K RU/s</span></span>|<span data-ttu-id="727db-134">2.5 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="727db-135">輸送量下限</span><span class="sxs-lookup"><span data-stu-id="727db-135">Minimum throughput</span></span>|<span data-ttu-id="727db-136">2.5K RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-136">2.5K RU/s</span></span>|<span data-ttu-id="727db-137">400 RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-137">400 RU/s</span></span>|<span data-ttu-id="727db-138">250 RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-138">250 RU/s</span></span>|<span data-ttu-id="727db-139">1 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-139">1 K RU/s</span></span>|<span data-ttu-id="727db-140">2.5 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="727db-141">儲存體上限</span><span class="sxs-lookup"><span data-stu-id="727db-141">Maximum storage</span></span>|<span data-ttu-id="727db-142">無限制</span><span class="sxs-lookup"><span data-stu-id="727db-142">Unlimited</span></span>|<span data-ttu-id="727db-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="727db-143">10 GB</span></span>|<span data-ttu-id="727db-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="727db-144">10 GB</span></span>|<span data-ttu-id="727db-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="727db-145">10 GB</span></span>|<span data-ttu-id="727db-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="727db-146">10 GB</span></span>|
|<span data-ttu-id="727db-147">價格 (每月)</span><span class="sxs-lookup"><span data-stu-id="727db-147">Price (monthly)</span></span>|<span data-ttu-id="727db-148">輸送量：$6 / 100 RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="727db-149">儲存體：$0.25/GB</span><span class="sxs-lookup"><span data-stu-id="727db-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="727db-150">輸送量：$6 / 100 RU/秒</span><span class="sxs-lookup"><span data-stu-id="727db-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="727db-151">儲存體：$0.25/GB</span><span class="sxs-lookup"><span data-stu-id="727db-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="727db-152">$25 美元</span><span class="sxs-lookup"><span data-stu-id="727db-152">$25 USD</span></span>|<span data-ttu-id="727db-153">$50 美元</span><span class="sxs-lookup"><span data-stu-id="727db-153">$50 USD</span></span>|<span data-ttu-id="727db-154">$100 美元</span><span class="sxs-lookup"><span data-stu-id="727db-154">$100 USD</span></span>|

<span data-ttu-id="727db-155">您是 EA 客戶嗎？</span><span class="sxs-lookup"><span data-stu-id="727db-155">Are you an EA customer?</span></span> <span data-ttu-id="727db-156">如果是，請參閱[如果我是 EA 客戶會受到什麼影響？](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="727db-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a><span data-ttu-id="727db-157">我要如何需要 toodo tooensure 不會中斷存取 toomy 資料嗎？</span><span class="sxs-lookup"><span data-stu-id="727db-157">What do I need toodo tooensure uninterrupted access toomy data?</span></span>

<span data-ttu-id="727db-158">Nothing，Cosmos DB 處理 hello 為您的移轉。</span><span class="sxs-lookup"><span data-stu-id="727db-158">Nothing, Cosmos DB handles hello migration for you.</span></span> <span data-ttu-id="727db-159">如果您擁有 S1、 S2 或 S3 的集合，您目前的集合將會移轉的 tooa 2017 年 7 月 31，單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="727db-159">If you have an S1, S2, or S3 collection, your current collection will be migrated tooa single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a><span data-ttu-id="727db-160">Hello 移轉之後如何變更我的集合？</span><span class="sxs-lookup"><span data-stu-id="727db-160">How will my collection change after hello migration?</span></span>

<span data-ttu-id="727db-161">如果您擁有 S1 集合，您將會移轉的 tooa 400 RU/秒的輸送量的單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="727db-161">If you have an S1 collection, you will be migrated tooa single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="727db-162">400 RU/秒是 hello 最低輸送量適用於單一分割區集合。</span><span class="sxs-lookup"><span data-stu-id="727db-162">400 RU/s is hello lowest throughput available with single partition collections.</span></span> <span data-ttu-id="727db-163">不過，400 RU/秒中的單一資料分割集合為大約使用 S1 集合費用與您相同的 hello hello 和 250k RU/秒 – 讓您不支付 hello 成本 hello 額外 150 RU/秒可用 tooyou。</span><span class="sxs-lookup"><span data-stu-id="727db-163">However, hello cost for 400 RU/s in hello a single partition collection is approximately hello same as you were paying with your S1 collection and 250 RU/s – so you are not paying for hello extra 150 RU/s available tooyou.</span></span>

<span data-ttu-id="727db-164">如果您擁有 S2 集合，您將會移轉的 tooa 單一資料分割集合，1 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="727db-164">If you have an S2 collection, you will be migrated tooa single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="727db-165">您會看到不變更 tooyour 輸送量層級。</span><span class="sxs-lookup"><span data-stu-id="727db-165">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="727db-166">如果您擁有 S3 集合，您將會移轉的 tooa 單一資料分割集合 2.5 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="727db-166">If you have an S3 collection, you will be migrated tooa single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="727db-167">您會看到不變更 tooyour 輸送量層級。</span><span class="sxs-lookup"><span data-stu-id="727db-167">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="727db-168">在每個這種情況下，移轉您的集合之後，您會無法 toocustomize 您輸送量層級，或它上下調整為所需的 tooprovide 低延遲存取 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="727db-168">In each of these cases, after your collection is migrated, you will be able toocustomize your throughput level, or scale it up and down as needed tooprovide low-latency access tooyour users.</span></span> <span data-ttu-id="727db-169">toochange hello 輸送量層級之後已移轉您的集合，只要 hello Azure 入口網站中開啟 Cosmos DB 帳戶、 按一下標尺、 選擇您的集合，和 hello 下列螢幕擷取畫面所示，然後調整 hello 輸送量層級：</span><span class="sxs-lookup"><span data-stu-id="727db-169">toochange hello throughput level after your collection has migrated, simply open your Cosmos DB account in hello Azure portal, click Scale, choose your collection, and then adjust hello throughput level, as shown in hello following screenshot:</span></span>

![如何在 tooscale 輸送量 hello Azure 入口網站](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a><span data-ttu-id="727db-171">如何將我的帳單之後變更我已移轉的 toohello 單一分割區集合？</span><span class="sxs-lookup"><span data-stu-id="727db-171">How will my billing change after I’m migrated toohello single partition collections?</span></span>

<span data-ttu-id="727db-172">假設您有 10 個 S1 集合，1 GB 的 hello 美國東部地區中的每個儲存體，而且您將移轉這些 10 S1 集合 too10 單一分割區集合在 400 RU/秒 （hello 最低層級）。</span><span class="sxs-lookup"><span data-stu-id="727db-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in hello US East region, and you migrate these 10 S1 collections too10 single partition collections at 400 RU/sec (hello minimum level).</span></span> <span data-ttu-id="727db-173">您的帳單將會看起來像這樣如果您維持完整月份 hello 10 的單一分割區集合：</span><span class="sxs-lookup"><span data-stu-id="727db-173">Your bill will look as follows if you keep hello 10 single partition collections for a full month:</span></span>

![如何 S1 定價 10 集合比較 too10 集合使用的單一資料分割集合定價](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="727db-175">如果我需要超過 10 GB 的儲存空間怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="727db-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="727db-176">不論您具有使用 S1、 S2 或 S3 效能層級的集合，或具有單一資料分割集合，其中有 10 GB 的可用儲存體，您可以使用 hello Cosmos DB 的資料移轉工具 toomigrate 資料 tooa 幾乎分割集合無限制的儲存體。</span><span class="sxs-lookup"><span data-stu-id="727db-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use hello Cosmos DB Data Migration tool toomigrate your data tooa partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="727db-177">資料分割的集合中的 hello 優點的相關資訊，請參閱[資料分割和 Azure Cosmos DB 中的縮放比例](documentdb-partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="727db-177">For information about hello benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="727db-178">如需有關資訊 toomigrate 您 S1、 S2、 S3 或單一資料分割集合 tooa 分割集合，請參閱[從單一資料分割 toopartitioned 集合移轉](documentdb-partition-data.md#migrating-from-single-partition)。</span><span class="sxs-lookup"><span data-stu-id="727db-178">For information about how toomigrate your S1, S2, S3, or single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="727db-179">我可以變更 hello S1、 S2 和 S3 效能層級，2017 年 8 月 1 之前, 之間嗎？</span><span class="sxs-lookup"><span data-stu-id="727db-179">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="727db-180">唯一的現有帳戶使用 S1、 S2 和 S3 效能會無法 toochange 並變更效能層級層透過 hello 入口網站，或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="727db-180">Only existing accounts with S1, S2, and S3 performance will be able toochange and alter performance level tiers through hello portal or programmatically.</span></span> <span data-ttu-id="727db-181">依年 8 月 1，2017，hello S1、 S2 和 S3 效能層級將不再可用。</span><span class="sxs-lookup"><span data-stu-id="727db-181">By August 1, 2017, hello S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="727db-182">如果您從 S1、 S3  S3 tooa 單一資料分割集合變更時，無法傳回 toohello S1、 S2 或 S3 效能層級。</span><span class="sxs-lookup"><span data-stu-id="727db-182">If you change from S1, S3, or S3 tooa single partition collection, you cannot return toohello S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="727db-183">如何得知我的收藏何時已移轉？</span><span class="sxs-lookup"><span data-stu-id="727db-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="727db-184">hello 移轉會發生在 2017 年 7 月 31。</span><span class="sxs-lookup"><span data-stu-id="727db-184">hello migration will occur on July 31, 2017.</span></span> <span data-ttu-id="727db-185">如果您擁有的集合，其使用 hello S1、 S2 或 S3 效能層級，hello Cosmos DB 小組會與您連絡以電子郵件進行 hello 移轉之前。</span><span class="sxs-lookup"><span data-stu-id="727db-185">If you have a collection that uses hello S1, S2 or S3 performance levels, hello Cosmos DB team will contact you by email before hello migration takes place.</span></span> <span data-ttu-id="727db-186">Hello 移轉完成之後，在 8 月 1，2017，hello Azure 入口網站會顯示您的集合，使用標準定價。</span><span class="sxs-lookup"><span data-stu-id="727db-186">Once hello migration is complete, on August 1, 2017, hello Azure portal will show that your collection uses Standard pricing.</span></span>

![如何 tooconfirm 集合已移轉 toohello 標準定價層](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a><span data-ttu-id="727db-188">如何將從 hello S1、 S2 或 S3 效能層級 toosingle 分割區集合自己移轉？</span><span class="sxs-lookup"><span data-stu-id="727db-188">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>

<span data-ttu-id="727db-189">您可以從 hello S1、 S2、 移轉和 S3 效能層級 toosingle 分割區集合使用 hello Azure 入口網站或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="727db-189">You can migrate from hello S1, S2, and S3 performance levels toosingle partition collections using hello Azure portal or programmatically.</span></span> <span data-ttu-id="727db-190">您可以在您自己之前年 8 月 1 toobenefit hello 彈性輸送量選項適用於單一資料分割的集合，或我們將會移轉您的集合，讓您在 2017 年 7 月 31。</span><span class="sxs-lookup"><span data-stu-id="727db-190">You can do this on your own before August 1 toobenefit from hello flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="727db-191">**使用 Azure 入口網站 hello toomigrate toosingle 分割區集合**</span><span class="sxs-lookup"><span data-stu-id="727db-191">**toomigrate toosingle partition collections using hello Azure portal**</span></span>

1. <span data-ttu-id="727db-192">在 hello [ **Azure 入口網站**](https://portal.azure.com)，按一下 [ **Azure Cosmos DB**，然後選取 [hello Cosmos DB 帳戶 toomodify。</span><span class="sxs-lookup"><span data-stu-id="727db-192">In hello [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select hello Cosmos DB account toomodify.</span></span> 
 
    <span data-ttu-id="727db-193">如果**Azure Cosmos DB**在 hello Jumpbar，請按一下 >，太捲動**資料庫**，選取**Azure Cosmos DB**，然後選取 hello DocumentDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="727db-193">If **Azure Cosmos DB** is not on hello Jumpbar, click >, scroll too**Databases**, select **Azure Cosmos DB**, and then select hello DocumentDB account.</span></span>  

2. <span data-ttu-id="727db-194">Hello 資源在功能表上，在**容器**，按一下 **標尺**從 hello 下拉式清單中，選取 hello 集合 toomodify，然後按一下**定價層**。</span><span class="sxs-lookup"><span data-stu-id="727db-194">On hello resource menu, under **Containers**, click **Scale**, select hello collection toomodify from hello drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="727db-195">使用預先定義的輸送量的帳戶具有 S1、S2 或 S3 定價層。</span><span class="sxs-lookup"><span data-stu-id="727db-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="727db-196">在 hello**選擇定價層**刀鋒視窗中，按一下 **標準**toochange toouser 定義輸送量，然後按一下**選取**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="727db-196">In hello **Choose your pricing tier** blade, click **Standard** toochange toouser-defined throughput, and then click **Select** toosave your change.</span></span>

    ![顯示其中 toochange hello 輸送量值 hello 設定 刀鋒視窗的螢幕擷取畫面](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="727db-198">在 hello**標尺**刀鋒視窗，hello**定價層**太變更**標準**和 hello**輸送量 （RU/秒）**方塊會顯示預設值為 400。</span><span class="sxs-lookup"><span data-stu-id="727db-198">Back in hello **Scale** blade, hello **Pricing Tier** is changed too**Standard** and hello **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="727db-199">設定介於 400 到 10000 之間的 hello 輸送量[要求單位](request-units.md)數/秒 （RU/秒）。</span><span class="sxs-lookup"><span data-stu-id="727db-199">Set hello throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="727db-200">hello**預估每月帳單**底部 hello hello 頁面會自動更新 tooprovide hello 每月成本估計。</span><span class="sxs-lookup"><span data-stu-id="727db-200">hello **Estimated Monthly Bill** at hello bottom of hello page updates automatically tooprovide an estimate of hello monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="727db-201">一旦您儲存變更，並移動 toohello 標準定價層，您無法回復 toohello S1、 S2 或 S3 效能層級。</span><span class="sxs-lookup"><span data-stu-id="727db-201">Once you save your changes and move toohello Standard pricing tier, you cannot roll back toohello S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="727db-202">按一下**儲存**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="727db-202">Click **Save** toosave your changes.</span></span>

    <span data-ttu-id="727db-203">如果您判斷您需要更多輸送量 (大於 10,000 RU/秒) 或更多儲存體 (大於 10 GB)，您可以建立資料分割的集合。</span><span class="sxs-lookup"><span data-stu-id="727db-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="727db-204">toomigrate 單一資料分割集合 tooa 分割集合，請參閱[從單一資料分割 toopartitioned 集合移轉](documentdb-partition-data.md#migrating-from-single-partition)。</span><span class="sxs-lookup"><span data-stu-id="727db-204">toomigrate a single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="727db-205">從 S1、 S2 或 S3 tooStandard 變更可能會佔用 too2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="727db-205">Changing from S1, S2, or S3 tooStandard may take up too2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="727db-206">**使用.NET SDK hello toomigrate toosingle 分割區集合**</span><span class="sxs-lookup"><span data-stu-id="727db-206">**toomigrate toosingle partition collections using hello .NET SDK**</span></span>

<span data-ttu-id="727db-207">變更集合的效能層級的另一個選項是透過我們的 SDK。</span><span class="sxs-lookup"><span data-stu-id="727db-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="727db-208">本節只涵蓋變更集合的效能層級使用我們[DocumentDB.NET API](documentdb-sdk-dotnet.md)，但我們其他 Sdk 類似 hello 處理程序。</span><span class="sxs-lookup"><span data-stu-id="727db-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but hello process is similar for our other SDKs.</span></span>

<span data-ttu-id="727db-209">以下是變更 hello 集合輸送量 too5，000 每秒的要求單位的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="727db-209">Here is a code snippet for changing hello collection throughput too5,000 request units per second:</span></span>
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="727db-210">請瀏覽[MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview 其他範例和深入了解我們提供的方法：</span><span class="sxs-lookup"><span data-stu-id="727db-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="727db-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="727db-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="727db-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="727db-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="727db-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="727db-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="727db-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="727db-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="727db-215">如果我是 EA 客戶會受到什麼影響？</span><span class="sxs-lookup"><span data-stu-id="727db-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="727db-216">EA 客戶將會受到保護，直到其目前合約的 hello 結尾的價格。</span><span class="sxs-lookup"><span data-stu-id="727db-216">EA customers will be price protected until hello end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="727db-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="727db-217">Next steps</span></span>
<span data-ttu-id="727db-218">進一步了解價格及使用 Azure Cosmos DB，管理資料 toolearn 瀏覽這些資源：</span><span class="sxs-lookup"><span data-stu-id="727db-218">toolearn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="727db-219">[在 Cosmos DB 中分割資料](documentdb-partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="727db-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="727db-220">了解 hello 差異單一磁碟分割容器和資料分割的容器，以及順暢地實作資料分割的策略 tooscale 的秘訣。</span><span class="sxs-lookup"><span data-stu-id="727db-220">Understand hello difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy tooscale seamlessly.</span></span>
2.  <span data-ttu-id="727db-221">[Cosmos DB 定價](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="727db-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="727db-222">深入了解 hello 佈建輸送量和耗用儲存體的成本。</span><span class="sxs-lookup"><span data-stu-id="727db-222">Learn about hello cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="727db-223">[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="727db-223">[Request units](request-units.md).</span></span> <span data-ttu-id="727db-224">了解 hello 耗用量的不同作業類型，例如讀取、 寫入、 查詢的輸送量。</span><span class="sxs-lookup"><span data-stu-id="727db-224">Understand hello consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
