---
title: "aaaAzure 計費企業應用程式開發介面的 Marketplace 費用 |Microsoft 文件"
description: "深入了解 hello 報告 Api 以程式設計的方式讓企業 Azure 客戶 toopull 耗用量資料。"
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="e17cc-103">適用於企業客戶的報告 API - Marketplace 市集費用</span><span class="sxs-lookup"><span data-stu-id="e17cc-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="e17cc-104">hello Marketplace 商店電量 API 傳回 hello 基於使用方式的 marketplace 費用細目-依日 hello 指定計費期間或開始和結束日期 （一次費用不包含）。</span><span class="sxs-lookup"><span data-stu-id="e17cc-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="e17cc-105">要求</span><span class="sxs-lookup"><span data-stu-id="e17cc-105">Request</span></span> 
<span data-ttu-id="e17cc-106">指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。</span><span class="sxs-lookup"><span data-stu-id="e17cc-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="e17cc-107">如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。</span><span class="sxs-lookup"><span data-stu-id="e17cc-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="e17cc-108">自訂時間範圍可以指定與 hello 開始和結束 hello 格式 yyyy MM dd，hello 支援最大時間範圍是 36 個月中的日期參數。</span><span class="sxs-lookup"><span data-stu-id="e17cc-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="e17cc-109">方法</span><span class="sxs-lookup"><span data-stu-id="e17cc-109">Method</span></span> | <span data-ttu-id="e17cc-110">要求 URI</span><span class="sxs-lookup"><span data-stu-id="e17cc-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="e17cc-111">GET</span><span class="sxs-lookup"><span data-stu-id="e17cc-111">GET</span></span>|<span data-ttu-id="e17cc-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="e17cc-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="e17cc-113">GET</span><span class="sxs-lookup"><span data-stu-id="e17cc-113">GET</span></span>|<span data-ttu-id="e17cc-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="e17cc-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="e17cc-115">GET</span><span class="sxs-lookup"><span data-stu-id="e17cc-115">GET</span></span>|<span data-ttu-id="e17cc-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="e17cc-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="e17cc-117">toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。</span><span class="sxs-lookup"><span data-stu-id="e17cc-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="e17cc-118">Response</span><span class="sxs-lookup"><span data-stu-id="e17cc-118">Response</span></span>
 
    
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
    

<span data-ttu-id="e17cc-119">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="e17cc-119">**Response property definitions**</span></span>

