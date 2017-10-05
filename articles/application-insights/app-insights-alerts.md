---
title: "在 Azure Application Insights 中設定警示 | Microsoft Docs"
description: "獲知回應時間緩慢、例外狀況，以及 Web 應用程式中的其他效能或使用量變更。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: c8386ffc5d68260eeb75edf7efb77db1163dcef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="set-alerts-in-application-insights"></a><span data-ttu-id="1d573-103">在 Application Insights 中設定警示</span><span class="sxs-lookup"><span data-stu-id="1d573-103">Set Alerts in Application Insights</span></span>
<span data-ttu-id="1d573-104">[Azure Application Insights][start] 可在 Web 應用程式中發生效能或使用量計量變更時對您發出警示。</span><span class="sxs-lookup"><span data-stu-id="1d573-104">[Azure Application Insights][start] can alert you to changes in performance or usage metrics in your web app.</span></span> 

<span data-ttu-id="1d573-105">Application Insights 會在[多種平台][platforms]上監視即時應用程式，協助您診斷效能問題，以及了解使用模式。</span><span class="sxs-lookup"><span data-stu-id="1d573-105">Application Insights monitors your live app on a [wide variety of platforms][platforms] to help you diagnose performance issues and understand usage patterns.</span></span>

<span data-ttu-id="1d573-106">共有三種警示︰</span><span class="sxs-lookup"><span data-stu-id="1d573-106">There are three kinds of alerts:</span></span>

* <span data-ttu-id="1d573-107">**計量警示**會在計量超出某些期間的臨界值 (例如回應時間、例外狀況計數、CPU 使用量或頁面檢視) 的時候通知您。</span><span class="sxs-lookup"><span data-stu-id="1d573-107">**Metric alerts** tell you when a metric crosses a threshold value for some period - such as response times, exception counts, CPU usage, or page views.</span></span> 
* <span data-ttu-id="1d573-108">[**Web 測試**][availability]會在您的網站無法在網際網路上使用或回應速度很慢時通知您。</span><span class="sxs-lookup"><span data-stu-id="1d573-108">[**Web tests**][availability] tell you when your site is unavailable on the internet, or responding slowly.</span></span> <span data-ttu-id="1d573-109">[深入了解][availability]。</span><span class="sxs-lookup"><span data-stu-id="1d573-109">[Learn more][availability].</span></span>
* <span data-ttu-id="1d573-110">[**主動診斷**](app-insights-proactive-diagnostics.md)會自動設定成通知您異常的效能模式。</span><span class="sxs-lookup"><span data-stu-id="1d573-110">[**Proactive diagnostics**](app-insights-proactive-diagnostics.md) are configured automatically to notify you about unusual performance patterns.</span></span>

<span data-ttu-id="1d573-111">在本文中，我們著重於計量警示。</span><span class="sxs-lookup"><span data-stu-id="1d573-111">We focus on metric alerts in this article.</span></span>

## <a name="set-a-metric-alert"></a><span data-ttu-id="1d573-112">設定計量警示</span><span class="sxs-lookup"><span data-stu-id="1d573-112">Set a Metric alert</span></span>
<span data-ttu-id="1d573-113">開啟 [警示規則] 刀鋒視窗，然後使用 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d573-113">Open the Alert rules blade, and then use the add button.</span></span> 

![在 [警示規則] 刀鋒視窗中，按一下 [新增警示]。](./media/app-insights-alerts/01-set-metric.png)

