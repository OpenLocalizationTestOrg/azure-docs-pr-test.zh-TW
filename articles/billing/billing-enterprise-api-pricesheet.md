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
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>適用於企業客戶的報告 API - PriceSheet

hello 價位表 API 提供 hello 註冊和帳單週期的每個計量表 hello 適用的速率。

##<a name="request"></a>要求
指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。 如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。

|方法 | 要求 URI|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet|

> [!Note]
> toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。
>

## <a name="response"></a>Response

    
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
>如果您使用 hello 預覽應用程式開發介面，就無法使用 meterId 欄位。
>

**回應屬性定義**

|屬性名稱| 類型| 說明
|-|-|-|
|id| 字串| hello 代表特定 PriceSheet 項目 （由計費週期的計量表） 的唯一識別碼|
|billingPeriodId| 字串| hello 代表特定的計費週期的唯一識別碼|
|meterId| 字串| hello 識別碼 hello 計量表。 它可以是對應的 toohello 使用量 meterId。|
|meterName| 字串| hello 計量表名稱|
|unitOfMeasure| 字串| hello 的度量單位來測量 hello 服務|
|includedQuantity| decimal| 包含的數量 |
|partNumber| 字串| hello 計量表相關聯的 hello 零件編號|
|unitPrice| decimal| hello 單價的 hello 計量表|
|currencyCode| 字串| hello unitPrice 的 hello 貨幣代碼|
<br/>
## <a name="see-also"></a>另請參閱

* [計費週期 API](billing-enterprise-api-billing-periods.md)

* [使用量詳細資料 API](billing-enterprise-api-usage-detail.md)

* [餘額與摘要 API](billing-enterprise-api-balance-summary.md)

* [Marketplace 市集費用 API](billing-enterprise-api-marketplace-storecharge.md)
