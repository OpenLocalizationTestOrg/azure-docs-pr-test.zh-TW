---
title: "資源使用量 API aaaTenant |Microsoft 文件"
description: "資源使用情況 API (用以擷取 Azure Stack 使用情況資訊) 的參考。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b9d7c7ee-e906-4978-92a3-a2c52df16c36
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: eb826aba87b3b5b79155d9003162f2b5e6871f82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tenant-resource-usage-api"></a><span data-ttu-id="03e3a-103">租用戶資源使用情況 API</span><span class="sxs-lookup"><span data-stu-id="03e3a-103">Tenant Resource Usage API</span></span>
<span data-ttu-id="03e3a-104">租用戶可以使用 hello 租用戶 API tooview hello 租用戶專屬的資源使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="03e3a-104">A tenant can use hello Tenant API tooview hello tenant’s own resource usage data.</span></span> <span data-ttu-id="03e3a-105">這個 API 已與 hello Azure 使用量 API 一致 （目前在私人預覽中）。</span><span class="sxs-lookup"><span data-stu-id="03e3a-105">This API is consistent with hello Azure Usage API (currently in private preview).</span></span>

<span data-ttu-id="03e3a-106">您可以使用 hello Windows PowerShell cmdlet **Get UsageAggregates** tooget 使用量資料會像在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="03e3a-106">You can use hello Windows PowerShell cmdlet **Get-UsageAggregates** tooget usage data like in Azure.</span></span>

## <a name="api-call"></a><span data-ttu-id="03e3a-107">API 呼叫</span><span class="sxs-lookup"><span data-stu-id="03e3a-107">API call</span></span>
### <a name="request"></a><span data-ttu-id="03e3a-108">要求</span><span class="sxs-lookup"><span data-stu-id="03e3a-108">Request</span></span>
<span data-ttu-id="03e3a-109">hello 要求取得耗用量詳細資料的 hello 要求訂用帳戶，以及 hello 要求的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="03e3a-109">hello request gets consumption details for hello requested subscriptions and for hello requested time frame.</span></span> <span data-ttu-id="03e3a-110">沒有要求主體。</span><span class="sxs-lookup"><span data-stu-id="03e3a-110">There is no request body.</span></span>

