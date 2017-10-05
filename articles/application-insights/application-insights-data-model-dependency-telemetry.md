---
title: "Azure Application Insights 遙測資料模型 - 相依性遙測 | Microsoft Docs"
description: "相依性遙測的 Application Insights 資料模型"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="8af22-103">相依性遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="8af22-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="8af22-104">相依性遙測 (在 [Application Insights](app-insights-overview.md) 中) 代表受監視元件與遠端元件 (例如 SQL 或 HTTP 端點) 的互動。</span><span class="sxs-lookup"><span data-stu-id="8af22-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="8af22-105">名稱</span><span class="sxs-lookup"><span data-stu-id="8af22-105">Name</span></span>

<span data-ttu-id="8af22-106">使用此相依性呼叫所起始之命令的名稱。</span><span class="sxs-lookup"><span data-stu-id="8af22-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="8af22-107">基數值低。</span><span class="sxs-lookup"><span data-stu-id="8af22-107">Low cardinality value.</span></span> <span data-ttu-id="8af22-108">範例為預存程序名稱和 URL 路徑範本。</span><span class="sxs-lookup"><span data-stu-id="8af22-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="8af22-109">ID</span><span class="sxs-lookup"><span data-stu-id="8af22-109">ID</span></span>

<span data-ttu-id="8af22-110">相依性呼叫執行個體的識別碼。</span><span class="sxs-lookup"><span data-stu-id="8af22-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="8af22-111">用來與此相依性呼叫的對應要求遙測項目相互關聯。</span><span class="sxs-lookup"><span data-stu-id="8af22-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="8af22-112">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="8af22-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="8af22-113">資料</span><span class="sxs-lookup"><span data-stu-id="8af22-113">Data</span></span>

<span data-ttu-id="8af22-114">此相依性呼叫所起始的命令。</span><span class="sxs-lookup"><span data-stu-id="8af22-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="8af22-115">範例為搭配所有查詢參數的 SQL 陳述式和 HTTP URL。</span><span class="sxs-lookup"><span data-stu-id="8af22-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="8af22-116">類型</span><span class="sxs-lookup"><span data-stu-id="8af22-116">Type</span></span>

<span data-ttu-id="8af22-117">相依性類型名稱。</span><span class="sxs-lookup"><span data-stu-id="8af22-117">Dependency type name.</span></span> <span data-ttu-id="8af22-118">相依性邏輯群組和其他欄位 (如 commandName 和 resultCode) 解譯的基數值較低。</span><span class="sxs-lookup"><span data-stu-id="8af22-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="8af22-119">範例為 SQL、Azure 資料表和 HTTP。</span><span class="sxs-lookup"><span data-stu-id="8af22-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="8af22-120">目標</span><span class="sxs-lookup"><span data-stu-id="8af22-120">Target</span></span>

<span data-ttu-id="8af22-121">相依性呼叫的目標網站。</span><span class="sxs-lookup"><span data-stu-id="8af22-121">Target site of a dependency call.</span></span> <span data-ttu-id="8af22-122">範例為伺服器名稱、主機位址。</span><span class="sxs-lookup"><span data-stu-id="8af22-122">Examples are server name, host address.</span></span> <span data-ttu-id="8af22-123">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="8af22-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="8af22-124">持續時間</span><span class="sxs-lookup"><span data-stu-id="8af22-124">Duration</span></span>

<span data-ttu-id="8af22-125">要求持續時間格式為︰`DD.HH:MM:SS.MMMMMM`。</span><span class="sxs-lookup"><span data-stu-id="8af22-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="8af22-126">必須小於 `1000` 天。</span><span class="sxs-lookup"><span data-stu-id="8af22-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="8af22-127">結果碼</span><span class="sxs-lookup"><span data-stu-id="8af22-127">Result code</span></span>

<span data-ttu-id="8af22-128">相依性呼叫的結果碼。</span><span class="sxs-lookup"><span data-stu-id="8af22-128">Result code of a dependency call.</span></span> <span data-ttu-id="8af22-129">範例為 SQL 錯誤碼與 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="8af22-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="8af22-130">成功</span><span class="sxs-lookup"><span data-stu-id="8af22-130">Success</span></span>

<span data-ttu-id="8af22-131">表示成功或失敗的呼叫。</span><span class="sxs-lookup"><span data-stu-id="8af22-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="8af22-132">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="8af22-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="8af22-133">自訂度量</span><span class="sxs-lookup"><span data-stu-id="8af22-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="8af22-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8af22-134">Next steps</span></span>

- <span data-ttu-id="8af22-135">設定 [.NET](app-insights-asp-net-dependencies.md) 的相依性追蹤。</span><span class="sxs-lookup"><span data-stu-id="8af22-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="8af22-136">設定 [Java](app-insights-java-agent.md) 的相依性追蹤。</span><span class="sxs-lookup"><span data-stu-id="8af22-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="8af22-137">撰寫自訂相依性遙測</span><span class="sxs-lookup"><span data-stu-id="8af22-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="8af22-138">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="8af22-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="8af22-139">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="8af22-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
