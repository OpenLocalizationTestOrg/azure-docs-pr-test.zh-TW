---
title: "aaaFiltering 和在前置處理 hello Azure Application Insights SDK |Microsoft 文件"
description: "撰寫 hello SDK toofilter 遙測處理器和遙測初始設定式或屬性 toohello 將資料加入 hello 遙測傳送 toohello Application Insights 入口網站之前。"
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
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>篩選和前置處理 hello Application Insights SDK 中的遙測


您可以撰寫，並設定外掛程式 hello Application Insights SDK toocustomize 遙測如何擷取及處理，才能傳送 toohello Application Insights 服務。

* [取樣](app-insights-sampling.md)減少 hello 的遙測資料的磁碟區，而不會影響您的統計資料。 它可將相關資料點寶持放在一起，因此您診斷問題時，能夠在資料點之間瀏覽。 在 hello 入口網站 hello 的總次數會相乘的 toocompensate hello 取樣。
* 篩選與遙測處理器[asp.net](#filtering)或[Java](app-insights-java-filter-telemetry.md)可讓您選取或修改在 hello SDK 遙測傳送 toohello 伺服器之前。 例如，您無法從 robots 排除要求減少 hello 的遙測資料的磁碟區。 但是，篩選會比取樣還要多的基本方法 tooreducing 流量。 它可讓您更充分掌控傳輸功能，但您有 toobe 注意會影響您的統計資料-例如，如果您篩選出所有成功的要求。
* [遙測初始設定式會將屬性加入](#add-properties)tooany 遙測傳送從您的應用程式，包括從 hello 標準模組的遙測。 例如，您可以加入導出的值。或版本號碼的哪些 toofilter hello hello 入口網站中的資料。
* [hello SDK API](app-insights-api-custom-events-metrics.md)是使用的 toosend 自訂事件和度量。

開始之前：

* 安裝 hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md)或[SDK for Java](app-insights-java-get-started.md)應用程式中。

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>篩選︰ITelemetryProcessor
這項技術可讓您更直接控制哪些是包含或排除 hello 遙測資料流。 您可以將它與取樣搭配使用或分開使用。

toofilter 遙測寫入遙測處理器並向 hello SDK。 所有的遙測資料會經過您的處理器，而且您可以選擇 toodrop hello 從串流處理，或加入其他屬性。 這包括從 hello HTTP 要求收集器與 hello 相依性的收集器，例如 hello 標準模組的遙測及撰寫您自己的遙測。 比方說，您可以篩選出有關來自傀儡程式要求或成功的相依性呼叫的遙測。

> [!WARNING]
> 篩選從 hello SDK 傳送嗨遙測使用處理器可能會扭曲 hello 統計資料在 hello 入口網站，請參閱，使其難以 toofollow 相關項目。
>
> 請考慮改用 [取樣](app-insights-sampling.md)。
>
>

### <a name="create-a-telemetry-processor-c"></a>建立遙測處理器 (C#)
1. 請確認您的專案中的 hello Application Insights SDK 2.0.0 版或更新版本。 在 Visual Studio 方案總管中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 封裝]。 檢查 NuGet 封裝管理員中的 Microsoft.ApplicationInsights.Web。
2. toocreate 篩選器，實作 ITelemetryProcessor。 這是遙測模組、遙測初始設定式和遙測通道之類的另一個擴充點。

    請注意，遙測處理器建構一連串的處理。 當您具現化遙測處理器時，您要傳入 hello 鏈結連結 toohello 下一個處理器。 遙測資料點傳遞 toohello Process 方法時，其功能，然後呼叫 hello hello 鏈結中的下一個遙測處理器。

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
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
1. 在 ApplicationInsights.config 中插入：

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(這是 hello 您用來初始化取樣篩選器的相同區段。)

您可以將字串值傳遞從 hello.config 檔案，藉由提供您的類別中的公用具名的屬性。

> [!WARNING]
> 請小心 toomatch hello 型別名稱和任何 hello.config 檔案 toohello 類別中的屬性名稱和 hello 程式碼中的屬性名稱。 如果 hello.config 檔案參考不存在類型或屬性，hello SDK 可能會以無訊息模式失敗 toosend 任何遙測。
>
>

**或者，**可以初始化程式碼中的 hello 篩選。 適合初始化類別-例如中 Global.asax.cs AppStart-中插入 hello 鏈結中的處理器：

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

在這個點之後建立的 TelemetryClients 會使用您的處理器。

### <a name="example-filters"></a>範例篩選器
#### <a name="synthetic-requests"></a>綜合要求
篩選出 bot 和 Web 測試。 雖然計量瀏覽器提供 hello 選項 toofilter 綜合來源時，此選項可減少流量在 hello SDK 篩選它們。

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>驗證失敗
篩選出具有 "401" 回應的要求。

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>篩選出快速遠端相依性呼叫
如果您只想 toodiagnose 很慢的呼叫，篩選出 hello 快速的。

> [!NOTE]
> 這會扭曲 hello 統計資料，您會看到 hello 入口網站。 如同 hello 相依性呼叫是所有失敗，則會尋找 hello 相依性圖表。
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

#### <a name="diagnose-dependency-issues"></a>診斷相依性問題
[這篇部落格](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/)自動傳送定期 ping toodependencies 描述專案 toodiagnose 相依性問題。


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>新增屬性︰ITelemetryInitializer
使用遙測初始設定式 toodefine 全域屬性所傳送的所有遙測資料。而且 toooverride 選取 hello 標準遙測模組的行為。

比方說，hello Application Insights Web 封裝會收集有關 HTTP 要求的遙測。 根據預設，它會將所有含 >= 400 回應碼的要求標記為失敗。 但是，如果您想 tootreat 400 為成功，您可以提供設定 hello 成功屬性的遙測初始設定式。

如果您提供的遙測初始設定式，它就稱為每當任何 hello Track*() 方法呼叫。 這包括 hello 標準遙測模組所呼叫的方法。 依照慣例，這些模組不會設定任何已由初始設定式設定的屬性。

**定義您的初始設定式**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
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
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**載入您的初始設定式**

在 ApplicationInsights.config 中：

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*或者，* hello 初始設定式中程式碼，例如 Global.aspx.cs 具現化：

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[詳細查看此範例。](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>JavaScript 遙測初始設定式
*JavaScript*

遙測初始設定式插入您從 hello 網站取得的 hello 初始化程式碼之後：

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

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Hello telemetryItem 上所提供的 hello 非自訂屬性中的摘要，請參閱[應用程式 Insights 匯出資料模型](app-insights-export-data-model.md)。

您可以依需要加入多個初始設定式。

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor 和 ITelemetryInitializer
Hello 遙測處理器與遙測初始設定式之間的差異為何？

* 有一些重疊與其可執行的動作： 兩者都可以是使用的 tooadd 屬性 tootelemetry。
* TelemetryInitializers 一律會在 TelemetryProcessors 之前執行。
* TelemetryProcessors 允許您 toocompletely 取代或捨棄遙測項目。
* TelemetryProcessors 不會處理效能計數器遙測。


## <a name="reference-docs"></a>參考文件
* [API 概觀](app-insights-api-custom-events-metrics.md)
* [ASP.NET 參考](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>SDK 程式碼
* [ASP.NET 核心 SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>接續步驟
* [搜尋事件和記錄檔](app-insights-diagnostic-search.md)
* [取樣](app-insights-sampling.md)
* [疑難排解](app-insights-troubleshoot-faq.md)
