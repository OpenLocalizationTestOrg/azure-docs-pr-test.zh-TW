---
title: "如何調整您的 Azure Time Series Insights 環境規模 | Microsoft Docs"
description: "本教學課程將說明如何調整您的 Azure Time Series Insights 環境規模"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 8f6c66ea2173c98179ec899d6626c2ab6f7ec4b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-your-time-series-insights-environment"></a><span data-ttu-id="81ed5-103">如何調整您的 Time Series Insights 環境規模</span><span class="sxs-lookup"><span data-stu-id="81ed5-103">How to scale your Time Series Insights environment</span></span>

<span data-ttu-id="81ed5-104">本教學課程將說明如何調整您的 Time Series Insights 環境規模。</span><span class="sxs-lookup"><span data-stu-id="81ed5-104">This tutorial covers how to scale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="81ed5-105">若 SKU 類型不同則無法進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="81ed5-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="81ed5-106">S1 SKU 的環境不能轉換成 S2 環境。</span><span class="sxs-lookup"><span data-stu-id="81ed5-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="81ed5-107">S1 SKU 輸入速率和容量</span><span class="sxs-lookup"><span data-stu-id="81ed5-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="81ed5-108">S1 SKU 容量</span><span class="sxs-lookup"><span data-stu-id="81ed5-108">S1 SKU Capacity</span></span> | <span data-ttu-id="81ed5-109">輸入速率</span><span class="sxs-lookup"><span data-stu-id="81ed5-109">Ingress Rate</span></span> | <span data-ttu-id="81ed5-110">儲存體容量上限</span><span class="sxs-lookup"><span data-stu-id="81ed5-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="81ed5-111">1</span><span class="sxs-lookup"><span data-stu-id="81ed5-111">1</span></span> | <span data-ttu-id="81ed5-112">1 GB (1 百萬個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-112">1 GB (1 million events)</span></span> | <span data-ttu-id="81ed5-113">一個月 30 GB (3 千萬個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="81ed5-114">10</span><span class="sxs-lookup"><span data-stu-id="81ed5-114">10</span></span> | <span data-ttu-id="81ed5-115">10 GB (1 千萬個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-115">10 GB (10 million events)</span></span> | <span data-ttu-id="81ed5-116">一個月 300 GB (3 億個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="81ed5-117">S2 SKU 輸入速率和容量</span><span class="sxs-lookup"><span data-stu-id="81ed5-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="81ed5-118">S2 SKU 容量</span><span class="sxs-lookup"><span data-stu-id="81ed5-118">S2 SKU Capacity</span></span> | <span data-ttu-id="81ed5-119">輸入速率</span><span class="sxs-lookup"><span data-stu-id="81ed5-119">Ingress Rate</span></span> | <span data-ttu-id="81ed5-120">儲存體容量上限</span><span class="sxs-lookup"><span data-stu-id="81ed5-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="81ed5-121">1</span><span class="sxs-lookup"><span data-stu-id="81ed5-121">1</span></span> | <span data-ttu-id="81ed5-122">10 GB (1 千萬個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-122">10 GB (10 million events)</span></span> | <span data-ttu-id="81ed5-123">一個月 300 GB (3 億個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="81ed5-124">10</span><span class="sxs-lookup"><span data-stu-id="81ed5-124">10</span></span> | <span data-ttu-id="81ed5-125">100 GB (1 億個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-125">100 GB (100 million events)</span></span> | <span data-ttu-id="81ed5-126">一個月 3 TB (30 億個事件)</span><span class="sxs-lookup"><span data-stu-id="81ed5-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="81ed5-127">容量是以線性方式擴充或減少，因此容量 2 的 S1 SKU 支援的輸入速率為一天 2 GB (2 百萬) 的事件，和 一個月 60 GB (6 千萬個事件)。</span><span class="sxs-lookup"><span data-stu-id="81ed5-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-the-capacity-of-your-environment"></a><span data-ttu-id="81ed5-128">變更您的環境容量</span><span class="sxs-lookup"><span data-stu-id="81ed5-128">Changing the capacity of your environment</span></span>

1. <span data-ttu-id="81ed5-129">在 Azure 入口網站中，選取您想要變更其容量的環境。</span><span class="sxs-lookup"><span data-stu-id="81ed5-129">In the Azure portal, select the environment whose capacity you want to change.</span></span>
1. <span data-ttu-id="81ed5-130">在 [設定] 下方按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="81ed5-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="81ed5-131">使用 [容量] 滑桿來選取符合您所需輸入速率和儲存容量的容量。</span><span class="sxs-lookup"><span data-stu-id="81ed5-131">Use the Capacity slider to select the capacity that meets the requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81ed5-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81ed5-132">Next steps</span></span>

* <span data-ttu-id="81ed5-133">請確定新容量足夠以避免產生節流。</span><span class="sxs-lookup"><span data-stu-id="81ed5-133">Verify that the new capacity is sufficient to prevent throttling.</span></span> <span data-ttu-id="81ed5-134">如需詳細資訊，請參閱[這裡](time-series-insights-diagnose-and-solve-problems.md)的*您的環境可能正在進行節流*一節。</span><span class="sxs-lookup"><span data-stu-id="81ed5-134">For more details, see the *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>