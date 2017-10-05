---
title: "Application Insights 中的效能計數器 | Microsoft Docs"
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
ms.openlocfilehash: 038d6e051be8112b9264e7efa6485965d11e32c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="1d276-103">Application Insights 中的系統效能計數器</span><span class="sxs-lookup"><span data-stu-id="1d276-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="1d276-104">Windows 提供多種[效能計數器](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) (例如 CPU 使用、記憶體、磁碟和網路使用量)。</span><span class="sxs-lookup"><span data-stu-id="1d276-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="1d276-105">您也可以自行定義。</span><span class="sxs-lookup"><span data-stu-id="1d276-105">You can also define your own.</span></span> <span data-ttu-id="1d276-106">如果應用程式是在您具有系統管理存取權的內部部署主機或虛擬機器上於 IIS 下執行，則 [Application Insights](app-insights-overview.md) 可以顯示這些效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1d276-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="1d276-107">這些圖表指出即時應用程式可用的資源，而且有助於識別伺服器執行個體之間的不平衡負載。</span><span class="sxs-lookup"><span data-stu-id="1d276-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="1d276-108">效能計數器會出現在 [伺服器] 刀鋒視窗中，其包括由伺服器執行個體所分段的資料表。</span><span class="sxs-lookup"><span data-stu-id="1d276-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Application Insights 中所報告的效能計數器](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="1d276-110">(效能計數器不適用於 Azure Web Apps。</span><span class="sxs-lookup"><span data-stu-id="1d276-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="1d276-111">但是，您可以[將 Azure 診斷傳送至 Application Insights](app-insights-azure-diagnostics.md))。</span><span class="sxs-lookup"><span data-stu-id="1d276-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="1d276-112">檢視計數器</span><span class="sxs-lookup"><span data-stu-id="1d276-112">View counters</span></span>
<span data-ttu-id="1d276-113">[伺服器] 刀鋒視窗會顯示一組預設效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1d276-113">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="1d276-114">若要查看其他計數器，請編輯 [伺服器] 刀鋒視窗上的圖表，或開啟新的[計量瀏覽器](app-insights-metrics-explorer.md)刀鋒視窗，並新增新的圖表。</span><span class="sxs-lookup"><span data-stu-id="1d276-114">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="1d276-115">當您編輯圖表時，可用的計數器會列為計量。</span><span class="sxs-lookup"><span data-stu-id="1d276-115">The available counters are listed as metrics when you edit a chart.</span></span>

![Application Insights 中所報告的效能計數器](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="1d276-117">若要在一個地方查看所有最常用的圖表，請建立[儀表板](app-insights-dashboards.md)，並在其中固定這些圖表。</span><span class="sxs-lookup"><span data-stu-id="1d276-117">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="1d276-118">新增計數器</span><span class="sxs-lookup"><span data-stu-id="1d276-118">Add counters</span></span>
<span data-ttu-id="1d276-119">如果您想要的效能計數器未顯示在計量清單中，則原因是 Application Insights SDK 未在 Web 伺服器中收集它。</span><span class="sxs-lookup"><span data-stu-id="1d276-119">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="1d276-120">您可以設定它執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="1d276-120">You can configure it to do so.</span></span>

1. <span data-ttu-id="1d276-121">在伺服器上使用這個 PowerShell 命令，以找出伺服器中可用的計數器：</span><span class="sxs-lookup"><span data-stu-id="1d276-121">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="1d276-122">(請參閱 [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="1d276-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="1d276-123">開啟 ApplicationInsights.config。</span><span class="sxs-lookup"><span data-stu-id="1d276-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="1d276-124">如果您已在開發期間將 Application Insights 新增至應用程式，請編輯專案中的 ApplicationInsights.config，然後將它重新部署至伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d276-124">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="1d276-125">如果您已在執行階段使用狀態監視器檢測 Web 應用程式，請在 IIS 的應用程式根目錄中找到 ApplicationInsights.config。</span><span class="sxs-lookup"><span data-stu-id="1d276-125">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="1d276-126">在每個伺服器執行個體中於該處對其進行更新。</span><span class="sxs-lookup"><span data-stu-id="1d276-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="1d276-127">編輯效能收集器指示詞：</span><span class="sxs-lookup"><span data-stu-id="1d276-127">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="1d276-128">您可以擷取標準計數器以及您自行實作的計數器。</span><span class="sxs-lookup"><span data-stu-id="1d276-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="1d276-129">`\Objects\Processes` 是所有 Windows 系統上都具有的標準計數器範例。</span><span class="sxs-lookup"><span data-stu-id="1d276-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="1d276-130">`\Sales(photo)\# Items Sold` 是可能在 Web 服務中實作的自訂計數器範例。</span><span class="sxs-lookup"><span data-stu-id="1d276-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="1d276-131">格式為 `\Category(instance)\Counter"`，若是沒有執行個體的類別，則為 `\Category\Counter`。</span><span class="sxs-lookup"><span data-stu-id="1d276-131">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="1d276-132">不符合 `[a-zA-Z()/-_ \.]+` 的計數器名稱需要有 `ReportAs`；亦即，它們包含不在下列集合中的字元：字母、圓括號、正斜線、連字號、底線、空格、點。</span><span class="sxs-lookup"><span data-stu-id="1d276-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="1d276-133">如果您指定執行個體，系統會收集它做為報告度量的 "CounterInstanceName" 維度。</span><span class="sxs-lookup"><span data-stu-id="1d276-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="1d276-134">在程式碼中收集效能計數器</span><span class="sxs-lookup"><span data-stu-id="1d276-134">Collecting performance counters in code</span></span>
<span data-ttu-id="1d276-135">若要收集系統效能計數器並將其傳送至 Application Insights，可以採用下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="1d276-135">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="1d276-136">或者，您可以透過您建立的自訂度量執行相同的作業︰</span><span class="sxs-lookup"><span data-stu-id="1d276-136">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="1d276-137">Analytics 中的效能計數器</span><span class="sxs-lookup"><span data-stu-id="1d276-137">Performance counters in Analytics</span></span>
<span data-ttu-id="1d276-138">您可以搜尋並顯示 [Analytics](app-insights-analytics.md) 中的效能計數器報告。</span><span class="sxs-lookup"><span data-stu-id="1d276-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="1d276-139">**PerformanceCounters** 結構描述會公開每個效能計數器的 `category`、`counter` 名稱和 `instance` 名稱。</span><span class="sxs-lookup"><span data-stu-id="1d276-139">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="1d276-140">在每個應用程式的遙測中，您只會看到該應用程式的計數器。</span><span class="sxs-lookup"><span data-stu-id="1d276-140">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="1d276-141">例如，若要查看哪些計數器可用︰</span><span class="sxs-lookup"><span data-stu-id="1d276-141">For example, to see what counters are available:</span></span> 

![Application Insights 分析中的效能計數器](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="1d276-143">(這裡的 'Instance' 指的是效能計數器執行個體，而不是角色或伺服器電腦執行個體。</span><span class="sxs-lookup"><span data-stu-id="1d276-143">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="1d276-144">效能計數器執行個體名稱一般會將計數器分段，例如依處理序或應用程式名稱的處理器時間。)</span><span class="sxs-lookup"><span data-stu-id="1d276-144">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="1d276-145">若要取得可用記憶體在最近一段時間的圖表︰</span><span class="sxs-lookup"><span data-stu-id="1d276-145">To get a chart of available memory over the recent period:</span></span> 

![Application Insights 分析中的記憶體時間圖表](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="1d276-147">與其他遙測一樣，**performanceCounters** 也有 `cloud_RoleInstance` 資料行可指出應用程式執行所在主機伺服器執行個體的身分識別。</span><span class="sxs-lookup"><span data-stu-id="1d276-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="1d276-148">例如，若要比較不同機器上的應用程式效能︰</span><span class="sxs-lookup"><span data-stu-id="1d276-148">For example, to compare the performance of your app on the different machines:</span></span> 

![Application Insights 分析中依角色執行個體分割的效能](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="1d276-150">ASP.NET 和 Application Insights 計數</span><span class="sxs-lookup"><span data-stu-id="1d276-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="1d276-151">*例外狀況率和例外狀況計量之間的差異為何？*</span><span class="sxs-lookup"><span data-stu-id="1d276-151">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="1d276-152"> 是系統效能計數器。</span><span class="sxs-lookup"><span data-stu-id="1d276-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="1d276-153">CLR 會計算所有擲回之已處理和未處理的例外狀況，並依據間隔的長度將總數分割為取樣間隔。</span><span class="sxs-lookup"><span data-stu-id="1d276-153">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="1d276-154">Application Insights SDK 會收集此結果並將它傳送至入口網站。</span><span class="sxs-lookup"><span data-stu-id="1d276-154">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="1d276-155"> 是在圖表的取樣間隔中由入口網站接收之 TrackException 報告的計數。</span><span class="sxs-lookup"><span data-stu-id="1d276-155">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="1d276-156">它只包含您程式碼中撰寫 TrackException 呼叫所在位置的已處理例外狀況，並且不包含所有的 [未處理例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="1d276-156">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="1d276-157">Alerts</span><span class="sxs-lookup"><span data-stu-id="1d276-157">Alerts</span></span>
<span data-ttu-id="1d276-158">與其他計量一樣，您可以[設定警示](app-insights-alerts.md)，在效能計數器超出您指定的界限時提出警告。</span><span class="sxs-lookup"><span data-stu-id="1d276-158">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="1d276-159">開啟 [警示] 刀鋒視窗，然後按一下 [新增警示]。</span><span class="sxs-lookup"><span data-stu-id="1d276-159">Open the Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="1d276-160"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="1d276-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="1d276-161">相依性追蹤</span><span class="sxs-lookup"><span data-stu-id="1d276-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="1d276-162">例外狀況追蹤</span><span class="sxs-lookup"><span data-stu-id="1d276-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

