---
title: "aaaAzure Advisor 效能建議 |Microsoft 文件"
description: "使用您的 Azure 部署的 Advisor toooptimize hello 效能。"
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="ef3d8-103">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="ef3d8-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="ef3d8-104">Azure Advisor 效能建議可協助改善 hello 速度和業務關鍵應用程式的回應性。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-104">Azure Advisor performance recommendations help improve hello speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="ef3d8-105">您可以從建議程式取得效能建議上 hello**效能**hello Advisor 儀表板 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-105">You can get performance recommendations from Advisor on hello **Performance** tab of hello Advisor dashboard.</span></span>

![建議程式效能索引標籤](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="ef3d8-107">使用 SQL DB Advisor 來改善資料庫效能</span><span class="sxs-lookup"><span data-stu-id="ef3d8-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="ef3d8-108">建議程式可針對所有的 Azure 資源提供一致的合併建議檢視。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="ef3d8-109">它可以整合與 SQL Database Advisor toobring 您改善您的 SQL Azure database 的 hello 效能的建議。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-109">It integrates with SQL Database Advisor toobring you recommendations for improving hello performance of your SQL Azure database.</span></span> <span data-ttu-id="ef3d8-110">SQL Database Advisor 會透過 SQL Azure 資料庫的 hello 效能分析您的使用記錄。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-110">SQL Database Advisor assesses hello performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="ef3d8-111">然後，它會提供最適合用於執行 hello 資料庫的一般工作負載的建議。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-111">It then offers recommendations that are best suited for running hello database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="ef3d8-112">tooget 建議資料庫還需要大約一週的使用方式，而且該星期內必須是某個一致的活動。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-112">tooget recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="ef3d8-113">相較於隨機蹦出的活動，一致的查詢模式更有利於 SQL Database Advisor 最佳化。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="ef3d8-114">如需 SQL Database Advisor 的詳細資訊，請參閱 [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/)。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![SQL Database 建議](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="ef3d8-116">改善 Redis 快取的效能和可靠性</span><span class="sxs-lookup"><span data-stu-id="ef3d8-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="ef3d8-117">Advisor 會識別高記憶體使用量、伺服器負載、網路頻寬或大量用戶端連線會對其效能造成負面影響的 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="ef3d8-118">Advisor 也會提供最佳做法建議 toohelp 避免潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-118">Advisor also provides best practices recommendations toohelp you avoid potential issues.</span></span> <span data-ttu-id="ef3d8-119">如需 Redis 快取建議的詳細資訊，請參閱 [Redis 快取建議程式](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor)。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="ef3d8-120">改善 App Service 的效能和可靠性</span><span class="sxs-lookup"><span data-stu-id="ef3d8-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="ef3d8-121">Azure 建議程式整合了最佳作法建議，以供提升應用程式服務體驗和探索相關的平台功能。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="ef3d8-122">應用程式服務建議的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="ef3d8-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="ef3d8-123">偵測應用程式執行階段與緩和選項已耗盡記憶體或 CPU 資源的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="ef3d8-124">偵測共置資源 (如 Web 應用程式和資料庫) 可改善效能並降低成本的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="ef3d8-125">如需應用程式服務建議的詳細資訊，請參閱 [Azure App Service 的最佳作法](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/)。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="ef3d8-126">![應用程式服務建議](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="ef3d8-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a><span data-ttu-id="ef3d8-127">如何 tooaccess Advisor 中的效能建議</span><span class="sxs-lookup"><span data-stu-id="ef3d8-127">How tooaccess Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="ef3d8-128">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ef3d8-129">在 hello 左窗格中，按一下 **更多服務**。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-129">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="ef3d8-130">在 hello 服務功能表窗格底下**監視及管理**，按一下  **Azure Advisor**。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-130">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="ef3d8-131">hello Advisor 儀表板會顯示。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-131">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="ef3d8-132">在 hello Advisor 儀表板上按一下 hello**效能** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-132">On hello Advisor dashboard, click hello **Performance** tab.</span></span>

5. <span data-ttu-id="ef3d8-133">選取 hello 訂用帳戶，您想 tooreceive 建議，然後按一下**取得建議**。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-133">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="ef3d8-134">tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-134">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="ef3d8-135">已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-135">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="ef3d8-136">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-136">This is a *one-time operation*.</span></span> <span data-ttu-id="ef3d8-137">Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。</span><span class="sxs-lookup"><span data-stu-id="ef3d8-137">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef3d8-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef3d8-138">Next steps</span></span>

<span data-ttu-id="ef3d8-139">toolearn 深入了解 Advisor 的建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ef3d8-139">toolearn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="ef3d8-140">簡介 tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="ef3d8-140">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="ef3d8-141">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="ef3d8-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="ef3d8-142">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="ef3d8-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="ef3d8-143">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="ef3d8-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="ef3d8-144">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="ef3d8-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

