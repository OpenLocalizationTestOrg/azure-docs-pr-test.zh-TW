---
title: "在您的 Java web 應用程式中的 Azure Application Insights 遙測 aaaFilter |Microsoft 文件"
description: "減少遙測流量來篩選掉 hello 事件中，您不需要 toomonitor。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="6a9dd-103">在 Java Web 應用程式中篩選遙測</span><span class="sxs-lookup"><span data-stu-id="6a9dd-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="6a9dd-104">篩選條件提供方式 tooselect hello 遙測，您[Java web 應用程式傳送 tooApplication Insights](app-insights-java-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="6a9dd-105">您可以使用一些現成可用的篩選器，也可以撰寫自己的自訂篩選器。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="6a9dd-106">hello 的方塊出篩選器包括：</span><span class="sxs-lookup"><span data-stu-id="6a9dd-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="6a9dd-107">追蹤嚴重性層級</span><span class="sxs-lookup"><span data-stu-id="6a9dd-107">Trace severity level</span></span>
* <span data-ttu-id="6a9dd-108">特定 URL、關鍵字或回應碼</span><span class="sxs-lookup"><span data-stu-id="6a9dd-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="6a9dd-109">快速的回應-也就是要求 toowhich 您的應用程式回應 tooquickly</span><span class="sxs-lookup"><span data-stu-id="6a9dd-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="6a9dd-110">特定事件名稱</span><span class="sxs-lookup"><span data-stu-id="6a9dd-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="6a9dd-111">篩選會扭曲應用程式的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="6a9dd-112">例如，您可能會決定，在訂單 toodiagnose 回應變慢，您將設定篩選 toodiscard 快速的回應時間。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="6a9dd-113">但是，您必須知道 hello Application Insights 所報告的平均回應時間就會低於 hello，則為 true 的速度，並讓的 hello 的要求計數小於 hello 實際計數。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="6a9dd-114">如果有此疑慮，請改用[取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="6a9dd-115">設定篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-115">Setting filters</span></span>

<span data-ttu-id="6a9dd-116">在 ApplicationInsights.xml，新增如下面範例所示的 `TelemetryProcessors` 區段：</span><span class="sxs-lookup"><span data-stu-id="6a9dd-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want toosee -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="6a9dd-117">[檢查 hello 組完整的內建處理器](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor)。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="6a9dd-118">內建篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="6a9dd-119">計量遙測篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="6a9dd-120">`NotNeeded` - 自訂計量名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="6a9dd-121">頁面檢視遙測篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="6a9dd-122">`DurationThresholdInMS`持續時間是指 toohello 時間 tooload hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="6a9dd-123">若已設定此屬性，則不會報告載入速度比此時間快的頁面。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="6a9dd-124">`NotNeededNames` - 頁面名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="6a9dd-125">`NotNeededUrls` - URL 片段的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="6a9dd-126">例如，`"home"`篩選出具有"home"hello URL 中的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="6a9dd-127">要求遙測篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="6a9dd-128">綜合來源篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-128">Synthetic Source filter</span></span>

<span data-ttu-id="6a9dd-129">篩選出 hello SyntheticSource 屬性中有值的所有遙測資料。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="6a9dd-130">這些包括來自 Bot、編目程式和可用性測試的要求。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="6a9dd-131">篩選出所有綜合要求的遙測︰</span><span class="sxs-lookup"><span data-stu-id="6a9dd-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="6a9dd-132">篩選出特定綜合來源的遙測︰</span><span class="sxs-lookup"><span data-stu-id="6a9dd-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="6a9dd-133">`NotNeeded` - 綜合來源名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="6a9dd-134">遙測事件篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-134">Telemetry Event filter</span></span>

<span data-ttu-id="6a9dd-135">篩選自訂事件 (使用 [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) 記錄)。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="6a9dd-136">`NotNeededNames` - 事件名稱的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="6a9dd-137">追蹤遙測篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-137">Trace Telemetry filter</span></span>

<span data-ttu-id="6a9dd-138">篩選記錄檔追蹤 (使用 [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 或[紀錄架構收集器](app-insights-java-trace-logs.md)記錄)。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="6a9dd-139">`FromSeverityLevel` 有效值為︰</span><span class="sxs-lookup"><span data-stu-id="6a9dd-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="6a9dd-140">OFF             - 篩選出所有追蹤</span><span class="sxs-lookup"><span data-stu-id="6a9dd-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="6a9dd-141">TRACE           - 不篩選。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-141">TRACE           - No filtering.</span></span> <span data-ttu-id="6a9dd-142">等於 tooTrace 層級</span><span class="sxs-lookup"><span data-stu-id="6a9dd-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="6a9dd-143">INFO            - 篩選出 TRACE 層級</span><span class="sxs-lookup"><span data-stu-id="6a9dd-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="6a9dd-144">WARN            - 篩選出 TRACE 和 INFO</span><span class="sxs-lookup"><span data-stu-id="6a9dd-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="6a9dd-145">ERROR           - 篩選出 WARN、INFO、TRACE</span><span class="sxs-lookup"><span data-stu-id="6a9dd-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="6a9dd-146">CRITICAL        - 篩選出 CRITICAL 以外的所有項目</span><span class="sxs-lookup"><span data-stu-id="6a9dd-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="6a9dd-147">自訂篩選器</span><span class="sxs-lookup"><span data-stu-id="6a9dd-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="6a9dd-148">1.撰寫篩選器的程式碼</span><span class="sxs-lookup"><span data-stu-id="6a9dd-148">1. Code your filter</span></span>

<span data-ttu-id="6a9dd-149">在您的程式碼中，建立類別來實作 `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="6a9dd-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="6a9dd-150">2.叫用的篩選器中 hello 設定檔</span><span class="sxs-lookup"><span data-stu-id="6a9dd-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="6a9dd-151">在 ApplicationInsights.xml 中：</span><span class="sxs-lookup"><span data-stu-id="6a9dd-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="6a9dd-152">疑難排解</span><span class="sxs-lookup"><span data-stu-id="6a9dd-152">Troubleshooting</span></span>

<span data-ttu-id="6a9dd-153">我的篩選器無法運作。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="6a9dd-154">請檢查您已提供有效的參數值。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="6a9dd-155">例如，持續時間應該是整數。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-155">For example, durations should be integers.</span></span> <span data-ttu-id="6a9dd-156">無效的值將導致 hello 篩選 toobe 忽略。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="6a9dd-157">如果您的自訂篩選器從建構函式或 set 方法擲回例外狀況，該篩選器將被忽略。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a9dd-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a9dd-158">Next steps</span></span>

* <span data-ttu-id="6a9dd-159">[取樣](app-insights-sampling.md) - 請考慮以取樣做為替代方式，因為它不會扭曲計量。</span><span class="sxs-lookup"><span data-stu-id="6a9dd-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
