---
title: "aaaHow...中 Azure Application Insights |Microsoft 文件"
description: "Application Insights 中的常見問題集。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>我如何在 Application Insights 中...？
## <a name="get-an-email-when-"></a>... 時收到電子郵件
### <a name="email-if-my-site-goes-down"></a>我的網站當機時寄送電子郵件
設定 [可用性 Web 測試](app-insights-monitor-web-app-availability.md)。

### <a name="email-if-my-site-is-overloaded"></a>我的網站多載時寄送電子郵件
針對 **伺服器回應時間** 設定 [警示](app-insights-alerts.md)。 介於 1 到 2 秒之間的閾值應該會運作。

![](./media/app-insights-how-do-i/030-server.png)

您的 app 也可能會藉由傳回失敗碼顯示資源耗盡的徵兆。 針對 [失敗的要求] 設定警示。

如果您想 tooset 警示上**伺服器例外狀況**，您可能必須 toodo[某些額外的安裝](app-insights-asp-net-exceptions.md)順序 toosee 資料中。

### <a name="email-on-exceptions"></a>傳送電子郵件的例外狀況
1. [設定例外狀況監視](app-insights-asp-net-exceptions.md)
2. [設定警示](app-insights-alerts.md)上 hello 例外狀況計數公制

### <a name="email-on-an-event-in-my-app"></a>我的 app 發生事件時寄送電子郵件
讓我們假設您想要 tooget 電子郵件，當發生特定事件。 Application Insights 並未直接提供此功能，但它可 [在計量超過某個閾值時傳送警示](app-insights-alerts.md)。

