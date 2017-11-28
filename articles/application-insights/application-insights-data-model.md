---
title: "aaaAzure 應用程式 Insights 遙測資料模型 |Microsoft 文件"
description: "Application Insights 資料模型概觀"
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
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a><span data-ttu-id="fe76d-103">Application Insights 遙測資料模型</span><span class="sxs-lookup"><span data-stu-id="fe76d-103">Application Insights telemetry data model</span></span>

<span data-ttu-id="fe76d-104">[Azure 的 Application Insights](app-insights-overview.md)傳送遙測從您的 web 應用程式 toohello Azure 入口網站，讓您可以分析 hello 效能和您的應用程式的使用方式。</span><span class="sxs-lookup"><span data-stu-id="fe76d-104">[Azure Application Insights](app-insights-overview.md) sends telemetry from your web application toohello Azure portal, so that you can analyze hello performance and usage of your application.</span></span> <span data-ttu-id="fe76d-105">hello 遙測模型已標準化，使其可能 toocreate 平台和語言無關的監視。</span><span class="sxs-lookup"><span data-stu-id="fe76d-105">hello telemetry model is standardized so that it is possible toocreate platform and language-independent monitoring.</span></span> 

<span data-ttu-id="fe76d-106">Application Insights 所收集的資料會建立一般應用程式執行模式的模型︰</span><span class="sxs-lookup"><span data-stu-id="fe76d-106">Data collected by Application Insights models this typical application execution pattern:</span></span>

![Application Insights 應用程式模型](./media/application-insights-data-model/application-insights-data-model.png)

<span data-ttu-id="fe76d-108">hello 下列類型的遙測資料會使用的 toomonitor hello 執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe76d-108">hello following types of telemetry are used toomonitor hello execution of your app.</span></span> <span data-ttu-id="fe76d-109">hello 下列三種類型通常會自動收集由 hello Application Insights SDK 從 hello web 應用程式架構：</span><span class="sxs-lookup"><span data-stu-id="fe76d-109">hello following three types are typically automatically collected by hello Application Insights SDK from hello web application framework:</span></span>

