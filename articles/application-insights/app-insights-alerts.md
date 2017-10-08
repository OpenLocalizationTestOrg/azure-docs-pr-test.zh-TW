---
title: "在 Azure Application Insights aaaSet 警示 |Microsoft 文件"
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
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a><span data-ttu-id="bda50-103">在 Application Insights 中設定警示</span><span class="sxs-lookup"><span data-stu-id="bda50-103">Set Alerts in Application Insights</span></span>
<span data-ttu-id="bda50-104">[Azure 的 Application Insights] [ start]可以提醒您 toochanges 的 web 應用程式中的效能或使用量度量。</span><span class="sxs-lookup"><span data-stu-id="bda50-104">[Azure Application Insights][start] can alert you toochanges in performance or usage metrics in your web app.</span></span> 

<span data-ttu-id="bda50-105">Application Insights 監視即時應用程式上[各種不同的平台][ platforms] toohelp 您診斷效能問題，並了解使用模式。</span><span class="sxs-lookup"><span data-stu-id="bda50-105">Application Insights monitors your live app on a [wide variety of platforms][platforms] toohelp you diagnose performance issues and understand usage patterns.</span></span>

<span data-ttu-id="bda50-106">共有三種警示︰</span><span class="sxs-lookup"><span data-stu-id="bda50-106">There are three kinds of alerts:</span></span>

* <span data-ttu-id="bda50-107">**計量警示**會在計量超出某些期間的臨界值 (例如回應時間、例外狀況計數、CPU 使用量或頁面檢視) 的時候通知您。</span><span class="sxs-lookup"><span data-stu-id="bda50-107">**Metric alerts** tell you when a metric crosses a threshold value for some period - such as response times, exception counts, CPU usage, or page views.</span></span> 
* <span data-ttu-id="bda50-108">[**Web 測試**] [ availability]告訴您無法在 hello 上使用您的網站是否網際網路或回應速度較慢。</span><span class="sxs-lookup"><span data-stu-id="bda50-108">[**Web tests**][availability] tell you when your site is unavailable on hello internet, or responding slowly.</span></span> <span data-ttu-id="bda50-109">[深入了解][availability]。</span><span class="sxs-lookup"><span data-stu-id="bda50-109">[Learn more][availability].</span></span>
* <span data-ttu-id="bda50-110">[**主動式診斷**](app-insights-proactive-diagnostics.md)會自動設定 toonotify 您有關不尋常的效能模式。</span><span class="sxs-lookup"><span data-stu-id="bda50-110">[**Proactive diagnostics**](app-insights-proactive-diagnostics.md) are configured automatically toonotify you about unusual performance patterns.</span></span>

<span data-ttu-id="bda50-111">在本文中，我們著重於計量警示。</span><span class="sxs-lookup"><span data-stu-id="bda50-111">We focus on metric alerts in this article.</span></span>

## <a name="set-a-metric-alert"></a><span data-ttu-id="bda50-112">設定計量警示</span><span class="sxs-lookup"><span data-stu-id="bda50-112">Set a Metric alert</span></span>
<span data-ttu-id="bda50-113">開啟 hello 警示規則刀鋒視窗中，然後再使用 hello 加入按鈕。</span><span class="sxs-lookup"><span data-stu-id="bda50-113">Open hello Alert rules blade, and then use hello add button.</span></span> 

![在 hello 警示規則刀鋒視窗中，選擇 [新增警示]。](./media/app-insights-alerts/01-set-metric.png)

