---
title: "aaaAzure 資源管理員要求限制 |Microsoft 文件"
description: "描述如何 toouse 節流設定與 Azure 資源管理員要求到達訂用帳戶的限制。"
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
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="29047-103">對 Resource Manager 要求進行節流</span><span class="sxs-lookup"><span data-stu-id="29047-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="29047-104">每個訂用帳戶和租用戶，資源管理員限制要求 too15，每小時 000 讀寫要求 too1，每小時 200。</span><span class="sxs-lookup"><span data-stu-id="29047-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="29047-105">這些限制適用於 tooeach Azure 資源管理員執行個體。在每個 Azure 區域中，有多個執行個體和 Azure 資源管理員是已部署的 tooall Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="29047-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="29047-106">因此，實際上的限制比上面列出的還要高，因為通常是由多個不同的執行個體來服務使用者要求。</span><span class="sxs-lookup"><span data-stu-id="29047-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="29047-107">如果您的應用程式或指令碼已達到這些限制，您需要 toothrottle 您的要求。</span><span class="sxs-lookup"><span data-stu-id="29047-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="29047-108">本主題說明如何 toodetermine hello 剩餘要求您必須先到達 hello 限制以及如何 toorespond 時已達到 hello 上限。</span><span class="sxs-lookup"><span data-stu-id="29047-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="29047-109">當您到達 hello 限制時，您會收到 hello HTTP 狀態碼**429 太多要求**。</span><span class="sxs-lookup"><span data-stu-id="29047-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="29047-110">hello 的要求數目是限定範圍的 tooeither 訂用帳戶或您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="29047-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="29047-111">如果您有多個，並行的應用程式提出要求，在您的訂用帳戶，來自這些應用程式的 hello 要求加在一起 toodetermine hello 數目其餘要求。</span><span class="sxs-lookup"><span data-stu-id="29047-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="29047-112">訂用帳戶範圍要求為 hello 牽涉到將您的訂用帳戶識別碼，例如擷取您的訂用帳戶中的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="29047-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="29047-113">受租用戶限制的要求則未包含訂用帳戶識別碼，例如擷取有效的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="29047-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="29047-114">剩餘的要求</span><span class="sxs-lookup"><span data-stu-id="29047-114">Remaining requests</span></span>
<span data-ttu-id="29047-115">您可以藉由檢查回應標頭判斷 hello 剩餘的要求數目。</span><span class="sxs-lookup"><span data-stu-id="29047-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="29047-116">每個要求包含 hello 剩餘的讀取和寫入要求數目的值。</span><span class="sxs-lookup"><span data-stu-id="29047-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="29047-117">hello 下表描述您可以檢查這些值為 hello 回應標頭：</span><span class="sxs-lookup"><span data-stu-id="29047-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="29047-118">回應標頭</span><span class="sxs-lookup"><span data-stu-id="29047-118">Response header</span></span> | <span data-ttu-id="29047-119">說明</span><span class="sxs-lookup"><span data-stu-id="29047-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29047-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="29047-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="29047-121">受訂用帳戶限制的剩餘讀取</span><span class="sxs-lookup"><span data-stu-id="29047-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="29047-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="29047-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="29047-123">受訂用帳戶限制的剩餘寫入</span><span class="sxs-lookup"><span data-stu-id="29047-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="29047-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="29047-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="29047-125">受租用戶限制的剩餘讀取</span><span class="sxs-lookup"><span data-stu-id="29047-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="29047-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="29047-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="29047-127">受租用戶限制的剩餘寫入</span><span class="sxs-lookup"><span data-stu-id="29047-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="29047-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="29047-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="29047-129">受訂用帳戶限制的剩餘資源類型要求。</span><span class="sxs-lookup"><span data-stu-id="29047-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="29047-130">如果服務已覆寫 hello 預設限制，才會傳回此標頭值。</span><span class="sxs-lookup"><span data-stu-id="29047-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="29047-131">資源管理員會加入此值，而非 hello 訂用帳戶的讀取或寫入。</span><span class="sxs-lookup"><span data-stu-id="29047-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="29047-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="29047-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="29047-133">受訂用帳戶限制的剩餘資源類型集合要求。</span><span class="sxs-lookup"><span data-stu-id="29047-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="29047-134">如果服務已覆寫 hello 預設限制，才會傳回此標頭值。</span><span class="sxs-lookup"><span data-stu-id="29047-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="29047-135">此值會提供其餘集合要求 （清單資源） 的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="29047-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="29047-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="29047-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="29047-137">受租用戶限制的剩餘資源類型要求。</span><span class="sxs-lookup"><span data-stu-id="29047-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="29047-138">此標頭只會加入租用戶層級的要求，而且只有當服務已覆寫 hello 預設限制。</span><span class="sxs-lookup"><span data-stu-id="29047-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="29047-139">資源管理員會加入此值，而非 hello 租用戶讀取或寫入。</span><span class="sxs-lookup"><span data-stu-id="29047-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="29047-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="29047-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="29047-141">受租用戶限制的剩餘資源類型集合要求。</span><span class="sxs-lookup"><span data-stu-id="29047-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="29047-142">此標頭只會加入租用戶層級的要求，而且只有當服務已覆寫 hello 預設限制。</span><span class="sxs-lookup"><span data-stu-id="29047-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="29047-143">擷取 hello 標頭值</span><span class="sxs-lookup"><span data-stu-id="29047-143">Retrieving hello header values</span></span>
<span data-ttu-id="29047-144">在程式碼或指令碼中擷取這些標頭值與擷取任何標頭值並無不同。</span><span class="sxs-lookup"><span data-stu-id="29047-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="29047-145">例如，在**C#**，擷取的 hello 標頭值**HttpWebResponse**名為物件**回應**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="29047-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="29047-146">在**PowerShell**，Invoke-webrequest 作業中擷取 hello 標頭值。</span><span class="sxs-lookup"><span data-stu-id="29047-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="29047-147">或者，如果想 toosee hello 剩餘要求進行偵錯，您可以提供 hello **-偵錯**參數上的您**PowerShell** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="29047-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="29047-148">它會傳回許多值，包括下列回應值的 hello:</span><span class="sxs-lookup"><span data-stu-id="29047-148">Which returns many values, including hello following response value:</span></span>

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

<span data-ttu-id="29047-149">在**Azure CLI**，您可以使用擷取 hello 標頭值 hello 更多詳細資料的選項。</span><span class="sxs-lookup"><span data-stu-id="29047-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="29047-150">它會傳回許多值，包括下列物件的 hello:</span><span class="sxs-lookup"><span data-stu-id="29047-150">Which returns many values, including hello following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="29047-151">在傳送下一個要求前先稍候</span><span class="sxs-lookup"><span data-stu-id="29047-151">Waiting before sending next request</span></span>
<span data-ttu-id="29047-152">當您到達 hello 要求限制時，資源管理員會傳回 hello **429** HTTP 狀態碼和**後重試**hello 標頭中的值。</span><span class="sxs-lookup"><span data-stu-id="29047-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="29047-153">hello**後重試**值傳送嗨下一個要求之前，先指定您的應用程式應等待的秒 （或睡眠） 的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="29047-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="29047-154">如果經過 hello 重試值之前，您就會傳送要求，則不會處理您的要求，並傳回新的重試值。</span><span class="sxs-lookup"><span data-stu-id="29047-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29047-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29047-155">Next steps</span></span>

* <span data-ttu-id="29047-156">如需有關限制和配額的詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="29047-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="29047-157">toolearn 需處理非同步 REST 要求，請參閱[追蹤非同步的 Azure 作業](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="29047-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
