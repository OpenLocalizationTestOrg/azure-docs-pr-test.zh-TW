---
title: "Application Insights 中的 aaaPerformance 計數器 |Microsoft 文件"
description: "監視 Application Insights 中的系統和自訂 .NET 效能計數器。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="88a0d-103">Application Insights 中的系統效能計數器</span><span class="sxs-lookup"><span data-stu-id="88a0d-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="88a0d-104">Windows 提供多種[效能計數器](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) (例如 CPU 使用、記憶體、磁碟和網路使用量)。</span><span class="sxs-lookup"><span data-stu-id="88a0d-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="88a0d-105">您也可以自行定義。</span><span class="sxs-lookup"><span data-stu-id="88a0d-105">You can also define your own.</span></span> <span data-ttu-id="88a0d-106">[Application Insights](app-insights-overview.md)可以顯示這些效能計數器，如果您的應用程式在 IIS 上執行內部部署主機或虛擬機器 toowhich 您具有系統管理存取權。</span><span class="sxs-lookup"><span data-stu-id="88a0d-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="88a0d-107">hello 圖表指出 hello 資源可用 tooyour 即時應用程式，並有助於 tooidentify 不平衡的負載，伺服器執行個體之間。</span><span class="sxs-lookup"><span data-stu-id="88a0d-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="88a0d-108">效能計數器會出現在 hello 伺服器刀鋒視窗，其中伺服器執行個體所包含的資料表分割。</span><span class="sxs-lookup"><span data-stu-id="88a0d-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Application Insights 中所報告的效能計數器](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="88a0d-110">(效能計數器不適用於 Azure Web Apps。</span><span class="sxs-lookup"><span data-stu-id="88a0d-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="88a0d-111">不過您也可以[傳送 Azure 診斷 tooApplication Insights](app-insights-azure-diagnostics.md)。)</span><span class="sxs-lookup"><span data-stu-id="88a0d-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="88a0d-112">檢視計數器</span><span class="sxs-lookup"><span data-stu-id="88a0d-112">View counters</span></span>
<span data-ttu-id="88a0d-113">hello 伺服器刀鋒視窗會顯示一組預設的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="88a0d-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="88a0d-114">toosee 其他計數器，編輯 hello 圖表 hello 伺服器刀鋒視窗中，或開啟新[計量瀏覽器](app-insights-metrics-explorer.md)刀鋒視窗並加入新的圖表。</span><span class="sxs-lookup"><span data-stu-id="88a0d-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="88a0d-115">當您編輯圖表 hello 可用的計數器會列為度量。</span><span class="sxs-lookup"><span data-stu-id="88a0d-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Application Insights 中所報告的效能計數器](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="88a0d-117">toosee 在一個地方，所有的實用圖表建立[儀表板](app-insights-dashboards.md)並將其釘選 tooit。</span><span class="sxs-lookup"><span data-stu-id="88a0d-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="88a0d-118">新增計數器</span><span class="sxs-lookup"><span data-stu-id="88a0d-118">Add counters</span></span>
<span data-ttu-id="88a0d-119">如果您想要的 hello 效能計數器不顯示 hello 度量清單，這是因為 hello Application Insights SDK 不收集 web 伺服器中。</span><span class="sxs-lookup"><span data-stu-id="88a0d-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="88a0d-120">您可以設定它 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="88a0d-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="88a0d-121">了解哪些計數器可在您的伺服器在 hello 伺服器使用此 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="88a0d-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="88a0d-122">(請參閱 [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="88a0d-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="88a0d-123">開啟 ApplicationInsights.config。</span><span class="sxs-lookup"><span data-stu-id="88a0d-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="88a0d-124">如果您在開發期間加入 Application Insights tooyour 應用程式，在專案中，編輯 ApplicationInsights.config，然後重新部署 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="88a0d-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="88a0d-125">如果您在執行階段使用狀態監視器 tooinstrument web 應用程式中，尋找 ApplicationInsights.config hello 應用程式在 IIS 中的 hello 根目錄中。</span><span class="sxs-lookup"><span data-stu-id="88a0d-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="88a0d-126">在每個伺服器執行個體中於該處對其進行更新。</span><span class="sxs-lookup"><span data-stu-id="88a0d-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="88a0d-127">編輯 hello 效能收集器指示詞：</span><span class="sxs-lookup"><span data-stu-id="88a0d-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="88a0d-128">您可以擷取標準計數器以及您自行實作的計數器。</span><span class="sxs-lookup"><span data-stu-id="88a0d-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="88a0d-129">`\Objects\Processes` 是所有 Windows 系統上都具有的標準計數器範例。</span><span class="sxs-lookup"><span data-stu-id="88a0d-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="88a0d-130">`\Sales(photo)\# Items Sold` 是可能在 Web 服務中實作的自訂計數器範例。</span><span class="sxs-lookup"><span data-stu-id="88a0d-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="88a0d-131">hello 格式是`\Category(instance)\Counter"`，或沒有執行個體的類別，只`\Category\Counter`。</span><span class="sxs-lookup"><span data-stu-id="88a0d-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="88a0d-132">`ReportAs`計數器名稱不符合需要`[a-zA-Z()/-_ \.]+`-也就是說，它們包含不在 hello 沿用集合中的字元： 字母、 方括號、 斜線、 連字號、 底線、 空間、 圓點。</span><span class="sxs-lookup"><span data-stu-id="88a0d-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="88a0d-133">如果您指定執行個體時，會收集維度"CounterInstanceName"hello 的報告度量。</span><span class="sxs-lookup"><span data-stu-id="88a0d-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="88a0d-134">在程式碼中收集效能計數器</span><span class="sxs-lookup"><span data-stu-id="88a0d-134">Collecting performance counters in code</span></span>
<span data-ttu-id="88a0d-135">toocollect 系統效能計數器，並將它們傳送 tooApplication Insights，您可以調整 hello 以下程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="88a0d-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="88a0d-136">或者，您可以執行 hello 相同工作，並使用您建立自訂的度量：</span><span class="sxs-lookup"><span data-stu-id="88a0d-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="88a0d-137">Analytics 中的效能計數器</span><span class="sxs-lookup"><span data-stu-id="88a0d-137">Performance counters in Analytics</span></span>
<span data-ttu-id="88a0d-138">您可以搜尋並顯示 [Analytics](app-insights-analytics.md) 中的效能計數器報告。</span><span class="sxs-lookup"><span data-stu-id="88a0d-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="88a0d-139">hello **performanceCounters**結構描述會公開 hello `category`，`counter`名稱，和`instance`每個效能計數器的名稱。</span><span class="sxs-lookup"><span data-stu-id="88a0d-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="88a0d-140">在 hello 每個應用程式的遙測，您會看到該應用程式只有 hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="88a0d-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="88a0d-141">例如，toosee 哪些計數器可用：</span><span class="sxs-lookup"><span data-stu-id="88a0d-141">For example, toosee what counters are available:</span></span> 

![Application Insights 分析中的效能計數器](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="88a0d-143">（'Instance' 這裡是指 toohello 效能計數器執行個體，不 hello 角色或伺服器電腦執行個體。</span><span class="sxs-lookup"><span data-stu-id="88a0d-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="88a0d-144">hello 效能計數器執行個體名稱通常區段計數器，例如處理器時間的 hello hello 程序或應用程式的名稱。）</span><span class="sxs-lookup"><span data-stu-id="88a0d-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="88a0d-145">tooget hello 最近期間上的可用記憶體的圖表：</span><span class="sxs-lookup"><span data-stu-id="88a0d-145">tooget a chart of available memory over hello recent period:</span></span> 

![Application Insights 分析中的記憶體時間圖表](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="88a0d-147">類似其他遙測**performanceCounters**也有一個資料行`cloud_RoleInstance`，指出您的應用程式執行所在的 hello 主機伺服器執行個體 hello 識別。</span><span class="sxs-lookup"><span data-stu-id="88a0d-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="88a0d-148">例如，toocompare hello 效能 hello 不同的電腦上的應用程式：</span><span class="sxs-lookup"><span data-stu-id="88a0d-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Application Insights 分析中依角色執行個體分割的效能](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="88a0d-150">ASP.NET 和 Application Insights 計數</span><span class="sxs-lookup"><span data-stu-id="88a0d-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="88a0d-151">*Hello hello 例外狀況率和例外狀況度量之間的差異為何？*</span><span class="sxs-lookup"><span data-stu-id="88a0d-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="88a0d-152"> 是系統效能計數器。</span><span class="sxs-lookup"><span data-stu-id="88a0d-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="88a0d-153">hello CLR 計算所有處理 hello 和未處理例外狀況擲回，並將取樣間隔中的 hello 總計除以 hello hello 間隔長度。</span><span class="sxs-lookup"><span data-stu-id="88a0d-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="88a0d-154">hello Application Insights SDK 會收集此結果，並將它傳送 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="88a0d-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="88a0d-155">*例外狀況*TrackException hello 入口網站中的 hello 圖表 hello 取樣間隔所接收的報告是 hello 的計數。</span><span class="sxs-lookup"><span data-stu-id="88a0d-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="88a0d-156">它包含只 hello 處理例外狀況，您已經撰寫 TrackException 呼叫您的程式碼中，且不包含所有[未處理例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="88a0d-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="88a0d-157">Alerts</span><span class="sxs-lookup"><span data-stu-id="88a0d-157">Alerts</span></span>
<span data-ttu-id="88a0d-158">您可以像其他度量，[設定警示](app-insights-alerts.md)toowarn 您如果效能計數器無法使用外部限制您所指定。</span><span class="sxs-lookup"><span data-stu-id="88a0d-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="88a0d-159">開啟 hello 警示刀鋒視窗，然後按一下 新增警示。</span><span class="sxs-lookup"><span data-stu-id="88a0d-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="88a0d-160"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="88a0d-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="88a0d-161">相依性追蹤</span><span class="sxs-lookup"><span data-stu-id="88a0d-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="88a0d-162">例外狀況追蹤</span><span class="sxs-lookup"><span data-stu-id="88a0d-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

