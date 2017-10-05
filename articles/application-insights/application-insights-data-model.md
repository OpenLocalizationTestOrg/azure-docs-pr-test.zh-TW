---
title: "Azure Application Insights 遙測資料模型 | Microsoft Docs"
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
ms.openlocfilehash: 6bcd30497622b01d4cd50bf7bbefebd4f00816b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-telemetry-data-model"></a><span data-ttu-id="53b2f-103">Application Insights 遙測資料模型</span><span class="sxs-lookup"><span data-stu-id="53b2f-103">Application Insights telemetry data model</span></span>

<span data-ttu-id="53b2f-104">[Azure Application Insights](app-insights-overview.md) 會將遙測從您的 Web 應用程式傳送到 Azure 入口網站，以便您可以分析應用程式的效能和使用量。</span><span class="sxs-lookup"><span data-stu-id="53b2f-104">[Azure Application Insights](app-insights-overview.md) sends telemetry from your web application to the Azure portal, so that you can analyze the performance and usage of your application.</span></span> <span data-ttu-id="53b2f-105">遙測模型已經過標準化，如此就可以建立平台與無關語言的監視。</span><span class="sxs-lookup"><span data-stu-id="53b2f-105">The telemetry model is standardized so that it is possible to create platform and language-independent monitoring.</span></span> 

<span data-ttu-id="53b2f-106">Application Insights 所收集的資料會建立一般應用程式執行模式的模型︰</span><span class="sxs-lookup"><span data-stu-id="53b2f-106">Data collected by Application Insights models this typical application execution pattern:</span></span>

![Application Insights 應用程式模型](./media/application-insights-data-model/application-insights-data-model.png)

<span data-ttu-id="53b2f-108">下列遙測類型可用來監視您應用程式的執行。</span><span class="sxs-lookup"><span data-stu-id="53b2f-108">The following types of telemetry are used to monitor the execution of your app.</span></span> <span data-ttu-id="53b2f-109">Application Insights SDK 通常會從 Web 應用程式架構自動收集下列三種類型：</span><span class="sxs-lookup"><span data-stu-id="53b2f-109">The following three types are typically automatically collected by the Application Insights SDK from the web application framework:</span></span>

