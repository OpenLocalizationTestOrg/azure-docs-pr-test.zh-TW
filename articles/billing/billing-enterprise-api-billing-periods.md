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
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>適用於企業客戶的報告 API - 計費週期

hello 計費週期 API 會傳回依反向時間順序指定註冊的計費週期 hello 的耗用量資料清單。 每個週期包含指向資料-BalanceSummary、 UsageDetails、 Marktplace 費用及 PriceSheet hello 四組 toohello API 路由的屬性。 如果 hello 期間沒有資料，hello 對應的屬性為 null。 


##<a name="request"></a>要求 
指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。 

|方法 | 要求 URI|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。
>

## <a name="response"></a>Response
 
    
    
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
    

**回應屬性定義**

|屬性名稱| 類型| 說明
|-|-|-|
|billingPeriodId| 字串| hello 代表特定的計費週期的唯一識別碼|
|billingStart| datetime| ISO 8601 字串 hello 期間的開始日期|
|billingEnd| datetime| ISO 8601 字串 hello 期間的結束日期|
|balanceSummary| 字串| 這段期間的路由 toohello 平衡摘要資料的 hello URL 路徑|
|usageDetails| 字串| 這段期間的路由 toohello 使用量詳細資料的 hello URL 路徑|
|marketplaceCharges| 字串| hello URL 路徑的這段期間的路由 toohello Marketplace 費用資料|
|priceSheet| 字串| 這段期間的路由 toohello PriceSheet 資料的 hello URL 路徑|

<br/>
## <a name="see-also"></a>另請參閱

* [餘額與摘要 API](billing-enterprise-api-balance-summary.md)

* [使用量詳細資料 API](billing-enterprise-api-usage-detail.md) 

* [Marketplace 市集費用 API](billing-enterprise-api-marketplace-storecharge.md) 

* [價位表 API](billing-enterprise-api-pricesheet.md)