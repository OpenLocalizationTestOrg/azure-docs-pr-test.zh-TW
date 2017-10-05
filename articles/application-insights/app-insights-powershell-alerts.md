---
title: "在 Application Insights 中使用 PowerShell 設定警示 | Microsoft Docs"
description: "自動化 Application Insights 的組態以取得有關度量變更的電子郵件。"
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
ms.openlocfilehash: 64675c51abf80daa3a55220f910aa8fdee1042ca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="cbf8a-103">在 Application Insights 中使用 PowerShell 設定警示</span><span class="sxs-lookup"><span data-stu-id="cbf8a-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="cbf8a-104">您可以在 [Application Insights](app-insights-overview.md) 中自動設定[警示](app-insights-alerts.md)的組態。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="cbf8a-105">此外，您可以[設定 webhook 以自動回應至警示](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cbf8a-106">如果您想要同時建立資源和警示，請考慮[使用 Azure Resource Manager 範本](app-insights-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="cbf8a-107">單次設定</span><span class="sxs-lookup"><span data-stu-id="cbf8a-107">One-time setup</span></span>
<span data-ttu-id="cbf8a-108">若您未曾將 PowerShell 與 Azure 訂用帳戶搭配使用：</span><span class="sxs-lookup"><span data-stu-id="cbf8a-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="cbf8a-109">在您要執行指令碼的電腦上，安裝 Azure Powershell 模組。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="cbf8a-110">安裝 [Microsoft Web Platform Installer (v5 或更高版本)](http://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="cbf8a-111">使用該程式安裝 Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbf8a-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="cbf8a-112">連接到 Azure</span><span class="sxs-lookup"><span data-stu-id="cbf8a-112">Connect to Azure</span></span>
<span data-ttu-id="cbf8a-113">啟動 Azure PowerShell 並 [連接至您的訂用帳戶](/powershell/azure/overview)：</span><span class="sxs-lookup"><span data-stu-id="cbf8a-113">Start Azure PowerShell and [connect to your subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="cbf8a-114">取得警示</span><span class="sxs-lookup"><span data-stu-id="cbf8a-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="cbf8a-115">Add alert</span><span class="sxs-lookup"><span data-stu-id="cbf8a-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="cbf8a-116">範例 1</span><span class="sxs-lookup"><span data-stu-id="cbf8a-116">Example 1</span></span>
<span data-ttu-id="cbf8a-117">若伺服器針對 HTTP 要求的回應時間 (平均超過 5 分鐘) 慢於 1 秒，則傳送電子郵件給我。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="cbf8a-118">我的 Application Insights 資源稱為 IceCreamWebApp，其位於 Fabrikam 資源群組。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="cbf8a-119">我是 Azure 訂用帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="cbf8a-120">GUID 是該訂用帳戶的 ID (而非應用程式的檢測金鑰)。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="cbf8a-121">範例 2</span><span class="sxs-lookup"><span data-stu-id="cbf8a-121">Example 2</span></span>
<span data-ttu-id="cbf8a-122">我已有應用程式，並在其中使用 [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) 來報告名為 "salesPerHour" 的度量。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="cbf8a-123">若 salesPerHour 超過 24 小時皆低於平均值 100，則傳送電子郵件給我的同事。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="cbf8a-124">您亦可針對使用其他追蹤呼叫之 [測量參數](app-insights-api-custom-events-metrics.md#properties) (例如 TrackEvent 或 trackPageView) 報告的度量，使用相同的規則。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="cbf8a-125">度量名稱</span><span class="sxs-lookup"><span data-stu-id="cbf8a-125">Metric names</span></span>
| <span data-ttu-id="cbf8a-126">度量名稱</span><span class="sxs-lookup"><span data-stu-id="cbf8a-126">Metric name</span></span> | <span data-ttu-id="cbf8a-127">畫面名稱</span><span class="sxs-lookup"><span data-stu-id="cbf8a-127">Screen name</span></span> | <span data-ttu-id="cbf8a-128">說明</span><span class="sxs-lookup"><span data-stu-id="cbf8a-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="cbf8a-129">瀏覽器例外狀況</span><span class="sxs-lookup"><span data-stu-id="cbf8a-129">Browser exceptions</span></span> |<span data-ttu-id="cbf8a-130">在瀏覽器中擲回的未攔截例外狀況計數。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="cbf8a-131">伺服器例外狀況</span><span class="sxs-lookup"><span data-stu-id="cbf8a-131">Server exceptions</span></span> |<span data-ttu-id="cbf8a-132">應用程式擲回的未處理例外狀況計數</span><span class="sxs-lookup"><span data-stu-id="cbf8a-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="cbf8a-133">用戶端處理時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-133">Client processing time</span></span> |<span data-ttu-id="cbf8a-134">從接收上個文件位元組直至載入 DOM 的經過時間。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="cbf8a-135">系統可能仍在處理非同步要求。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="cbf8a-136">頁面載入網路連線時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-136">Page load network connect time</span></span> |<span data-ttu-id="cbf8a-137">瀏覽器連線至網路所需的時間。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="cbf8a-138">可為 0 (若已快取)。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="cbf8a-139">接收回應時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-139">Receiving response time</span></span> |<span data-ttu-id="cbf8a-140">瀏覽器傳送要求直至開始接收回應的經過時間。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="cbf8a-141">傳送要求時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-141">Send request time</span></span> |<span data-ttu-id="cbf8a-142">瀏覽器傳送要求所耗費的時間。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="cbf8a-143">瀏覽器頁面載入時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-143">Browser page load time</span></span> |<span data-ttu-id="cbf8a-144">從使用者要求直至載入 DOM、樣式表、指令碼和影像的經過時間。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="cbf8a-145">可用的記憶體</span><span class="sxs-lookup"><span data-stu-id="cbf8a-145">Available memory</span></span> |<span data-ttu-id="cbf8a-146">針對處理程序或系統用途的立即可用實體記憶體。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="cbf8a-147">處理程序 IO 速率</span><span class="sxs-lookup"><span data-stu-id="cbf8a-147">Process IO Rate</span></span> |<span data-ttu-id="cbf8a-148">每秒讀取與寫入檔案、 網路和裝置的總位元組數。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="cbf8a-149">例外狀況比率</span><span class="sxs-lookup"><span data-stu-id="cbf8a-149">exception rate</span></span> |<span data-ttu-id="cbf8a-150">每秒擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="cbf8a-151">處理程序 CPU</span><span class="sxs-lookup"><span data-stu-id="cbf8a-151">Process CPU</span></span> |<span data-ttu-id="cbf8a-152">處理器針對應用程式處理程序執行指示，所用之全部處理程序執行緒的經過時間百分比。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="cbf8a-153">處理器時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-153">Processor time</span></span> |<span data-ttu-id="cbf8a-154">處理器針對非閒置執行緒所耗費時間的百分比。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="cbf8a-155">處理程序私人位元組</span><span class="sxs-lookup"><span data-stu-id="cbf8a-155">Process private bytes</span></span> |<span data-ttu-id="cbf8a-156">以獨佔方式指派至監視應用程式處理程序的記憶體。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="cbf8a-157">ASP.NET 要求執行時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-157">ASP.NET request execution time</span></span> |<span data-ttu-id="cbf8a-158">最近要求的執行時間。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="cbf8a-159">執行佇列中的 ASP.NET 要求</span><span class="sxs-lookup"><span data-stu-id="cbf8a-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="cbf8a-160">應用程式要求佇列的長度。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="cbf8a-161">ASP.NET 要求率</span><span class="sxs-lookup"><span data-stu-id="cbf8a-161">ASP.NET request rate</span></span> |<span data-ttu-id="cbf8a-162">每秒從 ASP.NET 發出所有應用程式要求的速率。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="cbf8a-163">相依性失敗</span><span class="sxs-lookup"><span data-stu-id="cbf8a-163">Dependency failures</span></span> |<span data-ttu-id="cbf8a-164">伺服器應用程式針對外部資源的呼叫失敗計數。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="cbf8a-165">伺服器回應時間</span><span class="sxs-lookup"><span data-stu-id="cbf8a-165">Server response time</span></span> |<span data-ttu-id="cbf8a-166">從接收 HTTP 要求直至完成傳送回應的經過時間。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="cbf8a-167">要求率</span><span class="sxs-lookup"><span data-stu-id="cbf8a-167">Request rate</span></span> |<span data-ttu-id="cbf8a-168">每秒發出所有應用程式要求的速率。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="cbf8a-169">失敗的要求</span><span class="sxs-lookup"><span data-stu-id="cbf8a-169">Failed requests</span></span> |<span data-ttu-id="cbf8a-170">產生回應碼的 HTTP 要求計數 >= 400</span><span class="sxs-lookup"><span data-stu-id="cbf8a-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="cbf8a-171">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="cbf8a-171">Page views</span></span> |<span data-ttu-id="cbf8a-172">網頁的用戶端使用者要求計數。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="cbf8a-173">系統會篩選掉綜合流量。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="cbf8a-174">{您的自訂度量名稱}</span><span class="sxs-lookup"><span data-stu-id="cbf8a-174">{your custom metric name}</span></span> |<span data-ttu-id="cbf8a-175">{您的度量名稱}</span><span class="sxs-lookup"><span data-stu-id="cbf8a-175">{Your metric name}</span></span> |<span data-ttu-id="cbf8a-176">由 [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) 或[追蹤呼叫之測量參數](app-insights-api-custom-events-metrics.md#properties)所報告的度量值。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="cbf8a-177">此度量由不同遙測模組所傳送：</span><span class="sxs-lookup"><span data-stu-id="cbf8a-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="cbf8a-178">度量群組</span><span class="sxs-lookup"><span data-stu-id="cbf8a-178">Metric group</span></span> | <span data-ttu-id="cbf8a-179">收集器模組</span><span class="sxs-lookup"><span data-stu-id="cbf8a-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="cbf8a-180">basicExceptionBrowser、</span><span class="sxs-lookup"><span data-stu-id="cbf8a-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="cbf8a-181">clientPerformance、</span><span class="sxs-lookup"><span data-stu-id="cbf8a-181">clientPerformance,</span></span><br/><span data-ttu-id="cbf8a-182">view</span><span class="sxs-lookup"><span data-stu-id="cbf8a-182">view</span></span> |[<span data-ttu-id="cbf8a-183">瀏覽器 JavaScript</span><span class="sxs-lookup"><span data-stu-id="cbf8a-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="cbf8a-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="cbf8a-184">performanceCounter</span></span> |[<span data-ttu-id="cbf8a-185">效能</span><span class="sxs-lookup"><span data-stu-id="cbf8a-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="cbf8a-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="cbf8a-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="cbf8a-187">相依性</span><span class="sxs-lookup"><span data-stu-id="cbf8a-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="cbf8a-188">request、</span><span class="sxs-lookup"><span data-stu-id="cbf8a-188">request,</span></span><br/><span data-ttu-id="cbf8a-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="cbf8a-189">requestFailed</span></span> |[<span data-ttu-id="cbf8a-190">伺服器要求</span><span class="sxs-lookup"><span data-stu-id="cbf8a-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="cbf8a-191">Webhook</span><span class="sxs-lookup"><span data-stu-id="cbf8a-191">Webhooks</span></span>
<span data-ttu-id="cbf8a-192">您可以[自動回應至警示](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="cbf8a-193">Azure 會在出現警示時呼叫您選擇的網址。</span><span class="sxs-lookup"><span data-stu-id="cbf8a-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="cbf8a-194">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cbf8a-194">See also</span></span>
* [<span data-ttu-id="cbf8a-195">用來設定 Application Insights 的指令碼</span><span class="sxs-lookup"><span data-stu-id="cbf8a-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="cbf8a-196">從範本建立 Application Insights 和 Web 測試資源</span><span class="sxs-lookup"><span data-stu-id="cbf8a-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="cbf8a-197">自動化 Microsoft Azure 診斷與 Application Insights 的耦合</span><span class="sxs-lookup"><span data-stu-id="cbf8a-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="cbf8a-198">自動回應至警示</span><span class="sxs-lookup"><span data-stu-id="cbf8a-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
