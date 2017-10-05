---
title: "Azure 計費企業版 API - 計費週期| Microsoft Docs"
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="eb377-103">適用於企業客戶的報告 API - 計費週期</span><span class="sxs-lookup"><span data-stu-id="eb377-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="eb377-104">計費週期 API 會傳回計費週期清單，其中包含所指定註冊的使用情況資料 (以反向時間順序排列)。</span><span class="sxs-lookup"><span data-stu-id="eb377-104">The Billing Periods API returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="eb377-105">每個週期包含指向四組資料 (BalanceSummary、UsageDetails、MarketplaceCharges 和 PriceSheet) 之 API 路由的屬性。</span><span class="sxs-lookup"><span data-stu-id="eb377-105">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="eb377-106">如果該週期沒有資料，則對應的屬性為 Null。</span><span class="sxs-lookup"><span data-stu-id="eb377-106">If the period does not have data, the corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="eb377-107">要求</span><span class="sxs-lookup"><span data-stu-id="eb377-107">Request</span></span> 
<span data-ttu-id="eb377-108">需要新增的常見標頭屬性在[這裡](billing-enterprise-api.md)詳述。</span><span class="sxs-lookup"><span data-stu-id="eb377-108">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="eb377-109">方法</span><span class="sxs-lookup"><span data-stu-id="eb377-109">Method</span></span> | <span data-ttu-id="eb377-110">要求 URI</span><span class="sxs-lookup"><span data-stu-id="eb377-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="eb377-111">GET</span><span class="sxs-lookup"><span data-stu-id="eb377-111">GET</span></span>| <span data-ttu-id="eb377-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="eb377-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="eb377-113">若要使用 API 的預覽版本，請將上述 URL 中的 v2 取代為 v1。</span><span class="sxs-lookup"><span data-stu-id="eb377-113">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="eb377-114">回應</span><span class="sxs-lookup"><span data-stu-id="eb377-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="eb377-115">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="eb377-115">**Response property definitions**</span></span>

|<span data-ttu-id="eb377-116">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="eb377-116">Property Name</span></span>| <span data-ttu-id="eb377-117">類型</span><span class="sxs-lookup"><span data-stu-id="eb377-117">Type</span></span>| <span data-ttu-id="eb377-118">說明</span><span class="sxs-lookup"><span data-stu-id="eb377-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="eb377-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="eb377-119">billingPeriodId</span></span>| <span data-ttu-id="eb377-120">string</span><span class="sxs-lookup"><span data-stu-id="eb377-120">string</span></span>| <span data-ttu-id="eb377-121">表示特定計費週期的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="eb377-121">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="eb377-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="eb377-122">billingStart</span></span>| <span data-ttu-id="eb377-123">datetime</span><span class="sxs-lookup"><span data-stu-id="eb377-123">datetime</span></span>| <span data-ttu-id="eb377-124">表示週期開始日期的 ISO 8601 字串</span><span class="sxs-lookup"><span data-stu-id="eb377-124">ISO 8601 string representing the period start date</span></span>|
|<span data-ttu-id="eb377-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="eb377-125">billingEnd</span></span>| <span data-ttu-id="eb377-126">datetime</span><span class="sxs-lookup"><span data-stu-id="eb377-126">datetime</span></span>| <span data-ttu-id="eb377-127">表示週期結束日期的 ISO 8601 字串</span><span class="sxs-lookup"><span data-stu-id="eb377-127">ISO 8601 string representing the period end date</span></span>|
|<span data-ttu-id="eb377-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="eb377-128">balanceSummary</span></span>| <span data-ttu-id="eb377-129">string</span><span class="sxs-lookup"><span data-stu-id="eb377-129">string</span></span>| <span data-ttu-id="eb377-130">路由到此週期之餘額摘要資料的 URL 路徑</span><span class="sxs-lookup"><span data-stu-id="eb377-130">The URL path that routes to the Balance Summary data for this period</span></span>|
|<span data-ttu-id="eb377-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="eb377-131">usageDetails</span></span>| <span data-ttu-id="eb377-132">字串</span><span class="sxs-lookup"><span data-stu-id="eb377-132">string</span></span>| <span data-ttu-id="eb377-133">路由到此週期之使用量詳細資料的 URL 路徑</span><span class="sxs-lookup"><span data-stu-id="eb377-133">The URL path that routes to the Usage Details data for this period</span></span>|
|<span data-ttu-id="eb377-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="eb377-134">marketplaceCharges</span></span>| <span data-ttu-id="eb377-135">string</span><span class="sxs-lookup"><span data-stu-id="eb377-135">string</span></span>| <span data-ttu-id="eb377-136">路由到此週期之 Marketplace 費用資料的 URL 路徑</span><span class="sxs-lookup"><span data-stu-id="eb377-136">The URL path that routes to the Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="eb377-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="eb377-137">priceSheet</span></span>| <span data-ttu-id="eb377-138">字串</span><span class="sxs-lookup"><span data-stu-id="eb377-138">string</span></span>| <span data-ttu-id="eb377-139">路由到此週期之 PriceSheet 資料的 URL 路徑</span><span class="sxs-lookup"><span data-stu-id="eb377-139">The URL path that routes to the PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="eb377-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="eb377-140">See also</span></span>

* [<span data-ttu-id="eb377-141">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="eb377-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="eb377-142">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="eb377-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="eb377-143">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="eb377-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="eb377-144">價位表 API</span><span class="sxs-lookup"><span data-stu-id="eb377-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)