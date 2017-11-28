---
title: "在 Application Insights aaaUse Powershell tooset 警示 |Microsoft 文件"
description: "自動化設定 Application Insights tooget 電子郵件的相關度量的變更。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="8c9e4-103">Application Insights 中使用 PowerShell tooset 警示</span><span class="sxs-lookup"><span data-stu-id="8c9e4-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="8c9e4-104">您可以自動化的 hello 設定[警示](app-insights-alerts.md)中[Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="8c9e4-105">此外，您可以[設定 webhook tooautomate 回應 tooan 警示](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8c9e4-106">如果您想 toocreate 資源和警示在 hello 相同的時間，請考慮[使用 Azure Resource Manager 範本](app-insights-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="8c9e4-107">單次設定</span><span class="sxs-lookup"><span data-stu-id="8c9e4-107">One-time setup</span></span>
<span data-ttu-id="8c9e4-108">若您未曾將 PowerShell 與 Azure 訂用帳戶搭配使用：</span><span class="sxs-lookup"><span data-stu-id="8c9e4-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="8c9e4-109">Hello toorun hello 指令碼所在的電腦上安裝 hello Azure Powershell 模組。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="8c9e4-110">安裝 [Microsoft Web Platform Installer (v5 或更高版本)](http://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="8c9e4-111">它使用 tooinstall Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="8c9e4-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="8c9e4-112">連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8c9e4-112">Connect tooAzure</span></span>
<span data-ttu-id="8c9e4-113">啟動 Azure PowerShell 和[連接 tooyour 訂閱](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="8c9e4-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="8c9e4-114">取得警示</span><span class="sxs-lookup"><span data-stu-id="8c9e4-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="8c9e4-115">Add alert</span><span class="sxs-lookup"><span data-stu-id="8c9e4-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="8c9e4-116">範例 1</span><span class="sxs-lookup"><span data-stu-id="8c9e4-116">Example 1</span></span>
<span data-ttu-id="8c9e4-117">電子郵件給我如果 hello 伺服器回應 tooHTTP 要求，超過 5 分鐘的平均值低於 1 秒。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="8c9e4-118">我的 Application Insights 資源稱為 IceCreamWebApp，其位於 Fabrikam 資源群組。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="8c9e4-119">我 hello hello Azure 訂用帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="8c9e4-120">hello GUID 是 hello 訂用帳戶 ID （不 hello 檢測金鑰的 hello 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="8c9e4-121">範例 2</span><span class="sxs-lookup"><span data-stu-id="8c9e4-121">Example 2</span></span>
<span data-ttu-id="8c9e4-122">我使用的應用程式有[trackmetric （)](app-insights-api-custom-events-metrics.md#trackmetric) tooreport 公制，名為"salesPerHour。 」</span><span class="sxs-lookup"><span data-stu-id="8c9e4-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="8c9e4-123">如果 「 salesPerHour"低於 100，平均過去 24 小時內，傳送電子郵件的同事 toomy。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="8c9e4-124">使用 hello hello 相同的規則可用於 hello 公制報告[度量參數](app-insights-api-custom-events-metrics.md#properties)TrackEvent 或 trackPageView 等其他追蹤呼叫。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="8c9e4-125">度量名稱</span><span class="sxs-lookup"><span data-stu-id="8c9e4-125">Metric names</span></span>
| <span data-ttu-id="8c9e4-126">度量名稱</span><span class="sxs-lookup"><span data-stu-id="8c9e4-126">Metric name</span></span> | <span data-ttu-id="8c9e4-127">畫面名稱</span><span class="sxs-lookup"><span data-stu-id="8c9e4-127">Screen name</span></span> | <span data-ttu-id="8c9e4-128">說明</span><span class="sxs-lookup"><span data-stu-id="8c9e4-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="8c9e4-129">瀏覽器例外狀況</span><span class="sxs-lookup"><span data-stu-id="8c9e4-129">Browser exceptions</span></span> |<span data-ttu-id="8c9e4-130">無法攔截 hello 瀏覽器中擲回的例外狀況的計數。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="8c9e4-131">伺服器例外狀況</span><span class="sxs-lookup"><span data-stu-id="8c9e4-131">Server exceptions</span></span> |<span data-ttu-id="8c9e4-132">Hello 應用程式所擲回未處理的例外狀況的計數</span><span class="sxs-lookup"><span data-stu-id="8c9e4-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="8c9e4-133">用戶端處理時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-133">Client processing time</span></span> |<span data-ttu-id="8c9e4-134">Hello DOM 載入之前收到 hello 文件的最後一個位元組之間的時間。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="8c9e4-135">系統可能仍在處理非同步要求。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="8c9e4-136">頁面載入網路連線時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-136">Page load network connect time</span></span> |<span data-ttu-id="8c9e4-137">時間 hello 瀏覽器會 tooconnect toohello 網路。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="8c9e4-138">可為 0 (若已快取)。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="8c9e4-139">接收回應時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-139">Receiving response time</span></span> |<span data-ttu-id="8c9e4-140">瀏覽器傳送要求 toostarting tooreceive 回應之間的時間。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="8c9e4-141">傳送要求時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-141">Send request time</span></span> |<span data-ttu-id="8c9e4-142">瀏覽器 toosend 要求所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="8c9e4-143">瀏覽器頁面載入時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-143">Browser page load time</span></span> |<span data-ttu-id="8c9e4-144">從使用者要求直至載入 DOM、樣式表、指令碼和影像的經過時間。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="8c9e4-145">可用的記憶體</span><span class="sxs-lookup"><span data-stu-id="8c9e4-145">Available memory</span></span> |<span data-ttu-id="8c9e4-146">針對處理程序或系統用途的立即可用實體記憶體。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="8c9e4-147">處理程序 IO 速率</span><span class="sxs-lookup"><span data-stu-id="8c9e4-147">Process IO Rate</span></span> |<span data-ttu-id="8c9e4-148">每個第二個讀取和寫入的 toofiles、 網路和裝置的總位元組數。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="8c9e4-149">例外狀況比率</span><span class="sxs-lookup"><span data-stu-id="8c9e4-149">exception rate</span></span> |<span data-ttu-id="8c9e4-150">每秒擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="8c9e4-151">處理程序 CPU</span><span class="sxs-lookup"><span data-stu-id="8c9e4-151">Process CPU</span></span> |<span data-ttu-id="8c9e4-152">hello hello 處理器 tooexecution 指示用於 hello 應用程式處理序的所有處理序執行緒的經過時間百分比。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="8c9e4-153">處理器時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-153">Processor time</span></span> |<span data-ttu-id="8c9e4-154">花在非閒置執行緒的 hello 處理器時間的 hello 百分比。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="8c9e4-155">處理程序私人位元組</span><span class="sxs-lookup"><span data-stu-id="8c9e4-155">Process private bytes</span></span> |<span data-ttu-id="8c9e4-156">以獨佔方式指派 toohello 記憶體受監視應用程式的處理程序。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="8c9e4-157">ASP.NET 要求執行時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-157">ASP.NET request execution time</span></span> |<span data-ttu-id="8c9e4-158">Hello 最近的要求執行時間。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="8c9e4-159">執行佇列中的 ASP.NET 要求</span><span class="sxs-lookup"><span data-stu-id="8c9e4-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="8c9e4-160">Hello 應用程式要求佇列的長度。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="8c9e4-161">ASP.NET 要求率</span><span class="sxs-lookup"><span data-stu-id="8c9e4-161">ASP.NET request rate</span></span> |<span data-ttu-id="8c9e4-162">所有要求速率 toohello 應用程式每秒從 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="8c9e4-163">相依性失敗</span><span class="sxs-lookup"><span data-stu-id="8c9e4-163">Dependency failures</span></span> |<span data-ttu-id="8c9e4-164">Hello 伺服器應用程式 tooexternal 資源失敗呼叫計數。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="8c9e4-165">伺服器回應時間</span><span class="sxs-lookup"><span data-stu-id="8c9e4-165">Server response time</span></span> |<span data-ttu-id="8c9e4-166">接收 HTTP 要求到完成傳送 hello 回應之間的時間。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="8c9e4-167">要求率</span><span class="sxs-lookup"><span data-stu-id="8c9e4-167">Request rate</span></span> |<span data-ttu-id="8c9e4-168">所有要求 toohello 應用程式每秒的速率。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="8c9e4-169">失敗的要求</span><span class="sxs-lookup"><span data-stu-id="8c9e4-169">Failed requests</span></span> |<span data-ttu-id="8c9e4-170">產生回應碼的 HTTP 要求計數 >= 400</span><span class="sxs-lookup"><span data-stu-id="8c9e4-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="8c9e4-171">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="8c9e4-171">Page views</span></span> |<span data-ttu-id="8c9e4-172">網頁的用戶端使用者要求計數。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="8c9e4-173">系統會篩選掉綜合流量。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="8c9e4-174">{您的自訂度量名稱}</span><span class="sxs-lookup"><span data-stu-id="8c9e4-174">{your custom metric name}</span></span> |<span data-ttu-id="8c9e4-175">{您的度量名稱}</span><span class="sxs-lookup"><span data-stu-id="8c9e4-175">{Your metric name}</span></span> |<span data-ttu-id="8c9e4-176">所報告您公制值[TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric)或 hello[測量呼叫的參數來追蹤](app-insights-api-custom-events-metrics.md#properties)。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="8c9e4-177">hello 度量資訊會傳送不同遙測模組：</span><span class="sxs-lookup"><span data-stu-id="8c9e4-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="8c9e4-178">度量群組</span><span class="sxs-lookup"><span data-stu-id="8c9e4-178">Metric group</span></span> | <span data-ttu-id="8c9e4-179">收集器模組</span><span class="sxs-lookup"><span data-stu-id="8c9e4-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="8c9e4-180">basicExceptionBrowser、</span><span class="sxs-lookup"><span data-stu-id="8c9e4-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="8c9e4-181">clientPerformance、</span><span class="sxs-lookup"><span data-stu-id="8c9e4-181">clientPerformance,</span></span><br/><span data-ttu-id="8c9e4-182">view</span><span class="sxs-lookup"><span data-stu-id="8c9e4-182">view</span></span> |[<span data-ttu-id="8c9e4-183">瀏覽器 JavaScript</span><span class="sxs-lookup"><span data-stu-id="8c9e4-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="8c9e4-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="8c9e4-184">performanceCounter</span></span> |[<span data-ttu-id="8c9e4-185">效能</span><span class="sxs-lookup"><span data-stu-id="8c9e4-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="8c9e4-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="8c9e4-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="8c9e4-187">相依性</span><span class="sxs-lookup"><span data-stu-id="8c9e4-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="8c9e4-188">request、</span><span class="sxs-lookup"><span data-stu-id="8c9e4-188">request,</span></span><br/><span data-ttu-id="8c9e4-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="8c9e4-189">requestFailed</span></span> |[<span data-ttu-id="8c9e4-190">伺服器要求</span><span class="sxs-lookup"><span data-stu-id="8c9e4-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="8c9e4-191">Webhook</span><span class="sxs-lookup"><span data-stu-id="8c9e4-191">Webhooks</span></span>
<span data-ttu-id="8c9e4-192">您可以[自動化回應 tooan 警示](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="8c9e4-193">Azure 會在出現警示時呼叫您選擇的網址。</span><span class="sxs-lookup"><span data-stu-id="8c9e4-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="8c9e4-194">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8c9e4-194">See also</span></span>
* [<span data-ttu-id="8c9e4-195">指令碼 tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c9e4-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="8c9e4-196">從範本建立 Application Insights 和 Web 測試資源</span><span class="sxs-lookup"><span data-stu-id="8c9e4-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="8c9e4-197">自動化結合的 Microsoft Azure 診斷 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="8c9e4-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="8c9e4-198">自動化回應 tooan 警示</span><span class="sxs-lookup"><span data-stu-id="8c9e4-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
