---
title: "aaaAzure 非同步作業 |Microsoft 文件"
description: "描述如何在 Azure 中的 tootrack 非同步作業。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="c4988-103">追蹤非同步 Azure 作業</span><span class="sxs-lookup"><span data-stu-id="c4988-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="c4988-104">某些 Azure REST 作業，以非同步方式執行，因為 hello 作業無法完成快速。</span><span class="sxs-lookup"><span data-stu-id="c4988-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="c4988-105">本主題描述如何 hello 回應中傳回 tootrack hello 非同步作業狀態的值。</span><span class="sxs-lookup"><span data-stu-id="c4988-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="c4988-106">非同步作業的狀態碼</span><span class="sxs-lookup"><span data-stu-id="c4988-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="c4988-107">非同步作業最初會傳回下列其中一個 HTTP 狀態碼︰</span><span class="sxs-lookup"><span data-stu-id="c4988-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="c4988-108">201 (已建立)</span><span class="sxs-lookup"><span data-stu-id="c4988-108">201 (Created)</span></span>
* <span data-ttu-id="c4988-109">202 (已接受)</span><span class="sxs-lookup"><span data-stu-id="c4988-109">202 (Accepted)</span></span> 

<span data-ttu-id="c4988-110">當 hello 作業成功完成時，它會傳回：</span><span class="sxs-lookup"><span data-stu-id="c4988-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="c4988-111">200 (確定)</span><span class="sxs-lookup"><span data-stu-id="c4988-111">200 (OK)</span></span>
* <span data-ttu-id="c4988-112">204 (沒有內容)</span><span class="sxs-lookup"><span data-stu-id="c4988-112">204 (No Content)</span></span> 

<span data-ttu-id="c4988-113">請參閱 toohello [REST API 文件](/rest/api/)toosee hello 回應 hello 作業正在執行。</span><span class="sxs-lookup"><span data-stu-id="c4988-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="c4988-114">監視作業的狀態</span><span class="sxs-lookup"><span data-stu-id="c4988-114">Monitor status of operation</span></span>
<span data-ttu-id="c4988-115">hello 非同步 REST 作業傳回的標頭的值，您使用 toodetermine hello 狀態 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="c4988-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="c4988-116">可能有三個標頭值 tooexamine:</span><span class="sxs-lookup"><span data-stu-id="c4988-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="c4988-117">`Azure-AsyncOperation`-URL 檢查 hello hello 作業進行中的狀態。</span><span class="sxs-lookup"><span data-stu-id="c4988-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="c4988-118">如果您的作業會傳回此值，請一律使用 hello 作業 （而不是位置） 的 it tootrack hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="c4988-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="c4988-119">`Location` - 用於判斷作業何時完成的 URL。</span><span class="sxs-lookup"><span data-stu-id="c4988-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="c4988-120">只在未傳回 Azure-AsyncOperation 時才使用此值。</span><span class="sxs-lookup"><span data-stu-id="c4988-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="c4988-121">`Retry-After`-hello 檢查 hello hello 非同步作業的狀態之前的秒數 toowait 數目。</span><span class="sxs-lookup"><span data-stu-id="c4988-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="c4988-122">不過，並非每個非同步作業會傳回所有這些值。</span><span class="sxs-lookup"><span data-stu-id="c4988-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="c4988-123">例如，您可能需要 tooevaluate hello Azure AsyncOperation 標頭值的一項作業和另一個作業的 hello 位置標頭值。</span><span class="sxs-lookup"><span data-stu-id="c4988-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="c4988-124">您會在擷取要求的任何標頭值，您可以擷取 hello 標頭值。</span><span class="sxs-lookup"><span data-stu-id="c4988-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="c4988-125">例如，在 C# 中，您要擷取的 hello 標頭值`HttpWebResponse`名為物件`response`以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4988-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="c4988-126">Azure-AsyncOperation 要求和回應</span><span class="sxs-lookup"><span data-stu-id="c4988-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="c4988-127">tooget hello 狀態 hello 非同步作業時，傳送 GET 要求 toohello URL Azure AsyncOperation 標頭值。</span><span class="sxs-lookup"><span data-stu-id="c4988-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="c4988-128">從這項作業的 hello 回應 hello 主體包含 hello 作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c4988-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="c4988-129">hello 下列範例顯示 hello hello 作業傳回的可能值：</span><span class="sxs-lookup"><span data-stu-id="c4988-129">hello following example shows hello possible values returned from hello operation:</span></span>

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

<span data-ttu-id="c4988-130">所有回應只傳回 `status`。</span><span class="sxs-lookup"><span data-stu-id="c4988-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="c4988-131">當 hello 狀態為 Failed 或已取消，則會傳回 hello 物件時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="c4988-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="c4988-132">所有其他值均為選擇性;因此，您會收到 hello 回應可能看起來與 hello 範例不同。</span><span class="sxs-lookup"><span data-stu-id="c4988-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="c4988-133">provisioningState 值</span><span class="sxs-lookup"><span data-stu-id="c4988-133">provisioningState values</span></span>

