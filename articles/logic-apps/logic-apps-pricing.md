---
title: "aaaPricing & 計費-Azure 邏輯應用程式 |Microsoft 文件"
description: "了解 Azure Logic Apps 的定價和計費方式。"
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Logic Apps 的定價模式
Azure 邏輯應用程式可讓您 tooscale 和 hello 雲端中執行的工作流程整合。  以下是 hello 計費和 Logic apps 定價方案的詳細資訊。
## <a name="consumption-pricing"></a>取用定價
新建立的 Logic Apps 會使用取用方案。 使用 hello Logic Apps 耗用量定價模型時，您只需支付您所使用。  使用取用方案時，Logic Apps 不會執行節流。
在執行邏輯應用程式執行個體時所執行的所有動作都會計量。
### <a name="what-are-action-executions"></a>什麼是動作執行？
邏輯應用程式定義中的每一個步驟是動作，包括觸發程序，控制流程步驟 like 條件，範圍，每個迴圈中，執行迴圈，直到呼叫 tooconnectors 和呼叫 toonative 動作。
觸發程序是特殊的動作，就會發生特定事件時，會設計的 tooinstantiate 邏輯應用程式的新執行個體。  有數個不同的行為，觸發程序，但是可能會影響 hello 邏輯應用程式計量付費的方式。
* **輪詢觸發程序**– 此觸發程序持續輪詢端點，直到其接收到滿足 hello 準則建立邏輯應用程式的執行個體的訊息。  hello 邏輯應用程式的設計工具中的 hello 觸發程序中，您可以設定 hello 輪詢間隔。  即使是未建立邏輯應用程式執行個體的輪詢要求也會計算為一個動作執行。
* **Webhook 觸發程序**– 此觸發程序會等到用戶端 toosend 它在特定端點上的要求。  每個要求傳送 toohello webhook 端點會算為動作執行。 hello 要求和 hello HTTP Webhook 觸發程序是這兩個 webhook 觸發程序。
* **循環觸發程序**– 此觸發程序建立 hello 邏輯應用程式設定 hello 觸發程序中的 hello 循環間隔時間為基礎的執行個體。  例如，循環觸發程序可設定的 toorun 每三天或甚至是每一分鐘。

Hello 觸發程序的記錄組件中的 hello 邏輯應用程式資源刀鋒視窗中，就可以看到觸發程序執行。

所有已執行的動作不論成功或失敗，都為計量為動作執行。  已略過到期 tooa 條件不符合的動作或未執行，因為 hello 邏輯應用程式終止之前完成的動作不會視為動作執行。

在迴圈內執行的動作會計算每個 hello 迴圈的反覆項目。  例如，在單一動作 for each 迴圈逐一查看 10 個項目清單會視為 hello 乘以 hello hello 迴圈 (1) 中的動作數目的 hello 清單 (10) 中的項目數目再加 1 hello 迴圈的 hello 起始的其中，在此範例中，將為 (10 * 1) + 1 = 11 動作執行。
已停用的 Logic Apps 不能具現化新的執行個體，因此在停用時不會收費。  留意，停用邏輯應用程式之後可能需要一段時間的 hello 執行個體 tooquiesce 之前完全停用。
### <a name="integration-account-usage"></a>整合帳戶用量
包含在耗用量為基礎的使用方式是[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)的瀏覽、 開發和測試之用，可讓您 toouse hello [B2B/EDI](logic-apps-enterprise-integration-b2b.md)和[XML 處理](logic-apps-enterprise-integration-xml.md)邏輯應用程式功能不需要額外成本。 您為無法 toocreate 一個帳戶，每個區域的最大值，然後存放 too10 協議與 25 的對應。 結構描述、憑證和協力廠商沒有限制，您可以視需要上載。

此外 toohello 包含整合帳戶耗用量，您也可以建立標準整合帳戶沒有這些限制與我們的標準邏輯應用程式 SLA。 如需詳細資訊，請參閱 [Azure 價格](https://azure.microsoft.com/pricing/details/logic-apps)。

## <a name="app-service-plans"></a>App Service 方案
邏輯應用程式先前所建立 App Service 方案的參考會繼續執行之前為 toobehave。 根據選擇的 hello 方案，被節流之後 hello 規定每日執行超過但 hello 動作執行計量表收費。
App Service 方案中的其訂用帳戶，並沒有明確 hello 邏輯應用程式相關聯的 toobe EA 客戶取得 hello 包含數量帶來效益。  比方說，如果您在標準的 App Service 方案 EA 訂用帳戶和邏輯應用程式中的 hello 相同訂用帳戶，則不支付 10000 的動作執行每日 （請參閱下表）。 

App Service 方案和其每日允許的動作執行次數︰
|  | 免費/共用/基本 | 標準 | 高級 |
| --- | --- | --- | --- |
| 每日的動作執行次數 |200 |10,000 |50,000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>從 App Service 方案定價 tooConsumption 轉換
邏輯應用程式的應用程式服務計劃與其相關聯 toochange tooa 取用模型移除 hello 參考 toohello App Service 方案中 hello 邏輯應用程式定義。  這項變更可以透過呼叫 tooa PowerShell cmdlet:`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>價格
如需定價詳細資料，請參閱 [Logic Apps 定價](https://azure.microsoft.com/pricing/details/logic-apps)。

## <a name="next-steps"></a>後續步驟
* [Logic Apps 概觀][whatis]
* [建立第一個邏輯應用程式][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

