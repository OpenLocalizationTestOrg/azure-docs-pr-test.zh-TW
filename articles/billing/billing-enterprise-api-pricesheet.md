---
title: "aaaAzure 計費企業應用程式開發介面層 PriceSheet |Microsoft 文件"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="971aa-103">適用於企業客戶的報告 API - PriceSheet</span><span class="sxs-lookup"><span data-stu-id="971aa-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="971aa-104">hello 價位表 API 提供 hello 註冊和帳單週期的每個計量表 hello 適用的速率。</span><span class="sxs-lookup"><span data-stu-id="971aa-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="971aa-105">要求</span><span class="sxs-lookup"><span data-stu-id="971aa-105">Request</span></span>
<span data-ttu-id="971aa-106">指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。</span><span class="sxs-lookup"><span data-stu-id="971aa-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="971aa-107">如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。</span><span class="sxs-lookup"><span data-stu-id="971aa-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="971aa-108">方法</span><span class="sxs-lookup"><span data-stu-id="971aa-108">Method</span></span> | <span data-ttu-id="971aa-109">要求 URI</span><span class="sxs-lookup"><span data-stu-id="971aa-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="971aa-110">GET</span><span class="sxs-lookup"><span data-stu-id="971aa-110">GET</span></span>|<span data-ttu-id="971aa-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="971aa-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="971aa-112">GET</span><span class="sxs-lookup"><span data-stu-id="971aa-112">GET</span></span>|<span data-ttu-id="971aa-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="971aa-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="971aa-114">toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。</span><span class="sxs-lookup"><span data-stu-id="971aa-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="971aa-115">Response</span><span class="sxs-lookup"><span data-stu-id="971aa-115">Response</span></span>

    
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
><span data-ttu-id="971aa-116">如果您使用 hello 預覽應用程式開發介面，就無法使用 meterId 欄位。</span><span class="sxs-lookup"><span data-stu-id="971aa-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="971aa-117">**回應屬性定義**</span><span class="sxs-lookup"><span data-stu-id="971aa-117">**Response property definitions**</span></span>

|<span data-ttu-id="971aa-118">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="971aa-118">Property Name</span></span>| <span data-ttu-id="971aa-119">類型</span><span class="sxs-lookup"><span data-stu-id="971aa-119">Type</span></span>| <span data-ttu-id="971aa-120">說明</span><span class="sxs-lookup"><span data-stu-id="971aa-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="971aa-121">id</span><span class="sxs-lookup"><span data-stu-id="971aa-121">id</span></span>| <span data-ttu-id="971aa-122">字串</span><span class="sxs-lookup"><span data-stu-id="971aa-122">string</span></span>| <span data-ttu-id="971aa-123">hello 代表特定 PriceSheet 項目 （由計費週期的計量表） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="971aa-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="971aa-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="971aa-124">billingPeriodId</span></span>| <span data-ttu-id="971aa-125">字串</span><span class="sxs-lookup"><span data-stu-id="971aa-125">string</span></span>| <span data-ttu-id="971aa-126">hello 代表特定的計費週期的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="971aa-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="971aa-127">meterId</span><span class="sxs-lookup"><span data-stu-id="971aa-127">meterId</span></span>| <span data-ttu-id="971aa-128">字串</span><span class="sxs-lookup"><span data-stu-id="971aa-128">string</span></span>| <span data-ttu-id="971aa-129">hello 識別碼 hello 計量表。</span><span class="sxs-lookup"><span data-stu-id="971aa-129">hello identifier for hello meter.</span></span> <span data-ttu-id="971aa-130">它可以是對應的 toohello 使用量 meterId。</span><span class="sxs-lookup"><span data-stu-id="971aa-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="971aa-131">meterName</span><span class="sxs-lookup"><span data-stu-id="971aa-131">meterName</span></span>| <span data-ttu-id="971aa-132">字串</span><span class="sxs-lookup"><span data-stu-id="971aa-132">string</span></span>| <span data-ttu-id="971aa-133">hello 計量表名稱</span><span class="sxs-lookup"><span data-stu-id="971aa-133">hello meter name</span></span>|
|<span data-ttu-id="971aa-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="971aa-134">unitOfMeasure</span></span>| <span data-ttu-id="971aa-135">字串</span><span class="sxs-lookup"><span data-stu-id="971aa-135">string</span></span>| <span data-ttu-id="971aa-136">hello 的度量單位來測量 hello 服務</span><span class="sxs-lookup"><span data-stu-id="971aa-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="971aa-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="971aa-137">includedQuantity</span></span>| <span data-ttu-id="971aa-138">decimal</span><span class="sxs-lookup"><span data-stu-id="971aa-138">decimal</span></span>| <span data-ttu-id="971aa-139">包含的數量</span><span class="sxs-lookup"><span data-stu-id="971aa-139">Quantity that is included</span></span> |
|<span data-ttu-id="971aa-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="971aa-140">partNumber</span></span>| <span data-ttu-id="971aa-141">字串</span><span class="sxs-lookup"><span data-stu-id="971aa-141">string</span></span>| <span data-ttu-id="971aa-142">hello 計量表相關聯的 hello 零件編號</span><span class="sxs-lookup"><span data-stu-id="971aa-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="971aa-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="971aa-143">unitPrice</span></span>| <span data-ttu-id="971aa-144">decimal</span><span class="sxs-lookup"><span data-stu-id="971aa-144">decimal</span></span>| <span data-ttu-id="971aa-145">hello 單價的 hello 計量表</span><span class="sxs-lookup"><span data-stu-id="971aa-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="971aa-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="971aa-146">currencyCode</span></span>| <span data-ttu-id="971aa-147">字串</span><span class="sxs-lookup"><span data-stu-id="971aa-147">string</span></span>| <span data-ttu-id="971aa-148">hello unitPrice 的 hello 貨幣代碼</span><span class="sxs-lookup"><span data-stu-id="971aa-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="971aa-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="971aa-149">See also</span></span>

* [<span data-ttu-id="971aa-150">計費週期 API</span><span class="sxs-lookup"><span data-stu-id="971aa-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="971aa-151">使用量詳細資料 API</span><span class="sxs-lookup"><span data-stu-id="971aa-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="971aa-152">餘額與摘要 API</span><span class="sxs-lookup"><span data-stu-id="971aa-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="971aa-153">Marketplace 市集費用 API</span><span class="sxs-lookup"><span data-stu-id="971aa-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
