---
title: "aaaApplicationInsights.config 參考-Azure |Microsoft 文件"
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
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="1f311-103">設定 Application Insights SDK hello ApplicationInsights.config 或.xml</span><span class="sxs-lookup"><span data-stu-id="1f311-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="1f311-104">hello Application Insights.NET SDK 的 NuGet 套件的數字所組成。</span><span class="sxs-lookup"><span data-stu-id="1f311-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="1f311-105">[Core 套件](http://www.nuget.org/packages/Microsoft.ApplicationInsights)提供 hello API，以將遙測傳送至 Application Insights hello。</span><span class="sxs-lookup"><span data-stu-id="1f311-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="1f311-106">[其他套件](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights)提供遙測*模組*和*初始設定式*，用於自動從您的應用程式和其內容追蹤遙測。</span><span class="sxs-lookup"><span data-stu-id="1f311-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="1f311-107">藉由調整 hello 設定檔，您可以啟用或停用遙測模組和初始設定式，和設定其中部分的參數。</span><span class="sxs-lookup"><span data-stu-id="1f311-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="1f311-108">hello 設定檔的名稱為`ApplicationInsights.config`或`ApplicationInsights.xml`，視您的應用程式的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="1f311-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="1f311-109">它會自動加入 tooyour 專案時您[安裝大部分的 hello SDK 版本][start]。</span><span class="sxs-lookup"><span data-stu-id="1f311-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="1f311-110">它也會加入 tooa web 應用程式由[IIS 伺服器上的狀態監視][redfield]，或當您選取 hello Appplication Insights[延伸模組的 Azure 網站或 VM](app-insights-azure-web-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="1f311-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="1f311-111">沒有對等檔案 toocontrol hello[在網頁中的 SDK][client]。</span><span class="sxs-lookup"><span data-stu-id="1f311-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="1f311-112">本文件描述您看到 hello 組態檔案，控制 hello hello SDK 元件的方式，以及哪些 NuGet 封裝會載入這些元件的 hello 區段。</span><span class="sxs-lookup"><span data-stu-id="1f311-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="1f311-113">遙測模組 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1f311-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="1f311-114">每個遙測模組收集特定類型的資料，並使用 hello 核心 API toosend hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1f311-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="1f311-115">hello 模組會安裝由不同的 NuGet 封裝，也加入 hello 需要的線條 toohello.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1f311-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="1f311-116">每個模組的 hello 組態檔中沒有節點。</span><span class="sxs-lookup"><span data-stu-id="1f311-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="1f311-117">toodisable 模組，請刪除 hello 節點，或加以註解化。</span><span class="sxs-lookup"><span data-stu-id="1f311-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="1f311-118">相依性追蹤</span><span class="sxs-lookup"><span data-stu-id="1f311-118">Dependency Tracking</span></span>
<span data-ttu-id="1f311-119">[相依性追蹤](app-insights-asp-net-dependencies.md)收集呼叫 toodatabases 和外部服務，以及資料庫，可讓您的應用程式的相關遙測。</span><span class="sxs-lookup"><span data-stu-id="1f311-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="1f311-120">tooallow 此模組會 toowork 在 IIS 伺服器，您需要太[安裝狀態監視器][redfield]。</span><span class="sxs-lookup"><span data-stu-id="1f311-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="1f311-121">toouse 在 Azure web 應用程式或 Vm，[選取 hello Application Insights 擴充功能](app-insights-azure-web-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="1f311-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="1f311-122">您也可以撰寫您自己的相依性追蹤程式碼使用 hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)。</span><span class="sxs-lookup"><span data-stu-id="1f311-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="1f311-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="1f311-124">效能收集器</span><span class="sxs-lookup"><span data-stu-id="1f311-124">Performance collector</span></span>
<span data-ttu-id="1f311-125">[收集系統效能計數器](app-insights-performance-counters.md)，例如 CPU、記憶體和網路負載 (從 IIS 安裝)。</span><span class="sxs-lookup"><span data-stu-id="1f311-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="1f311-126">您可以指定哪些計數器 toocollect，包括您已設定您自己的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1f311-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="1f311-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="1f311-128">Application Insights 診斷遙測</span><span class="sxs-lookup"><span data-stu-id="1f311-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="1f311-129">hello`DiagnosticsTelemetryModule`報告 hello 本身 Application Insights 檢測程式碼中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="1f311-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="1f311-130">例如，如果 hello 程式碼無法存取效能計數器或`ITelemetryInitializer`擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1f311-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="1f311-131">此模組所追蹤的追蹤遙測會出現在 hello[診斷搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="1f311-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="1f311-132">傳送診斷資料 toodc.services.vsallin.net。</span><span class="sxs-lookup"><span data-stu-id="1f311-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="1f311-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="1f311-134">如果您只安裝這個套件，不會自動建立 hello ApplicationInsights.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="1f311-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="1f311-135">開發人員模式</span><span class="sxs-lookup"><span data-stu-id="1f311-135">Developer Mode</span></span>
<span data-ttu-id="1f311-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`強制 hello Application Insights `TelemetryChannel` toosend 資料立即一個遙測項目一次，當偵錯工具附加 toohello 應用程式處理序。</span><span class="sxs-lookup"><span data-stu-id="1f311-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="1f311-137">這會減少 hello hello 時間之間的時間量，以及出現在 hello Application Insights 入口網站時您的應用程式會追蹤遙測。</span><span class="sxs-lookup"><span data-stu-id="1f311-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="1f311-138">但是會造成 CPU 和網路頻寬明顯的負擔。</span><span class="sxs-lookup"><span data-stu-id="1f311-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="1f311-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="1f311-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="1f311-140">Web 要求追蹤</span><span class="sxs-lookup"><span data-stu-id="1f311-140">Web Request Tracking</span></span>
<span data-ttu-id="1f311-141">報表 hello[回應時間與結果碼](app-insights-asp-net.md)的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="1f311-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="1f311-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="1f311-143">例外狀況追蹤</span><span class="sxs-lookup"><span data-stu-id="1f311-143">Exception tracking</span></span>
<span data-ttu-id="1f311-144">`ExceptionTrackingTelemetryModule` 追蹤 Web 應用程式中未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1f311-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="1f311-145">請參閱[失敗和例外狀況][exceptions]。</span><span class="sxs-lookup"><span data-stu-id="1f311-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="1f311-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="1f311-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - 追蹤 [未觀察到的工作例外狀況](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1f311-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="1f311-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - 追蹤背景工作角色、Windows 服務和主控台應用程式的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1f311-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="1f311-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="1f311-150">EventSource 追蹤</span><span class="sxs-lookup"><span data-stu-id="1f311-150">EventSource Tracking</span></span>
<span data-ttu-id="1f311-151">`EventSourceTelemetryModule`可讓您 tooconfigure EventSource 事件 toobe tooApplication Insights 當做追蹤。</span><span class="sxs-lookup"><span data-stu-id="1f311-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="1f311-152">如需追蹤 EventSource 事件的資訊，請參閱[使用 EventSource 事件](app-insights-asp-net-trace-logs.md#using-eventsource-events)。</span><span class="sxs-lookup"><span data-stu-id="1f311-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="1f311-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="1f311-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="1f311-154">ETW 事件追蹤</span><span class="sxs-lookup"><span data-stu-id="1f311-154">ETW Event Tracking</span></span>
<span data-ttu-id="1f311-155">`EtwCollectorTelemetryModule`可讓您從以追蹤傳送 tooApplication Insights ETW 提供者 toobe tooconfigure 事件。</span><span class="sxs-lookup"><span data-stu-id="1f311-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="1f311-156">如需追蹤 ETW 事件的資訊，請參閱[使用 ETW 事件](app-insights-asp-net-trace-logs.md#using-etw-events)。</span><span class="sxs-lookup"><span data-stu-id="1f311-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="1f311-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="1f311-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="1f311-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="1f311-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="1f311-159">hello Microsoft.ApplicationInsights 套件提供 hello[核心 API](https://msdn.microsoft.com/library/mt420197.aspx)的 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="1f311-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="1f311-160">hello 其他遙測模組使用，而且您也可以[toodefine 使用它自己的遙測](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="1f311-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="1f311-161">ApplicationInsights.config 中沒有項目。</span><span class="sxs-lookup"><span data-stu-id="1f311-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="1f311-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="1f311-163">如果您只安裝此 NuGet，不會產生任何 .config 檔案。</span><span class="sxs-lookup"><span data-stu-id="1f311-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="1f311-164">遙測通道</span><span class="sxs-lookup"><span data-stu-id="1f311-164">Telemetry Channel</span></span>
<span data-ttu-id="1f311-165">hello 遙測通道會管理緩衝和遙測 toohello Application Insights 服務的傳輸。</span><span class="sxs-lookup"><span data-stu-id="1f311-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="1f311-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`是服務的 hello 預設通道。</span><span class="sxs-lookup"><span data-stu-id="1f311-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="1f311-167">它會在記憶體中緩衝資料。</span><span class="sxs-lookup"><span data-stu-id="1f311-167">It buffers data in memory.</span></span>
* <span data-ttu-id="1f311-168">`Microsoft.ApplicationInsights.PersistenceChannel` 是主控台應用程式的替代通道。</span><span class="sxs-lookup"><span data-stu-id="1f311-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="1f311-169">當您的應用程式關閉，並會將它傳送 hello 應用程式一次啟動時，便可以節省任何 unflushed 的資料 toopersistent 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="1f311-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="1f311-170">遙測初始設定式 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1f311-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="1f311-171">遙測初始設定式設定與遙測的每個項目一起傳送的內容屬性。</span><span class="sxs-lookup"><span data-stu-id="1f311-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="1f311-172">您可以[撰寫您自己的初始設定式](app-insights-api-filtering-sampling.md#add-properties)tooset 內容屬性。</span><span class="sxs-lookup"><span data-stu-id="1f311-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="1f311-173">hello 標準初始設定式已設定完畢由 hello Web 或 WindowsServer NuGet 封裝：</span><span class="sxs-lookup"><span data-stu-id="1f311-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="1f311-174">`AccountIdTelemetryInitializer`設定 hello AccountId 屬性。</span><span class="sxs-lookup"><span data-stu-id="1f311-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="1f311-175">`AuthenticatedUserIdTelemetryInitializer`hello JavaScript SDK hello AuthenticatedUserId 屬性設定為集合。</span><span class="sxs-lookup"><span data-stu-id="1f311-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="1f311-176">`AzureRoleEnvironmentTelemetryInitializer`更新 hello`RoleName`和`RoleInstance`屬性 hello`Device`從 hello Azure 執行階段環境中擷取資訊的所有遙測項目內容。</span><span class="sxs-lookup"><span data-stu-id="1f311-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="1f311-177">`BuildInfoConfigComponentVersionTelemetryInitializer`更新 hello`Version`屬性 hello `Component` hello 值 hello 從擷取的所有遙測項目內容`BuildInfo.config`由 MS Build 所產生的檔案。</span><span class="sxs-lookup"><span data-stu-id="1f311-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="1f311-178">`ClientIpHeaderTelemetryInitializer`更新`Ip`屬性 hello`Location`所有遙測項目的內容根據 hello `X-Forwarded-For` hello 要求的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="1f311-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="1f311-179">`DeviceTelemetryInitializer`下列屬性的 hello 更新 hello`Device`遙測的所有項目內容。</span><span class="sxs-lookup"><span data-stu-id="1f311-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="1f311-180">`Type`設定得 「 電腦 」</span><span class="sxs-lookup"><span data-stu-id="1f311-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="1f311-181">`Id`已設定 hello web 應用程式執行所在 toohello hello 電腦網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1f311-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="1f311-182">`OemName`設定為擷取自 hello toohello 值`Win32_ComputerSystem.Manufacturer`欄位使用 WMI。</span><span class="sxs-lookup"><span data-stu-id="1f311-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="1f311-183">`Model`設定為擷取自 hello toohello 值`Win32_ComputerSystem.Model`欄位使用 WMI。</span><span class="sxs-lookup"><span data-stu-id="1f311-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="1f311-184">`NetworkType`設定為擷取自 hello toohello 值`NetworkInterface`。</span><span class="sxs-lookup"><span data-stu-id="1f311-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="1f311-185">`Language`設定的 hello toohello 名稱`CurrentCulture`。</span><span class="sxs-lookup"><span data-stu-id="1f311-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="1f311-186">`DomainNameRoleInstanceTelemetryInitializer`更新 hello`RoleInstance`屬性 hello`Device`遙測的所有項目 hello 網域名稱與 hello hello web 應用程式執行所在的電腦內容。</span><span class="sxs-lookup"><span data-stu-id="1f311-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="1f311-187">`OperationNameTelemetryInitializer`更新 hello`Name`屬性 hello`RequestTelemetry`和 hello`Name`屬性 hello`Operation`所有遙測項目的內容根據 hello HTTP 方法，以及 ASP.NET MVC 控制器和動作叫用的 tooprocess hello 的名稱要求。</span><span class="sxs-lookup"><span data-stu-id="1f311-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="1f311-188">`OperationIdTelemetryInitializer`或`OperationCorrelationTelemetryInitializer`更新 hello`Operation.Id`內容屬性的所有遙測項目追蹤同時處理要求，以自動產生的 hello `RequestTelemetry.Id`。</span><span class="sxs-lookup"><span data-stu-id="1f311-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="1f311-189">`SessionTelemetryInitializer`更新 hello`Id`屬性 hello `Session` hello 從擷取值的所有遙測項目內容`ai_session`cookie 所 hello ApplicationInsights JavaScript hello 使用者的瀏覽器中執行的檢測程式碼產生。</span><span class="sxs-lookup"><span data-stu-id="1f311-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="1f311-190">`SyntheticTelemetryInitializer`或`SyntheticUserAgentTelemetryInitializer`更新 hello `User`，`Session`和`Operation`時處理的要求的綜合的來源，例如可用性測試，或搜尋引擎 bot 追蹤這些內容屬性的所有遙測項目。</span><span class="sxs-lookup"><span data-stu-id="1f311-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="1f311-191">根據預設， [計量瀏覽器](app-insights-metrics-explorer.md) 不會顯示綜合的遙測。</span><span class="sxs-lookup"><span data-stu-id="1f311-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="1f311-192">hello`<Filters>`設定識別之 hello 要求的內容。</span><span class="sxs-lookup"><span data-stu-id="1f311-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="1f311-193">`UserAgentTelemetryInitializer`更新 hello`UserAgent`屬性 hello`User`所有遙測項目的內容根據 hello `User-Agent` hello 要求的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="1f311-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="1f311-194">`UserTelemetryInitializer`更新 hello`Id`和`AcquisitionDate`屬性`User`內容擷取自 hello 值的所有遙測項目`ai_user`hello 中執行的 hello Application Insights JavaScript 檢測程式碼所產生的 cookie使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1f311-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="1f311-195">`WebTestTelemetryInitializer`設定 hello 使用者 id、 工作階段識別碼和綜合的來源屬性的 HTTP 要求，來自[可用性測試](app-insights-monitor-web-app-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="1f311-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="1f311-196">hello`<Filters>`設定識別之 hello 要求的內容。</span><span class="sxs-lookup"><span data-stu-id="1f311-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="1f311-197">Service Fabric 中執行的.NET 應用程式，您可以包含 hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="1f311-198">這個套件包括`FabricTelemetryInitializer`，這樣會將 Service Fabric 屬性 tootelemetry 項目。</span><span class="sxs-lookup"><span data-stu-id="1f311-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="1f311-199">如需詳細資訊，請參閱 hello [GitHub 頁面](https://go.microsoft.com/fwlink/?linkid=848457)有關 hello 屬性加入此 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1f311-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="1f311-200">遙測處理器 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1f311-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="1f311-201">遙測處理器可以篩選和寄 hello SDK toohello 入口網站之前，請修改每個遙測項目。</span><span class="sxs-lookup"><span data-stu-id="1f311-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="1f311-202">您可以 [撰寫您自己的遙測處理器](app-insights-api-filtering-sampling.md#filtering)。</span><span class="sxs-lookup"><span data-stu-id="1f311-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="1f311-203">自適性取樣遙測處理器 (自 2.0.0-beta3 起)</span><span class="sxs-lookup"><span data-stu-id="1f311-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="1f311-204">此選項預設為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="1f311-204">This is enabled by default.</span></span> <span data-ttu-id="1f311-205">如果您的應用程式傳送許多遙測，此處理器會移除其中一些遙測。</span><span class="sxs-lookup"><span data-stu-id="1f311-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="1f311-206">hello 參數提供 hello 演算法的 hello 目標嘗試 tooachieve。</span><span class="sxs-lookup"><span data-stu-id="1f311-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="1f311-207">Hello SDK 可獨立作業，因此如果您的伺服器是叢集的多部電腦，將據此相乘 hello 的遙測資料的實際磁碟區的每個執行個體。</span><span class="sxs-lookup"><span data-stu-id="1f311-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="1f311-208">[深入了解取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="1f311-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="1f311-209">固定取樣遙測處理器 (自 2.0.0-beta1 起)</span><span class="sxs-lookup"><span data-stu-id="1f311-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="1f311-210">還有一種標準的 [取樣遙測處理器](app-insights-api-filtering-sampling.md) (自 2.0.1 起)：</span><span class="sxs-lookup"><span data-stu-id="1f311-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="1f311-211">通道參數 (Java)</span><span class="sxs-lookup"><span data-stu-id="1f311-211">Channel parameters (Java)</span></span>
<span data-ttu-id="1f311-212">這些參數會影響 hello Java SDK 應該如何儲存及排清 hello 它所收集的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="1f311-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="1f311-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="1f311-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="1f311-214">hello hello SDK 的記憶體中儲存體可以儲存的遙測項目數目。</span><span class="sxs-lookup"><span data-stu-id="1f311-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="1f311-215">當到達此數目時，hello 遙測緩衝區排清-也就是 hello 遙測項目會傳送 toohello Application Insights 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1f311-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="1f311-216">最小值：1</span><span class="sxs-lookup"><span data-stu-id="1f311-216">Min: 1</span></span>
* <span data-ttu-id="1f311-217">最大值：1000</span><span class="sxs-lookup"><span data-stu-id="1f311-217">Max: 1000</span></span>
* <span data-ttu-id="1f311-218">預設值：500</span><span class="sxs-lookup"><span data-stu-id="1f311-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="1f311-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="1f311-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="1f311-220">決定多久 hello hello 記憶體中儲存體中儲存的資料應排清 (傳送的 tooApplication Insights)。</span><span class="sxs-lookup"><span data-stu-id="1f311-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="1f311-221">最小值：1</span><span class="sxs-lookup"><span data-stu-id="1f311-221">Min: 1</span></span>
* <span data-ttu-id="1f311-222">最大值：300</span><span class="sxs-lookup"><span data-stu-id="1f311-222">Max: 300</span></span>
* <span data-ttu-id="1f311-223">預設值：5</span><span class="sxs-lookup"><span data-stu-id="1f311-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="1f311-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="1f311-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="1f311-225">決定 hello 以 mb 為單位配置 toohello hello 本機磁碟上的永續性儲存體大小上限。</span><span class="sxs-lookup"><span data-stu-id="1f311-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="1f311-226">這個儲存體用於保存無法傳輸 toobe toohello Application Insights 端點的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="1f311-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="1f311-227">當已符合 hello 儲存體大小時，將會捨棄新的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="1f311-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="1f311-228">最小值：1</span><span class="sxs-lookup"><span data-stu-id="1f311-228">Min: 1</span></span>
* <span data-ttu-id="1f311-229">最大值：100</span><span class="sxs-lookup"><span data-stu-id="1f311-229">Max: 100</span></span>
* <span data-ttu-id="1f311-230">預設值：10</span><span class="sxs-lookup"><span data-stu-id="1f311-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="1f311-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="1f311-231">InstrumentationKey</span></span>
<span data-ttu-id="1f311-232">這會決定您的資料會顯示 hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1f311-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="1f311-233">通常您會針對每個應用程式，用個別的金鑰建立個別資源。</span><span class="sxs-lookup"><span data-stu-id="1f311-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="1f311-234">如果您想 tooset hello 金鑰動態-例如如果您希望 toosend 結果從您的應用程式的 toodifferent 資源-您可以省略 hello 組態檔中的 hello 金鑰並將它設定在程式碼中。</span><span class="sxs-lookup"><span data-stu-id="1f311-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="1f311-235">tooset hello TelemetryClient，包括標準遙測模組的所有執行個體索引鍵在 TelemetryConfiguration.Active 設定 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="1f311-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="1f311-236">請在初始化方法中這麼做，例如 ASP.NET 服務中的 global.aspx.cs：</span><span class="sxs-lookup"><span data-stu-id="1f311-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="1f311-237">如果您只想 toosend 一組特定的事件 tooa 不同的資源，您可以設定特定 TelemetryClient hello 索引鍵：</span><span class="sxs-lookup"><span data-stu-id="1f311-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="1f311-238">新機碼 tooget [hello Application Insights 入口網站中建立新的資源][new]。</span><span class="sxs-lookup"><span data-stu-id="1f311-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f311-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f311-239">Next steps</span></span>
<span data-ttu-id="1f311-240">[深入了解 hello API][api]。</span><span class="sxs-lookup"><span data-stu-id="1f311-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
