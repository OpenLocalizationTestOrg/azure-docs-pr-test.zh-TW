---
title: "aaaSmart 偵測-效能異常 |Microsoft 文件"
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
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a><span data-ttu-id="b3777-104">智慧型偵測 - 效能異常</span><span class="sxs-lookup"><span data-stu-id="b3777-104">Smart Detection - Performance Anomalies</span></span>

<span data-ttu-id="b3777-105">[Application Insights](app-insights-overview.md)自動分析 hello web 應用程式的效能，並警告您有關潛在問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-105">[Application Insights](app-insights-overview.md) automatically analyzes hello performance of your web application, and can warn you about potential problems.</span></span> <span data-ttu-id="b3777-106">您會讀取到此訊息，可能是因為您收到一個我們的智慧型偵測通知。</span><span class="sxs-lookup"><span data-stu-id="b3777-106">You might be reading this because you received one of our smart detection notifications.</span></span>

<span data-ttu-id="b3777-107">除了設定您 Application Insights 的應用程式 (在 [ASP.NET](app-insights-asp-net.md) 上、[Java](app-insights-java-get-started.md) 或 [Node.js](app-insights-nodejs.md)，以及在[網頁程式碼](app-insights-javascript.md)中) 以外，這項功能不需要特殊設定。</span><span class="sxs-lookup"><span data-stu-id="b3777-107">This feature requires no special setup, other than configuring your app for Application Insights (on [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), or [Node.js](app-insights-nodejs.md), and in [web page code](app-insights-javascript.md)).</span></span> <span data-ttu-id="b3777-108">當您的應用程式產生足夠的遙測時，就會是在作用中。</span><span class="sxs-lookup"><span data-stu-id="b3777-108">It is active when your app generates enough telemetry.</span></span>

## <a name="when-would-i-get-a-smart-detection-notification"></a><span data-ttu-id="b3777-109">何時會取得智慧型偵測通知？</span><span class="sxs-lookup"><span data-stu-id="b3777-109">When would I get a smart detection notification?</span></span>

<span data-ttu-id="b3777-110">Application Insights 偵測 hello 應用程式的效能降低在下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="b3777-110">Application Insights has detected that hello performance of your application has degraded in one of these ways:</span></span>

* <span data-ttu-id="b3777-111">**回應時間降低**-您的應用程式已開始使用的放慢回應 toorequests。</span><span class="sxs-lookup"><span data-stu-id="b3777-111">**Response time degradation** - Your app has started responding toorequests more slowly than it used to.</span></span> <span data-ttu-id="b3777-112">hello 變更可能已快速，例如因為發生在最新的部署中的迴歸。</span><span class="sxs-lookup"><span data-stu-id="b3777-112">hello change might have been rapid, for example because there was a regression in your latest deployment.</span></span> <span data-ttu-id="b3777-113">或者它可能是逐漸進行的，可能是由於記憶體流失所造成。</span><span class="sxs-lookup"><span data-stu-id="b3777-113">Or it might have been gradual, maybe caused by a memory leak.</span></span> 
* <span data-ttu-id="b3777-114">**相依性持續時間降低**-呼叫 tooa REST API、 資料庫或其他相依性，可讓您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3777-114">**Dependency duration degradation** - Your app makes calls tooa REST API, database, or other dependency.</span></span> <span data-ttu-id="b3777-115">若要使用的放慢回應 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="b3777-115">hello dependency is responding more slowly than it used to.</span></span>
* <span data-ttu-id="b3777-116">**效能變慢模式**-您的應用程式會出現的 toohave 效能問題會影響某些的要求。</span><span class="sxs-lookup"><span data-stu-id="b3777-116">**Slow performance pattern** - Your app appears toohave a performance issue that is affecting only some requests.</span></span> <span data-ttu-id="b3777-117">例如，頁面在某一類型瀏覽器上的載入速度低於其他類型瀏覽器；或是某一部特定伺服器服務要求的速度較慢。</span><span class="sxs-lookup"><span data-stu-id="b3777-117">For example, pages are loading more slowly on one type of browser than others; or requests are being served more slowly from one particular server.</span></span> <span data-ttu-id="b3777-118">目前，我們的演算法會查看頁面載入時間、要求回應時間，和相依性回應時間。</span><span class="sxs-lookup"><span data-stu-id="b3777-118">Currently, our algorithms look at page load times, request response times, and dependency response times.</span></span>  

<span data-ttu-id="b3777-119">智慧偵測需要至少 8 天的順序 tooestablish 的一般效能基準線中的可用磁碟區上的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="b3777-119">Smart Detection requires at least 8 days of telemetry at a workable volume in order tooestablish a baseline of normal performance.</span></span> <span data-ttu-id="b3777-120">因此，您的應用程式在這段時間內執行之後，任何嚴重的問題都會發出通知。</span><span class="sxs-lookup"><span data-stu-id="b3777-120">So, after your application has been running for that period, any significant issue will result in a notification.</span></span>


## <a name="does-my-app-definitely-have-a-problem"></a><span data-ttu-id="b3777-121">我的應用程式絕對有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="b3777-121">Does my app definitely have a problem?</span></span>

