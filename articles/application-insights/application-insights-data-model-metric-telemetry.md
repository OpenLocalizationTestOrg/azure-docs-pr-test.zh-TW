---
title: "Azure Application Insights 遙測資料模型 - 計量遙測 | Microsoft Docs"
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
ms.openlocfilehash: 42e55db4f932de85ee1a71c408b889e0ff9fe3e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="48b9c-103">計量遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="48b9c-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="48b9c-104">[Application Insights](app-insights-overview.md) 支援兩種類型的計量遙測：單一測量和預先彙總的計量。</span><span class="sxs-lookup"><span data-stu-id="48b9c-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="48b9c-105">單一度量只有名稱與值。</span><span class="sxs-lookup"><span data-stu-id="48b9c-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="48b9c-106">預先彙總的計量會指定彙總間隔中計量的最小值和最大值以及它的標準差。</span><span class="sxs-lookup"><span data-stu-id="48b9c-106">Pre-aggregated metric specifies minimum and maximum value of the metric in the aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="48b9c-107">預先彙總的計量遙測會假設該彙總期間為一分鐘。</span><span class="sxs-lookup"><span data-stu-id="48b9c-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="48b9c-108">Application Insights 支援數個已知的計量名稱。</span><span class="sxs-lookup"><span data-stu-id="48b9c-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="48b9c-109">代表系統和程序計數器的計量︰</span><span class="sxs-lookup"><span data-stu-id="48b9c-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="48b9c-110">**.NET 名稱**</span><span class="sxs-lookup"><span data-stu-id="48b9c-110">**.NET name**</span></span>             | <span data-ttu-id="48b9c-111">**平台無從驗證的名稱**</span><span class="sxs-lookup"><span data-stu-id="48b9c-111">**Platform agnostic name**</span></span> | <span data-ttu-id="48b9c-112">**REST API 名稱**</span><span class="sxs-lookup"><span data-stu-id="48b9c-112">**REST API name**</span></span> | <span data-ttu-id="48b9c-113">**說明**</span><span class="sxs-lookup"><span data-stu-id="48b9c-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="48b9c-114">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-114">Work in progress...</span></span> | [<span data-ttu-id="48b9c-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="48b9c-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="48b9c-116">電腦 CPU 總數</span><span class="sxs-lookup"><span data-stu-id="48b9c-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="48b9c-117">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-117">Work in progress...</span></span> | [<span data-ttu-id="48b9c-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="48b9c-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="48b9c-119">磁碟上可用的記憶體</span><span class="sxs-lookup"><span data-stu-id="48b9c-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="48b9c-120">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-120">Work in progress...</span></span> | [<span data-ttu-id="48b9c-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="48b9c-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="48b9c-122">裝載應用程式之處理序的 CPU</span><span class="sxs-lookup"><span data-stu-id="48b9c-122">CPU of the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="48b9c-123">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-123">Work in progress...</span></span> | [<span data-ttu-id="48b9c-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="48b9c-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="48b9c-125">裝載應用程式之處理序所使用的記憶體</span><span class="sxs-lookup"><span data-stu-id="48b9c-125">memory used by the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="48b9c-126">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-126">Work in progress...</span></span> | [<span data-ttu-id="48b9c-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="48b9c-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="48b9c-128">裝載應用程式之處理序執行的 I/O 作業速率</span><span class="sxs-lookup"><span data-stu-id="48b9c-128">rate of I/O operations runs by process hosting the application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="48b9c-129">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-129">Work in progress...</span></span> | [<span data-ttu-id="48b9c-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="48b9c-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="48b9c-131">應用程式處理要求的速率</span><span class="sxs-lookup"><span data-stu-id="48b9c-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="48b9c-132">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-132">Work in progress...</span></span> | [<span data-ttu-id="48b9c-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="48b9c-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="48b9c-134">應用程式擲回例外狀況的速率</span><span class="sxs-lookup"><span data-stu-id="48b9c-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="48b9c-135">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-135">Work in progress...</span></span> | [<span data-ttu-id="48b9c-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="48b9c-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="48b9c-137">平均要求執行時間</span><span class="sxs-lookup"><span data-stu-id="48b9c-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="48b9c-138">進行中...</span><span class="sxs-lookup"><span data-stu-id="48b9c-138">Work in progress...</span></span> | [<span data-ttu-id="48b9c-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="48b9c-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="48b9c-140">佇列中等候處理的要求數目</span><span class="sxs-lookup"><span data-stu-id="48b9c-140">number of requests waiting for the processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="48b9c-141">名稱</span><span class="sxs-lookup"><span data-stu-id="48b9c-141">Name</span></span>

<span data-ttu-id="48b9c-142">您想要在 Application Insights 入口網站和 UI 中看到的計量名稱。</span><span class="sxs-lookup"><span data-stu-id="48b9c-142">Name of the metric you'd like to see in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="48b9c-143">值</span><span class="sxs-lookup"><span data-stu-id="48b9c-143">Value</span></span>

<span data-ttu-id="48b9c-144">度量的單一值。</span><span class="sxs-lookup"><span data-stu-id="48b9c-144">Single value for measurement.</span></span> <span data-ttu-id="48b9c-145">個別彙總度量的總和。</span><span class="sxs-lookup"><span data-stu-id="48b9c-145">Sum of individual measurements for the aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="48b9c-146">Count</span><span class="sxs-lookup"><span data-stu-id="48b9c-146">Count</span></span>

<span data-ttu-id="48b9c-147">彙總計量的計量權數。</span><span class="sxs-lookup"><span data-stu-id="48b9c-147">Metric weight of the aggregated metric.</span></span> <span data-ttu-id="48b9c-148">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="48b9c-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="48b9c-149">Min</span><span class="sxs-lookup"><span data-stu-id="48b9c-149">Min</span></span>

<span data-ttu-id="48b9c-150">彙總計量的最小值。</span><span class="sxs-lookup"><span data-stu-id="48b9c-150">Minimum value of the aggregated metric.</span></span> <span data-ttu-id="48b9c-151">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="48b9c-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="48b9c-152">max</span><span class="sxs-lookup"><span data-stu-id="48b9c-152">Max</span></span>

<span data-ttu-id="48b9c-153">彙總計量的最大值。</span><span class="sxs-lookup"><span data-stu-id="48b9c-153">Maximum value of the aggregated metric.</span></span> <span data-ttu-id="48b9c-154">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="48b9c-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="48b9c-155">標準差</span><span class="sxs-lookup"><span data-stu-id="48b9c-155">Standard deviation</span></span>

<span data-ttu-id="48b9c-156">彙總計量的標準差。</span><span class="sxs-lookup"><span data-stu-id="48b9c-156">Standard deviation of the aggregated metric.</span></span> <span data-ttu-id="48b9c-157">不應該為度量設定。</span><span class="sxs-lookup"><span data-stu-id="48b9c-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="48b9c-158">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="48b9c-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="48b9c-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48b9c-159">Next steps</span></span>

- <span data-ttu-id="48b9c-160">了解如何使用[自訂事件和計量的 Application Insights API](app-insights-api-custom-events-metrics.md#trackmetric)。</span><span class="sxs-lookup"><span data-stu-id="48b9c-160">Learn how to use [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="48b9c-161">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="48b9c-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="48b9c-162">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="48b9c-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
