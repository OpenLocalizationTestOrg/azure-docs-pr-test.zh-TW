---
title: "aaaAzure Insights 遙測資料模型的應用程式-事件遙測 |Microsoft 文件"
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="cdeaf-103">事件遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="cdeaf-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="cdeaf-104">您可以建立事件遙測項目 (在[Application Insights](app-insights-overview.md)) toorepresent 應用程式中發生的事件。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) toorepresent an event that occurred in your application.</span></span> <span data-ttu-id="cdeaf-105">通常它是與使用者互動的事件，例如按一下按鈕或簽出訂單。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="cdeaf-106">它也可以是初始化或組態更新等應用程式生命週期事件。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="cdeaf-107">語意上來說，事件可能會或可能不是相互關聯的 toorequests。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-107">Semantically, events may or may not be correlated toorequests.</span></span> <span data-ttu-id="cdeaf-108">不過，如果使用得當，事件遙測比要求或追蹤更重要。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="cdeaf-109">代表企業遙測事件，而且應該主旨 tooseparate，較不主動[取樣](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-109">Events represent business telemetry and should be a subject tooseparate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="cdeaf-110">名稱</span><span class="sxs-lookup"><span data-stu-id="cdeaf-110">Name</span></span>

<span data-ttu-id="cdeaf-111">事件名稱。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-111">Event name.</span></span> <span data-ttu-id="cdeaf-112">tooallow 適當的群組和實用的度量，限制您的應用程式，使其產生少量個別的事件名稱。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-112">tooallow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="cdeaf-113">例如，針對每個產生的事件執行個體，不要使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="cdeaf-114">最大長度︰512 個字元</span><span class="sxs-lookup"><span data-stu-id="cdeaf-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="cdeaf-115">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="cdeaf-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="cdeaf-116">自訂度量</span><span class="sxs-lookup"><span data-stu-id="cdeaf-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="cdeaf-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdeaf-117">Next steps</span></span>

- <span data-ttu-id="cdeaf-118">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="cdeaf-119">撰寫自訂事件遙測</span><span class="sxs-lookup"><span data-stu-id="cdeaf-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="cdeaf-120">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="cdeaf-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
