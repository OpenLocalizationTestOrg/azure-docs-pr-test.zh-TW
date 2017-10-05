---
title: "ASP.NET Core 的 Azure Application Insights | Microsoft Docs"
description: "監視 Web 應用程式的可用性、效能和使用方式。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d86495eea467977f6c079de72e2b49a2a1da2b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="343e3-103">ASP.NET Core 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="343e3-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="343e3-104">[Application Insights](app-insights-overview.md) 可讓您監視 Web 應用程式的可用性、效能和使用情況。</span><span class="sxs-lookup"><span data-stu-id="343e3-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="343e3-105">當您取得有關應用程式在現實世界的效能和效率的意見反應時，您可以在每個開發生命週期中針對設計方向做出明智的抉擇。</span><span class="sxs-lookup"><span data-stu-id="343e3-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![範例](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="343e3-107">您需要 [Microsoft Azure](http://azure.com)的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="343e3-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="343e3-108">使用 Microsoft 帳戶登入，可能是針對 Windows、XBox Live 或其他 Microsoft 雲端服務具備的帳戶。</span><span class="sxs-lookup"><span data-stu-id="343e3-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="343e3-109">您的小組可能已有 Azuare 組織訂用帳戶：請洽詢擁有者將您的 Microsoft 帳戶新增至其中。</span><span class="sxs-lookup"><span data-stu-id="343e3-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="343e3-110">開始使用</span><span class="sxs-lookup"><span data-stu-id="343e3-110">Getting started</span></span>

* <span data-ttu-id="343e3-111">在 Visual Studio [方案總管] 中以滑鼠右鍵按一下專案，然後選取 [設定 Application Insights]，或 [新增] > [Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="343e3-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="343e3-112">[深入了解](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="343e3-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="343e3-113">如果您沒有看到這些功能表命令，請遵循[手動設定入門指南 (英文)](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started)。</span><span class="sxs-lookup"><span data-stu-id="343e3-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="343e3-114">如果您的專案是使用 2017 年以前的 Visual Studio 版本建立，您可能需要執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="343e3-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="343e3-115">使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="343e3-115">Using Application Insights</span></span>
<span data-ttu-id="343e3-116">登入 [Microsoft Azure 入口網站](https://portal.azure.com)，選取 [所有資源] 或 [Application Insights]，然後選取您建立的資源以監視應用程式。</span><span class="sxs-lookup"><span data-stu-id="343e3-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="343e3-117">在另一個瀏覽器視窗中，使用您的應用程式一段時間。</span><span class="sxs-lookup"><span data-stu-id="343e3-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="343e3-118">您會看到資料出現在 Application Insights 圖表。</span><span class="sxs-lookup"><span data-stu-id="343e3-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="343e3-119">(您可能需要按一下 [重新整理])。在您的開發過程只會有少量的資料，但是當您發行應用程式並有許多使用者時，這些圖表就會真正活躍起來。</span><span class="sxs-lookup"><span data-stu-id="343e3-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="343e3-120">[概觀] 頁面會顯示關鍵效能圖表：伺服器回應時間、頁面載入時間和失敗的要求計數。</span><span class="sxs-lookup"><span data-stu-id="343e3-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="343e3-121">按一下任一圖表以查看更多的圖表和資料。</span><span class="sxs-lookup"><span data-stu-id="343e3-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="343e3-122">入口網站中的檢視分成三個主要類別：</span><span class="sxs-lookup"><span data-stu-id="343e3-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="343e3-123">[計量瀏覽器](app-insights-metrics-explorer.md)顯示計量和計數 (如回應時間、失敗率或您使用 [API](app-insights-api-custom-events-metrics.md) 自行建立的計量) 的圖形與表格。</span><span class="sxs-lookup"><span data-stu-id="343e3-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="343e3-124">依屬性值篩選和分割資料，以進一步了解您的應用程式和其使用者。</span><span class="sxs-lookup"><span data-stu-id="343e3-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="343e3-125">[搜尋總管](app-insights-diagnostic-search.md)列出個別事件，例如特定要求、例外狀況、記錄檔追蹤或您使用 [API](app-insights-api-custom-events-metrics.md) 自行建立的事件。</span><span class="sxs-lookup"><span data-stu-id="343e3-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="343e3-126">在事件中篩選和搜尋，並瀏覽相關事件以調查問題。</span><span class="sxs-lookup"><span data-stu-id="343e3-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="343e3-127">[分析](app-insights-analytics.md) 可讓您在遙測上執行類似 SQL 的查詢，而且這是一個功能強大的分析與診斷工具。</span><span class="sxs-lookup"><span data-stu-id="343e3-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="343e3-128">Alerts</span><span class="sxs-lookup"><span data-stu-id="343e3-128">Alerts</span></span>
* <span data-ttu-id="343e3-129">自動取得[主動診斷警示](app-insights-proactive-diagnostics.md)，告訴您相關的失敗率和其他度量異常的變更。</span><span class="sxs-lookup"><span data-stu-id="343e3-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="343e3-130">設定 [可用性測試](app-insights-monitor-web-app-availability.md) ，持續從全球各地的位置 測試您的網站，並在有任何測試失敗時立即取得電子郵件。</span><span class="sxs-lookup"><span data-stu-id="343e3-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="343e3-131">設定 [計量警示](app-insights-monitor-web-app-availability.md) ，以了解計量 (如回應時間或例外狀況率) 是否超出可接受的限制。</span><span class="sxs-lookup"><span data-stu-id="343e3-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="343e3-132">影片</span><span class="sxs-lookup"><span data-stu-id="343e3-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="343e3-133">開放原始碼</span><span class="sxs-lookup"><span data-stu-id="343e3-133">Open source</span></span>
[<span data-ttu-id="343e3-134">讀取和貢獻程式碼</span><span class="sxs-lookup"><span data-stu-id="343e3-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="343e3-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="343e3-135">Next steps</span></span>
* <span data-ttu-id="343e3-136">[將遙測加入至您的網頁](app-insights-javascript.md) 以監視頁面使用情況和效能。</span><span class="sxs-lookup"><span data-stu-id="343e3-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="343e3-137">[監視相依性](app-insights-asp-net-dependencies.md) ，可查看 REST、SQL 或其他外部資源是否降低您的效能。</span><span class="sxs-lookup"><span data-stu-id="343e3-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="343e3-138">[使用 API](app-insights-api-custom-events-metrics.md) 可傳送您自己的事件和計量，以取得您的應用程式效能和使用方式的更詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="343e3-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="343e3-139">[可用性測試](app-insights-monitor-web-app-availability.md) 可持續從世界各地檢查您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="343e3-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 

