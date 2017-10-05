---
title: "Azure Application Insights 中的智慧型偵測 | Microsoft Docs"
description: "Application Insights 會自動深入分析您的 App 遙測，並且警告您有潛在的問題。"
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="7e625-103">Application Insights 中的智慧型偵測</span><span class="sxs-lookup"><span data-stu-id="7e625-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="7e625-104">「智慧型偵測」會自動警告您 Web 應用程式中的可能效能問題。</span><span class="sxs-lookup"><span data-stu-id="7e625-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="7e625-105">它會針對您應用程式傳送給 [Application Insights](app-insights-overview.md) 的遙測執行主動式分析。</span><span class="sxs-lookup"><span data-stu-id="7e625-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="7e625-106">如果失敗率急遽上升或是用戶端或伺服器效能出現異常模式，您就會收到警示。</span><span class="sxs-lookup"><span data-stu-id="7e625-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="7e625-107">這項功能不需要進行任何設定。</span><span class="sxs-lookup"><span data-stu-id="7e625-107">This feature needs no configuration.</span></span> <span data-ttu-id="7e625-108">只要您的應用程式傳送的遙測足夠，它就能發揮作用。</span><span class="sxs-lookup"><span data-stu-id="7e625-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="7e625-109">您可以從所收到的電子郵件和從 [智慧型偵測] 刀鋒視窗，存取「智慧型偵測」警示。</span><span class="sxs-lookup"><span data-stu-id="7e625-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="7e625-110">檢閱智慧型偵測</span><span class="sxs-lookup"><span data-stu-id="7e625-110">Review your Smart Detections</span></span>
<span data-ttu-id="7e625-111">您可以透過兩種方式探索偵測︰</span><span class="sxs-lookup"><span data-stu-id="7e625-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="7e625-112">**接收來自 Application Insights 的電子郵件** 。</span><span class="sxs-lookup"><span data-stu-id="7e625-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="7e625-113">以下是典型範例︰</span><span class="sxs-lookup"><span data-stu-id="7e625-113">Here's a typical example:</span></span>
  
    ![電子郵件警示](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="7e625-115">按一下大型按鈕以在入口網站中開啟更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7e625-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="7e625-116">您應用程式 [概觀] 刀鋒視窗上的 [主動式偵測] 磚會顯示最新進的警示計數。</span><span class="sxs-lookup"><span data-stu-id="7e625-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="7e625-117">按一下圖格即可查看最新警示的清單。</span><span class="sxs-lookup"><span data-stu-id="7e625-117">Click the tile to see a list of recent alerts.</span></span>

![檢視最近的偵測](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="7e625-119">選取警示來查看其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7e625-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="7e625-120">可偵測到哪些問題？</span><span class="sxs-lookup"><span data-stu-id="7e625-120">What problems are detected?</span></span>
<span data-ttu-id="7e625-121">共有三種偵測︰</span><span class="sxs-lookup"><span data-stu-id="7e625-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="7e625-122">[智慧型偵測 - 失敗異常](app-insights-proactive-failure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="7e625-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="7e625-123">我們使用機器學習服務來為應用程式設定預期的失敗要求率，其會與負載和其他因素相互關聯。</span><span class="sxs-lookup"><span data-stu-id="7e625-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="7e625-124">如果失敗率超過預期限制，我們便會傳送警示。</span><span class="sxs-lookup"><span data-stu-id="7e625-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="7e625-125">[智慧型偵測 - 效能異常](app-insights-proactive-performance-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="7e625-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="7e625-126">如果作業或相依性持續時間的回應時間變得比歷史基準慢，或如果我們在回應時間或頁面載入時間發現異常模式，您就會收到通知。</span><span class="sxs-lookup"><span data-stu-id="7e625-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="7e625-127">[智慧型偵測 - Azure 雲端服務問題](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="7e625-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="7e625-128">如果您的應用程式裝載於 Azure 雲端服務，而且角色執行個體有啟動失敗、經常回收或執行階段損毀等現象，您便會收到警示。</span><span class="sxs-lookup"><span data-stu-id="7e625-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="7e625-129">(每個通知中的說明連結會帶您前往相關文章。)</span><span class="sxs-lookup"><span data-stu-id="7e625-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="7e625-130">影片</span><span class="sxs-lookup"><span data-stu-id="7e625-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="7e625-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e625-131">Next steps</span></span>
<span data-ttu-id="7e625-132">這些診斷工具可協助您檢查來自您的應用程式的遙測︰</span><span class="sxs-lookup"><span data-stu-id="7e625-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="7e625-133">計量瀏覽器</span><span class="sxs-lookup"><span data-stu-id="7e625-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="7e625-134">搜尋總管</span><span class="sxs-lookup"><span data-stu-id="7e625-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="7e625-135">分析 - 功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="7e625-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="7e625-136">「智慧型偵測」是全自動的。</span><span class="sxs-lookup"><span data-stu-id="7e625-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="7e625-137">但是，或許您會想要再設定一些警示？</span><span class="sxs-lookup"><span data-stu-id="7e625-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="7e625-138">手動設定的度量警示</span><span class="sxs-lookup"><span data-stu-id="7e625-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="7e625-139">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="7e625-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

