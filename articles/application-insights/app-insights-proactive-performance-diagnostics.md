---
title: "智慧型偵測 - 效能異常 | Microsoft Docs"
description: "Application Insights 會執行您應用程式遙測的智慧型分析，並且警告您有潛在的問題。 這項功能不需要進行任何設定。"
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: fbcd0c4bf0bf959f8a447d922e1e411b8a2af95f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection---performance-anomalies"></a><span data-ttu-id="c379a-104">智慧型偵測 - 效能異常</span><span class="sxs-lookup"><span data-stu-id="c379a-104">Smart Detection - Performance Anomalies</span></span>

<span data-ttu-id="c379a-105">[Application Insights](app-insights-overview.md) 會自動分析 Web 應用程式的效能，並且可以警告您有關潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-105">[Application Insights](app-insights-overview.md) automatically analyzes the performance of your web application, and can warn you about potential problems.</span></span> <span data-ttu-id="c379a-106">您會讀取到此訊息，可能是因為您收到一個我們的智慧型偵測通知。</span><span class="sxs-lookup"><span data-stu-id="c379a-106">You might be reading this because you received one of our smart detection notifications.</span></span>

<span data-ttu-id="c379a-107">除了設定您 Application Insights 的應用程式 (在 [ASP.NET](app-insights-asp-net.md) 上、[Java](app-insights-java-get-started.md) 或 [Node.js](app-insights-nodejs.md)，以及在[網頁程式碼](app-insights-javascript.md)中) 以外，這項功能不需要特殊設定。</span><span class="sxs-lookup"><span data-stu-id="c379a-107">This feature requires no special setup, other than configuring your app for Application Insights (on [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), or [Node.js](app-insights-nodejs.md), and in [web page code](app-insights-javascript.md)).</span></span> <span data-ttu-id="c379a-108">當您的應用程式產生足夠的遙測時，就會是在作用中。</span><span class="sxs-lookup"><span data-stu-id="c379a-108">It is active when your app generates enough telemetry.</span></span>

## <a name="when-would-i-get-a-smart-detection-notification"></a><span data-ttu-id="c379a-109">何時會取得智慧型偵測通知？</span><span class="sxs-lookup"><span data-stu-id="c379a-109">When would I get a smart detection notification?</span></span>

<span data-ttu-id="c379a-110">Application Insights 偵測到您的應用程式以下列其中一種方式降低效能︰</span><span class="sxs-lookup"><span data-stu-id="c379a-110">Application Insights has detected that the performance of your application has degraded in one of these ways:</span></span>

* <span data-ttu-id="c379a-111">**回應時間降低** - 您的應用程式回應要求速度已開始較以往更慢。</span><span class="sxs-lookup"><span data-stu-id="c379a-111">**Response time degradation** - Your app has started responding to requests more slowly than it used to.</span></span> <span data-ttu-id="c379a-112">變更可能很快速，例如因為您的最新部署中有一個迴歸。</span><span class="sxs-lookup"><span data-stu-id="c379a-112">The change might have been rapid, for example because there was a regression in your latest deployment.</span></span> <span data-ttu-id="c379a-113">或者它可能是逐漸進行的，可能是由於記憶體流失所造成。</span><span class="sxs-lookup"><span data-stu-id="c379a-113">Or it might have been gradual, maybe caused by a memory leak.</span></span> 
* <span data-ttu-id="c379a-114">**相依性持續時間降低** - 您的應用程式會呼叫 REST API、資料庫或其他相依性。</span><span class="sxs-lookup"><span data-stu-id="c379a-114">**Dependency duration degradation** - Your app makes calls to a REST API, database, or other dependency.</span></span> <span data-ttu-id="c379a-115">相依性回應較以往更慢。</span><span class="sxs-lookup"><span data-stu-id="c379a-115">The dependency is responding more slowly than it used to.</span></span>
* <span data-ttu-id="c379a-116">**效能變慢模式** - 您應用程式出現的效能問題只會影響部分要求。</span><span class="sxs-lookup"><span data-stu-id="c379a-116">**Slow performance pattern** - Your app appears to have a performance issue that is affecting only some requests.</span></span> <span data-ttu-id="c379a-117">例如，頁面在某一類型瀏覽器上的載入速度低於其他類型瀏覽器；或是某一部特定伺服器服務要求的速度較慢。</span><span class="sxs-lookup"><span data-stu-id="c379a-117">For example, pages are loading more slowly on one type of browser than others; or requests are being served more slowly from one particular server.</span></span> <span data-ttu-id="c379a-118">目前，我們的演算法會查看頁面載入時間、要求回應時間，和相依性回應時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-118">Currently, our algorithms look at page load times, request response times, and dependency response times.</span></span>  

