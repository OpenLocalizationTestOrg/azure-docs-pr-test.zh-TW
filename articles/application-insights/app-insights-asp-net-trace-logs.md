---
title: "在 Application Insights 中探索 .NET 追蹤記錄"
description: "搜尋使用 Trace、NLog 或 Log4Net 產生的記錄檔。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="37e5a-103">在 Application Insights 中探索 .NET 追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="37e5a-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="37e5a-104">如果您使用 NLog、log4Net 或 System.Diagnostics.Trace 在 ASP.NET 應用程式中進行診斷追蹤，您可以將記錄傳送至 [Azure Application Insights][start]，以在其中探索和搜尋這些記錄。</span><span class="sxs-lookup"><span data-stu-id="37e5a-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="37e5a-105">您的記錄檔會與來自應用程式的其他遙測合併，讓您可以識別與服務每個使用者要求相關聯的追蹤，並將它們與其他事件和例外狀況報告相互關聯。</span><span class="sxs-lookup"><span data-stu-id="37e5a-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="37e5a-106">您需要記錄擷取模組嗎？</span><span class="sxs-lookup"><span data-stu-id="37e5a-106">Do you need the log capture module?</span></span> <span data-ttu-id="37e5a-107">對於第三方記錄器來說，它是一個有用的配接器，但是如果您還沒使用 NLog、log4Net 或 System.Diagnostics.Trace，請考慮直接呼叫 [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 。</span><span class="sxs-lookup"><span data-stu-id="37e5a-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="37e5a-108">在您的 app 上安裝記錄</span><span class="sxs-lookup"><span data-stu-id="37e5a-108">Install logging on your app</span></span>
<span data-ttu-id="37e5a-109">在專案中安裝您選擇的記錄架構。</span><span class="sxs-lookup"><span data-stu-id="37e5a-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="37e5a-110">這應該會在 app.config 或 web.config 中產生一個項目。</span><span class="sxs-lookup"><span data-stu-id="37e5a-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="37e5a-111">如果您使用 System.Diagnostics.Trace，則必須在 web.config 中加入一個項目：</span><span class="sxs-lookup"><span data-stu-id="37e5a-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="37e5a-112">設定 Application Insights 收集記錄</span><span class="sxs-lookup"><span data-stu-id="37e5a-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="37e5a-113">如果您尚未這麼做，請**[將 Application Insights 新增至您的專案](app-insights-asp-net.md)**。</span><span class="sxs-lookup"><span data-stu-id="37e5a-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="37e5a-114">您將會看見包含記錄收集器的選項。</span><span class="sxs-lookup"><span data-stu-id="37e5a-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="37e5a-115">或者，在 [方案總管] 中以滑鼠右鍵按一下專案，來 **設定 Application Insights** 。</span><span class="sxs-lookup"><span data-stu-id="37e5a-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="37e5a-116">選取此選項以 [設定追蹤集合]。</span><span class="sxs-lookup"><span data-stu-id="37e5a-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="37e5a-117">*沒有 Application Insights 功能表或記錄收集器選項嗎？*</span><span class="sxs-lookup"><span data-stu-id="37e5a-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="37e5a-118">請嘗試進行[疑難排解](#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="37e5a-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="37e5a-119">手動安裝</span><span class="sxs-lookup"><span data-stu-id="37e5a-119">Manual installation</span></span>
<span data-ttu-id="37e5a-120">如果 Application Insights 安裝程式不支援您的專案類型 (例如 Windows 傳統型專案)，請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="37e5a-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="37e5a-121">如果您打算使用 log4Net 或 NLog，請將它安裝在您的專案。</span><span class="sxs-lookup"><span data-stu-id="37e5a-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="37e5a-122">在 [方案總管] 中，以滑鼠右鍵按一下您的專案並選擇 [ **管理 NuGet 封裝**]。</span><span class="sxs-lookup"><span data-stu-id="37e5a-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="37e5a-123">搜尋「Application Insights」</span><span class="sxs-lookup"><span data-stu-id="37e5a-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="37e5a-124">選取適當的套件 - 下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="37e5a-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="37e5a-125">Microsoft.ApplicationInsights.TraceListener (擷取 System.Diagnostics.Trace 呼叫)</span><span class="sxs-lookup"><span data-stu-id="37e5a-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="37e5a-126">Microsoft.ApplicationInsights.EventSourceListener (若為擷取 EventSource 事件)</span><span class="sxs-lookup"><span data-stu-id="37e5a-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="37e5a-127">Microsoft.ApplicationInsights.EtwListener (若為擷取 ETW 事件)</span><span class="sxs-lookup"><span data-stu-id="37e5a-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="37e5a-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="37e5a-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="37e5a-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="37e5a-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="37e5a-130">NuGet 封裝會安裝必要的組件，並修改 web.config 或 app.config。</span><span class="sxs-lookup"><span data-stu-id="37e5a-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="37e5a-131">插入診斷記錄呼叫</span><span class="sxs-lookup"><span data-stu-id="37e5a-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="37e5a-132">如果您使用 System.Diagnostics.Trace，典型的呼叫如下：</span><span class="sxs-lookup"><span data-stu-id="37e5a-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="37e5a-133">如果您偏好 log4net 或 NLog：</span><span class="sxs-lookup"><span data-stu-id="37e5a-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="37e5a-134">使用 EventSource 事件</span><span class="sxs-lookup"><span data-stu-id="37e5a-134">Using EventSource events</span></span>
<span data-ttu-id="37e5a-135">您可以將 [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 設定為要傳送至 Application Insights 作為追蹤的事件。</span><span class="sxs-lookup"><span data-stu-id="37e5a-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="37e5a-136">首先，安裝 `Microsoft.ApplicationInsights.EventSourceListener` NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="37e5a-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="37e5a-137">然後編輯 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 檔案的 `TelemetryModules` 區段。</span><span class="sxs-lookup"><span data-stu-id="37e5a-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="37e5a-138">針對每個來源，您可以設定下列參數︰</span><span class="sxs-lookup"><span data-stu-id="37e5a-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="37e5a-139">`Name` 會指定要收集之 EventSource 的名稱。</span><span class="sxs-lookup"><span data-stu-id="37e5a-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="37e5a-140">`Level` 會指定要收集的記錄等級。</span><span class="sxs-lookup"><span data-stu-id="37e5a-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="37e5a-141">可以是 `Critical`、`Error`、`Informational`、`LogAlways`、`Verbose`、`Warning` 其中一個。</span><span class="sxs-lookup"><span data-stu-id="37e5a-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="37e5a-142">`Keywords` (選擇性) 會指定要使用的關鍵字組合之整數值。</span><span class="sxs-lookup"><span data-stu-id="37e5a-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="37e5a-143">使用 DiagnosticSource 事件</span><span class="sxs-lookup"><span data-stu-id="37e5a-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="37e5a-144">您可以將 [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) 設定為要傳送至 Application Insights 作為追蹤的事件。</span><span class="sxs-lookup"><span data-stu-id="37e5a-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="37e5a-145">首先，安裝 [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="37e5a-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="37e5a-146">然後編輯 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 檔案的 `TelemetryModules` 區段。</span><span class="sxs-lookup"><span data-stu-id="37e5a-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="37e5a-147">針對您想要追蹤的每個 DiagnosticSource，新增項目並將其 `Name` 屬性設定為 DiagnosticSource 的名稱。</span><span class="sxs-lookup"><span data-stu-id="37e5a-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="37e5a-148">使用 ETW 事件</span><span class="sxs-lookup"><span data-stu-id="37e5a-148">Using ETW events</span></span>
<span data-ttu-id="37e5a-149">您可以設定要傳送至 Application Insights 作為追蹤的 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="37e5a-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="37e5a-150">首先，安裝 `Microsoft.ApplicationInsights.EtwCollector` NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="37e5a-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="37e5a-151">然後編輯 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 檔案的 `TelemetryModules` 區段。</span><span class="sxs-lookup"><span data-stu-id="37e5a-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="37e5a-152">僅在裝載 SDK 的處理序是以「效能記錄使用者」或系統管理員成員的身分識別執行時，才可收集 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="37e5a-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="37e5a-153">針對每個來源，您可以設定下列參數︰</span><span class="sxs-lookup"><span data-stu-id="37e5a-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="37e5a-154">`ProviderName` 是要收集之 ETW 提供者的名稱。</span><span class="sxs-lookup"><span data-stu-id="37e5a-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="37e5a-155">`ProviderGuid` 會指定要收集的 ETW 提供者 GUID，並可取代 `ProviderName` 使用之。</span><span class="sxs-lookup"><span data-stu-id="37e5a-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="37e5a-156">`Level` 會設定要收集的記錄等級。</span><span class="sxs-lookup"><span data-stu-id="37e5a-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="37e5a-157">可以是 `Critical`、`Error`、`Informational`、`LogAlways`、`Verbose`、`Warning` 其中一個。</span><span class="sxs-lookup"><span data-stu-id="37e5a-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="37e5a-158">`Keywords` (選擇性) 會設定要使用的關鍵字組合之整數值。</span><span class="sxs-lookup"><span data-stu-id="37e5a-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="37e5a-159">直接使用追蹤 API</span><span class="sxs-lookup"><span data-stu-id="37e5a-159">Using the Trace API directly</span></span>
<span data-ttu-id="37e5a-160">您可以直接呼叫 Application Insights 追蹤 API。</span><span class="sxs-lookup"><span data-stu-id="37e5a-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="37e5a-161">記錄配接器會使用此 API。</span><span class="sxs-lookup"><span data-stu-id="37e5a-161">The logging adapters use this API.</span></span>

<span data-ttu-id="37e5a-162">例如：</span><span class="sxs-lookup"><span data-stu-id="37e5a-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="37e5a-163">TrackTrace 的優點在於您可以將較長的資料放在訊息中。</span><span class="sxs-lookup"><span data-stu-id="37e5a-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="37e5a-164">例如，您可以在該處編碼 POST 資料。</span><span class="sxs-lookup"><span data-stu-id="37e5a-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="37e5a-165">此外，您可以在訊息中新增嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="37e5a-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="37e5a-166">就像其他遙測一樣，您可以新增屬性值以供協助篩選或搜尋不同的追蹤集。</span><span class="sxs-lookup"><span data-stu-id="37e5a-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="37e5a-167">例如：</span><span class="sxs-lookup"><span data-stu-id="37e5a-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="37e5a-168">在[搜尋][diagnostic]中，這可讓您輕鬆地篩選出與特定資料庫相關且具有特定嚴重性層級的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="37e5a-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="37e5a-169">探索記錄</span><span class="sxs-lookup"><span data-stu-id="37e5a-169">Explore your logs</span></span>
<span data-ttu-id="37e5a-170">在偵錯模式中執行您的 app 或即時部署它。</span><span class="sxs-lookup"><span data-stu-id="37e5a-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="37e5a-171">在 [Application Insights 入口網站][portal]中您的應用程式概觀刀鋒視窗，選擇 [搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="37e5a-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![在 Application Insights 中，選擇 [搜尋]](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![搜尋](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="37e5a-174">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="37e5a-174">You can, for example:</span></span>

* <span data-ttu-id="37e5a-175">篩選記錄追蹤，或具有特定屬性的項目</span><span class="sxs-lookup"><span data-stu-id="37e5a-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="37e5a-176">詳細檢查特定項目。</span><span class="sxs-lookup"><span data-stu-id="37e5a-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="37e5a-177">尋找與相同使用者要求相關的其他遙測 (也就是使用相同的 OperationId)</span><span class="sxs-lookup"><span data-stu-id="37e5a-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="37e5a-178">將此頁面的組態儲存為我的最愛</span><span class="sxs-lookup"><span data-stu-id="37e5a-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="37e5a-179">**取樣**</span><span class="sxs-lookup"><span data-stu-id="37e5a-179">**Sampling.**</span></span> <span data-ttu-id="37e5a-180">如果您的應用程式傳送大量資料，且您是使用 Application Insights SDK for ASP.NET 版本 2.0.0-beta3 或更新版本，則調適性取樣功能可能會運作，並只傳送一部分的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="37e5a-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="37e5a-181">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="37e5a-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="37e5a-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37e5a-182">Next steps</span></span>
<span data-ttu-id="37e5a-183">[在 ASP.NET 中診斷失敗和例外狀況][exceptions]</span><span class="sxs-lookup"><span data-stu-id="37e5a-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="37e5a-184">[深入了解搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="37e5a-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="37e5a-185">疑難排解</span><span class="sxs-lookup"><span data-stu-id="37e5a-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="37e5a-186">如果是 Java，我要怎麼做？</span><span class="sxs-lookup"><span data-stu-id="37e5a-186">How do I do this for Java?</span></span>
<span data-ttu-id="37e5a-187">使用 [Java 記錄配接器](app-insights-java-trace-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="37e5a-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="37e5a-188">專案內容功能表上沒有 Application Insights 選項</span><span class="sxs-lookup"><span data-stu-id="37e5a-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="37e5a-189">請檢查已在此開發電腦上安裝 Application Insights 工具。</span><span class="sxs-lookup"><span data-stu-id="37e5a-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="37e5a-190">在 Visual Studio 功能表 [工具、擴充功能和更新] 中，尋找 Application Insights 工具。</span><span class="sxs-lookup"><span data-stu-id="37e5a-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="37e5a-191">如果此工具不在 [已安裝] 索引標籤中，請開啟 [線上] 索引標籤並安裝它。</span><span class="sxs-lookup"><span data-stu-id="37e5a-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="37e5a-192">這可能是 Application Insights 工具不支援的一種專案類型。</span><span class="sxs-lookup"><span data-stu-id="37e5a-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="37e5a-193">請使用 [手動安裝](#manual-installation)。</span><span class="sxs-lookup"><span data-stu-id="37e5a-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="37e5a-194">組態工具中沒有記錄配接器選項</span><span class="sxs-lookup"><span data-stu-id="37e5a-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="37e5a-195">您必須先安裝記錄架構。</span><span class="sxs-lookup"><span data-stu-id="37e5a-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="37e5a-196">如果您使用 System.Diagnostics.Trace，請確定您[已在 `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx) 中設定它。</span><span class="sxs-lookup"><span data-stu-id="37e5a-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="37e5a-197">您已有最新版的 Application Insights 嗎？</span><span class="sxs-lookup"><span data-stu-id="37e5a-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="37e5a-198">在 Visual Studio 的 [工具] 功能表中，選擇 [擴充功能和更新]，然後開啟 [更新] 索引標籤。如果發現開發人員分析工具，請按一下該工具以進行更新。</span><span class="sxs-lookup"><span data-stu-id="37e5a-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="37e5a-199"><a name="emptykey"></a>我收到「檢測金鑰不能是空白」的錯誤</span><span class="sxs-lookup"><span data-stu-id="37e5a-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="37e5a-200">您可能只安裝記錄配接器 Nuget 封裝，但未安裝 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="37e5a-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="37e5a-201">在 [方案總管] 中，以滑鼠右鍵按一下 `ApplicationInsights.config` ，然後選擇 [ **更新 Application Insights**]。</span><span class="sxs-lookup"><span data-stu-id="37e5a-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="37e5a-202">將會出現對話方塊邀請您登入 Azure，並建立 Application Insights 資源或重複使用現有的資源。</span><span class="sxs-lookup"><span data-stu-id="37e5a-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="37e5a-203">這樣應該可以解決。</span><span class="sxs-lookup"><span data-stu-id="37e5a-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="37e5a-204">我可以在診斷搜尋中看見追蹤，但是看不到其他事件</span><span class="sxs-lookup"><span data-stu-id="37e5a-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="37e5a-205">有時候可能需要一段時間，所有事件和要求才會通過管線。</span><span class="sxs-lookup"><span data-stu-id="37e5a-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="37e5a-206"><a name="limits"></a>保留多少資料？</span><span class="sxs-lookup"><span data-stu-id="37e5a-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="37e5a-207">有好幾個因素會影響保留的資料量。</span><span class="sxs-lookup"><span data-stu-id="37e5a-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="37e5a-208">如需更多資訊，請參閱客戶事件計量頁面的 [限制][](app-insights-api-custom-events-metrics.md#limits) 區段。</span><span class="sxs-lookup"><span data-stu-id="37e5a-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="37e5a-209">我沒看到一些預期的記錄項目</span><span class="sxs-lookup"><span data-stu-id="37e5a-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="37e5a-210">如果您的應用程式傳送大量資料，且您是使用 Application Insights SDK for ASP.NET 版本 2.0.0-beta3 或更新版本，則調適性取樣功能可能會運作，並只傳送一部分的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="37e5a-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="37e5a-211">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="37e5a-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="37e5a-212"><a name="add"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="37e5a-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="37e5a-213">[設定可用性和回應性測試][availability]</span><span class="sxs-lookup"><span data-stu-id="37e5a-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="37e5a-214">[疑難排解][qna]</span><span class="sxs-lookup"><span data-stu-id="37e5a-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
