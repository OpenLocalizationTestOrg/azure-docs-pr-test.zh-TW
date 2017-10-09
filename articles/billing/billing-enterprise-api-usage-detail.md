---
title: "aaaAzure 計費企業應用程式開發介面的使用方式詳細資料 |Microsoft 文件"
description: "深入了解 Azure 計費的使用量與 RateCard Api，也就是使用的 tooprovide 深入了解 Azure 資源耗用量和趨勢。"
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a><span data-ttu-id="add18-103">適用於企業客戶的報告 API - 使用量詳細資料</span><span class="sxs-lookup"><span data-stu-id="add18-103">Reporting APIs for Enterprise customers - Usage Details</span></span>

<span data-ttu-id="add18-104">hello 使用量詳細資料 API 提供已使用的數量和所註冊的估計的費用的每日明細。</span><span class="sxs-lookup"><span data-stu-id="add18-104">hello Usage Detail API offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="add18-105">hello 結果也會包含有關執行個體、 公尺和部門。</span><span class="sxs-lookup"><span data-stu-id="add18-105">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="add18-106">您可以查詢 hello API，計費週期或指定的開始和結束日期。</span><span class="sxs-lookup"><span data-stu-id="add18-106">hello API can be queried by Billing period or by a specified start and end date.</span></span> 
## <a name="consumption-apis"></a><span data-ttu-id="add18-107">使用情況 API</span><span class="sxs-lookup"><span data-stu-id="add18-107">Consumption APIs</span></span>


##<a name="request"></a><span data-ttu-id="add18-108">要求</span><span class="sxs-lookup"><span data-stu-id="add18-108">Request</span></span> 
<span data-ttu-id="add18-109">指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。</span><span class="sxs-lookup"><span data-stu-id="add18-109">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="add18-110">如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。</span><span class="sxs-lookup"><span data-stu-id="add18-110">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="add18-111">自訂時間範圍可以指定與 hello 開始和結束日期參數中 hello 格式為 yyyy-mm-dd</span><span class="sxs-lookup"><span data-stu-id="add18-111">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd.</span></span> <span data-ttu-id="add18-112">hello 最大支援的時間範圍為 36 個月。</span><span class="sxs-lookup"><span data-stu-id="add18-112">hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="add18-113">方法</span><span class="sxs-lookup"><span data-stu-id="add18-113">Method</span></span> | <span data-ttu-id="add18-114">要求 URI</span><span class="sxs-lookup"><span data-stu-id="add18-114">Request URI</span></span>|
|-|-|
|<span data-ttu-id="add18-115">GET</span><span class="sxs-lookup"><span data-stu-id="add18-115">GET</span></span>|<span data-ttu-id="add18-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="add18-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span></span> 
|<span data-ttu-id="add18-117">GET</span><span class="sxs-lookup"><span data-stu-id="add18-117">GET</span></span>|<span data-ttu-id="add18-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="add18-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span></span>|
|<span data-ttu-id="add18-119">GET</span><span class="sxs-lookup"><span data-stu-id="add18-119">GET</span></span>|<span data-ttu-id="add18-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="add18-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="add18-121">toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。</span><span class="sxs-lookup"><span data-stu-id="add18-121">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="add18-122">Response</span><span class="sxs-lookup"><span data-stu-id="add18-122">Response</span></span>

> <span data-ttu-id="add18-123">因為 toohello 可能的大型磁碟區資料 hello 結果的分頁集合。</span><span class="sxs-lookup"><span data-stu-id="add18-123">Due toohello potentially large volume of data hello result set is paged.</span></span> <span data-ttu-id="add18-124">hello nextLink 屬性，如果有的話，會指定 hello hello 下一頁資料的連結。</span><span class="sxs-lookup"><span data-stu-id="add18-124">hello nextLink property, if present, specifies hello link for hello next page of data.</span></span> <span data-ttu-id="add18-125">如果 hello 連結是空的它代表的是 hello 最後一頁。</span><span class="sxs-lookup"><span data-stu-id="add18-125">If hello link is empty, it denotes that is hello last page.</span></span> 
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

<br/><span data-ttu-id="add18-126">
**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="add18-126">
**Response property definitions**</span></span>

