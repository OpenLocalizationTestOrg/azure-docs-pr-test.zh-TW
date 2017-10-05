---
title: "提供者資源使用狀況 API | Microsoft Docs"
description: "資源使用狀況 API (用以擷取 Azure Stack 使用狀況資訊) 的參考。"
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
ms.openlocfilehash: f43ec070e0269fad89b83c3075101e610a90ad96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="provider-resource-usage-api"></a><span data-ttu-id="e5e26-103">提供者資源使用狀況 API</span><span class="sxs-lookup"><span data-stu-id="e5e26-103">Provider Resource Usage API</span></span>
<span data-ttu-id="e5e26-104">「提供者」一詞適用於服務管理員和任何委派的提供者。</span><span class="sxs-lookup"><span data-stu-id="e5e26-104">The term provider applies to the service administrator and to any delegated providers.</span></span> <span data-ttu-id="e5e26-105">服務系統管理員和委派的提供者可以使用提供者使用量 API，來檢視其直接租用戶的使用方式。</span><span class="sxs-lookup"><span data-stu-id="e5e26-105">Service admins and delegated providers can use the Provider Usage API to view the usage of their direct tenants.</span></span> <span data-ttu-id="e5e26-106">例如，P0 可以呼叫提供者 API，以取得 P1 和 P2 直接使用的使用狀況資訊；而 P1 可呼叫以取得 P3 和 P4 的使用狀況資訊。</span><span class="sxs-lookup"><span data-stu-id="e5e26-106">For example, P0 can call the Provider API to get usage information on P1's and P2's direct usage, and P1 can call for usage information on P3 and P4.</span></span>

