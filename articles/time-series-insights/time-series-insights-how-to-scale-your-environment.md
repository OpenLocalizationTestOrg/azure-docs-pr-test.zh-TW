---
title: "aaaHow tooscale Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "本教學課程涵蓋如何 tooscale Azure 時間數列 Insights 環境"
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
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="8495c-103">如何 tooscale 時間數列 Insights 環境</span><span class="sxs-lookup"><span data-stu-id="8495c-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="8495c-104">本教學課程涵蓋如何 tooscale 時間數列 Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="8495c-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="8495c-105">若 SKU 類型不同則無法進行相應增加。</span><span class="sxs-lookup"><span data-stu-id="8495c-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="8495c-106">S1 SKU 的環境不能轉換成 S2 環境。</span><span class="sxs-lookup"><span data-stu-id="8495c-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="8495c-107">S1 SKU 輸入速率和容量</span><span class="sxs-lookup"><span data-stu-id="8495c-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="8495c-108">S1 SKU 容量</span><span class="sxs-lookup"><span data-stu-id="8495c-108">S1 SKU Capacity</span></span> | <span data-ttu-id="8495c-109">輸入速率</span><span class="sxs-lookup"><span data-stu-id="8495c-109">Ingress Rate</span></span> | <span data-ttu-id="8495c-110">儲存體容量上限</span><span class="sxs-lookup"><span data-stu-id="8495c-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="8495c-111">1</span><span class="sxs-lookup"><span data-stu-id="8495c-111">1</span></span> | <span data-ttu-id="8495c-112">1 GB (1 百萬個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-112">1 GB (1 million events)</span></span> | <span data-ttu-id="8495c-113">一個月 30 GB (3 千萬個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="8495c-114">10</span><span class="sxs-lookup"><span data-stu-id="8495c-114">10</span></span> | <span data-ttu-id="8495c-115">10 GB (1 千萬個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-115">10 GB (10 million events)</span></span> | <span data-ttu-id="8495c-116">一個月 300 GB (3 億個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="8495c-117">S2 SKU 輸入速率和容量</span><span class="sxs-lookup"><span data-stu-id="8495c-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="8495c-118">S2 SKU 容量</span><span class="sxs-lookup"><span data-stu-id="8495c-118">S2 SKU Capacity</span></span> | <span data-ttu-id="8495c-119">輸入速率</span><span class="sxs-lookup"><span data-stu-id="8495c-119">Ingress Rate</span></span> | <span data-ttu-id="8495c-120">儲存體容量上限</span><span class="sxs-lookup"><span data-stu-id="8495c-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="8495c-121">1</span><span class="sxs-lookup"><span data-stu-id="8495c-121">1</span></span> | <span data-ttu-id="8495c-122">10 GB (1 千萬個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-122">10 GB (10 million events)</span></span> | <span data-ttu-id="8495c-123">一個月 300 GB (3 億個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="8495c-124">10</span><span class="sxs-lookup"><span data-stu-id="8495c-124">10</span></span> | <span data-ttu-id="8495c-125">100 GB (1 億個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-125">100 GB (100 million events)</span></span> | <span data-ttu-id="8495c-126">一個月 3 TB (30 億個事件)</span><span class="sxs-lookup"><span data-stu-id="8495c-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="8495c-127">容量是以線性方式擴充或減少，因此容量 2 的 S1 SKU 支援的輸入速率為一天 2 GB (2 百萬) 的事件，和 一個月 60 GB (6 千萬個事件)。</span><span class="sxs-lookup"><span data-stu-id="8495c-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="8495c-128">變更環境的 hello 容量</span><span class="sxs-lookup"><span data-stu-id="8495c-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="8495c-129">在 hello Azure 入口網站，選取 hello 環境的容量想 toochange。</span><span class="sxs-lookup"><span data-stu-id="8495c-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="8495c-130">在 [設定] 下方按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="8495c-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="8495c-131">使用 hello 容量滑桿 tooselect hello 產能符合您的輸入速率的 hello 需求和儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="8495c-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8495c-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8495c-132">Next steps</span></span>

* <span data-ttu-id="8495c-133">確認 hello 新容量足夠 tooprevent 節流。</span><span class="sxs-lookup"><span data-stu-id="8495c-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="8495c-134">如需詳細資訊，請參閱 hello*您的環境可能會節流*區段[這裡](time-series-insights-diagnose-and-solve-problems.md)。</span><span class="sxs-lookup"><span data-stu-id="8495c-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