| <span data-ttu-id="03e3a-111">**方法**</span><span class="sxs-lookup"><span data-stu-id="03e3a-111">**Method**</span></span> | <span data-ttu-id="03e3a-112">**要求 URI**</span><span class="sxs-lookup"><span data-stu-id="03e3a-112">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="03e3a-113">GET</span><span class="sxs-lookup"><span data-stu-id="03e3a-113">GET</span></span> |<span data-ttu-id="03e3a-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="03e3a-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="03e3a-115">引數</span><span class="sxs-lookup"><span data-stu-id="03e3a-115">Arguments</span></span>
| <span data-ttu-id="03e3a-116">**引數**</span><span class="sxs-lookup"><span data-stu-id="03e3a-116">**Argument**</span></span> | <span data-ttu-id="03e3a-117">**說明**</span><span class="sxs-lookup"><span data-stu-id="03e3a-117">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="03e3a-118">*Armendpoint*</span><span class="sxs-lookup"><span data-stu-id="03e3a-118">*Armendpoint*</span></span> |<span data-ttu-id="03e3a-119">您 Azure Stack 環境的 Azure Resource Manager 端點。</span><span class="sxs-lookup"><span data-stu-id="03e3a-119">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="03e3a-120">hello Azure 堆疊的慣例是該 hello 名稱的 Azure 資源管理員端點的 hello 格式`https://management.{domain-name}`。</span><span class="sxs-lookup"><span data-stu-id="03e3a-120">hello Azure Stack convention is that hello name of Azure Resource Manager endpoint is in hello format `https://management.{domain-name}`.</span></span> <span data-ttu-id="03e3a-121">例如，如果 hello 網域名稱是 local.azurestack.external，則 hello 資源管理員端點是`https://management.local.azurestack.external`。</span><span class="sxs-lookup"><span data-stu-id="03e3a-121">For example, if hello domain name is local.azurestack.external, then hello Resource Manager  endpoint is `https://management.local.azurestack.external`.</span></span> |
| <span data-ttu-id="03e3a-122">*subId*</span><span class="sxs-lookup"><span data-stu-id="03e3a-122">*subId*</span></span> |<span data-ttu-id="03e3a-123">正在進行 hello 呼叫 hello 使用者訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="03e3a-123">Subscription ID of hello user who is making hello call.</span></span> <span data-ttu-id="03e3a-124">您可以使用此 API 只有 tooquery 單一訂用帳戶的使用方式。</span><span class="sxs-lookup"><span data-stu-id="03e3a-124">You can use this API only tooquery for a single subscription’s usage.</span></span> <span data-ttu-id="03e3a-125">提供者可以針對所有租用戶使用 hello 提供者資源使用量 API tooquery 使用方式。</span><span class="sxs-lookup"><span data-stu-id="03e3a-125">Providers can use hello Provider Resource Usage API tooquery usage for all tenants.</span></span> |
| <span data-ttu-id="03e3a-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="03e3a-126">*reportedStartTime*</span></span> |<span data-ttu-id="03e3a-127">Hello 查詢的開始時間。</span><span class="sxs-lookup"><span data-stu-id="03e3a-127">Start time of hello query.</span></span> <span data-ttu-id="03e3a-128">hello 值*DateTime*應該以 utc 格式且開頭 hello hello 小時的時間，例如： 13:00。</span><span class="sxs-lookup"><span data-stu-id="03e3a-128">hello value for *DateTime* should be in UTC and at hello beginning of hello hour, for example, 13:00.</span></span> <span data-ttu-id="03e3a-129">對於每日彙總，設定此值 tooUTC 午夜。</span><span class="sxs-lookup"><span data-stu-id="03e3a-129">For daily aggregation, set this value tooUTC midnight.</span></span> <span data-ttu-id="03e3a-130">hello 格式是*逸出*ISO 8601，例如，2015年-06-16t18%3a53%3a11%2b00 %3a00z，其中冒號會逸出太 %3a 和加上逸出太 %2b，讓它變成易記的 URI。</span><span class="sxs-lookup"><span data-stu-id="03e3a-130">hello format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped too%3a and plus is escaped too%2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="03e3a-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="03e3a-131">*reportedEndTime*</span></span> |<span data-ttu-id="03e3a-132">Hello 查詢的結束時間。</span><span class="sxs-lookup"><span data-stu-id="03e3a-132">End time of hello query.</span></span> <span data-ttu-id="03e3a-133">hello 太套用的條件約束*reportedStartTime*也適用於 toothis 引數。</span><span class="sxs-lookup"><span data-stu-id="03e3a-133">hello constraints that apply too*reportedStartTime* also apply toothis argument.</span></span> <span data-ttu-id="03e3a-134">hello 值*reportedEndTime*不可在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="03e3a-134">hello value for *reportedEndTime* cannot be in hello future.</span></span> |
| <span data-ttu-id="03e3a-135">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="03e3a-135">*aggregationGranularity*</span></span> |<span data-ttu-id="03e3a-136">這是選擇性引數，它可以有兩個截然不同的可能值 (每日及每小時)。</span><span class="sxs-lookup"><span data-stu-id="03e3a-136">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="03e3a-137">Hello 值建議，其中在每日資料粒度，則傳回 hello 資料和其他 hello 是每小時的解析度。</span><span class="sxs-lookup"><span data-stu-id="03e3a-137">As hello values suggest, one returns hello data in daily granularity, and hello other is an hourly resolution.</span></span> <span data-ttu-id="03e3a-138">hello 預設 hello 每日的選項。</span><span class="sxs-lookup"><span data-stu-id="03e3a-138">hello daily option is hello default.</span></span> |
| <span data-ttu-id="03e3a-139">*api-version*</span><span class="sxs-lookup"><span data-stu-id="03e3a-139">*api-version*</span></span> |<span data-ttu-id="03e3a-140">使用的 toomake hello 通訊協定版本此要求。</span><span class="sxs-lookup"><span data-stu-id="03e3a-140">Version of hello protocol that is used toomake this request.</span></span> <span data-ttu-id="03e3a-141">您必須使用 2015-06-01-preview。</span><span class="sxs-lookup"><span data-stu-id="03e3a-141">You must use 2015-06-01-preview.</span></span> |
| <span data-ttu-id="03e3a-142">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="03e3a-142">*continuationToken*</span></span> |<span data-ttu-id="03e3a-143">從 hello 最後一個呼叫 toohello 使用量 API 提供者擷取權杖。</span><span class="sxs-lookup"><span data-stu-id="03e3a-143">Token retrieved from hello last call toohello Usage API provider.</span></span> <span data-ttu-id="03e3a-144">回應大於 1000 行時就需要這個權杖，可作為進度的書籤。</span><span class="sxs-lookup"><span data-stu-id="03e3a-144">This token is needed when a response is greater than 1,000 lines and it acts as a bookmark for progress.</span></span> <span data-ttu-id="03e3a-145">如果不存在的話，會根據傳入的 hello 資料粒度的 hello 開頭的 hello 天或小時，從擷取資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="03e3a-145">If not present, hello data is retrieved from hello beginning of hello day or hour, based on hello granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="03e3a-146">Response</span><span class="sxs-lookup"><span data-stu-id="03e3a-146">Response</span></span>
<span data-ttu-id="03e3a-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="03e3a-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span></span>

