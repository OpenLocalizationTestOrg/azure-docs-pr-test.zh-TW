---
title: "aaaAzure Insights 遙測資料模型的應用程式-要求遙測 |Microsoft 文件"
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
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a><span data-ttu-id="53845-103">要求遙測：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="53845-103">Request telemetry: Application Insights data model</span></span>

<span data-ttu-id="53845-104">要求遙測項目 (在[Application Insights](app-insights-overview.md)) 代表 hello 觸發 tooyour 應用程式外部要求所執行的邏輯順序。</span><span class="sxs-lookup"><span data-stu-id="53845-104">A request telemetry item (in [Application Insights](app-insights-overview.md)) represents hello logical sequence of execution triggered by an external request tooyour application.</span></span> <span data-ttu-id="53845-105">依唯一識別每個要求執行`ID`和`url`包含所有 hello 執行中參數。</span><span class="sxs-lookup"><span data-stu-id="53845-105">Every request execution is identified by unique `ID` and `url` containing all hello execution parameters.</span></span> <span data-ttu-id="53845-106">您可以依邏輯分組要求`name`並定義 hello`source`這項要求。</span><span class="sxs-lookup"><span data-stu-id="53845-106">You can group requests by logical `name` and define hello `source` of this request.</span></span> <span data-ttu-id="53845-107">程式碼執行可能會導致 `success` 或 `fail`，並且有特定 `duration`。</span><span class="sxs-lookup"><span data-stu-id="53845-107">Code execution can result in `success` or `fail` and has a certain `duration`.</span></span> <span data-ttu-id="53845-108">成功和失敗的執行都可以進一步以 `resultCode` 分組。</span><span class="sxs-lookup"><span data-stu-id="53845-108">Both success and failure executions may be grouped further by `resultCode`.</span></span> <span data-ttu-id="53845-109">開始 hello 要求遙測 hello 信封層級上定義的時間。</span><span class="sxs-lookup"><span data-stu-id="53845-109">Start time for hello request telemetry defined on hello envelope level.</span></span>

<span data-ttu-id="53845-110">要求遙測支援使用自訂的 hello 標準的擴充性模型`properties`和`measurements`。</span><span class="sxs-lookup"><span data-stu-id="53845-110">Request telemetry supports hello standard extensibility model using custom `properties` and `measurements`.</span></span>

## <a name="name"></a><span data-ttu-id="53845-111">名稱</span><span class="sxs-lookup"><span data-stu-id="53845-111">Name</span></span>

<span data-ttu-id="53845-112">Hello 要求名稱表示程式碼採取路徑 tooprocess hello 要求。</span><span class="sxs-lookup"><span data-stu-id="53845-112">Name of hello request represents code path taken tooprocess hello request.</span></span> <span data-ttu-id="53845-113">較低的基數值 tooallow 更好的要求分組。</span><span class="sxs-lookup"><span data-stu-id="53845-113">Low cardinality value tooallow better grouping of requests.</span></span> <span data-ttu-id="53845-114">代表 HTTP 要求的 hello HTTP 方法和 URL 路徑範本，例如`GET /values/{id}`沒有實際的 hello`id`值。</span><span class="sxs-lookup"><span data-stu-id="53845-114">For HTTP requests it represents hello HTTP method and URL path template like `GET /values/{id}` without hello actual `id` value.</span></span>

