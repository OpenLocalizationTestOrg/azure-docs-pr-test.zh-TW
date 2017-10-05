---
title: "使用 Azure Application Insights 監視 Node.js 服務 | Microsoft Docs"
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
ms.openlocfilehash: ee65207e546c7050cc7bf35c36624fc49ad9eec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="d718c-103">使用 Application Insights 監視 Node.js 服務和應用程式</span><span class="sxs-lookup"><span data-stu-id="d718c-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="d718c-104">[Azure Application Insights](app-insights-overview.md) 會在您部署後端服務和元件之後加以監視，協助您[探索並快速診斷效能和其他問題](app-insights-detect-triage-diagnose.md)。</span><span class="sxs-lookup"><span data-stu-id="d718c-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="d718c-105">將它使用於任何地方裝載的 Node.js 服務︰您的資料中心、Azure VM 和 Web Apps，甚至式其他公用雲端。</span><span class="sxs-lookup"><span data-stu-id="d718c-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="d718c-106">若要接收、儲存和探索您的監視資料，請遵循下列指示，在您的程式碼中包含代理程式，並且在 Azure 中設定對應的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="d718c-106">To receive, store, and explore your monitoring data, follow the following instructions to include an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="d718c-107">代理程式會將資料傳送至該資源，進行進一步的分析和探索。</span><span class="sxs-lookup"><span data-stu-id="d718c-107">The agent sends data to that resource for further analysis and exploration.</span></span>

<span data-ttu-id="d718c-108">Node.js 代理程式可以自動監視傳入和傳出 HTTP 要求、數個系統計量及例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d718c-108">The Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="d718c-109">從 v0.20 開始，也可以監視一些常見的第三方套件，例如 `mongodb`、`mysql` 和 `redis`。</span><span class="sxs-lookup"><span data-stu-id="d718c-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="d718c-110">與傳入 HTTP 要求相關的所有事件都會相互關聯，以進行快速疑難排解。</span><span class="sxs-lookup"><span data-stu-id="d718c-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="d718c-111">使用稍後說明的代理程式 API 進行手動檢測，即可監視應用程式和系統的多個部分。</span><span class="sxs-lookup"><span data-stu-id="d718c-111">You can monitor more aspects of your app and system by manually instrumenting them using the agent API described later.</span></span>

