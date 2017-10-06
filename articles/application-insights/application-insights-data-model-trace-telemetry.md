---
title: "aaaAzure Insights 遙測資料模型的應用程式-追蹤遙測 |Microsoft 文件"
description: "追蹤遙測的 Application Insights 資料模型"
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
ms.openlocfilehash: dfdee958e07d57448ff41abc5cd33bfd05dac090
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="e6892-103">追蹤遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="e6892-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="e6892-104">追蹤遙測 (在 [Application Insights](app-insights-overview.md) 中) 代表以文字搜尋的 `printf` 樣式追蹤陳述式。</span><span class="sxs-lookup"><span data-stu-id="e6892-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="e6892-105">`Log4Net`、`NLog`和其他以文字為基礎的記錄檔項目會轉譯成此類型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="e6892-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="e6892-106">hello 追蹤沒有為擴充性的度量單位。</span><span class="sxs-lookup"><span data-stu-id="e6892-106">hello trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="e6892-107">訊息</span><span class="sxs-lookup"><span data-stu-id="e6892-107">Message</span></span>

<span data-ttu-id="e6892-108">追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="e6892-108">Trace message.</span></span>

<span data-ttu-id="e6892-109">最大長度︰32768 個字元</span><span class="sxs-lookup"><span data-stu-id="e6892-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="e6892-110">嚴重性層級</span><span class="sxs-lookup"><span data-stu-id="e6892-110">Severity level</span></span>

<span data-ttu-id="e6892-111">追蹤嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="e6892-111">Trace severity level.</span></span> <span data-ttu-id="e6892-112">值可為 `Verbose`、`Information`、`Warning`、`Error`、`Critical`。</span><span class="sxs-lookup"><span data-stu-id="e6892-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="e6892-113">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="e6892-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="e6892-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6892-114">Next steps</span></span>

- <span data-ttu-id="e6892-115">[在 Application Insights 中探索 .NET 追蹤記錄](app-insights-asp-net-trace-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="e6892-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="e6892-116">[在 Application Insights 中探索 Java 追蹤記錄](app-insights-java-trace-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="e6892-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="e6892-117">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="e6892-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="e6892-118">撰寫自訂追蹤遙測</span><span class="sxs-lookup"><span data-stu-id="e6892-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="e6892-119">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="e6892-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
