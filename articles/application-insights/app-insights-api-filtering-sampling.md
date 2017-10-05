---
title: "在 Application Insights SDK 中篩選及前置處理 | Microsoft Docs"
description: "撰寫 SDK 的遙測處理器和遙測初始設定式來篩選屬性或將屬性新增至資料，再將遙測傳送至 Application Insights 入口網站。"
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="2fd37-103">在 Application Insights SDK 中篩選及前置處理遙測</span><span class="sxs-lookup"><span data-stu-id="2fd37-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="2fd37-104">您可以針對 Application Insights SDK 撰寫與設定外掛程式，以自訂在遙測傳送至 Application Insights 服務之前，擷取與處理它的方式。</span><span class="sxs-lookup"><span data-stu-id="2fd37-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="2fd37-105">[取樣](app-insights-sampling.md) 可減少遙測的量而不會影響統計資料。</span><span class="sxs-lookup"><span data-stu-id="2fd37-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="2fd37-106">它可將相關資料點寶持放在一起，因此您診斷問題時，能夠在資料點之間瀏覽。</span><span class="sxs-lookup"><span data-stu-id="2fd37-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="2fd37-107">在入口網站中將乘以總計數，以補償取樣。</span><span class="sxs-lookup"><span data-stu-id="2fd37-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="2fd37-108">使用 [ASP.NET](#filtering) 或 [Java](app-insights-java-filter-telemetry.md) 適用的遙測處理器進行篩選，可讓您先在 SDK 中選取或修改遙測，再將遙測傳送到伺服器。</span><span class="sxs-lookup"><span data-stu-id="2fd37-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="2fd37-109">例如，您可以從傀儡程式中排除要求來減少遙測量。</span><span class="sxs-lookup"><span data-stu-id="2fd37-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="2fd37-110">但和取樣相比，篩選是減少流量更基本的方法。</span><span class="sxs-lookup"><span data-stu-id="2fd37-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="2fd37-111">它可讓您更充分掌握傳輸內容，但是您必須注意，它會影響統計資料 (例如，若您要篩選所有成功的要求)。</span><span class="sxs-lookup"><span data-stu-id="2fd37-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="2fd37-112">[遙測初始設定式會新增屬性](#add-properties) 至任何從應用程式傳送出來的遙測，包括從標準模組傳送出來的遙測。</span><span class="sxs-lookup"><span data-stu-id="2fd37-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="2fd37-113">例如，您可以新增計算好的值，或是用來在入口網站中篩選資料的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="2fd37-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="2fd37-114">[SDK API](app-insights-api-custom-events-metrics.md) 可用來傳送自訂事件和計量。</span><span class="sxs-lookup"><span data-stu-id="2fd37-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="2fd37-115">開始之前：</span><span class="sxs-lookup"><span data-stu-id="2fd37-115">Before you start:</span></span>

