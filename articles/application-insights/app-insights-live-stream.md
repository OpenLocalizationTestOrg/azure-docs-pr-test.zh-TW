---
title: "利用自訂計量與 Azure Application Insights 中的診斷度量資料流 aaaLive |Microsoft 文件"
description: "透過自訂計量即時監視您的 Web 應用程式，並透過失敗、追蹤和事件的即時摘要診斷問題。"
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>即時計量資料流︰以 1 秒的延遲進行監視與診斷 

探查 hello 訊號核心即時、 在生產環境 web 應用程式的使用中的即時度量資料流[Application Insights](app-insights-overview.md)。 選取和篩選度量和效能計數器 toowatch 即時，沒有任何佔用 tooyour 服務。 檢查失敗要求和例外狀況範例中的堆疊追蹤。 即時計量資料流可搭配[分析工具](app-insights-profiler.md)、[快照集偵錯工具](app-insights-snapshot-debugger.md)和[效能測試](app-insights-monitor-web-app-availability.md#performance-tests)，為您的即時網站提供強大且非侵入性的診斷工具。

您可以使用即時計量資料流：

* 藉由監看效能和失敗計數，在發行修正程式時進行驗證。
* 觀看 hello 影響的測試載入，並診斷問題的即時。 
* 專注於特定的測試工作階段，或選取和篩選您想要 toowatch hello 度量依篩選掉已知的問題。
* 在發生例外狀況時取得其追蹤。
* 使用篩選的實驗 toofind hello 最相關的 Kpi。
* 即時監看任何 Windows 效能計數器。
* 輕鬆地識別的伺服器時發生問題，並篩選所有 hello KPI/即時摘要的 toojust 該伺服器。

[![即時計量資料流影片](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

在內部部署執行的 ASP.NET 應用程式或 hello 雲端目前使用即時度量資料流。 

## <a name="get-started"></a>開始使用

1. 如果您尚未在 ASP.NET Web 應用程式或 [Windows Server 應用程式](app-insights-windows-services.md)中[安裝 Application Insights](app-insights-asp-net.md)，請立即安裝。 
2. **更新 toohello 最新版本**的 hello Application Insights 套件。 在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選擇 [管理 Nuget 套件]。 開啟 hello**更新**索引標籤上，核取**包含發行前版本**，然後選取 所有 hello Microsoft.ApplicationInsights.* 封裝。

    重新部署您的應用程式。

3. 在 hello [Azure 入口網站](https://portal.azure.com)，開啟您的應用程式的 hello Application Insights 資源，並開啟 即時資料流。

4. [安全 hello 控制通道](#secure-the-control-channel)如果您可能會在您的篩選條件中使用機密資料，例如客戶名稱。


![在 hello 概觀刀鋒視窗中，按一下 即時資料流](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>沒有資料？ 請檢查您的伺服器防火牆

檢查 hello[即時度量資料流的傳出連接埠](app-insights-ip-addresses.md#outgoing-ports)hello 防火牆的伺服器中開啟。 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>即時計量資料流與計量瀏覽器和分析有何不同？

| |即時資料流 | 計量瀏覽器和分析 |
|---|---|---|
|延遲|在一秒內顯示資料|在幾分鐘後進行彙總|
|沒有保留|資料保存在正在 hello 圖表上就會被捨棄|[資料會保留 90 天](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|隨選|當您開啟即時計量時會串流處理資料|每當 hello SDK 已安裝並啟用時，傳送資料|
|免費|即時資料流資料免費|主體太[定價](app-insights-pricing.md)
|取樣|傳輸所有選取的計量和計數器。 取樣失敗和堆疊追蹤。 不會套用 TelemetryProcessors。|可能[取樣](app-insights-api-filtering-sampling.md)事件|
|控制通道|篩選控制項訊號傳送 toohello SDK。 建議您[保護這個通道](#secure-channel)。|通訊是單向的 toohello 入口網站|


## <a name="select-and-filter-your-metrics"></a>選取並篩選您的計量

(用於傳統 ASP.NET 應用程式與 hello 最新的 SDK。)

您可以套用任何 Application Insights 遙測的任意的篩選條件，從 hello 入口網站來監視自訂即時的 KPI。 按一下 顯示當您滑鼠移過任何 hello 圖表的 hello 篩選控制項。 下列圖表中的 hello 繪製自訂要求計數 KPI 與 URL 和持續時間屬性的篩選。 驗證您的篩選條件以 hello 資料流預覽區段會顯示符合您指定在任何時間點的時間 hello 準則的遙測的即時摘要。 

![自訂要求 KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

您可以監視與計數不同的值。 hello 選項取決於資料流，這可能是任何 Application Insights 遙測 hello 類型： 要求、 相依性、 例外狀況、 追蹤、 事件或度量。 它可以是您自己的[自訂測量](app-insights-api-custom-events-metrics.md#properties)：

![值選項](./media/app-insights-live-stream/live-stream-valueoptions.png)

此外 tooApplication Insights 遙測，您也可以監視任何 Windows 效能計數器從 hello 資料流選項中選取，並提供 hello hello 效能計數器名稱。

即時計量會在兩個地方進行彙總︰在每一部伺服器上本機進行，以及在所有伺服器上進行。 您可以變更 hello 預設值為 hello 各自的下拉式清單中選取其他選項。

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>範例遙測︰自訂即時診斷事件
根據預設，hello 即時摘要的事件會顯示失敗的要求和相依性呼叫、 例外狀況、 事件和追蹤的範例。 按一下 hello 篩選圖示 toosee hello 套用準則的任何一點的時間。 

![預設的即時摘要](./media/app-insights-live-stream/live-stream-eventsdefault.png)

如同度量，您可以指定 hello Application Insights 遙測型別的任何任意準則 tooany。 在此範例中，我們要選取特定的要求失敗、追蹤及事件。 我們還會選取所有的例外狀況和相依性失敗。

![自訂即時摘要](./media/app-insights-live-stream/live-stream-events.png)

注意： 目前，對於例外狀況訊息為基礎的準則，使用 hello 最外層的例外狀況訊息。 在上述範例中，hello toofilter 出 hello 良性例外狀況的內部例外狀況訊息 (如下所示 hello"<-"分隔符號) 「 hello 用戶端中斷連接。 」 請使用不包含「讀取要求內容時發生錯誤」準則的訊息。

請參閱 hello 詳細 hello 中的項目按一下即時摘要。 您可以暫停 hello 摘要方法是按一下**暫停**或直接向下捲動，或按一下項目。 即時摘要捲動後 toohello 頂端之後, 會繼續，或按一下 hello 計數器的項目時所收集到已暫停。

![取樣的即時失敗](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>依伺服器執行個體篩選

如果您想 toomonitor 特定伺服器角色執行個體，您可以篩選由伺服器。

![取樣的即時失敗](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>SDK 需求
[Application Insights SDK for Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 的 2.4.0-beta2 版或更新版本提供「自訂即時計量串流」。 請記住 tooselect 」 包含發行前版本 」 選項，從 NuGet 套件管理員。

## <a name="secure-hello-control-channel"></a>Hello 控制通道的安全
hello 您指定自訂篩選準則會傳送 hello Application Insights SDK 後 toohello 即時度量元件。 hello 篩選可能包含機密資訊，例如 customerIDs。 您可以進行 hello 通道的安全密碼的 API 金鑰與此外 toohello 檢測金鑰。
### <a name="create-an-api-key"></a>建立 API 金鑰

![建立 API 金鑰](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>新增 API 金鑰 tooConfiguration
在 hello applicationinsights.config 檔案中加入 hello AuthenticationApiKey toohello QuickPulseTelemetryModule:
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
或在程式碼中，將它在 hello QuickPulseTelemetryModule:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

不過，如果您辨識並信任所有 hello 連接的伺服器，您可以嘗試 hello 自訂篩選器，而不驗證 hello 通道。 這個選項有六個月可供使用。 一旦每個新的工作階段或是新的伺服器上線後，就需要此覆寫。

![即時計量驗證選項](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>我們強烈建議您在 hello 篩選準則中輸入 CustomerID 等的潛在的敏感資訊之前，先設定 hello 驗證通道。
>

## <a name="generating-a-performance-test-load"></a>產生效能測試負載

如果您想 toowatch hello 效果，負載的增加，請使用 hello 效能測試刀鋒視窗。 它會模擬來自許多同時使用者的要求。 它可以執行任一個 「 手動測試 」 (ping 測試) 的單一的 URL，或執行[multi-step web 效能測試](app-insights-monitor-web-app-availability.md#multi-step-web-tests)您上傳 （在相同的方式為可用性測試的 hello)。

> [!TIP]
> 建立 hello 效能測試之後，開啟 hello 測試和 hello 即時資料流刀鋒視窗，在個別視窗中。 您可以查看當 hello 佇列效能測試啟動，並且在 hello 的監看即時資料流相同的時間。
>


## <a name="troubleshooting"></a>疑難排解

沒有資料？ 如果您的應用程式是在受保護的網路中︰即時計量串流會使用與其他 Application Insights 遙測不同的 IP 位址。 請確定[這些 IP 位址](app-insights-ip-addresses.md)在您的防火牆中為開啟狀態。



## <a name="next-steps"></a>後續步驟
* [使用 Application Insights 監視使用情況](app-insights-web-track-usage.md)
* [使用診斷搜尋](app-insights-diagnostic-search.md)
* [分析工具](app-insights-profiler.md)
* [快照集偵錯工具](app-insights-snapshot-debugger.md)
