---
title: "在 Visual Studio 中使用 Azure Application Insights 進行應用程式偵錯 | Microsoft Docs"
description: "偵錯期間和生產環境中的 Web 應用程式效能分析與診斷。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="3ab1c-103">在 Visual Studio 中使用 Azure Application Insights 進行應用程式偵錯</span><span class="sxs-lookup"><span data-stu-id="3ab1c-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="3ab1c-104">在 Visual Studio (2015 和更新版本) 中，您可以使用 [Azure Application Insights](app-insights-overview.md) 的遙測，在偵錯時和在生產環境中分析 ASP.NET Web 應用程式的效能並診斷問題。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="3ab1c-105">如果您使用 Visual Studio 2017 或更新版本建立 ASP.NET web 應用程式，它已經有 Application Insights SDK。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="3ab1c-106">否則，如果您尚未這麼做，[將 Application Insights 新增至您的應用程式](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="3ab1c-107">若要監視實際運作的應用程式，您通常可在 [Azure 入口網站](https://portal.azure.com)中檢視 Application Insights 遙測，您可以在其中設定警示及套用功能強大的監視工具。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="3ab1c-108">但若要進行偵錯，您也可以在 Visual Studio 中搜尋和分析遙測資料。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="3ab1c-109">您可以使用 Visual Studio 分析來自您的生產網站以及來自開發電腦上偵錯執行的遙測。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="3ab1c-110">在後者的情況下，即使您尚未設定 SDK 將遙測傳送至 Azure 入口網站，仍可以分析偵錯執行。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="3ab1c-111"><a name="run"></a> 偵錯您的專案</span><span class="sxs-lookup"><span data-stu-id="3ab1c-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="3ab1c-112">使用 F5，在本機偵錯模式下執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="3ab1c-113">開啟不同的頁面來產生一些遙測。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="3ab1c-114">在 Visual Studio 中，您可以看見 Application Insights 模組在您的專案中記錄的事件計數。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![在 Visual Studio 中，[Application Insights] 按鈕會在偵錯期間顯示。](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="3ab1c-116">按一下此按鈕以搜尋遙測。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="3ab1c-117">Application Insights 搜尋</span><span class="sxs-lookup"><span data-stu-id="3ab1c-117">Application Insights search</span></span>
<span data-ttu-id="3ab1c-118">[Application Insights 搜尋] 視窗會顯示已記錄的事件。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="3ab1c-119">(如果您在設定 Application Insights 時登入至 Azure，即可在 Azure 入口網站搜尋相同的事件。)</span><span class="sxs-lookup"><span data-stu-id="3ab1c-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![以滑鼠右鍵按一下專案，然後選擇 [Application Insights]、[搜尋]](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="3ab1c-121">選取或取消選取篩選條件之後，按一下文字搜尋欄位結尾的 [搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="3ab1c-122">任意文字搜尋適用於事件中的任何欄位。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="3ab1c-123">例如，搜尋頁面的 URL 的一部分；或者如用戶端城市的屬性值；或者追蹤記錄檔中的特定單字。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="3ab1c-124">按一下任何事件以查看其詳細屬性。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="3ab1c-125">對於 Web 應用程式的要求，您可以點閱程式碼。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-125">For requests to your web app, you can click through to the code.</span></span>

![在 [要求詳細資料] 之下，點閱程式碼。](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="3ab1c-127">您也可以開啟相關項目，協助診斷失敗的要求或例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![在 [要求詳細資料] 之下，向下捲動相關項目](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="3ab1c-129">檢視例外狀況和失敗的要求</span><span class="sxs-lookup"><span data-stu-id="3ab1c-129">View exceptions and failed requests</span></span>
<span data-ttu-id="3ab1c-130">例外狀況報告會顯示在 [搜尋] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="3ab1c-131">(在某些較舊的 ASP.NET 應用程式類型中，您必須[設定例外狀況監視](app-insights-asp-net-exceptions.md)，以查看架構所處理的例外狀況。)</span><span class="sxs-lookup"><span data-stu-id="3ab1c-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="3ab1c-132">按一下例外狀況以取得堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="3ab1c-133">如果應用程式的程式碼在 Visual Studio 中開啟，您可以從堆疊追蹤點選至程式碼的相關程式碼行。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![例外狀況堆疊追蹤](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="3ab1c-135">檢視程式碼中的要求和例外狀況摘要</span><span class="sxs-lookup"><span data-stu-id="3ab1c-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="3ab1c-136">在每個處理常式方法之上的 Code Lens 行中，您會看到過去 24 小時內由 Application Insights 記錄的要求和例外狀況計數。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![例外狀況堆疊追蹤](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="3ab1c-138">只有在您[設定應用程式以將遙測傳送至 Application Insights 入口網站](app-insights-asp-net.md)後，Code Lens 才會顯示 Application Insights 資料。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="3ab1c-139">深入了解 Code Lens 中的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3ab1c-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="3ab1c-140">趨勢</span><span class="sxs-lookup"><span data-stu-id="3ab1c-140">Trends</span></span>
<span data-ttu-id="3ab1c-141">趨勢是用來將應用程式一段時間內行為方式進行視覺化的工具。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="3ab1c-142">從 Application Insights 工具列按鈕或 [Application Insights 搜尋] 視窗選擇 [探索遙測趨勢]  。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="3ab1c-143">選擇五種常見查詢的其中一個，以便開始使用。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="3ab1c-144">您可以根據遙測類型、時間範圍和其他屬性，分析不同的資料集。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="3ab1c-145">若要尋找資料中的異常狀況，請選擇 [檢視類型] 下拉式清單底下的其中一個異常選項。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="3ab1c-146">視窗底部的篩選選項可讓您輕鬆地全神貫注於特定的遙測子集。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![趨勢](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="3ab1c-148">[深入了解趨勢](app-insights-visual-studio-trends.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="3ab1c-149">本機監視</span><span class="sxs-lookup"><span data-stu-id="3ab1c-149">Local monitoring</span></span>
<span data-ttu-id="3ab1c-150">(從 Visual Studio 2015 Update 2 開始) 如果您尚未設定 SDK 以將遙測傳送至 Application Insights 入口網站 (以便讓 ApplicationInsights.config 中沒有任何檢測金鑰)，則 [診斷] 視窗會顯示來自最新偵錯工作階段的遙測。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="3ab1c-151">如果您已發佈過應用程式先前的版本，這是比較好的做法。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="3ab1c-152">您不會想讓來自偵錯工作階段的遙測與 Application Insights 入口網站中來自已發佈之應用程式的遙測混在一起。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="3ab1c-153">如果您在將遙測傳送至入口網站之前有一些 [自訂遙測](app-insights-api-custom-events-metrics.md) 想要偵錯，它也很有用。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="3ab1c-154">首先，我完全設定 Application Insights 將遙測傳送至入口網站。但是現在我只想要查看在 Visual Studio 中的遙測。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="3ab1c-155">在 [搜尋] 視窗的 [設定] 中，即使您的應用程式將遙測傳送至入口網站，也有選項可搜尋本機診斷。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="3ab1c-156">若要停止將遙測傳送至入口網站，請將 ApplicationInsights.config 中的 `<instrumentationkey>...` 程式行註解化。當您準備再次將遙測傳送至入口網站時，請取消註解。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3ab1c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ab1c-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="3ab1c-158">**[新增更多測試](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="3ab1c-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="3ab1c-159">監視使用狀況、可用性、相依性、例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="3ab1c-160">整合來自記錄架構的追蹤。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="3ab1c-161">撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="3ab1c-163">**[使用 Application Insights 入口網站](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="3ab1c-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="3ab1c-164">檢視儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及匯出的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="3ab1c-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

