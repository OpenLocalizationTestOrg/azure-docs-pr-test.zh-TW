---
title: "智慧型偵測 - Application Insights 中的失敗異常 | Microsoft Docs"
description: "針對 Web 應用程式失敗要求比率的不尋常變化對您發出警示，並提供診斷分析。 不需要設定。"
services: application-insights
documentationcenter: 
author: yorac
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: bwren
ms.openlocfilehash: e82d35459110e122ec8438b406a52df61922b0fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection---failure-anomalies"></a><span data-ttu-id="1e81c-104">智慧型偵測 - 失敗異常</span><span class="sxs-lookup"><span data-stu-id="1e81c-104">Smart Detection - Failure Anomalies</span></span>
<span data-ttu-id="1e81c-105">當 Web 應用程式的失敗要求比率異常增加時，[Application Insights](app-insights-overview.md) 會以幾乎即時的方式自動通知您。</span><span class="sxs-lookup"><span data-stu-id="1e81c-105">[Application Insights](app-insights-overview.md) automatically notifies you in near real time if your web app experiences an abnormal rise in the rate of failed requests.</span></span> <span data-ttu-id="1e81c-106">它偵測到回報為失敗的 HTTP 要求率異常提高或相依性呼叫。</span><span class="sxs-lookup"><span data-stu-id="1e81c-106">It detects an unusual rise in the rate of HTTP requests or dependency calls that are reported as failed.</span></span> <span data-ttu-id="1e81c-107">對於要求，失敗的要求通常是回應碼為 400 或更高的要求。</span><span class="sxs-lookup"><span data-stu-id="1e81c-107">For requests, failed requests are usually those with response codes of 400 or higher.</span></span> <span data-ttu-id="1e81c-108">為了協助您分級並診斷問題，通知中會提供失敗的特性分析與相關遙測。</span><span class="sxs-lookup"><span data-stu-id="1e81c-108">To help you triage and diagnose the problem, an analysis of the characteristics of the failures and related telemetry is provided in the notification.</span></span> <span data-ttu-id="1e81c-109">其中也有 Application Insights 入口網站的連結，以供進一步診斷。</span><span class="sxs-lookup"><span data-stu-id="1e81c-109">There are also links to the Application Insights portal for further diagnosis.</span></span> <span data-ttu-id="1e81c-110">不需要設定該功能，因為它是使用機器學習演算法來預測一般失敗率。</span><span class="sxs-lookup"><span data-stu-id="1e81c-110">The feature needs no set-up nor configuration, as it uses machine learning algorithms to predict the normal failure rate.</span></span>

<span data-ttu-id="1e81c-111">這項功能適用於 Java 和 ASP.NET Web 應用程式，其裝載於雲端或您自己的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1e81c-111">This feature works for Java and ASP.NET web apps, hosted in the cloud or on your own servers.</span></span> <span data-ttu-id="1e81c-112">它也適用於產生要求或相依性遙測的任何應用程式 - 例如，如果您有呼叫 [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) 或 [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency) 的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="1e81c-112">It also works for any app that generates request or dependency telemetry - for example, if you have a worker role that calls [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) or [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

<span data-ttu-id="1e81c-113">設定[專案的 Application Insights](app-insights-overview.md)之後，如果您的應用程式產生某些最少量的遙測，錯誤異常的「智慧型偵測」需先花費 24 小時來了解您應用程式的正常行為，然後才會啟動而能夠傳送警示。</span><span class="sxs-lookup"><span data-stu-id="1e81c-113">After setting up [Application Insights for your project](app-insights-overview.md), and provided your app generates a certain minimum amount of telemetry, Smart Detection of failure anomalies takes 24 hours to learn the normal behavior of your app, before it is switched on and can send alerts.</span></span>

<span data-ttu-id="1e81c-114">以下是警示範例。</span><span class="sxs-lookup"><span data-stu-id="1e81c-114">Here's a sample alert.</span></span>

