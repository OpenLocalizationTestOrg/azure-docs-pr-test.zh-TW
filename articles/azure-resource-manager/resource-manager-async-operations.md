---
title: "Azure 非同步作業 | Microsoft Docs"
description: "描述如何在 Azure 中追蹤非同步作業。"
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
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="aff1b-103">追蹤非同步 Azure 作業</span><span class="sxs-lookup"><span data-stu-id="aff1b-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="aff1b-104">某些 Azure REST 作業因為無法快速完成，而以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="aff1b-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="aff1b-105">本主題說明如何透過回應中傳回的值，以追蹤非同步作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="aff1b-106">非同步作業的狀態碼</span><span class="sxs-lookup"><span data-stu-id="aff1b-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="aff1b-107">非同步作業最初會傳回下列其中一個 HTTP 狀態碼︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="aff1b-108">201 (已建立)</span><span class="sxs-lookup"><span data-stu-id="aff1b-108">201 (Created)</span></span>
* <span data-ttu-id="aff1b-109">202 (已接受)</span><span class="sxs-lookup"><span data-stu-id="aff1b-109">202 (Accepted)</span></span> 

<span data-ttu-id="aff1b-110">作業成功完成時會傳回下列其中一個狀態碼︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="aff1b-111">200 (確定)</span><span class="sxs-lookup"><span data-stu-id="aff1b-111">200 (OK)</span></span>
* <span data-ttu-id="aff1b-112">204 (沒有內容)</span><span class="sxs-lookup"><span data-stu-id="aff1b-112">204 (No Content)</span></span> 

<span data-ttu-id="aff1b-113">請參閱 [REST API 文件](/rest/api/)，查看您執行之作業的回應。</span><span class="sxs-lookup"><span data-stu-id="aff1b-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="aff1b-114">監視作業的狀態</span><span class="sxs-lookup"><span data-stu-id="aff1b-114">Monitor status of operation</span></span>
<span data-ttu-id="aff1b-115">非同步 REST 作業傳回的標頭值，可用來判斷作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="aff1b-116">可能有三個標頭值可檢查︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="aff1b-117">`Azure-AsyncOperation` - 用於檢查作業進行中狀態的 URL。</span><span class="sxs-lookup"><span data-stu-id="aff1b-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="aff1b-118">如果您的作業傳回此值，一律使用它 (而非 Location) 來追蹤作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="aff1b-119">`Location` - 用於判斷作業何時完成的 URL。</span><span class="sxs-lookup"><span data-stu-id="aff1b-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="aff1b-120">只在未傳回 Azure-AsyncOperation 時才使用此值。</span><span class="sxs-lookup"><span data-stu-id="aff1b-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="aff1b-121">`Retry-After` - 在檢查非同步作業的狀態之前等待的秒數。</span><span class="sxs-lookup"><span data-stu-id="aff1b-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="aff1b-122">不過，並非每個非同步作業會傳回所有這些值。</span><span class="sxs-lookup"><span data-stu-id="aff1b-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="aff1b-123">例如，您可能需要評估一項作業的 Azure AsyncOperation 標頭值，但要評估另一項作業的 Location 標頭值。</span><span class="sxs-lookup"><span data-stu-id="aff1b-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="aff1b-124">擷取標頭值的方式如同擷取要求的任何標頭值一樣。</span><span class="sxs-lookup"><span data-stu-id="aff1b-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="aff1b-125">例如，在 C# 中，您可以使用下列程式碼從名為 `response` 的 `HttpWebResponse` 物件擷取標頭值︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="aff1b-126">Azure-AsyncOperation 要求和回應</span><span class="sxs-lookup"><span data-stu-id="aff1b-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="aff1b-127">若要取得非同步作業的狀態，請將 GET 要求傳送至 Azure-AsyncOperation 標頭值中的 URL。</span><span class="sxs-lookup"><span data-stu-id="aff1b-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="aff1b-128">這項作業的回應內文包含作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aff1b-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="aff1b-129">下列範例顯示作業所傳回的可能值︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-129">The following example shows the possible values returned from the operation:</span></span>

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

<span data-ttu-id="aff1b-130">所有回應只傳回 `status`。</span><span class="sxs-lookup"><span data-stu-id="aff1b-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="aff1b-131">當狀態為 Failed 或 Canceled 時會傳回錯誤物件。</span><span class="sxs-lookup"><span data-stu-id="aff1b-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="aff1b-132">其他所有值都是選擇性，因此，您收到的回應可能不同於範例。</span><span class="sxs-lookup"><span data-stu-id="aff1b-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="aff1b-133">provisioningState 值</span><span class="sxs-lookup"><span data-stu-id="aff1b-133">provisioningState values</span></span>

