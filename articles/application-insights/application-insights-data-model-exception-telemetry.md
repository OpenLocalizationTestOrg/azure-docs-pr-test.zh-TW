---
title: "Azure Application Insights 遙測資料模型 - 例外狀況遙測 | Microsoft Docs"
description: "例外狀況遙測的 Application Insights 資料模型"
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
ms.openlocfilehash: 6b220b0cb6719bac606f599d657d08ab847c7590
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="405fe-103">例外狀況遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="405fe-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="405fe-104">在 [Application Insights](app-insights-overview.md) 中，例外狀況的執行個體代表受監視應用程式執行期間所發生的已處理或未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="405fe-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="405fe-105">問題識別碼</span><span class="sxs-lookup"><span data-stu-id="405fe-105">Problem Id</span></span>

<span data-ttu-id="405fe-106">例外狀況在程式碼中擲回位置的識別項。</span><span class="sxs-lookup"><span data-stu-id="405fe-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="405fe-107">用於例外狀況群組。</span><span class="sxs-lookup"><span data-stu-id="405fe-107">Used for exceptions grouping.</span></span> <span data-ttu-id="405fe-108">通常為例外狀況類型和呼叫堆疊中之函式的組合。</span><span class="sxs-lookup"><span data-stu-id="405fe-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="405fe-109">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="405fe-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="405fe-110">嚴重性層級</span><span class="sxs-lookup"><span data-stu-id="405fe-110">Severity level</span></span>

<span data-ttu-id="405fe-111">追蹤嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="405fe-111">Trace severity level.</span></span> <span data-ttu-id="405fe-112">值可為 `Verbose`、`Information`、`Warning`、`Error`、`Critical`。</span><span class="sxs-lookup"><span data-stu-id="405fe-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="405fe-113">例外狀況詳細資料</span><span class="sxs-lookup"><span data-stu-id="405fe-113">Exception details</span></span>

<span data-ttu-id="405fe-114">(等候進一步擴充)</span><span class="sxs-lookup"><span data-stu-id="405fe-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="405fe-115">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="405fe-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="405fe-116">自訂度量</span><span class="sxs-lookup"><span data-stu-id="405fe-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="405fe-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="405fe-117">Next steps</span></span>

- <span data-ttu-id="405fe-118">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="405fe-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="405fe-119">了解如何[使用 Application Insights 在 Web Apps 中診斷例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="405fe-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="405fe-120">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="405fe-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
