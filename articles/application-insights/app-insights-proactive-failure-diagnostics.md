---
title: "aaaSmart 偵測-失敗的異常狀況，在 Application Insights |Microsoft 文件"
description: "失敗的要求 tooyour web 應用程式的 hello 速率 toounusual 變更會提醒您，並提供診斷的分析。 不需要設定。"
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
ms.openlocfilehash: dfd178ca9546294be91f27b0c1b846d519539b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---failure-anomalies"></a><span data-ttu-id="1803e-104">智慧型偵測 - 失敗異常</span><span class="sxs-lookup"><span data-stu-id="1803e-104">Smart Detection - Failure Anomalies</span></span>
<span data-ttu-id="1803e-105">[Application Insights](app-insights-overview.md)自動通知您幾近即時如果您的 web 應用程式遇到 hello 的失敗要求率異常升高。</span><span class="sxs-lookup"><span data-stu-id="1803e-105">[Application Insights](app-insights-overview.md) automatically notifies you in near real time if your web app experiences an abnormal rise in hello rate of failed requests.</span></span> <span data-ttu-id="1803e-106">它會偵測的 HTTP 要求或報告為失敗的相依性呼叫的 hello 率異常升高。</span><span class="sxs-lookup"><span data-stu-id="1803e-106">It detects an unusual rise in hello rate of HTTP requests or dependency calls that are reported as failed.</span></span> <span data-ttu-id="1803e-107">對於要求，失敗的要求通常是回應碼為 400 或更高的要求。</span><span class="sxs-lookup"><span data-stu-id="1803e-107">For requests, failed requests are usually those with response codes of 400 or higher.</span></span> <span data-ttu-id="1803e-108">toohelp 分級，並診斷 hello 問題，hello 通知中提供的 hello 特性 hello 失敗及相關的遙測分析。</span><span class="sxs-lookup"><span data-stu-id="1803e-108">toohelp you triage and diagnose hello problem, an analysis of hello characteristics of hello failures and related telemetry is provided in hello notification.</span></span> <span data-ttu-id="1803e-109">也有連結 toohello Application Insights 入口網站，以供進一步診斷。</span><span class="sxs-lookup"><span data-stu-id="1803e-109">There are also links toohello Application Insights portal for further diagnosis.</span></span> <span data-ttu-id="1803e-110">hello 功能需要任何設定或組態，因為它會使用機器學習演算法 toopredict hello 正常失敗率。</span><span class="sxs-lookup"><span data-stu-id="1803e-110">hello feature needs no set-up nor configuration, as it uses machine learning algorithms toopredict hello normal failure rate.</span></span>

<span data-ttu-id="1803e-111">這項功能適用於 Java 和 ASP.NET web 應用程式，裝載於雲端 hello 或您自己的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1803e-111">This feature works for Java and ASP.NET web apps, hosted in hello cloud or on your own servers.</span></span> <span data-ttu-id="1803e-112">它也適用於產生要求或相依性遙測的任何應用程式 - 例如，如果您有呼叫 [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) 或 [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency) 的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="1803e-112">It also works for any app that generates request or dependency telemetry - for example, if you have a worker role that calls [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) or [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

<span data-ttu-id="1803e-113">設定好後[Application Insights 專案](app-insights-overview.md)，並提供您的應用程式會產生某些最小量的遙測，智慧失敗異常偵測採用 24 小時您的應用程式，它前面的 toolearn hello 正常行為會開啟，而且可以傳送警示。</span><span class="sxs-lookup"><span data-stu-id="1803e-113">After setting up [Application Insights for your project](app-insights-overview.md), and provided your app generates a certain minimum amount of telemetry, Smart Detection of failure anomalies takes 24 hours toolearn hello normal behavior of your app, before it is switched on and can send alerts.</span></span>

<span data-ttu-id="1803e-114">以下是警示範例。</span><span class="sxs-lookup"><span data-stu-id="1803e-114">Here's a sample alert.</span></span>