<span data-ttu-id="b3777-122">否，通知並不表示您的應用程式一定有問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-122">No, a notification doesn't mean that your app definitely has a problem.</span></span> <span data-ttu-id="b3777-123">它是只需有關可能會想要在 toolook 更緊密的東西的建議。</span><span class="sxs-lookup"><span data-stu-id="b3777-123">It's simply a suggestion about something you might want toolook at more closely.</span></span>

## <a name="how-do-i-fix-it"></a><span data-ttu-id="b3777-124">如何修正問題？</span><span class="sxs-lookup"><span data-stu-id="b3777-124">How do I fix it?</span></span>

<span data-ttu-id="b3777-125">hello 通知包含診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="b3777-125">hello notifications include diagnostic information.</span></span> <span data-ttu-id="b3777-126">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="b3777-126">Here's an example:</span></span>


![以下是伺服器回應時間降低偵測的範例](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. <span data-ttu-id="b3777-128">**分級**。</span><span class="sxs-lookup"><span data-stu-id="b3777-128">**Triage**.</span></span> <span data-ttu-id="b3777-129">hello 通知會顯示您的使用者人數，或多少作業會受到影響。</span><span class="sxs-lookup"><span data-stu-id="b3777-129">hello notification shows you how many users or how many operations are affected.</span></span> <span data-ttu-id="b3777-130">這可協助您指派優先權 toohello 問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-130">This can help you assign a priority toohello problem.</span></span>
2. <span data-ttu-id="b3777-131">**範圍**。</span><span class="sxs-lookup"><span data-stu-id="b3777-131">**Scope**.</span></span> <span data-ttu-id="b3777-132">Hello 問題會影響所有流量或一些頁面嗎？</span><span class="sxs-lookup"><span data-stu-id="b3777-132">Is hello problem affecting all traffic, or just some pages?</span></span> <span data-ttu-id="b3777-133">是受限制的 it tooparticular 瀏覽器或位置？</span><span class="sxs-lookup"><span data-stu-id="b3777-133">Is it restricted tooparticular browsers or locations?</span></span> <span data-ttu-id="b3777-134">這項資訊可以取自 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="b3777-134">This information can be obtained from hello notification.</span></span>
3. <span data-ttu-id="b3777-135">**診斷**。</span><span class="sxs-lookup"><span data-stu-id="b3777-135">**Diagnose**.</span></span> <span data-ttu-id="b3777-136">通常，hello hello 通知中的診斷資訊將會建議 hello hello 問題的性質。</span><span class="sxs-lookup"><span data-stu-id="b3777-136">Often, hello diagnostic information in hello notification will suggest hello nature of hello problem.</span></span> <span data-ttu-id="b3777-137">例如，如果要求率很高時回應時間變慢，表示您的伺服器或相依性已超載。</span><span class="sxs-lookup"><span data-stu-id="b3777-137">For example, if response time slows down when request rate is high, that suggests your server or dependencies are overloaded.</span></span> 

    <span data-ttu-id="b3777-138">否則，請開啟 Application Insights 中的 hello 效能刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b3777-138">Otherwise, open hello Performance blade in Application Insights.</span></span> <span data-ttu-id="b3777-139">您可以在此處找到[分析工具](app-insights-profiler.md)資料。</span><span class="sxs-lookup"><span data-stu-id="b3777-139">There, you will find [Profiler](app-insights-profiler.md) data.</span></span> <span data-ttu-id="b3777-140">擲回例外狀況時，您也可以嘗試 hello[快照偵錯工具](app-insights-snapshot-debugger.md)。</span><span class="sxs-lookup"><span data-stu-id="b3777-140">If exceptions are thrown, you can also try hello [snapshot debugger](app-insights-snapshot-debugger.md).</span></span>



## <a name="configure-email-notifications"></a><span data-ttu-id="b3777-141">設定電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="b3777-141">Configure Email Notifications</span></span>

<span data-ttu-id="b3777-142">智慧偵測通知是預設啟用，並且會傳送具有 toothose[擁有者、 參與者與讀者存取 toohello Application Insights 資源](app-insights-resources-roles-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="b3777-142">Smart Detection notifications are enabled by default and sent toothose who have [owners, contributors and readers access toohello Application Insights resource](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="b3777-143">toochange 這按一下**設定**hello 電子郵件通知，或開啟 Application Insights 中的智慧偵測設定。</span><span class="sxs-lookup"><span data-stu-id="b3777-143">toochange this, either click **Configure** in hello email notification, or open Smart Detection settings in Application Insights.</span></span> 
  
  ![智慧型偵測設定](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * <span data-ttu-id="b3777-145">您可以使用 hello**取消訂閱**hello 智慧偵測電子郵件 toostop 接收 hello 電子郵件通知中的連結。</span><span class="sxs-lookup"><span data-stu-id="b3777-145">You can use hello **unsubscribe** link in hello Smart Detection email toostop receiving hello email notifications.</span></span>

<span data-ttu-id="b3777-146">智慧偵測效能的異常狀況的相關電子郵件是每天每個 Application Insights 資源有限的 tooone 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b3777-146">Emails about Smart Detections performance anomalies are limited tooone email per day per Application Insights resource.</span></span> <span data-ttu-id="b3777-147">只有當至少一個新的問題所偵測到在那一天，將會傳送 hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b3777-147">hello email will be sent only if there is at least one new issue that was detected on that day.</span></span> <span data-ttu-id="b3777-148">您不會重複收到任何訊息。</span><span class="sxs-lookup"><span data-stu-id="b3777-148">You won't get repeats of any message.</span></span> 

## <a name="faq"></a><span data-ttu-id="b3777-149">常見問題集</span><span class="sxs-lookup"><span data-stu-id="b3777-149">FAQ</span></span>

* <span data-ttu-id="b3777-150">*所以你們會看到我的資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="b3777-150">*So, you guys look at my data?*</span></span>
  * <span data-ttu-id="b3777-151">否。</span><span class="sxs-lookup"><span data-stu-id="b3777-151">No.</span></span> <span data-ttu-id="b3777-152">hello 服務是完全自動。</span><span class="sxs-lookup"><span data-stu-id="b3777-152">hello service is entirely automatic.</span></span> <span data-ttu-id="b3777-153">只有您會收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="b3777-153">Only you get hello notifications.</span></span> <span data-ttu-id="b3777-154">您的資料是 [不公開的](app-insights-data-retention-privacy.md)。</span><span class="sxs-lookup"><span data-stu-id="b3777-154">Your data is [private](app-insights-data-retention-privacy.md).</span></span>
* <span data-ttu-id="b3777-155">*在分析 Application Insights 所收集的所有 hello 資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="b3777-155">*Do you analyze all hello data collected by Application Insights?*</span></span>
  * <span data-ttu-id="b3777-156">目前尚未。</span><span class="sxs-lookup"><span data-stu-id="b3777-156">Not at present.</span></span> <span data-ttu-id="b3777-157">我們目前會分析要求回應時間、相依性回應時間和頁面載入時間。</span><span class="sxs-lookup"><span data-stu-id="b3777-157">Currently, we analyze request response time, dependency response time and page load time.</span></span> <span data-ttu-id="b3777-158">我們後續的未來展望中將有其他計量的分析。</span><span class="sxs-lookup"><span data-stu-id="b3777-158">Analysis of additional metrics is on our backlog looking forward.</span></span>

* <span data-ttu-id="b3777-159">這適用於哪些類型的應用程式？</span><span class="sxs-lookup"><span data-stu-id="b3777-159">What types of application does this work for?</span></span>
  * <span data-ttu-id="b3777-160">任何應用程式會產生 hello 適當遙測中偵測到這些衰退。</span><span class="sxs-lookup"><span data-stu-id="b3777-160">These degradations are detected in any application that generates hello appropriate telemetry.</span></span> <span data-ttu-id="b3777-161">如果您在 Web 應用程式中安裝了 Application Insights，就會自動追蹤要求及相依性。</span><span class="sxs-lookup"><span data-stu-id="b3777-161">If you installed Application Insights in your web app, then requests and dependencies are automatically tracked.</span></span> <span data-ttu-id="b3777-162">但在後端服務或其他應用程式，當您插入呼叫太[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest)或[TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency)，則智慧偵測的作用中 hello 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="b3777-162">But in backend services or other apps, if you inserted calls too[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) or [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), then Smart Detection will work in hello same way.</span></span>

* <span data-ttu-id="b3777-163">我可以建立自己的異常偵測規則或自訂現有的規則嗎？</span><span class="sxs-lookup"><span data-stu-id="b3777-163">*Can I create my own anomaly detection rules or customize existing rules?*</span></span>

  * <span data-ttu-id="b3777-164">還不行，但是您可以︰</span><span class="sxs-lookup"><span data-stu-id="b3777-164">Not yet, but you can:</span></span>
    * <span data-ttu-id="b3777-165">[設定警示](app-insights-alerts.md)，使其在計量超出臨界值時通知您。</span><span class="sxs-lookup"><span data-stu-id="b3777-165">[Set up alerts](app-insights-alerts.md) that tell you when a metric crosses a threshold.</span></span>
    * <span data-ttu-id="b3777-166">[匯出遙測](app-insights-export-telemetry.md)tooa[資料庫](app-insights-code-sample-export-sql-stream-analytics.md)或[tooPowerBI](app-insights-export-power-bi.md)，其中您可以分析它自己。</span><span class="sxs-lookup"><span data-stu-id="b3777-166">[Export telemetry](app-insights-export-telemetry.md) tooa [database](app-insights-code-sample-export-sql-stream-analytics.md) or [tooPowerBI](app-insights-export-power-bi.md), where you can analyze it yourself.</span></span>
* <span data-ttu-id="b3777-167">*Hello 分析執行頻率為何？*</span><span class="sxs-lookup"><span data-stu-id="b3777-167">*How often is hello analysis performed?*</span></span>

  * <span data-ttu-id="b3777-168">我們 hello 分析每日 hello 遙測，從執行 hello 前一天 （以 UTC 時區的全天）。</span><span class="sxs-lookup"><span data-stu-id="b3777-168">We run hello analysis daily on hello telemetry from hello previous day (full day in UTC timezone).</span></span>
* <span data-ttu-id="b3777-169">*那麼，這可以取代[計量警示](app-insights-alerts.md)嗎？*</span><span class="sxs-lookup"><span data-stu-id="b3777-169">*So does this replace [metric alerts](app-insights-alerts.md)?*</span></span>
  * <span data-ttu-id="b3777-170">否。</span><span class="sxs-lookup"><span data-stu-id="b3777-170">No.</span></span>  <span data-ttu-id="b3777-171">我們請不要認可 toodetecting 每個您可以考慮異常的行為。</span><span class="sxs-lookup"><span data-stu-id="b3777-171">We don't commit toodetecting every behavior that you might consider abnormal.</span></span>


* <span data-ttu-id="b3777-172">*如果我沒有進行任何回應 tooa 通知中的項目，我會收到提醒？*</span><span class="sxs-lookup"><span data-stu-id="b3777-172">*If I don't do anything in reponse tooa notification, will I get a reminder?*</span></span>
  * <span data-ttu-id="b3777-173">不會，每個問題您只會收到一次訊息。</span><span class="sxs-lookup"><span data-stu-id="b3777-173">No, you get a message about each issue only once.</span></span> <span data-ttu-id="b3777-174">如果 hello 問題仍存在它將會更新的 hello 智慧偵測摘要刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="b3777-174">If hello issue persist it will be updated in hello Smart Detection feed blade.</span></span>
* <span data-ttu-id="b3777-175">*我遺失 hello 電子郵件。其中 hello 入口網站中找到 hello 通知？*</span><span class="sxs-lookup"><span data-stu-id="b3777-175">*I lost hello email. Where can I find hello notifications in hello portal?*</span></span>
  * <span data-ttu-id="b3777-176">在 hello 的應用程式的 Application Insights 概觀，按一下 hello**智慧偵測**磚。</span><span class="sxs-lookup"><span data-stu-id="b3777-176">In hello Application Insights overview of your app, click hello **Smart Detection** tile.</span></span> <span data-ttu-id="b3777-177">您會有無法 toofind back up too90 天的所有通知。</span><span class="sxs-lookup"><span data-stu-id="b3777-177">There you'll be able toofind all notifications up too90 days back.</span></span>

## <a name="how-can-i-improve-performance"></a><span data-ttu-id="b3777-178">如何改善效能？</span><span class="sxs-lookup"><span data-stu-id="b3777-178">How can I improve performance?</span></span>
<span data-ttu-id="b3777-179">因為您知道從您自己的經驗，速度慢且失敗的回應是 hello 網站使用者的最大麻煩的其中一個。</span><span class="sxs-lookup"><span data-stu-id="b3777-179">Slow and failed responses are one of hello biggest frustrations for web site users, as you know from your own experience.</span></span> <span data-ttu-id="b3777-180">因此，請務必 tooaddress hello 問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-180">So, it's important tooaddress hello issues.</span></span>

### <a name="triage"></a><span data-ttu-id="b3777-181">分級</span><span class="sxs-lookup"><span data-stu-id="b3777-181">Triage</span></span>
<span data-ttu-id="b3777-182">首先，這很重要嗎？</span><span class="sxs-lookup"><span data-stu-id="b3777-182">First, does it matter?</span></span> <span data-ttu-id="b3777-183">如果頁面一律為慢速 tooload，但僅有 1%的站台的使用者永遠在它有 toolook，或許您有更重要的事情 toothink 有關。</span><span class="sxs-lookup"><span data-stu-id="b3777-183">If a page is always slow tooload, but only 1% of your site's users ever have toolook at it, maybe you have more important things toothink about.</span></span> <span data-ttu-id="b3777-184">在 hello 相反地，如果只有 1%的使用者開啟它，但它可能是值得調查每次擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b3777-184">On hello other hand, if only 1% of users open it, but it throws exceptions every time, that might be worth investigating.</span></span>

<span data-ttu-id="b3777-185">一般方針是，使用 hello 影響陳述式 （受影響的使用者或 %的流量），但請注意，它不會 hello 整個本文。</span><span class="sxs-lookup"><span data-stu-id="b3777-185">Use hello impact statement (affected users or % of traffic) as a general guide, but be aware that it isn't hello whole story.</span></span> <span data-ttu-id="b3777-186">收集其他的辨識項 tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="b3777-186">Gather other evidence tooconfirm.</span></span>

<span data-ttu-id="b3777-187">請考慮 hello 問題的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="b3777-187">Consider hello parameters of hello issue.</span></span> <span data-ttu-id="b3777-188">如果與地理位置有關，請設定包括該地區的 [可用性測試](app-insights-monitor-web-app-availability.md) ：該地區可能只有網路問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-188">If it's geography-dependent, set up [availability tests](app-insights-monitor-web-app-availability.md) including that region: there might simply be network issues in that area.</span></span>

### <a name="diagnose-slow-page-loads"></a><span data-ttu-id="b3777-189">診斷頁面載入緩慢</span><span class="sxs-lookup"><span data-stu-id="b3777-189">Diagnose slow page loads</span></span>
<span data-ttu-id="b3777-190">其中是 hello 問題？</span><span class="sxs-lookup"><span data-stu-id="b3777-190">Where is hello problem?</span></span> <span data-ttu-id="b3777-191">是 hello 伺服器緩慢 toorespond、 hello 網頁很長，或 hello 瀏覽器沒有 toodo 大量工作 toodisplay 它嗎？</span><span class="sxs-lookup"><span data-stu-id="b3777-191">Is hello server slow toorespond, is hello page very long, or does hello browser have toodo a lot of work toodisplay it?</span></span>

<span data-ttu-id="b3777-192">開啟 hello 瀏覽器計量刀鋒伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3777-192">Open hello Browsers metric blade.</span></span> <span data-ttu-id="b3777-193">hello 分割瀏覽器頁面載入時間顯示即將 hello 時間的顯示。</span><span class="sxs-lookup"><span data-stu-id="b3777-193">hello segmented display of browser page load time shows where hello time is going.</span></span> 

* <span data-ttu-id="b3777-194">如果**傳送要求時間**是高，可能是 hello 伺服器回應很慢，或 hello 要求是使用大量資料的文章。</span><span class="sxs-lookup"><span data-stu-id="b3777-194">If **Send Request Time** is high, either hello server is responding slowly, or hello request is a post with a lot of data.</span></span> <span data-ttu-id="b3777-195">查看 hello[效能度量](app-insights-web-monitor-performance.md#metrics)tooinvestigate 回應時間。</span><span class="sxs-lookup"><span data-stu-id="b3777-195">Look at hello [performance metrics](app-insights-web-monitor-performance.md#metrics) tooinvestigate response times.</span></span>
* <span data-ttu-id="b3777-196">設定[相依性追蹤](app-insights-asp-net-dependencies.md)toosee hello 緩慢是否到期 tooexternal 服務或您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b3777-196">Set up [dependency tracking](app-insights-asp-net-dependencies.md) toosee whether hello slowness is due tooexternal services or your database.</span></span>
* <span data-ttu-id="b3777-197">如果 [接收回應]  是主導因素，您的頁面和其相依組件 (JavaScript、CSS 及影像等，而非以非同步方式載入的資料) 會很長。</span><span class="sxs-lookup"><span data-stu-id="b3777-197">If **Receiving Response** is predominant, your page and its dependent parts - JavaScript, CSS, images and so on (but not asynchronously loaded data) are long.</span></span> <span data-ttu-id="b3777-198">設定[可用性測試](app-insights-monitor-web-app-availability.md)，而且是確定 tooset hello 選項 tooload 相依組件。</span><span class="sxs-lookup"><span data-stu-id="b3777-198">Set up an [availability test](app-insights-monitor-web-app-availability.md), and be sure tooset hello option tooload dependent parts.</span></span> <span data-ttu-id="b3777-199">當您取得一些結果時，開啟結果的 hello 詳細資料並將其展開 toosee hello 載入不同的檔案的時間。</span><span class="sxs-lookup"><span data-stu-id="b3777-199">When you get some results, open hello detail of a result and expand it toosee hello load times of different files.</span></span>
* <span data-ttu-id="b3777-200">[用戶端處理時間]  過長表示指令碼執行速度很慢。</span><span class="sxs-lookup"><span data-stu-id="b3777-200">High **Client Processing time** suggests scripts are running slowly.</span></span> <span data-ttu-id="b3777-201">如果 hello 原因不明顯，請考慮加入一些執行時間程式碼，並傳送 hello 次 trackMetric 呼叫中。</span><span class="sxs-lookup"><span data-stu-id="b3777-201">If hello reason isn't obvious, consider adding some timing code and send hello times in trackMetric calls.</span></span>

### <a name="improve-slow-pages"></a><span data-ttu-id="b3777-202">改善慢速網頁</span><span class="sxs-lookup"><span data-stu-id="b3777-202">Improve slow pages</span></span>
<span data-ttu-id="b3777-203">沒有完整的建議改善您的伺服器回應和頁面載入時間，所以不會再次嘗試 toorepeat web 它在這裡。</span><span class="sxs-lookup"><span data-stu-id="b3777-203">There's a web full of advice on improving your server responses and page load times, so we won't try toorepeat it all here.</span></span> <span data-ttu-id="b3777-204">以下是少數的提示，您可能已經了解只 tooget 你想：</span><span class="sxs-lookup"><span data-stu-id="b3777-204">Here are a few tips that you probably already know about, just tooget you thinking:</span></span>

* <span data-ttu-id="b3777-205">慢速載入因為大型的檔案： 以非同步方式載入 hello 指令碼和其他組件。</span><span class="sxs-lookup"><span data-stu-id="b3777-205">Slow loading because of big files: Load hello scripts and other parts asynchronously.</span></span> <span data-ttu-id="b3777-206">使用指令碼統合。</span><span class="sxs-lookup"><span data-stu-id="b3777-206">Use script bundling.</span></span> <span data-ttu-id="b3777-207">分成個別載入其資料的 widget hello 主頁面。</span><span class="sxs-lookup"><span data-stu-id="b3777-207">Break hello main page into widgets that load their data separately.</span></span> <span data-ttu-id="b3777-208">不要傳送長資料表純舊 HTML： 指令碼 toorequest hello 資料做為 JSON 或其他精簡的格式，然後再填滿 hello 資料表中的位置。</span><span class="sxs-lookup"><span data-stu-id="b3777-208">Don't send plain old HTML for long tables: use a script toorequest hello data as JSON or other compact format, then fill hello table in place.</span></span> <span data-ttu-id="b3777-209">沒有與這個所有絕佳架構 toohelp。</span><span class="sxs-lookup"><span data-stu-id="b3777-209">There are great frameworks toohelp with all this.</span></span> <span data-ttu-id="b3777-210">(當然，也必須承擔大型指令碼)。</span><span class="sxs-lookup"><span data-stu-id="b3777-210">(They also entail big scripts, of course.)</span></span>
* <span data-ttu-id="b3777-211">降低伺服器的相依性： 請考慮 hello 元件的地理位置。</span><span class="sxs-lookup"><span data-stu-id="b3777-211">Slow server dependencies: Consider hello geographical locations of your components.</span></span> <span data-ttu-id="b3777-212">例如，如果您使用 Azure，請確定 hello 網頁伺服器與 hello 資料庫都處於 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="b3777-212">For example, if you're using Azure, make sure hello web server and hello database are in hello same region.</span></span> <span data-ttu-id="b3777-213">查詢是否會擷取超過所需的資訊？</span><span class="sxs-lookup"><span data-stu-id="b3777-213">Do queries retrieve more information than they need?</span></span> <span data-ttu-id="b3777-214">快取或批次處理是否有所幫助？</span><span class="sxs-lookup"><span data-stu-id="b3777-214">Would caching or batching help?</span></span>
* <span data-ttu-id="b3777-215">容量問題： 查看 hello 伺服器的度量資訊的回應時間，並要求計數。</span><span class="sxs-lookup"><span data-stu-id="b3777-215">Capacity issues: Look at hello server metrics of response times and request counts.</span></span> <span data-ttu-id="b3777-216">如果回應時間尖峰與要求計數尖峰不成比例，有可能是您的伺服器已被過度使用。</span><span class="sxs-lookup"><span data-stu-id="b3777-216">If response times peak disproportionately with peaks in request counts, it's likely that your servers are stretched.</span></span>


## <a name="server-response-time-degradation"></a><span data-ttu-id="b3777-217">伺服器回應時間降低</span><span class="sxs-lookup"><span data-stu-id="b3777-217">Server Response Time Degradation</span></span>

<span data-ttu-id="b3777-218">hello 回應時間降低通知會告訴您：</span><span class="sxs-lookup"><span data-stu-id="b3777-218">hello response time degradation notification tells you:</span></span>

* <span data-ttu-id="b3777-219">hello 回應時間會比較 toonormal 這項作業的回應時間。</span><span class="sxs-lookup"><span data-stu-id="b3777-219">hello response time compared toonormal response time for this operation.</span></span>
* <span data-ttu-id="b3777-220">受影響的使用者人數。</span><span class="sxs-lookup"><span data-stu-id="b3777-220">How many users are affected.</span></span>
* <span data-ttu-id="b3777-221">平均回應時間及 90th 百分位數的回應時間 hello 當天 hello 偵測和 7 天前的此作業。</span><span class="sxs-lookup"><span data-stu-id="b3777-221">Average response time and 90th percentile response time for this operation on hello day of hello detection and 7 days before.</span></span> 
* <span data-ttu-id="b3777-222">這項作業的計數要求的 hello 偵測的 hello 日期和 7 天前。</span><span class="sxs-lookup"><span data-stu-id="b3777-222">Count of this operation requests on hello day of hello detection and 7 days before.</span></span>
* <span data-ttu-id="b3777-223">這項作業之降低與相關相依性之降低間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b3777-223">Correlation between degradation in this operation and degradations in related dependencies.</span></span> 
* <span data-ttu-id="b3777-224">連結 toohelp 診斷 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-224">Links toohelp you diagnose hello problem.</span></span>
  * <span data-ttu-id="b3777-225">分析工具會追蹤您檢視作業的時間花在哪裡 toohelp （hello 連結是使用這項作業在 hello 偵測期間所收集的 Profiler 追蹤範例）。</span><span class="sxs-lookup"><span data-stu-id="b3777-225">Profiler traces toohelp you view where operation time is spent (hello link is available if Profiler trace examples were collected for this operation during hello detection period).</span></span> 
  * <span data-ttu-id="b3777-226">您可以在計量瀏覽器中的效能報告將這項作業的時間範圍/篩選條件進行交叉分析。</span><span class="sxs-lookup"><span data-stu-id="b3777-226">Performance reports in Metric Explorer, where you can slice and dice time range/filters for this operation.</span></span>
  * <span data-ttu-id="b3777-227">這個搜尋呼叫 tooview 特定呼叫屬性。</span><span class="sxs-lookup"><span data-stu-id="b3777-227">Search for this calls tooview specific calls properties.</span></span>
  * <span data-ttu-id="b3777-228">報告失敗-如果計數 1 >，這表示可能有貢獻 tooperformance 降低此作業中發生失敗。</span><span class="sxs-lookup"><span data-stu-id="b3777-228">Failure reports - If count > 1 this mean that there were failures in this operation that might have contributed tooperformance degradation.</span></span>

## <a name="dependency-duration-degradation"></a><span data-ttu-id="b3777-229">相依性持續時間降低</span><span class="sxs-lookup"><span data-stu-id="b3777-229">Dependency Duration Degradation</span></span>

<span data-ttu-id="b3777-230">現代應用程式更採用微服務設計的方法，在許多情況下導致 tooheavy 可靠性外部服務。</span><span class="sxs-lookup"><span data-stu-id="b3777-230">Modern application more and more adopt micro services design approach, which in many cases leads tooheavy reliability on external services.</span></span> <span data-ttu-id="b3777-231">例如，如果您的應用程式依賴某些資料平台，或您建立您自己 bot 服務您將可能轉送上某些認知的服務提供者 tooenable 多人為方式您 bot toointeract 和一些資料儲存區服務 bot toopull hello來自的答案。</span><span class="sxs-lookup"><span data-stu-id="b3777-231">For example, if your application relies on some data platform or even if you build your own bot service you will probably relay on some cognitive services provider tooenable your bots toointeract in more human ways and some data store service for bot toopull hello answers from.</span></span>  

<span data-ttu-id="b3777-232">範例相依性降低通知︰</span><span class="sxs-lookup"><span data-stu-id="b3777-232">Example dependency degradation notification:</span></span>

![以下是相依性持續時間降低偵測的範例](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

<span data-ttu-id="b3777-234">請注意，它會告訴您︰</span><span class="sxs-lookup"><span data-stu-id="b3777-234">Notice that it tells you:</span></span>

* <span data-ttu-id="b3777-235">hello 持續時間會比較 toonormal 這項作業的回應時間</span><span class="sxs-lookup"><span data-stu-id="b3777-235">hello duration compared toonormal response time for this operation</span></span>
* <span data-ttu-id="b3777-236">受影響的使用者人數</span><span class="sxs-lookup"><span data-stu-id="b3777-236">How many users are affected</span></span>
* <span data-ttu-id="b3777-237">平均持續時間和 90th 百分位數持續時間此相依性的 hello 偵測的 hello 日期和 7 天前</span><span class="sxs-lookup"><span data-stu-id="b3777-237">Average duration and 90th percentile duration for this dependency on hello day of hello detection and 7 days before</span></span>
* <span data-ttu-id="b3777-238">Hello 天數 hello 偵測和 7 天前呼叫的相依性的數目</span><span class="sxs-lookup"><span data-stu-id="b3777-238">Number of dependency calls on hello day of hello detection and 7 days before</span></span>
* <span data-ttu-id="b3777-239">連結 toohelp 診斷 hello 問題</span><span class="sxs-lookup"><span data-stu-id="b3777-239">Links toohelp you diagnose hello problem</span></span>
  * <span data-ttu-id="b3777-240">計量瀏覽器中此相依性的效能報告</span><span class="sxs-lookup"><span data-stu-id="b3777-240">Performance reports in Metric Explorer for this dependency</span></span>
  * <span data-ttu-id="b3777-241">搜尋此相依性呼叫 tooview 呼叫屬性</span><span class="sxs-lookup"><span data-stu-id="b3777-241">Search for this dependency calls tooview calls properties</span></span>
  * <span data-ttu-id="b3777-242">失敗 」 報告會-如果計數 > 1 表示已失敗的相依性呼叫期間 hello 偵測可能會有貢獻 tooduration 降級的期間。</span><span class="sxs-lookup"><span data-stu-id="b3777-242">Failure reports - If count > 1 this mean that there were failed dependency calls during hello detection period that might have contributed tooduration degradation.</span></span> 
  * <span data-ttu-id="b3777-243">使用計算此相依性持續時間和計數的查詢來開啟分析</span><span class="sxs-lookup"><span data-stu-id="b3777-243">Open Analytics with queries that calculate this dependency duration and count</span></span>  

## <a name="smart-detection-of-slow-performing-patterns"></a><span data-ttu-id="b3777-244">效能變慢模式的智慧型偵測</span><span class="sxs-lookup"><span data-stu-id="b3777-244">Smart Detection of slow performing patterns</span></span> 

<span data-ttu-id="b3777-245">Application Insights 會尋找可能只會影響某部分使用者，或只在某些情況下影響使用者的效能問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-245">Application Insights finds performance issues that might only affect some portion of your users, or only affect users in some cases.</span></span> <span data-ttu-id="b3777-246">例如，通知關於頁面在某一類型瀏覽器上的載入速度低於其他類型瀏覽器，或特定伺服器服務要求的速度較慢。</span><span class="sxs-lookup"><span data-stu-id="b3777-246">For example, notification about pages load is slowler on one type of browser than on other types of browsers, or if requests are served more slowly from a particular server.</span></span> <span data-ttu-id="b3777-247">它同時可以探索與屬性組合相關的問題，例如在某地區中使用特定作業系統的用戶端，頁面載入速度緩慢的問題。</span><span class="sxs-lookup"><span data-stu-id="b3777-247">It can also discover problems associated with combinations of properties, such as slow page loads in one geographical area for clients using particular operating system.</span></span>  

<span data-ttu-id="b3777-248">這類的異常狀況是很難 toodetect 只是藉由檢查 hello 資料，但比您想像的較常見。</span><span class="sxs-lookup"><span data-stu-id="b3777-248">Anomalies like these are very hard toodetect just by inspecting hello data, but are more common than you might think.</span></span> <span data-ttu-id="b3777-249">通常只在您的客戶抱怨時才會浮出檯面。</span><span class="sxs-lookup"><span data-stu-id="b3777-249">Often they only surface when your customers complain.</span></span> <span data-ttu-id="b3777-250">藉由這段時間，很晚： hello 受影響的使用者已切換 tooyour 競爭對手 ！</span><span class="sxs-lookup"><span data-stu-id="b3777-250">By that time, it’s too late: hello affected users are already switching tooyour competitors!</span></span>

<span data-ttu-id="b3777-251">目前，我們演算法會尋找在頁面載入時間，在 hello 伺服器的要求回應時間和相依性回應時間。</span><span class="sxs-lookup"><span data-stu-id="b3777-251">Currently, our algorithms look at page load times, request response times at hello server, and dependency response times.</span></span>  

<span data-ttu-id="b3777-252">您尚未 tooset 任何臨界值，或設定規則。</span><span class="sxs-lookup"><span data-stu-id="b3777-252">You don't have tooset any thresholds or configure rules.</span></span> <span data-ttu-id="b3777-253">機器學習和資料採礦演算法會使用的 toodetect 的異常模式。</span><span class="sxs-lookup"><span data-stu-id="b3777-253">Machine learning and data mining algorithms are used toodetect abnormal patterns.</span></span>

![從 hello 電子郵件警示，按一下 hello 連結 tooopen hello 診斷報告在 Azure 中](./media/app-insights-proactive-performance-diagnostics/03.png)

* <span data-ttu-id="b3777-255">**當**顯示偵測到 hello hello 問題的時間。</span><span class="sxs-lookup"><span data-stu-id="b3777-255">**When** shows hello time hello issue was detected.</span></span>
* <span data-ttu-id="b3777-256">[對象] 說明：</span><span class="sxs-lookup"><span data-stu-id="b3777-256">**What** describes:</span></span>

  * <span data-ttu-id="b3777-257">所偵測到; hello 問題</span><span class="sxs-lookup"><span data-stu-id="b3777-257">hello problem that was detected;</span></span>
  * <span data-ttu-id="b3777-258">我們發現顯示 hello 問題行為的事件集的 hello hello 特性。</span><span class="sxs-lookup"><span data-stu-id="b3777-258">hello characteristics of hello set of events that we found displayed hello problem behavior.</span></span>
* <span data-ttu-id="b3777-259">hello 表會比較 hello 佳的資料集的所有其他事件 hello 平均行為。</span><span class="sxs-lookup"><span data-stu-id="b3777-259">hello table compares hello poorly-performing set with hello average behavior of all other events.</span></span>

<span data-ttu-id="b3777-260">按一下相關的報告，hello 時間以及 hello 慢速執行設定的屬性篩選 hello 連結 tooopen 度量總管和搜尋。</span><span class="sxs-lookup"><span data-stu-id="b3777-260">Click hello links tooopen Metric Explorer and Search on relevant reports, filtered on hello time and properties of hello slow performing set.</span></span>

<span data-ttu-id="b3777-261">修改 hello 時間範圍和篩選 tooexplore hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="b3777-261">Modify hello time range and filters tooexplore hello telemetry.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3777-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3777-262">Next steps</span></span>
<span data-ttu-id="b3777-263">這些診斷工具可協助您檢查您的應用程式的遙測 hello:</span><span class="sxs-lookup"><span data-stu-id="b3777-263">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="b3777-264">分析工具</span><span class="sxs-lookup"><span data-stu-id="b3777-264">Profiler</span></span>](app-insights-profiler.md) 
* [<span data-ttu-id="b3777-265">快照集偵錯工具</span><span class="sxs-lookup"><span data-stu-id="b3777-265">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
* [<span data-ttu-id="b3777-266">分析</span><span class="sxs-lookup"><span data-stu-id="b3777-266">Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="b3777-267">分析智慧型診斷</span><span class="sxs-lookup"><span data-stu-id="b3777-267">Analytics smart diagnostics</span></span>](app-insights-analytics-diagnostics.md)

<span data-ttu-id="b3777-268">智慧型偵測是完全自動的。</span><span class="sxs-lookup"><span data-stu-id="b3777-268">Smart detections are completely automatic.</span></span> <span data-ttu-id="b3777-269">但您可能要 tooset 某些更多的警示嗎？</span><span class="sxs-lookup"><span data-stu-id="b3777-269">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="b3777-270">手動設定的度量警示</span><span class="sxs-lookup"><span data-stu-id="b3777-270">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="b3777-271">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="b3777-271">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
