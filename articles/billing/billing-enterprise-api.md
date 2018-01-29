---
title: "Azure 計費企業版 API | Microsoft Docs"
description: "了解可讓企業 Azure 客戶以程式設計方式提取使用情況資料的報告 API。"
services: 
documentationcenter: 
author: anandedwin
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
ms.openlocfilehash: 62a69aeb7499a961f95739fb3836942b670c7320
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>適用於企業客戶的報告 API 概觀
報告 API 可讓企業 Azure 客戶以程式設計方式提取使用情況和帳單資料，以使用慣用的資料分析工具進行分析。 

## <a name="enabling-data-access-to-the-api"></a>啟用對 API 的資料存取
* **產生或擷取 API 金鑰** - 登入企業入口網站，並遵循 [說明] - [報告 API] 底下的教學課程。 此說明文章的第一節說明如何針對指定的註冊產生或擷取 API 金鑰。
* **在 API 中傳遞金鑰** - 必須針對每個驗證和授權呼叫傳遞 API 金鑰。 下列屬性必須是針對 HTTP 標頭

|要求標頭金鑰 | 值|
|-|-|
|Authorization| 以此格式指定值：**bearer {API_KEY}** <br/> 範例：bearer eyr....09|

## <a name="consumption-apis"></a>使用情況 API
下述 API 的 Swagger 端點可在[這裡](https://consumption.azure.com/swagger/ui/index)取得，它可讓使用者輕鬆進行 API 自我檢查，並且能使用 [AutoRest](https://github.com/Azure/AutoRest) 或 [Swagger CodeGen](http://swagger.io/swagger-codegen/) 產生用戶端 SDK。 自 2014 年 5 月 1 日起的資料可透過此 API 取得。 

* **餘額與摘要** - [餘額與摘要 API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-balance-summary) 可提供餘額、新購買、Azure Marketplace 服務費用、調整，以及超額部分費用的每月摘要資訊。

* **使用量詳細資料** - [使用量詳細資料 API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail) 可提供註冊之使用量和預估費用的每日明細。 結果也包含執行個體、計量和部門的資訊。 API 可依計費週期或指定開始和結束日期來查詢。 

* **Marketplace 市集費用** - [Marketplace 市集費用 API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-marketplace-storecharge) 可針對指定的計費週期或開始和結束日期，傳回以使用量為基礎的 Marketplace 費用每日明細 (不含一次性費用)。

* **價位表** - [價位表 API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-pricesheet) 可針對指定註冊和計費週期的每個計量提供適用的費率。 

## <a name="helper-apis"></a>協助程式 API
 **列出計費週期** - [計費週期 API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-billing-periods) 會傳回計費週期清單，其中包含所指定註冊的使用情況資料 (以反向時間順序排列)。 每個週期包含指向四組資料 (BalanceSummary、UsageDetails、Marketplace 費用和價位表) 之 API 路由的屬性。


## <a name="api-response-codes"></a>API 回應碼  
|回應狀態碼|訊息|描述|
|-|-|-|
|200| OK|沒有錯誤|
|401| 未經授權| API 金鑰找不到、無效或過期等。|
|404| 無法使用| 找不到報告端點|
|400| 不正確的要求| 無效的參數 - 資料範圍、EA 編號等。|
|500| 伺服器錯誤| 處理要求時發生未預期的錯誤| 









