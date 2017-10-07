---
title: "aaaExplore.NET 追蹤記錄，在 Application Insights"
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
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="aeb7e-103">在 Application Insights 中探索 .NET 追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="aeb7e-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="aeb7e-104">如果您使用 NLog、 log4Net 或 System.Diagnostics.Trace 進行診斷追蹤 ASP.NET 應用程式中，您就可以讓您傳送的記錄[Azure Application Insights][start]，其中您可以瀏覽和搜尋它們。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="aeb7e-105">要與其他 hello 合併您的記錄檔，讓您可以識別即將從您的應用程式的遙測 hello 與每個使用者要求提供服務相關聯的追蹤，並將它們與其他事件和例外狀況報告相互關聯。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="aeb7e-106">您需要 hello 記錄擷取模組嗎？</span><span class="sxs-lookup"><span data-stu-id="aeb7e-106">Do you need hello log capture module?</span></span> <span data-ttu-id="aeb7e-107">對於第三方記錄器來說，它是一個有用的配接器，但是如果您還沒使用 NLog、log4Net 或 System.Diagnostics.Trace，請考慮直接呼叫 [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="aeb7e-108">在您的 app 上安裝記錄</span><span class="sxs-lookup"><span data-stu-id="aeb7e-108">Install logging on your app</span></span>
<span data-ttu-id="aeb7e-109">在專案中安裝您選擇的記錄架構。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="aeb7e-110">這應該會在 app.config 或 web.config 中產生一個項目。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="aeb7e-111">如果您使用 System.Diagnostics.Trace，您會需要 tooadd 項目 tooweb.config:</span><span class="sxs-lookup"><span data-stu-id="aeb7e-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

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
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="aeb7e-112">設定 Application Insights toocollect 記錄檔</span><span class="sxs-lookup"><span data-stu-id="aeb7e-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="aeb7e-113">**[將 Application Insights tooyour 專案](app-insights-asp-net.md)**如果您沒有執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="aeb7e-114">您會看到選項 tooinclude hello 記錄檔收集器。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="aeb7e-115">或者，在 [方案總管] 中以滑鼠右鍵按一下專案，來 **設定 Application Insights** 。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="aeb7e-116">選取 hello 選項太**設定追蹤集合**。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="aeb7e-117">*沒有 Application Insights 功能表或記錄收集器選項嗎？*</span><span class="sxs-lookup"><span data-stu-id="aeb7e-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="aeb7e-118">請嘗試進行[疑難排解](#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="aeb7e-119">手動安裝</span><span class="sxs-lookup"><span data-stu-id="aeb7e-119">Manual installation</span></span>
<span data-ttu-id="aeb7e-120">如果您的專案類型不支援 hello Application Insights 安裝程式 （例如 Windows 桌面專案），請使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="aeb7e-121">如果您計劃 toouse log4Net 或 NLog，請將它安裝在您的專案。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="aeb7e-122">在 [方案總管] 中，以滑鼠右鍵按一下您的專案並選擇 [ **管理 NuGet 封裝**]。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="aeb7e-123">搜尋「Application Insights」</span><span class="sxs-lookup"><span data-stu-id="aeb7e-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="aeb7e-124">選取 hello 適當套件的其中一個：</span><span class="sxs-lookup"><span data-stu-id="aeb7e-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="aeb7e-125">Microsoft.ApplicationInsights.TraceListener （toocapture System.Diagnostics.Trace 呼叫）</span><span class="sxs-lookup"><span data-stu-id="aeb7e-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="aeb7e-126">Microsoft.ApplicationInsights.EventSourceListener （toocapture EventSource 事件）</span><span class="sxs-lookup"><span data-stu-id="aeb7e-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="aeb7e-127">Microsoft.ApplicationInsights.EtwListener （toocapture ETW 事件）</span><span class="sxs-lookup"><span data-stu-id="aeb7e-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="aeb7e-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="aeb7e-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="aeb7e-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="aeb7e-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="aeb7e-130">hello NuGet 封裝會安裝 hello 必要組件，並也會修改 web.config 或 app.config。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="aeb7e-131">插入診斷記錄呼叫</span><span class="sxs-lookup"><span data-stu-id="aeb7e-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="aeb7e-132">如果您使用 System.Diagnostics.Trace，典型的呼叫如下：</span><span class="sxs-lookup"><span data-stu-id="aeb7e-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="aeb7e-133">如果您偏好 log4net 或 NLog：</span><span class="sxs-lookup"><span data-stu-id="aeb7e-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="aeb7e-134">使用 EventSource 事件</span><span class="sxs-lookup"><span data-stu-id="aeb7e-134">Using EventSource events</span></span>
<span data-ttu-id="aeb7e-135">您可以設定[System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)事件傳送 toobe tooApplication 為追蹤的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="aeb7e-136">首先，安裝 hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="aeb7e-137">然後編輯`TelemetryModules`區段 hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)檔案。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="aeb7e-138">每個來源，您可以設定下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="aeb7e-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="aeb7e-139">`Name`指定 hello EventSource toocollect hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="aeb7e-140">`Level`指定記錄層級 toocollect hello。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="aeb7e-141">可以是 `Critical`、`Error`、`Informational`、`LogAlways`、`Verbose`、`Warning` 其中一個。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="aeb7e-142">`Keywords`（選擇性） 指定關鍵字組合 toouse hello 整數的值。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="aeb7e-143">使用 DiagnosticSource 事件</span><span class="sxs-lookup"><span data-stu-id="aeb7e-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="aeb7e-144">您可以設定[System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)事件傳送 toobe tooApplication 為追蹤的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="aeb7e-145">首先，安裝 hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="aeb7e-146">然後編輯 hello`TelemetryModules`區段 hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)檔案。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="aeb7e-147">您要為每個 DiagnosticSource tootrace，加入一個項目以 hello`Name`您 DiagnosticSource toohello 名稱的屬性設定。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="aeb7e-148">使用 ETW 事件</span><span class="sxs-lookup"><span data-stu-id="aeb7e-148">Using ETW events</span></span>
<span data-ttu-id="aeb7e-149">您可以設定 ETW 事件 toobe tooApplication Insights 當做追蹤。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="aeb7e-150">首先，安裝 hello `Microsoft.ApplicationInsights.EtwCollector` NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="aeb7e-151">然後編輯`TelemetryModules`區段 hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)檔案。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="aeb7e-152">如果 hello 處理序主控 hello SDK 執行的 「 效能記錄使用者 」 或系統管理員成員的身分識別，您可以只收集 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="aeb7e-153">每個來源，您可以設定下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="aeb7e-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="aeb7e-154">`ProviderName`這是 hello ETW 提供者 toocollect hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="aeb7e-155">`ProviderGuid`指定 hello 的 hello ETW 提供者 toocollect，GUID 可以使用而不是`ProviderName`。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="aeb7e-156">`Level`設定記錄層級 toocollect hello。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="aeb7e-157">可以是 `Critical`、`Error`、`Informational`、`LogAlways`、`Verbose`、`Warning` 其中一個。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="aeb7e-158">`Keywords`（選擇性） 設定 hello 關鍵字組合 toouse 的整數的值。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="aeb7e-159">直接使用 hello 追蹤應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="aeb7e-159">Using hello Trace API directly</span></span>
<span data-ttu-id="aeb7e-160">您可以直接呼叫 hello Application Insights 追蹤應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="aeb7e-161">hello 記錄配接器會使用此 API。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="aeb7e-162">例如：</span><span class="sxs-lookup"><span data-stu-id="aeb7e-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="aeb7e-163">TrackTrace 的優點是您可以將較長的資料放在 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="aeb7e-164">例如，您可以在該處編碼 POST 資料。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="aeb7e-165">此外，您可以加入嚴重性層級 tooyour 訊息。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="aeb7e-166">與其他遙測，例如，您可以加入您可以使用 toohelp 篩選或搜尋不同的追蹤集合的屬性值。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="aeb7e-167">例如：</span><span class="sxs-lookup"><span data-stu-id="aeb7e-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="aeb7e-168">這可讓您在[搜尋][diagnostic]，tooeasily 篩選出特定嚴重性等級相關 tooa 特定資料庫的所有 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="aeb7e-169">探索記錄</span><span class="sxs-lookup"><span data-stu-id="aeb7e-169">Explore your logs</span></span>
<span data-ttu-id="aeb7e-170">在偵錯模式中執行您的 app 或即時部署它。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="aeb7e-171">在您的應用程式概觀刀鋒視窗中[hello Application Insights 入口網站][portal]，選擇[搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![在 Application Insights 中，選擇 [搜尋]](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![搜尋](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="aeb7e-174">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="aeb7e-174">You can, for example:</span></span>

* <span data-ttu-id="aeb7e-175">篩選記錄追蹤，或具有特定屬性的項目</span><span class="sxs-lookup"><span data-stu-id="aeb7e-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="aeb7e-176">詳細檢查特定項目。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="aeb7e-177">尋找有關 toohello 其他遙測同一個使用者要求 (亦即，與 hello 相同 OperationId)</span><span class="sxs-lookup"><span data-stu-id="aeb7e-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="aeb7e-178">此頁面的 hello 組態儲存為我的最愛</span><span class="sxs-lookup"><span data-stu-id="aeb7e-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="aeb7e-179">**取樣**</span><span class="sxs-lookup"><span data-stu-id="aeb7e-179">**Sampling.**</span></span> <span data-ttu-id="aeb7e-180">如果您的應用程式傳送大量資料，您使用 hello Application Insights SDK 或更新版本的 ASP.NET 版本 2.0.0-beta3 hello 調整取樣功能可能會運作，並傳送您遙測的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="aeb7e-181">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="aeb7e-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aeb7e-182">Next steps</span></span>
<span data-ttu-id="aeb7e-183">[在 ASP.NET 中診斷失敗和例外狀況][exceptions]</span><span class="sxs-lookup"><span data-stu-id="aeb7e-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="aeb7e-184">[深入了解搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="aeb7e-185">疑難排解</span><span class="sxs-lookup"><span data-stu-id="aeb7e-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="aeb7e-186">如果是 Java，我要怎麼做？</span><span class="sxs-lookup"><span data-stu-id="aeb7e-186">How do I do this for Java?</span></span>
<span data-ttu-id="aeb7e-187">使用 hello [Java 記錄配接器](app-insights-java-trace-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="aeb7e-188">沒有 hello 專案操作功能表上的 Application Insights 選項</span><span class="sxs-lookup"><span data-stu-id="aeb7e-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="aeb7e-189">請檢查已在此開發電腦上安裝 Application Insights 工具。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="aeb7e-190">在 Visual Studio 功能表 [工具、擴充功能和更新] 中，尋找 Application Insights 工具。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="aeb7e-191">如果沒有 hello 已安裝 索引標籤中，開啟線上 hello 索引標籤，並安裝它。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="aeb7e-192">這可能是 Application Insights 工具不支援的一種專案類型。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="aeb7e-193">請使用 [手動安裝](#manual-installation)。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="aeb7e-194">Hello 組態工具中沒有記錄配接器選項</span><span class="sxs-lookup"><span data-stu-id="aeb7e-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="aeb7e-195">您首先需要 tooinstall hello 記錄架構。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="aeb7e-196">如果您使用 System.Diagnostics.Trace，請確定您[已在 `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx) 中設定它。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="aeb7e-197">您已有 hello 最新版 Application Insights 嗎？</span><span class="sxs-lookup"><span data-stu-id="aeb7e-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="aeb7e-198">在 Visual Studio**工具**功能表上，選擇**擴充功能和更新**，並開啟 hello**更新** 索引標籤。如果開發人員分析工具已存在，請按一下 tooupdate 它。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="aeb7e-199"><a name="emptykey"></a>我收到「檢測金鑰不能是空白」的錯誤</span><span class="sxs-lookup"><span data-stu-id="aeb7e-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="aeb7e-200">似乎您已安裝而不需要安裝 Application Insights 記錄配接器的 Nuget 套件 hello。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="aeb7e-201">在 [方案總管] 中，以滑鼠右鍵按一下 `ApplicationInsights.config` ，然後選擇 [ **更新 Application Insights**]。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="aeb7e-202">就會顯示一個對話方塊，邀請您 toosign tooAzure 中，然後建立 Application Insights 資源，或重複使用現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="aeb7e-203">這樣應該可以解決。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="aeb7e-204">我可以看見追蹤在診斷搜尋中，但不是 hello 其他事件</span><span class="sxs-lookup"><span data-stu-id="aeb7e-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="aeb7e-205">有時可能需要一些所有 hello 事件和要求 tooget hello 管線。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="aeb7e-206"><a name="limits"></a>保留多少資料？</span><span class="sxs-lookup"><span data-stu-id="aeb7e-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="aeb7e-207">數個因素會影響 hello 保留的資料量。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="aeb7e-208">請參閱 hello[限制](app-insights-api-custom-events-metrics.md#limits)hello 客戶事件如需詳細資訊 度量頁面的區段。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="aeb7e-209">我沒有看到一些預期 hello 記錄項目</span><span class="sxs-lookup"><span data-stu-id="aeb7e-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="aeb7e-210">如果您的應用程式傳送大量資料，您使用 hello Application Insights SDK 或更新版本的 ASP.NET 版本 2.0.0-beta3 hello 調整取樣功能可能會運作，並傳送您遙測的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="aeb7e-211">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="aeb7e-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="aeb7e-212"><a name="add"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="aeb7e-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="aeb7e-213">[設定可用性和回應性測試][availability]</span><span class="sxs-lookup"><span data-stu-id="aeb7e-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="aeb7e-214">[疑難排解][qna]</span><span class="sxs-lookup"><span data-stu-id="aeb7e-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
