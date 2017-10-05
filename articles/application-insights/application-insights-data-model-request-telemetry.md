---
title: "Azure Application Insights 遙測資料模型 - 要求遙測 | Microsoft Docs"
description: "要求遙測的 Application Insights 資料模型"
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
ms.openlocfilehash: 8e782e45b706cadec66e7404dd9abc2e01dea917
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="request-telemetry-application-insights-data-model"></a><span data-ttu-id="3ed10-103">要求遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="3ed10-103">Request telemetry: Application Insights data model</span></span>

<span data-ttu-id="3ed10-104">要求遙測項目 (在 [Application Insights](app-insights-overview.md) 中) 代表外部要求對應用程式所觸發的執行邏輯順序。</span><span class="sxs-lookup"><span data-stu-id="3ed10-104">A request telemetry item (in [Application Insights](app-insights-overview.md)) represents the logical sequence of execution triggered by an external request to your application.</span></span> <span data-ttu-id="3ed10-105">每個要求執行都是由包含所有執行參數的唯一 `ID` 和 `url` 所識別。</span><span class="sxs-lookup"><span data-stu-id="3ed10-105">Every request execution is identified by unique `ID` and `url` containing all the execution parameters.</span></span> <span data-ttu-id="3ed10-106">您可以將這些要求依邏輯 `name` 群組，並定義這項要求的 `source`。</span><span class="sxs-lookup"><span data-stu-id="3ed10-106">You can group requests by logical `name` and define the `source` of this request.</span></span> <span data-ttu-id="3ed10-107">程式碼執行可能會導致 `success` 或 `fail`，並且有特定 `duration`。</span><span class="sxs-lookup"><span data-stu-id="3ed10-107">Code execution can result in `success` or `fail` and has a certain `duration`.</span></span> <span data-ttu-id="3ed10-108">成功和失敗的執行都可以進一步以 `resultCode` 分組。</span><span class="sxs-lookup"><span data-stu-id="3ed10-108">Both success and failure executions may be grouped further by `resultCode`.</span></span> <span data-ttu-id="3ed10-109">信封層級上定義之要求遙測的開始時間。</span><span class="sxs-lookup"><span data-stu-id="3ed10-109">Start time for the request telemetry defined on the envelope level.</span></span>

<span data-ttu-id="3ed10-110">要求遙測會使用自訂 `properties` 和 `measurements`支援標準的擴充性模型。</span><span class="sxs-lookup"><span data-stu-id="3ed10-110">Request telemetry supports the standard extensibility model using custom `properties` and `measurements`.</span></span>

## <a name="name"></a><span data-ttu-id="3ed10-111">名稱</span><span class="sxs-lookup"><span data-stu-id="3ed10-111">Name</span></span>

<span data-ttu-id="3ed10-112">要求的名稱代表處理要求所採用的程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="3ed10-112">Name of the request represents code path taken to process the request.</span></span> <span data-ttu-id="3ed10-113">較低的基數值可使群組要求更妥善。</span><span class="sxs-lookup"><span data-stu-id="3ed10-113">Low cardinality value to allow better grouping of requests.</span></span> <span data-ttu-id="3ed10-114">針對 HTTP 要求，它代表 HTTP 方法和 URL 路徑範本，例如無實際 `id` 值的 `GET /values/{id}`。</span><span class="sxs-lookup"><span data-stu-id="3ed10-114">For HTTP requests it represents the HTTP method and URL path template like `GET /values/{id}` without the actual `id` value.</span></span>