<span data-ttu-id="c4988-134">建立、更新或刪除資源的作業 (PUT、PATCH、DELETE) 通常會傳回 `provisioningState` 值。</span><span class="sxs-lookup"><span data-stu-id="c4988-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="c4988-135">當作業完成時會傳回下列三個值之一︰</span><span class="sxs-lookup"><span data-stu-id="c4988-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="c4988-136">Succeeded</span><span class="sxs-lookup"><span data-stu-id="c4988-136">Succeeded</span></span>
* <span data-ttu-id="c4988-137">Failed</span><span class="sxs-lookup"><span data-stu-id="c4988-137">Failed</span></span>
* <span data-ttu-id="c4988-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="c4988-138">Canceled</span></span>

<span data-ttu-id="c4988-139">所有其他值則表示 hello 作業仍在執行中。</span><span class="sxs-lookup"><span data-stu-id="c4988-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="c4988-140">hello 資源提供者可以傳回自訂的值，指出其狀態。</span><span class="sxs-lookup"><span data-stu-id="c4988-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="c4988-141">例如，您可能會收到**接受**hello 要求時接收並執行。</span><span class="sxs-lookup"><span data-stu-id="c4988-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="c4988-142">要求和回應範例</span><span class="sxs-lookup"><span data-stu-id="c4988-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="c4988-143">啟動虛擬機器 (202 與 Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="c4988-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="c4988-144">這個範例會示範如何 toodetermine hello 狀態**啟動**虛擬機器的作業。</span><span class="sxs-lookup"><span data-stu-id="c4988-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="c4988-145">hello 初始要求是下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4988-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="c4988-146">它傳回狀態碼 202。</span><span class="sxs-lookup"><span data-stu-id="c4988-146">It returns status code 202.</span></span> <span data-ttu-id="c4988-147">在 hello 標頭值，您會看到：</span><span class="sxs-lookup"><span data-stu-id="c4988-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="c4988-148">toocheck hello hello 非同步作業，傳送另一個要求 toothat URL 的狀態。</span><span class="sxs-lookup"><span data-stu-id="c4988-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="c4988-149">hello 回應主體會包含 hello hello 作業狀態：</span><span class="sxs-lookup"><span data-stu-id="c4988-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="c4988-150">部署資源 (201 與 Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="c4988-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="c4988-151">這個範例會示範如何 toodetermine hello 狀態**部署**部署資源 tooAzure 的作業。</span><span class="sxs-lookup"><span data-stu-id="c4988-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="c4988-152">hello 初始要求是下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4988-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="c4988-153">它傳回狀態碼 201。</span><span class="sxs-lookup"><span data-stu-id="c4988-153">It returns status code 201.</span></span> <span data-ttu-id="c4988-154">hello 回應 hello 主體包括：</span><span class="sxs-lookup"><span data-stu-id="c4988-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="c4988-155">在 hello 標頭值，您會看到：</span><span class="sxs-lookup"><span data-stu-id="c4988-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="c4988-156">toocheck hello hello 非同步作業，傳送另一個要求 toothat URL 的狀態。</span><span class="sxs-lookup"><span data-stu-id="c4988-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="c4988-157">hello 回應主體會包含 hello hello 作業狀態：</span><span class="sxs-lookup"><span data-stu-id="c4988-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="c4988-158">Hello 部署完成時，包含回應 hello:</span><span class="sxs-lookup"><span data-stu-id="c4988-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="c4988-159">建立儲存體帳戶 (202 與 Location 和 Retry-After)</span><span class="sxs-lookup"><span data-stu-id="c4988-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="c4988-160">這個範例會示範如何 toodetermine hello 的 hello 狀態**建立**儲存體帳戶的作業。</span><span class="sxs-lookup"><span data-stu-id="c4988-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="c4988-161">hello 初始要求是下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4988-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="c4988-162">和 hello 要求主體包含 hello 儲存體帳戶屬性：</span><span class="sxs-lookup"><span data-stu-id="c4988-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="c4988-163">它傳回狀態碼 202。</span><span class="sxs-lookup"><span data-stu-id="c4988-163">It returns status code 202.</span></span> <span data-ttu-id="c4988-164">在 hello 標頭值，您會看到下列兩個值的 hello:</span><span class="sxs-lookup"><span data-stu-id="c4988-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="c4988-165">之後等候數秒指定在重試之後，傳送給另一個要求 toothat URL 檢查 hello hello 非同步作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="c4988-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="c4988-166">如果 hello 要求仍在執行中，您會收到狀態碼 202。</span><span class="sxs-lookup"><span data-stu-id="c4988-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="c4988-167">如果 hello 要求已完成，您會收到狀態碼 200，並 hello 回應 hello 主體包含 hello 已建立的儲存體帳戶的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="c4988-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4988-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4988-168">Next steps</span></span>

* <span data-ttu-id="c4988-169">如需每個 REST 作業的相關文件，請參閱 [REST API 文件](/rest/api/)。</span><span class="sxs-lookup"><span data-stu-id="c4988-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="c4988-170">管理透過 hello 資源管理員 REST API 資源的相關資訊，請參閱[使用 hello 資源管理員 REST API](resource-manager-rest-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c4988-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="c4988-171">部署範本，透過 hello 資源管理員 REST API 的相關資訊，請參閱[部署具有資源管理員範本和資源管理員 REST API 資源](resource-group-template-deploy-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="c4988-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