* <span data-ttu-id="bda50-116">設定前 hello hello 資源的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="bda50-116">Set hello resource before hello other properties.</span></span> <span data-ttu-id="bda50-117">**選擇 hello 」 （元件） 」 資源**如果您想 tooset 效能或使用量度量的警示。</span><span class="sxs-lookup"><span data-stu-id="bda50-117">**Choose hello "(components)" resource** if you want tooset alerts on performance or usage metrics.</span></span>
* <span data-ttu-id="bda50-118">您提供給 toohello 警示的 hello 名稱必須是唯一 hello （不只是您的應用程式） 的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="bda50-118">hello name that you give toohello alert must be unique within hello resource group (not just your application).</span></span>
* <span data-ttu-id="bda50-119">能謹慎 toonote hello 單位中，系統會詢問 tooenter hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="bda50-119">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>
* <span data-ttu-id="bda50-120">如果您核取 hello 方塊 」 電子郵件擁有者..."，警示會傳送電子郵件 tooeveryone 擁有存取 toothis 資源群組。</span><span class="sxs-lookup"><span data-stu-id="bda50-120">If you check hello box "Email owners...", alerts are sent by email tooeveryone who has access toothis resource group.</span></span> <span data-ttu-id="bda50-121">tooexpand 這設定的人員，將它們加入 toohello[資源群組或訂用帳戶](app-insights-resources-roles-access-control.md)(不 hello 資源)。</span><span class="sxs-lookup"><span data-stu-id="bda50-121">tooexpand this set of people, add them toohello [resource group or subscription](app-insights-resources-roles-access-control.md) (not hello resource).</span></span>
* <span data-ttu-id="bda50-122">如果您指定 「 其他電子郵件 」，則會收到通知，toothose 個人或群組 （不論您核取 hello 」 電子郵件擁有者..."方塊）。</span><span class="sxs-lookup"><span data-stu-id="bda50-122">If you specify "Additional emails", alerts are sent toothose individuals or groups (whether or not you checked hello "email owners..." box).</span></span> 
* <span data-ttu-id="bda50-123">設定[webhook 位址](../monitoring-and-diagnostics/insights-webhooks-alerts.md)如果您已設定 web 應用程式回應 tooalerts。</span><span class="sxs-lookup"><span data-stu-id="bda50-123">Set a [webhook address](../monitoring-and-diagnostics/insights-webhooks-alerts.md) if you have set up a web app that responds tooalerts.</span></span> <span data-ttu-id="bda50-124">它會呼叫啟動 hello 警示和時獲得解決。</span><span class="sxs-lookup"><span data-stu-id="bda50-124">It is called both when hello alert is Activated and when it is Resolved.</span></span> <span data-ttu-id="bda50-125">(不過請注意，查詢參數目前不會當作 Webhook 屬性傳遞)。</span><span class="sxs-lookup"><span data-stu-id="bda50-125">(But note that at present, query parameters are not passed through as webhook properties.)</span></span>
* <span data-ttu-id="bda50-126">您可以停用或啟用 hello 警示： 請參閱 < hello 在 hello hello 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bda50-126">You can Disable or Enable hello alert: see hello buttons at hello top of hello blade.</span></span>

<span data-ttu-id="bda50-127">*看不見 hello 新增警示 按鈕。*</span><span class="sxs-lookup"><span data-stu-id="bda50-127">*I don't see hello Add Alert button.*</span></span> 

* <span data-ttu-id="bda50-128">您是否使用組織帳戶？</span><span class="sxs-lookup"><span data-stu-id="bda50-128">Are you using an organizational account?</span></span> <span data-ttu-id="bda50-129">如果您有擁有者或參與者存取 toothis 應用程式資源，您可以設定警示。</span><span class="sxs-lookup"><span data-stu-id="bda50-129">You can set alerts if you have owner or contributor access toothis application resource.</span></span> <span data-ttu-id="bda50-130">看看 hello 存取控制 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bda50-130">Take a look at hello Access Control blade.</span></span> <span data-ttu-id="bda50-131">[深入了解存取控制][roles]。</span><span class="sxs-lookup"><span data-stu-id="bda50-131">[Learn about access control][roles].</span></span>

