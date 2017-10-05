---
title: "使用 Azure Application Insights 來診斷 Web 應用程式中的失敗和例外狀況 | Microsoft Docs"
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
ms.openlocfilehash: 7eeacdc6677ccdebb1653e94a163ecb47090b7ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="b7cce-103">使用 Application Insights 在 Web 應用程式中診斷例外狀況</span><span class="sxs-lookup"><span data-stu-id="b7cce-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="b7cce-104">[Application Insights](app-insights-overview.md) 會回報您即時 Web 應用程式中的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b7cce-105">您可以在用戶端和伺服器端讓失敗的要求與例外狀況及其他事件相互關聯，以便快速地診斷原因。</span><span class="sxs-lookup"><span data-stu-id="b7cce-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="b7cce-106">設定例外狀況報告</span><span class="sxs-lookup"><span data-stu-id="b7cce-106">Set up exception reporting</span></span>
* <span data-ttu-id="b7cce-107">讓伺服器應用程式回報例外狀況︰</span><span class="sxs-lookup"><span data-stu-id="b7cce-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="b7cce-108">在應用程式程式碼中安裝 [Application Insights SDK](app-insights-asp-net.md)，或</span><span class="sxs-lookup"><span data-stu-id="b7cce-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="b7cce-109">IIS Web 伺服器：執行 [Application Insights 代理程式](app-insights-monitor-performance-live-website-now.md)；或</span><span class="sxs-lookup"><span data-stu-id="b7cce-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="b7cce-110">Azure Web 應用程式：新增 [Application Insights 擴充功能](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="b7cce-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="b7cce-111">Java Web 應用程式：安裝 [Java 代理程式](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="b7cce-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="b7cce-112">在您的網頁中安裝 [JavaScript 程式碼片段](app-insights-javascript.md)來攔截瀏覽器例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="b7cce-113">在某些應用程式架構中或搭配某些設定時，您必須採取一些額外的步驟，才能攔截較多的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="b7cce-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="b7cce-114">Web Form</span><span class="sxs-lookup"><span data-stu-id="b7cce-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="b7cce-115">MVC</span><span class="sxs-lookup"><span data-stu-id="b7cce-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="b7cce-116">Web API 1.*</span><span class="sxs-lookup"><span data-stu-id="b7cce-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="b7cce-117">Web API 2.*</span><span class="sxs-lookup"><span data-stu-id="b7cce-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="b7cce-118">WCF</span><span class="sxs-lookup"><span data-stu-id="b7cce-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="b7cce-119">使用 Visual Studio 診斷例外狀況</span><span class="sxs-lookup"><span data-stu-id="b7cce-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="b7cce-120">在 Visual Studio 中開啟應用程式解決方案以協助偵錯。</span><span class="sxs-lookup"><span data-stu-id="b7cce-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="b7cce-121">在您的伺服器上或開發機器上使用 F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7cce-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="b7cce-122">在 Visual Studio 中開啟 [Application Insights 搜尋] 視窗，並將它設定為顯示您的應用程式的事件。</span><span class="sxs-lookup"><span data-stu-id="b7cce-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="b7cce-123">當您偵錯時，您只要按一下 [Application Insights] 按鈕即可執行此操作。</span><span class="sxs-lookup"><span data-stu-id="b7cce-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![以滑鼠右鍵按一下專案，然後選擇 [Application Insights]、[開啟]。](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="b7cce-125">請注意，您可以篩選報告僅顯示例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="b7cce-126">*未顯示例外狀況？請參閱[擷取例外狀況](#exceptions)。*</span><span class="sxs-lookup"><span data-stu-id="b7cce-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="b7cce-127">按一下例外狀況報告以顯示其堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7cce-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="b7cce-128">按一下堆疊追蹤中的行參考，以開啟相關程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="b7cce-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="b7cce-129">在程式碼中，注意 CodeLens 會顯示關於例外狀況的資料︰</span><span class="sxs-lookup"><span data-stu-id="b7cce-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![CodeLens 的例外狀況通知。](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="b7cce-131">使用 Azure 入口網站診斷失敗</span><span class="sxs-lookup"><span data-stu-id="b7cce-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="b7cce-132">從應用程式的 [Application Insights] 概要，失敗磚會顯示例外狀況和失敗的 HTTP 要求的圖表，以及導致最頻繁失敗的要求 URL 的清單。</span><span class="sxs-lookup"><span data-stu-id="b7cce-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![選取 [設定]、[失敗]](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="b7cce-134">按一下清單中其中一個失敗的例外狀況類型，可取得該例外狀況的個別發生次數，您可以在其中查看詳細資料和堆疊追蹤︰</span><span class="sxs-lookup"><span data-stu-id="b7cce-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![選取失敗要求的執行個體，並在例外狀況詳細資料底下，取得例外狀況的執行個體。](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="b7cce-136">**或者，**您可以從要求清單中啟動，並尋找與它相關的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="b7cce-137">*未顯示例外狀況？請參閱[擷取例外狀況](#exceptions)。*</span><span class="sxs-lookup"><span data-stu-id="b7cce-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="b7cce-138">自訂追蹤和記錄資料</span><span class="sxs-lookup"><span data-stu-id="b7cce-138">Custom tracing and log data</span></span>
<span data-ttu-id="b7cce-139">若要取得您的 app 的特定診斷資料，您可以插入程式碼以傳送您自己的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="b7cce-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="b7cce-140">這會隨著要求、頁面檢視和其他自動收集的資料顯示在診斷搜尋中。</span><span class="sxs-lookup"><span data-stu-id="b7cce-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="b7cce-141">您有幾種選項：</span><span class="sxs-lookup"><span data-stu-id="b7cce-141">You have several options:</span></span>

* <span data-ttu-id="b7cce-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) 通常用來監視使用模式，但它傳送的資料也會出現在診斷搜尋的 [自訂事件] 下。</span><span class="sxs-lookup"><span data-stu-id="b7cce-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="b7cce-143">事件具有名稱，並且可以包含字串屬性和數值度量，您可以對其[篩選診斷搜尋](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="b7cce-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="b7cce-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 可讓您傳送較長的資料，例如 POST 資訊。</span><span class="sxs-lookup"><span data-stu-id="b7cce-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="b7cce-145">[TrackException()](#exceptions) 會傳送堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7cce-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="b7cce-146">[深入了解例外狀況](#exceptions)。</span><span class="sxs-lookup"><span data-stu-id="b7cce-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="b7cce-147">如果您已經使用 Log4Net 或 NLog 等記錄架構，您可以[擷取這些記錄](app-insights-asp-net-trace-logs.md)，然後在診斷搜尋中將它們連同要求和例外狀況資料一起檢視。</span><span class="sxs-lookup"><span data-stu-id="b7cce-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="b7cce-148">若要查看這些事件，請開啟[搜尋](app-insights-diagnostic-search.md)、開啟 [篩選]，然後選擇 [自訂事件]、[追蹤] 或 [例外狀況]。</span><span class="sxs-lookup"><span data-stu-id="b7cce-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![鑽研](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="b7cce-150">如果您的應用程式會產生大量遙測，調適性取樣模型會自動藉由僅傳送事件代表性片段，減少傳送到入口網站的量。</span><span class="sxs-lookup"><span data-stu-id="b7cce-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="b7cce-151">為相同作業之一部分的事件會選取或取消選取為群組，讓您可以在相關事件之間瀏覽。</span><span class="sxs-lookup"><span data-stu-id="b7cce-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="b7cce-152">了解取樣。</span><span class="sxs-lookup"><span data-stu-id="b7cce-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="b7cce-153">如何查看要求 POST 資料</span><span class="sxs-lookup"><span data-stu-id="b7cce-153">How to see request POST data</span></span>
<span data-ttu-id="b7cce-154">要求詳細資料不包括在 POST 呼叫中傳送至您的應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="b7cce-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="b7cce-155">若要報告此資料：</span><span class="sxs-lookup"><span data-stu-id="b7cce-155">To have this data reported:</span></span>

* <span data-ttu-id="b7cce-156">在您的應用程式專案中[安裝 SDK](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="b7cce-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="b7cce-157">在您的應用程式中插入程式碼來呼叫 [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace)。</span><span class="sxs-lookup"><span data-stu-id="b7cce-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="b7cce-158">在訊息參數中傳送 POST 資料。</span><span class="sxs-lookup"><span data-stu-id="b7cce-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="b7cce-159">允許的大小有限制，所以您應該嘗試只傳送基本的資料。</span><span class="sxs-lookup"><span data-stu-id="b7cce-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="b7cce-160">當您調查失敗的要求時，會發現相關聯的追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7cce-160">When you investigate a failed request, find the associated traces.</span></span>  

![鑽研](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="b7cce-162"><a name="exceptions"></a> 擷取例外狀況和相關的診斷資料</span><span class="sxs-lookup"><span data-stu-id="b7cce-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="b7cce-163">一開始，您不會在入口網站看到應用程式中造成失敗的所有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="b7cce-164">您會看到任何瀏覽器例外狀況 (如果您在網頁中使用 [JavaScript SDK](app-insights-javascript.md))。</span><span class="sxs-lookup"><span data-stu-id="b7cce-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="b7cce-165">但是 IIS 會攔截大部分的伺服器例外狀況，而且您必須撰寫一段程式碼才能查看它們。</span><span class="sxs-lookup"><span data-stu-id="b7cce-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="b7cce-166">您可以：</span><span class="sxs-lookup"><span data-stu-id="b7cce-166">You can:</span></span>

* <span data-ttu-id="b7cce-167">**明確記錄例外狀況** ，方法是將程式碼插入例外狀況處理常式中，以報告例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="b7cce-168">**自動擷取例外狀況** ，方法是設定您的 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="b7cce-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="b7cce-169">架構類型不同，則必要的新增項目也不同。</span><span class="sxs-lookup"><span data-stu-id="b7cce-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="b7cce-170">明確報告例外狀況</span><span class="sxs-lookup"><span data-stu-id="b7cce-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="b7cce-171">最簡單的方法是在例外狀況處理常式中插入 TrackException() 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="b7cce-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="b7cce-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b7cce-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="b7cce-173">C#</span><span class="sxs-lookup"><span data-stu-id="b7cce-173">C#</span></span>

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

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="b7cce-174">VB</span><span class="sxs-lookup"><span data-stu-id="b7cce-174">VB</span></span>

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

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="b7cce-175">屬性和度量參數是選用的，但對於[篩選和新增](app-insights-diagnostic-search.md)額外資訊來說，相當有用。</span><span class="sxs-lookup"><span data-stu-id="b7cce-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="b7cce-176">比方說，如果您有一個應用程式可以執行數個遊戲，則您可以找到與特定遊戲相關的所有例外狀況報告。</span><span class="sxs-lookup"><span data-stu-id="b7cce-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="b7cce-177">您可以將許多項目加入至每個字典，且項目數量不限。</span><span class="sxs-lookup"><span data-stu-id="b7cce-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="b7cce-178">瀏覽器例外狀況</span><span class="sxs-lookup"><span data-stu-id="b7cce-178">Browser exceptions</span></span>
<span data-ttu-id="b7cce-179">大部分的瀏覽器例外狀況都會報告。</span><span class="sxs-lookup"><span data-stu-id="b7cce-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="b7cce-180">如果您的網頁包含來自內容傳遞網路或其他網域的指令碼檔案，請確定指令碼標籤具有屬性 ```crossorigin="anonymous"```，而且伺服器會傳送 [CORS 標頭](http://enable-cors.org/)。</span><span class="sxs-lookup"><span data-stu-id="b7cce-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="b7cce-181">這可讓您從這些資源取得未處理 JavaScript 例外狀況的堆疊追蹤和詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b7cce-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="b7cce-182">Web Form</span><span class="sxs-lookup"><span data-stu-id="b7cce-182">Web forms</span></span>
<span data-ttu-id="b7cce-183">對於 Web Form，HTTP 模組能夠在未使用 CustomErrors 設定重新導向時收集例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="b7cce-184">但是，如果您有使用中的重新導向，將下列程式碼新增至 Global.asax.cs 中的 Application_Error 函式。</span><span class="sxs-lookup"><span data-stu-id="b7cce-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="b7cce-185">(如果您還沒有檔案，請加入 Global.asax 檔案。)</span><span class="sxs-lookup"><span data-stu-id="b7cce-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="b7cce-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="b7cce-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="b7cce-187">MVC</span><span class="sxs-lookup"><span data-stu-id="b7cce-187">MVC</span></span>
<span data-ttu-id="b7cce-188">如果 [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) 組態是 `Off`，則例外狀況將可供 [HTTP 模組](https://msdn.microsoft.com/library/ms178468.aspx)收集。</span><span class="sxs-lookup"><span data-stu-id="b7cce-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="b7cce-189">不過，如果它是 `RemoteOnly` (預設值) 或 `On`，則會清除例外狀況，且不適用於讓 Application Insights 自動收集。</span><span class="sxs-lookup"><span data-stu-id="b7cce-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="b7cce-190">您可以藉由覆寫 [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)，並且針對以下不同的 MVC 版本如下所示的套用已覆寫的類別，來進行修正 ([github 來源](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs))：</span><span class="sxs-lookup"><span data-stu-id="b7cce-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

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
                //If customError is Off, then AI HTTPModule will report the exception
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

#### <a name="mvc-2"></a><span data-ttu-id="b7cce-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="b7cce-191">MVC 2</span></span>
<span data-ttu-id="b7cce-192">使用您的控制器中的新屬性取代 HandleError 屬性。</span><span class="sxs-lookup"><span data-stu-id="b7cce-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="b7cce-193">範例</span><span class="sxs-lookup"><span data-stu-id="b7cce-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="b7cce-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="b7cce-194">MVC 3</span></span>
<span data-ttu-id="b7cce-195">註冊 `AiHandleErrorAttribute` 做為 Global.asax.cs 中的全域篩選器：</span><span class="sxs-lookup"><span data-stu-id="b7cce-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="b7cce-196">範例</span><span class="sxs-lookup"><span data-stu-id="b7cce-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="b7cce-197">MVC 4、MVC5</span><span class="sxs-lookup"><span data-stu-id="b7cce-197">MVC 4, MVC5</span></span>
<span data-ttu-id="b7cce-198">註冊 AiHandleErrorAttribute 做為 FilterConfig.cs 中的全域篩選器：</span><span class="sxs-lookup"><span data-stu-id="b7cce-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="b7cce-199">範例</span><span class="sxs-lookup"><span data-stu-id="b7cce-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="b7cce-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="b7cce-200">Web API 1.x</span></span>
<span data-ttu-id="b7cce-201">覆寫 System.Web.Http.Filters.ExceptionFilterAttribute：</span><span class="sxs-lookup"><span data-stu-id="b7cce-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

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

<span data-ttu-id="b7cce-202">您可以將此覆寫的屬性加入到特定的控制器，或將它加入至 WebApiConfig 類別中的全域篩選組態：</span><span class="sxs-lookup"><span data-stu-id="b7cce-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

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

[<span data-ttu-id="b7cce-203">範例</span><span class="sxs-lookup"><span data-stu-id="b7cce-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="b7cce-204">有一些無法處理的例外狀況篩選器案例。</span><span class="sxs-lookup"><span data-stu-id="b7cce-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="b7cce-205">例如：</span><span class="sxs-lookup"><span data-stu-id="b7cce-205">For example:</span></span>

* <span data-ttu-id="b7cce-206">從控制器建構函式擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="b7cce-207">從訊息處理常式擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="b7cce-208">在路由期間擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="b7cce-209">在回應內容序列化期間擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="b7cce-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="b7cce-210">Web API 2.x</span></span>
<span data-ttu-id="b7cce-211">新增 IExceptionLogger 的實作：</span><span class="sxs-lookup"><span data-stu-id="b7cce-211">Add an implementation of IExceptionLogger:</span></span>

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

<span data-ttu-id="b7cce-212">將其新增至 WebApiConfig 中的服務：</span><span class="sxs-lookup"><span data-stu-id="b7cce-212">Add this to the services in WebApiConfig:</span></span>

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
  <span data-ttu-id="b7cce-213">}</span><span class="sxs-lookup"><span data-stu-id="b7cce-213">}</span></span>

[<span data-ttu-id="b7cce-214">範例</span><span class="sxs-lookup"><span data-stu-id="b7cce-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="b7cce-215">做為替代方案，您可以：</span><span class="sxs-lookup"><span data-stu-id="b7cce-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="b7cce-216">以 IExceptionHandler 的自訂實作取代唯一的 ExceptionHandler。</span><span class="sxs-lookup"><span data-stu-id="b7cce-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="b7cce-217">這只會在架構仍然可以選擇要傳送的回應訊息時呼叫 (不會在針對執行個體中止連接時呼叫)</span><span class="sxs-lookup"><span data-stu-id="b7cce-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="b7cce-218">例外狀況篩選器 (如以上的 Web API 1.x 控制器章節所述) - 在所有案例中均不會呼叫。</span><span class="sxs-lookup"><span data-stu-id="b7cce-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="b7cce-219">WCF</span><span class="sxs-lookup"><span data-stu-id="b7cce-219">WCF</span></span>
<span data-ttu-id="b7cce-220">新增類別，該類別會擴充屬性和實作 IErrorHandler 和 IServiceBehavior。</span><span class="sxs-lookup"><span data-stu-id="b7cce-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

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

<span data-ttu-id="b7cce-221">將屬性新增至服務實作：</span><span class="sxs-lookup"><span data-stu-id="b7cce-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="b7cce-222">範例</span><span class="sxs-lookup"><span data-stu-id="b7cce-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="b7cce-223">例外狀況效能計數器</span><span class="sxs-lookup"><span data-stu-id="b7cce-223">Exception performance counters</span></span>
<span data-ttu-id="b7cce-224">如果您已在伺服器上[安裝 Application Insights代理程式](app-insights-monitor-performance-live-website-now.md)，您便可取得由 .NET 測量的例外狀況比率圖表。</span><span class="sxs-lookup"><span data-stu-id="b7cce-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="b7cce-225">這包括已處理和未處理的 .NET 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b7cce-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="b7cce-226">開啟 [計量瀏覽器] 刀鋒視窗、加入新圖表，然後選取 [效能計數器] 下方所列的 [例外狀況比率] 。</span><span class="sxs-lookup"><span data-stu-id="b7cce-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="b7cce-227">.NET framework 會計算間隔中的例外狀況次數並除以間隔長度，以計算得出例外狀況比率。</span><span class="sxs-lookup"><span data-stu-id="b7cce-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="b7cce-228">請注意，其與 Application Insights 入口網站執行 TrackException 報告計數算得的「例外狀況」計數不同。</span><span class="sxs-lookup"><span data-stu-id="b7cce-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="b7cce-229">取樣間隔不同，且 SDK 不會針對所有已處理與未處理的例外狀況傳送 TrackException 報告。</span><span class="sxs-lookup"><span data-stu-id="b7cce-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="b7cce-230">影片</span><span class="sxs-lookup"><span data-stu-id="b7cce-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="b7cce-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7cce-231">Next steps</span></span>
* [<span data-ttu-id="b7cce-232">監視 REST、SQL 及其他對相依性的呼叫</span><span class="sxs-lookup"><span data-stu-id="b7cce-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="b7cce-233">監視頁面載入時間、瀏覽器例外狀況及 AJAX 呼叫</span><span class="sxs-lookup"><span data-stu-id="b7cce-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="b7cce-234">監視效能計數器</span><span class="sxs-lookup"><span data-stu-id="b7cce-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
