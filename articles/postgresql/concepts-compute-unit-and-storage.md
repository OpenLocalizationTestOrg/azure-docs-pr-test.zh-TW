---
title: "說明適用於 PostgreSQL 的 Azure 資料庫中的計算單位 | Microsoft Docs"
description: "Azure DB PostgreSQL： 本文件說明計算單位，與您的工作負載達到時，會發生什麼情況的 hello 概念 hello 最大的計算單位。"
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 42ec766ff6ce82ceee34d42e0f4a4ad86bc7b45d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-postgresql"></a><span data-ttu-id="89eec-103">說明適用於 PostgreSQL 的 Azure 資料庫中的計算單位</span><span class="sxs-lookup"><span data-stu-id="89eec-103">Explaining Compute Units in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="89eec-104">本文說明的計算單位 hello 概念和工作負載達到 hello 計算的最大單位時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="89eec-104">This article explains hello concept of Compute Units and what happens when your workload reaches hello maximum Compute Units.</span></span>

## <a name="what-are-compute-units"></a><span data-ttu-id="89eec-105">什麼是計算單位？</span><span class="sxs-lookup"><span data-stu-id="89eec-105">What are Compute Units?</span></span>
<span data-ttu-id="89eec-106">計算的單位包括量值的 CPU 處理輸送量保證 toobe 可用 tooa PostgreSQL 伺服器將單一 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="89eec-106">Compute Units are a measure of CPU processing throughput that is guaranteed toobe available tooa single Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="89eec-107">計算單位是 CPU 和記憶體資源的混合量值。</span><span class="sxs-lookup"><span data-stu-id="89eec-107">A Compute Unit is a blended measure of CPU and memory resources.</span></span> <span data-ttu-id="89eec-108">一般來說，50 個計算的單位等同於 toohalf 的核心。</span><span class="sxs-lookup"><span data-stu-id="89eec-108">In general, 50 Compute Units equate toohalf of a core.</span></span> <span data-ttu-id="89eec-109">100 為計算單位等同於 tooone 核心。</span><span class="sxs-lookup"><span data-stu-id="89eec-109">100 Compute Units equate tooone core.</span></span> <span data-ttu-id="89eec-110">2000 計算單位等同於 tootwenty 核心的保證的處理輸送量 tooyour 可用伺服器。</span><span class="sxs-lookup"><span data-stu-id="89eec-110">2000 Compute Units equate tootwenty cores of guaranteed processing throughput available tooyour server.</span></span>

<span data-ttu-id="89eec-111">hello 每個計算的單位的記憶體數量最適合用於 hello 基本及標準定價層。</span><span class="sxs-lookup"><span data-stu-id="89eec-111">hello amount of memory per Compute Unit is optimized for hello Basic and Standard pricing tiers.</span></span> <span data-ttu-id="89eec-112">Hello 效能層級增加加倍 hello 計算單位等同資源可用 toothat toodoubling hello 組 PostgreSQL 將單一 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="89eec-112">Doubling hello Compute Units by increasing hello performance level equates toodoubling hello set of resource available toothat single Azure Database for PostgreSQL.</span></span>

<span data-ttu-id="89eec-113">例如，標準的 800 個計算單位所提供的 CPU 輸送量與記憶體，比標準的 100 個計算單位設定多 8 倍。</span><span class="sxs-lookup"><span data-stu-id="89eec-113">For example, a Standard 800 Compute Units provides 8x more CPU throughput and memory than a Standard 100 Compute Units configuration.</span></span> <span data-ttu-id="89eec-114">相同但是 hello 標準 100 計算單位是提供 CPU 輸送量比較 tooBasic 100 計算單位，hello 已預先設定的標準定價層中的記憶體數量為 double hello 的定價層的基本設定的記憶體的數量。</span><span class="sxs-lookup"><span data-stu-id="89eec-114">However, while Standard 100 Compute Units provide hello same CPU throughput compared tooBasic 100 Compute Units, hello amount of memory that is pre-configured in Standard pricing tier is double hello amount of memory configured for Basic pricing tier.</span></span> <span data-ttu-id="89eec-115">因此，標準定價層提供更好的工作負載效能且比基本定價層，以選取計算的單位相同的 hello 的交易延遲更低。</span><span class="sxs-lookup"><span data-stu-id="89eec-115">Therefore, Standard pricing tier provides better workload performance and lower transaction latency than Basic pricing tier with hello same Compute Units selected.</span></span>

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a><span data-ttu-id="89eec-116">如何判斷我的工作負載所需的計算單位的 hello 數目？</span><span class="sxs-lookup"><span data-stu-id="89eec-116">How can I determine hello number of Compute Units needed for my workload?</span></span>
<span data-ttu-id="89eec-117">如果您要尋找 toomigrate 現有 PostgreSQL 伺服器在內部部署執行或在虛擬機器上，您可以透過評估的處理輸送量多少核心您的工作負載需要判斷 hello 計算的單位數目。</span><span class="sxs-lookup"><span data-stu-id="89eec-117">If you are looking toomigrate an existing PostgreSQL server running on-premises or on a virtual machine, you can determine hello number of Compute Units by estimating how many cores of processing throughput your workload needs.</span></span> 

