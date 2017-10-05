---
title: "租用戶資源使用情況 API | Microsoft Docs"
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
ms.openlocfilehash: 0ad10564e631f9079b2544a6888c1d0dc467d7ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tenant-resource-usage-api"></a><span data-ttu-id="e7ec0-103">租用戶資源使用情況 API</span><span class="sxs-lookup"><span data-stu-id="e7ec0-103">Tenant Resource Usage API</span></span>
<span data-ttu-id="e7ec0-104">租用戶可以使用租用戶 API 來檢視租用戶的資源使用量資料。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-104">A tenant can use the Tenant API to view the tenant’s own resource usage data.</span></span> <span data-ttu-id="e7ec0-105">此 API 與 Azure 使用情況 API (目前處於私人預覽狀態) 一致。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-105">This API is consistent with the Azure Usage API (currently in private preview).</span></span>

<span data-ttu-id="e7ec0-106">您可以像在 Azure 中一樣，使用 Windows PowerShell Cmdlet **Get-UsageAggregates** 取得使用量資料。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-106">You can use the Windows PowerShell cmdlet **Get-UsageAggregates** to get usage data like in Azure.</span></span>

## <a name="api-call"></a><span data-ttu-id="e7ec0-107">API 呼叫</span><span class="sxs-lookup"><span data-stu-id="e7ec0-107">API call</span></span>
### <a name="request"></a><span data-ttu-id="e7ec0-108">要求</span><span class="sxs-lookup"><span data-stu-id="e7ec0-108">Request</span></span>
<span data-ttu-id="e7ec0-109">要求會取得所要求的訂用帳戶在要求的時間範圍內的耗用量詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-109">The request gets consumption details for the requested subscriptions and for the requested time frame.</span></span> <span data-ttu-id="e7ec0-110">沒有要求主體。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-110">There is no request body.</span></span>

| <span data-ttu-id="e7ec0-111">**方法**</span><span class="sxs-lookup"><span data-stu-id="e7ec0-111">**Method**</span></span> | <span data-ttu-id="e7ec0-112">**要求 URI**</span><span class="sxs-lookup"><span data-stu-id="e7ec0-112">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="e7ec0-113">GET</span><span class="sxs-lookup"><span data-stu-id="e7ec0-113">GET</span></span> |<span data-ttu-id="e7ec0-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="e7ec0-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="e7ec0-115">引數</span><span class="sxs-lookup"><span data-stu-id="e7ec0-115">Arguments</span></span>
| <span data-ttu-id="e7ec0-116">**引數**</span><span class="sxs-lookup"><span data-stu-id="e7ec0-116">**Argument**</span></span> | <span data-ttu-id="e7ec0-117">**說明**</span><span class="sxs-lookup"><span data-stu-id="e7ec0-117">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e7ec0-118">*Armendpoint*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-118">*Armendpoint*</span></span> |<span data-ttu-id="e7ec0-119">您 Azure Stack 環境的 Azure Resource Manager 端點。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-119">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="e7ec0-120">依 Azure Stack 慣例，Azure Resource Manager 端點名稱的格式是 `https://management.{domain-name}`。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-120">The Azure Stack convention is that the name of Azure Resource Manager endpoint is in the format `https://management.{domain-name}`.</span></span> <span data-ttu-id="e7ec0-121">例如，如果網域名稱是 local.azurestack.external，則 Resource Manager 端點名稱是 `https://management.local.azurestack.external`。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-121">For example, if the domain name is local.azurestack.external, then the Resource Manager  endpoint is `https://management.local.azurestack.external`.</span></span> |
| <span data-ttu-id="e7ec0-122">*subId*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-122">*subId*</span></span> |<span data-ttu-id="e7ec0-123">正在進行呼叫之使用者的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-123">Subscription ID of the user who is making the call.</span></span> <span data-ttu-id="e7ec0-124">您只能使用此 API 查詢單一訂用帳戶的使用情況。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-124">You can use this API only to query for a single subscription’s usage.</span></span> <span data-ttu-id="e7ec0-125">提供者可以使用提供者資源使用情況 API 查詢所有租用戶的使用情況。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-125">Providers can use the Provider Resource Usage API to query usage for all tenants.</span></span> |
| <span data-ttu-id="e7ec0-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-126">*reportedStartTime*</span></span> |<span data-ttu-id="e7ec0-127">查詢的開始時間。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-127">Start time of the query.</span></span> <span data-ttu-id="e7ec0-128">*DateTime* 值應該以 UTC 格式及小時開始時的時間呈現，例如 13:00。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span></span> <span data-ttu-id="e7ec0-129">對於每日彙總，請將這個值設定為 UTC 午夜。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-129">For daily aggregation, set this value to UTC midnight.</span></span> <span data-ttu-id="e7ec0-130">格式是*逸出的* ISO 8601，例如 2015-06-16T18%3a53%3a11%2b00%3a00Z，其中冒號會逸出為 %3a 而加號會逸出為 %2b，使其符合 URI 規範。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="e7ec0-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-131">*reportedEndTime*</span></span> |<span data-ttu-id="e7ec0-132">查詢的結束時間。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-132">End time of the query.</span></span> <span data-ttu-id="e7ec0-133">適用於 *reportedStartTime* 的限制也適用於此引數。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span></span> <span data-ttu-id="e7ec0-134">*reportedEndTime* 的值不能是未來的時間。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-134">The value for *reportedEndTime* cannot be in the future.</span></span> |
| <span data-ttu-id="e7ec0-135">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-135">*aggregationGranularity*</span></span> |<span data-ttu-id="e7ec0-136">這是選擇性引數，它可以有兩個截然不同的可能值 (每日及每小時)。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-136">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="e7ec0-137">如同以上兩個值所暗示，一個會每日傳回資料，另一個則會每小時傳回資料。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-137">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span></span> <span data-ttu-id="e7ec0-138">預設值為 [每日] 選項。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-138">The daily option is the default.</span></span> |
| <span data-ttu-id="e7ec0-139">*api-version*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-139">*api-version*</span></span> |<span data-ttu-id="e7ec0-140">用來提出此要求的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-140">Version of the protocol that is used to make this request.</span></span> <span data-ttu-id="e7ec0-141">您必須使用 2015-06-01-preview。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-141">You must use 2015-06-01-preview.</span></span> |
| <span data-ttu-id="e7ec0-142">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-142">*continuationToken*</span></span> |<span data-ttu-id="e7ec0-143">從上次呼叫使用情況 API 提供者所擷取的權杖。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-143">Token retrieved from the last call to the Usage API provider.</span></span> <span data-ttu-id="e7ec0-144">回應大於 1000 行時就需要這個權杖，可作為進度的書籤。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-144">This token is needed when a response is greater than 1,000 lines and it acts as a bookmark for progress.</span></span> <span data-ttu-id="e7ec0-145">若無此權杖，則會從一天或小時開始時的時間擷取資料，取決於所傳遞的細微性。</span><span class="sxs-lookup"><span data-stu-id="e7ec0-145">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="e7ec0-146">Response</span><span class="sxs-lookup"><span data-stu-id="e7ec0-146">Response</span></span>
<span data-ttu-id="e7ec0-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="e7ec0-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span></span>

