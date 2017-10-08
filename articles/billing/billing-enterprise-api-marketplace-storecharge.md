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
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>適用於企業客戶的報告 API - Marketplace 市集費用

hello Marketplace 商店電量 API 傳回 hello 基於使用方式的 marketplace 費用細目-依日 hello 指定計費期間或開始和結束日期 （一次費用不包含）。

##<a name="request"></a>要求 
指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。 如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。 自訂時間範圍可以指定與 hello 開始和結束 hello 格式 yyyy MM dd，hello 支援最大時間範圍是 36 個月中的日期參數。  

|方法 | 要求 URI|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。
>

## <a name="response"></a>Response
 
    
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
    

**回應屬性定義**

|屬性名稱| 類型| 說明
|-|-|-|
|id|字串|Hello marketplace 費用項目的唯一 Id|
|subscriptionGuid|Guid|hello 訂用帳戶 Guid|
|subscriptionName|字串|hello 訂用帳戶名稱|
|meterId|字串|識別碼 hello 發出計量表|
|usageStartDate|DateTime|Hello 使用量記錄的開始時間|
|usageEndDate|DateTime|Hello 使用量記錄的結束時間|
|offerName|字串|hello 供應項目名稱|
|resourceGroup|字串|hello 資源群組|
|instanceId|字串|執行個體識別碼|
|additionalInfo|字串|其他資訊 JSON 字串|
|tags|string|標籤 JSON 字串|
|orderNumber|字串|hello 訂單號碼|
|unitOfMeasure|字串|Hello 計量表的測量單位|
|costCenter|字串|hello 成本中心|
|accountId|int|hello 帳戶識別碼|
|accountName|字串 |hello 帳戶名稱|
|accountOwnerId|字串|hello 帳戶擁有者識別碼|
|departmentId|int|hello 部門識別碼|
|departmentName|字串|hello 部門名稱|
|publisherName|字串|hello 發行者名稱|
|planName|字串|hello 計劃名稱|
|consumedQuantity|decimal|此時間週期內的已耗用數量|
|resourceRate|decimal|單價的 hello 計量表|
|extendedCost|decimal|根據已耗用數量和延伸成本的預估費用|
<br/>
## <a name="see-also"></a>另請參閱

* [計費週期 API](billing-enterprise-api-billing-periods.md)

* [使用量詳細資料 API](billing-enterprise-api-usage-detail.md) 

* [餘額與摘要 API](billing-enterprise-api-balance-summary.md)

* [價位表 API](billing-enterprise-api-pricesheet.md)