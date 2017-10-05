---
title: "Azure 計費企業版 API - 餘額與摘要| Microsoft Docs"
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
ms.openlocfilehash: f6b149f0e656d2263705048aa5b644f5bb4a5712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="6f4fc-103">適用於企業客戶的報告 API - 餘額與摘要</span><span class="sxs-lookup"><span data-stu-id="6f4fc-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="6f4fc-104">餘額與摘要 API 可提供餘額、新購買、Azure Marketplace 服務費用、調整及超額部分費用的每月摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="6f4fc-104">The Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="6f4fc-105">要求</span><span class="sxs-lookup"><span data-stu-id="6f4fc-105">Request</span></span> 
<span data-ttu-id="6f4fc-106">需要新增的常見標頭屬性在[這裡](billing-enterprise-api.md)詳述。</span><span class="sxs-lookup"><span data-stu-id="6f4fc-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="6f4fc-107">如果未指定計費週期，則會傳回目前計費週期的資料。</span><span class="sxs-lookup"><span data-stu-id="6f4fc-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="6f4fc-108">方法</span><span class="sxs-lookup"><span data-stu-id="6f4fc-108">Method</span></span> | <span data-ttu-id="6f4fc-109">要求 URI</span><span class="sxs-lookup"><span data-stu-id="6f4fc-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="6f4fc-110">GET</span><span class="sxs-lookup"><span data-stu-id="6f4fc-110">GET</span></span>| <span data-ttu-id="6f4fc-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="6f4fc-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="6f4fc-112">GET</span><span class="sxs-lookup"><span data-stu-id="6f4fc-112">GET</span></span>| <span data-ttu-id="6f4fc-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="6f4fc-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="6f4fc-114">若要使用 API 的預覽版本，請將上述 URL 中的 v2 取代為 v1。</span><span class="sxs-lookup"><span data-stu-id="6f4fc-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="6f4fc-115">回應</span><span class="sxs-lookup"><span data-stu-id="6f4fc-115">Response</span></span>

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


<span data-ttu-id="6f4fc-116">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="6f4fc-116">**Response property definitions**</span></span>

