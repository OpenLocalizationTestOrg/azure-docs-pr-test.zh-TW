---
title: "資源使用量 API aaaProvider |Microsoft 文件"
description: "資源使用情況 API (用以擷取 Azure Stack 使用情況資訊) 的參考。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: alfredop
ms.openlocfilehash: 7cc2d7af27e6abc86e247b2ed0ab1bc236fdb1af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provider-resource-usage-api"></a><span data-ttu-id="449f0-103">提供者資源使用狀況 API</span><span class="sxs-lookup"><span data-stu-id="449f0-103">Provider Resource Usage API</span></span>
<span data-ttu-id="449f0-104">hello 詞彙提供者適用於 toohello 服務系統管理員和委派 tooany 提供者。</span><span class="sxs-lookup"><span data-stu-id="449f0-104">hello term provider applies toohello service administrator and tooany delegated providers.</span></span> <span data-ttu-id="449f0-105">服務系統管理員和委派的提供者可以使用其直接租用戶的提供者使用量 API tooview hello 使用方式。</span><span class="sxs-lookup"><span data-stu-id="449f0-105">Service admins and delegated providers can use the Provider Usage API tooview hello usage of their direct tenants.</span></span> <span data-ttu-id="449f0-106">例如，P0 可以呼叫 hello 提供者 API tooget 使用量資訊上的 P1 和 P2 的直接使用，而且 P1 可以呼叫 P3 和第 4 頁上的使用方式資訊。</span><span class="sxs-lookup"><span data-stu-id="449f0-106">For example, P0 can call hello Provider API tooget usage information on P1's and P2's direct usage, and P1 can call for usage information on P3 and P4.</span></span>