![顯示失敗相關叢集分析的範例智慧型偵測警示](./media/app-insights-proactive-failure-diagnostics/013.png)

> [!NOTE]
> <span data-ttu-id="1e81c-116">根據預設，您所取得的郵件格式會比這個範例還簡短。</span><span class="sxs-lookup"><span data-stu-id="1e81c-116">By default, you get a shorter format mail than this example.</span></span> <span data-ttu-id="1e81c-117">不過，您也可以 [切換到這個詳細格式](#configure-alerts)。</span><span class="sxs-lookup"><span data-stu-id="1e81c-117">But you can [switch to this detailed format](#configure-alerts).</span></span>
>
>

<span data-ttu-id="1e81c-118">請注意，它會告訴您︰</span><span class="sxs-lookup"><span data-stu-id="1e81c-118">Notice that it tells you:</span></span>

* <span data-ttu-id="1e81c-119">相較於一般應用程式行為的失敗率。</span><span class="sxs-lookup"><span data-stu-id="1e81c-119">The failure rate compared to normal app behavior.</span></span>
* <span data-ttu-id="1e81c-120">受影響的使用者人數 – 讓您知道應處理的數目。</span><span class="sxs-lookup"><span data-stu-id="1e81c-120">How many users are affected – so you know how much to worry.</span></span>
* <span data-ttu-id="1e81c-121">與失敗關聯的特性模式。</span><span class="sxs-lookup"><span data-stu-id="1e81c-121">A characteristic pattern associated with the failures.</span></span> <span data-ttu-id="1e81c-122">在此範例中，有特定的回應碼、要求名稱 (操作) 和應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="1e81c-122">In this example, there’s a particular response code, request name (operation) and app version.</span></span> <span data-ttu-id="1e81c-123">可立即告訴您從何處開始了解程式碼。</span><span class="sxs-lookup"><span data-stu-id="1e81c-123">That immediately tells you where to start looking in your code.</span></span> <span data-ttu-id="1e81c-124">其他可能性則可能是特定的瀏覽器或用戶端作業系統。</span><span class="sxs-lookup"><span data-stu-id="1e81c-124">Other possibilities could be a specific browser or client operating system.</span></span>
* <span data-ttu-id="1e81c-125">看起來似乎與特色失敗相關聯的例外狀況、記錄追蹤和相依性失敗 (資料庫或其他外部元件)。</span><span class="sxs-lookup"><span data-stu-id="1e81c-125">The exception, log traces, and dependency failure (databases or other external components) that appear to be associated with the characterized failures.</span></span>
* <span data-ttu-id="1e81c-126">直接連結到 Application Insights 的遙測上相關搜尋。</span><span class="sxs-lookup"><span data-stu-id="1e81c-126">Links directly to relevant searches on the telemetry in Application Insights.</span></span>

## <a name="benefits-of-smart-detection"></a><span data-ttu-id="1e81c-127">智慧型偵測的優點</span><span class="sxs-lookup"><span data-stu-id="1e81c-127">Benefits of Smart Detection</span></span>
<span data-ttu-id="1e81c-128">一般的 [度量警示](app-insights-alerts.md) 會告訴您可能有問題。</span><span class="sxs-lookup"><span data-stu-id="1e81c-128">Ordinary [metric alerts](app-insights-alerts.md) tell you there might be a problem.</span></span> <span data-ttu-id="1e81c-129">但「智慧型偵測」會為您啟動診斷工作，執行許多您原本必須自己執行的分析。</span><span class="sxs-lookup"><span data-stu-id="1e81c-129">But Smart Detection starts the diagnostic work for you, performing a lot of the analysis you would otherwise have to do yourself.</span></span> <span data-ttu-id="1e81c-130">您達到幾近封裝完成的結果，幫助您快速取得問題的根源。</span><span class="sxs-lookup"><span data-stu-id="1e81c-130">You get the results neatly packaged, helping you to get quickly to the root of the problem.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1e81c-131">運作方式</span><span class="sxs-lookup"><span data-stu-id="1e81c-131">How it works</span></span>
<span data-ttu-id="1e81c-132">「智慧型偵測」會監視從應用程式收到的遙測，特別是失敗率的遙測。</span><span class="sxs-lookup"><span data-stu-id="1e81c-132">Smart  Detection monitors the telemetry received from your app, and in particular the failure rates.</span></span> <span data-ttu-id="1e81c-133">此規則會計算 `Successful request` 屬性為 false 的要求數，以及 `Successful call` 屬性為 false 的相依性呼叫數。</span><span class="sxs-lookup"><span data-stu-id="1e81c-133">This rule counts the number of requests for which the `Successful request` property is false, and the number of dependency calls for which the `Successful call` property is false.</span></span> <span data-ttu-id="1e81c-134">對於要求，根據預設，`Successful request == (resultCode < 400)` (除非您撰寫自訂程式碼來[篩選](app-insights-api-filtering-sampling.md#filtering)或產生自己的 [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) 呼叫)。</span><span class="sxs-lookup"><span data-stu-id="1e81c-134">For requests, by default, `Successful request == (resultCode < 400)` (unless you have written custom code to [filter](app-insights-api-filtering-sampling.md#filtering) or generate your own [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) calls).</span></span> 

<span data-ttu-id="1e81c-135">您的應用程式效能具有一般的行為模式。</span><span class="sxs-lookup"><span data-stu-id="1e81c-135">Your app’s performance has a typical pattern of behavior.</span></span> <span data-ttu-id="1e81c-136">某些要求或相依性呼叫會比其他要求更容易失敗；且整體失敗率可能會隨著負載增加而上移。</span><span class="sxs-lookup"><span data-stu-id="1e81c-136">Some requests or dependency calls will be more prone to failure than others; and the overall failure rate may go up as load increases.</span></span> <span data-ttu-id="1e81c-137">「智慧型偵測」會使用機器學習服務來尋找這些異常狀況。</span><span class="sxs-lookup"><span data-stu-id="1e81c-137">Smart Detection uses machine learning to find these anomalies.</span></span>

<span data-ttu-id="1e81c-138">當遙測從您的 Web 應用程式進入 Application Insights 時，「智慧型偵測」會將目前的行為與過去幾天觀察到的模式做比較。</span><span class="sxs-lookup"><span data-stu-id="1e81c-138">As telemetry comes into Application Insights from your web app, Smart Detection compares the current behavior with the patterns seen over the past few days.</span></span> <span data-ttu-id="1e81c-139">如果觀察到與先前效能相比，失敗率異常提高，就會觸發分析。</span><span class="sxs-lookup"><span data-stu-id="1e81c-139">If an abnormal rise in failure rate is observed by comparison with previous performance, an analysis is triggered.</span></span>

<span data-ttu-id="1e81c-140">觸發分析時，服務會對失敗的要求執行叢集分析，以嘗試識別描述失敗特徵之值的模式。</span><span class="sxs-lookup"><span data-stu-id="1e81c-140">When an analysis is triggered, the service performs a cluster analysis on the failed request, to try to identify a pattern of values that characterize the failures.</span></span> <span data-ttu-id="1e81c-141">在上述範例中，分析已發現大部分失敗是關於特定結果碼、要求名稱、伺服器 URL 主機和角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="1e81c-141">In the example above, the analysis has discovered that most failures are about a specific result code, request name, Server URL host, and role instance.</span></span> <span data-ttu-id="1e81c-142">相反地，分析發現，用戶端作業系統屬性分散在多個值，因此未列出。</span><span class="sxs-lookup"><span data-stu-id="1e81c-142">By contrast, the analysis has discovered that the client operating system property is distributed over multiple values, and so it is not listed.</span></span>

<span data-ttu-id="1e81c-143">當您的服務使用這些遙測呼叫進行檢測時，分析器會尋找與已識別之叢集中的要求相關聯的例外狀況及相依性失敗，同時也包含與那些要求相關的任何追蹤記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="1e81c-143">When your service is instrumented with these telemetry calls, the analyser looks for an exception and a dependency failure that are associated with requests in the cluster it has identified, together with an example of any trace logs associated with those requests.</span></span>

<span data-ttu-id="1e81c-144">產生的分析報告會以警示寄送給您，除非您已設定不接收該報告。</span><span class="sxs-lookup"><span data-stu-id="1e81c-144">The resulting analysis is sent to you as alert, unless you have configured it not to.</span></span>

<span data-ttu-id="1e81c-145">如同 [您手動設定的警示](app-insights-alerts.md)，您可以檢查警示的狀態，並在 Application Insights 資源的 [警示] 刀鋒視窗中進行設定。</span><span class="sxs-lookup"><span data-stu-id="1e81c-145">Like the [alerts you set manually](app-insights-alerts.md), you can inspect the state of the alert and configure it in the Alerts blade of your Application Insights resource.</span></span> <span data-ttu-id="1e81c-146">但與其他警示不同，您並不需要設定「智慧型偵測」。</span><span class="sxs-lookup"><span data-stu-id="1e81c-146">But unlike other alerts, you don't need to set up or configure Smart Detection.</span></span> <span data-ttu-id="1e81c-147">若有需要，您可以將它停用或變更其目標電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1e81c-147">If you want, you can disable it or change its target email addresses.</span></span>

## <a name="configure-alerts"></a><span data-ttu-id="1e81c-148">設定警示</span><span class="sxs-lookup"><span data-stu-id="1e81c-148">Configure alerts</span></span>
<span data-ttu-id="1e81c-149">您可以停用「智慧型偵測」、變更電子郵件收件者、建立 Webhook，或選擇接收更詳細的警示訊息。</span><span class="sxs-lookup"><span data-stu-id="1e81c-149">You can disable Smart Detection, change the email recipients, create a webhook, or opt in to more detailed alert messages.</span></span>

<span data-ttu-id="1e81c-150">開啟 [警示] 頁面。</span><span class="sxs-lookup"><span data-stu-id="1e81c-150">Open the Alerts page.</span></span> <span data-ttu-id="1e81c-151">「失敗異常」已包含在任何您已手動設定的警示中，您可以查看它目前是否處於警示狀態。</span><span class="sxs-lookup"><span data-stu-id="1e81c-151">Failure Anomalies is included along with any alerts that you have set manually, and you can see whether it is currently in the alert state.</span></span>

![在 [概觀] 頁面中，按一下 [警示] 圖格。](./media/app-insights-proactive-failure-diagnostics/021.png)

<span data-ttu-id="1e81c-154">按一下警示來進行設定。</span><span class="sxs-lookup"><span data-stu-id="1e81c-154">Click the alert to configure it.</span></span>

![組態](./media/app-insights-proactive-failure-diagnostics/032.png)

<span data-ttu-id="1e81c-156">請注意，您可以停用「智慧型偵測」，但無法將它刪除 (或建立另一個「智慧型偵測」)。</span><span class="sxs-lookup"><span data-stu-id="1e81c-156">Notice that you can disable Smart Detection, but you can't delete it (or create another one).</span></span>

#### <a name="detailed-alerts"></a><span data-ttu-id="1e81c-157">詳細的警示</span><span class="sxs-lookup"><span data-stu-id="1e81c-157">Detailed alerts</span></span>
<span data-ttu-id="1e81c-158">如果您選取 [取得更詳細的診斷資料]，則電子郵件會包含詳細的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="1e81c-158">If you select "Get more detailed diagnostics" then the email will contain more diagnostic information.</span></span> <span data-ttu-id="1e81c-159">有時候您從電子郵件中的資料就能夠診斷問題。</span><span class="sxs-lookup"><span data-stu-id="1e81c-159">Sometimes you'll be able to diagnose the problem just from the data in the email.</span></span>

<span data-ttu-id="1e81c-160">因為更詳細的警示包含例外狀況和追蹤訊息，所以不太可能包含機密資訊。</span><span class="sxs-lookup"><span data-stu-id="1e81c-160">There's a slight risk that the more detailed alert could contain sensitive information, because it includes exception and trace messages.</span></span> <span data-ttu-id="1e81c-161">不過，只有當您的程式碼允許機密資訊進入這些訊息時，才會發生。</span><span class="sxs-lookup"><span data-stu-id="1e81c-161">However, this would only happen if your code could allow sensitive information into those messages.</span></span>

## <a name="triaging-and-diagnosing-an-alert"></a><span data-ttu-id="1e81c-162">分級和診斷警示</span><span class="sxs-lookup"><span data-stu-id="1e81c-162">Triaging and diagnosing an alert</span></span>
<span data-ttu-id="1e81c-163">發出警示表示系統偵測到要求失敗率異常上升。</span><span class="sxs-lookup"><span data-stu-id="1e81c-163">An alert indicates that an abnormal rise in the failed request rate was detected.</span></span> <span data-ttu-id="1e81c-164">原因可能是您的應用程式或其環境有問題。</span><span class="sxs-lookup"><span data-stu-id="1e81c-164">It's likely that there is some problem with your app or its environment.</span></span>

<span data-ttu-id="1e81c-165">您可以根據要求的百分比及受影響的使用者數目來決定此問題的緊急程度。</span><span class="sxs-lookup"><span data-stu-id="1e81c-165">From the percentage of requests and number of users affected, you can decide how urgent the issue is.</span></span> <span data-ttu-id="1e81c-166">在上述範例中，22.5% 的失敗率與正常比率 1% 相比，表示有問題。</span><span class="sxs-lookup"><span data-stu-id="1e81c-166">In the example above, the failure rate of 22.5% compares with a normal rate of 1%, indicates that something bad is going on.</span></span> <span data-ttu-id="1e81c-167">從另一方面來看，只有 11 位使用者受到影響。</span><span class="sxs-lookup"><span data-stu-id="1e81c-167">On the other hand, only 11 users were affected.</span></span> <span data-ttu-id="1e81c-168">如果是您的應用程式，您可以評估嚴重程度。</span><span class="sxs-lookup"><span data-stu-id="1e81c-168">If it were your app, you'd be able to assess how serious that is.</span></span>

<span data-ttu-id="1e81c-169">在多數情況下，您可以根據要求名稱、例外狀況、相依性失敗及提供的追蹤資料來快速診斷問題。</span><span class="sxs-lookup"><span data-stu-id="1e81c-169">In many cases, you will be able to diagnose the problem quickly from the request name, exception, dependency failure and trace data provided.</span></span>

<span data-ttu-id="1e81c-170">另有一些線索。</span><span class="sxs-lookup"><span data-stu-id="1e81c-170">There are some other clues.</span></span> <span data-ttu-id="1e81c-171">例如，此範例中的相依性失敗率與例外狀況率 (89.3%) 相同。</span><span class="sxs-lookup"><span data-stu-id="1e81c-171">For example, the dependency failure rate in this example is the same as the exception rate (89.3%).</span></span> <span data-ttu-id="1e81c-172">這可能表示例外狀況直接從相依性失敗產生，讓您清楚瞭解從何處開始查看程式碼。</span><span class="sxs-lookup"><span data-stu-id="1e81c-172">This suggests that the exception arises directly from the dependency failure - giving you a clear idea of where to start looking in your code.</span></span>

<span data-ttu-id="1e81c-173">若要進一步調查，每個區段中的連結將直接連結到已針對相關要求、例外狀況、相依性或追蹤篩選的 [搜尋頁面](app-insights-diagnostic-search.md) 。</span><span class="sxs-lookup"><span data-stu-id="1e81c-173">To investigate further, the links in each section will take you straight to a [search page](app-insights-diagnostic-search.md) filtered to the relevant requests, exception, dependency or traces.</span></span> <span data-ttu-id="1e81c-174">或者，您可以開啟 [Azure 入口網站](https://portal.azure.com)，瀏覽至應用程式的 Application Insights 資源，並開啟 [失敗] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1e81c-174">Or you can open the [Azure portal](https://portal.azure.com), navigate to the Application Insights resource for your app, and open the Failures blade.</span></span>

<span data-ttu-id="1e81c-175">在此範例中，按一下 [檢視相依性失敗詳細資料] 連結會開啟 [Application Insights 搜尋] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1e81c-175">In this example, clicking the 'View dependency failures details' link opens the Application Insights search blade.</span></span> <span data-ttu-id="1e81c-176">它會顯示具有根本原因範例的 SQL 陳述式︰必要欄位會提供 Null，而且在儲存作業過程中未通過驗證。</span><span class="sxs-lookup"><span data-stu-id="1e81c-176">It shows the SQL statement that has an example of the root cause: NULLs were provided at mandatory fields and did not pass validation during the save operation.</span></span>

![診斷搜尋](./media/app-insights-proactive-failure-diagnostics/051.png)

## <a name="review-recent-alerts"></a><span data-ttu-id="1e81c-178">檢閱最近的警示</span><span class="sxs-lookup"><span data-stu-id="1e81c-178">Review recent alerts</span></span>

<span data-ttu-id="1e81c-179">按一下 [智慧型偵測] 來移至最新的警示：</span><span class="sxs-lookup"><span data-stu-id="1e81c-179">Click **Smart Detection** to get to the most recent alert:</span></span>

![警示摘要](./media/app-insights-proactive-failure-diagnostics/070.png)


## <a name="whats-the-difference-"></a><span data-ttu-id="1e81c-181">不同之處在於...</span><span class="sxs-lookup"><span data-stu-id="1e81c-181">What's the difference ...</span></span>
<span data-ttu-id="1e81c-182">失敗異常的「智慧型偵測」可以與其他相似但不同的 Application Insights 功能互補。</span><span class="sxs-lookup"><span data-stu-id="1e81c-182">Smart Detection of failure anomalies complements other similar but distinct features of Application Insights.</span></span>

* <span data-ttu-id="1e81c-183">您可以設定[度量警示](app-insights-alerts.md)，且可以檢視各種度量，例如 CPU 使用量、要求率、頁面載入時間等等。</span><span class="sxs-lookup"><span data-stu-id="1e81c-183">[Metric Alerts](app-insights-alerts.md) are set by you and can monitor a wide range of metrics such as CPU occupancy, request rates,  page load times, and so on.</span></span> <span data-ttu-id="1e81c-184">您可以使用它們來向自己發出警告，例如，如果您需要增加更多資源時。</span><span class="sxs-lookup"><span data-stu-id="1e81c-184">You can use them to warn you, for example, if you need to add more resources.</span></span> <span data-ttu-id="1e81c-185">對比之下，失敗異常的「智慧型偵測」只涵蓋小範圍的重要度量 (目前僅包含要求失敗率)，其設計目的是要在 Web 應用程式的要求失敗率與其正常行為相比有明顯增加時，能以幾乎即時的方式通知您。</span><span class="sxs-lookup"><span data-stu-id="1e81c-185">By contrast, Smart Detection of failure anomalies covers a small range of critical metrics (currently only failed request rate), designed to notify you in near real time manner once your web app's failed request rate increases significantly compared to web app's normal behavior.</span></span>

    <span data-ttu-id="1e81c-186">「智慧型偵測」會自動因應主要條件來調整其臨界值。</span><span class="sxs-lookup"><span data-stu-id="1e81c-186">Smart Detection automatically adjusts its threshold in response to prevailing conditions.</span></span>

    <span data-ttu-id="1e81c-187">「智慧型偵測」會為您啟動診斷工作。</span><span class="sxs-lookup"><span data-stu-id="1e81c-187">Smart Detection starts the diagnostic work for you.</span></span>
* <span data-ttu-id="1e81c-188">[效能異常的智慧型偵測](app-insights-proactive-performance-diagnostics.md)也會使用機器智慧在您的度量中探索不尋常的模式，且您不需要進行任何設定。</span><span class="sxs-lookup"><span data-stu-id="1e81c-188">[Smart Detection of performance anomalies](app-insights-proactive-performance-diagnostics.md) also uses machine intelligence to discover unusual patterns in your metrics, and no configuration by you is required.</span></span> <span data-ttu-id="1e81c-189">但與失敗異常的「智慧型偵測」不同，效能異常的「智慧型偵測」目的是要尋找您各種使用方式中未獲得正確處理的片段，例如未獲得特定瀏覽器上特定的頁面正確處理。</span><span class="sxs-lookup"><span data-stu-id="1e81c-189">But unlike Smart Detection of failure anomalies, the purpose of Smart  Detection of performance anomalies is to find segments of your usage manifold that might be badly served - for example, by specific pages on a specific type of browser.</span></span> <span data-ttu-id="1e81c-190">此分析會每日執行，且如果發現任何結果，它可能不像警示那麼緊急。</span><span class="sxs-lookup"><span data-stu-id="1e81c-190">The analysis is performed daily, and if any result is found, it's likely to be much less urgent than an alert.</span></span> <span data-ttu-id="1e81c-191">對比之下，失敗異常的分析則是會對傳入的遙測持續執行，且如果伺服器失敗率超出預期，您就會在幾分鐘內收到通知。</span><span class="sxs-lookup"><span data-stu-id="1e81c-191">By contrast, the analysis for failure anomalies is performed continuously on incoming telemetry, and you will be notified within minutes if server failure rates are greater than expected.</span></span>

## <a name="if-you-receive-a-smart-detection-alert"></a><span data-ttu-id="1e81c-192">如果您收到「智慧型偵測」警示</span><span class="sxs-lookup"><span data-stu-id="1e81c-192">If you receive a Smart Detection alert</span></span>
<span data-ttu-id="1e81c-193">*為什麼會收到這個警示？*</span><span class="sxs-lookup"><span data-stu-id="1e81c-193">*Why have I received this alert?*</span></span>

* <span data-ttu-id="1e81c-194">我們偵測到要求失敗率相較於前一個期間正常基準異常上升。</span><span class="sxs-lookup"><span data-stu-id="1e81c-194">We detected an abnormal rise in failed requests rate compared to the normal baseline of the preceding period.</span></span> <span data-ttu-id="1e81c-195">在分析失敗和關聯的遙測後，我們認為您應該注意發生的問題。</span><span class="sxs-lookup"><span data-stu-id="1e81c-195">After analysis of the failures and associated telemetry, we think that there is a problem that you should look into.</span></span>

<span data-ttu-id="1e81c-196">*收到通知代表一定是有問題嗎？*</span><span class="sxs-lookup"><span data-stu-id="1e81c-196">*Does the notification mean I definitely have a problem?*</span></span>

* <span data-ttu-id="1e81c-197">我們嘗試針對應用程式中斷或效能降低發出警示，但只有您可以完全了解語意和對應用程式或使用者的影響。</span><span class="sxs-lookup"><span data-stu-id="1e81c-197">We try to alert on app disruption or degradation, but only you can fully understand the semantics and the impact on the app or users.</span></span>

<span data-ttu-id="1e81c-198">*所以你們會看到我的資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="1e81c-198">*So, you guys look at my data?*</span></span>

* <span data-ttu-id="1e81c-199">不會。</span><span class="sxs-lookup"><span data-stu-id="1e81c-199">No.</span></span> <span data-ttu-id="1e81c-200">服務完全是自動的。</span><span class="sxs-lookup"><span data-stu-id="1e81c-200">The service is entirely automatic.</span></span> <span data-ttu-id="1e81c-201">只有您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="1e81c-201">Only you get the notifications.</span></span> <span data-ttu-id="1e81c-202">您的資料是 [不公開的](app-insights-data-retention-privacy.md)。</span><span class="sxs-lookup"><span data-stu-id="1e81c-202">Your data is [private](app-insights-data-retention-privacy.md).</span></span>

<span data-ttu-id="1e81c-203">*我是否必須訂閱此警示？*</span><span class="sxs-lookup"><span data-stu-id="1e81c-203">*Do I have to subscribe to this alert?*</span></span>

* <span data-ttu-id="1e81c-204">編號</span><span class="sxs-lookup"><span data-stu-id="1e81c-204">No.</span></span> <span data-ttu-id="1e81c-205">每個傳送要求遙測的應用程式都有「智慧型偵測」警示規則。</span><span class="sxs-lookup"><span data-stu-id="1e81c-205">Every application that sends request telemetry has the Smart Detection alert rule.</span></span>

<span data-ttu-id="1e81c-206">*我是否可以取消訂閱或改為傳送通知給我的同事？*</span><span class="sxs-lookup"><span data-stu-id="1e81c-206">*Can I unsubscribe or get the notifications sent to my colleagues instead?*</span></span>

* <span data-ttu-id="1e81c-207">是，請在 [警示] 規則中，按一下 [智慧型偵測] 規則來設定它。</span><span class="sxs-lookup"><span data-stu-id="1e81c-207">Yes, In Alert rules, click the Smart Detection rule to configure it.</span></span> <span data-ttu-id="1e81c-208">您可以停用警示，或變更警示的收件者。</span><span class="sxs-lookup"><span data-stu-id="1e81c-208">You can disable the alert, or change recipients for the alert.</span></span>

<span data-ttu-id="1e81c-209">*我遺失了電子郵件。在入口網站中哪裡可以找到通知？*</span><span class="sxs-lookup"><span data-stu-id="1e81c-209">*I lost the email. Where can I find the notifications in the portal?*</span></span>

* <span data-ttu-id="1e81c-210">在 Azure 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="1e81c-210">In the Activity logs.</span></span> <span data-ttu-id="1e81c-211">在 Azure 中，開啟您應用程式的 Application Insights 資源，然後選取 [活動] 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1e81c-211">In Azure, open the Application Insights resource for your app, then select Activity logs.</span></span>

<span data-ttu-id="1e81c-212">*部分警示與已知問題相關，我不想接收它們。*</span><span class="sxs-lookup"><span data-stu-id="1e81c-212">*Some of the alerts are about known issues and I do not want to receive them.*</span></span>

* <span data-ttu-id="1e81c-213">我們已在稽核記錄檔中抑制警示。</span><span class="sxs-lookup"><span data-stu-id="1e81c-213">We have alert suppression on our backlog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e81c-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e81c-214">Next steps</span></span>
<span data-ttu-id="1e81c-215">這些診斷工具可協助您檢查來自您的應用程式的遙測︰</span><span class="sxs-lookup"><span data-stu-id="1e81c-215">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="1e81c-216">計量瀏覽器</span><span class="sxs-lookup"><span data-stu-id="1e81c-216">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="1e81c-217">搜尋總管</span><span class="sxs-lookup"><span data-stu-id="1e81c-217">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="1e81c-218">分析 - 功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="1e81c-218">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="1e81c-219">智慧型偵測是完全自動的。</span><span class="sxs-lookup"><span data-stu-id="1e81c-219">Smart detections are completely automatic.</span></span> <span data-ttu-id="1e81c-220">但是，或許您會想要再設定一些警示？</span><span class="sxs-lookup"><span data-stu-id="1e81c-220">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="1e81c-221">手動設定的度量警示</span><span class="sxs-lookup"><span data-stu-id="1e81c-221">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="1e81c-222">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="1e81c-222">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
