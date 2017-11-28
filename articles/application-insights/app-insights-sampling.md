---
title: "在 Azure Application Insights aaaTelemetry 取樣 |Microsoft 文件"
description: "如何 tookeep hello 控制下的遙測資料的磁碟的區。"
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="b33ef-103">Application Insights 中的取樣</span><span class="sxs-lookup"><span data-stu-id="b33ef-103">Sampling in Application Insights</span></span>


<span data-ttu-id="b33ef-104">取樣是 [Azure Application Insights](app-insights-overview.md) 中的一個功能。</span><span class="sxs-lookup"><span data-stu-id="b33ef-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b33ef-105">它是 hello 的建議方式 tooreduce 遙測流量和儲存體，同時保留應用程式資料的正確統計分析。</span><span class="sxs-lookup"><span data-stu-id="b33ef-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="b33ef-106">hello 篩選選取項目相關，如此您可以瀏覽項目，當您在進行診斷調查之間。</span><span class="sxs-lookup"><span data-stu-id="b33ef-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="b33ef-107">當度量的計數呈現 tooyou hello 入口網站中時，它們會重新正規化 tootake hello 取樣，toominimize 任何生效的 hello 統計帳戶。</span><span class="sxs-lookup"><span data-stu-id="b33ef-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="b33ef-108">取樣可減少流量與資料成本，而且可以協助您避免節流。</span><span class="sxs-lookup"><span data-stu-id="b33ef-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="b33ef-109">簡單地說︰</span><span class="sxs-lookup"><span data-stu-id="b33ef-109">In brief:</span></span>
* <span data-ttu-id="b33ef-110">取樣會保留 1  *n* 記錄，並捨棄 hello rest。</span><span class="sxs-lookup"><span data-stu-id="b33ef-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="b33ef-111">比方說，它可能會保留 5 個事件的其中 1 個，取樣率為 20%。</span><span class="sxs-lookup"><span data-stu-id="b33ef-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="b33ef-112">如果您的應用程式傳送大量遙測，ASP.NET Web 伺服器應用程式便會自動進行取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="b33ef-113">您也可以設定取樣以手動方式，是在 hello 入口網站上 hello 定價頁面。或在 hello hello.config 檔案中的 ASP.NET SDK，tooalso 減少 hello 網路流量。</span><span class="sxs-lookup"><span data-stu-id="b33ef-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="b33ef-114">如果您自訂的事件記錄，而且您想要確定，一組事件是保留或一起捨棄 toomake，確定它們有 hello OperationId 值相同。</span><span class="sxs-lookup"><span data-stu-id="b33ef-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="b33ef-115">hello 取樣除數 *n*  hello 屬性中的每一筆記錄來報告`itemCount`，hello 易記名稱的 「 要求計數 」 或 「 事件計數 」 下出現的搜尋中。</span><span class="sxs-lookup"><span data-stu-id="b33ef-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="b33ef-116">當取樣不在作業中，則 `itemCount==1`。</span><span class="sxs-lookup"><span data-stu-id="b33ef-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="b33ef-117">如果您要撰寫分析查詢，請 [考慮到取樣](app-insights-analytics-tour.md#counting-sampled-data)。</span><span class="sxs-lookup"><span data-stu-id="b33ef-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="b33ef-118">特別是，您應該使用 `summarize sum(itemCount)`，而非只計算記錄。</span><span class="sxs-lookup"><span data-stu-id="b33ef-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="b33ef-119">取樣類型</span><span class="sxs-lookup"><span data-stu-id="b33ef-119">Types of sampling</span></span>
<span data-ttu-id="b33ef-120">有三個替代的取樣方法：</span><span class="sxs-lookup"><span data-stu-id="b33ef-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="b33ef-121">**自動調整取樣**自動調整的遙測資料從您的 ASP.NET 應用程式中的 hello SDK 傳送 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b33ef-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="b33ef-122">預設從 SDK v 2.0.0-beta3 傳送。</span><span class="sxs-lookup"><span data-stu-id="b33ef-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="b33ef-123">目前僅供 ASP.NET 伺服器端遙測使用。</span><span class="sxs-lookup"><span data-stu-id="b33ef-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="b33ef-124">**固定速率取樣**減少 hello 的遙測資料傳送，從這兩個 ASP.NET 伺服器從使用者的瀏覽器的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b33ef-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="b33ef-125">您設定 hello 速率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-125">You set hello rate.</span></span> <span data-ttu-id="b33ef-126">hello 用戶端和伺服器將會同步處理其取樣因此，在搜尋中，您可以瀏覽相關的頁面檢視及要求。</span><span class="sxs-lookup"><span data-stu-id="b33ef-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="b33ef-127">**擷取取樣**hello Azure 入口網站中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="b33ef-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="b33ef-128">它會捨棄一些 hello 遙測來自您的應用程式，您所設定的速率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="b33ef-129">這不會減少遙測流量，但可協助您讓流量不要超過每月配額。</span><span class="sxs-lookup"><span data-stu-id="b33ef-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="b33ef-130">您可以將其設定而不必重新部署您的應用程式，而一致的方式適用於所有伺服器和用戶端 hello 能夠取樣最大好處。</span><span class="sxs-lookup"><span data-stu-id="b33ef-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="b33ef-131">如果自適性或固定速率取樣正在作業中，則會停用擷取取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="b33ef-132">擷取取樣</span><span class="sxs-lookup"><span data-stu-id="b33ef-132">Ingestion sampling</span></span>
<span data-ttu-id="b33ef-133">這種形式的取樣點 hello 從您網頁伺服器、 瀏覽器和裝置 hello 遙測當達到 hello Application Insights 服務端點的運作方式。</span><span class="sxs-lookup"><span data-stu-id="b33ef-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="b33ef-134">雖然它不會減少從您的應用程式傳送 hello 遙測流量，減少 hello 量處理，並保留 （和支付） 由 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="b33ef-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="b33ef-135">如果您的應用程式通常會超過每月配額，而且不需要 hello 選項使用的取樣 hello SDK 為基礎類型，請使用這種類型的取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="b33ef-136">設定 hello 取樣率，以 hello 配額和定價刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="b33ef-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![從 hello 應用程式概觀刀鋒視窗中，按一下設定、 配額、 範例，然後選取取樣率，並按一下 [更新]。](./media/app-insights-sampling/04.png)

<span data-ttu-id="b33ef-138">如同其他類型的取樣，hello 演算法會保留相關的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="b33ef-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="b33ef-139">例如，當您檢查在搜尋中的 hello 遙測，您可以 toofind hello 要求相關的 tooa 特定例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b33ef-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="b33ef-140">度量計量 (例如要求率及例外狀況率) 會正確地保留。</span><span class="sxs-lookup"><span data-stu-id="b33ef-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="b33ef-141">遭到取樣捨棄的資料點將無法在任何 Application Insights 功能中使用，例如 [連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="b33ef-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="b33ef-142">進行 SDK 自適性或固定速率取樣時，不執行擷取取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="b33ef-143">如果在 hello SDK hello 取樣率小於 100%，則 hello 擷取您所設定的取樣率會忽略。</span><span class="sxs-lookup"><span data-stu-id="b33ef-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="b33ef-144">hello hello 磚上顯示的值表示您將擷取取樣的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="b33ef-145">如果 SDK 取樣是作業中，它不代表 hello 實際取樣率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="b33ef-146">在您 Web 伺服器上的調適性取樣</span><span class="sxs-lookup"><span data-stu-id="b33ef-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="b33ef-147">自動調整取樣供 hello Application Insights SDK ASP.NET v 2.0.0-beta3 和更新版本，而且預設會啟用。</span><span class="sxs-lookup"><span data-stu-id="b33ef-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="b33ef-148">自動調整取樣會影響遙測資料從您網頁伺服器應用程式 toohello Application Insights 服務傳送嗨磁碟的區。</span><span class="sxs-lookup"><span data-stu-id="b33ef-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="b33ef-149">hello 磁碟區會自動調整 tookeep 內指定的最大速率的流量。</span><span class="sxs-lookup"><span data-stu-id="b33ef-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="b33ef-150">它無法在低遙測量的情況下運作，因此偵錯中的應用程式或使用率低的網站不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="b33ef-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="b33ef-151">tooachieve hello 目標磁碟區，某些產生的 hello 遙測會被捨棄。</span><span class="sxs-lookup"><span data-stu-id="b33ef-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="b33ef-152">但其他類型的取樣，類似 hello 演算法會保留相關的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="b33ef-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="b33ef-153">例如，當您檢查在搜尋中的 hello 遙測，您可以 toofind hello 要求相關的 tooa 特定例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b33ef-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="b33ef-154">度量會計算例如要求率和例外狀況率，調整的 toocompensate hello 取樣率，使它們在度量總管 中顯示大約正確的值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="b33ef-155">**更新您的專案 NuGet**最新封裝 toohello*發行前版本*新版 Application Insights： 以滑鼠右鍵按一下方案總管] 中的 hello 專案中，選擇 [管理 NuGet 封裝，請檢查**Include發行前版本**並 Microsoft.ApplicationInsights.Web 搜尋。</span><span class="sxs-lookup"><span data-stu-id="b33ef-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="b33ef-156">在[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)，您可以調整幾個參數，在 hello`AdaptiveSamplingTelemetryProcessor`節點。</span><span class="sxs-lookup"><span data-stu-id="b33ef-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="b33ef-157">hello 圖表所示為 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="b33ef-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="b33ef-158">hello hello 調整演算法的目標速率目標在於**每個伺服器主機上**。</span><span class="sxs-lookup"><span data-stu-id="b33ef-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="b33ef-159">若您的 web 應用程式執行許多主機上，所以當 tooremain 內您目標的速率在 hello Application Insights 入口網站的流量減少這個值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="b33ef-160">hello 間隔在哪一個 hello 的遙測資料的目前速率會重新評估。</span><span class="sxs-lookup"><span data-stu-id="b33ef-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="b33ef-161">評估是以移動平均來執行。</span><span class="sxs-lookup"><span data-stu-id="b33ef-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="b33ef-162">如果您的遙測對於 toosudden 暴增您可能想指定 tooshorten 此時間間隔。</span><span class="sxs-lookup"><span data-stu-id="b33ef-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="b33ef-163">取樣百分比值變更時，多久之後我們允許一次取樣百分比 toolower toocapture 較少的資料。</span><span class="sxs-lookup"><span data-stu-id="b33ef-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="b33ef-164">取樣百分比值變更時，多久之後我們允許一次取樣百分比 tooincrease toocapture 更多資料。</span><span class="sxs-lookup"><span data-stu-id="b33ef-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="b33ef-165">隨著取樣百分比改變，什麼是 hello 最小值我們要允許 tooset。</span><span class="sxs-lookup"><span data-stu-id="b33ef-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="b33ef-166">隨著取樣百分比改變，什麼是 hello 最大值我們要允許 tooset。</span><span class="sxs-lookup"><span data-stu-id="b33ef-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="b33ef-167">在 hello 計算中的 hello 移動平均，hello 權數指派 toohello 最新的值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="b33ef-168">使用小於 1 的值等於 tooor。</span><span class="sxs-lookup"><span data-stu-id="b33ef-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="b33ef-169">較小的值變更 hello 演算法較不反應式 toosudden。</span><span class="sxs-lookup"><span data-stu-id="b33ef-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="b33ef-170">hello hello 應用程式剛開始時指派的值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="b33ef-171">不要在偵錯時減少此值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="b33ef-172">以分號分隔不想讓 toobe 取樣的型別的清單。</span><span class="sxs-lookup"><span data-stu-id="b33ef-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="b33ef-173">可辨識的類型為：相依性、事件、例外狀況、頁面檢視、要求、追蹤。</span><span class="sxs-lookup"><span data-stu-id="b33ef-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="b33ef-174">Hello 的所有執行個體指定傳輸類型。未指定的 hello 類型會取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="b33ef-175">您要取樣的 toobe 類型以分號分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="b33ef-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="b33ef-176">可辨識的類型為：相依性、事件、例外狀況、頁面檢視、要求、追蹤。</span><span class="sxs-lookup"><span data-stu-id="b33ef-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="b33ef-177">hello 指定類型所取樣。所有執行個體的 hello 其他類型會永遠傳輸。</span><span class="sxs-lookup"><span data-stu-id="b33ef-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="b33ef-178">**關閉 tooswitch**調整取樣，移除 hello AdaptiveSamplingTelemetryProcessor 節點從 applicationinsights 設定。</span><span class="sxs-lookup"><span data-stu-id="b33ef-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="b33ef-179">替代方法：在程式碼中設定調適性取樣</span><span class="sxs-lookup"><span data-stu-id="b33ef-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="b33ef-180">而不是調整取樣 hello.config 檔案中的，您可以使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="b33ef-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="b33ef-181">這可讓您 toospecify hello 取樣率會重新評估時叫用的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="b33ef-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="b33ef-182">您可以使用此，例如，使用 toofind 出哪些取樣率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="b33ef-183">移除 hello `AdaptiveSamplingTelemetryProcessor` hello.config 檔案中的節點。</span><span class="sxs-lookup"><span data-stu-id="b33ef-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="b33ef-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="b33ef-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="b33ef-185">([深入了解遙測處理器](app-insights-api-filtering-sampling.md#filtering))。</span><span class="sxs-lookup"><span data-stu-id="b33ef-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="b33ef-186">具有 JavaScript 的網頁的取樣</span><span class="sxs-lookup"><span data-stu-id="b33ef-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="b33ef-187">您可以從任何伺服器設定固定取樣率的網頁。</span><span class="sxs-lookup"><span data-stu-id="b33ef-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="b33ef-188">當您[hello 網頁設定為 Application Insights](app-insights-javascript.md)，修改您從 hello Application Insights 入口網站取得的 hello 片段。</span><span class="sxs-lookup"><span data-stu-id="b33ef-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="b33ef-189">（在 ASP.NET 應用程式，hello 片段通常會出現在 _Layout.cshtml。）插入行像`samplingPercentage: 10,`hello 檢測金鑰之前：</span><span class="sxs-lookup"><span data-stu-id="b33ef-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="b33ef-190">Hello 取樣百分比，選擇的百分比是關閉的 too100 N，其中 N 是整數。</span><span class="sxs-lookup"><span data-stu-id="b33ef-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="b33ef-191">目前取樣並不支援其他值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="b33ef-192">如果您也可以啟用在 hello 伺服器固定速率取樣，hello 用戶端和伺服器將會同步，讓該，在搜尋時，您可以瀏覽相關的頁面檢視及要求。</span><span class="sxs-lookup"><span data-stu-id="b33ef-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="b33ef-193">適用於 ASP.NET 網站的固定取樣率</span><span class="sxs-lookup"><span data-stu-id="b33ef-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="b33ef-194">固定取樣可以減少從您網頁伺服器和網頁瀏覽器傳送的 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="b33ef-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="b33ef-195">但它會依照您設定的速率來降低遙測，這與調適性取樣不同。</span><span class="sxs-lookup"><span data-stu-id="b33ef-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="b33ef-196">它也會同步 hello 用戶端和伺服器取樣讓相關的項目，就會保留-例如，因此如果您看一下檢視中搜尋的頁面，您可以找到其相關的要求。</span><span class="sxs-lookup"><span data-stu-id="b33ef-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="b33ef-197">hello 的採樣演算法會保留相關項目。</span><span class="sxs-lookup"><span data-stu-id="b33ef-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="b33ef-198">對於每個 HTTP 要求事件，它及其相關事件會遭到捨棄或傳輸。</span><span class="sxs-lookup"><span data-stu-id="b33ef-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="b33ef-199">計量瀏覽器中速度，例如要求和例外狀況計數會乘以 hello 取樣率的因數 toocompensate，使其大約正確。</span><span class="sxs-lookup"><span data-stu-id="b33ef-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="b33ef-200">**更新您的專案 NuGet 套件**toohello 最新*發行前版本*新版 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="b33ef-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="b33ef-201">以滑鼠右鍵按一下方案總管] 中的 hello 專案中，選擇 [管理 NuGet 封裝，請檢查**包含發行前版本**並 Microsoft.ApplicationInsights.Web 搜尋。</span><span class="sxs-lookup"><span data-stu-id="b33ef-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="b33ef-202">**停用自動調整取樣**： 在[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)、 移除或註解 hello`AdaptiveSamplingTelemetryProcessor`節點。</span><span class="sxs-lookup"><span data-stu-id="b33ef-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="b33ef-203">**啟用 hello 固定速率取樣模組。**</span><span class="sxs-lookup"><span data-stu-id="b33ef-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="b33ef-204">加入這個程式碼片段太[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="b33ef-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="b33ef-205">Hello 取樣百分比，選擇的百分比是關閉的 too100 N，其中 N 是整數。</span><span class="sxs-lookup"><span data-stu-id="b33ef-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="b33ef-206">目前取樣並不支援其他值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="b33ef-207">替代方法：在伺服器程式碼中啟用固定取樣率</span><span class="sxs-lookup"><span data-stu-id="b33ef-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="b33ef-208">而不是設定 hello 取樣參數 hello.config 檔案中，您可以使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="b33ef-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="b33ef-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="b33ef-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="b33ef-210">([深入了解遙測處理器](app-insights-api-filtering-sampling.md#filtering))。</span><span class="sxs-lookup"><span data-stu-id="b33ef-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="b33ef-211">當 toouse 取樣嗎？</span><span class="sxs-lookup"><span data-stu-id="b33ef-211">When toouse sampling?</span></span>
<span data-ttu-id="b33ef-212">如果您使用 ASP.NET 的 SDK 版本 2.0.0-beta3 hello，會自動啟用自動調整取樣或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b33ef-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="b33ef-213">無論您使用哪個版本的 SDK，都可以 (在我們的伺服器上) 使用擷取取樣 。</span><span class="sxs-lookup"><span data-stu-id="b33ef-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="b33ef-214">對大多數小型和中型大小應用程式，您不需要取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="b33ef-215">hello 最有用的診斷資訊，並最精確的統計資料後所取得您所有的使用者活動上收集資料。</span><span class="sxs-lookup"><span data-stu-id="b33ef-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="b33ef-216">hello 的取樣的主要優點包括：</span><span class="sxs-lookup"><span data-stu-id="b33ef-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="b33ef-217">當您的應用程式在短時間間隔傳送非常高比率的遙測時，Application Insights 服務會將資料點卸除 (「節流」)。</span><span class="sxs-lookup"><span data-stu-id="b33ef-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="b33ef-218">hello 內 tookeep[配額](app-insights-pricing.md)的定價層的資料點。</span><span class="sxs-lookup"><span data-stu-id="b33ef-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="b33ef-219">tooreduce hello 收集的遙測資料從網路流量。</span><span class="sxs-lookup"><span data-stu-id="b33ef-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="b33ef-220">我應該使用哪種類型的取樣？</span><span class="sxs-lookup"><span data-stu-id="b33ef-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="b33ef-221">**如果是下列情形，請使用擷取取樣：**</span><span class="sxs-lookup"><span data-stu-id="b33ef-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="b33ef-222">您的遙測經常會超出每月配額。</span><span class="sxs-lookup"><span data-stu-id="b33ef-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="b33ef-223">您用 hello SDK 不支援取樣-例如，hello Java SDK 或 ASP.NET 版本的版本早於 2。</span><span class="sxs-lookup"><span data-stu-id="b33ef-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="b33ef-224">您收到大量來自使用者網頁瀏覽器的遙測。</span><span class="sxs-lookup"><span data-stu-id="b33ef-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="b33ef-225">**如果是下列情形，則使用固定取樣率：**</span><span class="sxs-lookup"><span data-stu-id="b33ef-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="b33ef-226">您使用 ASP.NET web 服務版本 2.0.0 的 hello Application Insights SDK 或更新版本，以及</span><span class="sxs-lookup"><span data-stu-id="b33ef-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="b33ef-227">您想要用戶端與伺服器之間的同步處理取樣如此，當您想調查中的事件[搜尋](app-insights-diagnostic-search.md)，您可以巡覽 hello 用戶端上的相關的事件與伺服器，例如頁面檢視和 http 要求。</span><span class="sxs-lookup"><span data-stu-id="b33ef-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="b33ef-228">您自信 hello 適當取樣百分比的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b33ef-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="b33ef-229">應該夠高 tooget 精確的衡量標準，但以下 hello 速率超過定價配額並 hello 節流限制。</span><span class="sxs-lookup"><span data-stu-id="b33ef-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="b33ef-230">**使用調適性取樣：**</span><span class="sxs-lookup"><span data-stu-id="b33ef-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="b33ef-231">否則，建議使用調適性取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="b33ef-232">啟用此選項預設會在 hello ASP.NET 伺服器 SDK，2.0.0-beta3 版本或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b33ef-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="b33ef-233">它只會影響速率達到某個最低值的流量，因此不會影響使用率較低的網站。</span><span class="sxs-lookup"><span data-stu-id="b33ef-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="b33ef-234">如何得知取樣是否正在運作中？</span><span class="sxs-lookup"><span data-stu-id="b33ef-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="b33ef-235">取樣率，不論它有已套用的位置，使用 toodiscover hello 實際[分析查詢](app-insights-analytics.md)如下：</span><span class="sxs-lookup"><span data-stu-id="b33ef-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="b33ef-236">在每個保留的記錄，`itemCount`指出 hello 原始記錄數目，它代表相等 too1 + hello 先前已捨棄的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="b33ef-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="b33ef-237">取樣運作方式？</span><span class="sxs-lookup"><span data-stu-id="b33ef-237">How does sampling work?</span></span>
<span data-ttu-id="b33ef-238">固定速率和彈性的取樣是 hello 的從 2.0.0 及更新版本的 ASP.NET 版本中 SDK 的功能。</span><span class="sxs-lookup"><span data-stu-id="b33ef-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="b33ef-239">擷取取樣是 hello Application Insights 服務的功能，而且可以在作業中如果 hello SDK 不會執行取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="b33ef-240">hello 的採樣演算法來決定哪些遙測項目 toodrop，以及哪些是 tookeep （不論它是否在 hello SDK 或在 hello Application Insights 服務）。</span><span class="sxs-lookup"><span data-stu-id="b33ef-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="b33ef-241">hello 取樣決策根據目標 toopreserve 保持不變，維持可採取動作，而且即使有一組縮減資料可靠的 Application Insights 中的診斷經驗的所有相互關聯的資料點的數個規則。</span><span class="sxs-lookup"><span data-stu-id="b33ef-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="b33ef-242">比方說，如果是失敗的要求，您的應用程式會傳送其他遙測項目 (例如從此要求記錄的例外狀況和追蹤)，取樣將不會分割此要求和其他遙測。</span><span class="sxs-lookup"><span data-stu-id="b33ef-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="b33ef-243">它會一起保留或卸除。</span><span class="sxs-lookup"><span data-stu-id="b33ef-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="b33ef-244">如此一來，當您查看 Application Insights 中的 hello 要求詳細資料，您可以永遠看到 hello 要求以及其相關聯的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="b33ef-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="b33ef-245">定義 「 使用者 」 的應用程式 (也就是最常見的 web 應用程式)，hello 取樣決策根據 hello 使用者識別碼，這表示，任何特定使用者的所有遙測已保留或卸除 hello 雜湊。</span><span class="sxs-lookup"><span data-stu-id="b33ef-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="b33ef-246">Hello 類型未定義的使用者 （例如 web 服務） 的應用程式的 hello 取樣決策根據 hello hello 要求的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="b33ef-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="b33ef-247">最後，兩者都不具有設定 （如範例遙測項目從無 http 內容的非同步執行緒報告） 的使用者，也不作業識別碼 hello 遙測項目取樣只會擷取遙測項目，每個類型的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="b33ef-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="b33ef-248">當呈現遙測後 tooyou，hello Application Insights 服務調整 hello 度量的 hello 相同的集合，如遺漏資料點的 hello toocompensate hello 次中使用的取樣百分比。</span><span class="sxs-lookup"><span data-stu-id="b33ef-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="b33ef-249">因此，當查看 Application Insights 中的 hello 遙測，hello 使用者會看到以統計方式正確會非常接近 toohello 實際數字的近似值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="b33ef-250">hello 近似值 hello 精確度主要是取決於設定的 hello 取樣百分比。</span><span class="sxs-lookup"><span data-stu-id="b33ef-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="b33ef-251">此外，hello 精確度會增加處理大量的大量使用者通常類似要求的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b33ef-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="b33ef-252">在 hello 換句話說，應用程式，不適用於大量負載的取樣不需要為這些應用程式通常可以傳送其所有的遙測資料仍 hello 配額，而不會造成資料遺失的節流。</span><span class="sxs-lookup"><span data-stu-id="b33ef-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="b33ef-253">請注意，Application Insights 不範例度量和工作階段遙測類型，因為這些類型，減少 hello 有效位數可以是非常讓人困擾。</span><span class="sxs-lookup"><span data-stu-id="b33ef-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="b33ef-254">調適性取樣</span><span class="sxs-lookup"><span data-stu-id="b33ef-254">Adaptive sampling</span></span>
<span data-ttu-id="b33ef-255">自動調整取樣 hello SDK，從目前的傳輸速率該監視器 hello 新增元件，並調整 hello 取樣百分比 tootry toostay 內 hello 目標的最大速率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="b33ef-256">hello 調整定期重新計算，並且根據移動平均值的 hello 外寄傳輸速率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="b33ef-257">取樣和 hello JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="b33ef-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="b33ef-258">hello 用戶端 (JavaScript) SDK 參與固定速率取樣搭配 hello 伺服器端 SDK。</span><span class="sxs-lookup"><span data-stu-id="b33ef-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="b33ef-259">hello 檢測頁面只會從相同的 hello 伺服器端所做的決策的使用者太 」 範例中。"hello 傳送用戶端遙測</span><span class="sxs-lookup"><span data-stu-id="b33ef-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="b33ef-260">此邏輯會是跨用戶端-伺服器-端及設計的 toomaintain 完整性的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="b33ef-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="b33ef-261">如此一來，您可以從 Application Insights 中的任何特定遙測項目找到這個使用者或工作階段的所有其他遙測項目。</span><span class="sxs-lookup"><span data-stu-id="b33ef-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="b33ef-262">*我的用戶端和伺服器端遙測未顯示您上方描述的協調範例。*</span><span class="sxs-lookup"><span data-stu-id="b33ef-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="b33ef-263">請確認您在伺服器及用戶端上都已啟用固定取樣率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="b33ef-264">請確定該 hello SDK 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b33ef-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="b33ef-265">您所設定的核取 hello 相同取樣 hello 用戶端和伺服器中的百分比。</span><span class="sxs-lookup"><span data-stu-id="b33ef-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b33ef-266">常見問題集</span><span class="sxs-lookup"><span data-stu-id="b33ef-266">Frequently Asked Questions</span></span>
<span data-ttu-id="b33ef-267">*為什麼不取樣簡單的「收集每個遙測類型百分之 X」？*</span><span class="sxs-lookup"><span data-stu-id="b33ef-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="b33ef-268">雖然此取樣方法會提供極高的有效位數中度量的近似值，它會破壞每個使用者、 工作階段和要求，這相當重要的診斷能力 toocorrelate 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="b33ef-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="b33ef-269">因此，對於「收集應用程式使用者百分之 X 的所有遙測項目」或「收集應用程式要求百分之 X 的所有遙測」邏輯，取樣的效果更佳。</span><span class="sxs-lookup"><span data-stu-id="b33ef-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="b33ef-270">Hello 遙測項目未與 hello 要求 （例如背景非同步處理） 相關聯，hello 改回是太"收集的每個遙測類型的所有項目 %x。 」</span><span class="sxs-lookup"><span data-stu-id="b33ef-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="b33ef-271">*經過一段時間，可以 hello 取樣百分比變更嗎？*</span><span class="sxs-lookup"><span data-stu-id="b33ef-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="b33ef-272">是，自動調整取樣逐漸變更 hello 目前觀察到的 hello 遙測資料的磁碟區所根據的 hello 取樣百分比。</span><span class="sxs-lookup"><span data-stu-id="b33ef-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="b33ef-273">*如果我使用固定速率取樣時，如何知道哪些取樣百分比運作 hello 最適合我的應用程式？*</span><span class="sxs-lookup"><span data-stu-id="b33ef-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="b33ef-274">其中一個方法是使用自動調整取樣 toostart，找出它評分 settles （請參閱上述問題的 hello） 和交換器 toofixed 速率然後取樣使用的速率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="b33ef-275">否則，您必須 tooguess。</span><span class="sxs-lookup"><span data-stu-id="b33ef-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="b33ef-276">分析目前的遙測 AI 使用量中出現任何節流也就是發生，以及評估 hello 磁碟區的 hello 收集遙測資料。</span><span class="sxs-lookup"><span data-stu-id="b33ef-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="b33ef-277">下列三個輸入，以及您選取的定價層建議多少，您可能會想 tooreduce hello 磁碟區的 hello 收集遙測資料。</span><span class="sxs-lookup"><span data-stu-id="b33ef-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="b33ef-278">不過，hello 您的使用者數目的增加或其他某些 shift hello 的遙測資料的磁碟區中可能會使您的評估。</span><span class="sxs-lookup"><span data-stu-id="b33ef-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="b33ef-279">*如果將取樣百分比設定成太低會發生什麼事？*</span><span class="sxs-lookup"><span data-stu-id="b33ef-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="b33ef-280">Application Insights 嘗試 toocompensate hello 視覺效果的 hello 減少 hello 資料磁碟區的資料時，極低取樣百分比 （over-aggressive 取樣） 可減少 hello 精確度的 hello 近似值。</span><span class="sxs-lookup"><span data-stu-id="b33ef-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="b33ef-281">此外，診斷體驗可能會受到負面影響，與 hello 不常失敗的或慢速要求出取樣。</span><span class="sxs-lookup"><span data-stu-id="b33ef-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="b33ef-282">*如果將取樣百分比設定成太高會發生什麼事？*</span><span class="sxs-lookup"><span data-stu-id="b33ef-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="b33ef-283">設定太高取樣百分比 （不變得積極夠） 導致 hello hello 數量不足，無法減少收集的遙測。</span><span class="sxs-lookup"><span data-stu-id="b33ef-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="b33ef-284">仍可能會發生資料遺失相關 toothrottling，以及使用 Application Insights hello 成本可能會高於您計劃，因為 toooverage 費用的遙測。</span><span class="sxs-lookup"><span data-stu-id="b33ef-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="b33ef-285">*我可以在何種平台上使用取樣？*</span><span class="sxs-lookup"><span data-stu-id="b33ef-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="b33ef-286">特定磁碟區，上述任何遙測，如果 hello SDK 目前並未在執行取樣擷取取樣會自動發生。</span><span class="sxs-lookup"><span data-stu-id="b33ef-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="b33ef-287">這會運作，例如，如果您的應用程式使用 Java 伺服器，或如果您使用較舊版本的 hello ASP.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="b33ef-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="b33ef-288">如果您使用 ASP.NET 的 SDK 版本 2.0.0 和更新版本 （裝載在 Azure 或您自己的伺服器上），您會收到自動調整取樣根據預設，但如上面所述，您可以切換 toofixed 速率。</span><span class="sxs-lookup"><span data-stu-id="b33ef-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="b33ef-289">使用固定速率取樣 hello 瀏覽器 SDK 會自動同步 toosample 相關事件。</span><span class="sxs-lookup"><span data-stu-id="b33ef-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="b33ef-290">*有希望 toosee 某些罕見的事件。如何取得其過去的 hello 取樣模組？*</span><span class="sxs-lookup"><span data-stu-id="b33ef-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="b33ef-291">初始化新 TelemetryConfiguration （不 hello 預設作用中） 與 TelemetryClient 個別執行個體。</span><span class="sxs-lookup"><span data-stu-id="b33ef-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="b33ef-292">使用該 toosend 罕見的事件。</span><span class="sxs-lookup"><span data-stu-id="b33ef-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b33ef-293">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b33ef-293">Next steps</span></span>
* <span data-ttu-id="b33ef-294">[篩選](app-insights-api-filtering-sampling.md) 可以對您的 SDK 所傳送的內容，提供更嚴格的控制。</span><span class="sxs-lookup"><span data-stu-id="b33ef-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

