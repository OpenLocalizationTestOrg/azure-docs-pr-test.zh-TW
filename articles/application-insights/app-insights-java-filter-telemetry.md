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
# <a name="filter-telemetry-in-your-java-web-app"></a>在 Java Web 應用程式中篩選遙測

篩選條件提供方式 tooselect hello 遙測，您[Java web 應用程式傳送 tooApplication Insights](app-insights-java-get-started.md)。 您可以使用一些現成可用的篩選器，也可以撰寫自己的自訂篩選器。

hello 的方塊出篩選器包括：

* 追蹤嚴重性層級
* 特定 URL、關鍵字或回應碼
* 快速的回應-也就是要求 toowhich 您的應用程式回應 tooquickly
* 特定事件名稱

> [!NOTE]
> 篩選會扭曲應用程式的 hello 度量。 例如，您可能會決定，在訂單 toodiagnose 回應變慢，您將設定篩選 toodiscard 快速的回應時間。 但是，您必須知道 hello Application Insights 所報告的平均回應時間就會低於 hello，則為 true 的速度，並讓的 hello 的要求計數小於 hello 實際計數。
> 如果有此疑慮，請改用[取樣](app-insights-sampling.md)。

## <a name="setting-filters"></a>設定篩選器

在 ApplicationInsights.xml，新增如下面範例所示的 `TelemetryProcessors` 區段：


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




[檢查 hello 組完整的內建處理器](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor)。

## <a name="built-in-filters"></a>內建篩選器

### <a name="metric-telemetry-filter"></a>計量遙測篩選器

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded` - 自訂計量名稱的逗號分隔清單。


### <a name="page-view-telemetry-filter"></a>頁面檢視遙測篩選器

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`持續時間是指 toohello 時間 tooload hello 頁面。 若已設定此屬性，則不會報告載入速度比此時間快的頁面。
* `NotNeededNames` - 頁面名稱的逗號分隔清單。
* `NotNeededUrls` - URL 片段的逗號分隔清單。 例如，`"home"`篩選出具有"home"hello URL 中的所有頁面。


### <a name="request-telemetry-filter"></a>要求遙測篩選器


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>綜合來源篩選器

篩選出 hello SyntheticSource 屬性中有值的所有遙測資料。 這些包括來自 Bot、編目程式和可用性測試的要求。

篩選出所有綜合要求的遙測︰


```XML

           <Processor type="SyntheticSourceFilter" />
```

篩選出特定綜合來源的遙測︰


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded` - 綜合來源名稱的逗號分隔清單。

### <a name="telemetry-event-filter"></a>遙測事件篩選器

篩選自訂事件 (使用 [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) 記錄)。


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames` - 事件名稱的逗號分隔清單。


### <a name="trace-telemetry-filter"></a>追蹤遙測篩選器

篩選記錄檔追蹤 (使用 [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 或[紀錄架構收集器](app-insights-java-trace-logs.md)記錄)。

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* `FromSeverityLevel` 有效值為︰
 *  OFF             - 篩選出所有追蹤
 *  TRACE           - 不篩選。 等於 tooTrace 層級
 *  INFO            - 篩選出 TRACE 層級
 *  WARN            - 篩選出 TRACE 和 INFO
 *  ERROR           - 篩選出 WARN、INFO、TRACE
 *  CRITICAL        - 篩選出 CRITICAL 以外的所有項目


## <a name="custom-filters"></a>自訂篩選器

### <a name="1-code-your-filter"></a>1.撰寫篩選器的程式碼

在您的程式碼中，建立類別來實作 `TelemetryProcessor`:

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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a>2.叫用的篩選器中 hello 設定檔

在 ApplicationInsights.xml 中：

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

## <a name="troubleshooting"></a>疑難排解

我的篩選器無法運作。

* 請檢查您已提供有效的參數值。 例如，持續時間應該是整數。 無效的值將導致 hello 篩選 toobe 忽略。 如果您的自訂篩選器從建構函式或 set 方法擲回例外狀況，該篩選器將被忽略。

## <a name="next-steps"></a>後續步驟

* [取樣](app-insights-sampling.md) - 請考慮以取樣做為替代方式，因為它不會扭曲計量。