<span data-ttu-id="53845-115">應用程式 Insights web SDK 會與相關事宜 tooletter 案例傳送要求 「 現狀 」 的名稱。</span><span class="sxs-lookup"><span data-stu-id="53845-115">Application Insights web SDK sends request name "as is" with regards tooletter case.</span></span> <span data-ttu-id="53845-116">在 UI 上的群組會區分大小寫因此`GET /Home/Index`分開計算從`GET /home/INDEX`即使它們通常會在 hello 相同控制器與動作執行。</span><span class="sxs-lookup"><span data-stu-id="53845-116">Grouping on UI is case-sensitive so `GET /Home/Index` is counted separately from `GET /home/INDEX` even though often they result in hello same controller and action execution.</span></span> <span data-ttu-id="53845-117">hello，原因是 url 通常會[區分大小寫](http://www.w3.org/TR/WD-html40-970708/htmlweb.html)。</span><span class="sxs-lookup"><span data-stu-id="53845-117">hello reason for that is that urls in general are [case-sensitive](http://www.w3.org/TR/WD-html40-970708/htmlweb.html).</span></span> <span data-ttu-id="53845-118">如果要將所有可能會想要 toosee`404`發生 hello url 為大寫。</span><span class="sxs-lookup"><span data-stu-id="53845-118">You may want toosee if all `404` happened for hello urls typed in uppercase.</span></span> <span data-ttu-id="53845-119">您可以讀取多個在要求名稱集合的 ASP.Net Web SDK 在 hello[部落格文章](http://apmtips.com/blog/2015/02/23/request-name-and-url/)。</span><span class="sxs-lookup"><span data-stu-id="53845-119">You can read more on request name collection by ASP.Net Web SDK in hello [blog post](http://apmtips.com/blog/2015/02/23/request-name-and-url/).</span></span>

<span data-ttu-id="53845-120">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="53845-120">Max length: 1024 characters</span></span>

## <a name="id"></a><span data-ttu-id="53845-121">ID</span><span class="sxs-lookup"><span data-stu-id="53845-121">ID</span></span>

<span data-ttu-id="53845-122">要求呼叫執行個體的識別碼。</span><span class="sxs-lookup"><span data-stu-id="53845-122">Identifier of a request call instance.</span></span> <span data-ttu-id="53845-123">用於要求和其他遙測項目之間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="53845-123">Used for correlation between request and other telemetry items.</span></span> <span data-ttu-id="53845-124">識別碼必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="53845-124">ID should be globally unique.</span></span> <span data-ttu-id="53845-125">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="53845-125">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="53845-126">最大長度︰128 個字元</span><span class="sxs-lookup"><span data-stu-id="53845-126">Max length: 128 characters</span></span>

## <a name="url"></a><span data-ttu-id="53845-127">Url</span><span class="sxs-lookup"><span data-stu-id="53845-127">Url</span></span>

<span data-ttu-id="53845-128">包含所有查詢字串參數的要求 URL。</span><span class="sxs-lookup"><span data-stu-id="53845-128">Request URL with all query string parameters.</span></span>

<span data-ttu-id="53845-129">最大長度︰2048 個字元</span><span class="sxs-lookup"><span data-stu-id="53845-129">Max length: 2048 characters</span></span>

## <a name="source"></a><span data-ttu-id="53845-130">來源</span><span class="sxs-lookup"><span data-stu-id="53845-130">Source</span></span>

<span data-ttu-id="53845-131">Hello 要求來源。</span><span class="sxs-lookup"><span data-stu-id="53845-131">Source of hello request.</span></span> <span data-ttu-id="53845-132">範例包括 hello 呼叫端的 hello 檢測金鑰或 hello 呼叫端的 hello ip 位址。</span><span class="sxs-lookup"><span data-stu-id="53845-132">Examples are hello instrumentation key of hello caller or hello ip address of hello caller.</span></span> <span data-ttu-id="53845-133">如需詳細資訊，請參閱[相互關聯](application-insights-correlation.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="53845-133">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="53845-134">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="53845-134">Max length: 1024 characters</span></span>

## <a name="duration"></a><span data-ttu-id="53845-135">持續時間</span><span class="sxs-lookup"><span data-stu-id="53845-135">Duration</span></span>

<span data-ttu-id="53845-136">要求持續時間格式為︰`DD.HH:MM:SS.MMMMMM`。</span><span class="sxs-lookup"><span data-stu-id="53845-136">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="53845-137">必須是正數且小於 `1000` 天。</span><span class="sxs-lookup"><span data-stu-id="53845-137">Must be positive and less than `1000` days.</span></span> <span data-ttu-id="53845-138">因為要求遙測代表 hello 與 hello 開頭和結尾 hello 的作業，此欄位為必要。</span><span class="sxs-lookup"><span data-stu-id="53845-138">This field is required as request telemetry represents hello operation with hello beginning and hello end.</span></span>

## <a name="response-code"></a><span data-ttu-id="53845-139">Response code</span><span class="sxs-lookup"><span data-stu-id="53845-139">Response code</span></span>

<span data-ttu-id="53845-140">要求執行的結果。</span><span class="sxs-lookup"><span data-stu-id="53845-140">Result of a request execution.</span></span> <span data-ttu-id="53845-141">HTTP 要求的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="53845-141">HTTP status code for HTTP requests.</span></span> <span data-ttu-id="53845-142">可能是 `HRESULT` 值或其他要求類型的例外狀況類型。</span><span class="sxs-lookup"><span data-stu-id="53845-142">It may be `HRESULT` value or exception type for other request types.</span></span>

<span data-ttu-id="53845-143">最大長度︰1024 個字元</span><span class="sxs-lookup"><span data-stu-id="53845-143">Max length: 1024 characters</span></span>

## <a name="success"></a><span data-ttu-id="53845-144">成功</span><span class="sxs-lookup"><span data-stu-id="53845-144">Success</span></span>

<span data-ttu-id="53845-145">表示成功或失敗的呼叫。</span><span class="sxs-lookup"><span data-stu-id="53845-145">Indication of successful or unsuccessful call.</span></span> <span data-ttu-id="53845-146">這是必填欄位。</span><span class="sxs-lookup"><span data-stu-id="53845-146">This field is required.</span></span> <span data-ttu-id="53845-147">當未明確設定太`false`-視為 toobe 成功的要求。</span><span class="sxs-lookup"><span data-stu-id="53845-147">When not set explicitly too`false` - request considered toobe successful.</span></span> <span data-ttu-id="53845-148">將此值設定為太`false`如果作業已因例外狀況或傳回錯誤結果碼。</span><span class="sxs-lookup"><span data-stu-id="53845-148">Set this value too`false` if operation was interrupted by exception or returned error result code.</span></span>

<span data-ttu-id="53845-149">Hello web 應用程式，Application Insights 定義要求為失敗 hello 回應程式碼時較少的 hello`400`或太等於`401`。</span><span class="sxs-lookup"><span data-stu-id="53845-149">For hello web applications, Application Insights define request as failed when hello response code is less hello `400` or equal too`401`.</span></span> <span data-ttu-id="53845-150">不過一些情況下這個預設對應不符合 hello hello 應用程式的語意。</span><span class="sxs-lookup"><span data-stu-id="53845-150">However there are cases when this default mapping does not match hello semantic of hello application.</span></span> <span data-ttu-id="53845-151">回應碼 `404` 可能表示「沒有記錄」，這可能是一般流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="53845-151">Response code `404` may indicate "no records", which can be part of regular flow.</span></span> <span data-ttu-id="53845-152">它也可能表示中斷的連結。</span><span class="sxs-lookup"><span data-stu-id="53845-152">It also may indicate a broken link.</span></span> <span data-ttu-id="53845-153">Hello 中斷連結，您甚至可以實作更進階的邏輯。</span><span class="sxs-lookup"><span data-stu-id="53845-153">For hello broken links, you can even implement more advanced logic.</span></span> <span data-ttu-id="53845-154">只有當那些連結位於相同站台藉由分析 url 查閱者 hello 時，您可以中斷的連結標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="53845-154">You can mark broken links as failures only when those links are located on hello same site by analyzing url referrer.</span></span> <span data-ttu-id="53845-155">或將它們標示為失敗時從 hello 公司的行動應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="53845-155">Or mark them as failures when accessed from hello company's mobile application.</span></span> <span data-ttu-id="53845-156">同樣地`301`和`302`表示失敗時從不支援重新導向的 hello 用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="53845-156">Similarly `301` and `302` indicates failure when accessed from hello client that doesn't support redirect.</span></span>

<span data-ttu-id="53845-157">部分接受的內容 `206` 可能表示整體要求失敗。</span><span class="sxs-lookup"><span data-stu-id="53845-157">Partially accepted content `206` may indicate a failure of an overall request.</span></span> <span data-ttu-id="53845-158">例如，Application Insights 端點會接收一批遙測項目作為單一要求。</span><span class="sxs-lookup"><span data-stu-id="53845-158">For instance, Application Insights endpoint receives a batch of telemetry items as a single request.</span></span> <span data-ttu-id="53845-159">它會傳回`206`當 hello 批次中的某些項目未處理成功。</span><span class="sxs-lookup"><span data-stu-id="53845-159">It returns `206` when some items in hello batch were not processed successfully.</span></span> <span data-ttu-id="53845-160">遞增的速率`206`表示需要 toobe 調查的問題。</span><span class="sxs-lookup"><span data-stu-id="53845-160">Increasing rate of `206` indicates a problem that needs toobe investigated.</span></span> <span data-ttu-id="53845-161">類似的邏輯適用於太`207`多重狀態可能 hello 成功 hello 最差的個別的回應碼。</span><span class="sxs-lookup"><span data-stu-id="53845-161">Similar logic applies too`207` Multi-Status where hello success may be hello worst of separate response codes.</span></span>

<span data-ttu-id="53845-162">您可以讀取多個開啟的要求結果的程式碼和狀態碼 hello[部落格文章](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/)。</span><span class="sxs-lookup"><span data-stu-id="53845-162">You can read more on request result code and status code in hello [blog post](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).</span></span>

## <a name="custom-properties"></a><span data-ttu-id="53845-163">自訂屬性</span><span class="sxs-lookup"><span data-stu-id="53845-163">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="53845-164">自訂度量</span><span class="sxs-lookup"><span data-stu-id="53845-164">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="53845-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53845-165">Next steps</span></span>

- [<span data-ttu-id="53845-166">撰寫自訂要求遙測</span><span class="sxs-lookup"><span data-stu-id="53845-166">Write custom request telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackrequest)
- <span data-ttu-id="53845-167">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="53845-167">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="53845-168">了解如何太[設定 ASP.NET Core](app-insights-asp-net.md)使用 Application Insights 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53845-168">Learn how too[configure ASP.NET Core](app-insights-asp-net.md) application with Application Insights.</span></span>
- <span data-ttu-id="53845-169">查看 Application Insights 支援的[平台](app-insights-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="53845-169">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
