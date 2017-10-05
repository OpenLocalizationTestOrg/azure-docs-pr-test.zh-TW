---
title: "Azure Application Insights 遙測資料模型 - 事件遙測 | Microsoft Docs"
description: "事件遙測的 Application Insights 資料模型"
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
ms.openlocfilehash: 422e193ae10938954602a6ef8c49fd47f473bc01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="9157e-103">事件遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="9157e-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="9157e-104">您可以建立事件遙測項目 (在 [Application Insights](app-insights-overview.md) 中) 來代表發生在您應用程式中的事件。</span><span class="sxs-lookup"><span data-stu-id="9157e-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application.</span></span> <span data-ttu-id="9157e-105">通常它是與使用者互動的事件，例如按一下按鈕或簽出訂單。</span><span class="sxs-lookup"><span data-stu-id="9157e-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="9157e-106">它也可以是初始化或組態更新等應用程式生命週期事件。</span><span class="sxs-lookup"><span data-stu-id="9157e-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="9157e-107">事件在語意上不一定會與要求相互關聯。</span><span class="sxs-lookup"><span data-stu-id="9157e-107">Semantically, events may or may not be correlated to requests.</span></span> <span data-ttu-id="9157e-108">不過，如果使用得當，事件遙測比要求或追蹤更重要。</span><span class="sxs-lookup"><span data-stu-id="9157e-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="9157e-109">事件代表商務遙測，且應該會受到個別、較不積極[取樣](app-insights-api-filtering-sampling.md)所影響。</span><span class="sxs-lookup"><span data-stu-id="9157e-109">Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="9157e-110">名稱</span><span class="sxs-lookup"><span data-stu-id="9157e-110">Name</span></span>

<span data-ttu-id="9157e-111">事件名稱。</span><span class="sxs-lookup"><span data-stu-id="9157e-111">Event name.</span></span> <span data-ttu-id="9157e-112">若要有適當的分組與實用的計量，請限制應用程式，使其產生少量的個別事件名稱。</span><span class="sxs-lookup"><span data-stu-id="9157e-112">To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="9157e-113">例如，針對每個產生的事件執行個體，不要使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="9157e-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="9157e-114">最大長度︰512 個字元</span><span class="sxs-lookup"><span data-stu-id="9157e-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="9157e-115">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="9157e-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="9157e-116">自訂度量</span><span class="sxs-lookup"><span data-stu-id="9157e-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="9157e-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9157e-117">Next steps</span></span>

- <span data-ttu-id="9157e-118">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="9157e-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="9157e-119">撰寫自訂事件遙測</span><span class="sxs-lookup"><span data-stu-id="9157e-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="9157e-120">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="9157e-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
