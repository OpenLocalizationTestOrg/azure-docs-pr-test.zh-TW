---
title: "ApplicationInsights.config 參考 - Azure | Microsoft Docs"
description: "啟用或停用資料收集模組，以及加入效能計數器和其他參數。"
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 7737f47d4181b5e920434f3a5372991efb58f63e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="55fbf-103">使用 ApplicationInsights.config 或 .xml 設定 Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="55fbf-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="55fbf-104">Application Insights .NET SDK 是由數個 NuGet 封裝所組成。</span><span class="sxs-lookup"><span data-stu-id="55fbf-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="55fbf-105">[核心封裝](http://www.nuget.org/packages/Microsoft.ApplicationInsights) 提供 API，用於傳送遙測至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="55fbf-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="55fbf-106">[其他套件](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights)提供遙測*模組*和*初始設定式*，用於自動從您的應用程式和其內容追蹤遙測。</span><span class="sxs-lookup"><span data-stu-id="55fbf-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="55fbf-107">您可以藉由調整組態檔，來啟用或停用遙測模組和初始設定式，並為其設定一些參數。</span><span class="sxs-lookup"><span data-stu-id="55fbf-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="55fbf-108">組態檔的名稱為 `ApplicationInsights.config` 或 `ApplicationInsights.xml`，端視您的應用程式類型而定。</span><span class="sxs-lookup"><span data-stu-id="55fbf-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="55fbf-109">當您[安裝大部分版本的 SDK][start] 時，系統會自動將組態檔加入至您的專案。</span><span class="sxs-lookup"><span data-stu-id="55fbf-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="55fbf-110">[IIS 伺服器上的狀態監視器][redfield]，或是當您[選取 Azure 網站或 VM 的 Application Insights 延伸模組](app-insights-azure-web-apps.md)時，也會將組態檔加入至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55fbf-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="55fbf-111">沒有同等的檔案可以控制[網頁中的 SDK][client]。</span><span class="sxs-lookup"><span data-stu-id="55fbf-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="55fbf-112">本文件說明您在組態檔中看到的內容、控制 SDK 元件的方式，以及哪些 NuGet 封裝載入這些元件。</span><span class="sxs-lookup"><span data-stu-id="55fbf-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="55fbf-113">遙測模組 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="55fbf-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="55fbf-114">每個遙測模組收集特定類型的資料，以及使用核心 API 來傳送資料。</span><span class="sxs-lookup"><span data-stu-id="55fbf-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="55fbf-115">模組由不同的 NuGet 封裝安裝，也會將必要的行加入 .config 檔案。</span><span class="sxs-lookup"><span data-stu-id="55fbf-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="55fbf-116">組態檔中的每個模組都有一個節點。</span><span class="sxs-lookup"><span data-stu-id="55fbf-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="55fbf-117">若要停用模組，請刪除節點或將其註解化。</span><span class="sxs-lookup"><span data-stu-id="55fbf-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="55fbf-118">相依性追蹤</span><span class="sxs-lookup"><span data-stu-id="55fbf-118">Dependency Tracking</span></span>
<span data-ttu-id="55fbf-119">[相依性追蹤](app-insights-asp-net-dependencies.md) 會收集有關您的 app 對資料庫和外部服務和資料庫呼叫的遙測。</span><span class="sxs-lookup"><span data-stu-id="55fbf-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="55fbf-120">若要允許此模組用於 IIS 伺服器，您必須[安裝狀態監視器][redfield]。</span><span class="sxs-lookup"><span data-stu-id="55fbf-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="55fbf-121">若要在 Azure Web 應用程式或 VM 中使用此模組， [請選取 Application Insights 延伸模組](app-insights-azure-web-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="55fbf-122">您也可以使用 [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)撰寫您自己的相依性追蹤程式碼。</span><span class="sxs-lookup"><span data-stu-id="55fbf-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="55fbf-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55fbf-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="55fbf-124">效能收集器</span><span class="sxs-lookup"><span data-stu-id="55fbf-124">Performance collector</span></span>
<span data-ttu-id="55fbf-125">[收集系統效能計數器](app-insights-performance-counters.md)，例如 CPU、記憶體和網路負載 (從 IIS 安裝)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="55fbf-126">您可以指定要收集哪些計數器，包括您自己所設定的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="55fbf-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="55fbf-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55fbf-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="55fbf-128">Application Insights 診斷遙測</span><span class="sxs-lookup"><span data-stu-id="55fbf-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="55fbf-129">`DiagnosticsTelemetryModule` 報告 Application Insights 檢測程式碼本身中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="55fbf-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="55fbf-130">例如，如果程式碼無法存取效能計數器，或 `ITelemetryInitializer` 擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="55fbf-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="55fbf-131">此模組所追蹤的追蹤遙測會出現在[診斷搜尋][diagnostic]中。</span><span class="sxs-lookup"><span data-stu-id="55fbf-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="55fbf-132">將診斷資料傳送至 dc.services.vsallin.net。</span><span class="sxs-lookup"><span data-stu-id="55fbf-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="55fbf-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55fbf-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="55fbf-134">如果您只安裝這個封裝，不會自動建立 ApplicationInsights.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="55fbf-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="55fbf-135">開發人員模式</span><span class="sxs-lookup"><span data-stu-id="55fbf-135">Developer Mode</span></span>
<span data-ttu-id="55fbf-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` 會強制 Application Insights `TelemetryChannel` 立即傳送資料，在偵錯工具附加至應用程式程序時一次傳送一個遙測項目。</span><span class="sxs-lookup"><span data-stu-id="55fbf-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="55fbf-137">這會減少您的應用程式追蹤遙測時，與當遙測出現在 Application Insights 入口網站時之間的時間量。</span><span class="sxs-lookup"><span data-stu-id="55fbf-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="55fbf-138">但是會造成 CPU 和網路頻寬明顯的負擔。</span><span class="sxs-lookup"><span data-stu-id="55fbf-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="55fbf-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="55fbf-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="55fbf-140">Web 要求追蹤</span><span class="sxs-lookup"><span data-stu-id="55fbf-140">Web Request Tracking</span></span>
<span data-ttu-id="55fbf-141">報告 HTTP 要求的 [回應時間和結果碼](app-insights-asp-net.md) 。</span><span class="sxs-lookup"><span data-stu-id="55fbf-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="55fbf-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55fbf-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="55fbf-143">例外狀況追蹤</span><span class="sxs-lookup"><span data-stu-id="55fbf-143">Exception tracking</span></span>
<span data-ttu-id="55fbf-144">`ExceptionTrackingTelemetryModule` 追蹤 Web 應用程式中未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="55fbf-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="55fbf-145">請參閱[失敗和例外狀況][exceptions]。</span><span class="sxs-lookup"><span data-stu-id="55fbf-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="55fbf-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55fbf-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="55fbf-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - 追蹤 [未觀察到的工作例外狀況](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="55fbf-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - 追蹤背景工作角色、Windows 服務和主控台應用程式的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="55fbf-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="55fbf-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55fbf-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="55fbf-150">EventSource 追蹤</span><span class="sxs-lookup"><span data-stu-id="55fbf-150">EventSource Tracking</span></span>
<span data-ttu-id="55fbf-151">`EventSourceTelemetryModule` 可讓您設定要傳送至 Application Insights 作為追蹤的 EventSource 事件。</span><span class="sxs-lookup"><span data-stu-id="55fbf-151">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="55fbf-152">如需追蹤 EventSource 事件的資訊，請參閱[使用 EventSource 事件](app-insights-asp-net-trace-logs.md#using-eventsource-events)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="55fbf-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="55fbf-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="55fbf-154">ETW 事件追蹤</span><span class="sxs-lookup"><span data-stu-id="55fbf-154">ETW Event Tracking</span></span>
<span data-ttu-id="55fbf-155">`EtwCollectorTelemetryModule` 可讓您設定要傳送至 Application Insights 作為追蹤的 ETW 提供者事件。</span><span class="sxs-lookup"><span data-stu-id="55fbf-155">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="55fbf-156">如需追蹤 ETW 事件的資訊，請參閱[使用 ETW 事件](app-insights-asp-net-trace-logs.md#using-etw-events)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="55fbf-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="55fbf-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="55fbf-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="55fbf-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="55fbf-159">Microsoft.ApplicationInsights 封裝提供 SDK 的 [核心 API](https://msdn.microsoft.com/library/mt420197.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="55fbf-159">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="55fbf-160">其他遙測模組使用此功能，您也可以 [使用它來定義您自己的遙測](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-160">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="55fbf-161">ApplicationInsights.config 中沒有項目。</span><span class="sxs-lookup"><span data-stu-id="55fbf-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="55fbf-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55fbf-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="55fbf-163">如果您只安裝此 NuGet，不會產生任何 .config 檔案。</span><span class="sxs-lookup"><span data-stu-id="55fbf-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="55fbf-164">遙測通道</span><span class="sxs-lookup"><span data-stu-id="55fbf-164">Telemetry Channel</span></span>
<span data-ttu-id="55fbf-165">遙測通道管理遙測的緩衝處理和到 Application Insights 服務的傳輸。</span><span class="sxs-lookup"><span data-stu-id="55fbf-165">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="55fbf-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` 是服務的預設通道。</span><span class="sxs-lookup"><span data-stu-id="55fbf-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="55fbf-167">它會在記憶體中緩衝資料。</span><span class="sxs-lookup"><span data-stu-id="55fbf-167">It buffers data in memory.</span></span>
* <span data-ttu-id="55fbf-168">`Microsoft.ApplicationInsights.PersistenceChannel` 是主控台應用程式的替代通道。</span><span class="sxs-lookup"><span data-stu-id="55fbf-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="55fbf-169">它可以在您的 app 關閉時將任何未清除的資料儲存到永續性儲存體，並在 app 重新啟動時再次傳送資料。</span><span class="sxs-lookup"><span data-stu-id="55fbf-169">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="55fbf-170">遙測初始設定式 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="55fbf-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="55fbf-171">遙測初始設定式設定與遙測的每個項目一起傳送的內容屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="55fbf-172">您可以 [撰寫您自己的初始設定式](app-insights-api-filtering-sampling.md#add-properties) 設定內容屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="55fbf-173">標準的初始設定式已由 Web 或 WindowsServer NuGet 封裝設定：</span><span class="sxs-lookup"><span data-stu-id="55fbf-173">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="55fbf-174">`AccountIdTelemetryInitializer` 設定 AccountId 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-174">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="55fbf-175">`AuthenticatedUserIdTelemetryInitializer` 如 JavaScript SDK 設定般設定 AuthenticatedUserId 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-175">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="55fbf-176">針對具有從 Azure 執行階段環境擷取之資訊的所有遙測項目，`AzureRoleEnvironmentTelemetryInitializer` 會更新 `Device` 內容的 `RoleName` 和 `RoleInstance` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-176">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="55fbf-177">針對具有從 MS 組建所產生之 `BuildInfo.config` 檔案擷取值的所有遙測項目，`BuildInfoConfigComponentVersionTelemetryInitializer` 會更新 `Component` 內容的 `Version` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="55fbf-178">`ClientIpHeaderTelemetryInitializer` 會根據要求的 `X-Forwarded-For` HTTP 標頭來更新所有遙測項目之 `Location` 內容的 `Ip` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="55fbf-179">`DeviceTelemetryInitializer` 會更新所有遙測項目 `Device` 內容的下列屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-179">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="55fbf-180">`Type` 設定為 "PC"</span><span class="sxs-lookup"><span data-stu-id="55fbf-180">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="55fbf-181">`Id` 設定為 Web 應用程式執行所在電腦的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="55fbf-181">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="55fbf-182">`OemName` 設定為使用 WMI 從 `Win32_ComputerSystem.Manufacturer` 欄位擷取的值。</span><span class="sxs-lookup"><span data-stu-id="55fbf-182">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="55fbf-183">`Model` 設定為使用 WMI 從 `Win32_ComputerSystem.Model` 欄位擷取的值。</span><span class="sxs-lookup"><span data-stu-id="55fbf-183">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="55fbf-184">`NetworkType` 設定為從 `NetworkInterface` 擷取的值。</span><span class="sxs-lookup"><span data-stu-id="55fbf-184">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="55fbf-185">`Language` 設定為 `CurrentCulture` 的名稱。</span><span class="sxs-lookup"><span data-stu-id="55fbf-185">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="55fbf-186">針對具有 Web 應用程式執行所在電腦之網域名稱的所有遙測項目，`DomainNameRoleInstanceTelemetryInitializer` 會更新 `Device` 內容的 `RoleInstance` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-186">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="55fbf-187">`OperationNameTelemetryInitializer` 會根據 HTTP 方法，以及 ASP.NET MVC 控制器的名稱和叫用來處理要求的動作，更新所有遙測項目 `RequestTelemetry` 之 `Name` 屬性和 `Operation` 內容的 `Name` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-187">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="55fbf-188">`OperationIdTelemetryInitializer` 或 `OperationCorrelationTelemetryInitializer` 在處理具有自動產生的 `RequestTelemetry.Id` 的要求時，會更新追蹤的所有遙測項目的 `Operation.Id` 內容屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="55fbf-189">針對具有從使用者瀏覽器中執行的 Application Insights JavaScript 檢測程式碼所產生之 `ai_session` Cookie 擷取值的所有遙測項目，`SessionTelemetryInitializer` 會更新 `Session` 內容的 `Id` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-189">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="55fbf-190">`SyntheticTelemetryInitializer` 或 `SyntheticUserAgentTelemetryInitializer` 在處理來自綜合來源 (例如可用性測試或搜尋引擎 Bot) 的要求時，會更新追蹤的所有遙測項目的 `User`、`Session` 和 `Operation` 內容屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="55fbf-191">根據預設， [計量瀏覽器](app-insights-metrics-explorer.md) 不會顯示綜合的遙測。</span><span class="sxs-lookup"><span data-stu-id="55fbf-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="55fbf-192">`<Filters>` 會設定要求的識別屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-192">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="55fbf-193">`UserAgentTelemetryInitializer` 會根據要求的 `User-Agent` HTTP 標頭來更新所有遙測項目之 `User` 內容的 `UserAgent` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-193">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="55fbf-194">針對具有從使用者瀏覽器中執行之 Application Insights JavaScript 檢測程式碼所產生的 `ai_user` Cookie 擷取值的所有遙測項目，`UserTelemetryInitializer` 會更新 `User` 內容的 `Id` 和 `AcquisitionDate` 屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-194">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="55fbf-195">`WebTestTelemetryInitializer` 會設定使用者識別碼、工作階段識別碼，以及來自 [可用性測試](app-insights-monitor-web-app-availability.md)的 HTTP 要求的綜合來源屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-195">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="55fbf-196">`<Filters>` 會設定要求的識別屬性。</span><span class="sxs-lookup"><span data-stu-id="55fbf-196">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="55fbf-197">針對 Service Fabric 中執行的 .NET 應用程式，您可以包含 `Microsoft.ApplicationInsights.ServiceFabric` NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="55fbf-197">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="55fbf-198">此套件包含的 `FabricTelemetryInitializer` 會將 Service Fabric 屬性新增至遙測項目。</span><span class="sxs-lookup"><span data-stu-id="55fbf-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="55fbf-199">如需詳細資訊，請參閱 [GitHub 頁面](https://go.microsoft.com/fwlink/?linkid=848457)了解這個 NuGet 套件所新增之屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="55fbf-199">For more information, see the [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="55fbf-200">遙測處理器 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="55fbf-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="55fbf-201">遙測處理器可以在遙測從 SDK 傳送至入口網站之前篩選並修改每個遙測項目。</span><span class="sxs-lookup"><span data-stu-id="55fbf-201">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="55fbf-202">您可以 [撰寫您自己的遙測處理器](app-insights-api-filtering-sampling.md#filtering)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="55fbf-203">自適性取樣遙測處理器 (自 2.0.0-beta3 起)</span><span class="sxs-lookup"><span data-stu-id="55fbf-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="55fbf-204">此選項預設為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="55fbf-204">This is enabled by default.</span></span> <span data-ttu-id="55fbf-205">如果您的應用程式傳送許多遙測，此處理器會移除其中一些遙測。</span><span class="sxs-lookup"><span data-stu-id="55fbf-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="55fbf-206">參數會提供演算法嘗試要達成的目標。</span><span class="sxs-lookup"><span data-stu-id="55fbf-206">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="55fbf-207">每個 SDK 執行個體都獨立運作，因此如果您的伺服器是數個機器的叢集，遙測的實際數量會隨之加乘。</span><span class="sxs-lookup"><span data-stu-id="55fbf-207">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="55fbf-208">[深入了解取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="55fbf-209">固定取樣遙測處理器 (自 2.0.0-beta1 起)</span><span class="sxs-lookup"><span data-stu-id="55fbf-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="55fbf-210">還有一種標準的 [取樣遙測處理器](app-insights-api-filtering-sampling.md) (自 2.0.1 起)：</span><span class="sxs-lookup"><span data-stu-id="55fbf-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="55fbf-211">通道參數 (Java)</span><span class="sxs-lookup"><span data-stu-id="55fbf-211">Channel parameters (Java)</span></span>
<span data-ttu-id="55fbf-212">這些參數會影響 Java SDK 應該儲存和排清它所收集之遙測資料的方式。</span><span class="sxs-lookup"><span data-stu-id="55fbf-212">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="55fbf-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="55fbf-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="55fbf-214">可以儲存在 SDK 記憶體內儲存空間中的遙測項目數。</span><span class="sxs-lookup"><span data-stu-id="55fbf-214">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="55fbf-215">達到這個數目時，會排清遙測緩衝區，也就是將遙測項目傳送至 Application Insights 伺服器。</span><span class="sxs-lookup"><span data-stu-id="55fbf-215">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="55fbf-216">最小值：1</span><span class="sxs-lookup"><span data-stu-id="55fbf-216">Min: 1</span></span>
* <span data-ttu-id="55fbf-217">最大值：1000</span><span class="sxs-lookup"><span data-stu-id="55fbf-217">Max: 1000</span></span>
* <span data-ttu-id="55fbf-218">預設值：500</span><span class="sxs-lookup"><span data-stu-id="55fbf-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="55fbf-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="55fbf-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="55fbf-220">決定應該以何種頻率排清儲存在記憶體內儲存空間的資料 (並傳送至 Application Insights)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-220">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="55fbf-221">最小值：1</span><span class="sxs-lookup"><span data-stu-id="55fbf-221">Min: 1</span></span>
* <span data-ttu-id="55fbf-222">最大值：300</span><span class="sxs-lookup"><span data-stu-id="55fbf-222">Max: 300</span></span>
* <span data-ttu-id="55fbf-223">預設值：5</span><span class="sxs-lookup"><span data-stu-id="55fbf-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="55fbf-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="55fbf-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="55fbf-225">決定分配給本機磁碟上永續性存放裝置的大小上限 (MB)。</span><span class="sxs-lookup"><span data-stu-id="55fbf-225">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="55fbf-226">此存放裝置會用於保存無法傳送至 Application Insights 端點的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="55fbf-226">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="55fbf-227">存放裝置大小達到上限時，會捨棄新的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="55fbf-227">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="55fbf-228">最小值：1</span><span class="sxs-lookup"><span data-stu-id="55fbf-228">Min: 1</span></span>
* <span data-ttu-id="55fbf-229">最大值：100</span><span class="sxs-lookup"><span data-stu-id="55fbf-229">Max: 100</span></span>
* <span data-ttu-id="55fbf-230">預設值：10</span><span class="sxs-lookup"><span data-stu-id="55fbf-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="55fbf-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="55fbf-231">InstrumentationKey</span></span>
<span data-ttu-id="55fbf-232">這會決定顯示您資料的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="55fbf-232">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="55fbf-233">通常您會針對每個應用程式，用個別的金鑰建立個別資源。</span><span class="sxs-lookup"><span data-stu-id="55fbf-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="55fbf-234">如果想要以動態方式設定金鑰 (例如，想要將應用程式的結果傳送到不同的資源)，您可以在組態檔中省略金鑰，並將金鑰設定在程式碼中。</span><span class="sxs-lookup"><span data-stu-id="55fbf-234">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="55fbf-235">若要針對 TelemetryClient 的所有執行個體 (包括標準遙測模組) 設定金鑰，請在 TelemetryConfiguration.Active 中設定金鑰。</span><span class="sxs-lookup"><span data-stu-id="55fbf-235">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="55fbf-236">請在初始化方法中這麼做，例如 ASP.NET 服務中的 global.aspx.cs：</span><span class="sxs-lookup"><span data-stu-id="55fbf-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="55fbf-237">如果您只想將特定的一組事件傳送至不同的資源，可以針對特定的 TelemetryClient 設定金鑰：</span><span class="sxs-lookup"><span data-stu-id="55fbf-237">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="55fbf-238">若要取得新的金鑰，請[在 Application Insights 入口網站中建立新的資源][new]。</span><span class="sxs-lookup"><span data-stu-id="55fbf-238">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="55fbf-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55fbf-239">Next steps</span></span>
<span data-ttu-id="55fbf-240">[深入了解 API][api]。</span><span class="sxs-lookup"><span data-stu-id="55fbf-240">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
