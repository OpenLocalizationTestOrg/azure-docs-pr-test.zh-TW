---
title: "aaaAzure 應用程式 Insights 遙測資料模型的相依性遙測 |Microsoft 文件"
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
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="3c1d6-103">相依性遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="3c1d6-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="3c1d6-104">相依性遙測 (在[Application Insights](app-insights-overview.md)) 代表與遠端的元件，例如 SQL 或 HTTP 端點的 hello 監視元件的互動。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of hello monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="3c1d6-105">名稱</span><span class="sxs-lookup"><span data-stu-id="3c1d6-105">Name</span></span>

<span data-ttu-id="3c1d6-106">此相依性呼叫以起始 hello 命令的名稱。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-106">Name of hello command initiated with this dependency call.</span></span> <span data-ttu-id="3c1d6-107">基數值低。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-107">Low cardinality value.</span></span> <span data-ttu-id="3c1d6-108">範例為預存程序名稱和 URL 路徑範本。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="3c1d6-109">ID</span><span class="sxs-lookup"><span data-stu-id="3c1d6-109">ID</span></span>

<span data-ttu-id="3c1d6-110">相依性呼叫執行個體的識別碼。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="3c1d6-111">用於相互關聯與 hello 要求遙測項目對應 toothis 相依性呼叫。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-111">Used for correlation with hello request telemetry item corresponding toothis dependency call.</span></span> <span data-ttu-id="3c1d6-112">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="3c1d6-113">資料</span><span class="sxs-lookup"><span data-stu-id="3c1d6-113">Data</span></span>

<span data-ttu-id="3c1d6-114">此相依性呼叫所起始的命令。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="3c1d6-115">範例為搭配所有查詢參數的 SQL 陳述式和 HTTP URL。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="3c1d6-116">類型</span><span class="sxs-lookup"><span data-stu-id="3c1d6-116">Type</span></span>

<span data-ttu-id="3c1d6-117">相依性類型名稱。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-117">Dependency type name.</span></span> <span data-ttu-id="3c1d6-118">相依性邏輯群組和其他欄位 (如 commandName 和 resultCode) 解譯的基數值較低。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="3c1d6-119">範例為 SQL、Azure 資料表和 HTTP。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="3c1d6-120">目標</span><span class="sxs-lookup"><span data-stu-id="3c1d6-120">Target</span></span>

<span data-ttu-id="3c1d6-121">相依性呼叫的目標網站。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-121">Target site of a dependency call.</span></span> <span data-ttu-id="3c1d6-122">範例為伺服器名稱、主機位址。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-122">Examples are server name, host address.</span></span> <span data-ttu-id="3c1d6-123">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="3c1d6-124">持續時間</span><span class="sxs-lookup"><span data-stu-id="3c1d6-124">Duration</span></span>

<span data-ttu-id="3c1d6-125">要求持續時間格式為︰`DD.HH:MM:SS.MMMMMM`。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="3c1d6-126">必須小於 `1000` 天。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="3c1d6-127">結果碼</span><span class="sxs-lookup"><span data-stu-id="3c1d6-127">Result code</span></span>

<span data-ttu-id="3c1d6-128">相依性呼叫的結果碼。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-128">Result code of a dependency call.</span></span> <span data-ttu-id="3c1d6-129">範例為 SQL 錯誤碼與 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="3c1d6-130">成功</span><span class="sxs-lookup"><span data-stu-id="3c1d6-130">Success</span></span>

<span data-ttu-id="3c1d6-131">表示成功或失敗的呼叫。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="3c1d6-132">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="3c1d6-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="3c1d6-133">自訂度量</span><span class="sxs-lookup"><span data-stu-id="3c1d6-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="3c1d6-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c1d6-134">Next steps</span></span>

- <span data-ttu-id="3c1d6-135">設定 [.NET](app-insights-asp-net-dependencies.md) 的相依性追蹤。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="3c1d6-136">設定 [Java](app-insights-java-agent.md) 的相依性追蹤。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="3c1d6-137">撰寫自訂相依性遙測</span><span class="sxs-lookup"><span data-stu-id="3c1d6-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="3c1d6-138">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3c1d6-139">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="3c1d6-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
