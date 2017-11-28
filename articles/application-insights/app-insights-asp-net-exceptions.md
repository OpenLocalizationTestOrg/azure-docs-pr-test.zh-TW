---
title: "aaaDiagnose 失敗和例外狀況中的 web 應用程式與 Azure Application Insights |Microsoft 文件"
description: "擷取從 ASP.NET 應用程式與所要求遙測的例外狀況。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="4a15a-103">使用 Application Insights 在 Web 應用程式中診斷例外狀況</span><span class="sxs-lookup"><span data-stu-id="4a15a-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="4a15a-104">[Application Insights](app-insights-overview.md) 會回報您即時 Web 應用程式中的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="4a15a-105">您可以與交互關聯失敗的要求例外狀況和其他事件在 hello 用戶端和伺服器，如此您就可以快速地診斷出 hello 原因。</span><span class="sxs-lookup"><span data-stu-id="4a15a-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="4a15a-106">設定例外狀況報告</span><span class="sxs-lookup"><span data-stu-id="4a15a-106">Set up exception reporting</span></span>
* <span data-ttu-id="4a15a-107">從您的伺服器應用程式報告 toohave 例外狀況：</span><span class="sxs-lookup"><span data-stu-id="4a15a-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="4a15a-108">在應用程式程式碼中安裝 [Application Insights SDK](app-insights-asp-net.md)，或</span><span class="sxs-lookup"><span data-stu-id="4a15a-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="4a15a-109">IIS Web 伺服器：執行 [Application Insights 代理程式](app-insights-monitor-performance-live-website-now.md)；或</span><span class="sxs-lookup"><span data-stu-id="4a15a-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="4a15a-110">Azure web 應用程式： 新增 hello [Application Insights 擴充功能](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="4a15a-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="4a15a-111">Java web 應用程式： 安裝 hello [Java 代理程式](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="4a15a-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="4a15a-112">安裝 hello [JavaScript 程式碼片段](app-insights-javascript.md)網頁 toocatch 瀏覽器例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="4a15a-113">在某些應用程式架構，或使用某些設定，您需要 tootake 某些額外的步驟 toocatch 詳細例外狀況：</span><span class="sxs-lookup"><span data-stu-id="4a15a-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="4a15a-114">Web Form</span><span class="sxs-lookup"><span data-stu-id="4a15a-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="4a15a-115">MVC</span><span class="sxs-lookup"><span data-stu-id="4a15a-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="4a15a-116">Web API 1.*</span><span class="sxs-lookup"><span data-stu-id="4a15a-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="4a15a-117">Web API 2.*</span><span class="sxs-lookup"><span data-stu-id="4a15a-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="4a15a-118">WCF</span><span class="sxs-lookup"><span data-stu-id="4a15a-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="4a15a-119">使用 Visual Studio 診斷例外狀況</span><span class="sxs-lookup"><span data-stu-id="4a15a-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="4a15a-120">在 Visual Studio 偵錯的 toohelp 開啟 hello 應用程式方案。</span><span class="sxs-lookup"><span data-stu-id="4a15a-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="4a15a-121">執行 hello 應用程式，您的伺服器上或使用 F5 在開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="4a15a-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="4a15a-122">在 Visual Studio 中，開啟 hello Application Insights 搜尋視窗，並將它從您的應用程式設定 toodisplay 事件。</span><span class="sxs-lookup"><span data-stu-id="4a15a-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="4a15a-123">您正在偵錯時，您可以只要按一下 hello Application Insights 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a15a-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 開啟。](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="4a15a-125">請注意，您可以篩選 hello 報表 tooshow 只是例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="4a15a-126">*未顯示例外狀況？請參閱[擷取例外狀況](#exceptions)。*</span><span class="sxs-lookup"><span data-stu-id="4a15a-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="4a15a-127">按一下 [例外狀況報告 tooshow] 其堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="4a15a-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="4a15a-128">按一下 hello 堆疊追蹤，tooopen hello 相關的程式碼檔案中的行參考。</span><span class="sxs-lookup"><span data-stu-id="4a15a-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="4a15a-129">在 hello 程式碼，請注意，CodeLens 會顯示 hello 例外狀況的相關資料：</span><span class="sxs-lookup"><span data-stu-id="4a15a-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![CodeLens 的例外狀況通知。](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="4a15a-131">使用 hello Azure 入口網站的診斷失敗</span><span class="sxs-lookup"><span data-stu-id="4a15a-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="4a15a-132">從您的應用程式的 hello Application Insights 概觀，hello 失敗磚會顯示例外狀況和失敗的 HTTP 要求的圖表以及 hello 的清單要求會導致 hello 最常失敗的 Url。</span><span class="sxs-lookup"><span data-stu-id="4a15a-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![選取 [設定]、[失敗]](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="4a15a-134">按一下透過其中一個 hello 失敗 hello 清單 tooget tooindividual 相符項目中的 hello 例外狀況，您可以在此查看 hello 詳細資料，堆疊追蹤的例外狀況類型：</span><span class="sxs-lookup"><span data-stu-id="4a15a-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![選取的執行個體失敗的要求，並在 例外狀況詳細資料，取得 tooinstances hello 例外狀況。](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="4a15a-136">**或者，**您可以開始從要求的 hello 清單，然後找出例外狀況相關的 tooit。</span><span class="sxs-lookup"><span data-stu-id="4a15a-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="4a15a-137">*未顯示例外狀況？請參閱[擷取例外狀況](#exceptions)。*</span><span class="sxs-lookup"><span data-stu-id="4a15a-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="4a15a-138">自訂追蹤和記錄資料</span><span class="sxs-lookup"><span data-stu-id="4a15a-138">Custom tracing and log data</span></span>
<span data-ttu-id="4a15a-139">tooget 診斷資料特定 tooyour 應用程式中，您可以插入程式碼 toosend 遙測資料。</span><span class="sxs-lookup"><span data-stu-id="4a15a-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="4a15a-140">這顯示在診斷搜尋、 hello 要求、 頁面檢視，以及其他自動收集資料。</span><span class="sxs-lookup"><span data-stu-id="4a15a-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="4a15a-141">您有幾種選項：</span><span class="sxs-lookup"><span data-stu-id="4a15a-141">You have several options:</span></span>

* <span data-ttu-id="4a15a-142">[Trackevent （)](app-insights-api-custom-events-metrics.md#trackevent)通常用來監視使用狀況模式，但它也會傳送的資料出現在自訂事件診斷搜尋 hello。</span><span class="sxs-lookup"><span data-stu-id="4a15a-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="4a15a-143">事件具有名稱，並且可以包含字串屬性和數值度量，您可以對其[篩選診斷搜尋](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="4a15a-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="4a15a-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 可讓您傳送較長的資料，例如 POST 資訊。</span><span class="sxs-lookup"><span data-stu-id="4a15a-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="4a15a-145">[TrackException()](#exceptions) 會傳送堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="4a15a-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="4a15a-146">[深入了解例外狀況](#exceptions)。</span><span class="sxs-lookup"><span data-stu-id="4a15a-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="4a15a-147">如果您已經使用 Log4Net 或 NLog 等記錄架構，您可以[擷取這些記錄](app-insights-asp-net-trace-logs.md)，然後在診斷搜尋中將它們連同要求和例外狀況資料一起檢視。</span><span class="sxs-lookup"><span data-stu-id="4a15a-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="4a15a-148">這些事件中，開啟 toosee[搜尋](app-insights-diagnostic-search.md)、 開啟篩選器，，，然後選擇 自訂事件、 追蹤或例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![鑽研](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="4a15a-150">如果您的應用程式會產生大量的遙測，hello 調整取樣模組將會自動減少 hello 磁碟區所傳送的 toohello 入口網站傳送代表性數部分的事件。</span><span class="sxs-lookup"><span data-stu-id="4a15a-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="4a15a-151">屬於的 hello 相同的作業將會被選取或取消選取此選項為群組，如此您可以瀏覽之間相關事件的事件。</span><span class="sxs-lookup"><span data-stu-id="4a15a-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="4a15a-152">了解取樣。</span><span class="sxs-lookup"><span data-stu-id="4a15a-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="4a15a-153">Toosee 要求張貼資料的方式</span><span class="sxs-lookup"><span data-stu-id="4a15a-153">How toosee request POST data</span></span>
<span data-ttu-id="4a15a-154">要求詳細資料不包含 hello 資料傳送 POST 呼叫 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a15a-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="4a15a-155">toohave 回報這項資料：</span><span class="sxs-lookup"><span data-stu-id="4a15a-155">toohave this data reported:</span></span>

* <span data-ttu-id="4a15a-156">[安裝 hello SDK](app-insights-asp-net.md)應用程式專案中。</span><span class="sxs-lookup"><span data-stu-id="4a15a-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="4a15a-157">將程式碼插入您的應用程式 toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace)。</span><span class="sxs-lookup"><span data-stu-id="4a15a-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="4a15a-158">傳送 hello 訊息參數中的 hello 張貼資料。</span><span class="sxs-lookup"><span data-stu-id="4a15a-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="4a15a-159">沒有允許 toohello 大小限制，因此您應該嘗試 toosend 只 hello 重要資料。</span><span class="sxs-lookup"><span data-stu-id="4a15a-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="4a15a-160">當您調查失敗的要求時，以尋找相關聯的 hello 追蹤。</span><span class="sxs-lookup"><span data-stu-id="4a15a-160">When you investigate a failed request, find hello associated traces.</span></span>  

![鑽研](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="4a15a-162"><a name="exceptions"></a> 擷取例外狀況和相關的診斷資料</span><span class="sxs-lookup"><span data-stu-id="4a15a-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="4a15a-163">首先，您將不會 hello 入口網站中看到您的應用程式會造成失敗的所有 hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="4a15a-164">您會看到瀏覽器中的任何例外狀況 (如果您使用 hello [JavaScript SDK](app-insights-javascript.md) web 網頁中)。</span><span class="sxs-lookup"><span data-stu-id="4a15a-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="4a15a-165">但大部分的伺服器例外狀況所捕捉 IIS，您有 toowrite 的位元的程式碼 toosee 它們。</span><span class="sxs-lookup"><span data-stu-id="4a15a-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="4a15a-166">您可以：</span><span class="sxs-lookup"><span data-stu-id="4a15a-166">You can:</span></span>

* <span data-ttu-id="4a15a-167">**明確地記錄例外狀況**插入程式碼中的例外狀況處理常式 tooreport hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="4a15a-168">**自動擷取例外狀況** ，方法是設定您的 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="4a15a-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="4a15a-169">hello 必要新增項目都會有不同不同類型的架構。</span><span class="sxs-lookup"><span data-stu-id="4a15a-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="4a15a-170">明確報告例外狀況</span><span class="sxs-lookup"><span data-stu-id="4a15a-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="4a15a-171">hello 最簡單的方式是在例外狀況處理常式中呼叫 tooTrackException() tooinsert。</span><span class="sxs-lookup"><span data-stu-id="4a15a-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="4a15a-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="4a15a-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="4a15a-173">C#</span><span class="sxs-lookup"><span data-stu-id="4a15a-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="4a15a-174">VB</span><span class="sxs-lookup"><span data-stu-id="4a15a-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="4a15a-175">hello 屬性和量值的參數是選擇性的但可用於[篩選和加入](app-insights-diagnostic-search.md)額外的資訊。</span><span class="sxs-lookup"><span data-stu-id="4a15a-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="4a15a-176">比方說，如果您有可以執行數個遊戲的應用程式，您無法找到所有 hello 例外狀況報告相關的 tooa 特定遊戲。</span><span class="sxs-lookup"><span data-stu-id="4a15a-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="4a15a-177">您可以像 tooeach 字典，做為您加入數目的項目。</span><span class="sxs-lookup"><span data-stu-id="4a15a-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="4a15a-178">瀏覽器例外狀況</span><span class="sxs-lookup"><span data-stu-id="4a15a-178">Browser exceptions</span></span>
<span data-ttu-id="4a15a-179">大部分的瀏覽器例外狀況都會報告。</span><span class="sxs-lookup"><span data-stu-id="4a15a-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="4a15a-180">如果您的網頁包含指令碼檔案的內容傳遞網路或其他網域，請確定指令碼標記具有 hello 屬性```crossorigin="anonymous"```，並將該 hello 伺服器傳送[CORS 標頭](http://enable-cors.org/)。</span><span class="sxs-lookup"><span data-stu-id="4a15a-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="4a15a-181">這可讓您 tooget 堆疊追蹤和從這些資源的未處理 JavaScript 例外狀況的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4a15a-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="4a15a-182">Web Form</span><span class="sxs-lookup"><span data-stu-id="4a15a-182">Web forms</span></span>
<span data-ttu-id="4a15a-183">Web form 設有 CustomErrors 沒有重新導向時 hello HTTP 模組時，將會無法 toocollect hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="4a15a-184">但是如果您有使用中的重新導向，加入下列行 toohello Application_Error 函式中 Global.asax.cs hello。</span><span class="sxs-lookup"><span data-stu-id="4a15a-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="4a15a-185">(如果您還沒有檔案，請加入 Global.asax 檔案。)</span><span class="sxs-lookup"><span data-stu-id="4a15a-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="4a15a-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="4a15a-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="4a15a-187">MVC</span><span class="sxs-lookup"><span data-stu-id="4a15a-187">MVC</span></span>
<span data-ttu-id="4a15a-188">如果 hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx)設定`Off`，則例外狀況將可供 hello [HTTP 模組](https://msdn.microsoft.com/library/ms178468.aspx)toocollect。</span><span class="sxs-lookup"><span data-stu-id="4a15a-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="4a15a-189">不過，如果它是`RemoteOnly`（預設值） 或`On`，然後將清除 hello 例外狀況並不適用於 Application Insights tooautomatically 收集。</span><span class="sxs-lookup"><span data-stu-id="4a15a-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="4a15a-190">您可以藉由覆寫 hello 修正[System.Web.Mvc.HandleErrorAttribute 類別](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)，並套用覆寫的 hello 類別，如所示為 hello 不同 MVC 以下的版本 ([github 來源](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="4a15a-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="4a15a-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="4a15a-191">MVC 2</span></span>
<span data-ttu-id="4a15a-192">Hello HandleError 屬性取代為您新的屬性，在您的控制站。</span><span class="sxs-lookup"><span data-stu-id="4a15a-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="4a15a-193">範例</span><span class="sxs-lookup"><span data-stu-id="4a15a-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="4a15a-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="4a15a-194">MVC 3</span></span>
<span data-ttu-id="4a15a-195">註冊 `AiHandleErrorAttribute` 做為 Global.asax.cs 中的全域篩選器：</span><span class="sxs-lookup"><span data-stu-id="4a15a-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="4a15a-196">範例</span><span class="sxs-lookup"><span data-stu-id="4a15a-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="4a15a-197">MVC 4、MVC5</span><span class="sxs-lookup"><span data-stu-id="4a15a-197">MVC 4, MVC5</span></span>
<span data-ttu-id="4a15a-198">註冊 AiHandleErrorAttribute 做為 FilterConfig.cs 中的全域篩選器：</span><span class="sxs-lookup"><span data-stu-id="4a15a-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="4a15a-199">範例</span><span class="sxs-lookup"><span data-stu-id="4a15a-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="4a15a-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="4a15a-200">Web API 1.x</span></span>
<span data-ttu-id="4a15a-201">覆寫 System.Web.Http.Filters.ExceptionFilterAttribute：</span><span class="sxs-lookup"><span data-stu-id="4a15a-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="4a15a-202">您無法加入此覆寫的屬性 toospecific 控制站，或將它 toohello 全域篩選器設定 hello 到 WebApiConfig 類別中：</span><span class="sxs-lookup"><span data-stu-id="4a15a-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="4a15a-203">範例</span><span class="sxs-lookup"><span data-stu-id="4a15a-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="4a15a-204">有無法處理 hello 例外狀況篩選條件的案例數目。</span><span class="sxs-lookup"><span data-stu-id="4a15a-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="4a15a-205">例如：</span><span class="sxs-lookup"><span data-stu-id="4a15a-205">For example:</span></span>

* <span data-ttu-id="4a15a-206">從控制器建構函式擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="4a15a-207">從訊息處理常式擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="4a15a-208">在路由期間擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="4a15a-209">在回應內容序列化期間擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="4a15a-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="4a15a-210">Web API 2.x</span></span>
<span data-ttu-id="4a15a-211">新增 IExceptionLogger 的實作：</span><span class="sxs-lookup"><span data-stu-id="4a15a-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="4a15a-212">視情況中新增此 toohello 服務：</span><span class="sxs-lookup"><span data-stu-id="4a15a-212">Add this toohello services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="4a15a-213">}</span><span class="sxs-lookup"><span data-stu-id="4a15a-213">}</span></span>

[<span data-ttu-id="4a15a-214">範例</span><span class="sxs-lookup"><span data-stu-id="4a15a-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="4a15a-215">做為替代方案，您可以：</span><span class="sxs-lookup"><span data-stu-id="4a15a-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="4a15a-216">取代 hello 只 ExceptionHandler 利用 IExceptionHandler 的自訂實作。</span><span class="sxs-lookup"><span data-stu-id="4a15a-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="4a15a-217">這只稱為 hello 架構時仍能 toochoose 的回應訊息 toosend （不是在 hello 連接已中止執行個體）</span><span class="sxs-lookup"><span data-stu-id="4a15a-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="4a15a-218">例外狀況篩選條件 （如中所述在上述的 Web API 1.x 控制站上的 hello > 一節）-不會在所有情況下呼叫。</span><span class="sxs-lookup"><span data-stu-id="4a15a-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="4a15a-219">WCF</span><span class="sxs-lookup"><span data-stu-id="4a15a-219">WCF</span></span>
<span data-ttu-id="4a15a-220">新增類別，該類別會擴充屬性和實作 IErrorHandler 和 IServiceBehavior。</span><span class="sxs-lookup"><span data-stu-id="4a15a-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="4a15a-221">加入 hello 屬性 toohello 服務實作：</span><span class="sxs-lookup"><span data-stu-id="4a15a-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="4a15a-222">範例</span><span class="sxs-lookup"><span data-stu-id="4a15a-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="4a15a-223">例外狀況效能計數器</span><span class="sxs-lookup"><span data-stu-id="4a15a-223">Exception performance counters</span></span>
<span data-ttu-id="4a15a-224">如果您有[安裝 Application Insights 的代理程式 hello](app-insights-monitor-performance-live-website-now.md)您在伺服器上，您可以取得 hello 例外狀況率，.NET 所測量的圖表。</span><span class="sxs-lookup"><span data-stu-id="4a15a-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="4a15a-225">這包括已處理和未處理的 .NET 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="4a15a-226">開啟 [計量瀏覽器] 刀鋒視窗、加入新圖表，然後選取 [效能計數器] 下方所列的 [例外狀況比率] 。</span><span class="sxs-lookup"><span data-stu-id="4a15a-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="4a15a-227">hello.NET framework 來計算 hello 速率的間隔中計算的例外狀況的 hello 數，然後除以 hello hello 間隔長度。</span><span class="sxs-lookup"><span data-stu-id="4a15a-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="4a15a-228">請注意，它將會不同於 hello '例外狀況' hello Application Insights 入口網站的計算方式是計算 TrackException 報告的計數。</span><span class="sxs-lookup"><span data-stu-id="4a15a-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="4a15a-229">hello 取樣間隔不同，而且 hello SDK 不會將傳送 TrackException 報告所有處理和未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4a15a-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="4a15a-230">影片</span><span class="sxs-lookup"><span data-stu-id="4a15a-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="4a15a-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a15a-231">Next steps</span></span>
* [<span data-ttu-id="4a15a-232">監視 REST、 SQL 及其他呼叫 toodependencies</span><span class="sxs-lookup"><span data-stu-id="4a15a-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="4a15a-233">監視頁面載入時間、瀏覽器例外狀況及 AJAX 呼叫</span><span class="sxs-lookup"><span data-stu-id="4a15a-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="4a15a-234">監視效能計數器</span><span class="sxs-lookup"><span data-stu-id="4a15a-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