* <span data-ttu-id="1d573-116">設定其他屬性之前的資源。</span><span class="sxs-lookup"><span data-stu-id="1d573-116">Set the resource before the other properties.</span></span> <span data-ttu-id="1d573-117">**選擇 "(元件)" 資源** 。</span><span class="sxs-lookup"><span data-stu-id="1d573-117">**Choose the "(components)" resource** if you want to set alerts on performance or usage metrics.</span></span>
* <span data-ttu-id="1d573-118">您提供的警示名稱必須為資源群組 (不只是您的應用程式) 中的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="1d573-118">The name that you give to the alert must be unique within the resource group (not just your application).</span></span>
* <span data-ttu-id="1d573-119">請小心注意系統要求您輸入臨界值時所使用的單位。</span><span class="sxs-lookup"><span data-stu-id="1d573-119">Be careful to note the units in which you're asked to enter the threshold value.</span></span>
* <span data-ttu-id="1d573-120">如果您勾選 [電子郵件擁有者] 方塊，系統會透過電子郵件，將警示傳給每個可以存取此資源群組的人員。</span><span class="sxs-lookup"><span data-stu-id="1d573-120">If you check the box "Email owners...", alerts are sent by email to everyone who has access to this resource group.</span></span> <span data-ttu-id="1d573-121">若要展開這一組人員，請將他們新增至 [資源群組或訂用帳戶](app-insights-resources-roles-access-control.md) (而非資源)。</span><span class="sxs-lookup"><span data-stu-id="1d573-121">To expand this set of people, add them to the [resource group or subscription](app-insights-resources-roles-access-control.md) (not the resource).</span></span>
* <span data-ttu-id="1d573-122">如果您指定 [其他電子郵件]，系統會將警示傳送給這些人員或群組 (無論您是否核取 [電子郵件擁有者] 方塊)。</span><span class="sxs-lookup"><span data-stu-id="1d573-122">If you specify "Additional emails", alerts are sent to those individuals or groups (whether or not you checked the "email owners..." box).</span></span> 
* <span data-ttu-id="1d573-123">如果您已設定回應通知的 Web 應用程式，請設定 [Webhook 位址](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="1d573-123">Set a [webhook address](../monitoring-and-diagnostics/insights-webhooks-alerts.md) if you have set up a web app that responds to alerts.</span></span> <span data-ttu-id="1d573-124">系統會在警示啟動和解決時加以呼叫。</span><span class="sxs-lookup"><span data-stu-id="1d573-124">It is called both when the alert is Activated and when it is Resolved.</span></span> <span data-ttu-id="1d573-125">(不過請注意，查詢參數目前不會當作 Webhook 屬性傳遞)。</span><span class="sxs-lookup"><span data-stu-id="1d573-125">(But note that at present, query parameters are not passed through as webhook properties.)</span></span>
* <span data-ttu-id="1d573-126">您可以停用或啟用警示：請參閱位於刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d573-126">You can Disable or Enable the alert: see the buttons at the top of the blade.</span></span>

<bpt id="p1">*</bpt>I don't see the Add Alert button.<ept id="p1">*</ept> 

* <span data-ttu-id="1d573-128">您是否使用組織帳戶？</span><span class="sxs-lookup"><span data-stu-id="1d573-128">Are you using an organizational account?</span></span> <span data-ttu-id="1d573-129">如果您有這個應用程式資源的擁有者或參與者存取權，您可以設定警示。</span><span class="sxs-lookup"><span data-stu-id="1d573-129">You can set alerts if you have owner or contributor access to this application resource.</span></span> <span data-ttu-id="1d573-130">請看一下 [存取控制] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1d573-130">Take a look at the Access Control blade.</span></span> <span data-ttu-id="1d573-131">[深入了解存取控制][roles]。</span><span class="sxs-lookup"><span data-stu-id="1d573-131">[Learn about access control][roles].</span></span>

> [!NOTE]
> <span data-ttu-id="1d573-132">在 [警示] 刀鋒視窗中，您會看到已經設定警示︰[主動診斷](app-insights-proactive-failure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="1d573-132">In the alerts blade, you see that there's already an alert set up: [Proactive Diagnostics](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="1d573-133">自動警示會監視要求失敗率這一個特定度量。</span><span class="sxs-lookup"><span data-stu-id="1d573-133">The automatic alert monitors one particular metric, request failure rate.</span></span> <span data-ttu-id="1d573-134">除非您決定要停用主動警示，否則不需要設定自己的要求失敗率警示。</span><span class="sxs-lookup"><span data-stu-id="1d573-134">Unless you decide to disable the proactive alert, you don't need to set your own alert on request failure rate.</span></span> 
> 
> 

## <a name="see-your-alerts"></a><span data-ttu-id="1d573-135">查看您的警示</span><span class="sxs-lookup"><span data-stu-id="1d573-135">See your alerts</span></span>
<span data-ttu-id="1d573-136">當警示在非作用中與作用中之間變更狀態時，您會收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="1d573-136">You get an email when an alert changes state between inactive and active.</span></span> 

<span data-ttu-id="1d573-137">每個警示目前的狀態都顯示在警示規則刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="1d573-137">The current state of each alert is shown in the Alert rules blade.</span></span>

<span data-ttu-id="1d573-138">警示下拉式清單中有最近活動的摘要：</span><span class="sxs-lookup"><span data-stu-id="1d573-138">There's a summary of recent activity in the alerts drop-down:</span></span>

![警示下拉式清單](./media/app-insights-alerts/010-alert-drop.png)

<span data-ttu-id="1d573-140">狀態變更的歷程記錄位於活動記錄檔中：</span><span class="sxs-lookup"><span data-stu-id="1d573-140">The history of state changes is in the Activity Log:</span></span>

![在 [概觀] 刀鋒視窗中，按一下 [設定]、[稽核記錄檔]](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a><span data-ttu-id="1d573-142">警示的運作方式</span><span class="sxs-lookup"><span data-stu-id="1d573-142">How alerts work</span></span>
* <span data-ttu-id="1d573-143">警示有三種狀態：「永遠不啟動」、「已啟動」和「已解決」。</span><span class="sxs-lookup"><span data-stu-id="1d573-143">An alert has three states: "Never activated", "Activated", and "Resolved."</span></span> <span data-ttu-id="1d573-144">「已啟動」表示您指定的條件在上次評估時為 true。</span><span class="sxs-lookup"><span data-stu-id="1d573-144">Activated means the condition you specified was true, when it was last evaluated.</span></span>
* <span data-ttu-id="1d573-145">警示狀態變更時，會產生通知。</span><span class="sxs-lookup"><span data-stu-id="1d573-145">A notification is generated when an alert changes state.</span></span> <span data-ttu-id="1d573-146">(如果警示條件在建立警示時已為 true，您可能在條件變為 false 之前都不會得到通知。)</span><span class="sxs-lookup"><span data-stu-id="1d573-146">(If the alert condition was already true when you created the alert, you might not get a notification until the condition goes false.)</span></span>
* <span data-ttu-id="1d573-147">如果您已勾選電子郵件方塊或提供電子郵件地址，則每個通知都會產生一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="1d573-147">Each notification generates an email if you checked the emails box, or provided email addresses.</span></span> <span data-ttu-id="1d573-148">您也可以於 [通知] 查看下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1d573-148">You can also look at the Notifications drop-down list.</span></span>
* <span data-ttu-id="1d573-149">每次度量抵達時都會評估警示，除此之外則無。</span><span class="sxs-lookup"><span data-stu-id="1d573-149">An alert is evaluated each time a metric arrives, but not otherwise.</span></span>
* <span data-ttu-id="1d573-150">評估會彙總前一個期間的度量，然後將其與臨界值進行比較，以決定新的狀態。</span><span class="sxs-lookup"><span data-stu-id="1d573-150">The evaluation aggregates the metric over the preceding period, and then compares it to the threshold to determine the new state.</span></span>
* <span data-ttu-id="1d573-151">您選擇的期間會指定彙總度量的間隔。</span><span class="sxs-lookup"><span data-stu-id="1d573-151">The period that you choose specifies the interval over which metrics are aggregated.</span></span> <span data-ttu-id="1d573-152">它並不會影響評估警示的頻率：這會根據度量抵達的頻率而定。</span><span class="sxs-lookup"><span data-stu-id="1d573-152">It doesn't affect how often the alert is evaluated: that depends on the frequency of arrival of metrics.</span></span>
* <span data-ttu-id="1d573-153">如果經過一段時間後沒有特定度量的資料到達，此間距會在警示評估上，以及在度量總管的圖表上有不同的效果。</span><span class="sxs-lookup"><span data-stu-id="1d573-153">If no data arrives for a particular metric for some time, the gap has different effects on alert evaluation and on the charts in metric explorer.</span></span> <span data-ttu-id="1d573-154">在計量總管中，如果沒看到資料的時間超過圖表的取樣間隔時間，則圖表會顯示 0 值。</span><span class="sxs-lookup"><span data-stu-id="1d573-154">In metric explorer, if no data is seen for longer than the chart's sampling interval, the chart shows a value of 0.</span></span> <span data-ttu-id="1d573-155">但是以相同度量為基礎的警示不會重新接受評估，而且警示的狀態會維持不變。</span><span class="sxs-lookup"><span data-stu-id="1d573-155">But an alert based on the same metric is not be reevaluated, and the alert's state remains unchanged.</span></span> 
  
    <span data-ttu-id="1d573-156">當資料終於抵達時，圖表會跳回非零的值。</span><span class="sxs-lookup"><span data-stu-id="1d573-156">When data eventually arrives, the chart jumps back to a non-zero value.</span></span> <span data-ttu-id="1d573-157">警示的評估作業會依您指定的期間，並根據可用的資料來進行。</span><span class="sxs-lookup"><span data-stu-id="1d573-157">The alert evaluates based on the data available for the period you specified.</span></span> <span data-ttu-id="1d573-158">如果新的資料點是期間內唯一可用的資料點，則彙總只會以該資料點為基礎。</span><span class="sxs-lookup"><span data-stu-id="1d573-158">If the new data point is the only one available in the period, the aggregate is based just on that data point.</span></span>
* <span data-ttu-id="1d573-159">即使您設定的期間較長，警示也可能會在警示和良好狀態之間經常變動。</span><span class="sxs-lookup"><span data-stu-id="1d573-159">An alert can flicker frequently between alert and healthy states, even if you set a long period.</span></span> <span data-ttu-id="1d573-160">如果度量值徘徊在臨界值附近，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="1d573-160">This can happen if the metric value hovers around the threshold.</span></span> <span data-ttu-id="1d573-161">臨界值中沒有任何磁滯：轉換為警示時的值會與轉換為良好時的值相同。</span><span class="sxs-lookup"><span data-stu-id="1d573-161">There is no hysteresis in the threshold: the transition to alert happens at the same value as the transition to healthy.</span></span>

## <a name="what-are-good-alerts-to-set"></a><span data-ttu-id="1d573-162">哪些是好的設定警示？</span><span class="sxs-lookup"><span data-stu-id="1d573-162">What are good alerts to set?</span></span>
<span data-ttu-id="1d573-163">這取決於您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d573-163">It depends on your application.</span></span> <span data-ttu-id="1d573-164">開始時，最好不要設定太多度量。</span><span class="sxs-lookup"><span data-stu-id="1d573-164">To start with, it's best not to set too many metrics.</span></span> <span data-ttu-id="1d573-165">花點時間查看您的應用程式執行時的度量圖表，以了解正常運作時的情形。</span><span class="sxs-lookup"><span data-stu-id="1d573-165">Spend some time looking at your metric charts while your app is running, to get a feel for how it behaves normally.</span></span> <span data-ttu-id="1d573-166">這個做法可協助您找出改善其效能的方式。</span><span class="sxs-lookup"><span data-stu-id="1d573-166">This practice helps you find ways to improve its performance.</span></span> <span data-ttu-id="1d573-167">然後設定警示，在度量偏離正常區域時通知您。</span><span class="sxs-lookup"><span data-stu-id="1d573-167">Then set up alerts to tell you when the metrics go outside the normal zone.</span></span> 

<span data-ttu-id="1d573-168">熱門的警示包括：</span><span class="sxs-lookup"><span data-stu-id="1d573-168">Popular alerts include:</span></span>

* <span data-ttu-id="1d573-169">[瀏覽器計量][client]，適合用於 Web 應用程式，尤其是瀏覽器**頁面載入時間**。</span><span class="sxs-lookup"><span data-stu-id="1d573-169">[Browser metrics][client], especially Browser **page load times**, are good for web applications.</span></span> <span data-ttu-id="1d573-170">如果您的分頁有許多指令碼，您應該尋找**瀏覽器例外狀況**。</span><span class="sxs-lookup"><span data-stu-id="1d573-170">If your page has many scripts, you should look for **browser exceptions**.</span></span> <span data-ttu-id="1d573-171">若要取得這些計量和警示，您必須設定[網頁監視][client]。</span><span class="sxs-lookup"><span data-stu-id="1d573-171">In order to get these metrics and alerts, you have to set up [web page monitoring][client].</span></span>
* <span data-ttu-id="1d573-172">Web 應用程式伺服器端的**伺服器回應時間**。</span><span class="sxs-lookup"><span data-stu-id="1d573-172">**Server response time** for the server side of web applications.</span></span> <span data-ttu-id="1d573-173">以及設定警示，注意這些計量，以查看高要求率時的差異是否不成比例：差異可能表示您的應用程式資源不足。</span><span class="sxs-lookup"><span data-stu-id="1d573-173">As well as setting up alerts, keep an eye on this metric to see if it varies disproportionately with high request rates: variation might indicate that your app is running out of resources.</span></span> 
* <span data-ttu-id="1d573-174">**伺服器例外狀況** - 若要查看它們，您只需要進行一些 [額外設定](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="1d573-174">**Server exceptions** - to see them, you have to do some [additional setup](app-insights-asp-net-exceptions.md).</span></span>

<span data-ttu-id="1d573-175">別忘了，[主動失敗率診斷](app-insights-proactive-failure-diagnostics.md)會自動監視應用程式以失敗碼回應要求的速率。</span><span class="sxs-lookup"><span data-stu-id="1d573-175">Don't forget that [proactive failure rate diagnostics](app-insights-proactive-failure-diagnostics.md) automatically monitor the rate at which your app responds to requests with failure codes.</span></span> 

## <a name="automation"></a><span data-ttu-id="1d573-176">自動化</span><span class="sxs-lookup"><span data-stu-id="1d573-176">Automation</span></span>
* [<span data-ttu-id="1d573-177">使用 PowerShell 自動設定警示</span><span class="sxs-lookup"><span data-stu-id="1d573-177">Use PowerShell to automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="1d573-178">使用 Webhook 自動回應警示</span><span class="sxs-lookup"><span data-stu-id="1d573-178">Use webhooks to automate responding to alerts</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a><span data-ttu-id="1d573-179">影片</span><span class="sxs-lookup"><span data-stu-id="1d573-179">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a><span data-ttu-id="1d573-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1d573-180">See also</span></span>
* [<span data-ttu-id="1d573-181">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="1d573-181">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="1d573-182">自動化設定警示</span><span class="sxs-lookup"><span data-stu-id="1d573-182">Automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="1d573-183">主動診斷</span><span class="sxs-lookup"><span data-stu-id="1d573-183">Proactive diagnostics</span></span>](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