<span data-ttu-id="03e3a-148">{</span><span class="sxs-lookup"><span data-stu-id="03e3a-148">{</span></span>

<span data-ttu-id="03e3a-149">"value": \[</span><span class="sxs-lookup"><span data-stu-id="03e3a-149">"value": \[</span></span>

<span data-ttu-id="03e3a-150">{</span><span class="sxs-lookup"><span data-stu-id="03e3a-150">{</span></span>

<span data-ttu-id="03e3a-151">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="03e3a-151">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span></span>

<span data-ttu-id="03e3a-152">"name": "sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="03e3a-152">"name": "sub1-meterID1",</span></span>

<span data-ttu-id="03e3a-153">"type": "Microsoft.Commerce/UsageAggregate",</span><span class="sxs-lookup"><span data-stu-id="03e3a-153">"type": "Microsoft.Commerce/UsageAggregate",</span></span>

<span data-ttu-id="03e3a-154">"properties": {</span><span class="sxs-lookup"><span data-stu-id="03e3a-154">"properties": {</span></span>

<span data-ttu-id="03e3a-155">"subscriptionId":"sub1",</span><span class="sxs-lookup"><span data-stu-id="03e3a-155">"subscriptionId":"sub1",</span></span>

<span data-ttu-id="03e3a-156">"usageStartTime": "2015-03-03T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="03e3a-156">"usageStartTime": "2015-03-03T00:00:00+00:00",</span></span>

<span data-ttu-id="03e3a-157">"usageEndTime": "2015-03-04T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="03e3a-157">"usageEndTime": "2015-03-04T00:00:00+00:00",</span></span>

<span data-ttu-id="03e3a-158">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span><span class="sxs-lookup"><span data-stu-id="03e3a-158">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span></span>

<span data-ttu-id="03e3a-159">"quantity":2.4000000000,</span><span class="sxs-lookup"><span data-stu-id="03e3a-159">"quantity":2.4000000000,</span></span>

<span data-ttu-id="03e3a-160">"meterId":"meterID1"</span><span class="sxs-lookup"><span data-stu-id="03e3a-160">"meterId":"meterID1"</span></span>

<span data-ttu-id="03e3a-161">}</span><span class="sxs-lookup"><span data-stu-id="03e3a-161">}</span></span>

<span data-ttu-id="03e3a-162">},</span><span class="sxs-lookup"><span data-stu-id="03e3a-162">},</span></span>

<span data-ttu-id="03e3a-163">…</span><span class="sxs-lookup"><span data-stu-id="03e3a-163">…</span></span>

### <a name="response-details"></a><span data-ttu-id="03e3a-164">回應詳細資料</span><span class="sxs-lookup"><span data-stu-id="03e3a-164">Response details</span></span>
| <span data-ttu-id="03e3a-165">**引數**</span><span class="sxs-lookup"><span data-stu-id="03e3a-165">**Argument**</span></span> | <span data-ttu-id="03e3a-166">**說明**</span><span class="sxs-lookup"><span data-stu-id="03e3a-166">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="03e3a-167">*id*</span><span class="sxs-lookup"><span data-stu-id="03e3a-167">*id*</span></span> |<span data-ttu-id="03e3a-168">Hello 的彙總使用方式的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="03e3a-168">Unique ID of hello usage aggregate</span></span> |
| <span data-ttu-id="03e3a-169">*name*</span><span class="sxs-lookup"><span data-stu-id="03e3a-169">*name*</span></span> |<span data-ttu-id="03e3a-170">Hello 使用量彙總名稱</span><span class="sxs-lookup"><span data-stu-id="03e3a-170">Name of hello usage aggregate</span></span> |
| <span data-ttu-id="03e3a-171">*type*</span><span class="sxs-lookup"><span data-stu-id="03e3a-171">*type*</span></span> |<span data-ttu-id="03e3a-172">資源定義</span><span class="sxs-lookup"><span data-stu-id="03e3a-172">Resource definition</span></span> |
| <span data-ttu-id="03e3a-173">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="03e3a-173">*subscriptionId*</span></span> |<span data-ttu-id="03e3a-174">Hello Azure 使用者的訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="03e3a-174">Subscription identifier of hello Azure user</span></span> |
| <span data-ttu-id="03e3a-175">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="03e3a-175">*usageStartTime*</span></span> |<span data-ttu-id="03e3a-176">UTC 的開始時間 hello 這個使用方式彙總所屬的使用方式值區 toowhich</span><span class="sxs-lookup"><span data-stu-id="03e3a-176">UTC start time of hello usage bucket toowhich this usage aggregate belongs</span></span> |
| <span data-ttu-id="03e3a-177">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="03e3a-177">*usageEndTime*</span></span> |<span data-ttu-id="03e3a-178">UTC 結束時間的這個使用方式彙總所屬的 hello 使用量值區 toowhich</span><span class="sxs-lookup"><span data-stu-id="03e3a-178">UTC end time of hello usage bucket toowhich this usage aggregate belongs</span></span> |
| <span data-ttu-id="03e3a-179">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="03e3a-179">*instanceData*</span></span> |<span data-ttu-id="03e3a-180">執行個體詳細資料的機碼值組 (新格式)：</span><span class="sxs-lookup"><span data-stu-id="03e3a-180">Key-value pairs of instance details (in a new format):</span></span><br>  <span data-ttu-id="03e3a-181">*resourceUri*：完整資源識別碼，包含資源群組和執行個體名稱</span><span class="sxs-lookup"><span data-stu-id="03e3a-181">*resourceUri*: Fully qualified resource ID, including resource groups and instance name</span></span> <br>  <span data-ttu-id="03e3a-182">*location*：此服務執行所在的區域</span><span class="sxs-lookup"><span data-stu-id="03e3a-182">*location*: Region in which this service was run</span></span> <br>  <span data-ttu-id="03e3a-183">*標記*： 該 hello 使用者所指定的資源標記</span><span class="sxs-lookup"><span data-stu-id="03e3a-183">*tags*: Resource tags that hello user specifies</span></span> <br>  <span data-ttu-id="03e3a-184">*additionalInfo*： 更詳細 hello 資源耗用，例如作業系統版本或映像類型</span><span class="sxs-lookup"><span data-stu-id="03e3a-184">*additionalInfo*: More details about hello resource that was consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="03e3a-185">*quantity*</span><span class="sxs-lookup"><span data-stu-id="03e3a-185">*quantity*</span></span> |<span data-ttu-id="03e3a-186">此時間範圍內發生的資源取用數量</span><span class="sxs-lookup"><span data-stu-id="03e3a-186">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="03e3a-187">*meterId*</span><span class="sxs-lookup"><span data-stu-id="03e3a-187">*meterId*</span></span> |<span data-ttu-id="03e3a-188">所耗用的 hello 資源的唯一識別碼 (也稱為*ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="03e3a-188">Unique ID for hello resource that was consumed (also called *ResourceID*)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="03e3a-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03e3a-189">Next steps</span></span>
[<span data-ttu-id="03e3a-190">提供者資源使用狀況 API</span><span class="sxs-lookup"><span data-stu-id="03e3a-190">Provider resource usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="03e3a-191">使用狀況相關常見問題集</span><span class="sxs-lookup"><span data-stu-id="03e3a-191">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

