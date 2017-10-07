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
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>適用於企業客戶的報告 API - 餘額與摘要

hello 平衡和摘要的應用程式開發介面提供了每月餘額、 購買、 Azure Marketplace 服務費用、 調整和 overage 費用的詳細資訊的摘要。


##<a name="request"></a>要求 
指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。 如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。

|方法 | 要求 URI|
|-|-|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary|
|GET| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary|

> [!Note]
> toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。
>

## <a name="response"></a>Response

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


**回應屬性定義**

|屬性名稱| 類型| 說明
|-|-|-|
|id|字串|hello 特定計費期和註冊的唯一識別碼|
|billingPeriodId|字串 |hello 計費週期的識別碼|
|currencyCode|字串 |hello 貨幣代碼|
|beginningBalance|decimal| hello 計費期的 hello 開始的餘額|
|endingBalance|decimal| hello hello （適用於開啟期間，這將會每日更新） 的計費期的期末餘額|
|newPurchases|decimal| 新購買總數|
|adjustments|decimal| 總調整量|
|utilized|decimal| 總承諾用量|
|serviceOverage|decimal| Azure 服務的超額部分|
|chargesBilledSeparately|decimal| 另外計費的費用|
|totalOverage|decimal| serviceOverage + chargesBilledSeparately|
|totalUsage|decimal| Azure 服務承諾用量 + 總超額部分|
|azureMarketplaceServiceCharges|decimal| Azure Marketplace 的總費用|
|newPurchasesDetails|名稱值組的 JSON 字串陣列|新購買的清單|
|adjustmentDetails|名稱值組的 JSON 字串陣列|調整的清單 (促銷信用額度、SIE 信用額度等) |


<br/>
## <a name="see-also"></a>另請參閱

* [計費週期 API](billing-enterprise-api-billing-periods.md)

* [使用量詳細資料 API](billing-enterprise-api-usage-detail.md) 

* [Marketplace 市集費用 API](billing-enterprise-api-marketplace-storecharge.md) 

* [價位表 API](billing-enterprise-api-pricesheet.md)