![顯示失敗相關叢集分析的範例智慧型偵測警示](./media/app-insights-proactive-failure-diagnostics/013.png)

> [!NOTE]
> <span data-ttu-id="1803e-116">根據預設，您所取得的郵件格式會比這個範例還簡短。</span><span class="sxs-lookup"><span data-stu-id="1803e-116">By default, you get a shorter format mail than this example.</span></span> <span data-ttu-id="1803e-117">不過您也可以[交換器 toothis 詳細的格式](#configure-alerts)。</span><span class="sxs-lookup"><span data-stu-id="1803e-117">But you can [switch toothis detailed format](#configure-alerts).</span></span>
>
>

<span data-ttu-id="1803e-118">請注意，它會告訴您︰</span><span class="sxs-lookup"><span data-stu-id="1803e-118">Notice that it tells you:</span></span>

* <span data-ttu-id="1803e-119">hello 失敗率比較 toonormal 應用程式行為。</span><span class="sxs-lookup"><span data-stu-id="1803e-119">hello failure rate compared toonormal app behavior.</span></span>
* <span data-ttu-id="1803e-120">受影響的使用者人數 – 讓您知道多少 tooworry。</span><span class="sxs-lookup"><span data-stu-id="1803e-120">How many users are affected – so you know how much tooworry.</span></span>
* <span data-ttu-id="1803e-121">Hello 失敗相關聯的特性模式。</span><span class="sxs-lookup"><span data-stu-id="1803e-121">A characteristic pattern associated with hello failures.</span></span> <span data-ttu-id="1803e-122">在此範例中，有特定的回應碼、要求名稱 (操作) 和應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="1803e-122">In this example, there’s a particular response code, request name (operation) and app version.</span></span> <span data-ttu-id="1803e-123">立即會告訴您其中 toostart 尋找程式碼中。</span><span class="sxs-lookup"><span data-stu-id="1803e-123">That immediately tells you where toostart looking in your code.</span></span> <span data-ttu-id="1803e-124">其他可能性則可能是特定的瀏覽器或用戶端作業系統。</span><span class="sxs-lookup"><span data-stu-id="1803e-124">Other possibilities could be a specific browser or client operating system.</span></span>
* <span data-ttu-id="1803e-125">hello 例外狀況、 記錄追蹤和顯示 toobe hello 與相關聯的相依性失敗 （資料庫或其他外部元件） 來區別失敗。</span><span class="sxs-lookup"><span data-stu-id="1803e-125">hello exception, log traces, and dependency failure (databases or other external components) that appear toobe associated with hello characterized failures.</span></span>
* <span data-ttu-id="1803e-126">直接連結在 Application Insights 中的 hello 遙測 toorelevant 搜尋。</span><span class="sxs-lookup"><span data-stu-id="1803e-126">Links directly toorelevant searches on hello telemetry in Application Insights.</span></span>

## <a name="benefits-of-smart-detection"></a><span data-ttu-id="1803e-127">智慧型偵測的優點</span><span class="sxs-lookup"><span data-stu-id="1803e-127">Benefits of Smart Detection</span></span>
<span data-ttu-id="1803e-128">一般的 [度量警示](app-insights-alerts.md) 會告訴您可能有問題。</span><span class="sxs-lookup"><span data-stu-id="1803e-128">Ordinary [metric alerts](app-insights-alerts.md) tell you there might be a problem.</span></span> <span data-ttu-id="1803e-129">但是智慧偵測開始為您執行許多原本必須另外 toodo 自行 hello 分析 hello 診斷工作。</span><span class="sxs-lookup"><span data-stu-id="1803e-129">But Smart Detection starts hello diagnostic work for you, performing a lot of hello analysis you would otherwise have toodo yourself.</span></span> <span data-ttu-id="1803e-130">您快速 hello 結果整齊地在封裝中，可幫助您 tooget toohello 根目錄 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="1803e-130">You get hello results neatly packaged, helping you tooget quickly toohello root of hello problem.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1803e-131">運作方式</span><span class="sxs-lookup"><span data-stu-id="1803e-131">How it works</span></span>
<span data-ttu-id="1803e-132">智慧型偵測監視 hello 遙測接收從您的應用程式，並在特定的 hello 失敗率。</span><span class="sxs-lookup"><span data-stu-id="1803e-132">Smart  Detection monitors hello telemetry received from your app, and in particular hello failure rates.</span></span> <span data-ttu-id="1803e-133">此規則會計算哪些 hello 要求的 hello 數目`Successful request`屬性為 false，而且會呼叫哪個 hello hello 相依性數目`Successful call`屬性為 false。</span><span class="sxs-lookup"><span data-stu-id="1803e-133">This rule counts hello number of requests for which hello `Successful request` property is false, and hello number of dependency calls for which hello `Successful call` property is false.</span></span> <span data-ttu-id="1803e-134">根據預設的要求， `Successful request == (resultCode < 400)` (除非您已經撰寫自訂程式碼太[篩選](app-insights-api-filtering-sampling.md#filtering)產生您自己或[TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest)呼叫)。</span><span class="sxs-lookup"><span data-stu-id="1803e-134">For requests, by default, `Successful request == (resultCode < 400)` (unless you have written custom code too[filter](app-insights-api-filtering-sampling.md#filtering) or generate your own [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) calls).</span></span> 

<span data-ttu-id="1803e-135">您的應用程式效能具有一般的行為模式。</span><span class="sxs-lookup"><span data-stu-id="1803e-135">Your app’s performance has a typical pattern of behavior.</span></span> <span data-ttu-id="1803e-136">部分要求或相依性呼叫將會更容易出錯 toofailure 比其他;和 hello 整體的失敗率可能向上負載增加時。</span><span class="sxs-lookup"><span data-stu-id="1803e-136">Some requests or dependency calls will be more prone toofailure than others; and hello overall failure rate may go up as load increases.</span></span> <span data-ttu-id="1803e-137">智慧型偵測會使用機器學習 toofind 這些異常狀況。</span><span class="sxs-lookup"><span data-stu-id="1803e-137">Smart Detection uses machine learning toofind these anomalies.</span></span>

<span data-ttu-id="1803e-138">遙測進入 Application Insights 從您的 web 應用程式，智慧偵測會比較 hello 目前的行為與 hello 模式透過 hello 看到過去幾天。</span><span class="sxs-lookup"><span data-stu-id="1803e-138">As telemetry comes into Application Insights from your web app, Smart Detection compares hello current behavior with hello patterns seen over hello past few days.</span></span> <span data-ttu-id="1803e-139">如果觀察到與先前效能相比，失敗率異常提高，就會觸發分析。</span><span class="sxs-lookup"><span data-stu-id="1803e-139">If an abnormal rise in failure rate is observed by comparison with previous performance, an analysis is triggered.</span></span>

<span data-ttu-id="1803e-140">分析觸發時，hello 服務叢集對執行分析 hello 失敗的要求，tootry tooidentify 歸納 hello 失敗的值的模式。</span><span class="sxs-lookup"><span data-stu-id="1803e-140">When an analysis is triggered, hello service performs a cluster analysis on hello failed request, tootry tooidentify a pattern of values that characterize hello failures.</span></span> <span data-ttu-id="1803e-141">Hello 上述範例中，在 hello 分析已探索最多失敗所需特定結果碼，要求名稱、 伺服器 URL 主機和角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="1803e-141">In hello example above, hello analysis has discovered that most failures are about a specific result code, request name, Server URL host, and role instance.</span></span> <span data-ttu-id="1803e-142">相反地，hello 分析已發現，hello 用戶端作業系統屬性會分散至多個值，因此未列。</span><span class="sxs-lookup"><span data-stu-id="1803e-142">By contrast, hello analysis has discovered that hello client operating system property is distributed over multiple values, and so it is not listed.</span></span>

<span data-ttu-id="1803e-143">當您的服務會使用這些遙測呼叫檢測時，hello 分析會尋找例外狀況，而且其已識別，以及任何與相關聯的追蹤記錄檔的範例 hello 叢集中的要求相關聯的相依性失敗要求。</span><span class="sxs-lookup"><span data-stu-id="1803e-143">When your service is instrumented with these telemetry calls, hello analyser looks for an exception and a dependency failure that are associated with requests in hello cluster it has identified, together with an example of any trace logs associated with those requests.</span></span>

<span data-ttu-id="1803e-144">hello 產生分析會與警示，傳送 tooyou，除非您已無法供設定。</span><span class="sxs-lookup"><span data-stu-id="1803e-144">hello resulting analysis is sent tooyou as alert, unless you have configured it not to.</span></span>

<span data-ttu-id="1803e-145">像 hello[您手動設定的警示](app-insights-alerts.md)，您可以檢查 hello hello 警示狀態和設定在 hello 警示刀鋒視窗中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1803e-145">Like hello [alerts you set manually](app-insights-alerts.md), you can inspect hello state of hello alert and configure it in hello Alerts blade of your Application Insights resource.</span></span> <span data-ttu-id="1803e-146">但不同於其他警示，您不需要 tooset 註冊，或設定智慧型偵測。</span><span class="sxs-lookup"><span data-stu-id="1803e-146">But unlike other alerts, you don't need tooset up or configure Smart Detection.</span></span> <span data-ttu-id="1803e-147">若有需要，您可以將它停用或變更其目標電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1803e-147">If you want, you can disable it or change its target email addresses.</span></span>

## <a name="configure-alerts"></a><span data-ttu-id="1803e-148">設定警示</span><span class="sxs-lookup"><span data-stu-id="1803e-148">Configure alerts</span></span>
<span data-ttu-id="1803e-149">您可以停用智慧偵測、 變更 hello 電子郵件收件者、 建立 webhook，或選擇加入詳細的 toomore 警示訊息。</span><span class="sxs-lookup"><span data-stu-id="1803e-149">You can disable Smart Detection, change hello email recipients, create a webhook, or opt in toomore detailed alert messages.</span></span>

<span data-ttu-id="1803e-150">開啟 hello 警示 頁面。</span><span class="sxs-lookup"><span data-stu-id="1803e-150">Open hello Alerts page.</span></span> <span data-ttu-id="1803e-151">失敗的異常狀況隨附以及任何您已手動設定，且您可以查看其是否目前在 hello 警示狀態的警示。</span><span class="sxs-lookup"><span data-stu-id="1803e-151">Failure Anomalies is included along with any alerts that you have set manually, and you can see whether it is currently in hello alert state.</span></span>

![在 hello 概觀頁面上，按一下警示磚。](./media/app-insights-proactive-failure-diagnostics/021.png)

<span data-ttu-id="1803e-154">按一下 hello 警示 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="1803e-154">Click hello alert tooconfigure it.</span></span>

![組態](./media/app-insights-proactive-failure-diagnostics/032.png)

<span data-ttu-id="1803e-156">請注意，您可以停用「智慧型偵測」，但無法將它刪除 (或建立另一個「智慧型偵測」)。</span><span class="sxs-lookup"><span data-stu-id="1803e-156">Notice that you can disable Smart Detection, but you can't delete it (or create another one).</span></span>

#### <a name="detailed-alerts"></a><span data-ttu-id="1803e-157">詳細的警示</span><span class="sxs-lookup"><span data-stu-id="1803e-157">Detailed alerts</span></span>
<span data-ttu-id="1803e-158">如果您選取 「 取得更詳細的診斷 」 hello 電子郵件會包含更多診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="1803e-158">If you select "Get more detailed diagnostics" then hello email will contain more diagnostic information.</span></span> <span data-ttu-id="1803e-159">有時候您可能會無法 toodiagnose hello 問題只從 hello 電子郵件中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1803e-159">Sometimes you'll be able toodiagnose hello problem just from hello data in hello email.</span></span>

<span data-ttu-id="1803e-160">沒有 hello 更詳細的警示有稍微風險可能包含機密資訊，因為它包含例外狀況和追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="1803e-160">There's a slight risk that hello more detailed alert could contain sensitive information, because it includes exception and trace messages.</span></span> <span data-ttu-id="1803e-161">不過，只有當您的程式碼允許機密資訊進入這些訊息時，才會發生。</span><span class="sxs-lookup"><span data-stu-id="1803e-161">However, this would only happen if your code could allow sensitive information into those messages.</span></span>

## <a name="triaging-and-diagnosing-an-alert"></a><span data-ttu-id="1803e-162">分級和診斷警示</span><span class="sxs-lookup"><span data-stu-id="1803e-162">Triaging and diagnosing an alert</span></span>
<span data-ttu-id="1803e-163">警示表示偵測 hello 失敗的要求率異常升高。</span><span class="sxs-lookup"><span data-stu-id="1803e-163">An alert indicates that an abnormal rise in hello failed request rate was detected.</span></span> <span data-ttu-id="1803e-164">原因可能是您的應用程式或其環境有問題。</span><span class="sxs-lookup"><span data-stu-id="1803e-164">It's likely that there is some problem with your app or its environment.</span></span>

<span data-ttu-id="1803e-165">您可以從 hello 要求以及受影響的使用者數目的百分比，決定如何緊急 hello 問題是。</span><span class="sxs-lookup"><span data-stu-id="1803e-165">From hello percentage of requests and number of users affected, you can decide how urgent hello issue is.</span></span> <span data-ttu-id="1803e-166">Hello 上述範例中，在 hello 失敗率 22.5%的比較與正常率 1%，表示不正確的項目正在進行的作業。</span><span class="sxs-lookup"><span data-stu-id="1803e-166">In hello example above, hello failure rate of 22.5% compares with a normal rate of 1%, indicates that something bad is going on.</span></span> <span data-ttu-id="1803e-167">在 hello 另一方面，11 只有使用者受到影響。</span><span class="sxs-lookup"><span data-stu-id="1803e-167">On hello other hand, only 11 users were affected.</span></span> <span data-ttu-id="1803e-168">如果它是您的應用程式時，您會無法 tooassess 嚴重程度的。</span><span class="sxs-lookup"><span data-stu-id="1803e-168">If it were your app, you'd be able tooassess how serious that is.</span></span>

<span data-ttu-id="1803e-169">在許多情況下，您會快速地從 hello 要求名稱、 例外狀況，提供相依性失敗和追蹤資料可以 toodiagnose hello 問題。</span><span class="sxs-lookup"><span data-stu-id="1803e-169">In many cases, you will be able toodiagnose hello problem quickly from hello request name, exception, dependency failure and trace data provided.</span></span>

<span data-ttu-id="1803e-170">另有一些線索。</span><span class="sxs-lookup"><span data-stu-id="1803e-170">There are some other clues.</span></span> <span data-ttu-id="1803e-171">例如，在此範例中的 hello 相依性失敗率為 hello 與 hello 例外狀況率 （89.3%) 相同。</span><span class="sxs-lookup"><span data-stu-id="1803e-171">For example, hello dependency failure rate in this example is hello same as hello exception rate (89.3%).</span></span> <span data-ttu-id="1803e-172">這暗示，hello 例外狀況，就會發生直接從 hello 相依性失敗-讓您清楚瞭解 where toostart 尋找程式碼中。</span><span class="sxs-lookup"><span data-stu-id="1803e-172">This suggests that hello exception arises directly from hello dependency failure - giving you a clear idea of where toostart looking in your code.</span></span>

<span data-ttu-id="1803e-173">tooinvestigate 此外，每個區段中的 hello 連結會帶您直線 tooa[搜尋頁面](app-insights-diagnostic-search.md)篩選 toohello 相關要求、 例外狀況、 相依性或追蹤。</span><span class="sxs-lookup"><span data-stu-id="1803e-173">tooinvestigate further, hello links in each section will take you straight tooa [search page](app-insights-diagnostic-search.md) filtered toohello relevant requests, exception, dependency or traces.</span></span> <span data-ttu-id="1803e-174">您也可以開啟 hello [Azure 入口網站](https://portal.azure.com)，瀏覽您的應用程式的 toohello Application Insights 資源，並開啟 hello 失敗刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1803e-174">Or you can open hello [Azure portal](https://portal.azure.com), navigate toohello Application Insights resource for your app, and open hello Failures blade.</span></span>

<span data-ttu-id="1803e-175">在此範例中，按一下 hello 檢視相依性失敗詳細資料 連結可開啟 hello Application Insights 搜尋刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1803e-175">In this example, clicking hello 'View dependency failures details' link opens hello Application Insights search blade.</span></span> <span data-ttu-id="1803e-176">它會顯示 hello SQL 陳述式具有 hello 根本原因的範例： Null 必要欄位在所提供，並且未通過 hello 儲存作業期間執行的驗證。</span><span class="sxs-lookup"><span data-stu-id="1803e-176">It shows hello SQL statement that has an example of hello root cause: NULLs were provided at mandatory fields and did not pass validation during hello save operation.</span></span>

![診斷搜尋](./media/app-insights-proactive-failure-diagnostics/051.png)

## <a name="review-recent-alerts"></a><span data-ttu-id="1803e-178">檢閱最近的警示</span><span class="sxs-lookup"><span data-stu-id="1803e-178">Review recent alerts</span></span>

<span data-ttu-id="1803e-179">按一下**智慧偵測**tooget toohello 最新警示：</span><span class="sxs-lookup"><span data-stu-id="1803e-179">Click **Smart Detection** tooget toohello most recent alert:</span></span>

![警示摘要](./media/app-insights-proactive-failure-diagnostics/070.png)


## <a name="whats-hello-difference-"></a><span data-ttu-id="1803e-181">Hello 差異為何...</span><span class="sxs-lookup"><span data-stu-id="1803e-181">What's hello difference ...</span></span>
<span data-ttu-id="1803e-182">失敗異常的「智慧型偵測」可以與其他相似但不同的 Application Insights 功能互補。</span><span class="sxs-lookup"><span data-stu-id="1803e-182">Smart Detection of failure anomalies complements other similar but distinct features of Application Insights.</span></span>

* <span data-ttu-id="1803e-183">您可以設定[度量警示](app-insights-alerts.md)，且可以檢視各種度量，例如 CPU 使用量、要求率、頁面載入時間等等。</span><span class="sxs-lookup"><span data-stu-id="1803e-183">[Metric Alerts](app-insights-alerts.md) are set by you and can monitor a wide range of metrics such as CPU occupancy, request rates,  page load times, and so on.</span></span> <span data-ttu-id="1803e-184">您可以使用這些 toowarn 您，比方說，如果您需要 tooadd 更多資源。</span><span class="sxs-lookup"><span data-stu-id="1803e-184">You can use them toowarn you, for example, if you need tooadd more resources.</span></span> <span data-ttu-id="1803e-185">相反地，智慧失敗異常偵測涵蓋您在接近即時的方式之後會大幅增加 web 應用程式的失敗的要求率比較 tooweb 應用程式的小範圍的關鍵度量 （目前只失敗的要求率），設計 toonotify正常的行為。</span><span class="sxs-lookup"><span data-stu-id="1803e-185">By contrast, Smart Detection of failure anomalies covers a small range of critical metrics (currently only failed request rate), designed toonotify you in near real time manner once your web app's failed request rate increases significantly compared tooweb app's normal behavior.</span></span>

    <span data-ttu-id="1803e-186">智慧型偵測會自動調整其回應 tooprevailing 條件中的臨界值。</span><span class="sxs-lookup"><span data-stu-id="1803e-186">Smart Detection automatically adjusts its threshold in response tooprevailing conditions.</span></span>

    <span data-ttu-id="1803e-187">智慧的偵測啟動 hello 為您的診斷工作。</span><span class="sxs-lookup"><span data-stu-id="1803e-187">Smart Detection starts hello diagnostic work for you.</span></span>
* <span data-ttu-id="1803e-188">[智慧型效能異常偵測](app-insights-proactive-performance-diagnostics.md)也會使用電腦智慧 toodiscover 異常模式在您的指標，並由您就不需要設定。</span><span class="sxs-lookup"><span data-stu-id="1803e-188">[Smart Detection of performance anomalies](app-insights-proactive-performance-diagnostics.md) also uses machine intelligence toodiscover unusual patterns in your metrics, and no configuration by you is required.</span></span> <span data-ttu-id="1803e-189">但不同於智慧失敗異常偵測，hello 智慧效能異常偵測的目的是 toofind 區段可能格式不提供您使用複寫-例如，透過瀏覽器對特定類型的特定頁面。</span><span class="sxs-lookup"><span data-stu-id="1803e-189">But unlike Smart Detection of failure anomalies, hello purpose of Smart  Detection of performance anomalies is toofind segments of your usage manifold that might be badly served - for example, by specific pages on a specific type of browser.</span></span> <span data-ttu-id="1803e-190">hello 分析執行每日，而且如果找到任何結果，可能 toobe 較緊急比警示。</span><span class="sxs-lookup"><span data-stu-id="1803e-190">hello analysis is performed daily, and if any result is found, it's likely toobe much less urgent than an alert.</span></span> <span data-ttu-id="1803e-191">相反地，失敗有異常的 hello 分析會持續執行傳入的遙測，且將會通知您分鐘內是否大於預期伺服器失敗率。</span><span class="sxs-lookup"><span data-stu-id="1803e-191">By contrast, hello analysis for failure anomalies is performed continuously on incoming telemetry, and you will be notified within minutes if server failure rates are greater than expected.</span></span>

## <a name="if-you-receive-a-smart-detection-alert"></a><span data-ttu-id="1803e-192">如果您收到「智慧型偵測」警示</span><span class="sxs-lookup"><span data-stu-id="1803e-192">If you receive a Smart Detection alert</span></span>
<span data-ttu-id="1803e-193">*為什麼會收到這個警示？*</span><span class="sxs-lookup"><span data-stu-id="1803e-193">*Why have I received this alert?*</span></span>

* <span data-ttu-id="1803e-194">我們偵測到異常升高的 hello 之前期間的失敗的要求速率與相比較 toohello 正常基準。</span><span class="sxs-lookup"><span data-stu-id="1803e-194">We detected an abnormal rise in failed requests rate compared toohello normal baseline of hello preceding period.</span></span> <span data-ttu-id="1803e-195">在分析後 hello 失敗和相關聯的遙測，我們認為您應該尋找問題。</span><span class="sxs-lookup"><span data-stu-id="1803e-195">After analysis of hello failures and associated telemetry, we think that there is a problem that you should look into.</span></span>

<span data-ttu-id="1803e-196">*Hello 通知意思明確有問題？*</span><span class="sxs-lookup"><span data-stu-id="1803e-196">*Does hello notification mean I definitely have a problem?*</span></span>

* <span data-ttu-id="1803e-197">我們嘗試 tooalert 上應用程式中斷或降級，但只有您可以完全了解 hello 語意以及 hello 影響 hello 應用程式或使用者。</span><span class="sxs-lookup"><span data-stu-id="1803e-197">We try tooalert on app disruption or degradation, but only you can fully understand hello semantics and hello impact on hello app or users.</span></span>

<span data-ttu-id="1803e-198">*所以你們會看到我的資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="1803e-198">*So, you guys look at my data?*</span></span>

* <span data-ttu-id="1803e-199">否。</span><span class="sxs-lookup"><span data-stu-id="1803e-199">No.</span></span> <span data-ttu-id="1803e-200">hello 服務是完全自動。</span><span class="sxs-lookup"><span data-stu-id="1803e-200">hello service is entirely automatic.</span></span> <span data-ttu-id="1803e-201">只有您會收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="1803e-201">Only you get hello notifications.</span></span> <span data-ttu-id="1803e-202">您的資料是 [不公開的](app-insights-data-retention-privacy.md)。</span><span class="sxs-lookup"><span data-stu-id="1803e-202">Your data is [private](app-insights-data-retention-privacy.md).</span></span>

<span data-ttu-id="1803e-203">*是否有 toosubscribe toothis 警示？*</span><span class="sxs-lookup"><span data-stu-id="1803e-203">*Do I have toosubscribe toothis alert?*</span></span>

* <span data-ttu-id="1803e-204">否。</span><span class="sxs-lookup"><span data-stu-id="1803e-204">No.</span></span> <span data-ttu-id="1803e-205">傳送要求遙測每個應用程式有 hello 智慧偵測的警示規則。</span><span class="sxs-lookup"><span data-stu-id="1803e-205">Every application that sends request telemetry has hello Smart Detection alert rule.</span></span>

<span data-ttu-id="1803e-206">*我是否可以取消訂閱或取得改成 toomy 同事傳送 hello 通知？*</span><span class="sxs-lookup"><span data-stu-id="1803e-206">*Can I unsubscribe or get hello notifications sent toomy colleagues instead?*</span></span>

* <span data-ttu-id="1803e-207">在警示的規則是，按一下 hello 智慧偵測規則 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="1803e-207">Yes, In Alert rules, click hello Smart Detection rule tooconfigure it.</span></span> <span data-ttu-id="1803e-208">您可以停用 hello 警示，或變更 hello 警示的收件者。</span><span class="sxs-lookup"><span data-stu-id="1803e-208">You can disable hello alert, or change recipients for hello alert.</span></span>

<span data-ttu-id="1803e-209">*我遺失 hello 電子郵件。其中 hello 入口網站中找到 hello 通知？*</span><span class="sxs-lookup"><span data-stu-id="1803e-209">*I lost hello email. Where can I find hello notifications in hello portal?*</span></span>

* <span data-ttu-id="1803e-210">在 hello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1803e-210">In hello Activity logs.</span></span> <span data-ttu-id="1803e-211">在 Azure 中，開啟您的應用程式的 hello Application Insights 資源，然後選取 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1803e-211">In Azure, open hello Application Insights resource for your app, then select Activity logs.</span></span>

<span data-ttu-id="1803e-212">*一些 hello 警示大約已知問題，而且我不想 tooreceive 它們。*</span><span class="sxs-lookup"><span data-stu-id="1803e-212">*Some of hello alerts are about known issues and I do not want tooreceive them.*</span></span>

* <span data-ttu-id="1803e-213">我們已在稽核記錄檔中抑制警示。</span><span class="sxs-lookup"><span data-stu-id="1803e-213">We have alert suppression on our backlog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1803e-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1803e-214">Next steps</span></span>
<span data-ttu-id="1803e-215">這些診斷工具可協助您檢查您的應用程式的遙測 hello:</span><span class="sxs-lookup"><span data-stu-id="1803e-215">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="1803e-216">計量瀏覽器</span><span class="sxs-lookup"><span data-stu-id="1803e-216">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="1803e-217">搜尋總管</span><span class="sxs-lookup"><span data-stu-id="1803e-217">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="1803e-218">分析 - 功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="1803e-218">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="1803e-219">智慧型偵測是完全自動的。</span><span class="sxs-lookup"><span data-stu-id="1803e-219">Smart detections are completely automatic.</span></span> <span data-ttu-id="1803e-220">但您可能要 tooset 某些更多的警示嗎？</span><span class="sxs-lookup"><span data-stu-id="1803e-220">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="1803e-221">手動設定的度量警示</span><span class="sxs-lookup"><span data-stu-id="1803e-221">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="1803e-222">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="1803e-222">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
