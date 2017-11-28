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
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="af51b-103">設定 Application Insights：追蹤相依性</span><span class="sxs-lookup"><span data-stu-id="af51b-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="af51b-104">「相依性」  是由應用程式呼叫的外部元件。</span><span class="sxs-lookup"><span data-stu-id="af51b-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="af51b-105">這通常是使用 HTTP 呼叫的服務，或資料庫，或檔案系統。</span><span class="sxs-lookup"><span data-stu-id="af51b-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="af51b-106">[Application Insights](app-insights-overview.md) 會測量您應用程式等待相依性所花費的時間，以及相依性呼叫失敗的頻率。</span><span class="sxs-lookup"><span data-stu-id="af51b-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="af51b-107">您可以調查特定的呼叫，且兩者產生關聯 toorequests 和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="af51b-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![範例圖表](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="af51b-109">hello 的全新相依性監視目前報告相依性呼叫 toothese 的類型：</span><span class="sxs-lookup"><span data-stu-id="af51b-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="af51b-110">伺服器</span><span class="sxs-lookup"><span data-stu-id="af51b-110">Server</span></span>
  * <span data-ttu-id="af51b-111">SQL DATABASE</span><span class="sxs-lookup"><span data-stu-id="af51b-111">SQL databases</span></span>
  * <span data-ttu-id="af51b-112">使用 HTTP 式繫結的 ASP.NET Web 和 WCF 服務</span><span class="sxs-lookup"><span data-stu-id="af51b-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="af51b-113">本機或遠端 HTTP 呼叫</span><span class="sxs-lookup"><span data-stu-id="af51b-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="af51b-114">Azure Cosmos DB、資料表、Blob 儲存體和佇列</span><span class="sxs-lookup"><span data-stu-id="af51b-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="af51b-115">網頁</span><span class="sxs-lookup"><span data-stu-id="af51b-115">Web pages</span></span>
  * <span data-ttu-id="af51b-116">AJAX 呼叫</span><span class="sxs-lookup"><span data-stu-id="af51b-116">AJAX calls</span></span>

