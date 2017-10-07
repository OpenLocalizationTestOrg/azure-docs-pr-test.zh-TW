---
title: "aaaAzure 應用程式 Insights 遙測資料模型的度量遙測 |Microsoft 文件"
description: "計量遙測的 Application Insights 資料模型"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="962d1-103">計量遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="962d1-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="962d1-104">[Application Insights](app-insights-overview.md) 支援兩種類型的計量遙測：單一測量和預先彙總的計量。</span><span class="sxs-lookup"><span data-stu-id="962d1-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="962d1-105">單一度量只有名稱與值。</span><span class="sxs-lookup"><span data-stu-id="962d1-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="962d1-106">預先彙總的度量會指定在 hello 彙總間隔和它的標準差 hello 標準最小和最大值。</span><span class="sxs-lookup"><span data-stu-id="962d1-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="962d1-107">預先彙總的計量遙測會假設該彙總期間為一分鐘。</span><span class="sxs-lookup"><span data-stu-id="962d1-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="962d1-108">Application Insights 支援數個已知的計量名稱。</span><span class="sxs-lookup"><span data-stu-id="962d1-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="962d1-109">代表系統和程序計數器的計量︰</span><span class="sxs-lookup"><span data-stu-id="962d1-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="962d1-110">**.NET 名稱**</span><span class="sxs-lookup"><span data-stu-id="962d1-110">**.NET name**</span></span>             | <span data-ttu-id="962d1-111">**平台無從驗證的名稱**</span><span class="sxs-lookup"><span data-stu-id="962d1-111">**Platform agnostic name**</span></span> | <span data-ttu-id="962d1-112">**REST API 名稱**</span><span class="sxs-lookup"><span data-stu-id="962d1-112">**REST API name**</span></span> | <span data-ttu-id="962d1-113">**說明**</span><span class="sxs-lookup"><span data-stu-id="962d1-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="962d1-114">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-114">Work in progress...</span></span> | [<span data-ttu-id="962d1-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="962d1-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="962d1-116">電腦 CPU 總數</span><span class="sxs-lookup"><span data-stu-id="962d1-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="962d1-117">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-117">Work in progress...</span></span> | [<span data-ttu-id="962d1-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="962d1-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="962d1-119">磁碟上可用的記憶體</span><span class="sxs-lookup"><span data-stu-id="962d1-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="962d1-120">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-120">Work in progress...</span></span> | [<span data-ttu-id="962d1-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="962d1-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="962d1-122">Hello 裝載 hello 應用程式的處理程序的 CPU</span><span class="sxs-lookup"><span data-stu-id="962d1-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="962d1-123">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-123">Work in progress...</span></span> | [<span data-ttu-id="962d1-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="962d1-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="962d1-125">hello 裝載 hello 應用程式的處理程序所使用的記憶體</span><span class="sxs-lookup"><span data-stu-id="962d1-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="962d1-126">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-126">Work in progress...</span></span> | [<span data-ttu-id="962d1-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="962d1-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="962d1-128">裝載 hello 應用程式的處理序所執行的 I/O 作業速率</span><span class="sxs-lookup"><span data-stu-id="962d1-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="962d1-129">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-129">Work in progress...</span></span> | [<span data-ttu-id="962d1-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="962d1-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="962d1-131">應用程式處理要求的速率</span><span class="sxs-lookup"><span data-stu-id="962d1-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="962d1-132">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-132">Work in progress...</span></span> | [<span data-ttu-id="962d1-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="962d1-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="962d1-134">應用程式擲回例外狀況的速率</span><span class="sxs-lookup"><span data-stu-id="962d1-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="962d1-135">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-135">Work in progress...</span></span> | [<span data-ttu-id="962d1-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="962d1-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="962d1-137">平均要求執行時間</span><span class="sxs-lookup"><span data-stu-id="962d1-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="962d1-138">進行中...</span><span class="sxs-lookup"><span data-stu-id="962d1-138">Work in progress...</span></span> | [<span data-ttu-id="962d1-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="962d1-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="962d1-140">等候處理佇列中的 hello 的要求數目</span><span class="sxs-lookup"><span data-stu-id="962d1-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="962d1-141">名稱</span><span class="sxs-lookup"><span data-stu-id="962d1-141">Name</span></span>

<span data-ttu-id="962d1-142">名稱的 hello 度量您想要在 Application Insights 入口網站和 UI 中的 toosee。</span><span class="sxs-lookup"><span data-stu-id="962d1-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="962d1-143">值</span><span class="sxs-lookup"><span data-stu-id="962d1-143">Value</span></span>

<span data-ttu-id="962d1-144">度量的單一值。</span><span class="sxs-lookup"><span data-stu-id="962d1-144">Single value for measurement.</span></span> <span data-ttu-id="962d1-145">Hello 彙總的個別度量值的總和。</span><span class="sxs-lookup"><span data-stu-id="962d1-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="962d1-146">Count</span><span class="sxs-lookup"><span data-stu-id="962d1-146">Count</span></span>

<span data-ttu-id="962d1-147">衡量標準權數 hello 的彙總度量。</span><span class="sxs-lookup"><span data-stu-id="962d1-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="962d1-148">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="962d1-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="962d1-149">Min</span><span class="sxs-lookup"><span data-stu-id="962d1-149">Min</span></span>

<span data-ttu-id="962d1-150">Hello 彙總的度量最小值。</span><span class="sxs-lookup"><span data-stu-id="962d1-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="962d1-151">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="962d1-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="962d1-152">max</span><span class="sxs-lookup"><span data-stu-id="962d1-152">Max</span></span>

<span data-ttu-id="962d1-153">彙總的 hello 標準的最大值。</span><span class="sxs-lookup"><span data-stu-id="962d1-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="962d1-154">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="962d1-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="962d1-155">標準差</span><span class="sxs-lookup"><span data-stu-id="962d1-155">Standard deviation</span></span>

<span data-ttu-id="962d1-156">彙總的 hello 標準的標準差。</span><span class="sxs-lookup"><span data-stu-id="962d1-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="962d1-157">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="962d1-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="962d1-158">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="962d1-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="962d1-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="962d1-159">Next steps</span></span>

- <span data-ttu-id="962d1-160">深入了解如何 toouse[應用程式的自訂事件和度量的 Insights API](app-insights-api-custom-events-metrics.md#trackmetric)。</span><span class="sxs-lookup"><span data-stu-id="962d1-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="962d1-161">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="962d1-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="962d1-162">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="962d1-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
