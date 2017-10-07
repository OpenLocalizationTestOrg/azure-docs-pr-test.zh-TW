---
title: "aaaSmart Detection in Azure Application Insights |Microsoft 文件"
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
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="442c0-103">Application Insights 中的智慧型偵測</span><span class="sxs-lookup"><span data-stu-id="442c0-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="442c0-104">「智慧型偵測」會自動警告您 Web 應用程式中的可能效能問題。</span><span class="sxs-lookup"><span data-stu-id="442c0-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="442c0-105">它會執行的應用程式傳送太 hello 遙測的主動式分析[Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="442c0-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="442c0-106">如果失敗率急遽上升或是用戶端或伺服器效能出現異常模式，您就會收到警示。</span><span class="sxs-lookup"><span data-stu-id="442c0-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="442c0-107">這項功能不需要進行任何設定。</span><span class="sxs-lookup"><span data-stu-id="442c0-107">This feature needs no configuration.</span></span> <span data-ttu-id="442c0-108">只要您的應用程式傳送的遙測足夠，它就能發揮作用。</span><span class="sxs-lookup"><span data-stu-id="442c0-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="442c0-109">您可以在 hello 電子郵件收到，和從 hello 智慧偵測刀鋒視窗存取智慧偵測警示。</span><span class="sxs-lookup"><span data-stu-id="442c0-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="442c0-110">檢閱智慧型偵測</span><span class="sxs-lookup"><span data-stu-id="442c0-110">Review your Smart Detections</span></span>
<span data-ttu-id="442c0-111">您可以透過兩種方式探索偵測︰</span><span class="sxs-lookup"><span data-stu-id="442c0-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="442c0-112">**接收來自 Application Insights 的電子郵件** 。</span><span class="sxs-lookup"><span data-stu-id="442c0-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="442c0-113">以下是典型範例︰</span><span class="sxs-lookup"><span data-stu-id="442c0-113">Here's a typical example:</span></span>
  
    ![電子郵件警示](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="442c0-115">按一下 hello 大按鈕 tooopen hello 入口網站中的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="442c0-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="442c0-116">**hello 智慧偵測磚**在您的應用程式概觀刀鋒視窗會顯示最近的警示計數。</span><span class="sxs-lookup"><span data-stu-id="442c0-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="442c0-117">按一下 hello 磚 toosee 一份最近的警示。</span><span class="sxs-lookup"><span data-stu-id="442c0-117">Click hello tile toosee a list of recent alerts.</span></span>

![檢視最近的偵測](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="442c0-119">選取警示的 toosee 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="442c0-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="442c0-120">可偵測到哪些問題？</span><span class="sxs-lookup"><span data-stu-id="442c0-120">What problems are detected?</span></span>
<span data-ttu-id="442c0-121">共有三種偵測︰</span><span class="sxs-lookup"><span data-stu-id="442c0-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="442c0-122">[智慧型偵測 - 失敗異常](app-insights-proactive-failure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="442c0-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="442c0-123">我們使用機器學習服務失敗的要求，您的應用程式中，然後再建立相互關聯使用負載和其他因素 tooset hello 預期率。</span><span class="sxs-lookup"><span data-stu-id="442c0-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="442c0-124">如果 hello 失敗率 hello 預期信封外，我們會傳送警示。</span><span class="sxs-lookup"><span data-stu-id="442c0-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="442c0-125">[智慧型偵測 - 效能異常](app-insights-proactive-performance-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="442c0-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="442c0-126">如果作業或相依性的持續時間的回應時間變慢 toohistorical 比較的基準或我們識別異常的模式中回應時間或頁面載入時間，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="442c0-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="442c0-127">[智慧型偵測 - Azure 雲端服務問題](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="442c0-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="442c0-128">如果您的應用程式裝載於 Azure 雲端服務，而且角色執行個體有啟動失敗、經常回收或執行階段損毀等現象，您便會收到警示。</span><span class="sxs-lookup"><span data-stu-id="442c0-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="442c0-129">（每個通知中的 hello 說明連結需要您 toohello 相關文章）。</span><span class="sxs-lookup"><span data-stu-id="442c0-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="442c0-130">影片</span><span class="sxs-lookup"><span data-stu-id="442c0-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="442c0-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="442c0-131">Next steps</span></span>
<span data-ttu-id="442c0-132">這些診斷工具可協助您檢查您的應用程式的遙測 hello:</span><span class="sxs-lookup"><span data-stu-id="442c0-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="442c0-133">計量瀏覽器</span><span class="sxs-lookup"><span data-stu-id="442c0-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="442c0-134">搜尋總管</span><span class="sxs-lookup"><span data-stu-id="442c0-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="442c0-135">分析 - 功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="442c0-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="442c0-136">「智慧型偵測」是全自動的。</span><span class="sxs-lookup"><span data-stu-id="442c0-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="442c0-137">但您可能要 tooset 某些更多的警示嗎？</span><span class="sxs-lookup"><span data-stu-id="442c0-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="442c0-138">手動設定的度量警示</span><span class="sxs-lookup"><span data-stu-id="442c0-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="442c0-139">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="442c0-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