<span data-ttu-id="89eec-118">如果您現有的內部部署或虛擬機器伺服器目前使用 4 個核心 (不含計算 CPU 超執行緒)，一開始請為適用於 PostgreSQL 伺服器的 Azure 資料庫設定 400 個計算單位。</span><span class="sxs-lookup"><span data-stu-id="89eec-118">If your existing on-premises or virtual machine server is currently utilizing 4 cores (without counting CPU hyperthread), start by configuring 400 Compute Units for your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="89eec-119">計算單位可根據您的工作負載需求，動態地相應增加或減少，而且幾乎不會產生任何應用程式停機時間。</span><span class="sxs-lookup"><span data-stu-id="89eec-119">Compute Units can be dynamically scaled up or down depending on your workload needs with virtually no application downtime.</span></span> 

<span data-ttu-id="89eec-120">在 Azure 入口網站或寫入 Azure CLI 命令-toomeasure hello 監視器 hello 度量圖表會計算單位。</span><span class="sxs-lookup"><span data-stu-id="89eec-120">Monitor hello Metrics graph in hello Azure portal or write Azure CLI commands -toomeasure compute units.</span></span> <span data-ttu-id="89eec-121">相關的度量 toomonitor 為 hello 計算單位百分比和計算的單位的限制。</span><span class="sxs-lookup"><span data-stu-id="89eec-121">Relevant metrics toomonitor are hello Compute Unit percentage and Compute Unit limit.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="89eec-122">如果您發現儲存體 IOPS 不完全利用 toohello 最大值，請考慮監視 hello 運算單位使用率以及。</span><span class="sxs-lookup"><span data-stu-id="89eec-122">If you find storage IOPS are not fully utilized toohello maximum, consider monitoring hello compute units utilization as well.</span></span> <span data-ttu-id="89eec-123">引發 hello 計算的單位可能會允許 IO 輸送量因而 hello 到期 toolimited CPU 或記憶體的效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="89eec-123">Raising hello Compute Units may allow for higher IO throughput by lessening hello performance bottleneck due toolimited CPU or memory.</span></span>

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a><span data-ttu-id="89eec-124">當我達到計算單位上限時會發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="89eec-124">What happens when I hit my maximum Compute Units?</span></span>
<span data-ttu-id="89eec-125">效能層級制定和控管 tooprovide 資源 toorun 資料庫工作負載向上 toohello hello 選取的定價層和效能層級的最大限制。</span><span class="sxs-lookup"><span data-stu-id="89eec-125">Performance levels are calibrated and governed tooprovide resources toorun your database workload up toohello max limits for hello selected pricing tier and performance level.</span></span> 

<span data-ttu-id="89eec-126">如果您的工作負載達到 hello 最大限制是 hello 計算單位或佈建的 IOPS 限制，您可以繼續 tooutilize hello 資源在 hello 最大的允許層級，但您的查詢很有可能 toosee 增加延遲。</span><span class="sxs-lookup"><span data-stu-id="89eec-126">If your workload reaches hello maximum limits in either hello Compute Units or provisioned IOPS limits, you can continue tooutilize hello resources at hello maximum allowed level, but your queries are likely toosee increased latencies.</span></span> <span data-ttu-id="89eec-127">這些限制不會導致任何錯誤，但而是會降低 hello 工作負載，除非 hello 緩慢的問題變成嚴重的查詢逾時。</span><span class="sxs-lookup"><span data-stu-id="89eec-127">These limits do not result in any errors, but rather a slowdown in hello workload, unless hello slowdown becomes so severe that queries time out.</span></span> 

<span data-ttu-id="89eec-128">如果您的工作負載達到 hello 最大連接數目限制，會引發明確的錯誤。</span><span class="sxs-lookup"><span data-stu-id="89eec-128">If your workload reaches hello maximum limits on number of connections, explicit errors are raised.</span></span> <span data-ttu-id="89eec-129">如需資源限制的詳細資訊，請參閱[適用於 PostgreSQL 的 Azure 資料庫中的限制](concepts-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="89eec-129">For more information on resources limits, see [Limitations in Azure Database for PostgreSQL](concepts-limits.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89eec-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89eec-130">Next steps</span></span>
<span data-ttu-id="89eec-131">如需定價層的詳細資訊，請參閱[適用於 PostgreSQL 的 Azure 資料庫定價層](./concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="89eec-131">For more information on pricing tiers, see [Azure Database for PostgreSQL pricing tiers](./concepts-service-tiers.md).</span></span>