|<span data-ttu-id="add18-127">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="add18-127">Property Name</span></span>| <span data-ttu-id="add18-128">類型</span><span class="sxs-lookup"><span data-stu-id="add18-128">Type</span></span>| <span data-ttu-id="add18-129">說明</span><span class="sxs-lookup"><span data-stu-id="add18-129">Description</span></span>
|-|-|-|
|<span data-ttu-id="add18-130">id</span><span class="sxs-lookup"><span data-stu-id="add18-130">id</span></span>| <span data-ttu-id="add18-131">字串</span><span class="sxs-lookup"><span data-stu-id="add18-131">string</span></span>| <span data-ttu-id="add18-132">hello hello API 呼叫的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="add18-132">hello unique Id for hello API call.</span></span> |
|<span data-ttu-id="add18-133">data</span><span class="sxs-lookup"><span data-stu-id="add18-133">data</span></span>| <span data-ttu-id="add18-134">JSON 陣列</span><span class="sxs-lookup"><span data-stu-id="add18-134">JSON array</span></span>| <span data-ttu-id="add18-135">hello 陣列的每個 instance\meter 每日使用量詳細資料。</span><span class="sxs-lookup"><span data-stu-id="add18-135">hello Array of daily usage details for every instance\meter.</span></span>|
|<span data-ttu-id="add18-136">nextLink</span><span class="sxs-lookup"><span data-stu-id="add18-136">nextLink</span></span>| <span data-ttu-id="add18-137">字串</span><span class="sxs-lookup"><span data-stu-id="add18-137">string</span></span>| <span data-ttu-id="add18-138">當有更多頁面資料 hello nextLink 點 toohello URL tooreturn hello 下一頁資料。</span><span class="sxs-lookup"><span data-stu-id="add18-138">When there are more pages of data hello nextLink points toohello URL tooreturn hello next page of data.</span></span> |
|<span data-ttu-id="add18-139">accountId</span><span class="sxs-lookup"><span data-stu-id="add18-139">accountId</span></span>| <span data-ttu-id="add18-140">int</span><span class="sxs-lookup"><span data-stu-id="add18-140">int</span></span>| <span data-ttu-id="add18-141">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="add18-141">Obsolete field.</span></span> <span data-ttu-id="add18-142">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="add18-142">Present for backward compatibility.</span></span> |
|<span data-ttu-id="add18-143">productId</span><span class="sxs-lookup"><span data-stu-id="add18-143">productId</span></span>| <span data-ttu-id="add18-144">int</span><span class="sxs-lookup"><span data-stu-id="add18-144">int</span></span>| <span data-ttu-id="add18-145">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="add18-145">Obsolete field.</span></span> <span data-ttu-id="add18-146">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="add18-146">Present for backward compatibility.</span></span> |
|<span data-ttu-id="add18-147">resourceLocationId</span><span class="sxs-lookup"><span data-stu-id="add18-147">resourceLocationId</span></span>| <span data-ttu-id="add18-148">int</span><span class="sxs-lookup"><span data-stu-id="add18-148">int</span></span>| <span data-ttu-id="add18-149">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="add18-149">Obsolete field.</span></span> <span data-ttu-id="add18-150">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="add18-150">Present for backward compatibility.</span></span> |
|<span data-ttu-id="add18-151">consumedServiceID</span><span class="sxs-lookup"><span data-stu-id="add18-151">consumedServiceID</span></span>| <span data-ttu-id="add18-152">int</span><span class="sxs-lookup"><span data-stu-id="add18-152">int</span></span>| <span data-ttu-id="add18-153">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="add18-153">Obsolete field.</span></span> <span data-ttu-id="add18-154">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="add18-154">Present for backward compatibility.</span></span> |
|<span data-ttu-id="add18-155">departmentId</span><span class="sxs-lookup"><span data-stu-id="add18-155">departmentId</span></span>| <span data-ttu-id="add18-156">int</span><span class="sxs-lookup"><span data-stu-id="add18-156">int</span></span>| <span data-ttu-id="add18-157">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="add18-157">Obsolete field.</span></span> <span data-ttu-id="add18-158">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="add18-158">Present for backward compatibility.</span></span> |
|<span data-ttu-id="add18-159">accountOwnerEmail</span><span class="sxs-lookup"><span data-stu-id="add18-159">accountOwnerEmail</span></span>| <span data-ttu-id="add18-160">字串</span><span class="sxs-lookup"><span data-stu-id="add18-160">string</span></span>| <span data-ttu-id="add18-161">Hello 帳戶擁有者的電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="add18-161">Email account of hello account owner.</span></span> |
|<span data-ttu-id="add18-162">accountName</span><span class="sxs-lookup"><span data-stu-id="add18-162">accountName</span></span>| <span data-ttu-id="add18-163">字串</span><span class="sxs-lookup"><span data-stu-id="add18-163">string</span></span>| <span data-ttu-id="add18-164">輸入客戶 hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="add18-164">Customer entered name of hello account.</span></span> |
|<span data-ttu-id="add18-165">serviceAdministratorId</span><span class="sxs-lookup"><span data-stu-id="add18-165">serviceAdministratorId</span></span>| <span data-ttu-id="add18-166">字串</span><span class="sxs-lookup"><span data-stu-id="add18-166">string</span></span>| <span data-ttu-id="add18-167">服務系統管理員的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="add18-167">Email Address of Service Administrator.</span></span> |
|<span data-ttu-id="add18-168">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="add18-168">subscriptionId</span></span>| <span data-ttu-id="add18-169">int</span><span class="sxs-lookup"><span data-stu-id="add18-169">int</span></span>| <span data-ttu-id="add18-170">已淘汰的欄位。</span><span class="sxs-lookup"><span data-stu-id="add18-170">Obsolete field.</span></span> <span data-ttu-id="add18-171">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="add18-171">Present for backward compatibility.</span></span> |
|<span data-ttu-id="add18-172">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="add18-172">subscriptionGuid</span></span>| <span data-ttu-id="add18-173">字串</span><span class="sxs-lookup"><span data-stu-id="add18-173">string</span></span>| <span data-ttu-id="add18-174">Hello 訂用帳戶的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="add18-174">Global Unique Identifier for hello subscription.</span></span> |
|<span data-ttu-id="add18-175">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="add18-175">subscriptionName</span></span>| <span data-ttu-id="add18-176">字串</span><span class="sxs-lookup"><span data-stu-id="add18-176">string</span></span>| <span data-ttu-id="add18-177">Hello 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="add18-177">Name of hello subscription.</span></span> |
|<span data-ttu-id="add18-178">日期</span><span class="sxs-lookup"><span data-stu-id="add18-178">date</span></span>| <span data-ttu-id="add18-179">字串</span><span class="sxs-lookup"><span data-stu-id="add18-179">string</span></span>| <span data-ttu-id="add18-180">hello 耗用量發生的日期。</span><span class="sxs-lookup"><span data-stu-id="add18-180">hello date on which consumption occurred.</span></span> |
|<span data-ttu-id="add18-181">product</span><span class="sxs-lookup"><span data-stu-id="add18-181">product</span></span>| <span data-ttu-id="add18-182">字串</span><span class="sxs-lookup"><span data-stu-id="add18-182">string</span></span>| <span data-ttu-id="add18-183">Hello 計量表上的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="add18-183">Additional details on hello meter.</span></span> <span data-ttu-id="add18-184">範例：A1(VM)Windows - 亞太地區東部</span><span class="sxs-lookup"><span data-stu-id="add18-184">Example: A1(VM)Windows - AP East</span></span>|
|<span data-ttu-id="add18-185">meterId</span><span class="sxs-lookup"><span data-stu-id="add18-185">meterId</span></span>| <span data-ttu-id="add18-186">字串</span><span class="sxs-lookup"><span data-stu-id="add18-186">string</span></span>| <span data-ttu-id="add18-187">hello 發出使用量 hello 計量表的識別碼。</span><span class="sxs-lookup"><span data-stu-id="add18-187">hello identifier for hello meter which emitted usage.</span></span> |
|<span data-ttu-id="add18-188">meterCategory</span><span class="sxs-lookup"><span data-stu-id="add18-188">meterCategory</span></span>| <span data-ttu-id="add18-189">字串</span><span class="sxs-lookup"><span data-stu-id="add18-189">string</span></span>| <span data-ttu-id="add18-190">hello Azure 平台使用的服務。</span><span class="sxs-lookup"><span data-stu-id="add18-190">hello Azure platform service that was used.</span></span> |
|<span data-ttu-id="add18-191">meterSubCategory</span><span class="sxs-lookup"><span data-stu-id="add18-191">meterSubCategory</span></span>| <span data-ttu-id="add18-192">字串</span><span class="sxs-lookup"><span data-stu-id="add18-192">string</span></span>| <span data-ttu-id="add18-193">定義可能會影響 hello 速率的 hello Azure 服務類型。</span><span class="sxs-lookup"><span data-stu-id="add18-193">Defines hello Azure service type that can affect hello rate.</span></span> <span data-ttu-id="add18-194">範例：A1 VM (非 Windows)</span><span class="sxs-lookup"><span data-stu-id="add18-194">Example: A1 VM (Non-Windows</span></span>|
|<span data-ttu-id="add18-195">meterRegion</span><span class="sxs-lookup"><span data-stu-id="add18-195">meterRegion</span></span>| <span data-ttu-id="add18-196">字串</span><span class="sxs-lookup"><span data-stu-id="add18-196">string</span></span>| <span data-ttu-id="add18-197">識別 hello 資料中心位置為基礎的價格特定服務的 hello 資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="add18-197">Identifies hello location of hello datacenter for certain services that are priced based on datacenter location.</span></span> |
|<span data-ttu-id="add18-198">meterName</span><span class="sxs-lookup"><span data-stu-id="add18-198">meterName</span></span>| <span data-ttu-id="add18-199">字串</span><span class="sxs-lookup"><span data-stu-id="add18-199">string</span></span>| <span data-ttu-id="add18-200">Hello 計量表的名稱。</span><span class="sxs-lookup"><span data-stu-id="add18-200">Name of hello meter.</span></span> |
|<span data-ttu-id="add18-201">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="add18-201">consumedQuantity</span></span>| <span data-ttu-id="add18-202">double</span><span class="sxs-lookup"><span data-stu-id="add18-202">double</span></span>| <span data-ttu-id="add18-203">hello hello 計量表已耗用的數量。</span><span class="sxs-lookup"><span data-stu-id="add18-203">hello amount of hello meter that has been consumed.</span></span> |
|<span data-ttu-id="add18-204">resourceRate</span><span class="sxs-lookup"><span data-stu-id="add18-204">resourceRate</span></span>| <span data-ttu-id="add18-205">double</span><span class="sxs-lookup"><span data-stu-id="add18-205">double</span></span>| <span data-ttu-id="add18-206">hello 速率適用每個計費單位。</span><span class="sxs-lookup"><span data-stu-id="add18-206">hello rate applicable per billable unit.</span></span> |
|<span data-ttu-id="add18-207">cost</span><span class="sxs-lookup"><span data-stu-id="add18-207">cost</span></span>| <span data-ttu-id="add18-208">double</span><span class="sxs-lookup"><span data-stu-id="add18-208">double</span></span>| <span data-ttu-id="add18-209">hello 具有已 hello 計量表所產生的費用。</span><span class="sxs-lookup"><span data-stu-id="add18-209">hello charge that has been incurred for hello meter.</span></span> |
|<span data-ttu-id="add18-210">resourceLocation</span><span class="sxs-lookup"><span data-stu-id="add18-210">resourceLocation</span></span>| <span data-ttu-id="add18-211">字串</span><span class="sxs-lookup"><span data-stu-id="add18-211">string</span></span>| <span data-ttu-id="add18-212">識別 hello hello 計量器執行所在的資料中心。</span><span class="sxs-lookup"><span data-stu-id="add18-212">Identifies hello datacenter where hello meter is running.</span></span> |
|<span data-ttu-id="add18-213">consumedService</span><span class="sxs-lookup"><span data-stu-id="add18-213">consumedService</span></span>| <span data-ttu-id="add18-214">字串</span><span class="sxs-lookup"><span data-stu-id="add18-214">string</span></span>| <span data-ttu-id="add18-215">hello Azure 平台使用的服務。</span><span class="sxs-lookup"><span data-stu-id="add18-215">hello Azure platform service that was used.</span></span> |
|<span data-ttu-id="add18-216">instanceId</span><span class="sxs-lookup"><span data-stu-id="add18-216">instanceId</span></span>| <span data-ttu-id="add18-217">字串</span><span class="sxs-lookup"><span data-stu-id="add18-217">string</span></span>| <span data-ttu-id="add18-218">這個識別碼是 hello hello 資源名稱或 hello 完整資源 id。</span><span class="sxs-lookup"><span data-stu-id="add18-218">This identifier is hello name of hello resource or hello fully qualified Resource ID.</span></span> <span data-ttu-id="add18-219">如需詳細資訊，請參閱 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)</span><span class="sxs-lookup"><span data-stu-id="add18-219">For more information, see [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)</span></span> |
|<span data-ttu-id="add18-220">serviceInfo1</span><span class="sxs-lookup"><span data-stu-id="add18-220">serviceInfo1</span></span>| <span data-ttu-id="add18-221">字串</span><span class="sxs-lookup"><span data-stu-id="add18-221">string</span></span>| <span data-ttu-id="add18-222">內部的 Azure 服務中繼資料。</span><span class="sxs-lookup"><span data-stu-id="add18-222">Internal Azure Service Metadata.</span></span> |
|<span data-ttu-id="add18-223">serviceInfo2</span><span class="sxs-lookup"><span data-stu-id="add18-223">serviceInfo2</span></span>| <span data-ttu-id="add18-224">字串</span><span class="sxs-lookup"><span data-stu-id="add18-224">string</span></span>| <span data-ttu-id="add18-225">例如，虛擬機器的映像類型和 ExpressRoute 的 ISP 名稱。</span><span class="sxs-lookup"><span data-stu-id="add18-225">For example, an image type for a virtual machine and ISP name for ExpressRoute.</span></span> |
|<span data-ttu-id="add18-226">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="add18-226">additionalInfo</span></span>| <span data-ttu-id="add18-227">字串</span><span class="sxs-lookup"><span data-stu-id="add18-227">string</span></span>| <span data-ttu-id="add18-228">服務專屬的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="add18-228">Service-specific metadata.</span></span> <span data-ttu-id="add18-229">例如，虛擬機器的影像類型。</span><span class="sxs-lookup"><span data-stu-id="add18-229">For example, an image type for a virtual machine.</span></span> |
|<span data-ttu-id="add18-230">tags</span><span class="sxs-lookup"><span data-stu-id="add18-230">tags</span></span>| <span data-ttu-id="add18-231">字串</span><span class="sxs-lookup"><span data-stu-id="add18-231">string</span></span>| <span data-ttu-id="add18-232">客戶已新增的標記。</span><span class="sxs-lookup"><span data-stu-id="add18-232">Customer added tags.</span></span> <span data-ttu-id="add18-233">如需詳細資訊，請參閱[使用標記組織您的 Azure 資源](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags)。</span><span class="sxs-lookup"><span data-stu-id="add18-233">For more information, see [Organize your Azure resources with tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags).</span></span> |
|<span data-ttu-id="add18-234">storeServiceIdentifier</span><span class="sxs-lookup"><span data-stu-id="add18-234">storeServiceIdentifier</span></span>| <span data-ttu-id="add18-235">字串</span><span class="sxs-lookup"><span data-stu-id="add18-235">string</span></span>| <span data-ttu-id="add18-236">不會使用這個資料行。</span><span class="sxs-lookup"><span data-stu-id="add18-236">This columns is not used.</span></span> <span data-ttu-id="add18-237">之所以顯示是為了提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="add18-237">Present for backward compatibility.</span></span> |
|<span data-ttu-id="add18-238">departmentName</span><span class="sxs-lookup"><span data-stu-id="add18-238">departmentName</span></span>| <span data-ttu-id="add18-239">字串</span><span class="sxs-lookup"><span data-stu-id="add18-239">string</span></span>| <span data-ttu-id="add18-240">Hello 部門的名稱。</span><span class="sxs-lookup"><span data-stu-id="add18-240">Name of hello department.</span></span> |
|<span data-ttu-id="add18-241">costCenter</span><span class="sxs-lookup"><span data-stu-id="add18-241">costCenter</span></span>| <span data-ttu-id="add18-242">字串</span><span class="sxs-lookup"><span data-stu-id="add18-242">string</span></span>| <span data-ttu-id="add18-243">hello 使用量相關聯的 hello 成本中心。</span><span class="sxs-lookup"><span data-stu-id="add18-243">hello cost center that hello usage is associated with.</span></span> |
|<span data-ttu-id="add18-244">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="add18-244">unitOfMeasure</span></span>| <span data-ttu-id="add18-245">字串</span><span class="sxs-lookup"><span data-stu-id="add18-245">string</span></span>| <span data-ttu-id="add18-246">識別 hello 服務負責中的 hello 單位。</span><span class="sxs-lookup"><span data-stu-id="add18-246">Identifies hello unit that hello service is charged in.</span></span> <span data-ttu-id="add18-247">範例：GB、小時、10,000 秒。</span><span class="sxs-lookup"><span data-stu-id="add18-247">Example: GB, hours, 10,000 s.</span></span> |
|<span data-ttu-id="add18-248">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="add18-248">resourceGroup</span></span>| <span data-ttu-id="add18-249">字串</span><span class="sxs-lookup"><span data-stu-id="add18-249">string</span></span>| <span data-ttu-id="add18-250">hello 資源群組中的 hello 已部署的計量器正在執行中。</span><span class="sxs-lookup"><span data-stu-id="add18-250">hello resource group in which hello deployed meter is running in.</span></span> <span data-ttu-id="add18-251">如需詳細資訊，請參閱 [Azure Resource Manager 概觀](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。</span><span class="sxs-lookup"><span data-stu-id="add18-251">For more information, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span> |
<br/>
## <a name="see-also"></a><span data-ttu-id="add18-252">另請參閱</span><span class="sxs-lookup"><span data-stu-id="add18-252">See also</span></span>

* [<span data-ttu-id="add18-253">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="add18-253">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="add18-254">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="add18-254">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="add18-255">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="add18-255">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="add18-256">價位表 API</span><span class="sxs-lookup"><span data-stu-id="add18-256">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