* <span data-ttu-id="53b2f-110">[**要求**](application-insights-data-model-request-telemetry.md)：產生以記錄應用程式所接收的要求。</span><span class="sxs-lookup"><span data-stu-id="53b2f-110">[**Request**](application-insights-data-model-request-telemetry.md) - Generated to log a request received by your app.</span></span> <span data-ttu-id="53b2f-111">例如，Application Insights Web SDK 會針對您 Web 應用程式接收的每個 HTTP 要求產生「要求」遙測項目。</span><span class="sxs-lookup"><span data-stu-id="53b2f-111">For example, the Application Insights web SDK automatically generates a Request telemetry item for each HTTP request that your web app receives.</span></span> 

    <span data-ttu-id="53b2f-112">**作業**是處理要求的執行緒。</span><span class="sxs-lookup"><span data-stu-id="53b2f-112">An **Operation** is the threads of execution that processes a request.</span></span> <span data-ttu-id="53b2f-113">您也可以[撰寫程式碼](app-insights-api-custom-events-metrics.md#trackrequest)來監視其他作業類型，例如，定期處理資料之 Web 工作或函式中的「喚醒」。</span><span class="sxs-lookup"><span data-stu-id="53b2f-113">You can also [write code](app-insights-api-custom-events-metrics.md#trackrequest) to monitor other types of operation, such as a "wake up" in a web job or function that periodically processes data.</span></span>  <span data-ttu-id="53b2f-114">每個作業都有識別碼。</span><span class="sxs-lookup"><span data-stu-id="53b2f-114">Each operation has an ID.</span></span> <span data-ttu-id="53b2f-115">此識別碼可用來將應用程式處理要求時產生的所有遙測加以 [分組] \(application-insights-correlation.md)。</span><span class="sxs-lookup"><span data-stu-id="53b2f-115">This ID that can be used to [group]((application-insights-correlation.md) all telemetry generated while your app is processing the request.</span></span> <span data-ttu-id="53b2f-116">每個作業可能會成功或失敗，而且有持續時間。</span><span class="sxs-lookup"><span data-stu-id="53b2f-116">Each operation either succeeds or fails, and has a duration of time.</span></span>
* <span data-ttu-id="53b2f-117">[**例外狀況**](application-insights-data-model-exception-telemetry.md)：通常表示造成作業失敗的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="53b2f-117">[**Exception**](application-insights-data-model-exception-telemetry.md) - Typically represents an exception that causes an operation to fail.</span></span>
* <span data-ttu-id="53b2f-118">[**相依性**](application-insights-data-model-dependency-telemetry.md)：代表從您的應用程式對外部服務或儲存體的呼叫，例如 REST API 或 SQL。</span><span class="sxs-lookup"><span data-stu-id="53b2f-118">[**Dependency**](application-insights-data-model-dependency-telemetry.md) - Represents a call from your app to an external service or storage such as a REST API or SQL.</span></span> <span data-ttu-id="53b2f-119">在 ASP.NET 中，SQL 的相依性呼叫是由 `System.Data` 所定義。</span><span class="sxs-lookup"><span data-stu-id="53b2f-119">In ASP.NET, dependency calls to SQL are defined by `System.Data`.</span></span> <span data-ttu-id="53b2f-120">HTTP 端點的呼叫是由 `System.Net` 所定義。</span><span class="sxs-lookup"><span data-stu-id="53b2f-120">Calls to HTTP endpoints are defined by `System.Net`.</span></span> 

<span data-ttu-id="53b2f-121">Application Insights 針對自訂遙測提供三種其他資料類型：</span><span class="sxs-lookup"><span data-stu-id="53b2f-121">Application Insights provides three additional data types for custom telemetry:</span></span>

* <span data-ttu-id="53b2f-122">[追蹤](application-insights-data-model-trace-telemetry.md)：可直接使用或透過配接器，以您所熟悉的檢測架構 (例如 `Log4Net` 或 `System.Diagnostics`) 來實作診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="53b2f-122">[Trace](application-insights-data-model-trace-telemetry.md) - used either directly, or through an adapter to implement diagnostics logging using an instrumentation framework that is familiar to you, such as `Log4Net` or `System.Diagnostics`.</span></span>
* <span data-ttu-id="53b2f-123">[事件](application-insights-data-model-event-telemetry.md)：通常用於擷取使用者與您服務的互動，藉以分析使用模式。</span><span class="sxs-lookup"><span data-stu-id="53b2f-123">[Event](application-insights-data-model-event-telemetry.md) - typically used to capture user interaction with your service, to analyze usage patterns.</span></span>
* <span data-ttu-id="53b2f-124">[計量](application-insights-data-model-metric-telemetry.md)：用於報告定期的純量測量。</span><span class="sxs-lookup"><span data-stu-id="53b2f-124">[Metric](application-insights-data-model-metric-telemetry.md) - used to report periodic scalar measurements.</span></span>

<span data-ttu-id="53b2f-125">每個遙測項目可以定義[內容資訊](application-insights-data-model-context.md)，例如應用程式版本或使用者工作階段識別碼。內容是一組在某些情況下會解除封鎖的強型別欄位。</span><span class="sxs-lookup"><span data-stu-id="53b2f-125">Every telemetry item can define the [context information](application-insights-data-model-context.md) like application version or user session id. Context is a set of strongly typed fields that unblocks certain scenarios.</span></span> <span data-ttu-id="53b2f-126">正確初始化應用程式版本之後，Application Insights 可以偵測與重新部署相互關聯的應用程式行為中是否有新模式。</span><span class="sxs-lookup"><span data-stu-id="53b2f-126">When application version is properly initialized, Application Insights can detect new patterns in application behavior correlated with redeployment.</span></span> <span data-ttu-id="53b2f-127">工作階段識別碼可用來計算中斷或某個問題對使用者造成的影響。</span><span class="sxs-lookup"><span data-stu-id="53b2f-127">Session id can be used to calculate the outage or an issue impact on users.</span></span> <span data-ttu-id="53b2f-128">計算特定失敗相依性、錯誤追蹤或重大例外狀況之工作階段識別碼值的相異計數，即可充分了解影響。</span><span class="sxs-lookup"><span data-stu-id="53b2f-128">Calculating distinct count of session id values for certain failed dependency, error trace or critical exception gives a good understanding of an impact.</span></span>

<span data-ttu-id="53b2f-129">Application Insights 遙測模型會定義將遙測與其所屬作業[相互關聯](application-insights-correlation.md)的方式。</span><span class="sxs-lookup"><span data-stu-id="53b2f-129">Application Insights telemetry model defines a way to [correlate](application-insights-correlation.md) telemetry to the operation of which it’s a part.</span></span> <span data-ttu-id="53b2f-130">例如，要求會發出 SQL Database 呼叫，並記錄診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="53b2f-130">For example, a request can make a SQL Database calls and recorded diagnostics info.</span></span> <span data-ttu-id="53b2f-131">針對會往回繫結至要求遙測的遙測項目，您可以設定這些遙測項目的相互關聯內容。</span><span class="sxs-lookup"><span data-stu-id="53b2f-131">You can set the correlation context for those telemetry items that tie it back to the request telemetry.</span></span>

## <a name="schema-improvements"></a><span data-ttu-id="53b2f-132">結構描述的增強功能</span><span class="sxs-lookup"><span data-stu-id="53b2f-132">Schema improvements</span></span>

<span data-ttu-id="53b2f-133">Application Insights 資料模型是簡單且基本但功能強大的方式，可建立您應用程式遙測的模型。</span><span class="sxs-lookup"><span data-stu-id="53b2f-133">Application Insights data model is a simple and basic yet powerful way to model your application telemetry.</span></span> <span data-ttu-id="53b2f-134">我們盡量保持模型可簡單且輕鬆地支援重要的案例，並擴充結構描述以供進階使用。</span><span class="sxs-lookup"><span data-stu-id="53b2f-134">We strive to keep the model simple and slim to support essential scenarios and allow to extend the schema for advanced use.</span></span>

<span data-ttu-id="53b2f-135">若要報告資料模型或結構描述的問題及建議，請使用 GitHub [ApplicationInsights-Home](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) 存放庫。</span><span class="sxs-lookup"><span data-stu-id="53b2f-135">To report data model or schema problems and suggestions use GitHub [ApplicationInsights-Home](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53b2f-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53b2f-136">Next steps</span></span>

- [<span data-ttu-id="53b2f-137">撰寫自訂遙測</span><span class="sxs-lookup"><span data-stu-id="53b2f-137">Write custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)
- <span data-ttu-id="53b2f-138">了解如何[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="53b2f-138">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="53b2f-139">使用[取樣](app-insights-sampling.md)，根據資料模型將遙測量降到最低。</span><span class="sxs-lookup"><span data-stu-id="53b2f-139">Use [sampling](app-insights-sampling.md) to minimize amount of telemetry based on data model.</span></span>
- <span data-ttu-id="53b2f-140">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="53b2f-140">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
