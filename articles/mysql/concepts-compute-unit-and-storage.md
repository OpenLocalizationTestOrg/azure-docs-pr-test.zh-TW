---
title: "說明適用於 MySQL 的 Azure 資料庫中的計算單位 | Microsoft Docs"
description: "適用於 MySQL 的 Azure DB：本文說明計算單位的概念，以及當您的工作負載到達計算單位上限時，會發生什麼狀況。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: a82c283df688d36cd284973312e276f30ed893c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a><span data-ttu-id="bbcc7-103">說明適用於 MySQL 的 Azure 資料庫中的計算單位</span><span class="sxs-lookup"><span data-stu-id="bbcc7-103">Explaining Compute Units in Azure Database for MySQL</span></span>
<span data-ttu-id="bbcc7-104">本文說明計算單位的概念，以及當您的工作負載到達計算單位上限時，會發生什麼狀況。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-104">This article explains the concept of Compute Units and what happens when your workload reaches the maximum Compute Units.</span></span>

## <a name="what-are-compute-units"></a><span data-ttu-id="bbcc7-105">什麼是計算單位？</span><span class="sxs-lookup"><span data-stu-id="bbcc7-105">What are Compute Units?</span></span>
<span data-ttu-id="bbcc7-106">計算單位是 CPU 處理輸送量的量值，保證可供單一適用於 MySQL 伺服器的 Azure 資料庫使用。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-106">Compute Units are a measure of CPU processing throughput that is guaranteed to be available to a single Azure Database for MySQL server.</span></span> <span data-ttu-id="bbcc7-107">計算單位是 CPU 和記憶體資源的混合量值。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-107">A Compute Unit is a blended measure of CPU and memory resources.</span></span> <span data-ttu-id="bbcc7-108">一般而言，50 個計算單位等於半個核心。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-108">In general, 50 Compute Units equate to half of a core.</span></span> <span data-ttu-id="bbcc7-109">100 個計算單位等於一個核心。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-109">100 Compute Units equate to one core.</span></span> <span data-ttu-id="bbcc7-110">2000 個計算單位等於 20 個保證可供您伺服器使用之處理輸送量的核心。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-110">2000 Compute Units equate to twenty cores of guaranteed processing throughput available to your server.</span></span>

<span data-ttu-id="bbcc7-111">每個計算單位的記憶體數量會針對基本和標準定價層進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-111">The amount of memory per Compute Unit is optimized for the Basic and Standard pricing tiers.</span></span> <span data-ttu-id="bbcc7-112">藉由提升效能等級來使計算單位數加倍，等於讓該單一適用於 MySQL 的 Azure 資料庫可用的資源集合加倍。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-112">Doubling the Compute Units by increasing the performance level equates to doubling the set of resource available to that single Azure Database for MySQL.</span></span>

<span data-ttu-id="bbcc7-113">例如，標準的 800 個計算單位所提供的 CPU 輸送量與記憶體，比標準的 100 個計算單位設定多 8 倍。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-113">For example, a Standard 800 Compute Units provides 8x more CPU throughput and memory than a Standard 100 Compute Units configuration.</span></span> <span data-ttu-id="bbcc7-114">不過，儘管相較於基本的 100 個計算單位，標準的 100 個計算單位會提供相同的 CPU 輸送量，但是，標準定價層中預先設定的記憶體量是針對基本定價層所設定之記憶體量的兩倍。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-114">However, while Standard 100 Compute Units provide the same CPU throughput compared to Basic 100 Compute Units, the amount of memory that is pre-configured in Standard pricing tier is double the amount of memory configured for Basic pricing tier.</span></span> <span data-ttu-id="bbcc7-115">因此，比起選取相同計算單位數的基本定價層，標準定價層提供更佳的工作負載效能與更低的交易延遲。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-115">Therefore, Standard pricing tier provides better workload performance and lower transaction latency than Basic pricing tier with the same Compute Units selected.</span></span>

