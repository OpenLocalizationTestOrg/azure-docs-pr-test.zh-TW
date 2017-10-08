---
title: "使用 Visual Studio 中的 Azure Application Insights aaaDebug 應用程式 |Microsoft 文件"
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
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="46362-103">在 Visual Studio 中使用 Azure Application Insights 進行應用程式偵錯</span><span class="sxs-lookup"><span data-stu-id="46362-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="46362-104">在 Visual Studio (2015 和更新版本) 中，您可以使用 [Azure Application Insights](app-insights-overview.md) 的遙測，在偵錯時和在生產環境中分析 ASP.NET Web 應用程式的效能並診斷問題。</span><span class="sxs-lookup"><span data-stu-id="46362-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="46362-105">如果您建立使用 Visual Studio 2017 的 ASP.NET web 應用程式或更新版本中，它已經有 hello Application Insights SDK。</span><span class="sxs-lookup"><span data-stu-id="46362-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="46362-106">否則，如果您沒有這樣做，[加入 Application Insights tooyour 應用程式](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="46362-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="46362-107">toomonitor 您的應用程式時在即時的生產環境中，您通常 hello Application Insights 遙測中檢視 hello [Azure 入口網站](https://portal.azure.com)，其中您可以設定警示和適用於功能強大的監視工具。</span><span class="sxs-lookup"><span data-stu-id="46362-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="46362-108">但偵錯時，也可以搜尋和分析在 Visual Studio 中的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="46362-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="46362-109">從您的生產網站和從偵錯您的開發電腦上執行，您可以使用 Visual Studio tooanalyze 遙測。</span><span class="sxs-lookup"><span data-stu-id="46362-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="46362-110">在 hello 後者的情況下，您可以分析偵錯執行，即使您尚未設定 hello SDK toosend 遙測 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="46362-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="46362-111"><a name="run"></a> 偵錯您的專案</span><span class="sxs-lookup"><span data-stu-id="46362-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="46362-112">使用 F5，在本機偵錯模式下執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46362-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="46362-113">開啟不同頁面 toogenerate 某些遙測。</span><span class="sxs-lookup"><span data-stu-id="46362-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="46362-114">在 Visual Studio 中，您會看到已將您的專案中的 hello Application Insights 模組所記錄的 hello 事件計數。</span><span class="sxs-lookup"><span data-stu-id="46362-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![在 Visual Studio 中，hello Application Insights 按鈕會顯示在偵錯期間。](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="46362-116">按一下此按鈕 toosearch 您遙測。</span><span class="sxs-lookup"><span data-stu-id="46362-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="46362-117">Application Insights 搜尋</span><span class="sxs-lookup"><span data-stu-id="46362-117">Application Insights search</span></span>
<span data-ttu-id="46362-118">hello Application Insights 搜尋視窗會顯示已記錄事件。</span><span class="sxs-lookup"><span data-stu-id="46362-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="46362-119">(如果您登入 tooAzure，當您設定 Application Insights，您可以搜尋 hello hello Azure 入口網站中的事件相同。)</span><span class="sxs-lookup"><span data-stu-id="46362-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 搜尋](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="46362-121">您選取或取消選取篩選器之後，按一下 在 hello 文字搜尋欄位中的 hello 結尾 hello 搜尋 按鈕。</span><span class="sxs-lookup"><span data-stu-id="46362-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="46362-122">hello 任意文字搜尋適用於所有在 hello 事件中的欄位。</span><span class="sxs-lookup"><span data-stu-id="46362-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="46362-123">例如，搜尋頁面; hello URL 的一部分或 hello 用戶端縣 （市）; 例如屬性的值或特定追蹤記錄檔中的文字。</span><span class="sxs-lookup"><span data-stu-id="46362-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="46362-124">按一下 任何事件 toosee 其詳細的內容。</span><span class="sxs-lookup"><span data-stu-id="46362-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="46362-125">要求 tooyour web 應用程式中，您可以按一下 toohello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="46362-125">For requests tooyour web app, you can click through toohello code.</span></span>

![要求的詳細資料] 下按一下 [透過 toohello 程式碼](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="46362-127">您也可以開啟相關的項目 toohelp 診斷失敗的要求或例外狀況。</span><span class="sxs-lookup"><span data-stu-id="46362-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![在 要求詳細資料，向下捲動 toorelated 項目](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="46362-129">檢視例外狀況和失敗的要求</span><span class="sxs-lookup"><span data-stu-id="46362-129">View exceptions and failed requests</span></span>
<span data-ttu-id="46362-130">例外狀況報告顯示 hello [搜尋] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="46362-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="46362-131">(在某些較舊類型的 ASP.NET 應用程式，也有[設定例外狀況監視](app-insights-asp-net-exceptions.md)toosee 由 hello 架構會處理的例外狀況。)</span><span class="sxs-lookup"><span data-stu-id="46362-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="46362-132">按一下 例外狀況 tooget 堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="46362-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="46362-133">如果 hello 的 hello 應用程式的程式碼是在 Visual Studio 中開啟，您可以透過按一下從 hello 堆疊追蹤 toohello 相關 hello 程式碼行。</span><span class="sxs-lookup"><span data-stu-id="46362-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![例外狀況堆疊追蹤](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="46362-135">Hello 程式碼中檢視要求和例外狀況的摘要</span><span class="sxs-lookup"><span data-stu-id="46362-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="46362-136">在 hello Code Lens 列每個處理常式方法的上方，您會看到 hello 要求和 Application Insights 在 hello 過去 24 小時記錄的例外狀況的計數。</span><span class="sxs-lookup"><span data-stu-id="46362-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![例外狀況堆疊追蹤](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="46362-138">Code Lens 顯示僅限 Application Insights 資料是否您具有[設定您的應用程式 toosend 遙測 toohello Application Insights 入口網站](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="46362-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="46362-139">深入了解 Code Lens 中的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="46362-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="46362-140">趨勢</span><span class="sxs-lookup"><span data-stu-id="46362-140">Trends</span></span>
<span data-ttu-id="46362-141">趨勢是用來將應用程式一段時間內行為方式進行視覺化的工具。</span><span class="sxs-lookup"><span data-stu-id="46362-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="46362-142">選擇**瀏覽遙測趨勢**從 hello Application Insights 工具列按鈕或 Application Insights 搜尋視窗。</span><span class="sxs-lookup"><span data-stu-id="46362-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="46362-143">選擇其中一個五個常見的查詢 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="46362-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="46362-144">您可以根據遙測類型、時間範圍和其他屬性，分析不同的資料集。</span><span class="sxs-lookup"><span data-stu-id="46362-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="46362-145">在您的資料，toofind 異常選擇其中一個 hello [檢視類型] 下拉式清單底下的 hello 異常選項。</span><span class="sxs-lookup"><span data-stu-id="46362-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="46362-146">在 hello hello 視窗底部的 hello 篩選選項使得中的輕鬆 toohone 您遙測的特定子集。</span><span class="sxs-lookup"><span data-stu-id="46362-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![趨勢](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="46362-148">[深入了解趨勢](app-insights-visual-studio-trends.md)。</span><span class="sxs-lookup"><span data-stu-id="46362-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="46362-149">本機監視</span><span class="sxs-lookup"><span data-stu-id="46362-149">Local monitoring</span></span>
<span data-ttu-id="46362-150">（從 Visual Studio 2015 Update 2)如果您尚未設定 hello SDK toosend 遙測 toohello Application Insights 入口網站 （以便 ApplicationInsights.config 中沒有任何檢測金鑰） hello diagnostics 視窗會顯示您最新偵錯工作階段遙測資料。</span><span class="sxs-lookup"><span data-stu-id="46362-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="46362-151">如果您已發佈過應用程式先前的版本，這是比較好的做法。</span><span class="sxs-lookup"><span data-stu-id="46362-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="46362-152">您不想從您的偵錯工作階段 toobe hello 遙測混 hello 遙測 hello 與 hello 發行的應用程式從 Application Insights 入口網站。</span><span class="sxs-lookup"><span data-stu-id="46362-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="46362-153">如果您有一些很也有用[自訂遙測](app-insights-api-custom-events-metrics.md)的 toodebug 傳送遙測 toohello 入口網站之前。</span><span class="sxs-lookup"><span data-stu-id="46362-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="46362-154">*首先，我可以完整設定 Application Insights toosend 遙測 toohello 入口網站。但現在我想 toosee 只能在 Visual Studio 中的 hello 遙測。*</span><span class="sxs-lookup"><span data-stu-id="46362-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="46362-155">在 hello 搜尋視窗的設定沒有選項 toosearch 本機診斷即使您的應用程式傳送遙測 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="46362-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="46362-156">正在傳送 toohello 入口網站中，註解 hello 列 toostop 遙測`<instrumentationkey>...`從 ApplicationInsights.config。當您再次準備好 toosend 遙測 toohello 入口網站時，請取消註解。</span><span class="sxs-lookup"><span data-stu-id="46362-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="46362-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46362-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="46362-158">**[新增更多測試](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="46362-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="46362-159">監視使用狀況、可用性、相依性、例外狀況。</span><span class="sxs-lookup"><span data-stu-id="46362-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="46362-160">整合來自記錄架構的追蹤。</span><span class="sxs-lookup"><span data-stu-id="46362-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="46362-161">撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="46362-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="46362-163">**[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="46362-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="46362-164">檢視儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及匯出的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="46362-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

