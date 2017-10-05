---
title: "Azure 計費企業版 API - 使用量詳細資料| Microsoft Docs"
description: "了解 Azure 計費使用情況和 RateCard API，其可用來提供 Azure 資源耗用量和趨勢的見解。"
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 5b49220e6eb27544dba54255ee88c56ad79c3141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a><span data-ttu-id="ac146-103">適用於企業客戶的報告 API - 使用量詳細資料</span><span class="sxs-lookup"><span data-stu-id="ac146-103">Reporting APIs for Enterprise customers - Usage Details</span></span>

<span data-ttu-id="ac146-104">使用量詳細資料 API 可提供註冊之使用量和預估費用的每日明細。</span><span class="sxs-lookup"><span data-stu-id="ac146-104">The Usage Detail API offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="ac146-105">結果也包含執行個體、計量和部門的資訊。</span><span class="sxs-lookup"><span data-stu-id="ac146-105">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="ac146-106">API 可依計費週期或指定開始和結束日期來查詢。</span><span class="sxs-lookup"><span data-stu-id="ac146-106">The API can be queried by Billing period or by a specified start and end date.</span></span> 
## <a name="consumption-apis"></a><span data-ttu-id="ac146-107">使用情況 API</span><span class="sxs-lookup"><span data-stu-id="ac146-107">Consumption APIs</span></span>


##<a name="request"></a><span data-ttu-id="ac146-108">要求</span><span class="sxs-lookup"><span data-stu-id="ac146-108">Request</span></span> 
<span data-ttu-id="ac146-109">需要新增的常見標頭屬性在[這裡](billing-enterprise-api.md)詳述。</span><span class="sxs-lookup"><span data-stu-id="ac146-109">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="ac146-110">如果未指定計費週期，則會傳回目前計費週期的資料。</span><span class="sxs-lookup"><span data-stu-id="ac146-110">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="ac146-111">可以使用格式為 yyyy-MM-dd 的開始和結束日期參數來指定自訂的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="ac146-111">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd.</span></span> <span data-ttu-id="ac146-112">支援的最大時間範圍是 36 個月。</span><span class="sxs-lookup"><span data-stu-id="ac146-112">The maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="ac146-113">方法</span><span class="sxs-lookup"><span data-stu-id="ac146-113">Method</span></span> | <span data-ttu-id="ac146-114">要求 URI</span><span class="sxs-lookup"><span data-stu-id="ac146-114">Request URI</span></span>|
|-|-|
|<span data-ttu-id="ac146-115">GET</span><span class="sxs-lookup"><span data-stu-id="ac146-115">GET</span></span>|<span data-ttu-id="ac146-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="ac146-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span></span> 
|<span data-ttu-id="ac146-117">GET</span><span class="sxs-lookup"><span data-stu-id="ac146-117">GET</span></span>|<span data-ttu-id="ac146-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="ac146-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span></span>|
|<span data-ttu-id="ac146-119">GET</span><span class="sxs-lookup"><span data-stu-id="ac146-119">GET</span></span>|<span data-ttu-id="ac146-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="ac146-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="ac146-121">若要使用 API 的預覽版本，請將上述 URL 中的 v2 取代為 v1。</span><span class="sxs-lookup"><span data-stu-id="ac146-121">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="ac146-122">Response</span><span class="sxs-lookup"><span data-stu-id="ac146-122">Response</span></span>

> <span data-ttu-id="ac146-123">由於結果的資料可能會相當龐大，因此結果集會以多個頁面顯示。</span><span class="sxs-lookup"><span data-stu-id="ac146-123">Due to the potentially large volume of data the result set is paged.</span></span> <span data-ttu-id="ac146-124">nextLink 屬性 (若存在) 會指定下一個資料分頁的連結。</span><span class="sxs-lookup"><span data-stu-id="ac146-124">The nextLink property, if present, specifies the link for the next page of data.</span></span> <span data-ttu-id="ac146-125">如果連結是空的，則表示該分頁是最後一個分頁。</span><span class="sxs-lookup"><span data-stu-id="ac146-125">If the link is empty, it denotes that is the last page.</span></span> 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/><span data-ttu-id="ac146-126">
**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="ac146-126">
**Response property definitions**</span></span>

