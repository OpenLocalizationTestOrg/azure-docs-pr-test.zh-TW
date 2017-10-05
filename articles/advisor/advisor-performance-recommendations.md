---
title: "Azure 建議程式效能建議 | Microsoft Docs"
description: "使用 Advisor 將 Azure 部署的效能最佳化。"
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
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="5829d-103">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="5829d-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="5829d-104">Advisor 效能建議有助於提升業務關鍵應用程式的速度和回應能力。</span><span class="sxs-lookup"><span data-stu-id="5829d-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="5829d-105">您可以在 Advisor 儀表板的 [效能] 索引標籤上，取得 Advisor 的效能建議。</span><span class="sxs-lookup"><span data-stu-id="5829d-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![建議程式效能索引標籤](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="5829d-107">使用 SQL DB Advisor 來改善資料庫效能</span><span class="sxs-lookup"><span data-stu-id="5829d-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="5829d-108">建議程式可針對所有的 Azure 資源提供一致的合併建議檢視。</span><span class="sxs-lookup"><span data-stu-id="5829d-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="5829d-109">它會與 SQL Database 建議程式整合，以提供改善 SQL Azure 資料庫效能的相關建議。</span><span class="sxs-lookup"><span data-stu-id="5829d-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="5829d-110">SQL Database 建議程式會藉由分析您的使用歷程記錄來評估 SQL Azure 資料庫的效能。</span><span class="sxs-lookup"><span data-stu-id="5829d-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="5829d-111">接著會提供最適合用於執行資料庫之一般工作負載的建議事項。</span><span class="sxs-lookup"><span data-stu-id="5829d-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="5829d-112">若要取得建議，資料庫必須持續使用一週，而且那一週之內必須有一些一致的活動。</span><span class="sxs-lookup"><span data-stu-id="5829d-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="5829d-113">相較於隨機蹦出的活動，一致的查詢模式更有利於 SQL Database Advisor 最佳化。</span><span class="sxs-lookup"><span data-stu-id="5829d-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="5829d-114">如需 SQL Database Advisor 的詳細資訊，請參閱 [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/)。</span><span class="sxs-lookup"><span data-stu-id="5829d-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![SQL Database 建議](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="5829d-116">改善 Redis 快取的效能和可靠性</span><span class="sxs-lookup"><span data-stu-id="5829d-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="5829d-117">Advisor 會識別高記憶體使用量、伺服器負載、網路頻寬或大量用戶端連線會對其效能造成負面影響的 Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="5829d-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="5829d-118">Advisor 也提供最佳做法建議來協助您避免潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="5829d-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="5829d-119">如需 Redis 快取建議的詳細資訊，請參閱 [Redis 快取建議程式](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor)。</span><span class="sxs-lookup"><span data-stu-id="5829d-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="5829d-120">改善 App Service 的效能和可靠性</span><span class="sxs-lookup"><span data-stu-id="5829d-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="5829d-121">Azure 建議程式整合了最佳作法建議，以供提升應用程式服務體驗和探索相關的平台功能。</span><span class="sxs-lookup"><span data-stu-id="5829d-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="5829d-122">應用程式服務建議的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="5829d-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="5829d-123">偵測應用程式執行階段與緩和選項已耗盡記憶體或 CPU 資源的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5829d-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="5829d-124">偵測共置資源 (如 Web 應用程式和資料庫) 可改善效能並降低成本的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5829d-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="5829d-125">如需應用程式服務建議的詳細資訊，請參閱 [Azure App Service 的最佳作法](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/)。</span><span class="sxs-lookup"><span data-stu-id="5829d-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="5829d-126">![應用程式服務建議](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="5829d-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="5829d-127">如何在建議程式中存取效能建議</span><span class="sxs-lookup"><span data-stu-id="5829d-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="5829d-128">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5829d-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5829d-129">在左側窗格中，按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="5829d-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="5829d-130">在服務功能表窗格中，於 [監視和管理] 底下，按一下 [Azure Advisor]。</span><span class="sxs-lookup"><span data-stu-id="5829d-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="5829d-131">隨即會顯示 Advisor 儀表板。</span><span class="sxs-lookup"><span data-stu-id="5829d-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="5829d-132">在 Advisor 儀表板上，按一下 [效能] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5829d-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="5829d-133">選取您想要接收建議的訂用帳戶，然後按一下 [取得建議]。</span><span class="sxs-lookup"><span data-stu-id="5829d-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="5829d-134">若要存取 Advisor 建議，您必須先向 Advisor「註冊您的訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="5829d-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="5829d-135">當「訂用帳戶擁有者」啟動 Advisor 儀表板，然後按一下 [取得建議] 按鈕時，便會註冊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5829d-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="5829d-136">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="5829d-136">This is a *one-time operation*.</span></span> <span data-ttu-id="5829d-137">註冊訂用帳戶之後，您能以訂用帳戶、資源群組或特定資源的 [擁有者]、[參與者] 或 [讀取者] 身分存取 Advisor 建議。</span><span class="sxs-lookup"><span data-stu-id="5829d-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5829d-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5829d-138">Next steps</span></span>

<span data-ttu-id="5829d-139">若要深入了解 Advisor 建議，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5829d-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="5829d-140">建議程式簡介</span><span class="sxs-lookup"><span data-stu-id="5829d-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="5829d-141">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="5829d-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="5829d-142">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="5829d-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="5829d-143">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="5829d-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="5829d-144">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="5829d-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