|<span data-ttu-id="6f4fc-117">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="6f4fc-117">Property Name</span></span>| <span data-ttu-id="6f4fc-118">類型</span><span class="sxs-lookup"><span data-stu-id="6f4fc-118">Type</span></span>| <span data-ttu-id="6f4fc-119">說明</span><span class="sxs-lookup"><span data-stu-id="6f4fc-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="6f4fc-120">id</span><span class="sxs-lookup"><span data-stu-id="6f4fc-120">id</span></span>|<span data-ttu-id="6f4fc-121">字串</span><span class="sxs-lookup"><span data-stu-id="6f4fc-121">string</span></span>|<span data-ttu-id="6f4fc-122">特定計費週期和註冊的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="6f4fc-122">The unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="6f4fc-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="6f4fc-123">billingPeriodId</span></span>|<span data-ttu-id="6f4fc-124">string</span><span class="sxs-lookup"><span data-stu-id="6f4fc-124">string</span></span> |<span data-ttu-id="6f4fc-125">計費週期識別碼</span><span class="sxs-lookup"><span data-stu-id="6f4fc-125">The billing period Id</span></span>|
|<span data-ttu-id="6f4fc-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="6f4fc-126">currencyCode</span></span>|<span data-ttu-id="6f4fc-127">字串</span><span class="sxs-lookup"><span data-stu-id="6f4fc-127">string</span></span> |<span data-ttu-id="6f4fc-128">貨幣代碼</span><span class="sxs-lookup"><span data-stu-id="6f4fc-128">The currency code</span></span>|
|<span data-ttu-id="6f4fc-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="6f4fc-129">beginningBalance</span></span>|<span data-ttu-id="6f4fc-130">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-130">decimal</span></span>| <span data-ttu-id="6f4fc-131">計費週期的開始餘額</span><span class="sxs-lookup"><span data-stu-id="6f4fc-131">The beginning balance for the billing period</span></span>|
|<span data-ttu-id="6f4fc-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="6f4fc-132">endingBalance</span></span>|<span data-ttu-id="6f4fc-133">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-133">decimal</span></span>| <span data-ttu-id="6f4fc-134">計費週期的結算餘額 (此值在開放期間內會每天更新)</span><span class="sxs-lookup"><span data-stu-id="6f4fc-134">The ending balance for the billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="6f4fc-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="6f4fc-135">newPurchases</span></span>|<span data-ttu-id="6f4fc-136">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-136">decimal</span></span>| <span data-ttu-id="6f4fc-137">新購買總數</span><span class="sxs-lookup"><span data-stu-id="6f4fc-137">Total new purchase amount</span></span>|
|<span data-ttu-id="6f4fc-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="6f4fc-138">adjustments</span></span>|<span data-ttu-id="6f4fc-139">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-139">decimal</span></span>| <span data-ttu-id="6f4fc-140">總調整量</span><span class="sxs-lookup"><span data-stu-id="6f4fc-140">Total adjustment amount</span></span>|
|<span data-ttu-id="6f4fc-141">utilized</span><span class="sxs-lookup"><span data-stu-id="6f4fc-141">utilized</span></span>|<span data-ttu-id="6f4fc-142">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-142">decimal</span></span>| <span data-ttu-id="6f4fc-143">總承諾用量</span><span class="sxs-lookup"><span data-stu-id="6f4fc-143">Total Commitment usage</span></span>|
|<span data-ttu-id="6f4fc-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="6f4fc-144">serviceOverage</span></span>|<span data-ttu-id="6f4fc-145">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-145">decimal</span></span>| <span data-ttu-id="6f4fc-146">Azure 服務的超額部分</span><span class="sxs-lookup"><span data-stu-id="6f4fc-146">Overage for Azure services</span></span>|
|<span data-ttu-id="6f4fc-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="6f4fc-147">chargesBilledSeparately</span></span>|<span data-ttu-id="6f4fc-148">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-148">decimal</span></span>| <span data-ttu-id="6f4fc-149">另外計費的費用</span><span class="sxs-lookup"><span data-stu-id="6f4fc-149">Charges Billed separately</span></span>|
|<span data-ttu-id="6f4fc-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="6f4fc-150">totalOverage</span></span>|<span data-ttu-id="6f4fc-151">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-151">decimal</span></span>| <span data-ttu-id="6f4fc-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="6f4fc-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="6f4fc-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="6f4fc-153">totalUsage</span></span>|<span data-ttu-id="6f4fc-154">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-154">decimal</span></span>| <span data-ttu-id="6f4fc-155">Azure 服務承諾用量 + 總超額部分</span><span class="sxs-lookup"><span data-stu-id="6f4fc-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="6f4fc-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="6f4fc-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="6f4fc-157">decimal</span><span class="sxs-lookup"><span data-stu-id="6f4fc-157">decimal</span></span>| <span data-ttu-id="6f4fc-158">Azure Marketplace 的總費用</span><span class="sxs-lookup"><span data-stu-id="6f4fc-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="6f4fc-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="6f4fc-159">newPurchasesDetails</span></span>|<span data-ttu-id="6f4fc-160">名稱值組的 JSON 字串陣列</span><span class="sxs-lookup"><span data-stu-id="6f4fc-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="6f4fc-161">新購買的清單</span><span class="sxs-lookup"><span data-stu-id="6f4fc-161">List of new purchases</span></span>|
|<span data-ttu-id="6f4fc-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="6f4fc-162">adjustmentDetails</span></span>|<span data-ttu-id="6f4fc-163">名稱值組的 JSON 字串陣列</span><span class="sxs-lookup"><span data-stu-id="6f4fc-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="6f4fc-164">調整的清單 (促銷信用額度、SIE 信用額度等)</span><span class="sxs-lookup"><span data-stu-id="6f4fc-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="6f4fc-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6f4fc-165">See also</span></span>

* [<span data-ttu-id="6f4fc-166">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="6f4fc-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="6f4fc-167">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="6f4fc-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="6f4fc-168">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="6f4fc-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="6f4fc-169">價位表 API</span><span class="sxs-lookup"><span data-stu-id="6f4fc-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)