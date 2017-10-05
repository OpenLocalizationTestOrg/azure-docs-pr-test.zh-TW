---
title: "常見的自動調整規模模式概觀 | Microsoft Docs"
description: "了解一些在 Azure 中自動調整資源規模的常見模式。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="b014f-103">常見的自動調整規模模式概觀</span><span class="sxs-lookup"><span data-stu-id="b014f-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="b014f-104">本文說明一些在 Azure 中調整資源規模的常見模式。</span><span class="sxs-lookup"><span data-stu-id="b014f-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="b014f-105">Azure 監視器自動調整規模僅適用於虛擬機器擴展集 (VMSS)、雲端服務、App Service 方案及 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="b014f-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="b014f-106">開始使用</span><span class="sxs-lookup"><span data-stu-id="b014f-106">Lets get started</span></span>

<span data-ttu-id="b014f-107">本文假設您已熟悉如何使用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="b014f-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="b014f-108">您可以[從這裡開始調整資源規模][1]。</span><span class="sxs-lookup"><span data-stu-id="b014f-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="b014f-109">下列是一些常見的調整規模模式。</span><span class="sxs-lookup"><span data-stu-id="b014f-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="b014f-110">根據 CPU 調整規模</span><span class="sxs-lookup"><span data-stu-id="b014f-110">Scale based on CPU</span></span>

<span data-ttu-id="b014f-111">您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且</span><span class="sxs-lookup"><span data-stu-id="b014f-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="b014f-112">您想要根據 CPU 進行相應放大/縮小。</span><span class="sxs-lookup"><span data-stu-id="b014f-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="b014f-113">此外，您想要確定執行個體數目會有下限。</span><span class="sxs-lookup"><span data-stu-id="b014f-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="b014f-114">另外還想要確定，您會將上限設定為您可調整到的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="b014f-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![根據 CPU 調整規模][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="b014f-116">在工作日與週末以不同方式調整規模</span><span class="sxs-lookup"><span data-stu-id="b014f-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="b014f-117">您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且</span><span class="sxs-lookup"><span data-stu-id="b014f-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="b014f-118">您預設想要 3 個執行個體 (在工作日)</span><span class="sxs-lookup"><span data-stu-id="b014f-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="b014f-119">您不預期週末會有流量，因此想要在週末相應減少為 1 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="b014f-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![在工作日與週末以不同方式調整規模][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="b014f-121">在假日期間以不同方式調整規模</span><span class="sxs-lookup"><span data-stu-id="b014f-121">Scale differently during holidays</span></span>

<span data-ttu-id="b014f-122">您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且</span><span class="sxs-lookup"><span data-stu-id="b014f-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="b014f-123">您預設想要根據 CPU 使用量相應增加/減少</span><span class="sxs-lookup"><span data-stu-id="b014f-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="b014f-124">不過，在假日期間 (或對貴企業很重要的特定天數)，您會想要覆寫預設值，以便有更多可供使用的容量。</span><span class="sxs-lookup"><span data-stu-id="b014f-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![在假日期間以不同方式調整規模][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="b014f-126">根據自訂計量調整規模</span><span class="sxs-lookup"><span data-stu-id="b014f-126">Scale based on custom metric</span></span>

<span data-ttu-id="b014f-127">您具有一個 Web 前端以及可與後端通訊的 API 層。</span><span class="sxs-lookup"><span data-stu-id="b014f-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="b014f-128">您想要根據前端的自訂事件來調整 API 層的規模 (例如：您想要根據購物車中的項目數來調整結帳程序)</span><span class="sxs-lookup"><span data-stu-id="b014f-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![根據自訂計量調整規模][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png