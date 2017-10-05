---
title: "Azure 計費企業版 API - Marketplace 費用| Microsoft Docs"
description: "了解可讓企業 Azure 客戶以程式設計方式提取使用情況資料的報告 API。"
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
ms.openlocfilehash: 5539623f7ae35e14b6dafe6fdf9efe4bcaba4fd3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="10ea5-103">適用於企業客戶的報告 API - Marketplace 市集費用</span><span class="sxs-lookup"><span data-stu-id="10ea5-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="10ea5-104">Marketplace 市集費用 API 可針對指定的計費週期或開始和結束日期，傳回以使用量為基礎的 Marketplace 費用每日明細 (不含一次性費用)。</span><span class="sxs-lookup"><span data-stu-id="10ea5-104">The Marketplace Store Charge API returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="10ea5-105">要求</span><span class="sxs-lookup"><span data-stu-id="10ea5-105">Request</span></span> 
<span data-ttu-id="10ea5-106">需要新增的常見標頭屬性在[這裡](billing-enterprise-api.md)詳述。</span><span class="sxs-lookup"><span data-stu-id="10ea5-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="10ea5-107">如果未指定計費週期，則會傳回目前計費週期的資料。</span><span class="sxs-lookup"><span data-stu-id="10ea5-107">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="10ea5-108">可以使用格式為 yyyy-MM-dd 的開始和結束日期參數來指定自訂的時間範圍，支援的最大時間範圍是 36 個月。</span><span class="sxs-lookup"><span data-stu-id="10ea5-108">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd, the maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="10ea5-109">方法</span><span class="sxs-lookup"><span data-stu-id="10ea5-109">Method</span></span> | <span data-ttu-id="10ea5-110">要求 URI</span><span class="sxs-lookup"><span data-stu-id="10ea5-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="10ea5-111">GET</span><span class="sxs-lookup"><span data-stu-id="10ea5-111">GET</span></span>|<span data-ttu-id="10ea5-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="10ea5-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="10ea5-113">GET</span><span class="sxs-lookup"><span data-stu-id="10ea5-113">GET</span></span>|<span data-ttu-id="10ea5-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="10ea5-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="10ea5-115">GET</span><span class="sxs-lookup"><span data-stu-id="10ea5-115">GET</span></span>|<span data-ttu-id="10ea5-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="10ea5-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="10ea5-117">若要使用 API 的預覽版本，請將上述 URL 中的 v2 取代為 v1。</span><span class="sxs-lookup"><span data-stu-id="10ea5-117">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="10ea5-118">回應</span><span class="sxs-lookup"><span data-stu-id="10ea5-118">Response</span></span>
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

<span data-ttu-id="10ea5-119">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="10ea5-119">**Response property definitions**</span></span>

