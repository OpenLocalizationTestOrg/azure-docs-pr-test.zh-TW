---
title: "aaaDependency Azure Application Insights 追蹤 |Microsoft 文件"
description: "使用 Application Insights 分析內部部署或 Microsoft Azure Web 應用程式的使用情況、可用性和效能。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>設定 Application Insights：追蹤相依性
「相依性」  是由應用程式呼叫的外部元件。 這通常是使用 HTTP 呼叫的服務，或資料庫，或檔案系統。 [Application Insights](app-insights-overview.md) 會測量您應用程式等待相依性所花費的時間，以及相依性呼叫失敗的頻率。 您可以調查特定的呼叫，且兩者產生關聯 toorequests 和例外狀況。

![範例圖表](./media/app-insights-asp-net-dependencies/10-intro.png)

hello 的全新相依性監視目前報告相依性呼叫 toothese 的類型：

* 伺服器
  * SQL DATABASE
  * 使用 HTTP 式繫結的 ASP.NET Web 和 WCF 服務
  * 本機或遠端 HTTP 呼叫
  * Azure Cosmos DB、資料表、Blob 儲存體和佇列
* 網頁
  * AJAX 呼叫

在選取的方法周圍使用[位元組程式碼檢測](https://msdn.microsoft.com/library/z9z62c29.aspx)來監視工作。 效能額外負荷非常小。

您也可以撰寫您自己的 SDK 呼叫 toomonitor 其他相依性，同時在 hello 用戶端和伺服器程式碼中使用 hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)。

## <a name="set-up-dependency-monitoring"></a>設定相依性監視
部分的相依性資訊會自動收集 hello [Application Insights SDK](app-insights-asp-net.md)。 tooget 完整的資料，會安裝適當的代理程式 hello hello 主機伺服器。