<span data-ttu-id="af51b-117">在選取的方法周圍使用[位元組程式碼檢測](https://msdn.microsoft.com/library/z9z62c29.aspx)來監視工作。</span><span class="sxs-lookup"><span data-stu-id="af51b-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="af51b-118">效能額外負荷非常小。</span><span class="sxs-lookup"><span data-stu-id="af51b-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="af51b-119">您也可以撰寫您自己的 SDK 呼叫 toomonitor 其他相依性，同時在 hello 用戶端和伺服器程式碼中使用 hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)。</span><span class="sxs-lookup"><span data-stu-id="af51b-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="af51b-120">設定相依性監視</span><span class="sxs-lookup"><span data-stu-id="af51b-120">Set up dependency monitoring</span></span>
<span data-ttu-id="af51b-121">部分的相依性資訊會自動收集 hello [Application Insights SDK](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="af51b-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="af51b-122">tooget 完整的資料，會安裝適當的代理程式 hello hello 主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="af51b-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="af51b-123">平台</span><span class="sxs-lookup"><span data-stu-id="af51b-123">Platform</span></span> | <span data-ttu-id="af51b-124">Install</span><span class="sxs-lookup"><span data-stu-id="af51b-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="af51b-125">IIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="af51b-125">IIS Server</span></span> |<span data-ttu-id="af51b-126">任一[在伺服器上安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)或[升級您的應用程式 too.NET framework 4.6 或更新版本](http://go.microsoft.com/fwlink/?LinkId=528259)並安裝 hello [Application Insights SDK](app-insights-asp-net.md)應用程式中。</span><span class="sxs-lookup"><span data-stu-id="af51b-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="af51b-127">Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="af51b-127">Azure Web App</span></span> |<span data-ttu-id="af51b-128">在您 web 應用程式控制台 」 中[開啟 hello Application Insights 刀鋒視窗，在您 web 應用程式的控制台中](app-insights-azure-web-apps.md)並出現提示時選擇安裝。</span><span class="sxs-lookup"><span data-stu-id="af51b-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="af51b-129">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="af51b-129">Azure Cloud Service</span></span> |<span data-ttu-id="af51b-130">[使用啟動工作](app-insights-cloudservices.md)或[安裝 .NET Framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="af51b-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="af51b-131">其中 toofind 相依性資料</span><span class="sxs-lookup"><span data-stu-id="af51b-131">Where toofind dependency data</span></span>
* <span data-ttu-id="af51b-132">[應用程式對應](#application-map)會以視覺化方式顯示您應用程式與相鄰元件之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="af51b-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="af51b-133">[效能、瀏覽器及失敗刀鋒視窗](#performance-and-blades)會顯示伺服器相依性資料。</span><span class="sxs-lookup"><span data-stu-id="af51b-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="af51b-134">[瀏覽器刀鋒視窗](#ajax-calls)會顯示來自您使用者瀏覽器的 AJAX 呼叫。</span><span class="sxs-lookup"><span data-stu-id="af51b-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="af51b-135">[按一下透過緩慢或失敗的要求從](#diagnose-slow-requests)toocheck 它們的相依性呼叫。</span><span class="sxs-lookup"><span data-stu-id="af51b-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="af51b-136">[分析](#analytics)可以是使用的 tooquery 相依性資料。</span><span class="sxs-lookup"><span data-stu-id="af51b-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="af51b-137">應用程式對應</span><span class="sxs-lookup"><span data-stu-id="af51b-137">Application Map</span></span>
<span data-ttu-id="af51b-138">應用程式對應做為您的應用程式的 hello 元件之間的視覺輔助工具 toodiscovering 相依性。</span><span class="sxs-lookup"><span data-stu-id="af51b-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="af51b-139">它會自動產生從 hello 從您的應用程式的遙測。</span><span class="sxs-lookup"><span data-stu-id="af51b-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="af51b-140">此範例會顯示 hello 瀏覽器的指令碼中的 AJAX 呼叫和伺服器 hello 從 REST 呼叫 tootwo 外部服務時，應用程式。</span><span class="sxs-lookup"><span data-stu-id="af51b-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![應用程式對應](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="af51b-142">**從 hello 方塊瀏覽**toorelevant 相依性和其他圖表。</span><span class="sxs-lookup"><span data-stu-id="af51b-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="af51b-143">**Pin hello 對應**toohello[儀表板](app-insights-dashboards.md)，其中將完全正常運作。</span><span class="sxs-lookup"><span data-stu-id="af51b-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="af51b-144">[深入了解](app-insights-app-map.md)。</span><span class="sxs-lookup"><span data-stu-id="af51b-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="af51b-145">效能和失敗刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="af51b-145">Performance and failure blades</span></span>
<span data-ttu-id="af51b-146">hello 效能刀鋒視窗會顯示 hello hello 伺服器應用程式所做的相依性呼叫持續時間。</span><span class="sxs-lookup"><span data-stu-id="af51b-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="af51b-147">其中會顯示摘要圖表和依呼叫劃分的表格。</span><span class="sxs-lookup"><span data-stu-id="af51b-147">There's a summary chart and a table segmented by call.</span></span>

![效能刀鋒視窗相依性圖表](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="af51b-149">按一下瀏覽 hello 摘要圖表或 hello 資料表項目 toosearch 未經處理的項目這些呼叫。</span><span class="sxs-lookup"><span data-stu-id="af51b-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![相依性呼叫執行個體](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="af51b-151">**失敗計數**會顯示在 hello**失敗**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="af51b-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="af51b-152">失敗是不是 hello 範圍 200-399 或無法辨識的任何傳回碼。</span><span class="sxs-lookup"><span data-stu-id="af51b-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="af51b-153">**100% 失敗？**</span><span class="sxs-lookup"><span data-stu-id="af51b-153">**100% failures?**</span></span> <span data-ttu-id="af51b-154">- 這可能是指您取得的只是部分相依性資料。</span><span class="sxs-lookup"><span data-stu-id="af51b-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="af51b-155">您需要[設定相依性監視適當 tooyour 平台](#set-up-dependency-monitoring)。</span><span class="sxs-lookup"><span data-stu-id="af51b-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="af51b-156">AJAX 呼叫</span><span class="sxs-lookup"><span data-stu-id="af51b-156">AJAX Calls</span></span>
<span data-ttu-id="af51b-157">hello 瀏覽器刀鋒視窗會顯示 hello 持續時間，並從呼叫的 AJAX 失敗率[web 網頁中的 JavaScript](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="af51b-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="af51b-158">它們會顯示為「相依性」。</span><span class="sxs-lookup"><span data-stu-id="af51b-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="af51b-159"><a name="diagnosis"></a> 診斷速度緩慢的要求</span><span class="sxs-lookup"><span data-stu-id="af51b-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="af51b-160">每個要求的事件與 hello 相依性呼叫相關聯，例外狀況和其他事件時正在處理您的應用程式會根據所追蹤 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="af51b-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="af51b-161">因此如果執行一些要求的格式錯誤，您可以了解是否因為 tooslow 回應從相依性。</span><span class="sxs-lookup"><span data-stu-id="af51b-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="af51b-162">讓我們逐步解說一個該情況的範例。</span><span class="sxs-lookup"><span data-stu-id="af51b-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="af51b-163">從要求 toodependencies 追蹤</span><span class="sxs-lookup"><span data-stu-id="af51b-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="af51b-164">開啟 hello 效能刀鋒視窗中，然後查看 hello 方格的要求：</span><span class="sxs-lookup"><span data-stu-id="af51b-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![含有平均和計數的要求清單](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="af51b-166">hello 前一個花費很長的時間。</span><span class="sxs-lookup"><span data-stu-id="af51b-166">hello top one is taking very long.</span></span> <span data-ttu-id="af51b-167">我們來看看我們可以查明 hello 時間花在哪裡。</span><span class="sxs-lookup"><span data-stu-id="af51b-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="af51b-168">按一下該資料列 toosee 個別要求事件：</span><span class="sxs-lookup"><span data-stu-id="af51b-168">Click that row toosee individual request events:</span></span>

![要求發生次數的清單](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="af51b-170">按一下任何長時間執行執行個體 tooinspect 進一步，並捲動 toohello 遠端相依性呼叫相關的 toothis 要求：</span><span class="sxs-lookup"><span data-stu-id="af51b-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![尋找呼叫 tooRemote 相依性，請識別不尋常的持續時間](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="af51b-172">它看起來像大部分的 hello 時間服務此要求花費在呼叫 tooa 本機服務。</span><span class="sxs-lookup"><span data-stu-id="af51b-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="af51b-173">選取該資料列 tooget 的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="af51b-173">Select that row tooget more information:</span></span>

![按一下 透過該遠端相依性 tooidentify hello 問題](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="af51b-175">這是其中 hello 問題看起來。</span><span class="sxs-lookup"><span data-stu-id="af51b-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="af51b-176">我們已正確指出哪個 hello 問題，所以現在我們只需要 toofind 出為何該呼叫所花這麼久。</span><span class="sxs-lookup"><span data-stu-id="af51b-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="af51b-177">要求時間軸</span><span class="sxs-lookup"><span data-stu-id="af51b-177">Request timeline</span></span>
<span data-ttu-id="af51b-178">在一個不同的案例中，並沒有任何特別長的相依性呼叫。</span><span class="sxs-lookup"><span data-stu-id="af51b-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="af51b-179">但藉由切換 toohello 時間表檢視，我們可以看到我們內部處理中發生 hello 延遲的位置：</span><span class="sxs-lookup"><span data-stu-id="af51b-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![尋找呼叫 tooRemote 相依性，請識別不尋常的持續時間](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="af51b-181">讓我們看起來應該在我們的程式碼 toosee 原因也就是，那里似乎之後第一個相依性呼叫 hello、 toobe 大的間隙。</span><span class="sxs-lookup"><span data-stu-id="af51b-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="af51b-182">剖析您的即時網站</span><span class="sxs-lookup"><span data-stu-id="af51b-182">Profile your live site</span></span>

<span data-ttu-id="af51b-183">其中 hello 次時，就不知道嗎？hello [Application Insights profiler](app-insights-profiler.md)追蹤 HTTP 呼叫 tooyour 即時網站，並顯示在程式碼中的哪一個函式所花費的 hello 最長時間。</span><span class="sxs-lookup"><span data-stu-id="af51b-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="af51b-184">失敗的要求</span><span class="sxs-lookup"><span data-stu-id="af51b-184">Failed requests</span></span>
<span data-ttu-id="af51b-185">失敗的要求也可能失敗的呼叫 toodependencies 相關聯。</span><span class="sxs-lookup"><span data-stu-id="af51b-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="af51b-186">同樣地，我們可以按一下 tootrack hello 問題。</span><span class="sxs-lookup"><span data-stu-id="af51b-186">Again, we can click through tootrack down hello problem.</span></span>

![按一下 hello 失敗的要求圖表](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="af51b-188">按一下透過 tooan 出現失敗的要求，並查看其相關聯的事件。</span><span class="sxs-lookup"><span data-stu-id="af51b-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![按一下要求類型，然後按一下 hello 執行個體 tooget tooa 不同檢視的 hello 相同的執行個體，請按一下此 tooget 例外狀況詳細資料。](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="af51b-190">Analytics</span><span class="sxs-lookup"><span data-stu-id="af51b-190">Analytics</span></span>
<span data-ttu-id="af51b-191">您可以追蹤 hello 中的相依性[記錄分析查詢語言](https://docs.loganalytics.io/)。</span><span class="sxs-lookup"><span data-stu-id="af51b-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="af51b-192">以下是一些範例。</span><span class="sxs-lookup"><span data-stu-id="af51b-192">Here are some examples.</span></span>

* <span data-ttu-id="af51b-193">尋找任何失敗的相依性呼叫：</span><span class="sxs-lookup"><span data-stu-id="af51b-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="af51b-194">尋找 AJAX 呼叫︰</span><span class="sxs-lookup"><span data-stu-id="af51b-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="af51b-195">尋找與要求關聯的相依性呼叫：</span><span class="sxs-lookup"><span data-stu-id="af51b-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="af51b-196">尋找與頁面檢視關聯的 AJAX 呼叫：</span><span class="sxs-lookup"><span data-stu-id="af51b-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="af51b-197">自訂相依性追蹤</span><span class="sxs-lookup"><span data-stu-id="af51b-197">Custom dependency tracking</span></span>
<span data-ttu-id="af51b-198">hello 標準的相依性追蹤模組自動探索外部的相依性，例如資料庫和 REST Api。</span><span class="sxs-lookup"><span data-stu-id="af51b-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="af51b-199">但是您可能想要一些額外的元件 toobe 處理 hello 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="af51b-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="af51b-200">您可以撰寫程式碼傳送相依性資訊，請使用 hello 相同[TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) hello 標準模組所使用。</span><span class="sxs-lookup"><span data-stu-id="af51b-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="af51b-201">比方說，如果您未自行撰寫，您可能有時間所有 hello 呼叫 tooit，您可以建立與組件的程式碼，toofind 出哪些比重它讓 tooyour 回應時間。</span><span class="sxs-lookup"><span data-stu-id="af51b-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="af51b-202">Application Insights 中的 hello 相依性圖表中顯示此資料傳送使用 toohave `TrackDependency`。</span><span class="sxs-lookup"><span data-stu-id="af51b-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="af51b-203">如果您想 tooswitch hello 標準的相依性追蹤模組時，移除在 hello 參考 tooDependencyTrackingTelemetryModule [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)。</span><span class="sxs-lookup"><span data-stu-id="af51b-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="af51b-204">疑難排解</span><span class="sxs-lookup"><span data-stu-id="af51b-204">Troubleshooting</span></span>
<span data-ttu-id="af51b-205">*相依性成功旗標一律顯示 true 或 false。*</span><span class="sxs-lookup"><span data-stu-id="af51b-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="af51b-206">*SQL 查詢未完整顯示。*</span><span class="sxs-lookup"><span data-stu-id="af51b-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="af51b-207">Hello SDK 升級 toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="af51b-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="af51b-208">如果您的 .NET 版本低於 4.6：</span><span class="sxs-lookup"><span data-stu-id="af51b-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="af51b-209">IIS 主機： 安裝[Application Insights 的代理程式](app-insights-monitor-performance-live-website-now.md)hello 主機伺服器上。</span><span class="sxs-lookup"><span data-stu-id="af51b-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="af51b-210">Azure web 應用程式： 開啟 Application Insights 在 hello web 應用程式控制項面板中，索引標籤，並安裝 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="af51b-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="af51b-211">影片</span><span class="sxs-lookup"><span data-stu-id="af51b-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="af51b-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af51b-212">Next steps</span></span>
* [<span data-ttu-id="af51b-213">例外狀況</span><span class="sxs-lookup"><span data-stu-id="af51b-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="af51b-214">使用者和頁面資料</span><span class="sxs-lookup"><span data-stu-id="af51b-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="af51b-215">Availability</span><span class="sxs-lookup"><span data-stu-id="af51b-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
