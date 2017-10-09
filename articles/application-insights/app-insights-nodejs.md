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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="389e0-103">使用 Application Insights 監視 Node.js 服務和應用程式</span><span class="sxs-lookup"><span data-stu-id="389e0-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="389e0-104">[Azure 的 Application Insights](app-insights-overview.md)監視您的後端服務和元件部署 toohelp 之後您[探索並快速地診斷效能和其他問題](app-insights-detect-triage-diagnose.md)。</span><span class="sxs-lookup"><span data-stu-id="389e0-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="389e0-105">將它使用於任何地方裝載的 Node.js 服務︰您的資料中心、Azure VM 和 Web Apps，甚至式其他公用雲端。</span><span class="sxs-lookup"><span data-stu-id="389e0-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="389e0-106">tooreceive，儲存和瀏覽您的監視資料，請遵循下列指示 tooinclude 代理程式程式碼中的 hello 和對應的 Application Insights 資源，在 Azure 中設定。</span><span class="sxs-lookup"><span data-stu-id="389e0-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="389e0-107">hello 代理程式傳送資料更進一步的分析和瀏覽的 toothat 資源。</span><span class="sxs-lookup"><span data-stu-id="389e0-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="389e0-108">hello Node.js 代理程式可以自動監視傳入和傳出 HTTP 要求、 數個系統度量，以及例外狀況。</span><span class="sxs-lookup"><span data-stu-id="389e0-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="389e0-109">從 v0.20 開始，也可以監視一些常見的第三方套件，例如 `mongodb`、`mysql` 和 `redis`。</span><span class="sxs-lookup"><span data-stu-id="389e0-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="389e0-110">所有事件的都相關 tooan 傳入 HTTP 要求相互關聯可加速進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="389e0-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="389e0-111">您可以監視您的應用程式的多個層面和系統是以手動方式進行檢測，讓它們使用下述的 hello 代理程式 API。</span><span class="sxs-lookup"><span data-stu-id="389e0-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![範例效能監視圖表](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="389e0-113">開始使用</span><span class="sxs-lookup"><span data-stu-id="389e0-113">Getting Started</span></span>

