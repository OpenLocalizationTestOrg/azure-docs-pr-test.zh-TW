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
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="2f037-103">我如何在 Application Insights 中...？</span><span class="sxs-lookup"><span data-stu-id="2f037-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="2f037-104">... 時收到電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f037-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="2f037-105">我的網站當機時寄送電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f037-105">Email if my site goes down</span></span>
<span data-ttu-id="2f037-106">設定 [可用性 Web 測試](app-insights-monitor-web-app-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="2f037-107">我的網站多載時寄送電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f037-107">Email if my site is overloaded</span></span>
<span data-ttu-id="2f037-108">針對 **伺服器回應時間** 設定 [警示](app-insights-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="2f037-109">介於 1 到 2 秒之間的閾值應該會運作。</span><span class="sxs-lookup"><span data-stu-id="2f037-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="2f037-110">您的 app 也可能會藉由傳回失敗碼顯示資源耗盡的徵兆。</span><span class="sxs-lookup"><span data-stu-id="2f037-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="2f037-111">針對 [失敗的要求] 設定警示。</span><span class="sxs-lookup"><span data-stu-id="2f037-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="2f037-112">如果您想 tooset 警示上**伺服器例外狀況**，您可能必須 toodo[某些額外的安裝](app-insights-asp-net-exceptions.md)順序 toosee 資料中。</span><span class="sxs-lookup"><span data-stu-id="2f037-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="2f037-113">傳送電子郵件的例外狀況</span><span class="sxs-lookup"><span data-stu-id="2f037-113">Email on exceptions</span></span>
1. [<span data-ttu-id="2f037-114">設定例外狀況監視</span><span class="sxs-lookup"><span data-stu-id="2f037-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="2f037-115">[設定警示](app-insights-alerts.md)上 hello 例外狀況計數公制</span><span class="sxs-lookup"><span data-stu-id="2f037-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="2f037-116">我的 app 發生事件時寄送電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f037-116">Email on an event in my app</span></span>
<span data-ttu-id="2f037-117">讓我們假設您想要 tooget 電子郵件，當發生特定事件。</span><span class="sxs-lookup"><span data-stu-id="2f037-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="2f037-118">Application Insights 並未直接提供此功能，但它可 [在計量超過某個閾值時傳送警示](app-insights-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="2f037-119">您可以針對 [自訂計量](app-insights-api-custom-events-metrics.md#trackmetric)設定警示，而不是自訂事件。</span><span class="sxs-lookup"><span data-stu-id="2f037-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="2f037-120">撰寫一些程式碼 tooincrease 度量 hello 事件發生時：</span><span class="sxs-lookup"><span data-stu-id="2f037-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="2f037-121">或：</span><span class="sxs-lookup"><span data-stu-id="2f037-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="2f037-122">警示有兩種狀態，因為您有 toosend 較低的值時考慮 toohave 結束 hello 警示：</span><span class="sxs-lookup"><span data-stu-id="2f037-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="2f037-123">建立圖表中的[度量總管](app-insights-metrics-explorer.md)toosee 您警示：</span><span class="sxs-lookup"><span data-stu-id="2f037-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="2f037-124">Hello 度量在短時間內超過 mid 值時，現在可以設定警示的 toofire:</span><span class="sxs-lookup"><span data-stu-id="2f037-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="2f037-125">設定 hello 平均期間 toohello 最小值。</span><span class="sxs-lookup"><span data-stu-id="2f037-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="2f037-126">當 hello 度量超出及低於 hello 臨界值，您會取得電子郵件。</span><span class="sxs-lookup"><span data-stu-id="2f037-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="2f037-127">某些點 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="2f037-127">Some points tooconsider:</span></span>

* <span data-ttu-id="2f037-128">警示有兩種狀態 (「警示」和「良好」)。</span><span class="sxs-lookup"><span data-stu-id="2f037-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="2f037-129">只有當度量資訊會收到，就會評估 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="2f037-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="2f037-130">Hello 狀態變更時才傳送一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="2f037-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="2f037-131">這就是為什麼有 toosend 高和低值的度量。</span><span class="sxs-lookup"><span data-stu-id="2f037-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="2f037-132">收到 hello 值製作 tooevaluate hello 警示 hello 平均透過之前期間的 hello。</span><span class="sxs-lookup"><span data-stu-id="2f037-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="2f037-133">這發生在每次收到度量時，讓您設定的 hello 期間比更頻繁地傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="2f037-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="2f037-134">因為 「 警示 」 和 「 良好 」，則會傳送電子郵件，您可能想 tooconsider 重新考慮單次事件做為兩個狀態的條件。</span><span class="sxs-lookup"><span data-stu-id="2f037-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="2f037-135">比方說，而不是 「 已完成工作 」 事件，會造成 「 工作正在進行中的 」 情況，您從何處取得電子郵件在 hello 開始和結束工作。</span><span class="sxs-lookup"><span data-stu-id="2f037-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="2f037-136">自動設定警示</span><span class="sxs-lookup"><span data-stu-id="2f037-136">Set up alerts automatically</span></span>
[<span data-ttu-id="2f037-137">使用 PowerShell toocreate 新警示</span><span class="sxs-lookup"><span data-stu-id="2f037-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="2f037-138">使用 PowerShell tooManage Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f037-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="2f037-139">建立新的資源</span><span class="sxs-lookup"><span data-stu-id="2f037-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="2f037-140">建立新的警示</span><span class="sxs-lookup"><span data-stu-id="2f037-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="2f037-141">區分不同版本的遙測</span><span class="sxs-lookup"><span data-stu-id="2f037-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="2f037-142">應用程式中的多個角色︰使用單一 Application Insights 資源，並依據 cloud_Rolename 進行篩選。</span><span class="sxs-lookup"><span data-stu-id="2f037-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="2f037-143">深入了解</span><span class="sxs-lookup"><span data-stu-id="2f037-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="2f037-144">區分開發、測試和發行版本︰使用不同的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="2f037-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="2f037-145">挑選從 web.config hello 檢測金鑰。[深入了解](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="2f037-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="2f037-146">報告組建版本︰使用遙測初始設定式新增屬性。</span><span class="sxs-lookup"><span data-stu-id="2f037-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="2f037-147">深入了解</span><span class="sxs-lookup"><span data-stu-id="2f037-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="2f037-148">監視後端伺服器與桌面應用程式</span><span class="sxs-lookup"><span data-stu-id="2f037-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="2f037-149">[使用 hello Windows Server SDK 模組](app-insights-windows-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="2f037-150">顯現資料</span><span class="sxs-lookup"><span data-stu-id="2f037-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="2f037-151">具有來自多個 App 之計量的儀表板</span><span class="sxs-lookup"><span data-stu-id="2f037-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="2f037-152">在 [計量總管](app-insights-metrics-explorer.md)中，自訂圖表並將它儲存為我的最愛。</span><span class="sxs-lookup"><span data-stu-id="2f037-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="2f037-153">將其釘選 toohello Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="2f037-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="2f037-154">資料來自其他來源和 Application Insights 的儀表板</span><span class="sxs-lookup"><span data-stu-id="2f037-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="2f037-155">[匯出遙測 tooPower BI](app-insights-export-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="2f037-156">或</span><span class="sxs-lookup"><span data-stu-id="2f037-156">Or</span></span>

* <span data-ttu-id="2f037-157">使用 SharePoint 做為您的儀表板，在 SharePoint web 組件中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="2f037-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="2f037-158">[使用連續匯出，以及資料流分析 tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="2f037-159">使用 PowerView tooexamine hello 資料庫，並建立 SharePoint web 組件上執行 powerview。</span><span class="sxs-lookup"><span data-stu-id="2f037-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="2f037-160">篩選出匿名或已驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="2f037-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="2f037-161">如果您的使用者登入，您可以設定 hello[驗證使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)。(它不會自動重新整理)。</span><span class="sxs-lookup"><span data-stu-id="2f037-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="2f037-162">接著，您可以：</span><span class="sxs-lookup"><span data-stu-id="2f037-162">You can then:</span></span>

* <span data-ttu-id="2f037-163">搜尋特定的使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="2f037-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="2f037-164">篩選度量 tooeither 匿名或已驗證使用者</span><span class="sxs-lookup"><span data-stu-id="2f037-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="2f037-165">修改屬性名稱或值</span><span class="sxs-lookup"><span data-stu-id="2f037-165">Modify property names or values</span></span>
<span data-ttu-id="2f037-166">建立 [篩選器](app-insights-api-filtering-sampling.md#filtering)。</span><span class="sxs-lookup"><span data-stu-id="2f037-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="2f037-167">這可讓您修改，或從您的應用程式 tooApplication Insights 傳送之前篩選遙測。</span><span class="sxs-lookup"><span data-stu-id="2f037-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="2f037-168">列出特定使用者和其使用方式</span><span class="sxs-lookup"><span data-stu-id="2f037-168">List specific users and their usage</span></span>
<span data-ttu-id="2f037-169">如果您只想太[搜尋特定使用者](#search-specific-users)，您可以設定 hello[驗證使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)。</span><span class="sxs-lookup"><span data-stu-id="2f037-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="2f037-170">如果您想要使用者清單以及像是他們查看過哪些頁面或登入頻率等資料，則有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="2f037-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="2f037-171">[設定驗證的使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)， [tooa 資料庫匯出](app-insights-code-sample-export-sql-stream-analytics.md)並使用適當工具 tooanalyze 您使用者資料。</span><span class="sxs-lookup"><span data-stu-id="2f037-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="2f037-172">如果您有只有少數的使用者，傳送自訂事件或度量，如 hello 公制值或事件名稱，以及設定 hello 使用者識別碼，作為屬性使用 hello 感興趣的資料。</span><span class="sxs-lookup"><span data-stu-id="2f037-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="2f037-173">tooanalyze 網頁檢視，來取代 hello 標準 JavaScript trackPageView 呼叫。</span><span class="sxs-lookup"><span data-stu-id="2f037-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="2f037-174">tooanalyze 伺服器端遙測，使用遙測初始設定式 tooadd hello 使用者識別碼 tooall 伺服器遙測。</span><span class="sxs-lookup"><span data-stu-id="2f037-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="2f037-175">然後您可以篩選與區段的度量和搜尋 hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="2f037-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="2f037-176">從我的應用程式 tooApplication Insights 減少流量</span><span class="sxs-lookup"><span data-stu-id="2f037-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="2f037-177">在[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)，停用不需要任何模組這類 hello 效能計數器收集器。</span><span class="sxs-lookup"><span data-stu-id="2f037-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="2f037-178">使用[取樣和篩選](app-insights-api-filtering-sampling.md)在 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="2f037-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="2f037-179">在您的網頁，請回報的每個頁面上檢視的 Ajax 呼叫的 hello 數目限制。</span><span class="sxs-lookup"><span data-stu-id="2f037-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="2f037-180">在 hello 指令碼之後的程式碼片段`instrumentationKey:...`，插入： `,maxAjaxCallsPerView:3` （或適當的數字）。</span><span class="sxs-lookup"><span data-stu-id="2f037-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="2f037-181">如果您使用[TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric)，計算 hello 彙總的度量值的批次傳送嗨結果之前。</span><span class="sxs-lookup"><span data-stu-id="2f037-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="2f037-182">有一個 TrackMetric() 的多載是針對該動作所提供。</span><span class="sxs-lookup"><span data-stu-id="2f037-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="2f037-183">深入了解 [價格和配額](app-insights-pricing.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="2f037-184">停用遙測</span><span class="sxs-lookup"><span data-stu-id="2f037-184">Disable telemetry</span></span>
<span data-ttu-id="2f037-185">太**動態停止和啟動**hello 收集和傳輸的遙測資料從伺服器 hello:</span><span class="sxs-lookup"><span data-stu-id="2f037-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="2f037-186">太**停用選取的標準收集器**-例如效能計數器、 HTTP 要求，或相依性-刪除或標記為註解中的 hello 相關行[ApplicationInsights.config](app-insights-api-custom-events-metrics.md)。例如，如果您想 toosend TrackRequest 資料，您可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="2f037-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="2f037-187">檢視系統效能計數器</span><span class="sxs-lookup"><span data-stu-id="2f037-187">View system performance counters</span></span>
<span data-ttu-id="2f037-188">您可以在計量瀏覽器中顯示的度量 hello 包括一組系統效能計數器。</span><span class="sxs-lookup"><span data-stu-id="2f037-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="2f037-189">有一個預先定義且標題為 **伺服器** 的刀鋒視窗會顯示它們其中幾個。</span><span class="sxs-lookup"><span data-stu-id="2f037-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![開啟 Application Insights 資源並按一下伺服器](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="2f037-191">如果您看不到效能計數器資料</span><span class="sxs-lookup"><span data-stu-id="2f037-191">If you see no performance counter data</span></span>
* <span data-ttu-id="2f037-192">**IIS 伺服器** 。</span><span class="sxs-lookup"><span data-stu-id="2f037-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="2f037-193">[安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="2f037-194">**Azure 網站** - 我們尚未支援效能計數器。</span><span class="sxs-lookup"><span data-stu-id="2f037-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="2f037-195">有許多標準的 hello Azure 網站控制台標準的一部分，您可以取得。</span><span class="sxs-lookup"><span data-stu-id="2f037-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="2f037-196">**Unix 伺服器** - [安裝 collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="2f037-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="2f037-197">toodisplay 更多效能計數器</span><span class="sxs-lookup"><span data-stu-id="2f037-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="2f037-198">首先，[新增圖表](app-insights-metrics-explorer.md)和 hello 計數器是否在 hello 基本設定，我們提供。</span><span class="sxs-lookup"><span data-stu-id="2f037-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="2f037-199">如果沒有，[加入 hello hello 效能計數器模組所收集的計數器 toohello 集合](app-insights-performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="2f037-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