![提供者階層的概念模型](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a><span data-ttu-id="449f0-108">API 呼叫參考</span><span class="sxs-lookup"><span data-stu-id="449f0-108">API call reference</span></span>
### <a name="request"></a><span data-ttu-id="449f0-109">要求</span><span class="sxs-lookup"><span data-stu-id="449f0-109">Request</span></span>
<span data-ttu-id="449f0-110">hello 要求取得耗用量詳細資料的 hello 要求訂用帳戶，以及 hello 要求的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="449f0-110">hello request gets consumption details for hello requested subscriptions and for hello requested time frame.</span></span> <span data-ttu-id="449f0-111">沒有要求主體。</span><span class="sxs-lookup"><span data-stu-id="449f0-111">There is no request body.</span></span>

<span data-ttu-id="449f0-112">這個應用程式開發介面的使用方式是提供者 API，因此 hello 呼叫端必須指派 hello 提供者的訂用帳戶中的擁有者、 參與者或讀取器角色。</span><span class="sxs-lookup"><span data-stu-id="449f0-112">This usage API is a Provider API, so hello caller must be assigned an Owner, Contributor, or Reader role in hello provider’s subscription.</span></span>

| <span data-ttu-id="449f0-113">**方法**</span><span class="sxs-lookup"><span data-stu-id="449f0-113">**Method**</span></span> | <span data-ttu-id="449f0-114">**要求 URI**</span><span class="sxs-lookup"><span data-stu-id="449f0-114">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="449f0-115">GET</span><span class="sxs-lookup"><span data-stu-id="449f0-115">GET</span></span> |<span data-ttu-id="449f0-116">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="449f0-116">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="449f0-117">引數</span><span class="sxs-lookup"><span data-stu-id="449f0-117">Arguments</span></span>
| <span data-ttu-id="449f0-118">**引數**</span><span class="sxs-lookup"><span data-stu-id="449f0-118">**Argument**</span></span> | <span data-ttu-id="449f0-119">**說明**</span><span class="sxs-lookup"><span data-stu-id="449f0-119">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="449f0-120">*armendpoint*</span><span class="sxs-lookup"><span data-stu-id="449f0-120">*armendpoint*</span></span> |<span data-ttu-id="449f0-121">您 Azure Stack 環境的 Azure Resource Manager 端點。</span><span class="sxs-lookup"><span data-stu-id="449f0-121">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="449f0-122">hello Azure 堆疊的慣例是該 hello 名稱的 Azure 資源管理員端點的 hello 格式`https://adminmanagement.{domain-name}`。</span><span class="sxs-lookup"><span data-stu-id="449f0-122">hello Azure Stack convention is that hello name of Azure Resource Manager endpoint is in hello format `https://adminmanagement.{domain-name}`.</span></span> <span data-ttu-id="449f0-123">例如，如果 hello 網域名稱是 local.azurestack.external，則 hello 資源管理員端點是`https://adminmanagement.local.azurestack.external`。</span><span class="sxs-lookup"><span data-stu-id="449f0-123">For example, if hello domain name is local.azurestack.external, then hello Resource Manager endpoint is `https://adminmanagement.local.azurestack.external`.</span></span> |
| <span data-ttu-id="449f0-124">*subId*</span><span class="sxs-lookup"><span data-stu-id="449f0-124">*subId*</span></span> |<span data-ttu-id="449f0-125">正在進行 hello 呼叫 hello 使用者訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="449f0-125">Subscription ID of hello user who is making hello call.</span></span> |
| <span data-ttu-id="449f0-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="449f0-126">*reportedStartTime*</span></span> |<span data-ttu-id="449f0-127">Hello 查詢的開始時間。</span><span class="sxs-lookup"><span data-stu-id="449f0-127">Start time of hello query.</span></span> <span data-ttu-id="449f0-128">hello 值*DateTime*應該以 utc 格式且開頭 hello hello 小時的時間，例如： 13:00。</span><span class="sxs-lookup"><span data-stu-id="449f0-128">hello value for *DateTime* should be in UTC and at hello beginning of hello hour, for example, 13:00.</span></span> <span data-ttu-id="449f0-129">對於每日彙總，設定此值 tooUTC 午夜。</span><span class="sxs-lookup"><span data-stu-id="449f0-129">For daily aggregation, set this value tooUTC midnight.</span></span> <span data-ttu-id="449f0-130">hello 格式是*逸出*ISO 8601，例如，2015年-06-16t18%3a53%3a11%2b00 %3a00z，其中冒號會逸出太 %3a 和加上逸出太 %2b，讓它變成易記的 URI。</span><span class="sxs-lookup"><span data-stu-id="449f0-130">hello format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped too%3a and plus is escaped too%2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="449f0-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="449f0-131">*reportedEndTime*</span></span> |<span data-ttu-id="449f0-132">Hello 查詢的結束時間。</span><span class="sxs-lookup"><span data-stu-id="449f0-132">End time of hello query.</span></span> <span data-ttu-id="449f0-133">hello 太套用的條件約束*reportedStartTime*也適用於 toothis 引數。</span><span class="sxs-lookup"><span data-stu-id="449f0-133">hello constraints that apply too*reportedStartTime* also apply toothis argument.</span></span> <span data-ttu-id="449f0-134">hello 值*reportedEndTime*不可在未來的 hello 或 hello 目前的日期。</span><span class="sxs-lookup"><span data-stu-id="449f0-134">hello value for *reportedEndTime* cannot be in hello future or hello current date.</span></span> <span data-ttu-id="449f0-135">如果是，hello 結果設定太 「 處理不完整。 」</span><span class="sxs-lookup"><span data-stu-id="449f0-135">If it is, hello result is set too"processing not complete."</span></span> |
| <span data-ttu-id="449f0-136">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="449f0-136">*aggregationGranularity*</span></span> |<span data-ttu-id="449f0-137">這是選擇性引數，它可以有兩個截然不同的可能值 (每日及每小時)。</span><span class="sxs-lookup"><span data-stu-id="449f0-137">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="449f0-138">Hello 值建議，其中在每日資料粒度，則傳回 hello 資料和其他 hello 是每小時的解析度。</span><span class="sxs-lookup"><span data-stu-id="449f0-138">As hello values suggest, one returns hello data in daily granularity, and hello other is an hourly resolution.</span></span> <span data-ttu-id="449f0-139">hello 預設 hello 每日的選項。</span><span class="sxs-lookup"><span data-stu-id="449f0-139">hello daily option is hello default.</span></span> |
| <span data-ttu-id="449f0-140">*subscriberId*</span><span class="sxs-lookup"><span data-stu-id="449f0-140">*subscriberId*</span></span> |<span data-ttu-id="449f0-141">訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="449f0-141">Subscription ID.</span></span> <span data-ttu-id="449f0-142">tooget 已篩選資料，無須 hello 的直接 hello 提供者的租用戶的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="449f0-142">tooget filtered data, hello subscription ID of a direct tenant of hello provider is required.</span></span> <span data-ttu-id="449f0-143">如果訂用帳戶 ID 未不指定任何參數，hello 呼叫就會傳回所有 hello 提供者的直接租用戶使用量資料。</span><span class="sxs-lookup"><span data-stu-id="449f0-143">If no subscription ID parameter is specified, hello call returns usage data for all hello provider’s direct tenants.</span></span> |
| <span data-ttu-id="449f0-144">*api-version*</span><span class="sxs-lookup"><span data-stu-id="449f0-144">*api-version*</span></span> |<span data-ttu-id="449f0-145">使用的 toomake hello 通訊協定版本此要求。</span><span class="sxs-lookup"><span data-stu-id="449f0-145">Version of hello protocol that is used toomake this request.</span></span> <span data-ttu-id="449f0-146">這個值會設定 too2015-06-01-預覽。</span><span class="sxs-lookup"><span data-stu-id="449f0-146">This value is set too2015-06-01-preview.</span></span> |
| <span data-ttu-id="449f0-147">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="449f0-147">*continuationToken*</span></span> |<span data-ttu-id="449f0-148">從 hello 最後一個呼叫 toohello 使用量 API 提供者擷取權杖。</span><span class="sxs-lookup"><span data-stu-id="449f0-148">Token retrieved from hello last call toohello Usage API provider.</span></span> <span data-ttu-id="449f0-149">回應是大於 1000 的行，它做為 hello 進度的書籤時，就需要這個語彙基元。</span><span class="sxs-lookup"><span data-stu-id="449f0-149">This token is needed when a response is greater than 1,000 lines and it acts as a bookmark for hello progress.</span></span> <span data-ttu-id="449f0-150">如果不存在的話，會根據傳入的 hello 資料粒度的 hello 開頭的 hello 天或小時，從擷取資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="449f0-150">If not present, hello data is retrieved from hello beginning of hello day or hour, based on hello granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="449f0-151">Response</span><span class="sxs-lookup"><span data-stu-id="449f0-151">Response</span></span>
<span data-ttu-id="449f0-152">GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="449f0-152">GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0</span></span>

<span data-ttu-id="449f0-153">{</span><span class="sxs-lookup"><span data-stu-id="449f0-153">{</span></span>

<span data-ttu-id="449f0-154">"value": \[</span><span class="sxs-lookup"><span data-stu-id="449f0-154">"value": \[</span></span>

<span data-ttu-id="449f0-155">{</span><span class="sxs-lookup"><span data-stu-id="449f0-155">{</span></span>

<span data-ttu-id="449f0-156">"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-</span><span class="sxs-lookup"><span data-stu-id="449f0-156">"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-</span></span>

<span data-ttu-id="449f0-157">meterID1",</span><span class="sxs-lookup"><span data-stu-id="449f0-157">meterID1",</span></span>

<span data-ttu-id="449f0-158">"name": "sub1.1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="449f0-158">"name": "sub1.1-meterID1",</span></span>

<span data-ttu-id="449f0-159">"type": "Microsoft.Commerce/UsageAggregate",</span><span class="sxs-lookup"><span data-stu-id="449f0-159">"type": "Microsoft.Commerce/UsageAggregate",</span></span>

<span data-ttu-id="449f0-160">"properties": {</span><span class="sxs-lookup"><span data-stu-id="449f0-160">"properties": {</span></span>

<span data-ttu-id="449f0-161">"subscriptionId":"sub1.1",</span><span class="sxs-lookup"><span data-stu-id="449f0-161">"subscriptionId":"sub1.1",</span></span>

<span data-ttu-id="449f0-162">"usageStartTime": "2015-03-03T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="449f0-162">"usageStartTime": "2015-03-03T00:00:00+00:00",</span></span>

<span data-ttu-id="449f0-163">"usageEndTime": "2015-03-04T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="449f0-163">"usageEndTime": "2015-03-04T00:00:00+00:00",</span></span>

<span data-ttu-id="449f0-164">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\</span><span class="sxs-lookup"><span data-stu-id="449f0-164">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\</span></span>

<span data-ttu-id="449f0-165">":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span><span class="sxs-lookup"><span data-stu-id="449f0-165">":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span></span>

<span data-ttu-id="449f0-166">"quantity":2.4000000000,</span><span class="sxs-lookup"><span data-stu-id="449f0-166">"quantity":2.4000000000,</span></span>

<span data-ttu-id="449f0-167">"meterId":"meterID1"</span><span class="sxs-lookup"><span data-stu-id="449f0-167">"meterId":"meterID1"</span></span>

<span data-ttu-id="449f0-168">}</span><span class="sxs-lookup"><span data-stu-id="449f0-168">}</span></span>

<span data-ttu-id="449f0-169">},</span><span class="sxs-lookup"><span data-stu-id="449f0-169">},</span></span>

<span data-ttu-id="449f0-170">…</span><span class="sxs-lookup"><span data-stu-id="449f0-170">…</span></span>

### <a name="response-details"></a><span data-ttu-id="449f0-171">回應詳細資料</span><span class="sxs-lookup"><span data-stu-id="449f0-171">Response details</span></span>
| <span data-ttu-id="449f0-172">**引數**</span><span class="sxs-lookup"><span data-stu-id="449f0-172">**Argument**</span></span> | <span data-ttu-id="449f0-173">**說明**</span><span class="sxs-lookup"><span data-stu-id="449f0-173">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="449f0-174">*id*</span><span class="sxs-lookup"><span data-stu-id="449f0-174">*id*</span></span> |<span data-ttu-id="449f0-175">Hello 的彙總使用方式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="449f0-175">Unique ID of hello usage aggregate</span></span> |
| <span data-ttu-id="449f0-176">*name*</span><span class="sxs-lookup"><span data-stu-id="449f0-176">*name*</span></span> |<span data-ttu-id="449f0-177">Hello 使用量彙總名稱</span><span class="sxs-lookup"><span data-stu-id="449f0-177">Name of hello usage aggregate</span></span> |
| <span data-ttu-id="449f0-178">*type*</span><span class="sxs-lookup"><span data-stu-id="449f0-178">*type*</span></span> |<span data-ttu-id="449f0-179">資源定義</span><span class="sxs-lookup"><span data-stu-id="449f0-179">Resource definition</span></span> |
| <span data-ttu-id="449f0-180">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="449f0-180">*subscriptionId*</span></span> |<span data-ttu-id="449f0-181">Hello Azure 堆疊使用者訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="449f0-181">Subscription identifier of hello Azure Stack user</span></span> |
| <span data-ttu-id="449f0-182">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="449f0-182">*usageStartTime*</span></span> |<span data-ttu-id="449f0-183">UTC 的開始時間 hello 這個使用方式彙總所屬的使用方式值區 toowhich</span><span class="sxs-lookup"><span data-stu-id="449f0-183">UTC start time of hello usage bucket toowhich this usage aggregate belongs</span></span> |
| <span data-ttu-id="449f0-184">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="449f0-184">*usageEndTime*</span></span> |<span data-ttu-id="449f0-185">UTC 結束時間的這個使用方式彙總所屬的 hello 使用量值區 toowhich</span><span class="sxs-lookup"><span data-stu-id="449f0-185">UTC end time of hello usage bucket toowhich this usage aggregate belongs</span></span> |
| <span data-ttu-id="449f0-186">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="449f0-186">*instanceData*</span></span> |<span data-ttu-id="449f0-187">執行個體詳細資料的機碼值組 (新格式)：</span><span class="sxs-lookup"><span data-stu-id="449f0-187">Key-value pairs of instance details (in a new format):</span></span><br> <span data-ttu-id="449f0-188">*resourceUri*： 完整資源識別碼，其中包括 hello 資源群組和 hello 執行個體名稱</span><span class="sxs-lookup"><span data-stu-id="449f0-188">*resourceUri*: Fully qualified resource ID, which includes hello resource groups and hello instance name</span></span> <br> <span data-ttu-id="449f0-189">*location*：此服務執行所在的區域</span><span class="sxs-lookup"><span data-stu-id="449f0-189">*location*: Region in which this service was run</span></span> <br> <span data-ttu-id="449f0-190">*標記*: hello 使用者所指定資源標記</span><span class="sxs-lookup"><span data-stu-id="449f0-190">*tags*: Resource tags that are specified by hello user</span></span> <br> <span data-ttu-id="449f0-191">*additionalInfo*： 更詳細 hello 資源耗用，例如作業系統版本或映像類型</span><span class="sxs-lookup"><span data-stu-id="449f0-191">*additionalInfo*: More details about hello resource that was consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="449f0-192">*quantity*</span><span class="sxs-lookup"><span data-stu-id="449f0-192">*quantity*</span></span> |<span data-ttu-id="449f0-193">此時間範圍內發生的資源取用數量</span><span class="sxs-lookup"><span data-stu-id="449f0-193">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="449f0-194">*meterId*</span><span class="sxs-lookup"><span data-stu-id="449f0-194">*meterId*</span></span> |<span data-ttu-id="449f0-195">所耗用的 hello 資源的唯一識別碼 (也稱為*ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="449f0-195">Unique ID for hello resource that was consumed (also called *ResourceID*)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="449f0-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="449f0-196">Next steps</span></span>
[<span data-ttu-id="449f0-197">租用戶資源使用狀況 API 參考</span><span class="sxs-lookup"><span data-stu-id="449f0-197">Tenant resource usage API reference</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="449f0-198">使用狀況相關常見問題集</span><span class="sxs-lookup"><span data-stu-id="449f0-198">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