## <a name="how-can-i-determine-the-number-of-compute-units-needed-for-my-workload"></a><span data-ttu-id="bbcc7-116">如何判斷我的工作負載所需的計算單位數？</span><span class="sxs-lookup"><span data-stu-id="bbcc7-116">How can I determine the number of Compute Units needed for my workload?</span></span>
<span data-ttu-id="bbcc7-117">如果您打算移轉在內部部署或虛擬機器上執行的現有 MySQL 伺服器，可透過評估工作負載需要多少個處理輸送量核心，來決定計算單位數。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-117">If you are looking to migrate an existing MySQL server running on-premises or on a virtual machine, you can determine the number of Compute Units by estimating how many cores of processing throughput your workload needs.</span></span> 

<span data-ttu-id="bbcc7-118">如果您現有的內部部署或虛擬機器伺服器目前使用 4 個核心 (不含計算 CPU 超執行緒)，一開始請為適用於 MySQL 伺服器的 Azure 資料庫設定 400 個計算單位。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-118">If your existing on-premises or virtual machine server is currently utilizing 4 cores (without counting CPU hyperthread), start by configuring 400 Compute Units for your Azure Database for MySQL server.</span></span> <span data-ttu-id="bbcc7-119">計算單位可根據您的工作負載需求，動態地相應增加或減少，而且幾乎不會產生任何應用程式停機時間。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-119">Compute Units can be dynamically scaled up or down depending on your workload needs with virtually no application downtime.</span></span> 

<span data-ttu-id="bbcc7-120">在 Azure 入口網站中監視計量圖表，或是撰寫 Azure CLI 命令來測量計算單位。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-120">Monitor the Metrics graph in the Azure portal or write Azure CLI commands -to measure compute units.</span></span> <span data-ttu-id="bbcc7-121">要監視的相關計量包括計算單位百分比和計算單位限制。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-121">Relevant metrics to monitor are the Compute Unit percentage and Compute Unit limit.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="bbcc7-122">如果您發現儲存體 IOPS 未完全用到極限，請考慮同時監視計算單位使用率。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-122">If you find storage IOPS are not fully utilized to the maximum, consider monitoring the compute units utilization as well.</span></span> <span data-ttu-id="bbcc7-123">提高計算單位會減少由於 CPU 或記憶體有限所造成的效能瓶頸，因此可能會提高 IO 輸送量。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-123">Raising the Compute Units may allow for higher IO throughput by lessening the performance bottleneck due to limited CPU or memory.</span></span>

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a><span data-ttu-id="bbcc7-124">當我達到計算單位上限時會發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="bbcc7-124">What happens when I hit my maximum Compute Units?</span></span>
<span data-ttu-id="bbcc7-125">效能等級會受校正和管理，以提供資源來將您的資料庫工作負載執行到所選定價層和效能等級的上限。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-125">Performance levels are calibrated and governed to provide resources to run your database workload up to the max limits for the selected pricing tier and performance level.</span></span> 

<span data-ttu-id="bbcc7-126">如果您的工作負載達到計算單位或已佈建 IOPS 限制的上限，您可以繼續利用最大允許層級的資源，但可能會經歷較長的查詢延遲。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-126">If your workload reaches the maximum limits in either the Compute Units or provisioned IOPS limits, you can continue to utilize the resources at the maximum allowed level, but your queries are likely to see increased latencies.</span></span> <span data-ttu-id="bbcc7-127">這些限制並不會導致任何錯誤，但除非是速度慢到使查詢逾時，否則會使工作負載速度變慢。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-127">These limits do not result in any errors, but rather a slowdown in the workload, unless the slowdown becomes so severe that queries time out.</span></span> 

<span data-ttu-id="bbcc7-128">如果您的工作負載到達連線數目上限，則會引發明確的錯誤。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-128">If your workload reaches the maximum limits on number of connections, explicit errors are raised.</span></span> <span data-ttu-id="bbcc7-129">如需資源限制的詳細資訊，請參閱[適用於 MySQL 的 Azure 資料庫中的限制](concepts-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-129">For more information on resources limits, see [Limitations in Azure Database for MySQL](concepts-limits.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbcc7-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bbcc7-130">Next steps</span></span>
<span data-ttu-id="bbcc7-131">如需定價層的詳細資訊，請參閱[適用於 MySQL 的 Azure 資料庫定價層](./concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="bbcc7-131">For more information on pricing tiers, see [Azure Database for MySQL pricing tiers](./concepts-service-tiers.md).</span></span>