![範例效能監視圖表](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="d718c-113">開始使用</span><span class="sxs-lookup"><span data-stu-id="d718c-113">Getting Started</span></span>

<span data-ttu-id="d718c-114">讓我們逐步設定應用程式或服務的監視。</span><span class="sxs-lookup"><span data-stu-id="d718c-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="d718c-115"><a name="resource"></a>設定 App Insights 資源</span><span class="sxs-lookup"><span data-stu-id="d718c-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="d718c-116">**開始之前**，請確定您有 Azure 訂用帳戶或[免費取得一個新訂用帳戶][azure-free-offer]。</span><span class="sxs-lookup"><span data-stu-id="d718c-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="d718c-117">如果您的組織已經有 Azure 訂用帳戶，系統管理員可以依照 [這些指示][add-aad-user] 將您新增至該訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d718c-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="d718c-118">現在登入 [Azure 入口網站][portal]並建立 Application Insights 資源，如下所示 - 按一下 [新增] > [開發人員工具] > [Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="d718c-118">Now log in to the [Azure portal][portal] and create an Application Insights resource as illustrated in the following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="d718c-119">此資源包含用於接收遙測資料的端點、此資料的儲存體、已儲存的報告和儀表板、規則和警示組態等等。</span><span class="sxs-lookup"><span data-stu-id="d718c-119">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![建立 App Insights 資源](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="d718c-121">在資源建立頁面上，從 [應用程式類型] 下拉式清單中選擇 [Node.js 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d718c-121">On the resource creation page, choose "Node.js Application" from the application type drop-down.</span></span> <span data-ttu-id="d718c-122">應用程式類型可決定為您建立的預設儀表板和報告集合。</span><span class="sxs-lookup"><span data-stu-id="d718c-122">The app type determines the default set of dashboards and reports created for you.</span></span> <span data-ttu-id="d718c-123">別擔心，任何 App Insights 資源實際上都可以從任何語言和平台收集資料。</span><span class="sxs-lookup"><span data-stu-id="d718c-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![新增 App Insights 資源表單](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="d718c-125"><a name="agent"></a> 設定 Node.js 代理程式</span><span class="sxs-lookup"><span data-stu-id="d718c-125"><a name="agent"></a> Set up the Node.js agent</span></span>

<span data-ttu-id="d718c-126">現在可以在您的應用程式中包含代理程式，以便蒐集資料。</span><span class="sxs-lookup"><span data-stu-id="d718c-126">Now it's time to include the agent in your app so it can gather data.</span></span>
<span data-ttu-id="d718c-127">如下所示，從入口網站複製資源的檢測金鑰 (以下稱為您的 `ikey`)。</span><span class="sxs-lookup"><span data-stu-id="d718c-127">Start by copying your resource's Instrumentation Key (hereinafter referred to as your `ikey`) from the portal as shown below.</span></span> <span data-ttu-id="d718c-128">App Insights 系統會使用此金鑰將資料對應至 Azure 資源，因此您必須在環境變數或您的程式碼中加以指定，以便代理程式使用。</span><span class="sxs-lookup"><span data-stu-id="d718c-128">The App Insights system uses this key to map data to your Azure resource so you need to specify it in an environment variable or your code for the agent to use.</span></span>  

![複製檢測金鑰](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="d718c-130">接著透過 package.json，將 Node.js 代理程式庫新增至您應用程式的相依性。</span><span class="sxs-lookup"><span data-stu-id="d718c-130">Next, add the Node.js agent library to your app's dependencies via package.json.</span></span> <span data-ttu-id="d718c-131">從您應用程式的根資料夾，執行︰</span><span class="sxs-lookup"><span data-stu-id="d718c-131">From the root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="d718c-132">您現在需要在您的程式碼中明確地載入此程式庫。</span><span class="sxs-lookup"><span data-stu-id="d718c-132">Now you need to explicitly load the library in your code.</span></span> <span data-ttu-id="d718c-133">因為代理程式會將檢測插入其他許多程式庫中，所以您應該儘早將它載入，甚至插入在其他 `require` 陳述式之前。</span><span class="sxs-lookup"><span data-stu-id="d718c-133">Because the agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="d718c-134">若要開始，請在第一個 .js 檔案頂端新增︰</span><span class="sxs-lookup"><span data-stu-id="d718c-134">To get started, at the top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="d718c-135">`setup` 方法會針對所有追蹤的項目，設定預設要使用的檢測金鑰 (以及 Azure 資源)。</span><span class="sxs-lookup"><span data-stu-id="d718c-135">The `setup` method configures the instrumentation key (and thus Azure resource) to be used by default for all tracked items.</span></span> <span data-ttu-id="d718c-136">在設定完成後呼叫 `start`，開始蒐集和傳送遙測資料。</span><span class="sxs-lookup"><span data-stu-id="d718c-136">Call `start` after configuration is finished to begin gathering and sending telemetry data.</span></span>

<span data-ttu-id="d718c-137">您也可以透過環境變數 APPINSIGHTS\_INSTRUMENTATIONKEY 提供 ikey，而非以手動方式將它傳遞至 `setup()` 或 `getClient()`。</span><span class="sxs-lookup"><span data-stu-id="d718c-137">You can also provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually to  `setup()` or `getClient()`.</span></span> <span data-ttu-id="d718c-138">這種做法可讓您將 ikeys 保留在認可的原始程式碼之外，並針對不同的環境指定不同的 ikey。</span><span class="sxs-lookup"><span data-stu-id="d718c-138">This practice lets you keep ikeys out of committed source code and to specify different ikeys for different environments.</span></span>

<span data-ttu-id="d718c-139">其他設定選項如以下述。</span><span class="sxs-lookup"><span data-stu-id="d718c-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="d718c-140">您可以將檢測金鑰設定為非空白字串，在不傳送遙測的情況下嘗試代理程式。</span><span class="sxs-lookup"><span data-stu-id="d718c-140">You can try the agent without sending telemetry by setting the instrumentation key to any non-empty string.</span></span>

### <span data-ttu-id="d718c-141"><a name="monitor"></a> 監視您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d718c-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="d718c-142">代理程式會自動蒐集有關 Node.js 執行階段和一些常見第三方模組的遙測。</span><span class="sxs-lookup"><span data-stu-id="d718c-142">The agent automatically gathers telemetry about the Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="d718c-143">現在使用您的應用程式來產生一些資料。</span><span class="sxs-lookup"><span data-stu-id="d718c-143">Use your application now to generate some of this data.</span></span>

<span data-ttu-id="d718c-144">然後，在 [Azure 入口網站][portal]中瀏覽至您稍早建立的 Application Insights 資源，並且在 [概觀時間表] 中尋找您的前幾個資料點，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="d718c-144">Then, in the [Azure portal][portal] browse to the Application Insights resource you created earlier and look for your first few data points in the Overview timeline, as in the following image.</span></span> <span data-ttu-id="d718c-145">逐一點選各個圖表以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d718c-145">Click through the charts for more details.</span></span>

![第一個資料點](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="d718c-147">按一下 [應用程式對應] 按鈕，以檢視針對您的應用程式找到的拓撲，如下列圖所示。</span><span class="sxs-lookup"><span data-stu-id="d718c-147">Click the Application map button to view the topology discovered for your app, as in the following image.</span></span> <span data-ttu-id="d718c-148">逐一點選對應中的各個元件，以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d718c-148">Click through components in the map for more details.</span></span>

![簡單的應用程式對應](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="d718c-150">使用 [調查] 區段下其他可用的檢視，深入了解您的應用程式並針對問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="d718c-150">Learn more about your app and troubleshoot problems using the other views available under the "Investigate" section.</span></span>

![調查區段](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="d718c-152">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="d718c-152">No data?</span></span>

<span data-ttu-id="d718c-153">因為代理程式會分批提交資料，所以項目可能會延遲顯示在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="d718c-153">Because the agent batches data for submission there may be a delay before items are displayed in the portal.</span></span> <span data-ttu-id="d718c-154">如果您未在您的資源中看到資料，請嘗試以下一些修正方式︰</span><span class="sxs-lookup"><span data-stu-id="d718c-154">If you don't see data in your resource try some of the following fixes:</span></span>

* <span data-ttu-id="d718c-155">多使用一下應用程式；採取更多動作，以產生更多遙測。</span><span class="sxs-lookup"><span data-stu-id="d718c-155">Use the application some more; take more actions to generate more telemetry.</span></span>
* <span data-ttu-id="d718c-156">按一下入口網站資源檢視中的 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="d718c-156">Click **Refresh** in the portal resource view.</span></span> <span data-ttu-id="d718c-157">圖表會自動定期重新整理，但重新整理會強制此動作立即發生。</span><span class="sxs-lookup"><span data-stu-id="d718c-157">Charts automatically refresh themselves periodically but refreshing forces this to happen immediately.</span></span>
* <span data-ttu-id="d718c-158">確認[所需的連出連接埠](app-insights-ip-addresses.md)已開啟。</span><span class="sxs-lookup"><span data-stu-id="d718c-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="d718c-159">開啟 [搜尋](app-insights-diagnostic-search.md) 圖格來查看個別事件。</span><span class="sxs-lookup"><span data-stu-id="d718c-159">Open the [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="d718c-160">查看[常見問題集][]。</span><span class="sxs-lookup"><span data-stu-id="d718c-160">Check the [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="d718c-161">代理程式組態</span><span class="sxs-lookup"><span data-stu-id="d718c-161">Agent Configuration</span></span>

<span data-ttu-id="d718c-162">以下是代理程式的設定方法及其預設值。</span><span class="sxs-lookup"><span data-stu-id="d718c-162">Following are the agent's configuration methods and their default values.</span></span>

<span data-ttu-id="d718c-163">若要使服務中的事件完全相互關聯，請務必設定 `.setAutoDependencyCorrelation(true)`。</span><span class="sxs-lookup"><span data-stu-id="d718c-163">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="d718c-164">這可讓代理程式追蹤 Node.js 中所有非同步回呼的內容。</span><span class="sxs-lookup"><span data-stu-id="d718c-164">This allows the agent to track context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="d718c-165">代理程式 API</span><span class="sxs-lookup"><span data-stu-id="d718c-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="d718c-166">[這裡](app-insights-api-custom-events-metrics.md)有 .NET 代理程式 API 的完整說明。</span><span class="sxs-lookup"><span data-stu-id="d718c-166">The .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="d718c-167">您可以使用 Application Insights Node.js 用戶端來追蹤任何要求、事件、計量或例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d718c-167">You can track any request, event, metric, or exception using the Application Insights Node.js client.</span></span> <span data-ttu-id="d718c-168">下列範例示範一些可用的 API。</span><span class="sxs-lookup"><span data-stu-id="d718c-168">The following example demonstrates some of the available APIs.</span></span>

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
  client.trackRequest(req, res); // Place at the beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="d718c-169">追蹤相依項目</span><span class="sxs-lookup"><span data-stu-id="d718c-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-to-all-events"></a><span data-ttu-id="d718c-170">將自訂屬性新增至所有事件</span><span class="sxs-lookup"><span data-stu-id="d718c-170">Add a custom property to all events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="d718c-171">追蹤 HTTP GET 要求</span><span class="sxs-lookup"><span data-stu-id="d718c-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="d718c-172">追蹤伺服器啟動時間</span><span class="sxs-lookup"><span data-stu-id="d718c-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="d718c-173">其他資源</span><span class="sxs-lookup"><span data-stu-id="d718c-173">More resources</span></span>

* [<span data-ttu-id="d718c-174">在入口網站中監視遙測</span><span class="sxs-lookup"><span data-stu-id="d718c-174">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="d718c-175">寫您的遙測的分析查詢</span><span class="sxs-lookup"><span data-stu-id="d718c-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
<span data-ttu-id="d718c-176">[常見問題集]: app-insights-troubleshoot-faq.md</span><span class="sxs-lookup"><span data-stu-id="d718c-176">[FAQ]: app-insights-troubleshoot-faq.md</span></span>
