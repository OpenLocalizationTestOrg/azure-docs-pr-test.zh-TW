---
title: "我如何在 Azure Application Insights 中... | Microsoft Docs"
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
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="a6517-103">我如何在 Application Insights 中...？</span><span class="sxs-lookup"><span data-stu-id="a6517-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="a6517-104">... 時收到電子郵件</span><span class="sxs-lookup"><span data-stu-id="a6517-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="a6517-105">我的網站當機時寄送電子郵件</span><span class="sxs-lookup"><span data-stu-id="a6517-105">Email if my site goes down</span></span>
<span data-ttu-id="a6517-106">設定 [可用性 Web 測試](app-insights-monitor-web-app-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="a6517-107">我的網站多載時寄送電子郵件</span><span class="sxs-lookup"><span data-stu-id="a6517-107">Email if my site is overloaded</span></span>
<span data-ttu-id="a6517-108">針對 **伺服器回應時間** 設定 [警示](app-insights-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="a6517-109">介於 1 到 2 秒之間的閾值應該會運作。</span><span class="sxs-lookup"><span data-stu-id="a6517-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="a6517-110">您的 app 也可能會藉由傳回失敗碼顯示資源耗盡的徵兆。</span><span class="sxs-lookup"><span data-stu-id="a6517-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="a6517-111">針對 [失敗的要求] 設定警示。</span><span class="sxs-lookup"><span data-stu-id="a6517-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="a6517-112">如果您想要針對 [伺服器例外狀況] 設定警示，可能必須進行 [一些其他設定](app-insights-asp-net-exceptions.md) 才能看到資料。</span><span class="sxs-lookup"><span data-stu-id="a6517-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="a6517-113">傳送電子郵件的例外狀況</span><span class="sxs-lookup"><span data-stu-id="a6517-113">Email on exceptions</span></span>
1. [<span data-ttu-id="a6517-114">設定例外狀況監視</span><span class="sxs-lookup"><span data-stu-id="a6517-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="a6517-115">[設定警示](app-insights-alerts.md) </span><span class="sxs-lookup"><span data-stu-id="a6517-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="a6517-116">我的 app 發生事件時寄送電子郵件</span><span class="sxs-lookup"><span data-stu-id="a6517-116">Email on an event in my app</span></span>
<span data-ttu-id="a6517-117">我們假設您想要在特定事件發生時收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a6517-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="a6517-118">Application Insights 並未直接提供此功能，但它可 [在計量超過某個閾值時傳送警示](app-insights-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="a6517-119">您可以針對 [自訂計量](app-insights-api-custom-events-metrics.md#trackmetric)設定警示，而不是自訂事件。</span><span class="sxs-lookup"><span data-stu-id="a6517-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="a6517-120">撰寫一些程式碼以在事件發生時增加計量：</span><span class="sxs-lookup"><span data-stu-id="a6517-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="a6517-121">或：</span><span class="sxs-lookup"><span data-stu-id="a6517-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="a6517-122">因為警示有兩個狀態，所以當您考慮讓警示結束時必須傳送較低的值：</span><span class="sxs-lookup"><span data-stu-id="a6517-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="a6517-123">在 [計量總管](app-insights-metrics-explorer.md) 中建立圖表來查看您的警示：</span><span class="sxs-lookup"><span data-stu-id="a6517-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="a6517-124">現在設定警示在計量一段短時間高於中間值時引發：</span><span class="sxs-lookup"><span data-stu-id="a6517-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="a6517-125">將平均期間設定為最小值。</span><span class="sxs-lookup"><span data-stu-id="a6517-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="a6517-126">您就會在計量高於和低於閾值時收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a6517-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="a6517-127">考慮事項：</span><span class="sxs-lookup"><span data-stu-id="a6517-127">Some points to consider:</span></span>

* <span data-ttu-id="a6517-128">警示有兩種狀態 (「警示」和「良好」)。</span><span class="sxs-lookup"><span data-stu-id="a6517-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="a6517-129">只有在收到計量時才會評估狀態。</span><span class="sxs-lookup"><span data-stu-id="a6517-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="a6517-130">只有在狀態變更時才會傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a6517-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="a6517-131">這是為什麼您必須同時傳送高值和低值的計量。</span><span class="sxs-lookup"><span data-stu-id="a6517-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="a6517-132">若要評估警示，會採用收到的值除以先前的期間來獲得平均值。</span><span class="sxs-lookup"><span data-stu-id="a6517-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="a6517-133">因為每次收到計量時都會進行計算，所以傳送電子郵件的頻率會比您設定的期間還要高。</span><span class="sxs-lookup"><span data-stu-id="a6517-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="a6517-134">由於「警示」和「良好」都會傳送電子郵件，所以您可能要以兩個狀態的條件來重新思考單次發生的事件。</span><span class="sxs-lookup"><span data-stu-id="a6517-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="a6517-135">例如，不要採用「作業完成」事件，而採用「作業進行中」的條件，您就可以在工作開始和結束時收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a6517-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="a6517-136">自動設定警示</span><span class="sxs-lookup"><span data-stu-id="a6517-136">Set up alerts automatically</span></span>
[<span data-ttu-id="a6517-137">使用 PowerShell 建立新的警示</span><span class="sxs-lookup"><span data-stu-id="a6517-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="a6517-138">使用 PowerShell 管理 Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6517-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="a6517-139">建立新的資源</span><span class="sxs-lookup"><span data-stu-id="a6517-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="a6517-140">建立新的警示</span><span class="sxs-lookup"><span data-stu-id="a6517-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="a6517-141">區分不同版本的遙測</span><span class="sxs-lookup"><span data-stu-id="a6517-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="a6517-142">應用程式中的多個角色︰使用單一 Application Insights 資源，並依據 cloud_Rolename 進行篩選。</span><span class="sxs-lookup"><span data-stu-id="a6517-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="a6517-143">深入了解</span><span class="sxs-lookup"><span data-stu-id="a6517-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="a6517-144">區分開發、測試和發行版本︰使用不同的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="a6517-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="a6517-145">從 web.config 挑選檢測金鑰。[深入了解](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="a6517-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="a6517-146">報告組建版本︰使用遙測初始設定式新增屬性。</span><span class="sxs-lookup"><span data-stu-id="a6517-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="a6517-147">深入了解</span><span class="sxs-lookup"><span data-stu-id="a6517-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="a6517-148">監視後端伺服器與桌面應用程式</span><span class="sxs-lookup"><span data-stu-id="a6517-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="a6517-149">[使用 Windows Server SDK 模組](app-insights-windows-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="a6517-150">顯現資料</span><span class="sxs-lookup"><span data-stu-id="a6517-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="a6517-151">具有來自多個 App 之計量的儀表板</span><span class="sxs-lookup"><span data-stu-id="a6517-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="a6517-152">在 [計量總管](app-insights-metrics-explorer.md)中，自訂圖表並將它儲存為我的最愛。</span><span class="sxs-lookup"><span data-stu-id="a6517-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="a6517-153">將它釘選到 Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="a6517-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="a6517-154">資料來自其他來源和 Application Insights 的儀表板</span><span class="sxs-lookup"><span data-stu-id="a6517-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="a6517-155">[將遙測匯出至 Power Bi](app-insights-export-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="a6517-156">或</span><span class="sxs-lookup"><span data-stu-id="a6517-156">Or</span></span>

* <span data-ttu-id="a6517-157">使用 SharePoint 做為您的儀表板，在 SharePoint web 組件中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="a6517-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="a6517-158">[使用連續的匯出和資料流分析來匯出至 SQL](app-insights-code-sample-export-sql-stream-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="a6517-159">使用 PowerView 來檢查資料庫，並建立適用於 PowerView 的 SharePoint web 組件。</span><span class="sxs-lookup"><span data-stu-id="a6517-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="a6517-160">篩選出匿名或已驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="a6517-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="a6517-161">如果您的使用者登入，您可以設定[驗證使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)。(它不會自動重新整理)。</span><span class="sxs-lookup"><span data-stu-id="a6517-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="a6517-162">接著，您可以：</span><span class="sxs-lookup"><span data-stu-id="a6517-162">You can then:</span></span>

* <span data-ttu-id="a6517-163">搜尋特定的使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="a6517-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="a6517-164">篩選匿名或已驗證使用者的計量</span><span class="sxs-lookup"><span data-stu-id="a6517-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="a6517-165">修改屬性名稱或值</span><span class="sxs-lookup"><span data-stu-id="a6517-165">Modify property names or values</span></span>
<span data-ttu-id="a6517-166">建立 [篩選器](app-insights-api-filtering-sampling.md#filtering)。</span><span class="sxs-lookup"><span data-stu-id="a6517-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="a6517-167">這可讓您先修改或篩選遙測，然後再將它從您的應用程式傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="a6517-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="a6517-168">列出特定使用者和其使用方式</span><span class="sxs-lookup"><span data-stu-id="a6517-168">List specific users and their usage</span></span>
<span data-ttu-id="a6517-169">如果您只想要[搜尋特定使用者](#search-specific-users)，就可以設定[驗證使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)。</span><span class="sxs-lookup"><span data-stu-id="a6517-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="a6517-170">如果您想要使用者清單以及像是他們查看過哪些頁面或登入頻率等資料，則有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="a6517-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="a6517-171">[設定驗證使用者識別碼](app-insights-api-custom-events-metrics.md#authenticated-users)、[匯出到資料庫](app-insights-code-sample-export-sql-stream-analytics.md)，然後使用適當的工具來分析使用者資料。</span><span class="sxs-lookup"><span data-stu-id="a6517-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="a6517-172">如果您只有少數的使用者，則可傳送自訂事件或計量、使用感興趣的資料做為計量值或事件名稱，然後設定使用者識別碼做為屬性。</span><span class="sxs-lookup"><span data-stu-id="a6517-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="a6517-173">若要分析頁面檢視，可取代標準的 JavaScript trackPageView 呼叫。</span><span class="sxs-lookup"><span data-stu-id="a6517-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="a6517-174">若要分析伺服器端遙測，可使用遙測初始設定式，將使用者識別碼新增至所有伺服器遙測。</span><span class="sxs-lookup"><span data-stu-id="a6517-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="a6517-175">然後您可以篩選與分割關於使用者識別碼的計量資訊和搜尋。</span><span class="sxs-lookup"><span data-stu-id="a6517-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="a6517-176">降低從我的 App 到 Application Insights 的流量</span><span class="sxs-lookup"><span data-stu-id="a6517-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="a6517-177">在 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)中，停用任何您不需要的模組，例如效能計數器收集器。</span><span class="sxs-lookup"><span data-stu-id="a6517-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="a6517-178">使用 SDK 中的 [取樣和篩選](app-insights-api-filtering-sampling.md) 。</span><span class="sxs-lookup"><span data-stu-id="a6517-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="a6517-179">您在網頁中，限制針對每個頁面檢視回報的 Ajax 呼叫次數。</span><span class="sxs-lookup"><span data-stu-id="a6517-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="a6517-180">在 `instrumentationKey:...` 之後的指令碼片段中，插入：`,maxAjaxCallsPerView:3` (或適當的數字)。</span><span class="sxs-lookup"><span data-stu-id="a6517-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="a6517-181">如果您使用的是 [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric)，請在傳送結果之前，先計算計量值批次的彙總。</span><span class="sxs-lookup"><span data-stu-id="a6517-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="a6517-182">有一個 TrackMetric() 的多載是針對該動作所提供。</span><span class="sxs-lookup"><span data-stu-id="a6517-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="a6517-183">深入了解 [價格和配額](app-insights-pricing.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="a6517-184">停用遙測</span><span class="sxs-lookup"><span data-stu-id="a6517-184">Disable telemetry</span></span>
<span data-ttu-id="a6517-185">若要從伺服器 **動態停止和開始** 收集及傳輸遙測資料：</span><span class="sxs-lookup"><span data-stu-id="a6517-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="a6517-186">若要 **停用選取的標準收集器** (例如效能計數器、HTTP 要求或相依性)，請刪除或註解化 [ApplicationInsights.config](app-insights-api-custom-events-metrics.md)中的相關行。例如，如果您想要傳送自己的 TrackRequest 資料，可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="a6517-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="a6517-187">檢視系統效能計數器</span><span class="sxs-lookup"><span data-stu-id="a6517-187">View system performance counters</span></span>
<span data-ttu-id="a6517-188">您可以在計量總管中顯示的計量資訊是一組系統效能計數器。</span><span class="sxs-lookup"><span data-stu-id="a6517-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="a6517-189">有一個預先定義且標題為 **伺服器** 的刀鋒視窗會顯示它們其中幾個。</span><span class="sxs-lookup"><span data-stu-id="a6517-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![開啟 Application Insights 資源並按一下伺服器](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="a6517-191">如果您看不到效能計數器資料</span><span class="sxs-lookup"><span data-stu-id="a6517-191">If you see no performance counter data</span></span>
* <span data-ttu-id="a6517-192">**IIS 伺服器** 。</span><span class="sxs-lookup"><span data-stu-id="a6517-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="a6517-193">[安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="a6517-194">**Azure 網站** - 我們尚未支援效能計數器。</span><span class="sxs-lookup"><span data-stu-id="a6517-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="a6517-195">您可以取得數個計量來做為 Azure 網站控制台的標準部分。</span><span class="sxs-lookup"><span data-stu-id="a6517-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="a6517-196">**Unix 伺服器** - [安裝 collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="a6517-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="a6517-197">顯示更多效能計數器</span><span class="sxs-lookup"><span data-stu-id="a6517-197">To display more performance counters</span></span>
* <span data-ttu-id="a6517-198">首先， [新增圖表](app-insights-metrics-explorer.md) ，並查看計數器是否位於我們提供的基本組合中。</span><span class="sxs-lookup"><span data-stu-id="a6517-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="a6517-199">如果沒有，請[將計數器加入效能計數器模組所收集的組合中](app-insights-performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="a6517-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
