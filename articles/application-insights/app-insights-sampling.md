---
title: "Azure Application Insights 中的遙測取樣 | Microsoft Docs"
description: "如何讓遙測量保持在控制下。"
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
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="e1f1e-103">Application Insights 中的取樣</span><span class="sxs-lookup"><span data-stu-id="e1f1e-103">Sampling in Application Insights</span></span>


<span data-ttu-id="e1f1e-104">取樣是 [Azure Application Insights](app-insights-overview.md) 中的一個功能。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="e1f1e-105">若要既能減少遙測流量和儲存空間，又能保有應用程式資料在統計上的正確分析，便建議使用此方法。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="e1f1e-106">篩選器會選取相關的項目，以便您在進行診斷調查時瀏覽各個項目。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="e1f1e-107">在入口網站中呈現度量計數時，就會重新正規化以考慮取樣，以將對統計資料帶來的任何影響降至最低。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="e1f1e-108">取樣可減少流量與資料成本，而且可以協助您避免節流。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="e1f1e-109">簡單地說︰</span><span class="sxs-lookup"><span data-stu-id="e1f1e-109">In brief:</span></span>
* <span data-ttu-id="e1f1e-110">取樣會保留 1  *n* 記錄，並捨棄其餘部分。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="e1f1e-111">比方說，它可能會保留 5 個事件的其中 1 個，取樣率為 20%。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="e1f1e-112">如果您的應用程式傳送大量遙測，ASP.NET Web 伺服器應用程式便會自動進行取樣。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="e1f1e-113">您也可以手動設定取樣，不論是透過入口網站的定價頁面；或是在 ASP.NET SDK 的 .config 檔案中，以便同時降低網路流量。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="e1f1e-114">如果您有記錄自訂事件，而且想要確定某組事件已一起保留下來還是遭到捨棄，請確定它們有相同的 OperationId 值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="e1f1e-115">取樣除數 *n* 屬性中的每一筆記錄來報告`itemCount`，搜尋在下方的好記的名稱 「 要求計數 」 或 「 事件計數 」。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="e1f1e-116">當取樣不在作業中，則 `itemCount==1`。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="e1f1e-117">如果您要撰寫分析查詢，請 [考慮到取樣](app-insights-analytics-tour.md#counting-sampled-data)。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="e1f1e-118">特別是，您應該使用 `summarize sum(itemCount)`，而非只計算記錄。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="e1f1e-119">取樣類型</span><span class="sxs-lookup"><span data-stu-id="e1f1e-119">Types of sampling</span></span>
<span data-ttu-id="e1f1e-120">有三個替代的取樣方法：</span><span class="sxs-lookup"><span data-stu-id="e1f1e-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="e1f1e-121">**調適性取樣** 會自動調整從您 ASP.NET 應用程式中 SDK 所傳送的遙測量。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="e1f1e-122">預設從 SDK v 2.0.0-beta3 傳送。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="e1f1e-123">目前僅供 ASP.NET 伺服器端遙測使用。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="e1f1e-124">「固定比例取樣」可減少從您 ASP.NET 伺服器和使用者的瀏覽器所傳送的遙測量，</span><span class="sxs-lookup"><span data-stu-id="e1f1e-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="e1f1e-125">而比例則由您設定。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-125">You set the rate.</span></span> <span data-ttu-id="e1f1e-126">用戶端和伺服器會同步處理它們的取樣，讓您可以在 [搜尋] 終於相關的頁面檢視和要求之間瀏覽。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="e1f1e-127">「擷取取樣」可在 Azure 入口網站中運作。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="e1f1e-128">它會根據您設定的比例，捨棄來自您應用程式的一些遙測。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="e1f1e-129">這不會減少遙測流量，但可協助您讓流量不要超過每月配額。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="e1f1e-130">擷取取樣的一大優點是您不需重新部署應用程式即可設定它，並且它對所有伺服器和用戶端的運作方式都一致。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="e1f1e-131">如果自適性或固定速率取樣正在作業中，則會停用擷取取樣。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="e1f1e-132">擷取取樣</span><span class="sxs-lookup"><span data-stu-id="e1f1e-132">Ingestion sampling</span></span>
<span data-ttu-id="e1f1e-133">這種形式的取樣會在來自您 Web 伺服器、瀏覽器及裝置的遙測抵達 Application Insights 服務端點時開始執行。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="e1f1e-134">雖然它不會減少來自您應用程式的遙測流量，但會減少 Application Insights 所處理及保留 (並收費) 的遙測量。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="e1f1e-135">如果您的應用程式通常會超過每月配額，且您無法選擇使用任何一種 SDK 式的取樣類型，請使用這種類型的取樣。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="e1f1e-136">在 [配額和價格] 刀鋒視窗中設定取樣率：</span><span class="sxs-lookup"><span data-stu-id="e1f1e-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![在 [應用程式概觀] 刀鋒視窗中，依序按一下 [設定]、[配額]、[範例]，然後選取某個取樣率，並按一下 [更新]。](./media/app-insights-sampling/04.png)

<span data-ttu-id="e1f1e-138">就跟其他取樣類型一樣，演算法會保留相關的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="e1f1e-139">舉例來說，當您在 [搜尋] 中檢查遙測時，將能夠尋找與特定例外狀況相關的要求。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="e1f1e-140">度量計量 (例如要求率及例外狀況率) 會正確地保留。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="e1f1e-141">遭到取樣捨棄的資料點將無法在任何 Application Insights 功能中使用，例如 [連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="e1f1e-142">進行 SDK 自適性或固定速率取樣時，不執行擷取取樣。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="e1f1e-143">如果 SDK 的取樣率小於 100%，則忽略您設定的擷取取樣率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="e1f1e-144">圖格上顯示的值會指出您要為擷取取樣的值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="e1f1e-145">如果 SDK 取樣在運作中，這並不代表實際的取樣率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="e1f1e-146">在您 Web 伺服器上的調適性取樣</span><span class="sxs-lookup"><span data-stu-id="e1f1e-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="e1f1e-147">Application Insights SDK for ASP.NET v 2.0.0-beta3 及更新版本提供調適性取樣功能，且預設為啟用。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="e1f1e-148">調適性取樣會影響從您的 Web 伺服器應用程式傳送給 Application Insights 服務的遙測量。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="e1f1e-149">系統會自動調整遙測量，以便讓流量速率不會超出指定的上限。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="e1f1e-150">它無法在低遙測量的情況下運作，因此偵錯中的應用程式或使用率低的網站不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="e1f1e-151">為了要讓遙測量達到目標，系統會捨棄部分已產生的遙測。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="e1f1e-152">但就跟其他取樣類型一樣，演算法會保留相關的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="e1f1e-153">舉例來說，當您在 [搜尋] 中檢查遙測時，將能夠尋找與特定例外狀況相關的要求。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="e1f1e-154">度量計量 (例如要求率及例外狀況率) 會受到調整來補償取樣率，讓它們能在計量瀏覽器中顯示大致上正確的值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="e1f1e-155">**將您專案的 NuGet 套件更新**至 Application Insights 的最新「發行前」版本：在 [方案總管] 中的專案上按一下滑鼠右鍵、選擇 [管理 NuGet 套件]、核取 [包含發行前版本]，然後搜尋 Microsoft.ApplicationInsights.Web。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="e1f1e-156">在 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 中，您可以調整 `AdaptiveSamplingTelemetryProcessor` 節點中的數個參數。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="e1f1e-157">顯示的數字是預設值：</span><span class="sxs-lookup"><span data-stu-id="e1f1e-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="e1f1e-158">調整演算法對於 **每部伺服器主機**的目標速率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="e1f1e-159">如果 Web 應用程式在許多主機上執行，請減少此值，以保持在您的 Application Insights 入口網站的流量目標速率內。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="e1f1e-160">目前遙測速率的間隔已重新評估。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="e1f1e-161">評估是以移動平均來執行。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="e1f1e-162">如果您的遙測會突然暴增，您可能想要縮短此間隔。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="e1f1e-163">當取樣百分比值變更時，多久之後我們可以降低取樣百分比，以擷取較少的資料。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="e1f1e-164">當取樣百分比值變更時，多久之後我們可以增加取樣百分比，以擷取較多的資料。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="e1f1e-165">隨著取樣百分比改變，我們可以設定的最小值是多少。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="e1f1e-166">隨著取樣百分比改變，我們可以設定的最大值是多少。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="e1f1e-167">在計算移動平均時，指派給最新的值的權數。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="e1f1e-168">使用等於或小於 1 的值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="e1f1e-169">較小的值會讓演算法不易受突然的變更影響。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="e1f1e-170">當應用程式剛開始時指派的值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="e1f1e-171">不要在偵錯時減少此值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="e1f1e-172">不要進行取樣的分號分隔類型清單。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="e1f1e-173">可辨識的類型為：相依性、事件、例外狀況、頁面檢視、要求、追蹤。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="e1f1e-174">會傳送所指定類型的所有執行個體；會針對未指定的類型進行取樣。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="e1f1e-175">要進行取樣的分號分隔類型清單。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="e1f1e-176">可辨識的類型為：相依性、事件、例外狀況、頁面檢視、要求、追蹤。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="e1f1e-177">會針對指定的類型進行取樣；將一律會傳輸其他類型的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="e1f1e-178">**若要關閉**調適型取樣，請將 AdaptiveSamplingTelemetryProcessor 節點從 applicationinsights-config 移除。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="e1f1e-179">替代方法：在程式碼中設定調適性取樣</span><span class="sxs-lookup"><span data-stu-id="e1f1e-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="e1f1e-180">除了在 .config 檔中調整取樣之外，您還可以使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="e1f1e-181">這可讓您指定在每次取樣率重新評估時叫用的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="e1f1e-182">例如，您可以使用這個方法來找出使用中的取樣率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="e1f1e-183">移除 .config 檔案中的 `AdaptiveSamplingTelemetryProcessor` 節點。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="e1f1e-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

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
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="e1f1e-185">([深入了解遙測處理器](app-insights-api-filtering-sampling.md#filtering))。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="e1f1e-186">具有 JavaScript 的網頁的取樣</span><span class="sxs-lookup"><span data-stu-id="e1f1e-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="e1f1e-187">您可以從任何伺服器設定固定取樣率的網頁。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="e1f1e-188">當您 [設定 Application Insights 的網頁](app-insights-javascript.md)時，請修改您從 Application Insights 入口網站取得的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="e1f1e-189">(在 ASP.NET 應用程式中，程式碼片段通常會出現在 _Layout.cshtml。)在檢測金鑰之前插入類似 `samplingPercentage: 10,` 的一行：</span><span class="sxs-lookup"><span data-stu-id="e1f1e-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

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

<span data-ttu-id="e1f1e-190">針對取樣百分比，選擇接近 100/N 的百分比，其中 N 是整數。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="e1f1e-191">目前取樣並不支援其他值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="e1f1e-192">如果您也在伺服器啟用固定比例取樣，用戶端和伺服器就會同步，讓您可以在 [搜尋] 中的相關頁面檢視與要求之間瀏覽。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="e1f1e-193">適用於 ASP.NET 網站的固定取樣率</span><span class="sxs-lookup"><span data-stu-id="e1f1e-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="e1f1e-194">固定取樣率會減少從您的 Web 伺服器及網頁瀏覽器所傳送的流量。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="e1f1e-195">但它會依照您設定的速率來降低遙測，這與調適性取樣不同。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="e1f1e-196">它也會同步處理用戶端及伺服器取樣，讓相關項目能夠保留；舉例來說，讓您在 [搜尋] 中查看頁面檢視時，能夠尋找其相關要求。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="e1f1e-197">取樣演算法會保留相關項目。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="e1f1e-198">對於每個 HTTP 要求事件，它及其相關事件會遭到捨棄或傳輸。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="e1f1e-199">在計量瀏覽器中，速率 (例如要求及例外狀況數) 會乘以某個係數來補償取樣率，讓它們能大致上正確。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="e1f1e-200">**將您專案的 NuGet 套件更新**至 Application Insights 的最新「發行前」版本。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="e1f1e-201">以滑鼠右鍵按一下方案總管中的專案，選擇 [管理 NuGet 封裝]，然後核取 [包含發行前版本]  並搜尋 Microsoft.ApplicationInsights.Web。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="e1f1e-202">**停用調適性取樣**：在 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 中，將 `AdaptiveSamplingTelemetryProcessor` 節點移除或設成註解。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="e1f1e-203">**啟用固定取樣率模組。**</span><span class="sxs-lookup"><span data-stu-id="e1f1e-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="e1f1e-204">將此程式碼片段新增至 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)：</span><span class="sxs-lookup"><span data-stu-id="e1f1e-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="e1f1e-205">針對取樣百分比，選擇接近 100/N 的百分比，其中 N 是整數。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="e1f1e-206">目前取樣並不支援其他值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="e1f1e-207">替代方法：在伺服器程式碼中啟用固定取樣率</span><span class="sxs-lookup"><span data-stu-id="e1f1e-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="e1f1e-208">除了在 .config 檔中設定取樣參數之外，您還可以使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="e1f1e-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-209">*C#*</span></span>

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

<span data-ttu-id="e1f1e-210">([深入了解遙測處理器](app-insights-api-filtering-sampling.md#filtering))。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="e1f1e-211">何時使用取樣？</span><span class="sxs-lookup"><span data-stu-id="e1f1e-211">When to use sampling?</span></span>
<span data-ttu-id="e1f1e-212">如果您使用 ASP.NET SDK 版本 2.0.0-beta3 或更新版本，調適性取樣會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="e1f1e-213">無論您使用哪個版本的 SDK，都可以 (在我們的伺服器上) 使用擷取取樣 。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="e1f1e-214">對大多數小型和中型大小應用程式，您不需要取樣。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="e1f1e-215">最有用的診斷資訊和最準確的統計資料會是透過收集所有使用者活動的資料取得。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="e1f1e-216">取樣的主要優點如下：</span><span class="sxs-lookup"><span data-stu-id="e1f1e-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="e1f1e-217">當您的應用程式在短時間間隔傳送非常高比率的遙測時，Application Insights 服務會將資料點卸除 (「節流」)。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="e1f1e-218">保持在定價層的資料點 [配額](app-insights-pricing.md) 內。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="e1f1e-219">若要從收集的遙測降低網路流量。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="e1f1e-220">我應該使用哪種類型的取樣？</span><span class="sxs-lookup"><span data-stu-id="e1f1e-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="e1f1e-221">**如果是下列情形，請使用擷取取樣：**</span><span class="sxs-lookup"><span data-stu-id="e1f1e-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="e1f1e-222">您的遙測經常會超出每月配額。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="e1f1e-223">您使用不支援取樣的 SDK 版本，例如 Java SDK 或是比 ASP.NET 版本 2 早的版本。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="e1f1e-224">您收到大量來自使用者網頁瀏覽器的遙測。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="e1f1e-225">**如果是下列情形，則使用固定取樣率：**</span><span class="sxs-lookup"><span data-stu-id="e1f1e-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="e1f1e-226">您使用 Application Insights SDK for ASP.NET Web 服務版本 2.0.0 或更新版本，且</span><span class="sxs-lookup"><span data-stu-id="e1f1e-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="e1f1e-227">您想要同步處理用戶端與伺服器之間的取樣，因此，當您在 [搜尋](app-insights-diagnostic-search.md)中調查事件時，您可以在用戶端與伺服器的相關事件之間調查，例如頁面檢視和 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="e1f1e-228">您對於您的應用程式的適當取樣百分比有信心。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="e1f1e-229">應該夠高以取得精確的度量，但是低於超過價格配額和節流限制的取樣率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="e1f1e-230">**使用調適性取樣：**</span><span class="sxs-lookup"><span data-stu-id="e1f1e-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="e1f1e-231">否則，建議使用調適性取樣。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="e1f1e-232">在 ASP.NET 伺服器 SDK 版本 2.0.0-beta3 或更新版本中，此功能為預設啟用。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="e1f1e-233">它只會影響速率達到某個最低值的流量，因此不會影響使用率較低的網站。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="e1f1e-234">如何得知取樣是否正在運作中？</span><span class="sxs-lookup"><span data-stu-id="e1f1e-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="e1f1e-235">若要找出實際的取樣率 (不論是否已套用)，請使用如下所示的 [分析查詢](app-insights-analytics.md) ︰</span><span class="sxs-lookup"><span data-stu-id="e1f1e-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="e1f1e-236">在每筆保留的記錄中， `itemCount` 表示它所代表的原始記錄筆數，其等於 1 + 先前捨棄的記錄筆數。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="e1f1e-237">取樣運作方式？</span><span class="sxs-lookup"><span data-stu-id="e1f1e-237">How does sampling work?</span></span>
<span data-ttu-id="e1f1e-238">固定取樣率和調適性取樣是 ASP.NET 版本 (從 2.0.0 更新版本開始) 中 SDK 的一項功能。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="e1f1e-239">擷取取樣是 Application Insights 服務的一項功能，而且可在 SDK 未執行取樣時運作。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="e1f1e-240">採樣演算法會決定要捨棄哪些遙測項目，以及要保留哪些遙測項目 (其是否位於 SDK 或 Application Insights 服務中)。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="e1f1e-241">取樣決策會根據數個規則，目標是要保留相關的資料點不變，在 Application Insights 中保有可採取動作而且即使有縮減資料集仍可靠的診斷經驗。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="e1f1e-242">比方說，如果是失敗的要求，您的應用程式會傳送其他遙測項目 (例如從此要求記錄的例外狀況和追蹤)，取樣將不會分割此要求和其他遙測。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="e1f1e-243">它會一起保留或卸除。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="e1f1e-244">如此一來，當您在 Application Insights 中查看要求詳細資料時，您一律可以看到要求和其相關聯的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="e1f1e-245">針對定義「使用者」的應用程式 (也就是最常見的 Web 應用程式)，取樣決策是根據使用者識別碼的雜湊，這表示任何特定使用者的所有遙測可加以保留或卸除。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="e1f1e-246">針對沒有定義使用者的應用程式類型 (例如 Web 服務)，取樣決策係根據要求的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="e1f1e-247">最後，對於未設定使用者或作業識別碼的遙測項目 (例如非同步執行緒報告、不具使用任何 http 內容的遙測項目)，取樣只會擷取每種類型的遙測項目的某個百分比。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="e1f1e-248">呈現遙測回來給您時，Application Insights 服務會以收集時使用的相同取樣百分比調整度量，來彌補遺漏的資料點。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="e1f1e-249">因此，在 Application Insights 中查看遙測時，使用者會看到統計正確也非常接近實際數的近似值。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="e1f1e-250">近似值的精確度絕大部分取決於設定的取樣百分比。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="e1f1e-251">此外，對於處理大量使用者的通常類似要求的應用程式，其精確度會增加。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="e1f1e-252">相反地，對於不處理大量負載的應用程式，就不需要取樣，因為這些應用程式通常可以傳送遙測同時保持在配額內，而不會因節流造成資料遺失。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="e1f1e-253">請注意，Application Insights 不會對度量和工作階段遙測類型取樣，因為這些類型的有效位數減少可能高度讓人困擾。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="e1f1e-254">調適性取樣</span><span class="sxs-lookup"><span data-stu-id="e1f1e-254">Adaptive sampling</span></span>
<span data-ttu-id="e1f1e-255">調適性取樣會新增元件，該元件會監視 SDK 的目前傳輸速率，並調整取樣百分比，以嘗試保持在目標最大速率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="e1f1e-256">調整會定期重新計算，並且根據外寄傳輸速率的移動平均。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="e1f1e-257">取樣與 JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="e1f1e-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="e1f1e-258">用戶端 (JavaScript) SDK 與伺服器端 SDK 一同參與固定取樣率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="e1f1e-259">已檢測的頁面只會從伺服器端決定「納入取樣」的相同使用者傳送用戶端遙測。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="e1f1e-260">此邏輯的設計是為了在用戶端和伺服器端之間保有使用者工作階段的完整性。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="e1f1e-261">如此一來，您可以從 Application Insights 中的任何特定遙測項目找到這個使用者或工作階段的所有其他遙測項目。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="e1f1e-262">*我的用戶端和伺服器端遙測未顯示您上方描述的協調範例。*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="e1f1e-263">請確認您在伺服器及用戶端上都已啟用固定取樣率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="e1f1e-264">確定 SDK 版本為 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="e1f1e-265">請檢查您的用戶端和伺服器中設定相同的取樣百分比。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="e1f1e-266">常見問題集</span><span class="sxs-lookup"><span data-stu-id="e1f1e-266">Frequently Asked Questions</span></span>
<span data-ttu-id="e1f1e-267">*為什麼不取樣簡單的「收集每個遙測類型百分之 X」？*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="e1f1e-268">雖然這個取樣方法會提供具有極高精確度的度量近似值，它會破壞根據每個使用者、工作階段和要求相互關聯資料的能力，而這對於診斷是非常重要。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="e1f1e-269">因此，對於「收集應用程式使用者百分之 X 的所有遙測項目」或「收集應用程式要求百分之 X 的所有遙測」邏輯，取樣的效果更佳。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="e1f1e-270">對於與要求無關聯的遙測項目 (例如背景非同步處理)，改為「收集每個遙測類型百分之 X 的所有項目」。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="e1f1e-271">*取樣百分比會隨著時間變更嗎？*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="e1f1e-272">是的，調適性取樣會根據目前觀察到的遙測量，逐漸變更取樣百分比。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="e1f1e-273">*如果我使用固定取樣率，如何知道哪個取樣百分比最適合我的應用程式？*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="e1f1e-274">開始使用調適性取樣的其中一個方法，就是找出它選擇的取樣率 (請參閱上一個問題)，然後再切換為使用該取樣率的固定取樣率。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="e1f1e-275">否則，您就必須猜測。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="e1f1e-276">分析 AI 中您目前的遙測使用量、觀察目前的節流，並估計所收集之遙測的量。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="e1f1e-277">這三項輸入與所選定價層，可對您可能想要減少收集的遙測量提出建議。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="e1f1e-278">不過，使用者數目的增加或遙測量的其他某些變化可能會讓您的評估失效。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="e1f1e-279">*如果將取樣百分比設定成太低會發生什麼事？*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="e1f1e-280">當 Application Insights 嘗試補償減少資料量縮減的資料視覺效果時，過度低的取樣百分比 (過度積極取樣) 會降低近似值的精確度。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="e1f1e-281">此外，診斷經驗可能會有負面影響，因為可能會出取樣出某些不常失敗或緩慢的要求。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="e1f1e-282">*如果將取樣百分比設定成太高會發生什麼事？*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="e1f1e-283">設定太高的取樣百分比 (不夠積極) 會導致收集的遙測量減少不足。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="e1f1e-284">您可能仍會遇到與節流相關的遙測資料遺失，而使用 Application Insights 的成本由於超額費可能高於您的計劃。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="e1f1e-285">*我可以在何種平台上使用取樣？*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="e1f1e-286">如果 SDK 未執行取樣，則擷取取樣會在任何遙測超過特定數量時自動運作。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="e1f1e-287">例如，如果您的 app 使用 Java 伺服器，或者如果您使用舊版 ASP.NET SDK，這應該可行。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="e1f1e-288">如果您使用 ASP.NET SDK 版本 2.0.0 和更新版本 (裝載於 Azure 或您自己的伺服器上)，您預設會得到調適性取樣，但您可以切換到固定取樣率 (如上所述)。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="e1f1e-289">使用固定取樣率，瀏覽器 SDK 會自動同步至取樣相關的事件。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="e1f1e-290">*我一律想要看見特定罕見的事件。我要如何讓它們通過取樣模組？*</span><span class="sxs-lookup"><span data-stu-id="e1f1e-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="e1f1e-291">使用新的 TelemetryConfiguration (非預設使用中的組態) 初始化個別的 TelemetryClient 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="e1f1e-292">使用該執行個體來傳送您的罕見的事件。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f1e-293">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1f1e-293">Next steps</span></span>
* <span data-ttu-id="e1f1e-294">[篩選](app-insights-api-filtering-sampling.md) 可以對您的 SDK 所傳送的內容，提供更嚴格的控制。</span><span class="sxs-lookup"><span data-stu-id="e1f1e-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