<span data-ttu-id="3ed10-115">Application Insights web SDK 會將要求名稱依「現狀」傳送 (考量字母大小寫)。</span><span class="sxs-lookup"><span data-stu-id="3ed10-115">Application Insights web SDK sends request name "as is" with regards to letter case.</span></span> <span data-ttu-id="3ed10-116">UI 上的群組會區分大小寫，因此 `GET /Home/Index` 會與 `GET /home/INDEX` 分開計算，即使它們通常會產生相同的控制器和動作執行。</span><span class="sxs-lookup"><span data-stu-id="3ed10-116">Grouping on UI is case-sensitive so `GET /Home/Index` is counted separately from `GET /home/INDEX` even though often they result in the same controller and action execution.</span></span> <span data-ttu-id="3ed10-117">原因是 URL 通常會[區分大小寫](http://www.w3.org/TR/WD-html40-970708/htmlweb.html)。</span><span class="sxs-lookup"><span data-stu-id="3ed10-117">The reason for that is that urls in general are [case-sensitive](http://www.w3.org/TR/WD-html40-970708/htmlweb.html).</span></span> <span data-ttu-id="3ed10-118">您可能要查看 URL 出現的所有 `404` 是否都以大寫輸入。</span><span class="sxs-lookup"><span data-stu-id="3ed10-118">You may want to see if all `404` happened for the urls typed in uppercase.</span></span> <span data-ttu-id="3ed10-119">您可以在[部落格文章](http://apmtips.com/blog/2015/02/23/request-name-and-url/)閱讀更多由 ASP.Net Web SDK 要求名稱集合的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3ed10-119">You can read more on request name collection by ASP.Net Web SDK in the [blog post](http://apmtips.com/blog/2015/02/23/request-name-and-url/).</span></span>

<span data-ttu-id="3ed10-120">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="3ed10-120">Max length: 1024 characters</span></span>

## <a name="id"></a><span data-ttu-id="3ed10-121">ID</span><span class="sxs-lookup"><span data-stu-id="3ed10-121">ID</span></span>

<span data-ttu-id="3ed10-122">要求呼叫執行個體的識別碼。</span><span class="sxs-lookup"><span data-stu-id="3ed10-122">Identifier of a request call instance.</span></span> <span data-ttu-id="3ed10-123">用於要求和其他遙測項目之間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="3ed10-123">Used for correlation between request and other telemetry items.</span></span> <span data-ttu-id="3ed10-124">識別碼必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="3ed10-124">ID should be globally unique.</span></span> <span data-ttu-id="3ed10-125">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="3ed10-125">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="3ed10-126">最大長度︰128 個字元</span><span class="sxs-lookup"><span data-stu-id="3ed10-126">Max length: 128 characters</span></span>

## <a name="url"></a><span data-ttu-id="3ed10-127">Url</span><span class="sxs-lookup"><span data-stu-id="3ed10-127">Url</span></span>

<span data-ttu-id="3ed10-128">包含所有查詢字串參數的要求 URL。</span><span class="sxs-lookup"><span data-stu-id="3ed10-128">Request URL with all query string parameters.</span></span>

<span data-ttu-id="3ed10-129">最大長度︰2048 個字元</span><span class="sxs-lookup"><span data-stu-id="3ed10-129">Max length: 2048 characters</span></span>

## <a name="source"></a><span data-ttu-id="3ed10-130">來源</span><span class="sxs-lookup"><span data-stu-id="3ed10-130">Source</span></span>

<span data-ttu-id="3ed10-131">要求的來源。</span><span class="sxs-lookup"><span data-stu-id="3ed10-131">Source of the request.</span></span> <span data-ttu-id="3ed10-132">範例包括呼叫端的檢測金鑰或呼叫端的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3ed10-132">Examples are the instrumentation key of the caller or the ip address of the caller.</span></span> <span data-ttu-id="3ed10-133">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="3ed10-133">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="3ed10-134">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="3ed10-134">Max length: 1024 characters</span></span>

## <a name="duration"></a><span data-ttu-id="3ed10-135">持續時間</span><span class="sxs-lookup"><span data-stu-id="3ed10-135">Duration</span></span>

<span data-ttu-id="3ed10-136">要求持續時間格式為︰`DD.HH:MM:SS.MMMMMM`。</span><span class="sxs-lookup"><span data-stu-id="3ed10-136">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="3ed10-137">必須是正數且小於 `1000` 天。</span><span class="sxs-lookup"><span data-stu-id="3ed10-137">Must be positive and less than `1000` days.</span></span> <span data-ttu-id="3ed10-138">這是必要欄位，因為要求遙測代表開頭與結尾的作業。</span><span class="sxs-lookup"><span data-stu-id="3ed10-138">This field is required as request telemetry represents the operation with the beginning and the end.</span></span>

## <a name="response-code"></a><span data-ttu-id="3ed10-139">Response code</span><span class="sxs-lookup"><span data-stu-id="3ed10-139">Response code</span></span>

<span data-ttu-id="3ed10-140">要求執行的結果。</span><span class="sxs-lookup"><span data-stu-id="3ed10-140">Result of a request execution.</span></span> <span data-ttu-id="3ed10-141">HTTP 要求的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3ed10-141">HTTP status code for HTTP requests.</span></span> <span data-ttu-id="3ed10-142">可能是 `HRESULT` 值或其他要求類型的例外狀況類型。</span><span class="sxs-lookup"><span data-stu-id="3ed10-142">It may be `HRESULT` value or exception type for other request types.</span></span>

<span data-ttu-id="3ed10-143">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="3ed10-143">Max length: 1024 characters</span></span>

## <a name="success"></a><span data-ttu-id="3ed10-144">成功</span><span class="sxs-lookup"><span data-stu-id="3ed10-144">Success</span></span>

<span data-ttu-id="3ed10-145">表示成功或失敗的呼叫。</span><span class="sxs-lookup"><span data-stu-id="3ed10-145">Indication of successful or unsuccessful call.</span></span> <span data-ttu-id="3ed10-146">這是必填欄位。</span><span class="sxs-lookup"><span data-stu-id="3ed10-146">This field is required.</span></span> <span data-ttu-id="3ed10-147">當未明確設定為 `false` 時 - 要求會視為成功。</span><span class="sxs-lookup"><span data-stu-id="3ed10-147">When not set explicitly to `false` - request considered to be successful.</span></span> <span data-ttu-id="3ed10-148">如果作業是例外狀況而中斷或傳回錯誤結果碼，將此值設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="3ed10-148">Set this value to `false` if operation was interrupted by exception or returned error result code.</span></span>

<span data-ttu-id="3ed10-149">針對 Web 應用程式，當回應碼小於 `400` 或等於 `401` 時，Application Insights 會將要求定義為失敗。</span><span class="sxs-lookup"><span data-stu-id="3ed10-149">For the web applications, Application Insights define request as failed when the response code is less the `400` or equal to `401`.</span></span> <span data-ttu-id="3ed10-150">不過有可能會發生這個預設對應與應用程式之語意不相符的情況。</span><span class="sxs-lookup"><span data-stu-id="3ed10-150">However there are cases when this default mapping does not match the semantic of the application.</span></span> <span data-ttu-id="3ed10-151">回應碼 `404` 可能表示「沒有記錄」，這可能是一般流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="3ed10-151">Response code `404` may indicate "no records", which can be part of regular flow.</span></span> <span data-ttu-id="3ed10-152">它也可能表示中斷的連結。</span><span class="sxs-lookup"><span data-stu-id="3ed10-152">It also may indicate a broken link.</span></span> <span data-ttu-id="3ed10-153">針對中斷連結，您甚至可以實作更進階的邏輯。</span><span class="sxs-lookup"><span data-stu-id="3ed10-153">For the broken links, you can even implement more advanced logic.</span></span> <span data-ttu-id="3ed10-154">只有當中斷的連結藉由分析 URL 查閱者位於相同網站時，您才可以將這些連結標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="3ed10-154">You can mark broken links as failures only when those links are located on the same site by analyzing url referrer.</span></span> <span data-ttu-id="3ed10-155">或是從公司的行動應用程式存取時，才可以將它們標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="3ed10-155">Or mark them as failures when accessed from the company's mobile application.</span></span> <span data-ttu-id="3ed10-156">同樣地，從不支援重新導向的用戶端存取時，`301` 和 `302` 會表示失敗。</span><span class="sxs-lookup"><span data-stu-id="3ed10-156">Similarly `301` and `302` indicates failure when accessed from the client that doesn't support redirect.</span></span>

<span data-ttu-id="3ed10-157">部分接受的內容 `206` 可能表示整體要求失敗。</span><span class="sxs-lookup"><span data-stu-id="3ed10-157">Partially accepted content `206` may indicate a failure of an overall request.</span></span> <span data-ttu-id="3ed10-158">例如，Application Insights 端點會接收一批遙測項目作為單一要求。</span><span class="sxs-lookup"><span data-stu-id="3ed10-158">For instance, Application Insights endpoint receives a batch of telemetry items as a single request.</span></span> <span data-ttu-id="3ed10-159">當批次中的某些項目未處理成功時，它會傳回 `206`。</span><span class="sxs-lookup"><span data-stu-id="3ed10-159">It returns `206` when some items in the batch were not processed successfully.</span></span> <span data-ttu-id="3ed10-160">`206` 的速率遞增表示有需要調查的問題。</span><span class="sxs-lookup"><span data-stu-id="3ed10-160">Increasing rate of `206` indicates a problem that needs to be investigated.</span></span> <span data-ttu-id="3ed10-161">類似的邏輯也適用於 `207` 多狀態，當中成功可能是不同回應代碼的最差狀況。</span><span class="sxs-lookup"><span data-stu-id="3ed10-161">Similar logic applies to `207` Multi-Status where the success may be the worst of separate response codes.</span></span>

<span data-ttu-id="3ed10-162">您可以在[部落格文章](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/)中閱讀更多要求結果碼和狀態碼的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3ed10-162">You can read more on request result code and status code in the [blog post](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).</span></span>

## <a name="custom-properties"></a><span data-ttu-id="3ed10-163">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="3ed10-163">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="3ed10-164">自訂度量</span><span class="sxs-lookup"><span data-stu-id="3ed10-164">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="3ed10-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ed10-165">Next steps</span></span>

- [<span data-ttu-id="3ed10-166">撰寫自訂要求遙測</span><span class="sxs-lookup"><span data-stu-id="3ed10-166">Write custom request telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackrequest)
- <span data-ttu-id="3ed10-167">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3ed10-167">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3ed10-168">了解如何使用 Application Insights [設定 ASP.NET Core](app-insights-asp-net.md) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ed10-168">Learn how to [configure ASP.NET Core](app-insights-asp-net.md) application with Application Insights.</span></span>
- <span data-ttu-id="3ed10-169">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="3ed10-169">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