<span data-ttu-id="389e0-114">讓我們逐步設定應用程式或服務的監視。</span><span class="sxs-lookup"><span data-stu-id="389e0-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="389e0-115"><a name="resource"></a>設定 App Insights 資源</span><span class="sxs-lookup"><span data-stu-id="389e0-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="389e0-116">**開始之前**，請確定您有 Azure 訂用帳戶或[免費取得一個新訂用帳戶][azure-free-offer]。</span><span class="sxs-lookup"><span data-stu-id="389e0-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="389e0-117">如果您的組織已經有 Azure 訂用帳戶，系統管理員可以依照[這些指示][ add-aad-user] tooadd 您 tooit。</span><span class="sxs-lookup"><span data-stu-id="389e0-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="389e0-118">現在登入 toohello [Azure 入口網站][ portal]和 hello 下列所示，建立 Application Insights 資源-請按一下 [新增] > [開發人員工具] >"Application Insights"。</span><span class="sxs-lookup"><span data-stu-id="389e0-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="389e0-119">hello 資源包含接收遙測資料，這項資料儲存報表和儀表板、 規則和警示的設定和更多的儲存體的端點。</span><span class="sxs-lookup"><span data-stu-id="389e0-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![建立 App Insights 資源](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="389e0-121">Hello 資源建立在頁面上，請從 hello 應用程式類型 下拉式清單中選擇 「 Node.js 應用程式 」。</span><span class="sxs-lookup"><span data-stu-id="389e0-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="389e0-122">hello 應用程式類型會決定 hello 和預設集的儀表板為您建立的報表。</span><span class="sxs-lookup"><span data-stu-id="389e0-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="389e0-123">別擔心，任何 App Insights 資源實際上都可以從任何語言和平台收集資料。</span><span class="sxs-lookup"><span data-stu-id="389e0-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![新增 App Insights 資源表單](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="389e0-125"><a name="agent"></a>將 hello Node.js 代理程式設定</span><span class="sxs-lookup"><span data-stu-id="389e0-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="389e0-126">現在它是在應用程式中的階段 tooinclude hello 代理程式，讓其收集的資料。</span><span class="sxs-lookup"><span data-stu-id="389e0-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="389e0-127">開始複製資源的檢測金鑰 (以下稱為 tooas 您`ikey`) 從 hello 入口網站如下所示。</span><span class="sxs-lookup"><span data-stu-id="389e0-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="389e0-128">系統會使用此索引鍵 toomap 資料 tooyour Azure 資源，因此您需要 toospecify App Insights hello 它的環境變數或 hello 代理程式 toouse 您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="389e0-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![複製檢測金鑰](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="389e0-130">接下來，將透過 package.json 的 hello Node.js 代理程式程式庫 tooyour 應用程式的相依性。</span><span class="sxs-lookup"><span data-stu-id="389e0-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="389e0-131">從您的應用程式的 hello 根資料夾中，執行：</span><span class="sxs-lookup"><span data-stu-id="389e0-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="389e0-132">現在您需要 tooexplicitly 負載 hello 程式庫程式碼中。</span><span class="sxs-lookup"><span data-stu-id="389e0-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="389e0-133">因為 hello 代理程式會插入到許多其他程式庫的檢測，您應該載入它之前其他盡早`require`陳述式。</span><span class="sxs-lookup"><span data-stu-id="389e0-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="389e0-134">tooget 啟動，在您的第一個.js 檔案 hello 最上方加入：</span><span class="sxs-lookup"><span data-stu-id="389e0-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="389e0-135">hello `setup` hello 檢測金鑰 （和 Azure 資源），方法會設定 toobe 預設用於所有追蹤的項目。</span><span class="sxs-lookup"><span data-stu-id="389e0-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="389e0-136">呼叫`start`組態完成的 toobegin 收集及傳送遙測資料之後。</span><span class="sxs-lookup"><span data-stu-id="389e0-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="389e0-137">您也可以提供透過 hello 環境變數 APPINSIGHTS ikey\_INSTRUMENTATIONKEY，而不是傳遞它以手動方式太`setup()`或`getClient()`。</span><span class="sxs-lookup"><span data-stu-id="389e0-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="389e0-138">這種作法可以讓您將超出認可的原始程式碼 ikeys 和 toospecify 不同 ikeys 不同環境。</span><span class="sxs-lookup"><span data-stu-id="389e0-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="389e0-139">其他設定選項如以下述。</span><span class="sxs-lookup"><span data-stu-id="389e0-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="389e0-140">您可以嘗試 hello 代理程式，而不傳送遙測設定 hello 檢測金鑰 tooany 是非空白字串。</span><span class="sxs-lookup"><span data-stu-id="389e0-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="389e0-141"><a name="monitor"></a> 監視您的應用程式</span><span class="sxs-lookup"><span data-stu-id="389e0-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="389e0-142">hello 代理程式會自動收集有關 hello Node.js 執行階段遙測和某些常見的協力廠商模組。</span><span class="sxs-lookup"><span data-stu-id="389e0-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="389e0-143">使用您的應用程式現在 toogenerate 有些資料。</span><span class="sxs-lookup"><span data-stu-id="389e0-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="389e0-144">然後，在 hello [Azure 入口網站][ portal]瀏覽您稍早建立的 toohello Application Insights 資源，並尋找您的第一個幾個資料點中 hello 概觀時間表中，如 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="389e0-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="389e0-145">按一下瀏覽 hello 圖表，以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="389e0-145">Click through hello charts for more details.</span></span>

![第一個資料點](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="389e0-147">按一下 hello 應用程式對應按鈕 tooview hello 拓樸探索到的應用程式中，如 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="389e0-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="389e0-148">按一下瀏覽元件 hello 對應中的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="389e0-148">Click through components in hello map for more details.</span></span>

![簡單的應用程式對應](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="389e0-150">深入了解您的應用程式和疑難排解使用 hello hello"調查 」 一節底下可使用其他檢視。</span><span class="sxs-lookup"><span data-stu-id="389e0-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![調查區段](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="389e0-152">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="389e0-152">No data?</span></span>

<span data-ttu-id="389e0-153">因為 hello 代理程式批次提交的資料有可能延遲才能 hello 入口網站中顯示的項目。</span><span class="sxs-lookup"><span data-stu-id="389e0-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="389e0-154">如果您沒有看到您在資源中的資料嘗試進行的一些 hello 遵循修正：</span><span class="sxs-lookup"><span data-stu-id="389e0-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="389e0-155">使用 hello 應用程式的其他功能;需要更多動作 toogenerate 更多的遙測。</span><span class="sxs-lookup"><span data-stu-id="389e0-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="389e0-156">按一下**重新整理**hello 入口網站的資源檢視中。</span><span class="sxs-lookup"><span data-stu-id="389e0-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="389e0-157">圖表會自動定期重新整理本身，但立即重新整理會強制此 toohappen。</span><span class="sxs-lookup"><span data-stu-id="389e0-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="389e0-158">確認[所需的連出連接埠](app-insights-ip-addresses.md)已開啟。</span><span class="sxs-lookup"><span data-stu-id="389e0-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="389e0-159">開啟 hello[搜尋](app-insights-diagnostic-search.md)磚，然後尋找個別事件。</span><span class="sxs-lookup"><span data-stu-id="389e0-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="389e0-160">檢查 hello[常見問題集][]。</span><span class="sxs-lookup"><span data-stu-id="389e0-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="389e0-161">代理程式組態</span><span class="sxs-lookup"><span data-stu-id="389e0-161">Agent Configuration</span></span>

<span data-ttu-id="389e0-162">以下是 hello 代理程式的設定方法，其預設值。</span><span class="sxs-lookup"><span data-stu-id="389e0-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="389e0-163">toofully 交互關聯事件，在服務中，是確定 tooset `.setAutoDependencyCorrelation(true)`。</span><span class="sxs-lookup"><span data-stu-id="389e0-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="389e0-164">這可讓 hello 代理程式 tootrack 內容到 Node.js 中的非同步回呼。</span><span class="sxs-lookup"><span data-stu-id="389e0-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="389e0-165">代理程式 API</span><span class="sxs-lookup"><span data-stu-id="389e0-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="389e0-166">hello.NET 代理程式 API 的完整說明[這裡](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="389e0-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="389e0-167">您可以追蹤任何要求、 事件、 計量或使用 hello 應用程式 Insights Node.js 用戶端的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="389e0-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="389e0-168">hello 下列範例會示範部分 hello 可用的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="389e0-168">hello following example demonstrates some of hello available APIs.</span></span>

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

### <a name="track-your-dependencies"></a><span data-ttu-id="389e0-169">追蹤相依項目</span><span class="sxs-lookup"><span data-stu-id="389e0-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="389e0-170">加入自訂屬性 tooall 事件</span><span class="sxs-lookup"><span data-stu-id="389e0-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="389e0-171">追蹤 HTTP GET 要求</span><span class="sxs-lookup"><span data-stu-id="389e0-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="389e0-172">追蹤伺服器啟動時間</span><span class="sxs-lookup"><span data-stu-id="389e0-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="389e0-173">其他資源</span><span class="sxs-lookup"><span data-stu-id="389e0-173">More resources</span></span>

* [<span data-ttu-id="389e0-174">監視您 hello 入口網站中的遙測</span><span class="sxs-lookup"><span data-stu-id="389e0-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="389e0-175">寫您的遙測的分析查詢</span><span class="sxs-lookup"><span data-stu-id="389e0-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[常見問題集]: app-insights-troubleshoot-faq.md
