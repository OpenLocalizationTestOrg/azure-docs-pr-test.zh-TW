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
# <a name="system-performance-counters-in-application-insights"></a>Application Insights 中的系統效能計數器
Windows 提供多種[效能計數器](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) (例如 CPU 使用、記憶體、磁碟和網路使用量)。 您也可以自行定義。 [Application Insights](app-insights-overview.md)可以顯示這些效能計數器，如果您的應用程式在 IIS 上執行內部部署主機或虛擬機器 toowhich 您具有系統管理存取權。 hello 圖表指出 hello 資源可用 tooyour 即時應用程式，並有助於 tooidentify 不平衡的負載，伺服器執行個體之間。

效能計數器會出現在 hello 伺服器刀鋒視窗，其中伺服器執行個體所包含的資料表分割。

![Application Insights 中所報告的效能計數器](./media/app-insights-performance-counters/counters-by-server-instance.png)

(效能計數器不適用於 Azure Web Apps。 不過您也可以[傳送 Azure 診斷 tooApplication Insights](app-insights-azure-diagnostics.md)。)

## <a name="view-counters"></a>檢視計數器
hello 伺服器刀鋒視窗會顯示一組預設的效能計數器。 

toosee 其他計數器，編輯 hello 圖表 hello 伺服器刀鋒視窗中，或開啟新[計量瀏覽器](app-insights-metrics-explorer.md)刀鋒視窗並加入新的圖表。 

當您編輯圖表 hello 可用的計數器會列為度量。

![Application Insights 中所報告的效能計數器](./media/app-insights-performance-counters/choose-performance-counters.png)

toosee 在一個地方，所有的實用圖表建立[儀表板](app-insights-dashboards.md)並將其釘選 tooit。

## <a name="add-counters"></a>新增計數器
如果您想要的 hello 效能計數器不顯示 hello 度量清單，這是因為 hello Application Insights SDK 不收集 web 伺服器中。 您可以設定它 toodo 因此。

1. 了解哪些計數器可在您的伺服器在 hello 伺服器使用此 PowerShell 命令：
   
    `Get-Counter -ListSet *`
   
    (請參閱 [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx)。)
2. 開啟 ApplicationInsights.config。
   
   * 如果您在開發期間加入 Application Insights tooyour 應用程式，在專案中，編輯 ApplicationInsights.config，然後重新部署 tooyour 伺服器。
   * 如果您在執行階段使用狀態監視器 tooinstrument web 應用程式中，尋找 ApplicationInsights.config hello 應用程式在 IIS 中的 hello 根目錄中。 在每個伺服器執行個體中於該處對其進行更新。
3. 編輯 hello 效能收集器指示詞：
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

您可以擷取標準計數器以及您自行實作的計數器。 `\Objects\Processes` 是所有 Windows 系統上都具有的標準計數器範例。 `\Sales(photo)\# Items Sold` 是可能在 Web 服務中實作的自訂計數器範例。 

hello 格式是`\Category(instance)\Counter"`，或沒有執行個體的類別，只`\Category\Counter`。

`ReportAs`計數器名稱不符合需要`[a-zA-Z()/-_ \.]+`-也就是說，它們包含不在 hello 沿用集合中的字元： 字母、 方括號、 斜線、 連字號、 底線、 空間、 圓點。

如果您指定執行個體時，會收集維度"CounterInstanceName"hello 的報告度量。

### <a name="collecting-performance-counters-in-code"></a>在程式碼中收集效能計數器
toocollect 系統效能計數器，並將它們傳送 tooApplication Insights，您可以調整 hello 以下程式碼片段：


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

或者，您可以執行 hello 相同工作，並使用您建立自訂的度量：

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Analytics 中的效能計數器
您可以搜尋並顯示 [Analytics](app-insights-analytics.md) 中的效能計數器報告。

hello **performanceCounters**結構描述會公開 hello `category`，`counter`名稱，和`instance`每個效能計數器的名稱。  在 hello 每個應用程式的遙測，您會看到該應用程式只有 hello 計數器。 例如，toosee 哪些計數器可用： 

![Application Insights 分析中的效能計數器](./media/app-insights-performance-counters/analytics-performance-counters.png)

（'Instance' 這裡是指 toohello 效能計數器執行個體，不 hello 角色或伺服器電腦執行個體。 hello 效能計數器執行個體名稱通常區段計數器，例如處理器時間的 hello hello 程序或應用程式的名稱。）

tooget hello 最近期間上的可用記憶體的圖表： 

![Application Insights 分析中的記憶體時間圖表](./media/app-insights-performance-counters/analytics-available-memory.png)

類似其他遙測**performanceCounters**也有一個資料行`cloud_RoleInstance`，指出您的應用程式執行所在的 hello 主機伺服器執行個體 hello 識別。 例如，toocompare hello 效能 hello 不同的電腦上的應用程式： 

![Application Insights 分析中依角色執行個體分割的效能](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>ASP.NET 和 Application Insights 計數
*Hello hello 例外狀況率和例外狀況度量之間的差異為何？*

*  是系統效能計數器。 hello CLR 計算所有處理 hello 和未處理例外狀況擲回，並將取樣間隔中的 hello 總計除以 hello hello 間隔長度。 hello Application Insights SDK 會收集此結果，並將它傳送 toohello 入口網站。
* *例外狀況*TrackException hello 入口網站中的 hello 圖表 hello 取樣間隔所接收的報告是 hello 的計數。 它包含只 hello 處理例外狀況，您已經撰寫 TrackException 呼叫您的程式碼中，且不包含所有[未處理例外狀況](app-insights-asp-net-exceptions.md)。 

## <a name="alerts"></a>Alerts
您可以像其他度量，[設定警示](app-insights-alerts.md)toowarn 您如果效能計數器無法使用外部限制您所指定。 開啟 hello 警示刀鋒視窗，然後按一下 新增警示。

## <a name="next"></a>接續步驟
* [相依性追蹤](app-insights-asp-net-dependencies.md)
* [例外狀況追蹤](app-insights-asp-net-exceptions.md)