|<span data-ttu-id="e17cc-120">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e17cc-120">Property Name</span></span>| <span data-ttu-id="e17cc-121">類型</span><span class="sxs-lookup"><span data-stu-id="e17cc-121">Type</span></span>| <span data-ttu-id="e17cc-122">說明</span><span class="sxs-lookup"><span data-stu-id="e17cc-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="e17cc-123">id</span><span class="sxs-lookup"><span data-stu-id="e17cc-123">id</span></span>|<span data-ttu-id="e17cc-124">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-124">string</span></span>|<span data-ttu-id="e17cc-125">Hello marketplace 費用項目的唯一 Id</span><span class="sxs-lookup"><span data-stu-id="e17cc-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="e17cc-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="e17cc-126">subscriptionGuid</span></span>|<span data-ttu-id="e17cc-127">Guid</span><span class="sxs-lookup"><span data-stu-id="e17cc-127">Guid</span></span>|<span data-ttu-id="e17cc-128">hello 訂用帳戶 Guid</span><span class="sxs-lookup"><span data-stu-id="e17cc-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="e17cc-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="e17cc-129">subscriptionName</span></span>|<span data-ttu-id="e17cc-130">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-130">string</span></span>|<span data-ttu-id="e17cc-131">hello 訂用帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="e17cc-131">hello Subscription Name</span></span>|
|<span data-ttu-id="e17cc-132">meterId</span><span class="sxs-lookup"><span data-stu-id="e17cc-132">meterId</span></span>|<span data-ttu-id="e17cc-133">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-133">string</span></span>|<span data-ttu-id="e17cc-134">識別碼 hello 發出計量表</span><span class="sxs-lookup"><span data-stu-id="e17cc-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="e17cc-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="e17cc-135">usageStartDate</span></span>|<span data-ttu-id="e17cc-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="e17cc-136">DateTime</span></span>|<span data-ttu-id="e17cc-137">Hello 使用量記錄的開始時間</span><span class="sxs-lookup"><span data-stu-id="e17cc-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="e17cc-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="e17cc-138">usageEndDate</span></span>|<span data-ttu-id="e17cc-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="e17cc-139">DateTime</span></span>|<span data-ttu-id="e17cc-140">Hello 使用量記錄的結束時間</span><span class="sxs-lookup"><span data-stu-id="e17cc-140">End time for hello usage record</span></span>|
|<span data-ttu-id="e17cc-141">offerName</span><span class="sxs-lookup"><span data-stu-id="e17cc-141">offerName</span></span>|<span data-ttu-id="e17cc-142">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-142">string</span></span>|<span data-ttu-id="e17cc-143">hello 供應項目名稱</span><span class="sxs-lookup"><span data-stu-id="e17cc-143">hello Offer name</span></span>|
|<span data-ttu-id="e17cc-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="e17cc-144">resourceGroup</span></span>|<span data-ttu-id="e17cc-145">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-145">string</span></span>|<span data-ttu-id="e17cc-146">hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="e17cc-146">hello resource Group</span></span>|
|<span data-ttu-id="e17cc-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="e17cc-147">instanceId</span></span>|<span data-ttu-id="e17cc-148">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-148">string</span></span>|<span data-ttu-id="e17cc-149">執行個體識別碼</span><span class="sxs-lookup"><span data-stu-id="e17cc-149">Instance Id</span></span>|
|<span data-ttu-id="e17cc-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="e17cc-150">additionalInfo</span></span>|<span data-ttu-id="e17cc-151">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-151">string</span></span>|<span data-ttu-id="e17cc-152">其他資訊 JSON 字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-152">Additional info JSON string</span></span>|
|<span data-ttu-id="e17cc-153">tags</span><span class="sxs-lookup"><span data-stu-id="e17cc-153">tags</span></span>|<span data-ttu-id="e17cc-154">string</span><span class="sxs-lookup"><span data-stu-id="e17cc-154">string</span></span>|<span data-ttu-id="e17cc-155">標籤 JSON 字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-155">Tag JSON string</span></span>|
|<span data-ttu-id="e17cc-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="e17cc-156">orderNumber</span></span>|<span data-ttu-id="e17cc-157">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-157">string</span></span>|<span data-ttu-id="e17cc-158">hello 訂單號碼</span><span class="sxs-lookup"><span data-stu-id="e17cc-158">hello order number</span></span>|
|<span data-ttu-id="e17cc-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="e17cc-159">unitOfMeasure</span></span>|<span data-ttu-id="e17cc-160">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-160">string</span></span>|<span data-ttu-id="e17cc-161">Hello 計量表的測量單位</span><span class="sxs-lookup"><span data-stu-id="e17cc-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="e17cc-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="e17cc-162">costCenter</span></span>|<span data-ttu-id="e17cc-163">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-163">string</span></span>|<span data-ttu-id="e17cc-164">hello 成本中心</span><span class="sxs-lookup"><span data-stu-id="e17cc-164">hello cost center</span></span>|
|<span data-ttu-id="e17cc-165">accountId</span><span class="sxs-lookup"><span data-stu-id="e17cc-165">accountId</span></span>|<span data-ttu-id="e17cc-166">int</span><span class="sxs-lookup"><span data-stu-id="e17cc-166">int</span></span>|<span data-ttu-id="e17cc-167">hello 帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e17cc-167">hello account Id</span></span>|
|<span data-ttu-id="e17cc-168">accountName</span><span class="sxs-lookup"><span data-stu-id="e17cc-168">accountName</span></span>|<span data-ttu-id="e17cc-169">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-169">string</span></span> |<span data-ttu-id="e17cc-170">hello 帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="e17cc-170">hello Account Name</span></span>|
|<span data-ttu-id="e17cc-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="e17cc-171">accountOwnerId</span></span>|<span data-ttu-id="e17cc-172">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-172">string</span></span>|<span data-ttu-id="e17cc-173">hello 帳戶擁有者識別碼</span><span class="sxs-lookup"><span data-stu-id="e17cc-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="e17cc-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="e17cc-174">departmentId</span></span>|<span data-ttu-id="e17cc-175">int</span><span class="sxs-lookup"><span data-stu-id="e17cc-175">int</span></span>|<span data-ttu-id="e17cc-176">hello 部門識別碼</span><span class="sxs-lookup"><span data-stu-id="e17cc-176">hello department Id</span></span>|
|<span data-ttu-id="e17cc-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="e17cc-177">departmentName</span></span>|<span data-ttu-id="e17cc-178">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-178">string</span></span>|<span data-ttu-id="e17cc-179">hello 部門名稱</span><span class="sxs-lookup"><span data-stu-id="e17cc-179">hello department name</span></span>|
|<span data-ttu-id="e17cc-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="e17cc-180">publisherName</span></span>|<span data-ttu-id="e17cc-181">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-181">string</span></span>|<span data-ttu-id="e17cc-182">hello 發行者名稱</span><span class="sxs-lookup"><span data-stu-id="e17cc-182">hello publisher name</span></span>|
|<span data-ttu-id="e17cc-183">planName</span><span class="sxs-lookup"><span data-stu-id="e17cc-183">planName</span></span>|<span data-ttu-id="e17cc-184">字串</span><span class="sxs-lookup"><span data-stu-id="e17cc-184">string</span></span>|<span data-ttu-id="e17cc-185">hello 計劃名稱</span><span class="sxs-lookup"><span data-stu-id="e17cc-185">hello Plan name</span></span>|
|<span data-ttu-id="e17cc-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="e17cc-186">consumedQuantity</span></span>|<span data-ttu-id="e17cc-187">decimal</span><span class="sxs-lookup"><span data-stu-id="e17cc-187">decimal</span></span>|<span data-ttu-id="e17cc-188">此時間週期內的已耗用數量</span><span class="sxs-lookup"><span data-stu-id="e17cc-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="e17cc-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="e17cc-189">resourceRate</span></span>|<span data-ttu-id="e17cc-190">decimal</span><span class="sxs-lookup"><span data-stu-id="e17cc-190">decimal</span></span>|<span data-ttu-id="e17cc-191">單價的 hello 計量表</span><span class="sxs-lookup"><span data-stu-id="e17cc-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="e17cc-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="e17cc-192">extendedCost</span></span>|<span data-ttu-id="e17cc-193">decimal</span><span class="sxs-lookup"><span data-stu-id="e17cc-193">decimal</span></span>|<span data-ttu-id="e17cc-194">根據已耗用數量和延伸成本的預估費用</span><span class="sxs-lookup"><span data-stu-id="e17cc-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="e17cc-195">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e17cc-195">See also</span></span>

* [<span data-ttu-id="e17cc-196">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="e17cc-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="e17cc-197">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="e17cc-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="e17cc-198">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="e17cc-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="e17cc-199">價位表 API</span><span class="sxs-lookup"><span data-stu-id="e17cc-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)