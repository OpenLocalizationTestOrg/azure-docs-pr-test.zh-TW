---
title: "Azure 搜尋中的服務限制 | Microsoft Docs"
description: "容量計劃中使用的服務限制，以及 Azure 搜尋服務要求和回應的最大限制。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: 60e63401e3915e62e1ec5ac03cd548c291580b24
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="service-limits-in-azure-search"></a><span data-ttu-id="fac43-103">Azure 搜尋中的服務限制</span><span class="sxs-lookup"><span data-stu-id="fac43-103">Service limits in Azure Search</span></span>
<span data-ttu-id="fac43-104">儲存體與工作負載的最大限制，以及索引、文件和其他物件的數量上限，皆取決於您是否在**免費**、**基本**，還是**標準**定價層中[佈建 Azure 搜尋服務](search-create-service-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fac43-104">Maximum limits on storage, workloads, and quantities of indexes, documents, and other objects depend on whether you [provision Azure Search](search-create-service-portal.md) at a **Free**, **Basic**, or **Standard** pricing tier.</span></span>

* <span data-ttu-id="fac43-105">**免費** 的是 Azure 訂用帳戶隨附的多租用戶共用服務。</span><span class="sxs-lookup"><span data-stu-id="fac43-105">**Free** is a multi-tenant shared service that comes with your Azure subscription.</span></span> <span data-ttu-id="fac43-106">此為針對現有訂用帳戶提供的免費選項，無須額外費用，可讓您試驗服務後再註冊專用資源。</span><span class="sxs-lookup"><span data-stu-id="fac43-106">It's a no-additional-cost option for existing subscribers that allows you to experiment with the service before signing up for dedicated resources.</span></span>
* <span data-ttu-id="fac43-107">**基本**會針對生產環境工作負載提供較小規模的專用計算資源。</span><span class="sxs-lookup"><span data-stu-id="fac43-107">**Basic** provides dedicated computing resources for production workloads at a smaller scale.</span></span>
* <span data-ttu-id="fac43-108">**標準** 是在專用的機器上執行，在各層級具有更多的儲存和處理容量。</span><span class="sxs-lookup"><span data-stu-id="fac43-108">**Standard** runs on dedicated machines, with more storage and processing capacity at every level.</span></span> <span data-ttu-id="fac43-109">標準共有四個等級︰S1、S2、S3 及 S3 高密度 (S3 HD)。</span><span class="sxs-lookup"><span data-stu-id="fac43-109">Standard comes in four levels: S1, S2, S3, and S3 High Density (S3 HD).</span></span>

> [!NOTE]
> <span data-ttu-id="fac43-110">服務會佈建在特定層。</span><span class="sxs-lookup"><span data-stu-id="fac43-110">A service is provisioned at a specific tier.</span></span> <span data-ttu-id="fac43-111">如果您需要跨層以取得更多容量，您必須佈建新服務 (未提供就地升級)。</span><span class="sxs-lookup"><span data-stu-id="fac43-111">If you need to jump tiers to get more capacity, you must provision a new service (there is no in-place upgrade).</span></span> <span data-ttu-id="fac43-112">如需詳細資訊，請參閱[選擇 SKU 或階層](search-sku-tier.md)。</span><span class="sxs-lookup"><span data-stu-id="fac43-112">For more information, see [Choose a SKU or tier](search-sku-tier.md).</span></span> <span data-ttu-id="fac43-113">若要深入了解如何在已佈建的服務內調整容量，請參閱[調整適用於查詢和編製索引工作負載的資源等級](search-capacity-planning.md)。</span><span class="sxs-lookup"><span data-stu-id="fac43-113">To learn more about adjusting capacity within a service you've already provisioned, see [Scale resource levels for query and indexing workloads](search-capacity-planning.md).</span></span>
>

## <a name="per-subscription-limits"></a><span data-ttu-id="fac43-114">每一訂用帳戶限制</span><span class="sxs-lookup"><span data-stu-id="fac43-114">Per subscription limits</span></span>
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a><span data-ttu-id="fac43-115">每一服務限制</span><span class="sxs-lookup"><span data-stu-id="fac43-115">Per service limits</span></span>
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a><span data-ttu-id="fac43-116">每一索引限制</span><span class="sxs-lookup"><span data-stu-id="fac43-116">Per index limits</span></span>
<span data-ttu-id="fac43-117">索引限制與索引子限制之間有一對一的對應關係。</span><span class="sxs-lookup"><span data-stu-id="fac43-117">There is a one-to-one correspondence between limits on indexes and limits on indexers.</span></span> <span data-ttu-id="fac43-118">若限制 200 個索引，則在相同服務中，索引子的最大限制也是為 200 個。</span><span class="sxs-lookup"><span data-stu-id="fac43-118">Given a limit of 200 indexes, the maximum limit for indexers is also 200 for the same service.</span></span>

| <span data-ttu-id="fac43-119">資源</span><span class="sxs-lookup"><span data-stu-id="fac43-119">Resource</span></span> | <span data-ttu-id="fac43-120">免費</span><span class="sxs-lookup"><span data-stu-id="fac43-120">Free</span></span> | <span data-ttu-id="fac43-121">基本</span><span class="sxs-lookup"><span data-stu-id="fac43-121">Basic</span></span> | <span data-ttu-id="fac43-122">S1</span><span class="sxs-lookup"><span data-stu-id="fac43-122">S1</span></span> | <span data-ttu-id="fac43-123">S2</span><span class="sxs-lookup"><span data-stu-id="fac43-123">S2</span></span> | <span data-ttu-id="fac43-124">S3</span><span class="sxs-lookup"><span data-stu-id="fac43-124">S3</span></span> | <span data-ttu-id="fac43-125">S3 HD</span><span class="sxs-lookup"><span data-stu-id="fac43-125">S3 HD</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fac43-126">索引︰每個索引的欄位上限</span><span class="sxs-lookup"><span data-stu-id="fac43-126">Index: maximum fields per index</span></span> |<span data-ttu-id="fac43-127">1000</span><span class="sxs-lookup"><span data-stu-id="fac43-127">1000</span></span> |<span data-ttu-id="fac43-128">100 <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fac43-128">100 <sup>1</sup></span></span> |<span data-ttu-id="fac43-129">1000</span><span class="sxs-lookup"><span data-stu-id="fac43-129">1000</span></span> |<span data-ttu-id="fac43-130">1000</span><span class="sxs-lookup"><span data-stu-id="fac43-130">1000</span></span> |<span data-ttu-id="fac43-131">1000</span><span class="sxs-lookup"><span data-stu-id="fac43-131">1000</span></span> |<span data-ttu-id="fac43-132">1000</span><span class="sxs-lookup"><span data-stu-id="fac43-132">1000</span></span> |
| <span data-ttu-id="fac43-133">索引：每個索引的評分設定檔上限</span><span class="sxs-lookup"><span data-stu-id="fac43-133">Index: maximum scoring profiles per index</span></span> |<span data-ttu-id="fac43-134">100</span><span class="sxs-lookup"><span data-stu-id="fac43-134">100</span></span> |<span data-ttu-id="fac43-135">100</span><span class="sxs-lookup"><span data-stu-id="fac43-135">100</span></span> |<span data-ttu-id="fac43-136">100</span><span class="sxs-lookup"><span data-stu-id="fac43-136">100</span></span> |<span data-ttu-id="fac43-137">100</span><span class="sxs-lookup"><span data-stu-id="fac43-137">100</span></span> |<span data-ttu-id="fac43-138">100</span><span class="sxs-lookup"><span data-stu-id="fac43-138">100</span></span> |<span data-ttu-id="fac43-139">100</span><span class="sxs-lookup"><span data-stu-id="fac43-139">100</span></span> |
| <span data-ttu-id="fac43-140">索引：每個設定檔的函式上限</span><span class="sxs-lookup"><span data-stu-id="fac43-140">Index: maximum functions per profile</span></span> |<span data-ttu-id="fac43-141">8</span><span class="sxs-lookup"><span data-stu-id="fac43-141">8</span></span> |<span data-ttu-id="fac43-142">8</span><span class="sxs-lookup"><span data-stu-id="fac43-142">8</span></span> |<span data-ttu-id="fac43-143">8</span><span class="sxs-lookup"><span data-stu-id="fac43-143">8</span></span> |<span data-ttu-id="fac43-144">8</span><span class="sxs-lookup"><span data-stu-id="fac43-144">8</span></span> |<span data-ttu-id="fac43-145">8</span><span class="sxs-lookup"><span data-stu-id="fac43-145">8</span></span> |<span data-ttu-id="fac43-146">8</span><span class="sxs-lookup"><span data-stu-id="fac43-146">8</span></span> |
| <span data-ttu-id="fac43-147">索引子︰每次叫用的索引編製負載上限</span><span class="sxs-lookup"><span data-stu-id="fac43-147">Indexers: maximum indexing load per invocation</span></span> |<span data-ttu-id="fac43-148">10,000 份文件</span><span class="sxs-lookup"><span data-stu-id="fac43-148">10,000 documents</span></span> |<span data-ttu-id="fac43-149">僅限制文件上限</span><span class="sxs-lookup"><span data-stu-id="fac43-149">Limited only by maximum documents</span></span> |<span data-ttu-id="fac43-150">僅限制文件上限</span><span class="sxs-lookup"><span data-stu-id="fac43-150">Limited only by maximum documents</span></span> |<span data-ttu-id="fac43-151">僅限制文件上限</span><span class="sxs-lookup"><span data-stu-id="fac43-151">Limited only by maximum documents</span></span> |<span data-ttu-id="fac43-152">僅限制文件上限</span><span class="sxs-lookup"><span data-stu-id="fac43-152">Limited only by maximum documents</span></span> |<span data-ttu-id="fac43-153">N/A <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fac43-153">N/A <sup>2</sup></span></span> |
| <span data-ttu-id="fac43-154">索引子︰執行時間上限</span><span class="sxs-lookup"><span data-stu-id="fac43-154">Indexers: maximum running time</span></span> | <span data-ttu-id="fac43-155">1-3 分鐘 <sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="fac43-155">1-3 minutes <sup>3</sup></span></span> |<span data-ttu-id="fac43-156">24 小時</span><span class="sxs-lookup"><span data-stu-id="fac43-156">24 hours</span></span> |<span data-ttu-id="fac43-157">24 小時</span><span class="sxs-lookup"><span data-stu-id="fac43-157">24 hours</span></span> |<span data-ttu-id="fac43-158">24 小時</span><span class="sxs-lookup"><span data-stu-id="fac43-158">24 hours</span></span> |<span data-ttu-id="fac43-159">24 小時</span><span class="sxs-lookup"><span data-stu-id="fac43-159">24 hours</span></span> |<span data-ttu-id="fac43-160">N/A <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fac43-160">N/A <sup>2</sup></span></span> |
| <span data-ttu-id="fac43-161">Blob 索引子︰Blob 大小上限，MB</span><span class="sxs-lookup"><span data-stu-id="fac43-161">Blob indexer: maximum blob size, MB</span></span> |<span data-ttu-id="fac43-162">16</span><span class="sxs-lookup"><span data-stu-id="fac43-162">16</span></span> |<span data-ttu-id="fac43-163">16</span><span class="sxs-lookup"><span data-stu-id="fac43-163">16</span></span> |<span data-ttu-id="fac43-164">128</span><span class="sxs-lookup"><span data-stu-id="fac43-164">128</span></span> |<span data-ttu-id="fac43-165">256</span><span class="sxs-lookup"><span data-stu-id="fac43-165">256</span></span> |<span data-ttu-id="fac43-166">256</span><span class="sxs-lookup"><span data-stu-id="fac43-166">256</span></span> |<span data-ttu-id="fac43-167">N/A <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fac43-167">N/A <sup>2</sup></span></span> |
| <span data-ttu-id="fac43-168">Blob 索引子︰從 Blob 擷取的內容字元數上限</span><span class="sxs-lookup"><span data-stu-id="fac43-168">Blob indexer: maximum characters of content extracted from a blob</span></span> |<span data-ttu-id="fac43-169">32,000</span><span class="sxs-lookup"><span data-stu-id="fac43-169">32,000</span></span> |<span data-ttu-id="fac43-170">64,000</span><span class="sxs-lookup"><span data-stu-id="fac43-170">64,000</span></span> |<span data-ttu-id="fac43-171">4 百萬</span><span class="sxs-lookup"><span data-stu-id="fac43-171">4 million</span></span> |<span data-ttu-id="fac43-172">4 百萬</span><span class="sxs-lookup"><span data-stu-id="fac43-172">4 million</span></span> |<span data-ttu-id="fac43-173">4 百萬</span><span class="sxs-lookup"><span data-stu-id="fac43-173">4 million</span></span> |<span data-ttu-id="fac43-174">N/A <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fac43-174">N/A <sup>2</sup></span></span> |

<span data-ttu-id="fac43-175"><sup>1</sup> 基本層是唯一具有較低限制 (每個索引 100 個欄位) 的 SKU。</span><span class="sxs-lookup"><span data-stu-id="fac43-175"><sup>1</sup> Basic tier is the only SKU with a lower limit of 100 fields per index.</span></span>

<span data-ttu-id="fac43-176"><sup>2</sup> S3 HD 目前不支援索引子。</span><span class="sxs-lookup"><span data-stu-id="fac43-176"><sup>2</sup> S3 HD doesn't currently support indexers.</span></span> <span data-ttu-id="fac43-177">如果您對此功能有迫切的需求，請連絡 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="fac43-177">Contact Azure Support if you have an urgent need for this capability.</span></span>

<span data-ttu-id="fac43-178"><sup>3</sup> 免費層的索引子執行時間上限，針對 Blob 來源為 3 分鐘，針對其他所有資料來源為 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="fac43-178"><sup>3</sup> Indexer maximum execution time for the Free tier is 3 minutes for blob sources and 1 minute for all other data sources.</span></span>

## <a name="document-size-limits"></a><span data-ttu-id="fac43-179">文件大小限制</span><span class="sxs-lookup"><span data-stu-id="fac43-179">Document size limits</span></span>
| <span data-ttu-id="fac43-180">資源</span><span class="sxs-lookup"><span data-stu-id="fac43-180">Resource</span></span> | <span data-ttu-id="fac43-181">免費</span><span class="sxs-lookup"><span data-stu-id="fac43-181">Free</span></span> | <span data-ttu-id="fac43-182">基本</span><span class="sxs-lookup"><span data-stu-id="fac43-182">Basic</span></span> | <span data-ttu-id="fac43-183">S1</span><span class="sxs-lookup"><span data-stu-id="fac43-183">S1</span></span> | <span data-ttu-id="fac43-184">S2</span><span class="sxs-lookup"><span data-stu-id="fac43-184">S2</span></span> | <span data-ttu-id="fac43-185">S3</span><span class="sxs-lookup"><span data-stu-id="fac43-185">S3</span></span> | <span data-ttu-id="fac43-186">S3 HD</span><span class="sxs-lookup"><span data-stu-id="fac43-186">S3 HD</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fac43-187">每個索引 API 的文件大小</span><span class="sxs-lookup"><span data-stu-id="fac43-187">Individual document size per Index API</span></span> |<span data-ttu-id="fac43-188"><16 MB</span><span class="sxs-lookup"><span data-stu-id="fac43-188"><16 MB</span></span> |<span data-ttu-id="fac43-189"><16 MB</span><span class="sxs-lookup"><span data-stu-id="fac43-189"><16 MB</span></span> |<span data-ttu-id="fac43-190"><16 MB</span><span class="sxs-lookup"><span data-stu-id="fac43-190"><16 MB</span></span> |<span data-ttu-id="fac43-191"><16 MB</span><span class="sxs-lookup"><span data-stu-id="fac43-191"><16 MB</span></span> |<span data-ttu-id="fac43-192"><16 MB</span><span class="sxs-lookup"><span data-stu-id="fac43-192"><16 MB</span></span> |<span data-ttu-id="fac43-193"><16 MB</span><span class="sxs-lookup"><span data-stu-id="fac43-193"><16 MB</span></span> |

<span data-ttu-id="fac43-194">指呼叫「索引 API」時的文件大小上限。</span><span class="sxs-lookup"><span data-stu-id="fac43-194">Refers to the maximum document size when calling an Index API.</span></span> <span data-ttu-id="fac43-195">文件大小是索引 API 要求主體大小的實際限制。</span><span class="sxs-lookup"><span data-stu-id="fac43-195">Document size is actually a limit on the size of the Index API request body.</span></span> <span data-ttu-id="fac43-196">由於您可以一次將多份文件整批傳遞給「索引 API」，因此大小限制實際上取決於批次中的文件數量。</span><span class="sxs-lookup"><span data-stu-id="fac43-196">Since you can pass a batch of multiple documents to the Index API at once, the size limit actually depends on how many documents are in the batch.</span></span> <span data-ttu-id="fac43-197">針對具有單一文件的批次，文件大小上限為 16 MB 的 JSON。</span><span class="sxs-lookup"><span data-stu-id="fac43-197">For a batch with a single document, the maximum document size is 16 MB of JSON.</span></span>

<span data-ttu-id="fac43-198">為了降低文件大小，請記得從要求中排除不可查詢的資料。</span><span class="sxs-lookup"><span data-stu-id="fac43-198">To keep document size down, remember to exclude non-queryable data from the request.</span></span> <span data-ttu-id="fac43-199">影像和其他二進位資料無法執行查詢，而且不應該儲存於索引中。</span><span class="sxs-lookup"><span data-stu-id="fac43-199">Images and other binary data are not directly queryable and shouldn't be stored in the index.</span></span> <span data-ttu-id="fac43-200">若要將不可搜尋的資料整合到搜尋結果，請定義不可搜尋的欄位，將 URL 參考儲存於資源中。</span><span class="sxs-lookup"><span data-stu-id="fac43-200">To integrate non-queryable data into search results, define a non-searchable field that stores a URL reference to the resource.</span></span>

## <a name="workload-limits-queries-per-second"></a><span data-ttu-id="fac43-201">工作負載限制 (每秒查詢次數)</span><span class="sxs-lookup"><span data-stu-id="fac43-201">Workload limits (Queries per second)</span></span>
| <span data-ttu-id="fac43-202">資源</span><span class="sxs-lookup"><span data-stu-id="fac43-202">Resource</span></span> | <span data-ttu-id="fac43-203">免費</span><span class="sxs-lookup"><span data-stu-id="fac43-203">Free</span></span> | <span data-ttu-id="fac43-204">基本</span><span class="sxs-lookup"><span data-stu-id="fac43-204">Basic</span></span> | <span data-ttu-id="fac43-205">S1</span><span class="sxs-lookup"><span data-stu-id="fac43-205">S1</span></span> | <span data-ttu-id="fac43-206">S2</span><span class="sxs-lookup"><span data-stu-id="fac43-206">S2</span></span> | <span data-ttu-id="fac43-207">S3</span><span class="sxs-lookup"><span data-stu-id="fac43-207">S3</span></span> | <span data-ttu-id="fac43-208">S3 HD</span><span class="sxs-lookup"><span data-stu-id="fac43-208">S3 HD</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fac43-209">QPS</span><span class="sxs-lookup"><span data-stu-id="fac43-209">QPS</span></span> |<span data-ttu-id="fac43-210">N/A </span><span class="sxs-lookup"><span data-stu-id="fac43-210">N/A</span></span> |<span data-ttu-id="fac43-211">~3/每個複本</span><span class="sxs-lookup"><span data-stu-id="fac43-211">~3 per replica</span></span> |<span data-ttu-id="fac43-212">~15/每個複本</span><span class="sxs-lookup"><span data-stu-id="fac43-212">~15 per replica</span></span> |<span data-ttu-id="fac43-213">~60/每個複本</span><span class="sxs-lookup"><span data-stu-id="fac43-213">~60 per replica</span></span> |<span data-ttu-id="fac43-214">>60/每個複本</span><span class="sxs-lookup"><span data-stu-id="fac43-214">>60 per replica</span></span> |<span data-ttu-id="fac43-215">>60/每個複本</span><span class="sxs-lookup"><span data-stu-id="fac43-215">>60 per replica</span></span> |

<span data-ttu-id="fac43-216">每秒查詢次數 (QPS) 是根據啟發學習法所得的近似值，這是使用模擬及實際的客戶工作負載來導出的估計值。</span><span class="sxs-lookup"><span data-stu-id="fac43-216">Queries per second (QPS) is an approximation based on heuristics, using simulated and actual customer workloads to derive estimated values.</span></span> <span data-ttu-id="fac43-217">確實的 QPS 輸送量會視您的資料和查詢本質而有所差異。</span><span class="sxs-lookup"><span data-stu-id="fac43-217">Exact QPS throughput varies depending on your data and the nature of the query.</span></span>

<span data-ttu-id="fac43-218">雖然上面提供粗略的估計值，但是實際的查詢率難以判斷，尤其是在輸送量會依可用頻寬和系統資源競爭而有所不同的「免費」共用服務中。</span><span class="sxs-lookup"><span data-stu-id="fac43-218">Although rough estimates are provided above, an actual rate is difficult to determine, especially in the Free shared service where throughput is based on available bandwidth and competition for system resources.</span></span> <span data-ttu-id="fac43-219">在「免費層」中，運算資源和儲存體資源是由多個訂用帳戶共用，因此您解決方案的 QPS 將一律依有多少其他工作負載在同時執行而有所不同。</span><span class="sxs-lookup"><span data-stu-id="fac43-219">In the Free tier, compute and storage resources are shared by multiple subscribers, so QPS for your solution will always vary depending on how many other workloads are running at the same time.</span></span>

<span data-ttu-id="fac43-220">在標準層級中，由於可控制較多的參數，所以能更準確地估計 QPS。</span><span class="sxs-lookup"><span data-stu-id="fac43-220">At the standard level, you can estimate QPS more closely because you have control over more of the parameters.</span></span> <span data-ttu-id="fac43-221">如需有關如何計算您工作負載之 QPS 的指引，請參閱 [管理您的搜尋解決方案](search-manage.md) 。</span><span class="sxs-lookup"><span data-stu-id="fac43-221">See the best practices section in [Manage your search solution](search-manage.md) for guidance on how to calculate QPS for your workloads.</span></span>

## <a name="api-request-limits"></a><span data-ttu-id="fac43-222">API 要求限制</span><span class="sxs-lookup"><span data-stu-id="fac43-222">API Request limits</span></span>
* <span data-ttu-id="fac43-223">每個要求最多 16 MB <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fac43-223">Maximum of 16 MB per request <sup>1</sup></span></span>
* <span data-ttu-id="fac43-224">最長 8 KB 的 URL 長度</span><span class="sxs-lookup"><span data-stu-id="fac43-224">Maximum 8 KB URL length</span></span>
* <span data-ttu-id="fac43-225">每個索引上傳、合併、或刪除批次最多包含 1000 個文件</span><span class="sxs-lookup"><span data-stu-id="fac43-225">Maximum 1000 documents per batch of index uploads, merges, or deletes</span></span>
* <span data-ttu-id="fac43-226">$orderby 子句中最多 32 個欄位</span><span class="sxs-lookup"><span data-stu-id="fac43-226">Maximum 32 fields in $orderby clause</span></span>
* <span data-ttu-id="fac43-227">最大搜尋詞彙的大小是 utf-8 編碼文字的 32,766 個位元組 (32 KB 減 2 個位元組)</span><span class="sxs-lookup"><span data-stu-id="fac43-227">Maximum search term size is 32,766 bytes (32 KB minus 2 bytes) of UTF-8 encoded text</span></span>

<span data-ttu-id="fac43-228"><sup>1</sup> 在「Azure 搜尋服務」中，要求主體的上限是 16 MB，這會針對不受理論上限制約束之個別欄位或集合的內容強加實際限制 (如需有關欄位組合和限制的詳細資訊，請參閱[支援的資料類型](https://msdn.microsoft.com/library/azure/dn798938.aspx))。</span><span class="sxs-lookup"><span data-stu-id="fac43-228"><sup>1</sup> In Azure Search, the body of a request is subject to an upper limit of 16 MB, imposing a practical limit on the contents of individual fields or collections that are not otherwise constrained by theoretical limits (see [Supported data types](https://msdn.microsoft.com/library/azure/dn798938.aspx) for more information about field composition and restrictions).</span></span>

## <a name="api-response-limits"></a><span data-ttu-id="fac43-229">API 回應限制</span><span class="sxs-lookup"><span data-stu-id="fac43-229">API Response limits</span></span>
* <span data-ttu-id="fac43-230">每一頁搜尋結果最多傳回 1000 個文件</span><span class="sxs-lookup"><span data-stu-id="fac43-230">Maximum 1000 documents returned per page of search results</span></span>
* <span data-ttu-id="fac43-231">每個建議 API 要求最多傳回 100 個建議</span><span class="sxs-lookup"><span data-stu-id="fac43-231">Maximum 100 suggestions returned per Suggest API request</span></span>

## <a name="api-key-limits"></a><span data-ttu-id="fac43-232">API 金鑰限制</span><span class="sxs-lookup"><span data-stu-id="fac43-232">API Key limits</span></span>
<span data-ttu-id="fac43-233">API 金鑰可用於服務驗證。</span><span class="sxs-lookup"><span data-stu-id="fac43-233">Api-keys are used for service authentication.</span></span> <span data-ttu-id="fac43-234">有兩種類型。</span><span class="sxs-lookup"><span data-stu-id="fac43-234">There are two types.</span></span> <span data-ttu-id="fac43-235">系統管理金鑰是在要求標頭中指定，並會授與完整的服務讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="fac43-235">Admin keys are specified in the request header and grant full read-write access to the service.</span></span> <span data-ttu-id="fac43-236">查詢金鑰為唯讀並在 URL 上指定，且通常會發佈到用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="fac43-236">Query keys are read-only, specified on the URL, and typically distributed to client applications.</span></span>

* <span data-ttu-id="fac43-237">每個服務最多 2 個系統管理金鑰</span><span class="sxs-lookup"><span data-stu-id="fac43-237">Maximum of 2 admin keys per service</span></span>
* <span data-ttu-id="fac43-238">每個服務最多 50 個查詢金鑰</span><span class="sxs-lookup"><span data-stu-id="fac43-238">Maximum of 50 query keys per service</span></span>