<span data-ttu-id="aff1b-134">建立、更新或刪除資源的作業 (PUT、PATCH、DELETE) 通常會傳回 `provisioningState` 值。</span><span class="sxs-lookup"><span data-stu-id="aff1b-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="aff1b-135">當作業完成時會傳回下列三個值之一︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="aff1b-136">Succeeded</span><span class="sxs-lookup"><span data-stu-id="aff1b-136">Succeeded</span></span>
* <span data-ttu-id="aff1b-137">Failed</span><span class="sxs-lookup"><span data-stu-id="aff1b-137">Failed</span></span>
* <span data-ttu-id="aff1b-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="aff1b-138">Canceled</span></span>

<span data-ttu-id="aff1b-139">其他所有值表示作業仍在執行中。</span><span class="sxs-lookup"><span data-stu-id="aff1b-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="aff1b-140">資源提供者可以傳回自訂值來指出其狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="aff1b-141">例如，當要求已收到且正在執行時，您可能會收到 **Accepted**。</span><span class="sxs-lookup"><span data-stu-id="aff1b-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="aff1b-142">要求和回應範例</span><span class="sxs-lookup"><span data-stu-id="aff1b-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="aff1b-143">啟動虛擬機器 (202 與 Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="aff1b-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="aff1b-144">這個範例示範如何判斷虛擬機器**啟動**作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="aff1b-145">初始要求是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="aff1b-146">它傳回狀態碼 202。</span><span class="sxs-lookup"><span data-stu-id="aff1b-146">It returns status code 202.</span></span> <span data-ttu-id="aff1b-147">在標頭值之中，您會看到：</span><span class="sxs-lookup"><span data-stu-id="aff1b-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="aff1b-148">若要檢查非同步作業的狀態，請將另一個要求傳送至該 URL。</span><span class="sxs-lookup"><span data-stu-id="aff1b-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="aff1b-149">回應內文包含作業的狀態︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="aff1b-150">部署資源 (201 與 Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="aff1b-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="aff1b-151">這個範例示範將資源部署至 Azure 時，如何判斷**部署**作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="aff1b-152">初始要求是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="aff1b-153">它傳回狀態碼 201。</span><span class="sxs-lookup"><span data-stu-id="aff1b-153">It returns status code 201.</span></span> <span data-ttu-id="aff1b-154">回應內文包含︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="aff1b-155">在標頭值之中，您會看到：</span><span class="sxs-lookup"><span data-stu-id="aff1b-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="aff1b-156">若要檢查非同步作業的狀態，請將另一個要求傳送至該 URL。</span><span class="sxs-lookup"><span data-stu-id="aff1b-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="aff1b-157">回應內文包含作業的狀態︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="aff1b-158">部署完成時，回應包含︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="aff1b-159">建立儲存體帳戶 (202 與 Location 和 Retry-After)</span><span class="sxs-lookup"><span data-stu-id="aff1b-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="aff1b-160">這個範例示範如何判斷儲存體帳戶**建立**作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="aff1b-161">初始要求是下列格式︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="aff1b-162">要求內文包含儲存體帳戶的屬性︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="aff1b-163">它傳回狀態碼 202。</span><span class="sxs-lookup"><span data-stu-id="aff1b-163">It returns status code 202.</span></span> <span data-ttu-id="aff1b-164">在標頭值之中，您會看到下列兩個值︰</span><span class="sxs-lookup"><span data-stu-id="aff1b-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="aff1b-165">等待 Retry-After 中指定的秒數經過之後，將另一個要求傳送至該 URL，以檢查非同步作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="aff1b-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="aff1b-166">如果要求仍在執行中，您會收到狀態碼 202。</span><span class="sxs-lookup"><span data-stu-id="aff1b-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="aff1b-167">如果要求已完成，您會收到狀態碼 200，回應內文會包含已建立之儲存體帳戶的屬性。</span><span class="sxs-lookup"><span data-stu-id="aff1b-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aff1b-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aff1b-168">Next steps</span></span>

* <span data-ttu-id="aff1b-169">如需每個 REST 作業的相關文件，請參閱 [REST API 文件](/rest/api/)。</span><span class="sxs-lookup"><span data-stu-id="aff1b-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="aff1b-170">如需透過 Resource Manager REST API 管理資源的相關資訊，請參閱[使用 Resource Manager REST API](resource-manager-rest-api.md)。</span><span class="sxs-lookup"><span data-stu-id="aff1b-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="aff1b-171">如需透過 Resource Manager REST API 部署範本的相關資訊，請參閱[使用 Resource Manager 範本和 Resource Manager REST API 部署資源](resource-group-template-deploy-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="aff1b-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>