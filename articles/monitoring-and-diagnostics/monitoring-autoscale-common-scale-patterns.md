---
title: "常見的自動調整規模模式 aaaOverview |Microsoft 文件"
description: "了解一些常見模式 tooauto hello Azure 中調整您的資源。"
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
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="3fd19-103">常見的自動調整規模模式概觀</span><span class="sxs-lookup"><span data-stu-id="3fd19-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="3fd19-104">本文將說明一些常見模式 tooscale hello 您在 Azure 中的資源。</span><span class="sxs-lookup"><span data-stu-id="3fd19-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="3fd19-105">只有 tooVirtual 機器規模集 (VMSS)、 雲端服務、 應用程式服務方案和應用程式服務環境，適用於 azure 監視的自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="3fd19-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="3fd19-106">開始使用</span><span class="sxs-lookup"><span data-stu-id="3fd19-106">Lets get started</span></span>

<span data-ttu-id="3fd19-107">本文假設您已熟悉如何使用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="3fd19-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="3fd19-108">您可以[取得您的資源已啟動這裡 tooscale][1]。</span><span class="sxs-lookup"><span data-stu-id="3fd19-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="3fd19-109">hello 以下是一些 hello 常見延展模式。</span><span class="sxs-lookup"><span data-stu-id="3fd19-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="3fd19-110">根據 CPU 調整規模</span><span class="sxs-lookup"><span data-stu-id="3fd19-110">Scale based on CPU</span></span>

<span data-ttu-id="3fd19-111">您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且</span><span class="sxs-lookup"><span data-stu-id="3fd19-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="3fd19-112">您想要 tooscale out/小數位數以根據 CPU。</span><span class="sxs-lookup"><span data-stu-id="3fd19-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="3fd19-113">此外，您還想 tooensure 沒有執行個體數目下限。</span><span class="sxs-lookup"><span data-stu-id="3fd19-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="3fd19-114">此外，您想要設定執行個體可調整成最大限制 toohello 數目的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="3fd19-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![根據 CPU 調整規模][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="3fd19-116">在工作日與週末以不同方式調整規模</span><span class="sxs-lookup"><span data-stu-id="3fd19-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="3fd19-117">您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且</span><span class="sxs-lookup"><span data-stu-id="3fd19-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="3fd19-118">您預設想要 3 個執行個體 (在工作日)</span><span class="sxs-lookup"><span data-stu-id="3fd19-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="3fd19-119">您不希望週末的流量，因此想 too1 執行個體關閉 tooscale 週末。</span><span class="sxs-lookup"><span data-stu-id="3fd19-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![在工作日與週末以不同方式調整規模][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="3fd19-121">在假日期間以不同方式調整規模</span><span class="sxs-lookup"><span data-stu-id="3fd19-121">Scale differently during holidays</span></span>

<span data-ttu-id="3fd19-122">您具有 Web 應用程式 (/VMSS/雲端服務角色)，而且</span><span class="sxs-lookup"><span data-stu-id="3fd19-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="3fd19-123">您想要 tooscale 向上/向下預設根據 CPU 使用量</span><span class="sxs-lookup"><span data-stu-id="3fd19-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="3fd19-124">不過，在假日旺季期間 （或對您的企業很重要的特定幾天） 時想 toooverride hello 預設值，然後可以利用更多容量。</span><span class="sxs-lookup"><span data-stu-id="3fd19-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![在假日期間以不同方式調整規模][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="3fd19-126">根據自訂計量調整規模</span><span class="sxs-lookup"><span data-stu-id="3fd19-126">Scale based on custom metric</span></span>

<span data-ttu-id="3fd19-127">您必須在 web 前端和應用程式開發介面層與 hello 後端通訊。</span><span class="sxs-lookup"><span data-stu-id="3fd19-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="3fd19-128">您想根據在 hello 前端的自訂事件 tooscale hello 應用程式開發介面層 (範例： 您想要的 tooscale 您簽出程序根據 hello hello 購物車中的項目數目)</span><span class="sxs-lookup"><span data-stu-id="3fd19-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![根據自訂計量調整規模][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png