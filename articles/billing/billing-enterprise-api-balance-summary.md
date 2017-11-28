---
title: "aaaAzure 計費企業應用程式開發介面的平衡和摘要 |Microsoft 文件"
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="2be16-103">適用於企業客戶的報告 API - 餘額與摘要</span><span class="sxs-lookup"><span data-stu-id="2be16-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="2be16-104">hello 平衡和摘要的應用程式開發介面提供了每月餘額、 購買、 Azure Marketplace 服務費用、 調整和 overage 費用的詳細資訊的摘要。</span><span class="sxs-lookup"><span data-stu-id="2be16-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="2be16-105">要求</span><span class="sxs-lookup"><span data-stu-id="2be16-105">Request</span></span> 
<span data-ttu-id="2be16-106">指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2be16-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="2be16-107">如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。</span><span class="sxs-lookup"><span data-stu-id="2be16-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="2be16-108">方法</span><span class="sxs-lookup"><span data-stu-id="2be16-108">Method</span></span> | <span data-ttu-id="2be16-109">要求 URI</span><span class="sxs-lookup"><span data-stu-id="2be16-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="2be16-110">GET</span><span class="sxs-lookup"><span data-stu-id="2be16-110">GET</span></span>| <span data-ttu-id="2be16-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="2be16-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="2be16-112">GET</span><span class="sxs-lookup"><span data-stu-id="2be16-112">GET</span></span>| <span data-ttu-id="2be16-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="2be16-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="2be16-114">toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。</span><span class="sxs-lookup"><span data-stu-id="2be16-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="2be16-115">Response</span><span class="sxs-lookup"><span data-stu-id="2be16-115">Response</span></span>

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


<span data-ttu-id="2be16-116">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="2be16-116">**Response property definitions**</span></span>

|<span data-ttu-id="2be16-117">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="2be16-117">Property Name</span></span>| <span data-ttu-id="2be16-118">類型</span><span class="sxs-lookup"><span data-stu-id="2be16-118">Type</span></span>| <span data-ttu-id="2be16-119">說明</span><span class="sxs-lookup"><span data-stu-id="2be16-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="2be16-120">id</span><span class="sxs-lookup"><span data-stu-id="2be16-120">id</span></span>|<span data-ttu-id="2be16-121">字串</span><span class="sxs-lookup"><span data-stu-id="2be16-121">string</span></span>|<span data-ttu-id="2be16-122">hello 特定計費期和註冊的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="2be16-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="2be16-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="2be16-123">billingPeriodId</span></span>|<span data-ttu-id="2be16-124">字串</span><span class="sxs-lookup"><span data-stu-id="2be16-124">string</span></span> |<span data-ttu-id="2be16-125">hello 計費週期的識別碼</span><span class="sxs-lookup"><span data-stu-id="2be16-125">hello billing period Id</span></span>|
|<span data-ttu-id="2be16-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="2be16-126">currencyCode</span></span>|<span data-ttu-id="2be16-127">字串</span><span class="sxs-lookup"><span data-stu-id="2be16-127">string</span></span> |<span data-ttu-id="2be16-128">hello 貨幣代碼</span><span class="sxs-lookup"><span data-stu-id="2be16-128">hello currency code</span></span>|
|<span data-ttu-id="2be16-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="2be16-129">beginningBalance</span></span>|<span data-ttu-id="2be16-130">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-130">decimal</span></span>| <span data-ttu-id="2be16-131">hello 計費期的 hello 開始的餘額</span><span class="sxs-lookup"><span data-stu-id="2be16-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="2be16-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="2be16-132">endingBalance</span></span>|<span data-ttu-id="2be16-133">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-133">decimal</span></span>| <span data-ttu-id="2be16-134">hello hello （適用於開啟期間，這將會每日更新） 的計費期的期末餘額</span><span class="sxs-lookup"><span data-stu-id="2be16-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="2be16-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="2be16-135">newPurchases</span></span>|<span data-ttu-id="2be16-136">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-136">decimal</span></span>| <span data-ttu-id="2be16-137">新購買總數</span><span class="sxs-lookup"><span data-stu-id="2be16-137">Total new purchase amount</span></span>|
|<span data-ttu-id="2be16-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="2be16-138">adjustments</span></span>|<span data-ttu-id="2be16-139">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-139">decimal</span></span>| <span data-ttu-id="2be16-140">總調整量</span><span class="sxs-lookup"><span data-stu-id="2be16-140">Total adjustment amount</span></span>|
|<span data-ttu-id="2be16-141">utilized</span><span class="sxs-lookup"><span data-stu-id="2be16-141">utilized</span></span>|<span data-ttu-id="2be16-142">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-142">decimal</span></span>| <span data-ttu-id="2be16-143">總承諾用量</span><span class="sxs-lookup"><span data-stu-id="2be16-143">Total Commitment usage</span></span>|
|<span data-ttu-id="2be16-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="2be16-144">serviceOverage</span></span>|<span data-ttu-id="2be16-145">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-145">decimal</span></span>| <span data-ttu-id="2be16-146">Azure 服務的超額部分</span><span class="sxs-lookup"><span data-stu-id="2be16-146">Overage for Azure services</span></span>|
|<span data-ttu-id="2be16-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="2be16-147">chargesBilledSeparately</span></span>|<span data-ttu-id="2be16-148">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-148">decimal</span></span>| <span data-ttu-id="2be16-149">另外計費的費用</span><span class="sxs-lookup"><span data-stu-id="2be16-149">Charges Billed separately</span></span>|
|<span data-ttu-id="2be16-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="2be16-150">totalOverage</span></span>|<span data-ttu-id="2be16-151">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-151">decimal</span></span>| <span data-ttu-id="2be16-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="2be16-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="2be16-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="2be16-153">totalUsage</span></span>|<span data-ttu-id="2be16-154">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-154">decimal</span></span>| <span data-ttu-id="2be16-155">Azure 服務承諾用量 + 總超額部分</span><span class="sxs-lookup"><span data-stu-id="2be16-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="2be16-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="2be16-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="2be16-157">decimal</span><span class="sxs-lookup"><span data-stu-id="2be16-157">decimal</span></span>| <span data-ttu-id="2be16-158">Azure Marketplace 的總費用</span><span class="sxs-lookup"><span data-stu-id="2be16-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="2be16-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="2be16-159">newPurchasesDetails</span></span>|<span data-ttu-id="2be16-160">名稱值組的 JSON 字串陣列</span><span class="sxs-lookup"><span data-stu-id="2be16-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="2be16-161">新購買的清單</span><span class="sxs-lookup"><span data-stu-id="2be16-161">List of new purchases</span></span>|
|<span data-ttu-id="2be16-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="2be16-162">adjustmentDetails</span></span>|<span data-ttu-id="2be16-163">名稱值組的 JSON 字串陣列</span><span class="sxs-lookup"><span data-stu-id="2be16-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="2be16-164">調整的清單 (促銷信用額度、SIE 信用額度等)</span><span class="sxs-lookup"><span data-stu-id="2be16-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="2be16-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2be16-165">See also</span></span>

* [<span data-ttu-id="2be16-166">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="2be16-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="2be16-167">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="2be16-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="2be16-168">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="2be16-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="2be16-169">價位表 API</span><span class="sxs-lookup"><span data-stu-id="2be16-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)