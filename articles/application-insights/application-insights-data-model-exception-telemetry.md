---
title: "aaaAzure Insights 遙測資料模型的應用程式的例外狀況遙測 |Microsoft 文件"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="be26e-103">例外狀況遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="be26e-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="be26e-104">在[Application Insights](app-insights-overview.md)，例外狀況的執行個體代表 hello 受監視應用程式執行期間發生的處理或未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="be26e-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of hello monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="be26e-105">問題識別碼</span><span class="sxs-lookup"><span data-stu-id="be26e-105">Problem Id</span></span>

<span data-ttu-id="be26e-106">已在程式碼中擲回 hello 例外狀況的識別項。</span><span class="sxs-lookup"><span data-stu-id="be26e-106">Identifier of where hello exception was thrown in code.</span></span> <span data-ttu-id="be26e-107">用於例外狀況群組。</span><span class="sxs-lookup"><span data-stu-id="be26e-107">Used for exceptions grouping.</span></span> <span data-ttu-id="be26e-108">一般例外狀況類型的組合和 hello 函式的呼叫堆疊。</span><span class="sxs-lookup"><span data-stu-id="be26e-108">Typically a combination of exception type and a function from hello call stack.</span></span>

<span data-ttu-id="be26e-109">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="be26e-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="be26e-110">嚴重性層級</span><span class="sxs-lookup"><span data-stu-id="be26e-110">Severity level</span></span>

<span data-ttu-id="be26e-111">追蹤嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="be26e-111">Trace severity level.</span></span> <span data-ttu-id="be26e-112">值可為 `Verbose`、`Information`、`Warning`、`Error`、`Critical`。</span><span class="sxs-lookup"><span data-stu-id="be26e-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="be26e-113">例外狀況詳細資料</span><span class="sxs-lookup"><span data-stu-id="be26e-113">Exception details</span></span>

<span data-ttu-id="be26e-114">(toobe 擴充)</span><span class="sxs-lookup"><span data-stu-id="be26e-114">(toobe extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="be26e-115">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="be26e-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="be26e-116">自訂度量</span><span class="sxs-lookup"><span data-stu-id="be26e-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="be26e-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be26e-117">Next steps</span></span>

- <span data-ttu-id="be26e-118">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="be26e-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="be26e-119">了解如何太[診斷使用 Application Insights web 應用程式中的例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="be26e-119">Learn how too[diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="be26e-120">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="be26e-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
