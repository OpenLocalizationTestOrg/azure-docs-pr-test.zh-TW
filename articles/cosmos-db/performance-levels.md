---
title: "DocumentDB API 效能等級 | Microsoft Docs"
description: "了解 DocumentDB API 效能等級如何可讓您根據每個容器來保留輸送量。"
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
ms.openlocfilehash: c8d4733e57eb760dbb8e8ca96f6ba55671d1742f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="retiring-the-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="16eb0-103">淘汰 S1、S2 和 S3 效能層級</span><span class="sxs-lookup"><span data-stu-id="16eb0-103">Retiring the S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="16eb0-104">本文所討論的 S1、S2 和 S3 效能層級將會淘汰，而且也無法再供新的 DocumentDB API 帳戶使用。</span><span class="sxs-lookup"><span data-stu-id="16eb0-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="16eb0-105">本文概述 S1、S2 和 S3 效能層級，並討論使用這些效能層級的集合在 2017 年 8 月 1 日將如何移轉至單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels will be migrated to single partition collections on August 1st, 2017.</span></span> <span data-ttu-id="16eb0-106">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="16eb0-106">After reading this article, you'll be able to answer the following questions:</span></span>

- [<span data-ttu-id="16eb0-107">為何 S1、S2 和 S3 效能層級將要淘汰？</span><span class="sxs-lookup"><span data-stu-id="16eb0-107">Why are the S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="16eb0-108">單一分割區集合和資料分割的集合與 S1、S2、S3 效能層級之比較為何？</span><span class="sxs-lookup"><span data-stu-id="16eb0-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="16eb0-109">我該怎麼做才能確保不中斷地的存取我的資料？</span><span class="sxs-lookup"><span data-stu-id="16eb0-109">What do I need to do to ensure uninterrupted access to my data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="16eb0-110">在移轉之後我的集合會如何變更？</span><span class="sxs-lookup"><span data-stu-id="16eb0-110">How will my collection change after the migration?</span></span>](#collection-change)
- [<span data-ttu-id="16eb0-111">我移轉至單一資料分割集合之後，我的帳單將如何變更呢？</span><span class="sxs-lookup"><span data-stu-id="16eb0-111">How will my billing change after I’m migrated to single partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="16eb0-112">如果我需要超過 10 GB 的儲存體會如何？</span><span class="sxs-lookup"><span data-stu-id="16eb0-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="16eb0-113">在 2017 年 8 月 1 前，我可以在 S1、S2 和 S3 效能層級之間變更嗎？</span><span class="sxs-lookup"><span data-stu-id="16eb0-113">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="16eb0-114">如何得知我的收藏何時已移轉？</span><span class="sxs-lookup"><span data-stu-id="16eb0-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="16eb0-115">如何自己從 S1、S2、S3 效能層級移轉至單一資料分割集合？</span><span class="sxs-lookup"><span data-stu-id="16eb0-115">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="16eb0-116">如果我是 EA 客戶會受到什麼影響？</span><span class="sxs-lookup"><span data-stu-id="16eb0-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-the-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="16eb0-117">為何 S1、S2 和 S3 效能層級將要淘汰？</span><span class="sxs-lookup"><span data-stu-id="16eb0-117">Why are the S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="16eb0-118">S1、S2 和 S3 效能層級不提供 DocumentDB API 集合所提供的彈性。</span><span class="sxs-lookup"><span data-stu-id="16eb0-118">The S1, S2, and S3 performance levels do not offer the flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="16eb0-119">使用 S1、S2、S3 效能層級，輸送量和儲存容量皆會預先設定且不提供彈性。</span><span class="sxs-lookup"><span data-stu-id="16eb0-119">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="16eb0-120">Azure Cosmos DB 現在可讓您自訂輸送量和儲存體，提供您更大的彈性能夠隨您的需求進行變更。</span><span class="sxs-lookup"><span data-stu-id="16eb0-120">Azure Cosmos DB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-to-the-s1-s2-s3-performance-levels"></a><span data-ttu-id="16eb0-121">單一分割區集合和資料分割的集合與 S1、S2、S3 效能層級之比較為何？</span><span class="sxs-lookup"><span data-stu-id="16eb0-121">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="16eb0-122">下表比較單一資料分割集合、資料分割集合和 S1、S2、S3 效能層級中可用的輸送量和儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="16eb0-122">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="16eb0-123">美國東部 2 區域的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="16eb0-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="16eb0-124">資料分割的集合</span><span class="sxs-lookup"><span data-stu-id="16eb0-124">Partitioned collection</span></span>|<span data-ttu-id="16eb0-125">單一資料分割集合</span><span class="sxs-lookup"><span data-stu-id="16eb0-125">Single partition collection</span></span>|<span data-ttu-id="16eb0-126">S1</span><span class="sxs-lookup"><span data-stu-id="16eb0-126">S1</span></span>|<span data-ttu-id="16eb0-127">S2</span><span class="sxs-lookup"><span data-stu-id="16eb0-127">S2</span></span>|<span data-ttu-id="16eb0-128">S3</span><span class="sxs-lookup"><span data-stu-id="16eb0-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="16eb0-129">最大輸送量</span><span class="sxs-lookup"><span data-stu-id="16eb0-129">Maximum throughput</span></span>|<span data-ttu-id="16eb0-130">無限制</span><span class="sxs-lookup"><span data-stu-id="16eb0-130">Unlimited</span></span>|<span data-ttu-id="16eb0-131">10K RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-131">10K RU/s</span></span>|<span data-ttu-id="16eb0-132">250 RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-132">250 RU/s</span></span>|<span data-ttu-id="16eb0-133">1 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-133">1 K RU/s</span></span>|<span data-ttu-id="16eb0-134">2.5 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="16eb0-135">輸送量下限</span><span class="sxs-lookup"><span data-stu-id="16eb0-135">Minimum throughput</span></span>|<span data-ttu-id="16eb0-136">2.5K RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-136">2.5K RU/s</span></span>|<span data-ttu-id="16eb0-137">400 RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-137">400 RU/s</span></span>|<span data-ttu-id="16eb0-138">250 RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-138">250 RU/s</span></span>|<span data-ttu-id="16eb0-139">1 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-139">1 K RU/s</span></span>|<span data-ttu-id="16eb0-140">2.5 K RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="16eb0-141">儲存體上限</span><span class="sxs-lookup"><span data-stu-id="16eb0-141">Maximum storage</span></span>|<span data-ttu-id="16eb0-142">無限制</span><span class="sxs-lookup"><span data-stu-id="16eb0-142">Unlimited</span></span>|<span data-ttu-id="16eb0-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="16eb0-143">10 GB</span></span>|<span data-ttu-id="16eb0-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="16eb0-144">10 GB</span></span>|<span data-ttu-id="16eb0-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="16eb0-145">10 GB</span></span>|<span data-ttu-id="16eb0-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="16eb0-146">10 GB</span></span>|
|<span data-ttu-id="16eb0-147">價格 (每月)</span><span class="sxs-lookup"><span data-stu-id="16eb0-147">Price (monthly)</span></span>|<span data-ttu-id="16eb0-148">輸送量：$6 / 100 RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="16eb0-149">儲存體：$0.25/GB</span><span class="sxs-lookup"><span data-stu-id="16eb0-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="16eb0-150">輸送量：$6 / 100 RU/秒</span><span class="sxs-lookup"><span data-stu-id="16eb0-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="16eb0-151">儲存體：$0.25/GB</span><span class="sxs-lookup"><span data-stu-id="16eb0-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="16eb0-152">$25 美元</span><span class="sxs-lookup"><span data-stu-id="16eb0-152">$25 USD</span></span>|<span data-ttu-id="16eb0-153">$50 美元</span><span class="sxs-lookup"><span data-stu-id="16eb0-153">$50 USD</span></span>|<span data-ttu-id="16eb0-154">$100 美元</span><span class="sxs-lookup"><span data-stu-id="16eb0-154">$100 USD</span></span>|

<span data-ttu-id="16eb0-155">您是 EA 客戶嗎？</span><span class="sxs-lookup"><span data-stu-id="16eb0-155">Are you an EA customer?</span></span> <span data-ttu-id="16eb0-156">如果是，請參閱[如果我是 EA 客戶會受到什麼影響？](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="16eb0-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-to-do-to-ensure-uninterrupted-access-to-my-data"></a><span data-ttu-id="16eb0-157">我該怎麼做才能確保不中斷地的存取我的資料？</span><span class="sxs-lookup"><span data-stu-id="16eb0-157">What do I need to do to ensure uninterrupted access to my data?</span></span>

<span data-ttu-id="16eb0-158">無須執行任何動作，Cosmos DB 會處理您的移轉。</span><span class="sxs-lookup"><span data-stu-id="16eb0-158">Nothing, Cosmos DB handles the migration for you.</span></span> <span data-ttu-id="16eb0-159">如果您有 S1、S2 或 S3 集合，您目前的集合將會在 2017 年 7 月 31 日移轉至單一磁碟分割集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-159">If you have an S1, S2, or S3 collection, your current collection will be migrated to a single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-the-migration"></a><span data-ttu-id="16eb0-160">在移轉之後我的集合會如何變更？</span><span class="sxs-lookup"><span data-stu-id="16eb0-160">How will my collection change after the migration?</span></span>

<span data-ttu-id="16eb0-161">如果您有一個 S1 集合，將會以 400 RU/秒的輸送量移轉至單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-161">If you have an S1 collection, you will be migrated to a single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="16eb0-162">400 RU/秒是適用於單一資料分割集合的最低輸送量。</span><span class="sxs-lookup"><span data-stu-id="16eb0-162">400 RU/s is the lowest throughput available with single partition collections.</span></span> <span data-ttu-id="16eb0-163">不過，單一資料分割集合中 400 RU/秒的成本，大致上與您已支付的 S1 集合與 250 RU/秒相同 – 因此您不需要支付供您使用的額外 150 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="16eb0-163">However, the cost for 400 RU/s in the a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span></span>

<span data-ttu-id="16eb0-164">如果您有一個 S2 集合，將會以 1 K RU/秒移轉至單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-164">If you have an S2 collection, you will be migrated to a single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="16eb0-165">您不會看到您的輸送量層級有任何變更。</span><span class="sxs-lookup"><span data-stu-id="16eb0-165">You will see no change to your throughput level.</span></span>

<span data-ttu-id="16eb0-166">如果您有一個 S3 集合，將會以 2.5 K RU/秒移轉至單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-166">If you have an S3 collection, you will be migrated to a single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="16eb0-167">您不會看到您的輸送量層級有任何變更。</span><span class="sxs-lookup"><span data-stu-id="16eb0-167">You will see no change to your throughput level.</span></span>

<span data-ttu-id="16eb0-168">在每一個情況下，在移轉您的集合之後，您將能夠自訂您的輸送量層級，或視需要將它相應增加及減少，為使用者提供低延遲存取。</span><span class="sxs-lookup"><span data-stu-id="16eb0-168">In each of these cases, after your collection is migrated, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span></span> <span data-ttu-id="16eb0-169">若要在移轉您的集合之後變更輸送量層級，只要在 Azure 入口網站中開啟 Cosmos DB 帳戶，按一下 [調整]、選擇您的集合，然後調整輸送量層級，如下列螢幕擷取畫面所示︰</span><span class="sxs-lookup"><span data-stu-id="16eb0-169">To change the throughput level after your collection has migrated, simply open your Cosmos DB account in the Azure portal, click Scale, choose your collection, and then adjust the throughput level, as shown in the following screenshot:</span></span>

![如何在 Azure 入口網站中調整輸送量](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-to-the-single-partition-collections"></a><span data-ttu-id="16eb0-171">我移轉至單一資料分割集合之後，我的帳單將如何變更呢？</span><span class="sxs-lookup"><span data-stu-id="16eb0-171">How will my billing change after I’m migrated to the single partition collections?</span></span>

<span data-ttu-id="16eb0-172">假設您在美國東部區域有 10 個 S1 集合，每個有 1 GB 的儲存空間，您將這 10 個 S1 集合以 400 RU/秒 (最小層級) 移轉至 10 個單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span></span> <span data-ttu-id="16eb0-173">如果您一整個月保留 10 個單一資料分割集合，您的帳單會看起來如下︰</span><span class="sxs-lookup"><span data-stu-id="16eb0-173">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span></span>

![10 個集合的 S1 價格與使用單一資料分割集合的 10 個集合價格比較會如何](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="16eb0-175">如果我需要超過 10 GB 的儲存空間怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="16eb0-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="16eb0-176">無論您擁有具有 S1、S2 或 S3 效能層級的集合，或是擁有單一資料分割集合，全部都有 10 GB 的可用儲存空間，您可以利用幾乎不受限制的儲存空間使用 Cosmos DB 資料移轉工具將您的資料移轉至資料分割的集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the Cosmos DB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="16eb0-177">如需資料分割集合優點的相關詳細資訊，請參閱 [Azure Cosmos DB 中的資料分割與規模調整](documentdb-partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="16eb0-177">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="16eb0-178">如需將 S1、S2、S3 或單一資料分割集合移轉到資料分割集合的詳細資訊，請參閱[從單一資料分割移轉至資料分割集合](documentdb-partition-data.md#migrating-from-single-partition)。</span><span class="sxs-lookup"><span data-stu-id="16eb0-178">For information about how to migrate your S1, S2, S3, or single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-the-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="16eb0-179">在 2017 年 8 月 1 前，我可以在 S1、S2 和 S3 效能層級之間變更嗎？</span><span class="sxs-lookup"><span data-stu-id="16eb0-179">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="16eb0-180">只有 S1、S2 和 S3 效能的現有帳戶可以變更，且透過入口網站或以程式設計的方式變更效能層級層。</span><span class="sxs-lookup"><span data-stu-id="16eb0-180">Only existing accounts with S1, S2, and S3 performance will be able to change and alter performance level tiers through the portal or programmatically.</span></span> <span data-ttu-id="16eb0-181">至 2017 年 8 月 1 日起，S1、S2 和 S3 效能層級不再提供使用。</span><span class="sxs-lookup"><span data-stu-id="16eb0-181">By August 1, 2017, the S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="16eb0-182">如果您從 S1、S3 或 S3 變更為單一資料分割集合，將無法回到 S1、S2 或 S3 效能層級。</span><span class="sxs-lookup"><span data-stu-id="16eb0-182">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="16eb0-183">如何得知我的收藏何時已移轉？</span><span class="sxs-lookup"><span data-stu-id="16eb0-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="16eb0-184">移轉會在 2017 年 7 月 31 日發生。</span><span class="sxs-lookup"><span data-stu-id="16eb0-184">The migration will occur on July 31, 2017.</span></span> <span data-ttu-id="16eb0-185">如果您擁有的集合是使用 S1、S2 或 S3 效能層級，Cosmos DB 小組會在進行移轉之前，透過電子郵件與您連絡。</span><span class="sxs-lookup"><span data-stu-id="16eb0-185">If you have a collection that uses the S1, S2 or S3 performance levels, the Cosmos DB team will contact you by email before the migration takes place.</span></span> <span data-ttu-id="16eb0-186">一旦完成移轉後，在 2017 年 8 月 1 日，Azure 入口網站會顯示您的集合是使用標準價格。</span><span class="sxs-lookup"><span data-stu-id="16eb0-186">Once the migration is complete, on August 1, 2017, the Azure portal will show that your collection uses Standard pricing.</span></span>

![如何確認您的集合已移轉至標準定價層](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-the-s1-s2-s3-performance-levels-to-single-partition-collections-on-my-own"></a><span data-ttu-id="16eb0-188">如何自己從 S1、S2、S3 效能層級移轉至單一資料分割集合？</span><span class="sxs-lookup"><span data-stu-id="16eb0-188">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>

<span data-ttu-id="16eb0-189">您可以使用 Azure 入口網站或以程式設計的方式，從 S1、S2 和 S3 效能層級移轉至單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-189">You can migrate from the S1, S2, and S3 performance levels to single partition collections using the Azure portal or programmatically.</span></span> <span data-ttu-id="16eb0-190">您可以在 8 月 1 日之前自行進行此動作，以受益於單一資料分割的集合具彈性的可用輸送量，或是我們會在 2017 年 7 月 31 日為您移轉集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-190">You can do this on your own before August 1 to benefit from the flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="16eb0-191">**若要使用 Azure 入口網站移轉至單一資料分割集合**</span><span class="sxs-lookup"><span data-stu-id="16eb0-191">**To migrate to single partition collections using the Azure portal**</span></span>

1. <span data-ttu-id="16eb0-192">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [Azure Cosmos DB]，然後選取要修改的 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="16eb0-192">In the [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select the Cosmos DB account to modify.</span></span> 
 
    <span data-ttu-id="16eb0-193">如果 [Azure Cosmos DB] 不在動態工具列中，按一下 >，捲動到 [資料庫]，選取 [Azure Cosmos DB]，然後選取 DocumentDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="16eb0-193">If **Azure Cosmos DB** is not on the Jumpbar, click >, scroll to **Databases**, select **Azure Cosmos DB**, and then select the DocumentDB account.</span></span>  

2. <span data-ttu-id="16eb0-194">在 [資源] 功能表上，於 [容器] 下，按一下 [級別]，從下拉式清單選取要修改的集合，然後按一下 [定價層]。</span><span class="sxs-lookup"><span data-stu-id="16eb0-194">On the resource menu, under **Containers**, click **Scale**, select the collection to modify from the drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="16eb0-195">使用預先定義的輸送量的帳戶具有 S1、S2 或 S3 定價層。</span><span class="sxs-lookup"><span data-stu-id="16eb0-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="16eb0-196">在 [選擇定價層] 刀鋒視窗中按一下 [標準] 來變更使用者定義的輸送量，然後按一下 [選取] 以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="16eb0-196">In the **Choose your pricing tier** blade, click **Standard** to change to user-defined throughput, and then click **Select** to save your change.</span></span>

    ![[設定] 刀鋒視窗的螢幕擷取畫面，其中顯示可供變更輸送量值的位置](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="16eb0-198">回到 [調整] 刀鋒視窗中，[定價層] 已變更為 [標準]，並且 [輸送量 (RU/秒)] 方塊會顯示預設值 400。</span><span class="sxs-lookup"><span data-stu-id="16eb0-198">Back in the **Scale** blade, the **Pricing Tier** is changed to **Standard** and the **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="16eb0-199">將輸送量設定為介於 400 到 10,000 個 [要求單位](request-units.md)/秒 (RU/秒)。</span><span class="sxs-lookup"><span data-stu-id="16eb0-199">Set the throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="16eb0-200">頁面底部的 [估計每月帳單] 會自動更新以提供每月成本估計。</span><span class="sxs-lookup"><span data-stu-id="16eb0-200">The **Estimated Monthly Bill** at the bottom of the page updates automatically to provide an estimate of the monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="16eb0-201">一旦您儲存變更並移至標準定價層後，將無法復原為 S1、S2 或 S3 效能層級。</span><span class="sxs-lookup"><span data-stu-id="16eb0-201">Once you save your changes and move to the Standard pricing tier, you cannot roll back to the S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="16eb0-202">按一下 [確定] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="16eb0-202">Click **Save** to save your changes.</span></span>

    <span data-ttu-id="16eb0-203">如果您判斷您需要更多輸送量 (大於 10,000 RU/秒) 或更多儲存體 (大於 10 GB)，您可以建立資料分割的集合。</span><span class="sxs-lookup"><span data-stu-id="16eb0-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="16eb0-204">若要將單一資料分割集合移轉到資料分割的集合，請參閱[從單一資料分割移轉至資料分割集合](documentdb-partition-data.md#migrating-from-single-partition)。</span><span class="sxs-lookup"><span data-stu-id="16eb0-204">To migrate a single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="16eb0-205">從 S1、S2 或 S3 變更為標準可能需要 2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="16eb0-205">Changing from S1, S2, or S3 to Standard may take up to 2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="16eb0-206">**若要使用 .NET SDK 移轉至單一資料分割集合**</span><span class="sxs-lookup"><span data-stu-id="16eb0-206">**To migrate to single partition collections using the .NET SDK**</span></span>

<span data-ttu-id="16eb0-207">變更集合的效能層級的另一個選項是透過我們的 SDK。</span><span class="sxs-lookup"><span data-stu-id="16eb0-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="16eb0-208">本節只涵蓋使用我們的 [DocumentDB .NET API](documentdb-sdk-dotnet.md)來變更集合的效能層級，但程序類似於我們的其他 SDK。</span><span class="sxs-lookup"><span data-stu-id="16eb0-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but the process is similar for our other SDKs.</span></span>

<span data-ttu-id="16eb0-209">以下是變更集合輸送量為每秒 5,000 要求單位的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="16eb0-209">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span></span>
    
```C#
    //Fetch the resource to be updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set the throughput to 5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes to the database by replacing the original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="16eb0-210">請造訪 [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) 以檢視其他範例，並深入了解我們提供的方法：</span><span class="sxs-lookup"><span data-stu-id="16eb0-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="16eb0-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="16eb0-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="16eb0-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="16eb0-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="16eb0-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="16eb0-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="16eb0-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="16eb0-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="16eb0-215">如果我是 EA 客戶會受到什麼影響？</span><span class="sxs-lookup"><span data-stu-id="16eb0-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="16eb0-216">EA 客戶將會受保護的價格，直到其目前合約結束。</span><span class="sxs-lookup"><span data-stu-id="16eb0-216">EA customers will be price protected until the end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16eb0-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16eb0-217">Next steps</span></span>
<span data-ttu-id="16eb0-218">若要深入了解 Azure Cosmos DB 的價格和管理資料，請探索這些資源：</span><span class="sxs-lookup"><span data-stu-id="16eb0-218">To learn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="16eb0-219">[在 Cosmos DB 中分割資料](documentdb-partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="16eb0-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="16eb0-220">了解單一資料分割容器和資料分割容器的差異，以及實作資料分割策略以順暢地調整的秘訣。</span><span class="sxs-lookup"><span data-stu-id="16eb0-220">Understand the difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy to scale seamlessly.</span></span>
2.  <span data-ttu-id="16eb0-221">[Cosmos DB 定價](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="16eb0-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="16eb0-222">深入了解佈建輸送量和使用儲存體的成本。</span><span class="sxs-lookup"><span data-stu-id="16eb0-222">Learn about the cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="16eb0-223">[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="16eb0-223">[Request units](request-units.md).</span></span> <span data-ttu-id="16eb0-224">了解不同作業類型，例如讀取、寫入、查詢的輸送量耗用量。</span><span class="sxs-lookup"><span data-stu-id="16eb0-224">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