> [!NOTE]
> <span data-ttu-id="bda50-132">在 hello 警示刀鋒視窗中，您看到已有的警示集：[主動式診斷](app-insights-proactive-failure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="bda50-132">In hello alerts blade, you see that there's already an alert set up: [Proactive Diagnostics](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="bda50-133">hello 自動警示監視一個特定度量，要求失敗率。</span><span class="sxs-lookup"><span data-stu-id="bda50-133">hello automatic alert monitors one particular metric, request failure rate.</span></span> <span data-ttu-id="bda50-134">除非您決定 toodisable hello 主動式警示，您不需要 tooset 上要求失敗率警示。</span><span class="sxs-lookup"><span data-stu-id="bda50-134">Unless you decide toodisable hello proactive alert, you don't need tooset your own alert on request failure rate.</span></span> 
> 
> 

## <a name="see-your-alerts"></a><span data-ttu-id="bda50-135">查看您的警示</span><span class="sxs-lookup"><span data-stu-id="bda50-135">See your alerts</span></span>
<span data-ttu-id="bda50-136">當警示在非作用中與作用中之間變更狀態時，您會收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="bda50-136">You get an email when an alert changes state between inactive and active.</span></span> 

<span data-ttu-id="bda50-137">hello 警示規則 刀鋒視窗會顯示 hello 的每個警示的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="bda50-137">hello current state of each alert is shown in hello Alert rules blade.</span></span>

<span data-ttu-id="bda50-138">下拉式清單沒有 hello 警示中的最近活動的摘要：</span><span class="sxs-lookup"><span data-stu-id="bda50-138">There's a summary of recent activity in hello alerts drop-down:</span></span>

![警示下拉式清單](./media/app-insights-alerts/010-alert-drop.png)

<span data-ttu-id="bda50-140">hello 變更歷程記錄的狀態處於 hello 活動記錄檔：</span><span class="sxs-lookup"><span data-stu-id="bda50-140">hello history of state changes is in hello Activity Log:</span></span>

![在 hello 概觀刀鋒視窗中，按一下 設定，稽核記錄檔](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a><span data-ttu-id="bda50-142">警示的運作方式</span><span class="sxs-lookup"><span data-stu-id="bda50-142">How alerts work</span></span>
* <span data-ttu-id="bda50-143">警示有三種狀態：「永遠不啟動」、「已啟動」和「已解決」。</span><span class="sxs-lookup"><span data-stu-id="bda50-143">An alert has three states: "Never activated", "Activated", and "Resolved."</span></span> <span data-ttu-id="bda50-144">已啟動的方式 hello，已為 true，當上一次評估時指定的條件。</span><span class="sxs-lookup"><span data-stu-id="bda50-144">Activated means hello condition you specified was true, when it was last evaluated.</span></span>
* <span data-ttu-id="bda50-145">警示狀態變更時，會產生通知。</span><span class="sxs-lookup"><span data-stu-id="bda50-145">A notification is generated when an alert changes state.</span></span> <span data-ttu-id="bda50-146">（如果 hello 警示條件已，則為 true，當您建立 hello 警示時，您可能無法取得通知之前 hello 條件變成 false。）</span><span class="sxs-lookup"><span data-stu-id="bda50-146">(If hello alert condition was already true when you created hello alert, you might not get a notification until hello condition goes false.)</span></span>
* <span data-ttu-id="bda50-147">如果您檢查 hello 電子郵件 方塊中，或提供電子郵件地址，每個通知就會產生一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="bda50-147">Each notification generates an email if you checked hello emails box, or provided email addresses.</span></span> <span data-ttu-id="bda50-148">您也可以查看 hello 通知下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bda50-148">You can also look at hello Notifications drop-down list.</span></span>
* <span data-ttu-id="bda50-149">每次度量抵達時都會評估警示，除此之外則無。</span><span class="sxs-lookup"><span data-stu-id="bda50-149">An alert is evaluated each time a metric arrives, but not otherwise.</span></span>
* <span data-ttu-id="bda50-150">hello 評估 hello 前面期間，透過彙總 hello 度量，然後比較 toohello 閾值 toodetermine hello 新狀態。</span><span class="sxs-lookup"><span data-stu-id="bda50-150">hello evaluation aggregates hello metric over hello preceding period, and then compares it toohello threshold toodetermine hello new state.</span></span>
* <span data-ttu-id="bda50-151">您選擇的 hello 期間指定 hello 彙總度量資訊會經過的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="bda50-151">hello period that you choose specifies hello interval over which metrics are aggregated.</span></span> <span data-ttu-id="bda50-152">它並不會影響 hello 警示評估的頻率： hello 抵達的度量的頻率而定。</span><span class="sxs-lookup"><span data-stu-id="bda50-152">It doesn't affect how often hello alert is evaluated: that depends on hello frequency of arrival of metrics.</span></span>
* <span data-ttu-id="bda50-153">如果沒有資料到達特定度量的一些時間，hello 差距就會有警示評估和度量總管 中的 hello 圖表上不同的效果。</span><span class="sxs-lookup"><span data-stu-id="bda50-153">If no data arrives for a particular metric for some time, hello gap has different effects on alert evaluation and on hello charts in metric explorer.</span></span> <span data-ttu-id="bda50-154">在度量總管中，如果沒有資料會超過 hello 圖表的取樣間隔內，看到 hello 圖表可顯示值為 0。</span><span class="sxs-lookup"><span data-stu-id="bda50-154">In metric explorer, if no data is seen for longer than hello chart's sampling interval, hello chart shows a value of 0.</span></span> <span data-ttu-id="bda50-155">但警示根據 hello 相同的度量不會重新評估和 hello 警示的狀態會保持不變。</span><span class="sxs-lookup"><span data-stu-id="bda50-155">But an alert based on hello same metric is not be reevaluated, and hello alert's state remains unchanged.</span></span> 
  
    <span data-ttu-id="bda50-156">當資料最後會到達時，hello 圖表就會跳後 tooa 非零值。</span><span class="sxs-lookup"><span data-stu-id="bda50-156">When data eventually arrives, hello chart jumps back tooa non-zero value.</span></span> <span data-ttu-id="bda50-157">評估 hello 警示根據 hello 資料可供您指定的 hello 週期。</span><span class="sxs-lookup"><span data-stu-id="bda50-157">hello alert evaluates based on hello data available for hello period you specified.</span></span> <span data-ttu-id="bda50-158">如果只有一個可用 hello 內 hello hello 新資料點，彙總的 hello 以只在資料點。</span><span class="sxs-lookup"><span data-stu-id="bda50-158">If hello new data point is hello only one available in hello period, hello aggregate is based just on that data point.</span></span>
* <span data-ttu-id="bda50-159">即使您設定的期間較長，警示也可能會在警示和良好狀態之間經常變動。</span><span class="sxs-lookup"><span data-stu-id="bda50-159">An alert can flicker frequently between alert and healthy states, even if you set a long period.</span></span> <span data-ttu-id="bda50-160">這種情況 hello 公制值停留周圍 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="bda50-160">This can happen if hello metric value hovers around hello threshold.</span></span> <span data-ttu-id="bda50-161">Hello 臨界值中沒有任何 hysteresis: hello 轉換 tooalert 會發生在相同的值為 hello 轉換 toohealthy hello。</span><span class="sxs-lookup"><span data-stu-id="bda50-161">There is no hysteresis in hello threshold: hello transition tooalert happens at hello same value as hello transition toohealthy.</span></span>

## <a name="what-are-good-alerts-tooset"></a><span data-ttu-id="bda50-162">良好的警示 tooset 有哪些？</span><span class="sxs-lookup"><span data-stu-id="bda50-162">What are good alerts tooset?</span></span>
<span data-ttu-id="bda50-163">這取決於您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bda50-163">It depends on your application.</span></span> <span data-ttu-id="bda50-164">toostart，最好不 tooset 太多的度量。</span><span class="sxs-lookup"><span data-stu-id="bda50-164">toostart with, it's best not tooset too many metrics.</span></span> <span data-ttu-id="bda50-165">花點時間查看的度量的圖表，您的應用程式執行時，tooget 感覺如何正常運作。</span><span class="sxs-lookup"><span data-stu-id="bda50-165">Spend some time looking at your metric charts while your app is running, tooget a feel for how it behaves normally.</span></span> <span data-ttu-id="bda50-166">這種作法可協助您找到方式 tooimprove 其效能。</span><span class="sxs-lookup"><span data-stu-id="bda50-166">This practice helps you find ways tooimprove its performance.</span></span> <span data-ttu-id="bda50-167">然後時，設定警示 tootell 您 hello 度量傳送 hello 一般區域外部。</span><span class="sxs-lookup"><span data-stu-id="bda50-167">Then set up alerts tootell you when hello metrics go outside hello normal zone.</span></span> 

<span data-ttu-id="bda50-168">熱門的警示包括：</span><span class="sxs-lookup"><span data-stu-id="bda50-168">Popular alerts include:</span></span>

* <span data-ttu-id="bda50-169">[瀏覽器計量][client]，適合用於 Web 應用程式，尤其是瀏覽器**頁面載入時間**。</span><span class="sxs-lookup"><span data-stu-id="bda50-169">[Browser metrics][client], especially Browser **page load times**, are good for web applications.</span></span> <span data-ttu-id="bda50-170">如果您的分頁有許多指令碼，您應該尋找**瀏覽器例外狀況**。</span><span class="sxs-lookup"><span data-stu-id="bda50-170">If your page has many scripts, you should look for **browser exceptions**.</span></span> <span data-ttu-id="bda50-171">在訂單 tooget 這些度量和警示，您必須 tooset[網頁監視][client]。</span><span class="sxs-lookup"><span data-stu-id="bda50-171">In order tooget these metrics and alerts, you have tooset up [web page monitoring][client].</span></span>
* <span data-ttu-id="bda50-172">**伺服器回應時間**hello 伺服器端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bda50-172">**Server response time** for hello server side of web applications.</span></span> <span data-ttu-id="bda50-173">以及設定警示，請留意這個度量 toosee 如果它會隨著不當比例高要求率： 變化可能表示您的應用程式時用資源不足。</span><span class="sxs-lookup"><span data-stu-id="bda50-173">As well as setting up alerts, keep an eye on this metric toosee if it varies disproportionately with high request rates: variation might indicate that your app is running out of resources.</span></span> 
* <span data-ttu-id="bda50-174">**伺服器例外狀況**-toosee 它們，您有一些 toodo[額外安裝](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="bda50-174">**Server exceptions** - toosee them, you have toodo some [additional setup](app-insights-asp-net-exceptions.md).</span></span>

<span data-ttu-id="bda50-175">請記住，[主動式失敗率診斷](app-insights-proactive-failure-diagnostics.md)自動監視器 hello 速率您的應用程式會回應 toorequests 的失敗碼。</span><span class="sxs-lookup"><span data-stu-id="bda50-175">Don't forget that [proactive failure rate diagnostics](app-insights-proactive-failure-diagnostics.md) automatically monitor hello rate at which your app responds toorequests with failure codes.</span></span> 

## <a name="automation"></a><span data-ttu-id="bda50-176">自動化</span><span class="sxs-lookup"><span data-stu-id="bda50-176">Automation</span></span>
* [<span data-ttu-id="bda50-177">使用 PowerShell tooautomate 設定警告</span><span class="sxs-lookup"><span data-stu-id="bda50-177">Use PowerShell tooautomate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="bda50-178">使用 webhook tooautomate 回應 tooalerts</span><span class="sxs-lookup"><span data-stu-id="bda50-178">Use webhooks tooautomate responding tooalerts</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a><span data-ttu-id="bda50-179">影片</span><span class="sxs-lookup"><span data-stu-id="bda50-179">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a><span data-ttu-id="bda50-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bda50-180">See also</span></span>
* [<span data-ttu-id="bda50-181">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="bda50-181">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="bda50-182">自動化設定警示</span><span class="sxs-lookup"><span data-stu-id="bda50-182">Automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="bda50-183">主動診斷</span><span class="sxs-lookup"><span data-stu-id="bda50-183">Proactive diagnostics</span></span>](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