| 平台 | Install |
| --- | --- |
| IIS 伺服器 |任一[在伺服器上安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)或[升級您的應用程式 too.NET framework 4.6 或更新版本](http://go.microsoft.com/fwlink/?LinkId=528259)並安裝 hello [Application Insights SDK](app-insights-asp-net.md)應用程式中。 |
| Azure Web 應用程式 |在您 web 應用程式控制台 」 中[開啟 hello Application Insights 刀鋒視窗，在您 web 應用程式的控制台中](app-insights-azure-web-apps.md)並出現提示時選擇安裝。 |
| Azure 雲端服務 |[使用啟動工作](app-insights-cloudservices.md)或[安裝 .NET Framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md) |

## <a name="where-toofind-dependency-data"></a>其中 toofind 相依性資料
* [應用程式對應](#application-map)會以視覺化方式顯示您應用程式與相鄰元件之間的相依性。
* [效能、瀏覽器及失敗刀鋒視窗](#performance-and-blades)會顯示伺服器相依性資料。
* [瀏覽器刀鋒視窗](#ajax-calls)會顯示來自您使用者瀏覽器的 AJAX 呼叫。
* [按一下透過緩慢或失敗的要求從](#diagnose-slow-requests)toocheck 它們的相依性呼叫。
* [分析](#analytics)可以是使用的 tooquery 相依性資料。

## <a name="application-map"></a>應用程式對應
應用程式對應做為您的應用程式的 hello 元件之間的視覺輔助工具 toodiscovering 相依性。 它會自動產生從 hello 從您的應用程式的遙測。 此範例會顯示 hello 瀏覽器的指令碼中的 AJAX 呼叫和伺服器 hello 從 REST 呼叫 tootwo 外部服務時，應用程式。

![應用程式對應](./media/app-insights-asp-net-dependencies/08.png)

* **從 hello 方塊瀏覽**toorelevant 相依性和其他圖表。
* **Pin hello 對應**toohello[儀表板](app-insights-dashboards.md)，其中將完全正常運作。

[深入了解](app-insights-app-map.md)。

## <a name="performance-and-failure-blades"></a>效能和失敗刀鋒視窗
hello 效能刀鋒視窗會顯示 hello hello 伺服器應用程式所做的相依性呼叫持續時間。 其中會顯示摘要圖表和依呼叫劃分的表格。

![效能刀鋒視窗相依性圖表](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

按一下瀏覽 hello 摘要圖表或 hello 資料表項目 toosearch 未經處理的項目這些呼叫。

![相依性呼叫執行個體](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**失敗計數**會顯示在 hello**失敗**刀鋒視窗。 失敗是不是 hello 範圍 200-399 或無法辨識的任何傳回碼。

> [!NOTE]
> **100% 失敗？** - 這可能是指您取得的只是部分相依性資料。 您需要[設定相依性監視適當 tooyour 平台](#set-up-dependency-monitoring)。
>
>

## <a name="ajax-calls"></a>AJAX 呼叫
hello 瀏覽器刀鋒視窗會顯示 hello 持續時間，並從呼叫的 AJAX 失敗率[web 網頁中的 JavaScript](app-insights-javascript.md)。 它們會顯示為「相依性」。

## <a name="diagnosis"></a> 診斷速度緩慢的要求
每個要求的事件與 hello 相依性呼叫相關聯，例外狀況和其他事件時正在處理您的應用程式會根據所追蹤 hello 要求。 因此如果執行一些要求的格式錯誤，您可以了解是否因為 tooslow 回應從相依性。

讓我們逐步解說一個該情況的範例。

### <a name="tracing-from-requests-toodependencies"></a>從要求 toodependencies 追蹤
開啟 hello 效能刀鋒視窗中，然後查看 hello 方格的要求：

![含有平均和計數的要求清單](./media/app-insights-asp-net-dependencies/02-reqs.png)

hello 前一個花費很長的時間。 我們來看看我們可以查明 hello 時間花在哪裡。

按一下該資料列 toosee 個別要求事件：

![要求發生次數的清單](./media/app-insights-asp-net-dependencies/03-instances.png)

按一下任何長時間執行執行個體 tooinspect 進一步，並捲動 toohello 遠端相依性呼叫相關的 toothis 要求：

![尋找呼叫 tooRemote 相依性，請識別不尋常的持續時間](./media/app-insights-asp-net-dependencies/04-dependencies.png)

它看起來像大部分的 hello 時間服務此要求花費在呼叫 tooa 本機服務。

選取該資料列 tooget 的詳細資訊：

![按一下 透過該遠端相依性 tooidentify hello 問題](./media/app-insights-asp-net-dependencies/05-detail.png)

這是其中 hello 問題看起來。 我們已正確指出哪個 hello 問題，所以現在我們只需要 toofind 出為何該呼叫所花這麼久。

### <a name="request-timeline"></a>要求時間軸
在一個不同的案例中，並沒有任何特別長的相依性呼叫。 但藉由切換 toohello 時間表檢視，我們可以看到我們內部處理中發生 hello 延遲的位置：

![尋找呼叫 tooRemote 相依性，請識別不尋常的持續時間](./media/app-insights-asp-net-dependencies/04-1.png)

讓我們看起來應該在我們的程式碼 toosee 原因也就是，那里似乎之後第一個相依性呼叫 hello、 toobe 大的間隙。

### <a name="profile-your-live-site"></a>剖析您的即時網站

其中 hello 次時，就不知道嗎？hello [Application Insights profiler](app-insights-profiler.md)追蹤 HTTP 呼叫 tooyour 即時網站，並顯示在程式碼中的哪一個函式所花費的 hello 最長時間。

## <a name="failed-requests"></a>失敗的要求
失敗的要求也可能失敗的呼叫 toodependencies 相關聯。 同樣地，我們可以按一下 tootrack hello 問題。

![按一下 hello 失敗的要求圖表](./media/app-insights-asp-net-dependencies/06-fail.png)

按一下透過 tooan 出現失敗的要求，並查看其相關聯的事件。

![按一下要求類型，然後按一下 hello 執行個體 tooget tooa 不同檢視的 hello 相同的執行個體，請按一下此 tooget 例外狀況詳細資料。](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Analytics
您可以追蹤 hello 中的相依性[記錄分析查詢語言](https://docs.loganalytics.io/)。 以下是一些範例。

* 尋找任何失敗的相依性呼叫：

```

    dependencies | where success != "True" | take 10
```

* 尋找 AJAX 呼叫︰

```

    dependencies | where client_Type == "Browser" | take 10
```

* 尋找與要求關聯的相依性呼叫：

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* 尋找與頁面檢視關聯的 AJAX 呼叫：

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>自訂相依性追蹤
hello 標準的相依性追蹤模組自動探索外部的相依性，例如資料庫和 REST Api。 但是您可能想要一些額外的元件 toobe 處理 hello 相同的方式。

您可以撰寫程式碼傳送相依性資訊，請使用 hello 相同[TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) hello 標準模組所使用。

比方說，如果您未自行撰寫，您可能有時間所有 hello 呼叫 tooit，您可以建立與組件的程式碼，toofind 出哪些比重它讓 tooyour 回應時間。 Application Insights 中的 hello 相依性圖表中顯示此資料傳送使用 toohave `TrackDependency`。

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

如果您想 tooswitch hello 標準的相依性追蹤模組時，移除在 hello 參考 tooDependencyTrackingTelemetryModule [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)。

## <a name="troubleshooting"></a>疑難排解
*相依性成功旗標一律顯示 true 或 false。*

*SQL 查詢未完整顯示。*

* Hello SDK 升級 toohello 最新版本。 如果您的 .NET 版本低於 4.6：
  * IIS 主機： 安裝[Application Insights 的代理程式](app-insights-monitor-performance-live-website-now.md)hello 主機伺服器上。
  * Azure web 應用程式： 開啟 Application Insights 在 hello web 應用程式控制項面板中，索引標籤，並安裝 Application Insights。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>後續步驟
* [例外狀況](app-insights-asp-net-exceptions.md)
* [使用者和頁面資料](app-insights-javascript.md)
* [Availability](app-insights-monitor-web-app-availability.md)
