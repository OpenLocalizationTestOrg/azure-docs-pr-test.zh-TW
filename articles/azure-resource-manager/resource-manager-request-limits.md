---
title: "Azure Resource Manager 要求限制 | Microsoft Docs"
description: "描述如何在到達訂用帳戶限制時，對 Azure Resource Manager 要求使用節流。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="6bb3a-103">對 Resource Manager 要求進行節流</span><span class="sxs-lookup"><span data-stu-id="6bb3a-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="6bb3a-104">針對每個訂用帳戶和租用戶，Resource Manager 限制每小時只能有 15000 個讀取要求和 1200 個寫入要求。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="6bb3a-105">這些限制會套用到每個 Azure Resource Manager 執行個體；每個 Azure 區域中都有多個執行個體，且 Azure Resource Manager 會部署到所有 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="6bb3a-106">因此，實際上的限制比上面列出的還要高，因為通常是由多個不同的執行個體來服務使用者要求。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="6bb3a-107">如果應用程式或指令碼到達這些限制，便需要對要求進行節流。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="6bb3a-108">本主題說明如何判斷還剩多少要求便會到達限制，以及在到達限制時該如何應對。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="6bb3a-109">當您到達限制時，您會收到 HTTP 狀態碼 **429 太多要求**。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="6bb3a-110">要求數會受訂用帳戶或租用戶所限制。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="6bb3a-111">如果訂用帳戶中有多個並行應用程式提出要求，來自這些應用程式的要求會加總起來，以判斷剩餘的要求數。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="6bb3a-112">受訂用帳戶限制的要求是涉及傳遞訂用帳戶識別碼的要求，例如擷取訂用帳戶中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="6bb3a-113">受租用戶限制的要求則未包含訂用帳戶識別碼，例如擷取有效的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="6bb3a-114">剩餘的要求</span><span class="sxs-lookup"><span data-stu-id="6bb3a-114">Remaining requests</span></span>
<span data-ttu-id="6bb3a-115">您可以藉由檢查回應標頭來判斷剩餘的要求數。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="6bb3a-116">每個要求都包含剩餘之讀取和寫入要求數的值。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="6bb3a-117">下表描述可供檢查這些值的回應標頭︰</span><span class="sxs-lookup"><span data-stu-id="6bb3a-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="6bb3a-118">回應標頭</span><span class="sxs-lookup"><span data-stu-id="6bb3a-118">Response header</span></span> | <span data-ttu-id="6bb3a-119">說明</span><span class="sxs-lookup"><span data-stu-id="6bb3a-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6bb3a-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="6bb3a-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="6bb3a-121">受訂用帳戶限制的剩餘讀取</span><span class="sxs-lookup"><span data-stu-id="6bb3a-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="6bb3a-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="6bb3a-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="6bb3a-123">受訂用帳戶限制的剩餘寫入</span><span class="sxs-lookup"><span data-stu-id="6bb3a-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="6bb3a-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="6bb3a-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="6bb3a-125">受租用戶限制的剩餘讀取</span><span class="sxs-lookup"><span data-stu-id="6bb3a-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="6bb3a-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="6bb3a-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="6bb3a-127">受租用戶限制的剩餘寫入</span><span class="sxs-lookup"><span data-stu-id="6bb3a-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="6bb3a-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="6bb3a-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="6bb3a-129">受訂用帳戶限制的剩餘資源類型要求。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="6bb3a-130">只有在服務已覆寫預設限制時，才會傳回此標頭值。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="6bb3a-131">Resource Manager 會新增此值，而非訂用帳戶讀取或寫入。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="6bb3a-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="6bb3a-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="6bb3a-133">受訂用帳戶限制的剩餘資源類型集合要求。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="6bb3a-134">只有在服務已覆寫預設限制時，才會傳回此標頭值。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="6bb3a-135">這個值會提供剩餘的集合要求 (列出資源) 數目。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="6bb3a-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="6bb3a-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="6bb3a-137">受租用戶限制的剩餘資源類型要求。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="6bb3a-138">只有租用戶層級的要求且在服務已覆寫預設限制時，才會新增此標頭。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="6bb3a-139">Resource Manager 會新增此值，而非租用戶讀取或寫入。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="6bb3a-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="6bb3a-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="6bb3a-141">受租用戶限制的剩餘資源類型集合要求。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="6bb3a-142">只有租用戶層級的要求且在服務已覆寫預設限制時，才會新增此標頭。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="6bb3a-143">擷取標頭值</span><span class="sxs-lookup"><span data-stu-id="6bb3a-143">Retrieving the header values</span></span>
<span data-ttu-id="6bb3a-144">在程式碼或指令碼中擷取這些標頭值與擷取任何標頭值並無不同。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="6bb3a-145">例如，在 **C#** 中，您可以使用下列程式碼從 **HttpWebResponse** 物件 (名為 **response**) 擷取標頭值︰</span><span class="sxs-lookup"><span data-stu-id="6bb3a-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="6bb3a-146">在 **PowerShell** 中，您可以從 Invoke-WebRequest 作業擷取標頭值。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="6bb3a-147">或者，如果您想要查看可用於偵錯的剩餘要求，您可以在 **PowerShell** Cmdlet 提供 **-Debug** 參數。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="6bb3a-148">這會傳回許多值，包括下列回應值︰</span><span class="sxs-lookup"><span data-stu-id="6bb3a-148">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="6bb3a-149">在 **Azure CLI** 中，您可以使用更詳細的選項擷取標頭值。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="6bb3a-150">這會傳回許多值，包括下列物件︰</span><span class="sxs-lookup"><span data-stu-id="6bb3a-150">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="6bb3a-151">在傳送下一個要求前先稍候</span><span class="sxs-lookup"><span data-stu-id="6bb3a-151">Waiting before sending next request</span></span>
<span data-ttu-id="6bb3a-152">當您到達要求限制時，Resource Manager 會在標頭中傳回 **429** HTTP 狀態碼和 **Retry-After** 值。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="6bb3a-153">**Retry-After** 值會指定應用程式在傳送下一個要求之前所應等待 (或睡眠) 的秒數。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="6bb3a-154">如果重試值沒過您就傳送要求，則不會處理要求，並且會傳回新的重試值。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bb3a-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bb3a-155">Next steps</span></span>

* <span data-ttu-id="6bb3a-156">如需有關限制和配額的詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="6bb3a-157">若要了解如何處理非同步 REST 要求，請參閱[追蹤非同步 Azure 作業 (英文)](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="6bb3a-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