* <span data-ttu-id="2fd37-116">在應用程式中安裝 Application Insights [SDK for ASP.NET](app-insights-asp-net.md) 或 [SDK for Java](app-insights-java-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="2fd37-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="2fd37-117">篩選︰ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="2fd37-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="2fd37-118">這項技術可讓您更直接地控制包含在遙測串流中或排除於遙測串流外的內容。</span><span class="sxs-lookup"><span data-stu-id="2fd37-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="2fd37-119">您可以將它與取樣搭配使用或分開使用。</span><span class="sxs-lookup"><span data-stu-id="2fd37-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="2fd37-120">若要篩選遙測，請撰寫遙測處理器，並將它向 SDK 註冊。</span><span class="sxs-lookup"><span data-stu-id="2fd37-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="2fd37-121">所有遙測都會通過處理器，您可以選擇從串流中卸除或加入屬性。</span><span class="sxs-lookup"><span data-stu-id="2fd37-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="2fd37-122">這包括來自標準模組 (例如 HTTP 要求收集器和相依性收集器) 的遙測，以及您自己撰寫的遙測。</span><span class="sxs-lookup"><span data-stu-id="2fd37-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="2fd37-123">比方說，您可以篩選出有關來自傀儡程式要求或成功的相依性呼叫的遙測。</span><span class="sxs-lookup"><span data-stu-id="2fd37-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="2fd37-124">篩選傳送自使用處理器的 SDK 的遙測可能會曲解您在入口網站中看到的統計資料，並且難以追蹤相關的項目。</span><span class="sxs-lookup"><span data-stu-id="2fd37-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="2fd37-125">請考慮改用 [取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="2fd37-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="2fd37-126">建立遙測處理器 (C#)</span><span class="sxs-lookup"><span data-stu-id="2fd37-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="2fd37-127">確認專案中的 Application Insights SDK 為 2.0.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2fd37-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="2fd37-128">在 Visual Studio 方案總管中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="2fd37-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="2fd37-129">檢查 NuGet 封裝管理員中的 Microsoft.ApplicationInsights.Web。</span><span class="sxs-lookup"><span data-stu-id="2fd37-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="2fd37-130">若要建立篩選器，請實作 ITelemetryProcessor。</span><span class="sxs-lookup"><span data-stu-id="2fd37-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="2fd37-131">這是遙測模組、遙測初始設定式和遙測通道之類的另一個擴充點。</span><span class="sxs-lookup"><span data-stu-id="2fd37-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="2fd37-132">請注意，遙測處理器建構一連串的處理。</span><span class="sxs-lookup"><span data-stu-id="2fd37-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="2fd37-133">當您具現化遙測處理器時，您會傳遞連結至鏈結中的下一個處理器。</span><span class="sxs-lookup"><span data-stu-id="2fd37-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="2fd37-134">遙測資料點傳遞至處理序方法時，它會完成其工作並接著呼叫鏈結中的下一個遙測處理器。</span><span class="sxs-lookup"><span data-stu-id="2fd37-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. <span data-ttu-id="2fd37-135">在 ApplicationInsights.config 中插入：</span><span class="sxs-lookup"><span data-stu-id="2fd37-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="2fd37-136">(這是您用來初始化取樣篩選器的相同區段)。</span><span class="sxs-lookup"><span data-stu-id="2fd37-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="2fd37-137">您可以在類別中提供公開具名屬性，以從 .config 檔案傳遞字串值。</span><span class="sxs-lookup"><span data-stu-id="2fd37-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="2fd37-138">仔細地將 .config 檔案中的類型名稱和任何屬性名稱與程式碼中的類別和屬性名稱做比對。</span><span class="sxs-lookup"><span data-stu-id="2fd37-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="2fd37-139">如果 .config 檔案參考不存在的類型或屬性，SDK 可能無法傳送任何遙測，而且不會產生任何訊息。</span><span class="sxs-lookup"><span data-stu-id="2fd37-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="2fd37-140"> ，您也可以在程式碼中初始化篩選。</span><span class="sxs-lookup"><span data-stu-id="2fd37-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="2fd37-141">在適當的初始化類別中 - 例如在 Global.asax.cs 中的 AppStart - 插入您的處理器至鏈結：</span><span class="sxs-lookup"><span data-stu-id="2fd37-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="2fd37-142">在這個點之後建立的 TelemetryClients 會使用您的處理器。</span><span class="sxs-lookup"><span data-stu-id="2fd37-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="2fd37-143">範例篩選器</span><span class="sxs-lookup"><span data-stu-id="2fd37-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="2fd37-144">綜合要求</span><span class="sxs-lookup"><span data-stu-id="2fd37-144">Synthetic requests</span></span>
<span data-ttu-id="2fd37-145">篩選出 bot 和 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="2fd37-145">Filter out bots and web tests.</span></span> <span data-ttu-id="2fd37-146">雖然計量瀏覽器可讓您篩選出綜合來源，此選項會藉由在 SDK 篩選它們以降低流量。</span><span class="sxs-lookup"><span data-stu-id="2fd37-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="2fd37-147">驗證失敗</span><span class="sxs-lookup"><span data-stu-id="2fd37-147">Failed authentication</span></span>
<span data-ttu-id="2fd37-148">篩選出具有 "401" 回應的要求。</span><span class="sxs-lookup"><span data-stu-id="2fd37-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="2fd37-149">篩選出快速遠端相依性呼叫</span><span class="sxs-lookup"><span data-stu-id="2fd37-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="2fd37-150">如果您只想要診斷速度很慢的呼叫，請篩選出快的項目。</span><span class="sxs-lookup"><span data-stu-id="2fd37-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="2fd37-151">這樣會曲解您在入口網站上看到的統計資料。</span><span class="sxs-lookup"><span data-stu-id="2fd37-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="2fd37-152">相依性圖表將看起來好像相依性呼叫均失敗。</span><span class="sxs-lookup"><span data-stu-id="2fd37-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="2fd37-153">診斷相依性問題</span><span class="sxs-lookup"><span data-stu-id="2fd37-153">Diagnose dependency issues</span></span>
<span data-ttu-id="2fd37-154">[這篇部落格文章](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) 描述可自動傳送定期的 Ping 給相依項目，藉以診斷相依性問題的專案。</span><span class="sxs-lookup"><span data-stu-id="2fd37-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="2fd37-155">新增屬性︰ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="2fd37-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="2fd37-156">使用遙測初始設定式來定義與所有遙測一起傳送的全域屬性；並覆寫選取的標準遙測模組行為。</span><span class="sxs-lookup"><span data-stu-id="2fd37-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="2fd37-157">例如，Web 封裝的 Application Insights 會收集有關 HTTP 要求的遙測。</span><span class="sxs-lookup"><span data-stu-id="2fd37-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="2fd37-158">根據預設，它會將所有含 >= 400 回應碼的要求標記為失敗。</span><span class="sxs-lookup"><span data-stu-id="2fd37-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="2fd37-159">但如果您想將 400 視為成功，您可以提供設定 Success 屬性的遙測初始設定式。</span><span class="sxs-lookup"><span data-stu-id="2fd37-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="2fd37-160">如果您提供遙測初始設定式，會在呼叫任何的 Track*() 方法時呼叫它。</span><span class="sxs-lookup"><span data-stu-id="2fd37-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="2fd37-161">這包括由標準遙測模組呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="2fd37-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="2fd37-162">依照慣例，這些模組不會設定任何已由初始設定式設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="2fd37-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="2fd37-163">**定義您的初始設定式**</span><span class="sxs-lookup"><span data-stu-id="2fd37-163">**Define your initializer**</span></span>

<span data-ttu-id="2fd37-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="2fd37-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="2fd37-165">**載入您的初始設定式**</span><span class="sxs-lookup"><span data-stu-id="2fd37-165">**Load your initializer**</span></span>

<span data-ttu-id="2fd37-166">在 ApplicationInsights.config 中：</span><span class="sxs-lookup"><span data-stu-id="2fd37-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="2fd37-167">*或者* ，您也可以在程式碼 (如 Global.aspx.cs) 中具現化初始設定式：</span><span class="sxs-lookup"><span data-stu-id="2fd37-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="2fd37-168">詳細查看此範例。</span><span class="sxs-lookup"><span data-stu-id="2fd37-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="2fd37-169">JavaScript 遙測初始設定式</span><span class="sxs-lookup"><span data-stu-id="2fd37-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="2fd37-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="2fd37-170">*JavaScript*</span></span>

<span data-ttu-id="2fd37-171">在您從入口網站取得的初始化程式碼之後立即插入遙測初始設定式：</span><span class="sxs-lookup"><span data-stu-id="2fd37-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="2fd37-172">如需 telemetryItem 上可用的非自訂屬性摘要，請參閱 [Application Insights 匯出資料模型](app-insights-export-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="2fd37-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="2fd37-173">您可以依需要加入多個初始設定式。</span><span class="sxs-lookup"><span data-stu-id="2fd37-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="2fd37-174">ITelemetryProcessor 和 ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="2fd37-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="2fd37-175">遙測處理器與遙測初始設定式之間有何差異？</span><span class="sxs-lookup"><span data-stu-id="2fd37-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="2fd37-176">它們的用途有部分重疊︰兩者都可以用來在遙測中新增屬性。</span><span class="sxs-lookup"><span data-stu-id="2fd37-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="2fd37-177">TelemetryInitializers 一律會在 TelemetryProcessors 之前執行。</span><span class="sxs-lookup"><span data-stu-id="2fd37-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="2fd37-178">TelemetryProcessors 可讓您完全取代或捨棄遙測項目。</span><span class="sxs-lookup"><span data-stu-id="2fd37-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="2fd37-179">TelemetryProcessors 不會處理效能計數器遙測。</span><span class="sxs-lookup"><span data-stu-id="2fd37-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="2fd37-180">參考文件</span><span class="sxs-lookup"><span data-stu-id="2fd37-180">Reference docs</span></span>
* [<span data-ttu-id="2fd37-181">API 概觀</span><span class="sxs-lookup"><span data-stu-id="2fd37-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="2fd37-182">ASP.NET 參考</span><span class="sxs-lookup"><span data-stu-id="2fd37-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="2fd37-183">SDK 程式碼</span><span class="sxs-lookup"><span data-stu-id="2fd37-183">SDK Code</span></span>
* [<span data-ttu-id="2fd37-184">ASP.NET 核心 SDK</span><span class="sxs-lookup"><span data-stu-id="2fd37-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="2fd37-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="2fd37-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="2fd37-186">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="2fd37-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="2fd37-187"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="2fd37-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="2fd37-188">搜尋事件和記錄檔</span><span class="sxs-lookup"><span data-stu-id="2fd37-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="2fd37-189">取樣</span><span class="sxs-lookup"><span data-stu-id="2fd37-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="2fd37-190">疑難排解</span><span class="sxs-lookup"><span data-stu-id="2fd37-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