![提供者階層的概念模型](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a><span data-ttu-id="e5e26-108">API 呼叫參考</span><span class="sxs-lookup"><span data-stu-id="e5e26-108">API call reference</span></span>
### <a name="request"></a><span data-ttu-id="e5e26-109">要求</span><span class="sxs-lookup"><span data-stu-id="e5e26-109">Request</span></span>
<span data-ttu-id="e5e26-110">要求會取得所要求的訂用帳戶在要求的時間範圍內的耗用量詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e5e26-110">The request gets consumption details for the requested subscriptions and for the requested time frame.</span></span> <span data-ttu-id="e5e26-111">沒有要求主體。</span><span class="sxs-lookup"><span data-stu-id="e5e26-111">There is no request body.</span></span>

<span data-ttu-id="e5e26-112">此使用狀況 API 是提供者 API，因此必須將提供者訂用帳戶中的「擁有者」、「參與者」或「讀者」角色指派給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="e5e26-112">This usage API is a Provider API, so the caller must be assigned an Owner, Contributor, or Reader role in the provider’s subscription.</span></span>

| <span data-ttu-id="e5e26-113">**方法**</span><span class="sxs-lookup"><span data-stu-id="e5e26-113">**Method**</span></span> | <span data-ttu-id="e5e26-114">**要求 URI**</span><span class="sxs-lookup"><span data-stu-id="e5e26-114">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="e5e26-115">GET</span><span class="sxs-lookup"><span data-stu-id="e5e26-115">GET</span></span> |<span data-ttu-id="e5e26-116">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="e5e26-116">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="e5e26-117">引數</span><span class="sxs-lookup"><span data-stu-id="e5e26-117">Arguments</span></span>
| <span data-ttu-id="e5e26-118">**引數**</span><span class="sxs-lookup"><span data-stu-id="e5e26-118">**Argument**</span></span> | <span data-ttu-id="e5e26-119">**說明**</span><span class="sxs-lookup"><span data-stu-id="e5e26-119">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e5e26-120">*armendpoint*</span><span class="sxs-lookup"><span data-stu-id="e5e26-120">*armendpoint*</span></span> |<span data-ttu-id="e5e26-121">您 Azure Stack 環境的 Azure Resource Manager 端點。</span><span class="sxs-lookup"><span data-stu-id="e5e26-121">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="e5e26-122">依 Azure Stack 慣例，Azure Resource Manager 端點名稱的格式是 `https://adminmanagement.{domain-name}`。</span><span class="sxs-lookup"><span data-stu-id="e5e26-122">The Azure Stack convention is that the name of Azure Resource Manager endpoint is in the format `https://adminmanagement.{domain-name}`.</span></span> <span data-ttu-id="e5e26-123">例如，如果網域名稱是 local.azurestack.external，則 Resource Manager 端點名稱是 `https://adminmanagement.local.azurestack.external`。</span><span class="sxs-lookup"><span data-stu-id="e5e26-123">For example, if the domain name is local.azurestack.external, then the Resource Manager endpoint is `https://adminmanagement.local.azurestack.external`.</span></span> |
| <span data-ttu-id="e5e26-124">*subId*</span><span class="sxs-lookup"><span data-stu-id="e5e26-124">*subId*</span></span> |<span data-ttu-id="e5e26-125">正在進行呼叫的使用者訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e5e26-125">Subscription ID of the user who is making the call.</span></span> |
| <span data-ttu-id="e5e26-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="e5e26-126">*reportedStartTime*</span></span> |<span data-ttu-id="e5e26-127">查詢的開始時間。</span><span class="sxs-lookup"><span data-stu-id="e5e26-127">Start time of the query.</span></span> <span data-ttu-id="e5e26-128">*DateTime* 值應該以 UTC 格式及小時開始時的時間呈現，例如 13:00。</span><span class="sxs-lookup"><span data-stu-id="e5e26-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span></span> <span data-ttu-id="e5e26-129">對於每日彙總，請將這個值設定為 UTC 午夜。</span><span class="sxs-lookup"><span data-stu-id="e5e26-129">For daily aggregation, set this value to UTC midnight.</span></span> <span data-ttu-id="e5e26-130">格式是*逸出的* ISO 8601，例如 2015-06-16T18%3a53%3a11%2b00%3a00Z，其中冒號會逸出為 %3a 而加號會逸出為 %2b，使其符合 URI 規範。</span><span class="sxs-lookup"><span data-stu-id="e5e26-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="e5e26-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="e5e26-131">*reportedEndTime*</span></span> |<span data-ttu-id="e5e26-132">查詢的結束時間。</span><span class="sxs-lookup"><span data-stu-id="e5e26-132">End time of the query.</span></span> <span data-ttu-id="e5e26-133">適用於 *reportedStartTime* 的限制也適用於此引數。</span><span class="sxs-lookup"><span data-stu-id="e5e26-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span></span> <span data-ttu-id="e5e26-134">*reportedEndTime* 的值不得為未來或目前的日期。</span><span class="sxs-lookup"><span data-stu-id="e5e26-134">The value for *reportedEndTime* cannot be in the future or the current date.</span></span> <span data-ttu-id="e5e26-135">如果是，結果會設為「處理未完成。」</span><span class="sxs-lookup"><span data-stu-id="e5e26-135">If it is, the result is set to "processing not complete."</span></span> |
| <span data-ttu-id="e5e26-136">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="e5e26-136">*aggregationGranularity*</span></span> |<span data-ttu-id="e5e26-137">這是選擇性引數，它可以有兩個截然不同的可能值 (每日及每小時)。</span><span class="sxs-lookup"><span data-stu-id="e5e26-137">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="e5e26-138">如同以上兩個值所暗示，一個會每日傳回資料，另一個則會每小時傳回資料。</span><span class="sxs-lookup"><span data-stu-id="e5e26-138">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span></span> <span data-ttu-id="e5e26-139">預設值為 [每日] 選項。</span><span class="sxs-lookup"><span data-stu-id="e5e26-139">The daily option is the default.</span></span> |
| <span data-ttu-id="e5e26-140">*subscriberId*</span><span class="sxs-lookup"><span data-stu-id="e5e26-140">*subscriberId*</span></span> |<span data-ttu-id="e5e26-141">訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e5e26-141">Subscription ID.</span></span> <span data-ttu-id="e5e26-142">若要取得篩選的資料，需要提供者的直接租用戶訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e5e26-142">To get filtered data, the subscription ID of a direct tenant of the provider is required.</span></span> <span data-ttu-id="e5e26-143">如果未指定訂用帳戶 ID 參數，呼叫會傳回所有提供者直接租用戶的使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="e5e26-143">If no subscription ID parameter is specified, the call returns usage data for all the provider’s direct tenants.</span></span> |
| <span data-ttu-id="e5e26-144">*api-version*</span><span class="sxs-lookup"><span data-stu-id="e5e26-144">*api-version*</span></span> |<span data-ttu-id="e5e26-145">用來提出此要求的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="e5e26-145">Version of the protocol that is used to make this request.</span></span> <span data-ttu-id="e5e26-146">此值會設定為 2015-06-01-preview。</span><span class="sxs-lookup"><span data-stu-id="e5e26-146">This value is set to 2015-06-01-preview.</span></span> |
| <span data-ttu-id="e5e26-147">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="e5e26-147">*continuationToken*</span></span> |<span data-ttu-id="e5e26-148">從上次呼叫使用狀況 API 提供者所擷取的權杖。</span><span class="sxs-lookup"><span data-stu-id="e5e26-148">Token retrieved from the last call to the Usage API provider.</span></span> <span data-ttu-id="e5e26-149">回應大於 1000 行時就需要這個權杖，可作為進度的書籤。</span><span class="sxs-lookup"><span data-stu-id="e5e26-149">This token is needed when a response is greater than 1,000 lines and it acts as a bookmark for the progress.</span></span> <span data-ttu-id="e5e26-150">若無此權杖，則會從一天或小時開始時的時間擷取資料，取決於所傳遞的細微性。</span><span class="sxs-lookup"><span data-stu-id="e5e26-150">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="e5e26-151">Response</span><span class="sxs-lookup"><span data-stu-id="e5e26-151">Response</span></span>
<span data-ttu-id="e5e26-152">GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="e5e26-152">GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0</span></span>

<span data-ttu-id="e5e26-153">{</span><span class="sxs-lookup"><span data-stu-id="e5e26-153">{</span></span>

<span data-ttu-id="e5e26-154">"value": \[</span><span class="sxs-lookup"><span data-stu-id="e5e26-154">"value": \[</span></span>

<span data-ttu-id="e5e26-155">{</span><span class="sxs-lookup"><span data-stu-id="e5e26-155">{</span></span>

<span data-ttu-id="e5e26-156">"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-</span><span class="sxs-lookup"><span data-stu-id="e5e26-156">"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-</span></span>

<span data-ttu-id="e5e26-157">meterID1",</span><span class="sxs-lookup"><span data-stu-id="e5e26-157">meterID1",</span></span>

<span data-ttu-id="e5e26-158">"name": "sub1.1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="e5e26-158">"name": "sub1.1-meterID1",</span></span>

<span data-ttu-id="e5e26-159">"type": "Microsoft.Commerce/UsageAggregate",</span><span class="sxs-lookup"><span data-stu-id="e5e26-159">"type": "Microsoft.Commerce/UsageAggregate",</span></span>

<span data-ttu-id="e5e26-160">"properties": {</span><span class="sxs-lookup"><span data-stu-id="e5e26-160">"properties": {</span></span>

<span data-ttu-id="e5e26-161">"subscriptionId":"sub1.1",</span><span class="sxs-lookup"><span data-stu-id="e5e26-161">"subscriptionId":"sub1.1",</span></span>

<span data-ttu-id="e5e26-162">"usageStartTime": "2015-03-03T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="e5e26-162">"usageStartTime": "2015-03-03T00:00:00+00:00",</span></span>

<span data-ttu-id="e5e26-163">"usageEndTime": "2015-03-04T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="e5e26-163">"usageEndTime": "2015-03-04T00:00:00+00:00",</span></span>

<span data-ttu-id="e5e26-164">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\</span><span class="sxs-lookup"><span data-stu-id="e5e26-164">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\</span></span>

<span data-ttu-id="e5e26-165">":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span><span class="sxs-lookup"><span data-stu-id="e5e26-165">":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span></span>

<span data-ttu-id="e5e26-166">"quantity":2.4000000000,</span><span class="sxs-lookup"><span data-stu-id="e5e26-166">"quantity":2.4000000000,</span></span>

<span data-ttu-id="e5e26-167">"meterId":"meterID1"</span><span class="sxs-lookup"><span data-stu-id="e5e26-167">"meterId":"meterID1"</span></span>

<span data-ttu-id="e5e26-168">}</span><span class="sxs-lookup"><span data-stu-id="e5e26-168">}</span></span>

<span data-ttu-id="e5e26-169">},</span><span class="sxs-lookup"><span data-stu-id="e5e26-169">},</span></span>

<span data-ttu-id="e5e26-170">…</span><span class="sxs-lookup"><span data-stu-id="e5e26-170">…</span></span>

### <a name="response-details"></a><span data-ttu-id="e5e26-171">回應詳細資料</span><span class="sxs-lookup"><span data-stu-id="e5e26-171">Response details</span></span>
| <span data-ttu-id="e5e26-172">**引數**</span><span class="sxs-lookup"><span data-stu-id="e5e26-172">**Argument**</span></span> | <span data-ttu-id="e5e26-173">**說明**</span><span class="sxs-lookup"><span data-stu-id="e5e26-173">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e5e26-174">*id*</span><span class="sxs-lookup"><span data-stu-id="e5e26-174">*id*</span></span> |<span data-ttu-id="e5e26-175">使用情況彙總的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e5e26-175">Unique ID of the usage aggregate</span></span> |
| <span data-ttu-id="e5e26-176">*name*</span><span class="sxs-lookup"><span data-stu-id="e5e26-176">*name*</span></span> |<span data-ttu-id="e5e26-177">使用情況彙總的名稱</span><span class="sxs-lookup"><span data-stu-id="e5e26-177">Name of the usage aggregate</span></span> |
| <span data-ttu-id="e5e26-178">*type*</span><span class="sxs-lookup"><span data-stu-id="e5e26-178">*type*</span></span> |<span data-ttu-id="e5e26-179">資源定義</span><span class="sxs-lookup"><span data-stu-id="e5e26-179">Resource definition</span></span> |
| <span data-ttu-id="e5e26-180">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="e5e26-180">*subscriptionId*</span></span> |<span data-ttu-id="e5e26-181">Azure Stack 使用者訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e5e26-181">Subscription identifier of the Azure Stack user</span></span> |
| <span data-ttu-id="e5e26-182">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="e5e26-182">*usageStartTime*</span></span> |<span data-ttu-id="e5e26-183">此使用情況彙總所屬的使用情況貯體 UTC 開始時間</span><span class="sxs-lookup"><span data-stu-id="e5e26-183">UTC start time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="e5e26-184">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="e5e26-184">*usageEndTime*</span></span> |<span data-ttu-id="e5e26-185">此使用情況彙總所屬的使用情況貯體 UTC 結束時間</span><span class="sxs-lookup"><span data-stu-id="e5e26-185">UTC end time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="e5e26-186">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="e5e26-186">*instanceData*</span></span> |<span data-ttu-id="e5e26-187">執行個體詳細資料的機碼值組 (新格式)：</span><span class="sxs-lookup"><span data-stu-id="e5e26-187">Key-value pairs of instance details (in a new format):</span></span><br> <span data-ttu-id="e5e26-188">*resourceUri*：完整資源 ID，包含資源群組和執行個體名稱</span><span class="sxs-lookup"><span data-stu-id="e5e26-188">*resourceUri*: Fully qualified resource ID, which includes the resource groups and the instance name</span></span> <br> <span data-ttu-id="e5e26-189">*location*：此服務執行所在的區域</span><span class="sxs-lookup"><span data-stu-id="e5e26-189">*location*: Region in which this service was run</span></span> <br> <span data-ttu-id="e5e26-190">*tags*：使用者所指定的資源標記</span><span class="sxs-lookup"><span data-stu-id="e5e26-190">*tags*: Resource tags that are specified by the user</span></span> <br> <span data-ttu-id="e5e26-191">*additionalInfo*：更多關於所耗用資源的詳細資料 (例如，作業系統版本或映像類型)</span><span class="sxs-lookup"><span data-stu-id="e5e26-191">*additionalInfo*: More details about the resource that was consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="e5e26-192">*quantity*</span><span class="sxs-lookup"><span data-stu-id="e5e26-192">*quantity*</span></span> |<span data-ttu-id="e5e26-193">此時間範圍內發生的資源取用數量</span><span class="sxs-lookup"><span data-stu-id="e5e26-193">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="e5e26-194">*meterId*</span><span class="sxs-lookup"><span data-stu-id="e5e26-194">*meterId*</span></span> |<span data-ttu-id="e5e26-195">所取用資源的唯一識別碼 ( *ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="e5e26-195">Unique ID for the resource that was consumed (also called *ResourceID*)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e5e26-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5e26-196">Next steps</span></span>
[<span data-ttu-id="e5e26-197">租用戶資源使用狀況 API 參考</span><span class="sxs-lookup"><span data-stu-id="e5e26-197">Tenant resource usage API reference</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="e5e26-198">使用狀況相關常見問題集</span><span class="sxs-lookup"><span data-stu-id="e5e26-198">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