<span data-ttu-id="e7ec0-148">{</span><span class="sxs-lookup"><span data-stu-id="e7ec0-148">{</span></span>

<span data-ttu-id="e7ec0-149">"value": \[</span><span class="sxs-lookup"><span data-stu-id="e7ec0-149">"value": \[</span></span>

<span data-ttu-id="e7ec0-150">{</span><span class="sxs-lookup"><span data-stu-id="e7ec0-150">{</span></span>

<span data-ttu-id="e7ec0-151">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="e7ec0-151">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span></span>

<span data-ttu-id="e7ec0-152">"name": "sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="e7ec0-152">"name": "sub1-meterID1",</span></span>

<span data-ttu-id="e7ec0-153">"type": "Microsoft.Commerce/UsageAggregate",</span><span class="sxs-lookup"><span data-stu-id="e7ec0-153">"type": "Microsoft.Commerce/UsageAggregate",</span></span>

<span data-ttu-id="e7ec0-154">"properties": {</span><span class="sxs-lookup"><span data-stu-id="e7ec0-154">"properties": {</span></span>

<span data-ttu-id="e7ec0-155">"subscriptionId":"sub1",</span><span class="sxs-lookup"><span data-stu-id="e7ec0-155">"subscriptionId":"sub1",</span></span>

<span data-ttu-id="e7ec0-156">"usageStartTime": "2015-03-03T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="e7ec0-156">"usageStartTime": "2015-03-03T00:00:00+00:00",</span></span>

<span data-ttu-id="e7ec0-157">"usageEndTime": "2015-03-04T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="e7ec0-157">"usageEndTime": "2015-03-04T00:00:00+00:00",</span></span>

<span data-ttu-id="e7ec0-158">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span><span class="sxs-lookup"><span data-stu-id="e7ec0-158">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span></span>

<span data-ttu-id="e7ec0-159">"quantity":2.4000000000,</span><span class="sxs-lookup"><span data-stu-id="e7ec0-159">"quantity":2.4000000000,</span></span>

<span data-ttu-id="e7ec0-160">"meterId":"meterID1"</span><span class="sxs-lookup"><span data-stu-id="e7ec0-160">"meterId":"meterID1"</span></span>

<span data-ttu-id="e7ec0-161">}</span><span class="sxs-lookup"><span data-stu-id="e7ec0-161">}</span></span>

<span data-ttu-id="e7ec0-162">},</span><span class="sxs-lookup"><span data-stu-id="e7ec0-162">},</span></span>

<span data-ttu-id="e7ec0-163">…</span><span class="sxs-lookup"><span data-stu-id="e7ec0-163">…</span></span>

### <a name="response-details"></a><span data-ttu-id="e7ec0-164">回應詳細資料</span><span class="sxs-lookup"><span data-stu-id="e7ec0-164">Response details</span></span>
| <span data-ttu-id="e7ec0-165">**引數**</span><span class="sxs-lookup"><span data-stu-id="e7ec0-165">**Argument**</span></span> | <span data-ttu-id="e7ec0-166">**說明**</span><span class="sxs-lookup"><span data-stu-id="e7ec0-166">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e7ec0-167">*id*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-167">*id*</span></span> |<span data-ttu-id="e7ec0-168">使用情況彙總的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="e7ec0-168">Unique ID of the usage aggregate</span></span> |
| <span data-ttu-id="e7ec0-169">*name*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-169">*name*</span></span> |<span data-ttu-id="e7ec0-170">使用情況彙總的名稱</span><span class="sxs-lookup"><span data-stu-id="e7ec0-170">Name of the usage aggregate</span></span> |
| <span data-ttu-id="e7ec0-171">*type*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-171">*type*</span></span> |<span data-ttu-id="e7ec0-172">資源定義</span><span class="sxs-lookup"><span data-stu-id="e7ec0-172">Resource definition</span></span> |
| <span data-ttu-id="e7ec0-173">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-173">*subscriptionId*</span></span> |<span data-ttu-id="e7ec0-174">Azure 使用者的訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e7ec0-174">Subscription identifier of the Azure user</span></span> |
| <span data-ttu-id="e7ec0-175">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-175">*usageStartTime*</span></span> |<span data-ttu-id="e7ec0-176">此使用情況彙總所屬的使用情況貯體 UTC 開始時間</span><span class="sxs-lookup"><span data-stu-id="e7ec0-176">UTC start time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="e7ec0-177">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-177">*usageEndTime*</span></span> |<span data-ttu-id="e7ec0-178">此使用情況彙總所屬的使用情況貯體 UTC 結束時間</span><span class="sxs-lookup"><span data-stu-id="e7ec0-178">UTC end time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="e7ec0-179">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-179">*instanceData*</span></span> |<span data-ttu-id="e7ec0-180">執行個體詳細資料的機碼值組 (新格式)：</span><span class="sxs-lookup"><span data-stu-id="e7ec0-180">Key-value pairs of instance details (in a new format):</span></span><br>  <span data-ttu-id="e7ec0-181">*resourceUri*：完整資源識別碼，包含資源群組和執行個體名稱</span><span class="sxs-lookup"><span data-stu-id="e7ec0-181">*resourceUri*: Fully qualified resource ID, including resource groups and instance name</span></span> <br>  <span data-ttu-id="e7ec0-182">*location*：此服務執行所在的區域</span><span class="sxs-lookup"><span data-stu-id="e7ec0-182">*location*: Region in which this service was run</span></span> <br>  <span data-ttu-id="e7ec0-183">*tags*：使用者指定的資源標記</span><span class="sxs-lookup"><span data-stu-id="e7ec0-183">*tags*: Resource tags that the user specifies</span></span> <br>  <span data-ttu-id="e7ec0-184">*additionalInfo*：更多關於所取用資源的詳細資料 (例如，作業系統版本或映像類型)</span><span class="sxs-lookup"><span data-stu-id="e7ec0-184">*additionalInfo*: More details about the resource that was consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="e7ec0-185">*quantity*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-185">*quantity*</span></span> |<span data-ttu-id="e7ec0-186">此時間範圍內發生的資源取用數量</span><span class="sxs-lookup"><span data-stu-id="e7ec0-186">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="e7ec0-187">*meterId*</span><span class="sxs-lookup"><span data-stu-id="e7ec0-187">*meterId*</span></span> |<span data-ttu-id="e7ec0-188">所取用資源的唯一識別碼 ( *ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="e7ec0-188">Unique ID for the resource that was consumed (also called *ResourceID*)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e7ec0-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7ec0-189">Next steps</span></span>
[<span data-ttu-id="e7ec0-190">提供者資源使用狀況 API</span><span class="sxs-lookup"><span data-stu-id="e7ec0-190">Provider resource usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="e7ec0-191">使用狀況相關常見問題集</span><span class="sxs-lookup"><span data-stu-id="e7ec0-191">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