您可以針對 [自訂計量](app-insights-api-custom-events-metrics.md#trackmetric)設定警示，而不是自訂事件。 撰寫一些程式碼 tooincrease 度量 hello 事件發生時：

    telemetry.TrackMetric("Alarm", 10);

或：

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

警示有兩種狀態，因為您有 toosend 較低的值時考慮 toohave 結束 hello 警示：

    telemetry.TrackMetric("Alarm", 0.5);

建立圖表中的[度量總管](app-insights-metrics-explorer.md)toosee 您警示：

![](./media/app-insights-how-do-i/010-alarm.png)

Hello 度量在短時間內超過 mid 值時，現在可以設定警示的 toofire:

![](./media/app-insights-how-do-i/020-threshold.png)

設定 hello 平均期間 toohello 最小值。

當 hello 度量超出及低於 hello 臨界值，您會取得電子郵件。

某些點 tooconsider:

* 警示有兩種狀態 (「警示」和「良好」)。 只有當度量資訊會收到，就會評估 hello 狀態。
* Hello 狀態變更時才傳送一封電子郵件。 這就是為什麼有 toosend 高和低值的度量。
* 收到 hello 值製作 tooevaluate hello 警示 hello 平均透過之前期間的 hello。 這發生在每次收到度量時，讓您設定的 hello 期間比更頻繁地傳送電子郵件。
* 因為 「 警示 」 和 「 良好 」，則會傳送電子郵件，您可能想 tooconsider 重新考慮單次事件做為兩個狀態的條件。 比方說，而不是 「 已完成工作 」 事件，會造成 「 工作正在進行中的 」 情況，您從何處取得電子郵件在 hello 開始和結束工作。

### <a name="set-up-alerts-automatically"></a>自動設定警示
[使用 PowerShell toocreate 新警示](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>使用 PowerShell tooManage Application Insights
* [建立新的資源](app-insights-powershell-script-create-resource.md)
* [建立新的警示](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>區分不同版本的遙測

* 應用程式中的多個角色︰使用單一 Application Insights 資源，並依據 cloud_Rolename 進行篩選。 [深入了解](app-insights-monitor-multi-role-apps.md)
* 區分開發、測試和發行版本︰使用不同的 Application Insights 資源。 挑選從 web.config hello 檢測金鑰。[深入了解](app-insights-separate-resources.md)
* 報告組建版本︰使用遙測初始設定式新增屬性。 [深入了解](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>監視後端伺服器與桌面應用程式
[使用 hello Windows Server SDK 模組](app-insights-windows-desktop.md)。

## <a name="visualize-data"></a>顯現資料
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>具有來自多個 App 之計量的儀表板
* 在 [計量總管](app-insights-metrics-explorer.md)中，自訂圖表並將它儲存為我的最愛。 將其釘選 toohello Azure 儀表板。

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>資料來自其他來源和 Application Insights 的儀表板
* [匯出遙測 tooPower BI](app-insights-export-power-bi.md)。

或

* 使用 SharePoint 做為您的儀表板，在 SharePoint web 組件中顯示資料。 [使用連續匯出，以及資料流分析 tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md)。  使用 PowerView tooexamine hello 資料庫，並建立 SharePoint web 組件上執行 powerview。

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>篩選出匿名或已驗證的使用者
如果您的使用者登入，您可以設定 hello[驗證使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)。(它不會自動重新整理)。

接著，您可以：

* 搜尋特定的使用者識別碼

![](./media/app-insights-how-do-i/110-search.png)

* 篩選度量 tooeither 匿名或已驗證使用者

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>修改屬性名稱或值
建立 [篩選器](app-insights-api-filtering-sampling.md#filtering)。 這可讓您修改，或從您的應用程式 tooApplication Insights 傳送之前篩選遙測。

## <a name="list-specific-users-and-their-usage"></a>列出特定使用者和其使用方式
如果您只想太[搜尋特定使用者](#search-specific-users)，您可以設定 hello[驗證使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)。

如果您想要使用者清單以及像是他們查看過哪些頁面或登入頻率等資料，則有兩個選項：

* [設定驗證的使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)， [tooa 資料庫匯出](app-insights-code-sample-export-sql-stream-analytics.md)並使用適當工具 tooanalyze 您使用者資料。
* 如果您有只有少數的使用者，傳送自訂事件或度量，如 hello 公制值或事件名稱，以及設定 hello 使用者識別碼，作為屬性使用 hello 感興趣的資料。 tooanalyze 網頁檢視，來取代 hello 標準 JavaScript trackPageView 呼叫。 tooanalyze 伺服器端遙測，使用遙測初始設定式 tooadd hello 使用者識別碼 tooall 伺服器遙測。 然後您可以篩選與區段的度量和搜尋 hello 使用者識別碼。

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>從我的應用程式 tooApplication Insights 減少流量
* 在[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)，停用不需要任何模組這類 hello 效能計數器收集器。
* 使用[取樣和篩選](app-insights-api-filtering-sampling.md)在 hello SDK。
* 在您的網頁，請回報的每個頁面上檢視的 Ajax 呼叫的 hello 數目限制。 在 hello 指令碼之後的程式碼片段`instrumentationKey:...`，插入： `,maxAjaxCallsPerView:3` （或適當的數字）。
* 如果您使用[TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric)，計算 hello 彙總的度量值的批次傳送嗨結果之前。 有一個 TrackMetric() 的多載是針對該動作所提供。

深入了解 [價格和配額](app-insights-pricing.md)。

## <a name="disable-telemetry"></a>停用遙測
太**動態停止和啟動**hello 收集和傳輸的遙測資料從伺服器 hello:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



太**停用選取的標準收集器**-例如效能計數器、 HTTP 要求，或相依性-刪除或標記為註解中的 hello 相關行[ApplicationInsights.config](app-insights-api-custom-events-metrics.md)。例如，如果您想 toosend TrackRequest 資料，您可以這麼做。

## <a name="view-system-performance-counters"></a>檢視系統效能計數器
您可以在計量瀏覽器中顯示的度量 hello 包括一組系統效能計數器。 有一個預先定義且標題為 **伺服器** 的刀鋒視窗會顯示它們其中幾個。

![開啟 Application Insights 資源並按一下伺服器](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>如果您看不到效能計數器資料
* **IIS 伺服器** 。 [安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)。
* **Azure 網站** - 我們尚未支援效能計數器。 有許多標準的 hello Azure 網站控制台標準的一部分，您可以取得。
* **Unix 伺服器** - [安裝 collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay 更多效能計數器
* 首先，[新增圖表](app-insights-metrics-explorer.md)和 hello 計數器是否在 hello 基本設定，我們提供。
* 如果沒有，[加入 hello hello 效能計數器模組所收集的計數器 toohello 集合](app-insights-performance-counters.md)。