* <span data-ttu-id="fe76d-110">[**要求**](application-insights-data-model-request-telemetry.md) -產生 toolog 您應用程式所收到的要求。</span><span class="sxs-lookup"><span data-stu-id="fe76d-110">[**Request**](application-insights-data-model-request-telemetry.md) - Generated toolog a request received by your app.</span></span> <span data-ttu-id="fe76d-111">例如，hello Application Insights web SDK 會自動產生每個 web 應用程式接收的 HTTP 要求的要求遙測項的目。</span><span class="sxs-lookup"><span data-stu-id="fe76d-111">For example, hello Application Insights web SDK automatically generates a Request telemetry item for each HTTP request that your web app receives.</span></span> 

    <span data-ttu-id="fe76d-112">**作業**是 hello 執行執行緒的處理要求。</span><span class="sxs-lookup"><span data-stu-id="fe76d-112">An **Operation** is hello threads of execution that processes a request.</span></span> <span data-ttu-id="fe76d-113">您也可以[撰寫程式碼](app-insights-api-custom-events-metrics.md#trackrequest)toomonitor 其他類型的作業，例如 「 喚醒 」 中的 web 工作，或函式，會定期處理資料。</span><span class="sxs-lookup"><span data-stu-id="fe76d-113">You can also [write code](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor other types of operation, such as a "wake up" in a web job or function that periodically processes data.</span></span>  <span data-ttu-id="fe76d-114">每個作業都有識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe76d-114">Each operation has an ID.</span></span> <span data-ttu-id="fe76d-115">這個識別碼可能是使用的 too[group]((application-insights-correlation.md) 所有遙測都產生您的應用程式正在處理 hello 要求時。</span><span class="sxs-lookup"><span data-stu-id="fe76d-115">This ID that can be used too[group]((application-insights-correlation.md) all telemetry generated while your app is processing hello request.</span></span> <span data-ttu-id="fe76d-116">每個作業可能會成功或失敗，而且有持續時間。</span><span class="sxs-lookup"><span data-stu-id="fe76d-116">Each operation either succeeds or fails, and has a duration of time.</span></span>
* <span data-ttu-id="fe76d-117">[**例外狀況**](application-insights-data-model-exception-telemetry.md) -通常表示導致作業 toofail 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="fe76d-117">[**Exception**](application-insights-data-model-exception-telemetry.md) - Typically represents an exception that causes an operation toofail.</span></span>
* <span data-ttu-id="fe76d-118">[**相依性**](application-insights-data-model-dependency-telemetry.md) -代表呼叫從您的應用程式 tooan 外部服務或儲存體，例如 REST API 或 SQL。</span><span class="sxs-lookup"><span data-stu-id="fe76d-118">[**Dependency**](application-insights-data-model-dependency-telemetry.md) - Represents a call from your app tooan external service or storage such as a REST API or SQL.</span></span> <span data-ttu-id="fe76d-119">在 ASP.NET 中，所定義相依性呼叫 tooSQL `System.Data`。</span><span class="sxs-lookup"><span data-stu-id="fe76d-119">In ASP.NET, dependency calls tooSQL are defined by `System.Data`.</span></span> <span data-ttu-id="fe76d-120">呼叫 tooHTTP 端點會由`System.Net`。</span><span class="sxs-lookup"><span data-stu-id="fe76d-120">Calls tooHTTP endpoints are defined by `System.Net`.</span></span> 

<span data-ttu-id="fe76d-121">Application Insights 針對自訂遙測提供三種其他資料類型：</span><span class="sxs-lookup"><span data-stu-id="fe76d-121">Application Insights provides three additional data types for custom telemetry:</span></span>

* <span data-ttu-id="fe76d-122">[追蹤](application-insights-data-model-trace-telemetry.md)-請直接使用，或透過配接器 tooimplement 診斷記錄的使用是很熟悉 tooyou，例如 instrumentation framework`Log4Net`或`System.Diagnostics`。</span><span class="sxs-lookup"><span data-stu-id="fe76d-122">[Trace](application-insights-data-model-trace-telemetry.md) - used either directly, or through an adapter tooimplement diagnostics logging using an instrumentation framework that is familiar tooyou, such as `Log4Net` or `System.Diagnostics`.</span></span>
* <span data-ttu-id="fe76d-123">[事件](application-insights-data-model-event-telemetry.md)-通常是使用與您的服務 tooanalyze 習慣 toocapture 使用者互動。</span><span class="sxs-lookup"><span data-stu-id="fe76d-123">[Event](application-insights-data-model-event-telemetry.md) - typically used toocapture user interaction with your service, tooanalyze usage patterns.</span></span>
* <span data-ttu-id="fe76d-124">[公制](application-insights-data-model-metric-telemetry.md)-使用 tooreport 週期性的純量度量。</span><span class="sxs-lookup"><span data-stu-id="fe76d-124">[Metric](application-insights-data-model-metric-telemetry.md) - used tooreport periodic scalar measurements.</span></span>

<span data-ttu-id="fe76d-125">每個遙測項目可以定義 hello[內容資訊](application-insights-data-model-context.md)像應用程式版本或使用者工作階段識別碼。內容是一組在某些情況下會解除封鎖的強型別欄位。</span><span class="sxs-lookup"><span data-stu-id="fe76d-125">Every telemetry item can define hello [context information](application-insights-data-model-context.md) like application version or user session id. Context is a set of strongly typed fields that unblocks certain scenarios.</span></span> <span data-ttu-id="fe76d-126">正確初始化應用程式版本之後，Application Insights 可以偵測與重新部署相互關聯的應用程式行為中是否有新模式。</span><span class="sxs-lookup"><span data-stu-id="fe76d-126">When application version is properly initialized, Application Insights can detect new patterns in application behavior correlated with redeployment.</span></span> <span data-ttu-id="fe76d-127">工作階段識別碼可以是使用的 toocalculate hello 中斷或使用者問題影響。</span><span class="sxs-lookup"><span data-stu-id="fe76d-127">Session id can be used toocalculate hello outage or an issue impact on users.</span></span> <span data-ttu-id="fe76d-128">計算特定失敗相依性、錯誤追蹤或重大例外狀況之工作階段識別碼值的相異計數，即可充分了解影響。</span><span class="sxs-lookup"><span data-stu-id="fe76d-128">Calculating distinct count of session id values for certain failed dependency, error trace or critical exception gives a good understanding of an impact.</span></span>

<span data-ttu-id="fe76d-129">Application Insights 遙測模型定義的方式太[相互關聯](application-insights-correlation.md)遙測 toohello 作業，它是在其中一部分。</span><span class="sxs-lookup"><span data-stu-id="fe76d-129">Application Insights telemetry model defines a way too[correlate](application-insights-correlation.md) telemetry toohello operation of which it’s a part.</span></span> <span data-ttu-id="fe76d-130">例如，要求會發出 SQL Database 呼叫，並記錄診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="fe76d-130">For example, a request can make a SQL Database calls and recorded diagnostics info.</span></span> <span data-ttu-id="fe76d-131">您可以設定遙測項目，將它連接後 toohello 要求遙測 hello 相互關聯內容。</span><span class="sxs-lookup"><span data-stu-id="fe76d-131">You can set hello correlation context for those telemetry items that tie it back toohello request telemetry.</span></span>

## <a name="schema-improvements"></a><span data-ttu-id="fe76d-132">結構描述的增強功能</span><span class="sxs-lookup"><span data-stu-id="fe76d-132">Schema improvements</span></span>

<span data-ttu-id="fe76d-133">應用程式的 Insights 資料模型是簡單和基本但功能強大的方式 toomodel 您應用程式遙測。</span><span class="sxs-lookup"><span data-stu-id="fe76d-133">Application Insights data model is a simple and basic yet powerful way toomodel your application telemetry.</span></span> <span data-ttu-id="fe76d-134">我們致力於 tookeep hello 模型簡單和輕薄 toosupport 重要案例，並允許 tooextend hello 結構描述，供進階使用。</span><span class="sxs-lookup"><span data-stu-id="fe76d-134">We strive tookeep hello model simple and slim toosupport essential scenarios and allow tooextend hello schema for advanced use.</span></span>

<span data-ttu-id="fe76d-135">tooreport 資料模型或結構描述問題，以及建議使用 GitHub [ApplicationInsights 首頁](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema)儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fe76d-135">tooreport data model or schema problems and suggestions use GitHub [ApplicationInsights-Home](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe76d-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe76d-136">Next steps</span></span>

- [<span data-ttu-id="fe76d-137">撰寫自訂遙測</span><span class="sxs-lookup"><span data-stu-id="fe76d-137">Write custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)
- <span data-ttu-id="fe76d-138">了解如何太[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="fe76d-138">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="fe76d-139">使用[取樣](app-insights-sampling.md)的遙測的 toominimize 數量取決於資料模型。</span><span class="sxs-lookup"><span data-stu-id="fe76d-139">Use [sampling](app-insights-sampling.md) toominimize amount of telemetry based on data model.</span></span>
- <span data-ttu-id="fe76d-140">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="fe76d-140">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
