---
title: "使用 Azure Application Insights 服務 aaaMonitor Node.js |Microsoft 文件"
description: "使用 Application Insights 監視 Node.js 服務的效能和診斷問題。"
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>使用 Application Insights 監視 Node.js 服務和應用程式

[Azure 的 Application Insights](app-insights-overview.md)監視您的後端服務和元件部署 toohelp 之後您[探索並快速地診斷效能和其他問題](app-insights-detect-triage-diagnose.md)。 將它使用於任何地方裝載的 Node.js 服務︰您的資料中心、Azure VM 和 Web Apps，甚至式其他公用雲端。

tooreceive，儲存和瀏覽您的監視資料，請遵循下列指示 tooinclude 代理程式程式碼中的 hello 和對應的 Application Insights 資源，在 Azure 中設定。 hello 代理程式傳送資料更進一步的分析和瀏覽的 toothat 資源。

hello Node.js 代理程式可以自動監視傳入和傳出 HTTP 要求、 數個系統度量，以及例外狀況。 從 v0.20 開始，也可以監視一些常見的第三方套件，例如 `mongodb`、`mysql` 和 `redis`。 所有事件的都相關 tooan 傳入 HTTP 要求相互關聯可加速進行疑難排解。

您可以監視您的應用程式的多個層面和系統是以手動方式進行檢測，讓它們使用下述的 hello 代理程式 API。

![範例效能監視圖表](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>開始使用

讓我們逐步設定應用程式或服務的監視。

### <a name="resource"></a>設定 App Insights 資源

**開始之前**，請確定您有 Azure 訂用帳戶或[免費取得一個新訂用帳戶][azure-free-offer]。 如果您的組織已經有 Azure 訂用帳戶，系統管理員可以依照[這些指示][ add-aad-user] tooadd 您 tooit。

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

現在登入 toohello [Azure 入口網站][ portal]和 hello 下列所示，建立 Application Insights 資源-請按一下 [新增] > [開發人員工具] >"Application Insights"。 hello 資源包含接收遙測資料，這項資料儲存報表和儀表板、 規則和警示的設定和更多的儲存體的端點。

![建立 App Insights 資源](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Hello 資源建立在頁面上，請從 hello 應用程式類型 下拉式清單中選擇 「 Node.js 應用程式 」。 hello 應用程式類型會決定 hello 和預設集的儀表板為您建立的報表。 別擔心，任何 App Insights 資源實際上都可以從任何語言和平台收集資料。

![新增 App Insights 資源表單](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>將 hello Node.js 代理程式設定

現在它是在應用程式中的階段 tooinclude hello 代理程式，讓其收集的資料。
開始複製資源的檢測金鑰 (以下稱為 tooas 您`ikey`) 從 hello 入口網站如下所示。 系統會使用此索引鍵 toomap 資料 tooyour Azure 資源，因此您需要 toospecify App Insights hello 它的環境變數或 hello 代理程式 toouse 您的程式碼中。  

![複製檢測金鑰](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

接下來，將透過 package.json 的 hello Node.js 代理程式程式庫 tooyour 應用程式的相依性。 從您的應用程式的 hello 根資料夾中，執行：

```bash
npm install applicationinsights --save
```

現在您需要 tooexplicitly 負載 hello 程式庫程式碼中。 因為 hello 代理程式會插入到許多其他程式庫的檢測，您應該載入它之前其他盡早`require`陳述式。 tooget 啟動，在您的第一個.js 檔案 hello 最上方加入：

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

hello `setup` hello 檢測金鑰 （和 Azure 資源），方法會設定 toobe 預設用於所有追蹤的項目。 呼叫`start`組態完成的 toobegin 收集及傳送遙測資料之後。

您也可以提供透過 hello 環境變數 APPINSIGHTS ikey\_INSTRUMENTATIONKEY，而不是傳遞它以手動方式太`setup()`或`getClient()`。 這種作法可以讓您將超出認可的原始程式碼 ikeys 和 toospecify 不同 ikeys 不同環境。

其他設定選項如以下述。

您可以嘗試 hello 代理程式，而不傳送遙測設定 hello 檢測金鑰 tooany 是非空白字串。

### <a name="monitor"></a> 監視您的應用程式

hello 代理程式會自動收集有關 hello Node.js 執行階段遙測和某些常見的協力廠商模組。 使用您的應用程式現在 toogenerate 有些資料。

然後，在 hello [Azure 入口網站][ portal]瀏覽您稍早建立的 toohello Application Insights 資源，並尋找您的第一個幾個資料點中 hello 概觀時間表中，如 hello 下列影像所示。 按一下瀏覽 hello 圖表，以取得詳細資料。

![第一個資料點](./media/app-insights-nodejs/12-first-perf.png)

按一下 hello 應用程式對應按鈕 tooview hello 拓樸探索到的應用程式中，如 hello 下列影像所示。 按一下瀏覽元件 hello 對應中的更多詳細資料。

![簡單的應用程式對應](./media/app-insights-nodejs/06-appinsights_appmap.png)

深入了解您的應用程式和疑難排解使用 hello hello"調查 」 一節底下可使用其他檢視。

![調查區段](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>沒有資料？

因為 hello 代理程式批次提交的資料有可能延遲才能 hello 入口網站中顯示的項目。 如果您沒有看到您在資源中的資料嘗試進行的一些 hello 遵循修正：

* 使用 hello 應用程式的其他功能;需要更多動作 toogenerate 更多的遙測。
* 按一下**重新整理**hello 入口網站的資源檢視中。 圖表會自動定期重新整理本身，但立即重新整理會強制此 toohappen。
* 確認[所需的連出連接埠](app-insights-ip-addresses.md)已開啟。
* 開啟 hello[搜尋](app-insights-diagnostic-search.md)磚，然後尋找個別事件。
* 檢查 hello[常見問題集][]。


## <a name="agent-configuration"></a>代理程式組態

以下是 hello 代理程式的設定方法，其預設值。

toofully 交互關聯事件，在服務中，是確定 tooset `.setAutoDependencyCorrelation(true)`。 這可讓 hello 代理程式 tootrack 內容到 Node.js 中的非同步回呼。

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a>代理程式 API

<!-- TODO: Fully document agent API. -->

hello.NET 代理程式 API 的完整說明[這裡](app-insights-api-custom-events-metrics.md)。

您可以追蹤任何要求、 事件、 計量或使用 hello 應用程式 Insights Node.js 用戶端的例外狀況。 hello 下列範例會示範部分 hello 可用的應用程式開發介面。

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a>追蹤相依項目

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a>加入自訂屬性 tooall 事件

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>追蹤 HTTP GET 要求

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>追蹤伺服器啟動時間

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>其他資源

* [監視您 hello 入口網站中的遙測](app-insights-dashboards.md)
* [寫您的遙測的分析查詢](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[常見問題集]: app-insights-troubleshoot-faq.md
