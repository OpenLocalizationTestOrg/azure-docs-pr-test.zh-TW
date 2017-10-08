---
title: "aaaAzure 計費企業應用程式開發介面 |Microsoft 文件"
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>適用於企業客戶的報告 API 概觀
hello 報告 Api 可讓企業 Azure 客戶 tooprogrammatically 提取耗用量和計費資料到慣用的資料分析工具。 

## <a name="enabling-data-access-toohello-api"></a>啟用資料存取 toohello API
* **產生或擷取 hello API 金鑰**-toohello 企業入口網站，然後遵循 hello 教學課程中說明的記錄檔-Reporting Api。 在此說明文章的 hello 第一節說明 hello toogenerate 或擷取 hello API 金鑰指定註冊的方式。
* **傳入 hello API 金鑰**-hello API 金鑰需要 toobe 傳遞每個呼叫進行驗證和授權。 hello 下列屬性需要 toobe toohello HTTP 標頭

|要求標頭金鑰 | 值|
|-|-|
|Authorization| 以此格式指定 hello 值： **bearer {API_KEY}** <br/> 範例：bearer eyr....09|

## <a name="consumption-apis"></a>使用情況 API
有可用 Swagger 端點[這裡](https://consumption.azure.com/swagger/ui/index)hello Api 低於此應該啟用簡單自我 hello API 和 hello 能力 toogenerate 用戶端 Sdk 的使用說明[AutoRest](https://github.com/Azure/AutoRest)或[Swagger CodeGen](http://swagger.io/swagger-codegen/)。 自 2014 年 5 月 1 日起的資料可透過此 API 取得。 

* **平衡和摘要**-hello[平衡和摘要的應用程式開發介面](billing-enterprise-api-balance-summary.md)提供每月餘額、 購買、 Azure Marketplace 服務的費用、 調整及 overage 費用的詳細資訊的摘要。

* **使用方式詳細資料**-hello[使用量詳細資料 API](billing-enterprise-api-usage-detail.md)提供已使用的數量和所註冊的估計的費用的每日明細。 hello 結果也會包含有關執行個體、 公尺和部門。 您可以查詢 hello API，計費週期或指定的開始和結束日期。 

* **Marketplace 商店電量**-hello [Marketplace 商店電量 API](billing-enterprise-api-marketplace-storecharge.md)傳回依日排列的 hello 基於使用方式的 marketplace 費用明細 hello 指定計費期間或開始和結束日期 （一次費用不包含）.

* **價位表**-hello[價位表 API](billing-enterprise-api-pricesheet.md)提供每個計量器 hello 註冊和帳單週期 hello 適用的速率。 

## <a name="helper-apis"></a>協助程式 API
 **列出計費週期**-hello[計費週期 API](billing-enterprise-api-billing-periods.md)會傳回一份計費週期 hello 依反向時間順序指定註冊都耗用量資料。 每個週期包含指向 hello 四組資料-BalanceSummary、 UsageDetails、 Marketplace 費用及價位表的 toohello API 路由的屬性。


## <a name="api-response-codes"></a>API 回應碼  
|回應狀態碼|訊息|描述|
|-|-|-|
|200| OK|沒有錯誤|
|401| 未經授權| API 金鑰找不到、無效或過期等。|
|404| 無法使用| 找不到報告端點|
|400| 不正確的要求| 無效的參數 - 資料範圍、EA 編號等。|
|500| 伺服器錯誤| 處理要求時發生未預期的錯誤| 









