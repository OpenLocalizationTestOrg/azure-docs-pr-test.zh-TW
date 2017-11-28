---
title: "Application Insights for ASP.NET Core aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="b5be9-103">ASP.NET Core 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5be9-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="b5be9-104">[Application Insights](app-insights-overview.md) 可讓您監視 Web 應用程式的可用性、效能和使用情況。</span><span class="sxs-lookup"><span data-stu-id="b5be9-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="b5be9-105">Hello 您善加 hello 效能和效率 hello 中的應用程式的相關意見反應，可以讓謹慎的選擇 hello 方向 hello 設計的每個開發週期中。</span><span class="sxs-lookup"><span data-stu-id="b5be9-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![範例](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="b5be9-107">您需要 [Microsoft Azure](http://azure.com)的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5be9-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="b5be9-108">使用 Microsoft 帳戶登入，可能是針對 Windows、XBox Live 或其他 Microsoft 雲端服務具備的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5be9-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="b5be9-109">您的小組可能會有組織的訂用帳戶 tooAzure： 詢問 hello 擁有者 tooadd 您 tooit 使用您的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5be9-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b5be9-110">開始使用</span><span class="sxs-lookup"><span data-stu-id="b5be9-110">Getting started</span></span>

* <span data-ttu-id="b5be9-111">在 Visual Studio [方案總管] 中以滑鼠右鍵按一下專案，然後選取 [設定 Application Insights]，或 [新增] > [Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="b5be9-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="b5be9-112">[深入了解](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="b5be9-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="b5be9-113">如果您沒有看到這些功能表命令，請遵循 hello[手動使用者入門指南](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started)。</span><span class="sxs-lookup"><span data-stu-id="b5be9-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="b5be9-114">您可能需要 toodo 這如果使用您的專案建立 2017年之前的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="b5be9-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="b5be9-115">使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5be9-115">Using Application Insights</span></span>
<span data-ttu-id="b5be9-116">登入 hello [Microsoft Azure 入口網站](https://portal.azure.com)，選取**所有資源**或**Application Insights**，然後選取您的應用程式建立 toomonitor hello 資源。</span><span class="sxs-lookup"><span data-stu-id="b5be9-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="b5be9-117">在另一個瀏覽器視窗中，使用您的應用程式一段時間。</span><span class="sxs-lookup"><span data-stu-id="b5be9-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="b5be9-118">您會看到顯示 hello Application Insights 圖表中的資料。</span><span class="sxs-lookup"><span data-stu-id="b5be9-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="b5be9-119">（您可能需要重新整理 tooclick）。在您的開發過程只會有少量的資料，但是當您發行應用程式並有許多使用者時，這些圖表就會真正活躍起來。</span><span class="sxs-lookup"><span data-stu-id="b5be9-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="b5be9-120">hello 概觀 頁面上顯示關鍵效能圖表： 伺服器回應時間、 頁面載入時間和失敗要求的計數。</span><span class="sxs-lookup"><span data-stu-id="b5be9-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="b5be9-121">多個圖表和資料，請按一下任何圖 toosee。</span><span class="sxs-lookup"><span data-stu-id="b5be9-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="b5be9-122">Hello 入口網站中的檢視可分成三大類：</span><span class="sxs-lookup"><span data-stu-id="b5be9-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="b5be9-123">[計量瀏覽器](app-insights-metrics-explorer.md)顯示圖表及資料表的度量和計數，例如回應時間、 失敗率或度量您自行建立以 hello [API](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="b5be9-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="b5be9-124">篩選器和區段 hello 資料屬性值 tooget 進一步了解您的應用程式和它的使用者。</span><span class="sxs-lookup"><span data-stu-id="b5be9-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="b5be9-125">[搜尋總管](app-insights-diagnostic-search.md)個別事件，例如特定要求、 例外狀況、 記錄追蹤或以 hello 自己建立的事件會列出[API](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="b5be9-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="b5be9-126">篩選和搜尋 hello 事件中，瀏覽不同的相關的事件 tooinvestigate 問題。</span><span class="sxs-lookup"><span data-stu-id="b5be9-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="b5be9-127">[分析](app-insights-analytics.md) 可讓您在遙測上執行類似 SQL 的查詢，而且這是一個功能強大的分析與診斷工具。</span><span class="sxs-lookup"><span data-stu-id="b5be9-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="b5be9-128">Alerts</span><span class="sxs-lookup"><span data-stu-id="b5be9-128">Alerts</span></span>
* <span data-ttu-id="b5be9-129">自動取得[主動診斷警示](app-insights-proactive-diagnostics.md)，告訴您相關的失敗率和其他度量異常的變更。</span><span class="sxs-lookup"><span data-stu-id="b5be9-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="b5be9-130">設定[可用性測試](app-insights-monitor-web-app-availability.md)tootest 任何測試失敗時以電子郵件傳送您的網站持續全球性、 位置和 get。</span><span class="sxs-lookup"><span data-stu-id="b5be9-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="b5be9-131">設定[度量的警示](app-insights-monitor-web-app-availability.md)tooknow 如果度量資訊，例如回應時間或例外狀況率超出可接受的限制。</span><span class="sxs-lookup"><span data-stu-id="b5be9-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="b5be9-132">影片</span><span class="sxs-lookup"><span data-stu-id="b5be9-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="b5be9-133">開放原始碼</span><span class="sxs-lookup"><span data-stu-id="b5be9-133">Open source</span></span>
[<span data-ttu-id="b5be9-134">閱讀及張貼 toohello 程式碼</span><span class="sxs-lookup"><span data-stu-id="b5be9-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="b5be9-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5be9-135">Next steps</span></span>
* <span data-ttu-id="b5be9-136">[將遙測 tooyour web 網頁](app-insights-javascript.md)toomonitor 頁面使用方式和效能。</span><span class="sxs-lookup"><span data-stu-id="b5be9-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="b5be9-137">[監視的相依性](app-insights-asp-net-dependencies.md)toosee 如果 REST、 SQL 或其他外部資源會減緩您。</span><span class="sxs-lookup"><span data-stu-id="b5be9-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="b5be9-138">[使用 hello API](app-insights-api-custom-events-metrics.md) toosend 您自己的事件和度量的應用程式的效能和使用方式的更詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="b5be9-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="b5be9-139">[可用性測試](app-insights-monitor-web-app-availability.md)檢查 hello 世界各地不斷地從應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5be9-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