<span data-ttu-id="c379a-119">智慧型偵測需要可用磁碟區中至少 8 天的遙測，才能建立一般效能的基準。</span><span class="sxs-lookup"><span data-stu-id="c379a-119">Smart Detection requires at least 8 days of telemetry at a workable volume in order to establish a baseline of normal performance.</span></span> <span data-ttu-id="c379a-120">因此，您的應用程式在這段時間內執行之後，任何嚴重的問題都會發出通知。</span><span class="sxs-lookup"><span data-stu-id="c379a-120">So, after your application has been running for that period, any significant issue will result in a notification.</span></span>


## <a name="does-my-app-definitely-have-a-problem"></a><span data-ttu-id="c379a-121">我的應用程式絕對有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="c379a-121">Does my app definitely have a problem?</span></span>

<span data-ttu-id="c379a-122">否，通知並不表示您的應用程式一定有問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-122">No, a notification doesn't mean that your app definitely has a problem.</span></span> <span data-ttu-id="c379a-123">這只是一個建議，您可以仔細探究其中的問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-123">It's simply a suggestion about something you might want to look at more closely.</span></span>

## <a name="how-do-i-fix-it"></a><span data-ttu-id="c379a-124">如何修正問題？</span><span class="sxs-lookup"><span data-stu-id="c379a-124">How do I fix it?</span></span>

<span data-ttu-id="c379a-125">通知會包含診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="c379a-125">The notifications include diagnostic information.</span></span> <span data-ttu-id="c379a-126">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="c379a-126">Here's an example:</span></span>


