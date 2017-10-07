---
title: "aaaAzure 計費企業應用程式開發介面的計費週期 |Microsoft 文件"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="58234-103">適用於企業客戶的報告 API - 計費週期</span><span class="sxs-lookup"><span data-stu-id="58234-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="58234-104">hello 計費週期 API 會傳回依反向時間順序指定註冊的計費週期 hello 的耗用量資料清單。</span><span class="sxs-lookup"><span data-stu-id="58234-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="58234-105">每個週期包含指向資料-BalanceSummary、 UsageDetails、 Marktplace 費用及 PriceSheet hello 四組 toohello API 路由的屬性。</span><span class="sxs-lookup"><span data-stu-id="58234-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="58234-106">如果 hello 期間沒有資料，hello 對應的屬性為 null。</span><span class="sxs-lookup"><span data-stu-id="58234-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="58234-107">要求</span><span class="sxs-lookup"><span data-stu-id="58234-107">Request</span></span> 
<span data-ttu-id="58234-108">指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。</span><span class="sxs-lookup"><span data-stu-id="58234-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="58234-109">方法</span><span class="sxs-lookup"><span data-stu-id="58234-109">Method</span></span> | <span data-ttu-id="58234-110">要求 URI</span><span class="sxs-lookup"><span data-stu-id="58234-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="58234-111">GET</span><span class="sxs-lookup"><span data-stu-id="58234-111">GET</span></span>| <span data-ttu-id="58234-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="58234-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="58234-113">toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。</span><span class="sxs-lookup"><span data-stu-id="58234-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="58234-114">Response</span><span class="sxs-lookup"><span data-stu-id="58234-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="58234-115">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="58234-115">**Response property definitions**</span></span>

|<span data-ttu-id="58234-116">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="58234-116">Property Name</span></span>| <span data-ttu-id="58234-117">類型</span><span class="sxs-lookup"><span data-stu-id="58234-117">Type</span></span>| <span data-ttu-id="58234-118">說明</span><span class="sxs-lookup"><span data-stu-id="58234-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="58234-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="58234-119">billingPeriodId</span></span>| <span data-ttu-id="58234-120">字串</span><span class="sxs-lookup"><span data-stu-id="58234-120">string</span></span>| <span data-ttu-id="58234-121">hello 代表特定的計費週期的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="58234-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="58234-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="58234-122">billingStart</span></span>| <span data-ttu-id="58234-123">datetime</span><span class="sxs-lookup"><span data-stu-id="58234-123">datetime</span></span>| <span data-ttu-id="58234-124">ISO 8601 字串 hello 期間的開始日期</span><span class="sxs-lookup"><span data-stu-id="58234-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="58234-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="58234-125">billingEnd</span></span>| <span data-ttu-id="58234-126">datetime</span><span class="sxs-lookup"><span data-stu-id="58234-126">datetime</span></span>| <span data-ttu-id="58234-127">ISO 8601 字串 hello 期間的結束日期</span><span class="sxs-lookup"><span data-stu-id="58234-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="58234-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="58234-128">balanceSummary</span></span>| <span data-ttu-id="58234-129">字串</span><span class="sxs-lookup"><span data-stu-id="58234-129">string</span></span>| <span data-ttu-id="58234-130">這段期間的路由 toohello 平衡摘要資料的 hello URL 路徑</span><span class="sxs-lookup"><span data-stu-id="58234-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="58234-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="58234-131">usageDetails</span></span>| <span data-ttu-id="58234-132">字串</span><span class="sxs-lookup"><span data-stu-id="58234-132">string</span></span>| <span data-ttu-id="58234-133">這段期間的路由 toohello 使用量詳細資料的 hello URL 路徑</span><span class="sxs-lookup"><span data-stu-id="58234-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="58234-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="58234-134">marketplaceCharges</span></span>| <span data-ttu-id="58234-135">字串</span><span class="sxs-lookup"><span data-stu-id="58234-135">string</span></span>| <span data-ttu-id="58234-136">hello URL 路徑的這段期間的路由 toohello Marketplace 費用資料</span><span class="sxs-lookup"><span data-stu-id="58234-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="58234-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="58234-137">priceSheet</span></span>| <span data-ttu-id="58234-138">字串</span><span class="sxs-lookup"><span data-stu-id="58234-138">string</span></span>| <span data-ttu-id="58234-139">這段期間的路由 toohello PriceSheet 資料的 hello URL 路徑</span><span class="sxs-lookup"><span data-stu-id="58234-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="58234-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="58234-140">See also</span></span>

* [<span data-ttu-id="58234-141">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="58234-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="58234-142">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="58234-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="58234-143">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="58234-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="58234-144">價位表 API</span><span class="sxs-lookup"><span data-stu-id="58234-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)