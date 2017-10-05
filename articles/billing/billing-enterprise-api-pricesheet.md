---
title: "Azure 計費企業版 API - PriceSheet| Microsoft Docs"
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
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="cb166-103">適用於企業客戶的報告 API - PriceSheet</span><span class="sxs-lookup"><span data-stu-id="cb166-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="cb166-104">價位表 API 可針對指定註冊和計費週期的每個計量提供適用的費率。</span><span class="sxs-lookup"><span data-stu-id="cb166-104">The Price Sheet API provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="cb166-105">要求</span><span class="sxs-lookup"><span data-stu-id="cb166-105">Request</span></span>
<span data-ttu-id="cb166-106">需要新增的常見標頭屬性在[這裡](billing-enterprise-api.md)詳述。</span><span class="sxs-lookup"><span data-stu-id="cb166-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="cb166-107">如果未指定計費週期，則會傳回目前計費週期的資料。</span><span class="sxs-lookup"><span data-stu-id="cb166-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="cb166-108">方法</span><span class="sxs-lookup"><span data-stu-id="cb166-108">Method</span></span> | <span data-ttu-id="cb166-109">要求 URI</span><span class="sxs-lookup"><span data-stu-id="cb166-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="cb166-110">GET</span><span class="sxs-lookup"><span data-stu-id="cb166-110">GET</span></span>|<span data-ttu-id="cb166-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="cb166-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="cb166-112">GET</span><span class="sxs-lookup"><span data-stu-id="cb166-112">GET</span></span>|<span data-ttu-id="cb166-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="cb166-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="cb166-114">若要使用 API 的預覽版本，請將上述 URL 中的 v2 取代為 v1。</span><span class="sxs-lookup"><span data-stu-id="cb166-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="cb166-115">Response</span><span class="sxs-lookup"><span data-stu-id="cb166-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="cb166-116">如果您使用的是預覽版 API，就無法使用 meterId 欄位。</span><span class="sxs-lookup"><span data-stu-id="cb166-116">If you are using the Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="cb166-117">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="cb166-117">**Response property definitions**</span></span>

|<span data-ttu-id="cb166-118">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="cb166-118">Property Name</span></span>| <span data-ttu-id="cb166-119">類型</span><span class="sxs-lookup"><span data-stu-id="cb166-119">Type</span></span>| <span data-ttu-id="cb166-120">說明</span><span class="sxs-lookup"><span data-stu-id="cb166-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="cb166-121">id</span><span class="sxs-lookup"><span data-stu-id="cb166-121">id</span></span>| <span data-ttu-id="cb166-122">string</span><span class="sxs-lookup"><span data-stu-id="cb166-122">string</span></span>| <span data-ttu-id="cb166-123">表示特定 PriceSheet 項目的唯一識別碼 (依計費週期的計量)</span><span class="sxs-lookup"><span data-stu-id="cb166-123">The unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="cb166-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="cb166-124">billingPeriodId</span></span>| <span data-ttu-id="cb166-125">string</span><span class="sxs-lookup"><span data-stu-id="cb166-125">string</span></span>| <span data-ttu-id="cb166-126">表示特定計費週期的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="cb166-126">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="cb166-127">meterId</span><span class="sxs-lookup"><span data-stu-id="cb166-127">meterId</span></span>| <span data-ttu-id="cb166-128">字串</span><span class="sxs-lookup"><span data-stu-id="cb166-128">string</span></span>| <span data-ttu-id="cb166-129">計量的識別碼。</span><span class="sxs-lookup"><span data-stu-id="cb166-129">The identifier for the meter.</span></span> <span data-ttu-id="cb166-130">它可以對應至使用量 meterId。</span><span class="sxs-lookup"><span data-stu-id="cb166-130">It can be mapped to the usage meterId.</span></span>|
|<span data-ttu-id="cb166-131">meterName</span><span class="sxs-lookup"><span data-stu-id="cb166-131">meterName</span></span>| <span data-ttu-id="cb166-132">字串</span><span class="sxs-lookup"><span data-stu-id="cb166-132">string</span></span>| <span data-ttu-id="cb166-133">計量名稱</span><span class="sxs-lookup"><span data-stu-id="cb166-133">The meter name</span></span>|
|<span data-ttu-id="cb166-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="cb166-134">unitOfMeasure</span></span>| <span data-ttu-id="cb166-135">字串</span><span class="sxs-lookup"><span data-stu-id="cb166-135">string</span></span>| <span data-ttu-id="cb166-136">測量服務的度量單位</span><span class="sxs-lookup"><span data-stu-id="cb166-136">The Unit of Measure for measuring the service</span></span>|
|<span data-ttu-id="cb166-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="cb166-137">includedQuantity</span></span>| <span data-ttu-id="cb166-138">decimal</span><span class="sxs-lookup"><span data-stu-id="cb166-138">decimal</span></span>| <span data-ttu-id="cb166-139">包含的數量</span><span class="sxs-lookup"><span data-stu-id="cb166-139">Quantity that is included</span></span> |
|<span data-ttu-id="cb166-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="cb166-140">partNumber</span></span>| <span data-ttu-id="cb166-141">string</span><span class="sxs-lookup"><span data-stu-id="cb166-141">string</span></span>| <span data-ttu-id="cb166-142">與計量相關聯的組件編號</span><span class="sxs-lookup"><span data-stu-id="cb166-142">The part number associated with the Meter</span></span>|
|<span data-ttu-id="cb166-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="cb166-143">unitPrice</span></span>| <span data-ttu-id="cb166-144">decimal</span><span class="sxs-lookup"><span data-stu-id="cb166-144">decimal</span></span>| <span data-ttu-id="cb166-145">計量的單價</span><span class="sxs-lookup"><span data-stu-id="cb166-145">The unit price for the meter</span></span>|
|<span data-ttu-id="cb166-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="cb166-146">currencyCode</span></span>| <span data-ttu-id="cb166-147">字串</span><span class="sxs-lookup"><span data-stu-id="cb166-147">string</span></span>| <span data-ttu-id="cb166-148">unitPrice 的貨幣代碼</span><span class="sxs-lookup"><span data-stu-id="cb166-148">The currency code for the unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="cb166-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cb166-149">See also</span></span>

* [<span data-ttu-id="cb166-150">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="cb166-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="cb166-151">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="cb166-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="cb166-152">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="cb166-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="cb166-153">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="cb166-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