|<span data-ttu-id="10ea5-120">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="10ea5-120">Property Name</span></span>| <span data-ttu-id="10ea5-121">類型</span><span class="sxs-lookup"><span data-stu-id="10ea5-121">Type</span></span>| <span data-ttu-id="10ea5-122">說明</span><span class="sxs-lookup"><span data-stu-id="10ea5-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="10ea5-123">id</span><span class="sxs-lookup"><span data-stu-id="10ea5-123">id</span></span>|<span data-ttu-id="10ea5-124">string</span><span class="sxs-lookup"><span data-stu-id="10ea5-124">string</span></span>|<span data-ttu-id="10ea5-125">Marketplace 費用項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="10ea5-125">Unique Id for the marketplace charge item</span></span>|
|<span data-ttu-id="10ea5-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="10ea5-126">subscriptionGuid</span></span>|<span data-ttu-id="10ea5-127">Guid</span><span class="sxs-lookup"><span data-stu-id="10ea5-127">Guid</span></span>|<span data-ttu-id="10ea5-128">訂用帳戶 GUID</span><span class="sxs-lookup"><span data-stu-id="10ea5-128">The Subscription Guid</span></span>|
|<span data-ttu-id="10ea5-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="10ea5-129">subscriptionName</span></span>|<span data-ttu-id="10ea5-130">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-130">string</span></span>|<span data-ttu-id="10ea5-131">訂用帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="10ea5-131">The Subscription Name</span></span>|
|<span data-ttu-id="10ea5-132">meterId</span><span class="sxs-lookup"><span data-stu-id="10ea5-132">meterId</span></span>|<span data-ttu-id="10ea5-133">string</span><span class="sxs-lookup"><span data-stu-id="10ea5-133">string</span></span>|<span data-ttu-id="10ea5-134">所發出計量的識別碼</span><span class="sxs-lookup"><span data-stu-id="10ea5-134">Id for the emitted Meter</span></span>|
|<span data-ttu-id="10ea5-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="10ea5-135">usageStartDate</span></span>|<span data-ttu-id="10ea5-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="10ea5-136">DateTime</span></span>|<span data-ttu-id="10ea5-137">使用量記錄的開始使間</span><span class="sxs-lookup"><span data-stu-id="10ea5-137">Start time for the usage record</span></span>|
|<span data-ttu-id="10ea5-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="10ea5-138">usageEndDate</span></span>|<span data-ttu-id="10ea5-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="10ea5-139">DateTime</span></span>|<span data-ttu-id="10ea5-140">使用量記錄的結束使間</span><span class="sxs-lookup"><span data-stu-id="10ea5-140">End time for the usage record</span></span>|
|<span data-ttu-id="10ea5-141">offerName</span><span class="sxs-lookup"><span data-stu-id="10ea5-141">offerName</span></span>|<span data-ttu-id="10ea5-142">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-142">string</span></span>|<span data-ttu-id="10ea5-143">優惠名稱</span><span class="sxs-lookup"><span data-stu-id="10ea5-143">The Offer name</span></span>|
|<span data-ttu-id="10ea5-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="10ea5-144">resourceGroup</span></span>|<span data-ttu-id="10ea5-145">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-145">string</span></span>|<span data-ttu-id="10ea5-146">資源群組</span><span class="sxs-lookup"><span data-stu-id="10ea5-146">The resource Group</span></span>|
|<span data-ttu-id="10ea5-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="10ea5-147">instanceId</span></span>|<span data-ttu-id="10ea5-148">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-148">string</span></span>|<span data-ttu-id="10ea5-149">執行個體識別碼</span><span class="sxs-lookup"><span data-stu-id="10ea5-149">Instance Id</span></span>|
|<span data-ttu-id="10ea5-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="10ea5-150">additionalInfo</span></span>|<span data-ttu-id="10ea5-151">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-151">string</span></span>|<span data-ttu-id="10ea5-152">其他資訊 JSON 字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-152">Additional info JSON string</span></span>|
|<span data-ttu-id="10ea5-153">tags</span><span class="sxs-lookup"><span data-stu-id="10ea5-153">tags</span></span>|<span data-ttu-id="10ea5-154">string</span><span class="sxs-lookup"><span data-stu-id="10ea5-154">string</span></span>|<span data-ttu-id="10ea5-155">標籤 JSON 字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-155">Tag JSON string</span></span>|
|<span data-ttu-id="10ea5-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="10ea5-156">orderNumber</span></span>|<span data-ttu-id="10ea5-157">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-157">string</span></span>|<span data-ttu-id="10ea5-158">訂單編號</span><span class="sxs-lookup"><span data-stu-id="10ea5-158">The order number</span></span>|
|<span data-ttu-id="10ea5-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="10ea5-159">unitOfMeasure</span></span>|<span data-ttu-id="10ea5-160">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-160">string</span></span>|<span data-ttu-id="10ea5-161">計量的度量單位</span><span class="sxs-lookup"><span data-stu-id="10ea5-161">Unit of measure for the meter</span></span>|
|<span data-ttu-id="10ea5-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="10ea5-162">costCenter</span></span>|<span data-ttu-id="10ea5-163">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-163">string</span></span>|<span data-ttu-id="10ea5-164">成本中心</span><span class="sxs-lookup"><span data-stu-id="10ea5-164">The cost center</span></span>|
|<span data-ttu-id="10ea5-165">accountId</span><span class="sxs-lookup"><span data-stu-id="10ea5-165">accountId</span></span>|<span data-ttu-id="10ea5-166">int</span><span class="sxs-lookup"><span data-stu-id="10ea5-166">int</span></span>|<span data-ttu-id="10ea5-167">帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="10ea5-167">The account Id</span></span>|
|<span data-ttu-id="10ea5-168">accountName</span><span class="sxs-lookup"><span data-stu-id="10ea5-168">accountName</span></span>|<span data-ttu-id="10ea5-169">string</span><span class="sxs-lookup"><span data-stu-id="10ea5-169">string</span></span> |<span data-ttu-id="10ea5-170">帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="10ea5-170">The Account Name</span></span>|
|<span data-ttu-id="10ea5-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="10ea5-171">accountOwnerId</span></span>|<span data-ttu-id="10ea5-172">string</span><span class="sxs-lookup"><span data-stu-id="10ea5-172">string</span></span>|<span data-ttu-id="10ea5-173">帳戶擁有者識別碼</span><span class="sxs-lookup"><span data-stu-id="10ea5-173">The Account Owner Id</span></span>|
|<span data-ttu-id="10ea5-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="10ea5-174">departmentId</span></span>|<span data-ttu-id="10ea5-175">int</span><span class="sxs-lookup"><span data-stu-id="10ea5-175">int</span></span>|<span data-ttu-id="10ea5-176">部門識別碼</span><span class="sxs-lookup"><span data-stu-id="10ea5-176">The department Id</span></span>|
|<span data-ttu-id="10ea5-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="10ea5-177">departmentName</span></span>|<span data-ttu-id="10ea5-178">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-178">string</span></span>|<span data-ttu-id="10ea5-179">部門名稱</span><span class="sxs-lookup"><span data-stu-id="10ea5-179">The department name</span></span>|
|<span data-ttu-id="10ea5-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="10ea5-180">publisherName</span></span>|<span data-ttu-id="10ea5-181">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-181">string</span></span>|<span data-ttu-id="10ea5-182">發行者名稱</span><span class="sxs-lookup"><span data-stu-id="10ea5-182">The publisher name</span></span>|
|<span data-ttu-id="10ea5-183">planName</span><span class="sxs-lookup"><span data-stu-id="10ea5-183">planName</span></span>|<span data-ttu-id="10ea5-184">字串</span><span class="sxs-lookup"><span data-stu-id="10ea5-184">string</span></span>|<span data-ttu-id="10ea5-185">方案名稱</span><span class="sxs-lookup"><span data-stu-id="10ea5-185">The Plan name</span></span>|
|<span data-ttu-id="10ea5-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="10ea5-186">consumedQuantity</span></span>|<span data-ttu-id="10ea5-187">decimal</span><span class="sxs-lookup"><span data-stu-id="10ea5-187">decimal</span></span>|<span data-ttu-id="10ea5-188">此時間週期內的已耗用數量</span><span class="sxs-lookup"><span data-stu-id="10ea5-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="10ea5-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="10ea5-189">resourceRate</span></span>|<span data-ttu-id="10ea5-190">decimal</span><span class="sxs-lookup"><span data-stu-id="10ea5-190">decimal</span></span>|<span data-ttu-id="10ea5-191">計量的單價</span><span class="sxs-lookup"><span data-stu-id="10ea5-191">Unit price for the meter</span></span>|
|<span data-ttu-id="10ea5-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="10ea5-192">extendedCost</span></span>|<span data-ttu-id="10ea5-193">decimal</span><span class="sxs-lookup"><span data-stu-id="10ea5-193">decimal</span></span>|<span data-ttu-id="10ea5-194">根據已耗用數量和延伸成本的預估費用</span><span class="sxs-lookup"><span data-stu-id="10ea5-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="10ea5-195">另請參閱</span><span class="sxs-lookup"><span data-stu-id="10ea5-195">See also</span></span>

* [<span data-ttu-id="10ea5-196">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="10ea5-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="10ea5-197">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="10ea5-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="10ea5-198">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="10ea5-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="10ea5-199">價位表 API</span><span class="sxs-lookup"><span data-stu-id="10ea5-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)