|<span data-ttu-id="ac146-127">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="ac146-127">Property Name</span></span>| <span data-ttu-id="ac146-128">類型</span><span class="sxs-lookup"><span data-stu-id="ac146-128">Type</span></span>| <span data-ttu-id="ac146-129">說明</span><span class="sxs-lookup"><span data-stu-id="ac146-129">Description</span></span>
|-|-|-|
|<span data-ttu-id="ac146-130">id</span><span class="sxs-lookup"><span data-stu-id="ac146-130">id</span></span>| <span data-ttu-id="ac146-131">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-131">string</span></span>| <span data-ttu-id="ac146-132">API 呼叫的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac146-132">The unique Id for the API call.</span></span> |
|<span data-ttu-id="ac146-133">data</span><span class="sxs-lookup"><span data-stu-id="ac146-133">data</span></span>| <span data-ttu-id="ac146-134">JSON 陣列</span><span class="sxs-lookup"><span data-stu-id="ac146-134">JSON array</span></span>| <span data-ttu-id="ac146-135">每個執行個體\計量的每日使用量詳細資料陣列。</span><span class="sxs-lookup"><span data-stu-id="ac146-135">The Array of daily usage details for every instance\meter.</span></span>|
|<span data-ttu-id="ac146-136">nextLink</span><span class="sxs-lookup"><span data-stu-id="ac146-136">nextLink</span></span>| <span data-ttu-id="ac146-137">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-137">string</span></span>| <span data-ttu-id="ac146-138">當有更多的資料分頁時，nextLink 會指向能傳回下一個資料分頁的 URL。</span><span class="sxs-lookup"><span data-stu-id="ac146-138">When there are more pages of data the nextLink points to the URL to return the next page of data.</span></span> |
|<span data-ttu-id="ac146-139">accountId</span><span class="sxs-lookup"><span data-stu-id="ac146-139">accountId</span></span>| <span data-ttu-id="ac146-140">int</span><span class="sxs-lookup"><span data-stu-id="ac146-140">int</span></span>| <span data-ttu-id="ac146-141">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac146-141">Obsolete field.</span></span> <span data-ttu-id="ac146-142">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="ac146-142">Present for backward compatibility.</span></span> |
|<span data-ttu-id="ac146-143">productId</span><span class="sxs-lookup"><span data-stu-id="ac146-143">productId</span></span>| <span data-ttu-id="ac146-144">int</span><span class="sxs-lookup"><span data-stu-id="ac146-144">int</span></span>| <span data-ttu-id="ac146-145">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac146-145">Obsolete field.</span></span> <span data-ttu-id="ac146-146">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="ac146-146">Present for backward compatibility.</span></span> |
|<span data-ttu-id="ac146-147">resourceLocationId</span><span class="sxs-lookup"><span data-stu-id="ac146-147">resourceLocationId</span></span>| <span data-ttu-id="ac146-148">int</span><span class="sxs-lookup"><span data-stu-id="ac146-148">int</span></span>| <span data-ttu-id="ac146-149">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac146-149">Obsolete field.</span></span> <span data-ttu-id="ac146-150">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="ac146-150">Present for backward compatibility.</span></span> |
|<span data-ttu-id="ac146-151">consumedServiceID</span><span class="sxs-lookup"><span data-stu-id="ac146-151">consumedServiceID</span></span>| <span data-ttu-id="ac146-152">int</span><span class="sxs-lookup"><span data-stu-id="ac146-152">int</span></span>| <span data-ttu-id="ac146-153">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac146-153">Obsolete field.</span></span> <span data-ttu-id="ac146-154">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="ac146-154">Present for backward compatibility.</span></span> |
|<span data-ttu-id="ac146-155">departmentId</span><span class="sxs-lookup"><span data-stu-id="ac146-155">departmentId</span></span>| <span data-ttu-id="ac146-156">int</span><span class="sxs-lookup"><span data-stu-id="ac146-156">int</span></span>| <span data-ttu-id="ac146-157">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac146-157">Obsolete field.</span></span> <span data-ttu-id="ac146-158">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="ac146-158">Present for backward compatibility.</span></span> |
|<span data-ttu-id="ac146-159">accountOwnerEmail</span><span class="sxs-lookup"><span data-stu-id="ac146-159">accountOwnerEmail</span></span>| <span data-ttu-id="ac146-160">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-160">string</span></span>| <span data-ttu-id="ac146-161">帳戶擁有者的電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac146-161">Email account of the account owner.</span></span> |
|<span data-ttu-id="ac146-162">accountName</span><span class="sxs-lookup"><span data-stu-id="ac146-162">accountName</span></span>| <span data-ttu-id="ac146-163">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-163">string</span></span>| <span data-ttu-id="ac146-164">客戶輸入的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ac146-164">Customer entered name of the account.</span></span> |
|<span data-ttu-id="ac146-165">serviceAdministratorId</span><span class="sxs-lookup"><span data-stu-id="ac146-165">serviceAdministratorId</span></span>| <span data-ttu-id="ac146-166">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-166">string</span></span>| <span data-ttu-id="ac146-167">服務系統管理員的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ac146-167">Email Address of Service Administrator.</span></span> |
|<span data-ttu-id="ac146-168">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="ac146-168">subscriptionId</span></span>| <span data-ttu-id="ac146-169">int</span><span class="sxs-lookup"><span data-stu-id="ac146-169">int</span></span>| <span data-ttu-id="ac146-170">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="ac146-170">Obsolete field.</span></span> <span data-ttu-id="ac146-171">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="ac146-171">Present for backward compatibility.</span></span> |
|<span data-ttu-id="ac146-172">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="ac146-172">subscriptionGuid</span></span>| <span data-ttu-id="ac146-173">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-173">string</span></span>| <span data-ttu-id="ac146-174">訂用帳戶的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac146-174">Global Unique Identifier for the subscription.</span></span> |
|<span data-ttu-id="ac146-175">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="ac146-175">subscriptionName</span></span>| <span data-ttu-id="ac146-176">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-176">string</span></span>| <span data-ttu-id="ac146-177">訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="ac146-177">Name of the subscription.</span></span> |
|<span data-ttu-id="ac146-178">日期</span><span class="sxs-lookup"><span data-stu-id="ac146-178">date</span></span>| <span data-ttu-id="ac146-179">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-179">string</span></span>| <span data-ttu-id="ac146-180">取用的發生日期。</span><span class="sxs-lookup"><span data-stu-id="ac146-180">The date on which consumption occurred.</span></span> |
|<span data-ttu-id="ac146-181">product</span><span class="sxs-lookup"><span data-stu-id="ac146-181">product</span></span>| <span data-ttu-id="ac146-182">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-182">string</span></span>| <span data-ttu-id="ac146-183">計量的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ac146-183">Additional details on the meter.</span></span> <span data-ttu-id="ac146-184">範例：A1(VM)Windows - 亞太地區東部</span><span class="sxs-lookup"><span data-stu-id="ac146-184">Example: A1(VM)Windows - AP East</span></span>|
|<span data-ttu-id="ac146-185">meterId</span><span class="sxs-lookup"><span data-stu-id="ac146-185">meterId</span></span>| <span data-ttu-id="ac146-186">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-186">string</span></span>| <span data-ttu-id="ac146-187">發出使用量之計量的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac146-187">The identifier for the meter which emitted usage.</span></span> |
|<span data-ttu-id="ac146-188">meterCategory</span><span class="sxs-lookup"><span data-stu-id="ac146-188">meterCategory</span></span>| <span data-ttu-id="ac146-189">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-189">string</span></span>| <span data-ttu-id="ac146-190">所使用的 Azure 平台服務。</span><span class="sxs-lookup"><span data-stu-id="ac146-190">The Azure platform service that was used.</span></span> |
|<span data-ttu-id="ac146-191">meterSubCategory</span><span class="sxs-lookup"><span data-stu-id="ac146-191">meterSubCategory</span></span>| <span data-ttu-id="ac146-192">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-192">string</span></span>| <span data-ttu-id="ac146-193">定義可能會影響費率的 Azure 服務類型。</span><span class="sxs-lookup"><span data-stu-id="ac146-193">Defines the Azure service type that can affect the rate.</span></span> <span data-ttu-id="ac146-194">範例：A1 VM (非 Windows)</span><span class="sxs-lookup"><span data-stu-id="ac146-194">Example: A1 VM (Non-Windows</span></span>|
|<span data-ttu-id="ac146-195">meterRegion</span><span class="sxs-lookup"><span data-stu-id="ac146-195">meterRegion</span></span>| <span data-ttu-id="ac146-196">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-196">string</span></span>| <span data-ttu-id="ac146-197">針對根據資料中心位置定價的某些服務，識別資料中心的位置。</span><span class="sxs-lookup"><span data-stu-id="ac146-197">Identifies the location of the datacenter for certain services that are priced based on datacenter location.</span></span> |
|<span data-ttu-id="ac146-198">meterName</span><span class="sxs-lookup"><span data-stu-id="ac146-198">meterName</span></span>| <span data-ttu-id="ac146-199">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-199">string</span></span>| <span data-ttu-id="ac146-200">計量的名稱。</span><span class="sxs-lookup"><span data-stu-id="ac146-200">Name of the meter.</span></span> |
|<span data-ttu-id="ac146-201">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="ac146-201">consumedQuantity</span></span>| <span data-ttu-id="ac146-202">double</span><span class="sxs-lookup"><span data-stu-id="ac146-202">double</span></span>| <span data-ttu-id="ac146-203">已耗用的計量數量。</span><span class="sxs-lookup"><span data-stu-id="ac146-203">The amount of the meter that has been consumed.</span></span> |
|<span data-ttu-id="ac146-204">resourceRate</span><span class="sxs-lookup"><span data-stu-id="ac146-204">resourceRate</span></span>| <span data-ttu-id="ac146-205">double</span><span class="sxs-lookup"><span data-stu-id="ac146-205">double</span></span>| <span data-ttu-id="ac146-206">每個可計費單位的適用費率。</span><span class="sxs-lookup"><span data-stu-id="ac146-206">The rate applicable per billable unit.</span></span> |
|<span data-ttu-id="ac146-207">cost</span><span class="sxs-lookup"><span data-stu-id="ac146-207">cost</span></span>| <span data-ttu-id="ac146-208">double</span><span class="sxs-lookup"><span data-stu-id="ac146-208">double</span></span>| <span data-ttu-id="ac146-209">計量已產生的費用。</span><span class="sxs-lookup"><span data-stu-id="ac146-209">The charge that has been incurred for the meter.</span></span> |
|<span data-ttu-id="ac146-210">resourceLocation</span><span class="sxs-lookup"><span data-stu-id="ac146-210">resourceLocation</span></span>| <span data-ttu-id="ac146-211">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-211">string</span></span>| <span data-ttu-id="ac146-212">識別正在執行計量的資料中心。</span><span class="sxs-lookup"><span data-stu-id="ac146-212">Identifies the datacenter where the meter is running.</span></span> |
|<span data-ttu-id="ac146-213">consumedService</span><span class="sxs-lookup"><span data-stu-id="ac146-213">consumedService</span></span>| <span data-ttu-id="ac146-214">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-214">string</span></span>| <span data-ttu-id="ac146-215">所使用的 Azure 平台服務。</span><span class="sxs-lookup"><span data-stu-id="ac146-215">The Azure platform service that was used.</span></span> |
|<span data-ttu-id="ac146-216">instanceId</span><span class="sxs-lookup"><span data-stu-id="ac146-216">instanceId</span></span>| <span data-ttu-id="ac146-217">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-217">string</span></span>| <span data-ttu-id="ac146-218">此識別碼是資源的名稱或完整的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac146-218">This identifier is the name of the resource or the fully qualified Resource ID.</span></span> <span data-ttu-id="ac146-219">如需詳細資訊，請參閱 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)</span><span class="sxs-lookup"><span data-stu-id="ac146-219">For more information, see [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)</span></span> |
|<span data-ttu-id="ac146-220">serviceInfo1</span><span class="sxs-lookup"><span data-stu-id="ac146-220">serviceInfo1</span></span>| <span data-ttu-id="ac146-221">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-221">string</span></span>| <span data-ttu-id="ac146-222">內部的 Azure 服務中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ac146-222">Internal Azure Service Metadata.</span></span> |
|<span data-ttu-id="ac146-223">serviceInfo2</span><span class="sxs-lookup"><span data-stu-id="ac146-223">serviceInfo2</span></span>| <span data-ttu-id="ac146-224">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-224">string</span></span>| <span data-ttu-id="ac146-225">例如，虛擬機器的映像類型和 ExpressRoute 的 ISP 名稱。</span><span class="sxs-lookup"><span data-stu-id="ac146-225">For example, an image type for a virtual machine and ISP name for ExpressRoute.</span></span> |
|<span data-ttu-id="ac146-226">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="ac146-226">additionalInfo</span></span>| <span data-ttu-id="ac146-227">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-227">string</span></span>| <span data-ttu-id="ac146-228">服務專屬的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ac146-228">Service-specific metadata.</span></span> <span data-ttu-id="ac146-229">例如，虛擬機器的影像類型。</span><span class="sxs-lookup"><span data-stu-id="ac146-229">For example, an image type for a virtual machine.</span></span> |
|<span data-ttu-id="ac146-230">tags</span><span class="sxs-lookup"><span data-stu-id="ac146-230">tags</span></span>| <span data-ttu-id="ac146-231">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-231">string</span></span>| <span data-ttu-id="ac146-232">客戶已新增的標記。</span><span class="sxs-lookup"><span data-stu-id="ac146-232">Customer added tags.</span></span> <span data-ttu-id="ac146-233">如需詳細資訊，請參閱[使用標記組織您的 Azure 資源](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags)。</span><span class="sxs-lookup"><span data-stu-id="ac146-233">For more information, see [Organize your Azure resources with tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags).</span></span> |
|<span data-ttu-id="ac146-234">storeServiceIdentifier</span><span class="sxs-lookup"><span data-stu-id="ac146-234">storeServiceIdentifier</span></span>| <span data-ttu-id="ac146-235">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-235">string</span></span>| <span data-ttu-id="ac146-236">不會使用這個資料行。</span><span class="sxs-lookup"><span data-stu-id="ac146-236">This columns is not used.</span></span> <span data-ttu-id="ac146-237">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="ac146-237">Present for backward compatibility.</span></span> |
|<span data-ttu-id="ac146-238">departmentName</span><span class="sxs-lookup"><span data-stu-id="ac146-238">departmentName</span></span>| <span data-ttu-id="ac146-239">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-239">string</span></span>| <span data-ttu-id="ac146-240">部門名稱。</span><span class="sxs-lookup"><span data-stu-id="ac146-240">Name of the department.</span></span> |
|<span data-ttu-id="ac146-241">costCenter</span><span class="sxs-lookup"><span data-stu-id="ac146-241">costCenter</span></span>| <span data-ttu-id="ac146-242">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-242">string</span></span>| <span data-ttu-id="ac146-243">使用量的相關聯成本中心。</span><span class="sxs-lookup"><span data-stu-id="ac146-243">The cost center that the usage is associated with.</span></span> |
|<span data-ttu-id="ac146-244">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="ac146-244">unitOfMeasure</span></span>| <span data-ttu-id="ac146-245">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-245">string</span></span>| <span data-ttu-id="ac146-246">識別服務的計費單位。</span><span class="sxs-lookup"><span data-stu-id="ac146-246">Identifies the unit that the service is charged in.</span></span> <span data-ttu-id="ac146-247">範例：GB、小時、10,000 秒。</span><span class="sxs-lookup"><span data-stu-id="ac146-247">Example: GB, hours, 10,000 s.</span></span> |
|<span data-ttu-id="ac146-248">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac146-248">resourceGroup</span></span>| <span data-ttu-id="ac146-249">字串</span><span class="sxs-lookup"><span data-stu-id="ac146-249">string</span></span>| <span data-ttu-id="ac146-250">部署的資源正在其中執行的計量群組。</span><span class="sxs-lookup"><span data-stu-id="ac146-250">The resource group in which the deployed meter is running in.</span></span> <span data-ttu-id="ac146-251">如需詳細資訊，請參閱 [Azure Resource Manager 概觀](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。</span><span class="sxs-lookup"><span data-stu-id="ac146-251">For more information, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span> |
<br/>
## <a name="see-also"></a><span data-ttu-id="ac146-252">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ac146-252">See also</span></span>

* [<span data-ttu-id="ac146-253">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="ac146-253">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="ac146-254">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="ac146-254">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="ac146-255">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="ac146-255">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="ac146-256">價位表 API</span><span class="sxs-lookup"><span data-stu-id="ac146-256">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
