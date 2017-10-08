---
title: "aaaAzure 應用程式 Insights 常見問題集 |Microsoft 文件"
description: "關於 Application Insights 的常見問題集。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights：常見問題集

## <a name="configuration-problems"></a>組態問題
*我在設定下列項目時有問題：*

* [.NET 應用程式](app-insights-asp-net-troubleshoot-no-data.md)
* [監視已在執行的應用程式](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Azure 診斷](app-insights-azure-diagnostics.md)
* [Java Web 應用程式](app-insights-java-troubleshoot.md)

我的伺服器沒有傳回資料

* [設定防火牆例外狀況](app-insights-ip-addresses.md)
* [設定 ASP.NET 伺服器](app-insights-monitor-performance-live-website-now.md)
* [設定 Java 伺服器](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>我是否可以搭配 ... 來使用 Application Insights 嗎？

* [IIS 伺服器 (內部部署或 VM 中) 上的 Web 應用程式](app-insights-asp-net.md)
* [Java Web 應用程式](app-insights-java-get-started.md)
* [Node.js 應用程式](app-insights-nodejs.md)
* [Azure 上的 Web 應用程式](app-insights-azure-web-apps.md)
* [Azure 上的雲端服務](app-insights-cloudservices.md)
* [在 Docker 中執行的應用程式伺服器](app-insights-docker.md)
* [單一頁面 Web 應用程式](app-insights-javascript.md)
* [Sharepoint](app-insights-sharepoint.md)
* [Windows 傳統型應用程式](app-insights-windows-desktop.md)
* [其他平台](app-insights-platforms.md)

## <a name="is-it-free"></a>它是免費的嗎？

是，可作為實驗用途。 在 hello 基本定價計劃，您的應用程式可以傳送特定允許使用資料的每個月免費提供。 hello 免費額度是夠大 toocover 開發和發行應用程式的使用者數少。 您可以從正在處理設定 cap tooprevent 多個指定的資料量。

較大的磁碟區的遙測資料會以 hello Gb 計費。 我們提供一些秘訣太[限制您的費用](app-insights-pricing.md)。

hello 企業計劃會產生每個 web 伺服器節點傳送遙測每一天的費用。 如果您想要在大規模 toouse 連續匯出，就會適用。

[讀取 hello 定價方案](https://azure.microsoft.com/pricing/details/application-insights/)。

## <a name="how-much-is-it-costing"></a>費用是多少？

* 開啟 hello**功能 + 定價**頁面中的 Application Insights 資源。 系統會顯示一張最近使用量的圖表。 您可以視需要設定資料量上限。
* 開啟 hello [Azure 帳單 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview)toosee 帳單所有資源。

## <a name="q14"></a>Application Insights 在我的專案中修改什麼？
hello 詳細資料，取決於 hello 類型的專案。 若是 Web 應用程式：

* 將這些檔案 tooyour 專案：

  * ApplicationInsights.config。
  * ai.js
* 安裝這些 NuGet 套件：

  * *應用程式 Insights API* -hello 核心應用程式開發介面
  * *Web 應用程式的應用程式 Insights API* -使用從伺服器 hello toosend 遙測
  * *JavaScript 應用程式的應用程式 Insights API* -使用 hello 用戶端從 toosend 遙測

    hello 封裝包含這些組件：
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* 將項目插入至：

  * Web.config
  * packages.config
* (新專案只-如果您[加入 Application Insights tooan 現有專案][start]，擁有 toodo 它以手動方式。)程式碼片段插入 hello 用戶端和伺服器程式碼 tooinitialize 其與 hello Application Insights 資源識別碼。 例如，在 MVC 應用程式程式碼插入 hello 主版頁面 Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>如何從舊版 SDK 升級？
請參閱 hello[版本資訊](app-insights-release-notes.md)hello SDK 適當 tooyour 類型的應用程式。

## <a name="update"></a>如何變更我的專案將資料傳送到哪一個 Azure 資源？
在 [方案總管] 中，以滑鼠右鍵按一下 `ApplicationInsights.config` ，然後選擇 [ **更新 Application Insights**]。 您可以在 Azure 中傳送 hello 資料 tooan 現有或新資源。 hello 更新精靈變更 hello ApplicationInsights.config 決定 hello 伺服器 SDK 傳送資料的位置中的檢測金鑰。 除非您取消選取 [更新全部]，它也會變更 hello 金鑰，並出現在您的網頁。

## <a name="what-is-status-monitor"></a>什麼是狀態監視器？

您可以使用您的 IIS web 伺服器 toohelp 中的傳統型應用程式設定 Application Insights web 應用程式中。 它不會收集遙測資料：當您沒有在設定應用程式時，可以將它停止。 

[深入了解](app-insights-monitor-performance-live-website-now.md#questions)。

## <a name="what-telemetry-is-collected-by-application-insights"></a>Application Insights 會收集什麼遙測資料？

從伺服器 Web 應用程式：

* HTTP 要求
* [相依項目](app-insights-asp-net-dependencies.md)。 呼叫： SQL 資料庫;HTTP 呼叫 tooexternal 服務;Azure DB Cosmos、 資料表、 blob 儲存體和佇列。 
* [例外狀況](app-insights-asp-net-exceptions.md)和堆疊追蹤。
* [效能計數器](app-insights-performance-counters.md)-如果您使用[狀態監視器](app-insights-monitor-performance-live-website-now.md)，Azure monitoring(app-insights-azure-web-apps.md) 或 hello [Application Insights collectd 寫入器](app-insights-java-collectd.md)。
* 您以程式碼撰寫的[自訂事件和計量](app-insights-api-custom-events-metrics.md)。
* [追蹤記錄檔](app-insights-asp-net-trace-logs.md)如果您設定 hello 適當收集器。

從[用戶端網頁](app-insights-javascript.md)：

* [頁面檢視計數](app-insights-web-track-usage.md)
* [AJAX 呼叫](app-insights-asp-net-dependencies.md) - 從執行中指令碼發出的要求。
* 頁面檢視載入資料
* 使用者和工作階段計數
* [已驗證的使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)

從其他來源 (如果您設定它們的話)：

* [Azure 診斷](app-insights-azure-diagnostics.md)
* [Docker 容器](app-insights-docker.md)
* [匯入資料表 tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>我是否可以篩選掉或修改某些遙測？

是，在 hello 伺服器，您可以撰寫：

* 遙測處理器 toofilter 或新增屬性 tooselected 遙測項目，再從您的應用程式進行傳送。
* 遙測初始設定式 tooadd 屬性 tooall 項目的遙測資料。

深入了解 [ASP.NET](app-insights-api-filtering-sampling.md) 或 [Java](app-insights-java-filter-telemetry.md)。

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>如何計算城市、國家/地區及其他地理位置的資料？

我們查閱 hello IP 位址 （IPv4 或 IPv6） 的 hello web 用戶端使用[GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/)。

* 瀏覽器遙測： 我們收集 hello 寄件者的 IP 位址。
* 伺服器遙測： hello Application Insights 模組收集 hello 用戶端 IP 位址。 如果已設定 `X-Forwarded-For`，則不會收集該位址。

您可以設定 hello `ClientIpHeaderTelemetryInitializer` tootake hello IP 位址，從不同的標頭。 在某些系統上，例如，它被移 proxy、 負載平衡器或 CDN 太`X-Originating-IP`。 [深入了解](http://apmtips.com/blog/2016/07/05/client-ip-address/)。

您可以[使用 Power BI](app-insights-export-power-bi.md) toodisplay 地圖上您要求的遙測。


## <a name="data"></a>資料保留多久 hello 入口網站中？ 是否安全？
請參閱[資料保留和隱私權][data]。

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>個人識別資訊 (PII) 可以傳送嗨遙測中？

如果您的程式碼會傳送這類資料，就有可能。 如果堆疊追蹤中的變數包含 PII，也可能發生這種情況。 您的開發小組應該會執行風險評定 tooensure 正確處理的 PII。 [深入了解資料保留和隱私權](app-insights-data-retention-privacy.md)。

hello 的 hello 用戶端的 web 位址的最後一個八位元會永遠設 too0 之後擷取 hello 入口網站。

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>在我的網頁原始碼中可以看見我的 iKey。 

* 這在監視解決方案中是常見的做法。
* 它不能使用的 toosteal 您的資料。
* 它可能是使用的 tooskew 資料或觸發程序的警示。
* 我們尚未聽到有任何客戶有這類問題。

您可以：

* 針對用戶端和伺服器資料使用兩個個別的 iKey (個別的 Application Insights 資源)。 或
* 撰寫會在您的伺服器中執行的 proxy，並已透過該 proxy 的資料傳送的 hello web 用戶端。

## <a name="post"></a>如何在診斷搜尋中查看 POST 資料？
我們不會自動記錄張貼資料，但是您可以使用 TrackTrace 呼叫： hello 資料放入 hello 訊息參數。 雖然您無法在其上進行篩選，這會有較長的大小上限超過 hello 限制在 string 屬性上。

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>我應該使用單一還是多個 Application Insights 資源？

針對所有 hello 元件或角色的單一資源使用中的單一商務系統中。 對於開發、測試和發行版本以及獨立的應用程式，則請使用不同的資源。

* [請參閱這裡 hello 討論](app-insights-separate-resources.md)
* [範例 - 具有背景工作角色和 Web 角色的雲端服務](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>如何以動態方式變更 hello 檢測金鑰？

* [這裡的討論](app-insights-separate-resources.md)
* [範例 - 具有背景工作角色和 Web 角色的雲端服務](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>什麼是 hello 使用者與工作階段計數？

* hello JavaScript SDK hello web 用戶端、 tooidentify 傳回使用者和工作階段 cookie toogroup 活動上設定使用者 cookie。
* 如果沒有任何用戶端指令碼，您可以[hello 伺服器端設定 cookie](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/)。
* 如果有一個真實的使用者以不同的瀏覽器使用您的站台，或是使用 InPrivate/Incognito 瀏覽，或透過不同的電腦，則系統會將其計算多次。
* tooidentify 跨機器和瀏覽器中，登入的使用者加入呼叫太[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users)。

## <a name="q17"></a> 我是否已啟用 Application Insights 中的所有項目？
| 您應該會看到 | 如何 tooget 它 | 取得原因 |
| --- | --- | --- |
| 可用性圖表 |[Web 測試](app-insights-monitor-web-app-availability.md) |知道您的 Web 應用程式已啟動 |
| 伺服器應用程式效能：回應時間... |[將 Application Insights tooyour 專案](app-insights-asp-net.md)或[伺服器上安裝 AI 狀態監視器](app-insights-monitor-performance-live-website-now.md)(或撰寫您自己的程式碼太[追蹤相依性](app-insights-api-custom-events-metrics.md#trackdependency)) |偵測效能問題 |
| 相依性遙測 |[在伺服器上安裝 AI 狀態監視器](app-insights-monitor-performance-live-website-now.md) |診斷資料庫或其他外部元件的問題 |
| 取得例外狀況的堆疊追蹤 |[在程式碼中插入 TrackException 呼叫](app-insights-asp-net-exceptions.md) (但部分會自動報告) |偵測並診斷例外狀況 |
| 搜尋記錄追蹤 |[新增記錄配接器](app-insights-asp-net-trace-logs.md) |診斷例外狀況、效能問題 |
| 用戶端使用基本概念：頁面檢視、工作階段... |[網頁中的 JavaScript 初始設定式](app-insights-javascript.md) |流量分析 |
| 用戶端自訂度量 |[追蹤網頁中的呼叫](app-insights-api-custom-events-metrics.md) |增強使用者經驗 |
| 伺服器自訂度量 |[追蹤伺服器中的呼叫](app-insights-api-custom-events-metrics.md) |商業智慧 |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>為何 hello 計算搜尋和度量的圖表中不相等嗎？

[取樣](app-insights-sampling.md)減少 hello 遙測項目數目 （要求、 自訂的事件等等），實際上會從您的應用程式 toohello 入口網站傳送。 在搜尋中，您會看到 hello 實際收到的項目數目。 在度量圖表中顯示的事件計數的您會看到 hello 原始發生的事件數目。 

每個傳輸的項目都帶有一個 `itemCount` 屬性，此屬性會顯示該項目代表的原始事件數目。 tooobserve 取樣作業中，您可以執行此查詢在分析中：

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>自動化

### <a name="configuring-application-insights"></a>設定 Application Insights

您可以[撰寫 PowerShell 指令碼](app-insights-powershell.md)以使用「Azure 資源監視器」來：

* 建立和更新 Application Insights 資源。
* 設定 hello 定價計劃。
* 收到 hello 檢測金鑰。
* 新增計量警示。
* 新增可用性測試。

您無法設定「計量瀏覽器」報告或設定連續匯出。

### <a name="querying-hello-telemetry"></a>查詢 hello 遙測

使用 hello [REST API](https://dev.applicationinsights.io/) toorun[分析](app-insights-analytics.md)查詢。

## <a name="how-can-i-set-an-alert-on-an-event"></a>我要如何在事件上設定警示？

Azure 警示僅針對計量。 請建立一個會在每次事件發生時超出值臨界值的自訂計量。 然後 hello 度量上設定警示。 注意： 您會收到通知，每當 hello 度量超出任一方向; 中的 hello 閾值將不會取得通知之前 hello 第一個交叉，不論它們是否 hello 初始值高或過低。一定會有延遲時間為幾分鐘的時間。

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Azure Web 應用程式與 Application Insights 之間的資料傳輸需要收費嗎？

* 如果您的 Azure Web 應用程式是裝載在具有 Application Insights 集合端點的資料中心內，就不會有費用。 
* 如果您的裝載資料中心內沒有任何集合端點，您應用程式的遙測資料就會產生 [Azure 傳出費用](https://azure.microsoft.com/pricing/details/bandwidth/)。

這並不取決於您 Application Insights 資源的裝載位置。 它只相依於我們端點 hello 分佈。

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>可以傳送遙測 toohello Application Insights 入口網站嗎？

我們建議您使用我們的 Sdk，並使用 hello SDK API (app-insights-api-custom-events-metrics.md)。 有各種 hello SDK 的[平台](app-insights-platforms.md)。 這些 SDK 可處理緩衝、壓縮、節流、重試等。 不過，hello[擷取結構描述](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema)和[端點通訊協定](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md)都是公用的。

## <a name="can-i-monitor-an-intranet-web-server"></a>我是否可以監視內部網路 Web 伺服器？

有兩種方式：

### <a name="firewall-door"></a>防火牆門

可讓您的 web 伺服器 toosend 遙測 tooour 端點 https://dc.services.visualstudio.com:443 和 https://rt.services.visualstudio.com:443。 

### <a name="proxy"></a>Proxy

從您的伺服器 tooa 閘道內部，ApplicationInsights.config 中設定此網路上路由流量：

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

您的閘道路由傳送 hello 流量 toohttps://dc.services.visualstudio.com:443/v2/追蹤

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>我是否可以在內部網路伺服器上執行可用性 Web 測試？

我們[web 測試](app-insights-monitor-web-app-availability.md)出席狀態的分散 hello 地球的點上執行。 有兩個解決方案：

* 防火牆門-允許要求從 tooyour 伺服器[hello 長度和可變清單中的 web 測試代理程式](app-insights-ip-addresses.md)。
* 撰寫您自己的程式碼 toosend 定期要求 tooyour 伺服器從您的內部網路內。 您可以針對這個目的執行 Visual Studio Web 測試。 hello 軟體測試人員可以傳送 hello 結果使用 hello TrackAvailability() API tooApplication 見解。

## <a name="more-answers"></a>更多解答
* [Application Insights 論壇](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