![以下是伺服器回應時間降低偵測的範例](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. <span data-ttu-id="c379a-128">**分級**。</span><span class="sxs-lookup"><span data-stu-id="c379a-128">**Triage**.</span></span> <span data-ttu-id="c379a-129">通知會顯示受影響的使用者人數或作業數。</span><span class="sxs-lookup"><span data-stu-id="c379a-129">The notification shows you how many users or how many operations are affected.</span></span> <span data-ttu-id="c379a-130">這可協助您將優先順序指派給此問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-130">This can help you assign a priority to the problem.</span></span>
2. <span data-ttu-id="c379a-131">**範圍**。</span><span class="sxs-lookup"><span data-stu-id="c379a-131">**Scope**.</span></span> <span data-ttu-id="c379a-132">此問題是否會影響所有流量，還是只會影響某些頁面？</span><span class="sxs-lookup"><span data-stu-id="c379a-132">Is the problem affecting all traffic, or just some pages?</span></span> <span data-ttu-id="c379a-133">它是否限制為特定的瀏覽器或位置？</span><span class="sxs-lookup"><span data-stu-id="c379a-133">Is it restricted to particular browsers or locations?</span></span> <span data-ttu-id="c379a-134">可以從通知取得這項資訊。</span><span class="sxs-lookup"><span data-stu-id="c379a-134">This information can be obtained from the notification.</span></span>
3. <span data-ttu-id="c379a-135">**診斷**。</span><span class="sxs-lookup"><span data-stu-id="c379a-135">**Diagnose**.</span></span> <span data-ttu-id="c379a-136">通常，通知中的診斷資訊會建議問題的本質。</span><span class="sxs-lookup"><span data-stu-id="c379a-136">Often, the diagnostic information in the notification will suggest the nature of the problem.</span></span> <span data-ttu-id="c379a-137">例如，如果要求率很高時回應時間變慢，表示您的伺服器或相依性已超載。</span><span class="sxs-lookup"><span data-stu-id="c379a-137">For example, if response time slows down when request rate is high, that suggests your server or dependencies are overloaded.</span></span> 

    <span data-ttu-id="c379a-138">否則，在 Application Insights 中開啟 [效能] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c379a-138">Otherwise, open the Performance blade in Application Insights.</span></span> <span data-ttu-id="c379a-139">您可以在此處找到[分析工具](app-insights-profiler.md)資料。</span><span class="sxs-lookup"><span data-stu-id="c379a-139">There, you will find [Profiler](app-insights-profiler.md) data.</span></span> <span data-ttu-id="c379a-140">如果擲回例外狀況，則您也可以嘗試[快照集偵錯工具](app-insights-snapshot-debugger.md)。</span><span class="sxs-lookup"><span data-stu-id="c379a-140">If exceptions are thrown, you can also try the [snapshot debugger](app-insights-snapshot-debugger.md).</span></span>



## <a name="configure-email-notifications"></a><span data-ttu-id="c379a-141">設定電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="c379a-141">Configure Email Notifications</span></span>

<span data-ttu-id="c379a-142">依預設會啟用智慧型偵測通知，並將這些通知傳送給具有 [Application Insights 資源的擁有者、參與者和讀取者存取權](app-insights-resources-roles-access-control.md)的人員。</span><span class="sxs-lookup"><span data-stu-id="c379a-142">Smart Detection notifications are enabled by default and sent to those who have [owners, contributors and readers access to the Application Insights resource](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="c379a-143">若要變更這種情況，請按一下電子郵件通知中的 [設定]，或開啟 Application Insights 中的 [智慧型偵測] 設定。</span><span class="sxs-lookup"><span data-stu-id="c379a-143">To change this, either click **Configure** in the email notification, or open Smart Detection settings in Application Insights.</span></span> 
  
  ![智慧型偵測設定](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * <span data-ttu-id="c379a-145">您可以使用智慧型偵測電子郵件中的 [取消訂閱] 連結，停止接收電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="c379a-145">You can use the **unsubscribe** link in the Smart Detection email to stop receiving the email notifications.</span></span>

<span data-ttu-id="c379a-146">每個 Application Insights 資源每天僅限一個關於智慧型偵測效能異常的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="c379a-146">Emails about Smart Detections performance anomalies are limited to one email per day per Application Insights resource.</span></span> <span data-ttu-id="c379a-147">只有在當天偵測到至少一個新的問題時，才會傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="c379a-147">The email will be sent only if there is at least one new issue that was detected on that day.</span></span> <span data-ttu-id="c379a-148">您不會重複收到任何訊息。</span><span class="sxs-lookup"><span data-stu-id="c379a-148">You won't get repeats of any message.</span></span> 

## <a name="faq"></a><span data-ttu-id="c379a-149">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c379a-149">FAQ</span></span>

* <span data-ttu-id="c379a-150">*所以你們會看到我的資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="c379a-150">*So, you guys look at my data?*</span></span>
  * <span data-ttu-id="c379a-151">不會。</span><span class="sxs-lookup"><span data-stu-id="c379a-151">No.</span></span> <span data-ttu-id="c379a-152">服務完全是自動的。</span><span class="sxs-lookup"><span data-stu-id="c379a-152">The service is entirely automatic.</span></span> <span data-ttu-id="c379a-153">只有您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="c379a-153">Only you get the notifications.</span></span> <span data-ttu-id="c379a-154">您的資料是 [不公開的](app-insights-data-retention-privacy.md)。</span><span class="sxs-lookup"><span data-stu-id="c379a-154">Your data is [private](app-insights-data-retention-privacy.md).</span></span>
* <span data-ttu-id="c379a-155">*你們會分析 Application Insights 收集的所有資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="c379a-155">*Do you analyze all the data collected by Application Insights?*</span></span>
  * <span data-ttu-id="c379a-156">目前尚未。</span><span class="sxs-lookup"><span data-stu-id="c379a-156">Not at present.</span></span> <span data-ttu-id="c379a-157">我們目前會分析要求回應時間、相依性回應時間和頁面載入時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-157">Currently, we analyze request response time, dependency response time and page load time.</span></span> <span data-ttu-id="c379a-158">我們後續的未來展望中將有其他計量的分析。</span><span class="sxs-lookup"><span data-stu-id="c379a-158">Analysis of additional metrics is on our backlog looking forward.</span></span>

* <span data-ttu-id="c379a-159">這適用於哪些類型的應用程式？</span><span class="sxs-lookup"><span data-stu-id="c379a-159">What types of application does this work for?</span></span>
  * <span data-ttu-id="c379a-160">會在產生適當遙測的任何應用程式中偵測到這些降低。</span><span class="sxs-lookup"><span data-stu-id="c379a-160">These degradations are detected in any application that generates the appropriate telemetry.</span></span> <span data-ttu-id="c379a-161">如果您在 Web 應用程式中安裝了 Application Insights，就會自動追蹤要求及相依性。</span><span class="sxs-lookup"><span data-stu-id="c379a-161">If you installed Application Insights in your web app, then requests and dependencies are automatically tracked.</span></span> <span data-ttu-id="c379a-162">但在後端服務或其他應用程式中，如果您將呼叫插入 [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) 或 [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency)，則智慧型偵測會以相同的方式運作。</span><span class="sxs-lookup"><span data-stu-id="c379a-162">But in backend services or other apps, if you inserted calls to [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) or [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), then Smart Detection will work in the same way.</span></span>

* <span data-ttu-id="c379a-163">我可以建立自己的異常偵測規則或自訂現有的規則嗎？</span><span class="sxs-lookup"><span data-stu-id="c379a-163">*Can I create my own anomaly detection rules or customize existing rules?*</span></span>

  * <span data-ttu-id="c379a-164">還不行，但是您可以︰</span><span class="sxs-lookup"><span data-stu-id="c379a-164">Not yet, but you can:</span></span>
    * <span data-ttu-id="c379a-165">[設定警示](app-insights-alerts.md)，使其在計量超出臨界值時通知您。</span><span class="sxs-lookup"><span data-stu-id="c379a-165">[Set up alerts](app-insights-alerts.md) that tell you when a metric crosses a threshold.</span></span>
    * <span data-ttu-id="c379a-166">[將遙測匯出](app-insights-export-telemetry.md)至[資料庫](app-insights-code-sample-export-sql-stream-analytics.md)或[至 PowerBI](app-insights-export-power-bi.md)，以自行分析它。</span><span class="sxs-lookup"><span data-stu-id="c379a-166">[Export telemetry](app-insights-export-telemetry.md) to a [database](app-insights-code-sample-export-sql-stream-analytics.md) or [to PowerBI](app-insights-export-power-bi.md), where you can analyze it yourself.</span></span>
* <span data-ttu-id="c379a-167">*執行分析的頻率為何？*</span><span class="sxs-lookup"><span data-stu-id="c379a-167">*How often is the analysis performed?*</span></span>

  * <span data-ttu-id="c379a-168">我們每天都會根據前一天的遙測執行分析 (UTC 時區中全天)。</span><span class="sxs-lookup"><span data-stu-id="c379a-168">We run the analysis daily on the telemetry from the previous day (full day in UTC timezone).</span></span>
* <span data-ttu-id="c379a-169">*那麼，這可以取代[計量警示](app-insights-alerts.md)嗎？*</span><span class="sxs-lookup"><span data-stu-id="c379a-169">*So does this replace [metric alerts](app-insights-alerts.md)?*</span></span>
  * <span data-ttu-id="c379a-170">否。</span><span class="sxs-lookup"><span data-stu-id="c379a-170">No.</span></span>  <span data-ttu-id="c379a-171">我們不保證能偵測到您可能認為異常的每項行為。</span><span class="sxs-lookup"><span data-stu-id="c379a-171">We don't commit to detecting every behavior that you might consider abnormal.</span></span>


* <span data-ttu-id="c379a-172">如果我完全不回應通知，是否會收到提醒？</span><span class="sxs-lookup"><span data-stu-id="c379a-172">*If I don't do anything in reponse to a notification, will I get a reminder?*</span></span>
  * <span data-ttu-id="c379a-173">不會，每個問題您只會收到一次訊息。</span><span class="sxs-lookup"><span data-stu-id="c379a-173">No, you get a message about each issue only once.</span></span> <span data-ttu-id="c379a-174">如果問題仍然存在，就會在 [智慧型偵測摘要] 刀鋒視窗中進行更新。</span><span class="sxs-lookup"><span data-stu-id="c379a-174">If the issue persist it will be updated in the Smart Detection feed blade.</span></span>
* <span data-ttu-id="c379a-175">*我遺失了電子郵件。在入口網站中哪裡可以找到通知？*</span><span class="sxs-lookup"><span data-stu-id="c379a-175">*I lost the email. Where can I find the notifications in the portal?*</span></span>
  * <span data-ttu-id="c379a-176">在應用程式的 Application Insights 概觀中，按一下 [智慧型偵測] 磚。</span><span class="sxs-lookup"><span data-stu-id="c379a-176">In the Application Insights overview of your app, click the **Smart Detection** tile.</span></span> <span data-ttu-id="c379a-177">您可以在這裡找到最多 90 天前的所有通知。</span><span class="sxs-lookup"><span data-stu-id="c379a-177">There you'll be able to find all notifications up to 90 days back.</span></span>

## <a name="how-can-i-improve-performance"></a><span data-ttu-id="c379a-178">如何改善效能？</span><span class="sxs-lookup"><span data-stu-id="c379a-178">How can I improve performance?</span></span>
<span data-ttu-id="c379a-179">您可從自己的經驗得知，對網站使用者而言，回應緩慢和失敗是最大挫折之一。</span><span class="sxs-lookup"><span data-stu-id="c379a-179">Slow and failed responses are one of the biggest frustrations for web site users, as you know from your own experience.</span></span> <span data-ttu-id="c379a-180">因此，請務必解決問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-180">So, it's important to address the issues.</span></span>

### <a name="triage"></a><span data-ttu-id="c379a-181">分級</span><span class="sxs-lookup"><span data-stu-id="c379a-181">Triage</span></span>
<span data-ttu-id="c379a-182">首先，這很重要嗎？</span><span class="sxs-lookup"><span data-stu-id="c379a-182">First, does it matter?</span></span> <span data-ttu-id="c379a-183">如果頁面的載入速度一直很慢，但是只有 1% 的網站台使用者必須查看該網頁，您或許有更重要的事項需要考慮。</span><span class="sxs-lookup"><span data-stu-id="c379a-183">If a page is always slow to load, but only 1% of your site's users ever have to look at it, maybe you have more important things to think about.</span></span> <span data-ttu-id="c379a-184">另一方面，如果只有 1% 的使用者開啟該網頁，但它每次都擲回例外狀況，這可能就是值得調查的問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-184">On the other hand, if only 1% of users open it, but it throws exceptions every time, that might be worth investigating.</span></span>

<span data-ttu-id="c379a-185">使用影響敘述 (受影響的使用者或流量的 %) 作為一般指南，但請留意該敘述並不是全部的詳情。</span><span class="sxs-lookup"><span data-stu-id="c379a-185">Use the impact statement (affected users or % of traffic) as a general guide, but be aware that it isn't the whole story.</span></span> <span data-ttu-id="c379a-186">蒐集其他證據進行確認。</span><span class="sxs-lookup"><span data-stu-id="c379a-186">Gather other evidence to confirm.</span></span>

<span data-ttu-id="c379a-187">請考慮這個問題的參數。</span><span class="sxs-lookup"><span data-stu-id="c379a-187">Consider the parameters of the issue.</span></span> <span data-ttu-id="c379a-188">如果與地理位置有關，請設定包括該地區的 [可用性測試](app-insights-monitor-web-app-availability.md) ：該地區可能只有網路問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-188">If it's geography-dependent, set up [availability tests](app-insights-monitor-web-app-availability.md) including that region: there might simply be network issues in that area.</span></span>

### <a name="diagnose-slow-page-loads"></a><span data-ttu-id="c379a-189">診斷頁面載入緩慢</span><span class="sxs-lookup"><span data-stu-id="c379a-189">Diagnose slow page loads</span></span>
<span data-ttu-id="c379a-190">問題出在哪裡？</span><span class="sxs-lookup"><span data-stu-id="c379a-190">Where is the problem?</span></span> <span data-ttu-id="c379a-191">伺服器是否回應太慢、頁面是否很長，或瀏覽器必須執行很多工作才能顯示頁面？</span><span class="sxs-lookup"><span data-stu-id="c379a-191">Is the server slow to respond, is the page very long, or does the browser have to do a lot of work to display it?</span></span>

<span data-ttu-id="c379a-192">開啟 [瀏覽器] 計量刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c379a-192">Open the Browsers metric blade.</span></span> <span data-ttu-id="c379a-193">分段顯示的瀏覽器頁面載入時間可顯示時間的進度。</span><span class="sxs-lookup"><span data-stu-id="c379a-193">The segmented display of browser page load time shows where the time is going.</span></span> 

* <span data-ttu-id="c379a-194">如果 [傳送要求時間]  太久，不是伺服器回應速度緩慢，就是要求是含有大量資料的文章。</span><span class="sxs-lookup"><span data-stu-id="c379a-194">If **Send Request Time** is high, either the server is responding slowly, or the request is a post with a lot of data.</span></span> <span data-ttu-id="c379a-195">查看 [效能計量](app-insights-web-monitor-performance.md#metrics) 以調查回應時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-195">Look at the [performance metrics](app-insights-web-monitor-performance.md#metrics) to investigate response times.</span></span>
* <span data-ttu-id="c379a-196">設定 [相依性追蹤](app-insights-asp-net-dependencies.md) 以查看速度慢是否是外部服務或您的資料庫所造成。</span><span class="sxs-lookup"><span data-stu-id="c379a-196">Set up [dependency tracking](app-insights-asp-net-dependencies.md) to see whether the slowness is due to external services or your database.</span></span>
* <span data-ttu-id="c379a-197">如果 [接收回應]  是主導因素，您的頁面和其相依組件 (JavaScript、CSS 及影像等，而非以非同步方式載入的資料) 會很長。</span><span class="sxs-lookup"><span data-stu-id="c379a-197">If **Receiving Response** is predominant, your page and its dependent parts - JavaScript, CSS, images and so on (but not asynchronously loaded data) are long.</span></span> <span data-ttu-id="c379a-198">設定 [可用性測試](app-insights-monitor-web-app-availability.md)，而且務必設定載入相依組件的選項。</span><span class="sxs-lookup"><span data-stu-id="c379a-198">Set up an [availability test](app-insights-monitor-web-app-availability.md), and be sure to set the option to load dependent parts.</span></span> <span data-ttu-id="c379a-199">當您取得一些結果時，請開啟結果的詳細資料並將它展開，以查看不同檔案的載入時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-199">When you get some results, open the detail of a result and expand it to see the load times of different files.</span></span>
* <span data-ttu-id="c379a-200">[用戶端處理時間]  過長表示指令碼執行速度很慢。</span><span class="sxs-lookup"><span data-stu-id="c379a-200">High **Client Processing time** suggests scripts are running slowly.</span></span> <span data-ttu-id="c379a-201">如果原因不明顯，請考慮加入一些時間計時程式碼並在 trackMetric 呼叫中傳送時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-201">If the reason isn't obvious, consider adding some timing code and send the times in trackMetric calls.</span></span>

### <a name="improve-slow-pages"></a><span data-ttu-id="c379a-202">改善慢速網頁</span><span class="sxs-lookup"><span data-stu-id="c379a-202">Improve slow pages</span></span>
<span data-ttu-id="c379a-203">Web 上有改善您的伺服器回應和頁面載入時間的完整建議，因此我們不會嘗試這次重複說明。</span><span class="sxs-lookup"><span data-stu-id="c379a-203">There's a web full of advice on improving your server responses and page load times, so we won't try to repeat it all here.</span></span> <span data-ttu-id="c379a-204">以下是您可能已知道的一些祕訣，這只是為提醒您：</span><span class="sxs-lookup"><span data-stu-id="c379a-204">Here are a few tips that you probably already know about, just to get you thinking:</span></span>

* <span data-ttu-id="c379a-205">由大型檔案造成的緩慢載入：以非同步方式載入指令碼和其他組件。</span><span class="sxs-lookup"><span data-stu-id="c379a-205">Slow loading because of big files: Load the scripts and other parts asynchronously.</span></span> <span data-ttu-id="c379a-206">使用指令碼統合。</span><span class="sxs-lookup"><span data-stu-id="c379a-206">Use script bundling.</span></span> <span data-ttu-id="c379a-207">將主頁面分成可個別載入其資料的 Widget。</span><span class="sxs-lookup"><span data-stu-id="c379a-207">Break the main page into widgets that load their data separately.</span></span> <span data-ttu-id="c379a-208">不要對長資料表傳送純舊式 HTML：使用指令碼要求 JSON 或其他壓縮格式的資料，然後就地填滿資料表。</span><span class="sxs-lookup"><span data-stu-id="c379a-208">Don't send plain old HTML for long tables: use a script to request the data as JSON or other compact format, then fill the table in place.</span></span> <span data-ttu-id="c379a-209">有一些絕佳的架構可協助進行這一切。</span><span class="sxs-lookup"><span data-stu-id="c379a-209">There are great frameworks to help with all this.</span></span> <span data-ttu-id="c379a-210">(當然，也必須承擔大型指令碼)。</span><span class="sxs-lookup"><span data-stu-id="c379a-210">(They also entail big scripts, of course.)</span></span>
* <span data-ttu-id="c379a-211">降低伺服器相依性：考慮您的元件的地理位置。</span><span class="sxs-lookup"><span data-stu-id="c379a-211">Slow server dependencies: Consider the geographical locations of your components.</span></span> <span data-ttu-id="c379a-212">比方說，如果您使用 Azure，請確定 Web 伺服器和資料庫位於相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="c379a-212">For example, if you're using Azure, make sure the web server and the database are in the same region.</span></span> <span data-ttu-id="c379a-213">查詢是否會擷取超過所需的資訊？</span><span class="sxs-lookup"><span data-stu-id="c379a-213">Do queries retrieve more information than they need?</span></span> <span data-ttu-id="c379a-214">快取或批次處理是否有所幫助？</span><span class="sxs-lookup"><span data-stu-id="c379a-214">Would caching or batching help?</span></span>
* <span data-ttu-id="c379a-215">容量問題：查看回應時間和要求計數的伺服器計量。</span><span class="sxs-lookup"><span data-stu-id="c379a-215">Capacity issues: Look at the server metrics of response times and request counts.</span></span> <span data-ttu-id="c379a-216">如果回應時間尖峰與要求計數尖峰不成比例，有可能是您的伺服器已被過度使用。</span><span class="sxs-lookup"><span data-stu-id="c379a-216">If response times peak disproportionately with peaks in request counts, it's likely that your servers are stretched.</span></span>


## <a name="server-response-time-degradation"></a><span data-ttu-id="c379a-217">伺服器回應時間降低</span><span class="sxs-lookup"><span data-stu-id="c379a-217">Server Response Time Degradation</span></span>

<span data-ttu-id="c379a-218">回應時間降低通知會告訴您︰</span><span class="sxs-lookup"><span data-stu-id="c379a-218">The response time degradation notification tells you:</span></span>

* <span data-ttu-id="c379a-219">相較於這項作業一般回應時間的回應時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-219">The response time compared to normal response time for this operation.</span></span>
* <span data-ttu-id="c379a-220">受影響的使用者人數。</span><span class="sxs-lookup"><span data-stu-id="c379a-220">How many users are affected.</span></span>
* <span data-ttu-id="c379a-221">偵測到當天和 7 天前這項作業的平均回應時間和第 90 百分位回應時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-221">Average response time and 90th percentile response time for this operation on the day of the detection and 7 days before.</span></span> 
* <span data-ttu-id="c379a-222">偵測到當天和 7 天前這項作業的要求計數。</span><span class="sxs-lookup"><span data-stu-id="c379a-222">Count of this operation requests on the day of the detection and 7 days before.</span></span>
* <span data-ttu-id="c379a-223">這項作業之降低與相關相依性之降低間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="c379a-223">Correlation between degradation in this operation and degradations in related dependencies.</span></span> 
* <span data-ttu-id="c379a-224">連結可幫助您診斷問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-224">Links to help you diagnose the problem.</span></span>
  * <span data-ttu-id="c379a-225">分析工具追蹤可協助您檢視作業花費時間之處 (如果在偵測期間收集到這項作業的分析工具追蹤範例，則可使用連結)。</span><span class="sxs-lookup"><span data-stu-id="c379a-225">Profiler traces to help you view where operation time is spent (the link is available if Profiler trace examples were collected for this operation during the detection period).</span></span> 
  * <span data-ttu-id="c379a-226">您可以在計量瀏覽器中的效能報告將這項作業的時間範圍/篩選條件進行交叉分析。</span><span class="sxs-lookup"><span data-stu-id="c379a-226">Performance reports in Metric Explorer, where you can slice and dice time range/filters for this operation.</span></span>
  * <span data-ttu-id="c379a-227">搜尋此呼叫可檢視特定的呼叫屬性。</span><span class="sxs-lookup"><span data-stu-id="c379a-227">Search for this calls to view specific calls properties.</span></span>
  * <span data-ttu-id="c379a-228">報告失敗 - 如果計數 > 1，表示這項作業中的失敗可能造成效能降低。</span><span class="sxs-lookup"><span data-stu-id="c379a-228">Failure reports - If count > 1 this mean that there were failures in this operation that might have contributed to performance degradation.</span></span>

## <a name="dependency-duration-degradation"></a><span data-ttu-id="c379a-229">相依性持續時間降低</span><span class="sxs-lookup"><span data-stu-id="c379a-229">Dependency Duration Degradation</span></span>

<span data-ttu-id="c379a-230">現代化應用程式採用越來越多微服務設計的方法，在許多情況下，會造成外部服務的重度可靠性。</span><span class="sxs-lookup"><span data-stu-id="c379a-230">Modern application more and more adopt micro services design approach, which in many cases leads to heavy reliability on external services.</span></span> <span data-ttu-id="c379a-231">例如，如果您的應用程式需仰賴某些資料平台，或即使您建立自己的 Bot 服務，可能還是需要一些辨識服務提供者，才能讓您的 Bot 以更人性化的方式進行互動，且 Bot 也需要一些可提取回答的資料存放服務。</span><span class="sxs-lookup"><span data-stu-id="c379a-231">For example, if your application relies on some data platform or even if you build your own bot service you will probably relay on some cognitive services provider to enable your bots to interact in more human ways and some data store service for bot to pull the answers from.</span></span>  

<span data-ttu-id="c379a-232">範例相依性降低通知︰</span><span class="sxs-lookup"><span data-stu-id="c379a-232">Example dependency degradation notification:</span></span>

![以下是相依性持續時間降低偵測的範例](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

<span data-ttu-id="c379a-234">請注意，它會告訴您︰</span><span class="sxs-lookup"><span data-stu-id="c379a-234">Notice that it tells you:</span></span>

* <span data-ttu-id="c379a-235">相較於這項作業一般回應時間的持續時間</span><span class="sxs-lookup"><span data-stu-id="c379a-235">The duration compared to normal response time for this operation</span></span>
* <span data-ttu-id="c379a-236">受影響的使用者人數</span><span class="sxs-lookup"><span data-stu-id="c379a-236">How many users are affected</span></span>
* <span data-ttu-id="c379a-237">偵測到當天和 7 天前此相依性的平均持續時間和第 90 百分位持續時間</span><span class="sxs-lookup"><span data-stu-id="c379a-237">Average duration and 90th percentile duration for this dependency on the day of the detection and 7 days before</span></span>
* <span data-ttu-id="c379a-238">偵測到當天和 7 天前的相依性呼叫數目</span><span class="sxs-lookup"><span data-stu-id="c379a-238">Number of dependency calls on the day of the detection and 7 days before</span></span>
* <span data-ttu-id="c379a-239">連結可幫助您診斷問題</span><span class="sxs-lookup"><span data-stu-id="c379a-239">Links to help you diagnose the problem</span></span>
  * <span data-ttu-id="c379a-240">計量瀏覽器中此相依性的效能報告</span><span class="sxs-lookup"><span data-stu-id="c379a-240">Performance reports in Metric Explorer for this dependency</span></span>
  * <span data-ttu-id="c379a-241">搜尋此相依性呼叫可檢視呼叫屬性</span><span class="sxs-lookup"><span data-stu-id="c379a-241">Search for this dependency calls to view calls properties</span></span>
  * <span data-ttu-id="c379a-242">報告失敗 - 如果計數 > 1，表示偵測期間失敗的相依性呼叫可能造成持續時間降低。</span><span class="sxs-lookup"><span data-stu-id="c379a-242">Failure reports - If count > 1 this mean that there were failed dependency calls during the detection period that might have contributed to duration degradation.</span></span> 
  * <span data-ttu-id="c379a-243">使用計算此相依性持續時間和計數的查詢來開啟分析</span><span class="sxs-lookup"><span data-stu-id="c379a-243">Open Analytics with queries that calculate this dependency duration and count</span></span>  

## <a name="smart-detection-of-slow-performing-patterns"></a><span data-ttu-id="c379a-244">效能變慢模式的智慧型偵測</span><span class="sxs-lookup"><span data-stu-id="c379a-244">Smart Detection of slow performing patterns</span></span> 

<span data-ttu-id="c379a-245">Application Insights 會尋找可能只會影響某部分使用者，或只在某些情況下影響使用者的效能問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-245">Application Insights finds performance issues that might only affect some portion of your users, or only affect users in some cases.</span></span> <span data-ttu-id="c379a-246">例如，通知關於頁面在某一類型瀏覽器上的載入速度低於其他類型瀏覽器，或特定伺服器服務要求的速度較慢。</span><span class="sxs-lookup"><span data-stu-id="c379a-246">For example, notification about pages load is slowler on one type of browser than on other types of browsers, or if requests are served more slowly from a particular server.</span></span> <span data-ttu-id="c379a-247">它同時可以探索與屬性組合相關的問題，例如在某地區中使用特定作業系統的用戶端，頁面載入速度緩慢的問題。</span><span class="sxs-lookup"><span data-stu-id="c379a-247">It can also discover problems associated with combinations of properties, such as slow page loads in one geographical area for clients using particular operating system.</span></span>  

<span data-ttu-id="c379a-248">這類異常狀況很難只藉由調查資料來偵測，但比您想像的更為常見。</span><span class="sxs-lookup"><span data-stu-id="c379a-248">Anomalies like these are very hard to detect just by inspecting the data, but are more common than you might think.</span></span> <span data-ttu-id="c379a-249">通常只在您的客戶抱怨時才會浮出檯面。</span><span class="sxs-lookup"><span data-stu-id="c379a-249">Often they only surface when your customers complain.</span></span> <span data-ttu-id="c379a-250">但那時就太晚了：受影響的使用者已經轉而選擇您的對手！</span><span class="sxs-lookup"><span data-stu-id="c379a-250">By that time, it’s too late: the affected users are already switching to your competitors!</span></span>

<span data-ttu-id="c379a-251">目前，我們的演算法會查看頁面載入時間、伺服器上的要求回應時間，和相依性回應時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-251">Currently, our algorithms look at page load times, request response times at the server, and dependency response times.</span></span>  

<span data-ttu-id="c379a-252">您不需設定任何臨界值或設定規則。</span><span class="sxs-lookup"><span data-stu-id="c379a-252">You don't have to set any thresholds or configure rules.</span></span> <span data-ttu-id="c379a-253">機器學習服務和資料採礦演算法會用來偵測異常模式。</span><span class="sxs-lookup"><span data-stu-id="c379a-253">Machine learning and data mining algorithms are used to detect abnormal patterns.</span></span>

![按一下電子郵件警示中的連結，可在 Azure 中開啟診斷報告](./media/app-insights-proactive-performance-diagnostics/03.png)

* <span data-ttu-id="c379a-255">**時間**顯示偵測到問題的時間。</span><span class="sxs-lookup"><span data-stu-id="c379a-255">**When** shows the time the issue was detected.</span></span>
* <span data-ttu-id="c379a-256">[對象] 說明：</span><span class="sxs-lookup"><span data-stu-id="c379a-256">**What** describes:</span></span>

  * <span data-ttu-id="c379a-257">偵測到的問題；</span><span class="sxs-lookup"><span data-stu-id="c379a-257">The problem that was detected;</span></span>
  * <span data-ttu-id="c379a-258">我們發現的事件集的特性顯示了問題行為。</span><span class="sxs-lookup"><span data-stu-id="c379a-258">The characteristics of the set of events that we found displayed the problem behavior.</span></span>
* <span data-ttu-id="c379a-259">表格會比較效能差的事件集和所有其他事件的平均行為。</span><span class="sxs-lookup"><span data-stu-id="c379a-259">The table compares the poorly-performing set with the average behavior of all other events.</span></span>

<span data-ttu-id="c379a-260">按下連結以開啟 [計量瀏覽器]，搜尋相關報告、篩選緩慢執行的事件集的時間和屬性。</span><span class="sxs-lookup"><span data-stu-id="c379a-260">Click the links to open Metric Explorer and Search on relevant reports, filtered on the time and properties of the slow performing set.</span></span>

<span data-ttu-id="c379a-261">修改時間範圍和篩選器可探索遙測。</span><span class="sxs-lookup"><span data-stu-id="c379a-261">Modify the time range and filters to explore the telemetry.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c379a-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c379a-262">Next steps</span></span>
<span data-ttu-id="c379a-263">這些診斷工具可協助您檢查來自您的應用程式的遙測︰</span><span class="sxs-lookup"><span data-stu-id="c379a-263">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="c379a-264">分析工具</span><span class="sxs-lookup"><span data-stu-id="c379a-264">Profiler</span></span>](app-insights-profiler.md) 
* [<span data-ttu-id="c379a-265">快照集偵錯工具</span><span class="sxs-lookup"><span data-stu-id="c379a-265">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
* [<span data-ttu-id="c379a-266">分析</span><span class="sxs-lookup"><span data-stu-id="c379a-266">Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="c379a-267">分析智慧型診斷</span><span class="sxs-lookup"><span data-stu-id="c379a-267">Analytics smart diagnostics</span></span>](app-insights-analytics-diagnostics.md)

<span data-ttu-id="c379a-268">智慧型偵測是完全自動的。</span><span class="sxs-lookup"><span data-stu-id="c379a-268">Smart detections are completely automatic.</span></span> <span data-ttu-id="c379a-269">但是，或許您會想要再設定一些警示？</span><span class="sxs-lookup"><span data-stu-id="c379a-269">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="c379a-270">手動設定的度量警示</span><span class="sxs-lookup"><span data-stu-id="c379a-270">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="c379a-271">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="c379a-271">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
