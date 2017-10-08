---
title: "Azure 邏輯應用程式的 aaaWebhook 連接器 |Microsoft 文件"
description: "Toouse webhook 動作和觸發程序 tooperform 動作要如何篩選陣列從邏輯應用程式"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>開始使用 hello webhook 連接器

Hello webhook 動作以及觸發程序，您可以啟動、 暫停和繼續流程 tooperform 這些工作：

* 收到項目時，即從 [Azure 事件中樞](https://github.com/logicappsio/EventHubAPI) 觸發
* 等待核准再繼續工作流程

深入了解[如何 toocreate 自訂應用程式開發介面支援 webhook](../logic-apps/logic-apps-create-api-app.md)。

## <a name="use-hello-webhook-trigger"></a>使用 hello webhook 觸發程序

[觸發程序](connectors-overview.md)是啟動邏輯應用程式工作流程的事件。 webhook 觸發程序是以事件為基礎，而不是依賴對新項目進行輪詢。 像 hello[要求觸發程序](connectors-native-reqres.md)，hello 邏輯應用程式引發 hello 即時事件發生時。 hello webhook 觸發程序註冊*回呼 URL* tooa 服務，並使用該 URL toofire hello 邏輯應用程式做為所需。

以下是示範向上 HTTP tooset 觸發程序在 hello 邏輯應用程式的設計工具中的範例。 hello 步驟假設您已部署或正在存取的 API，遵循 hello [webhook 訂閱及取消訂閱中的 logic apps 模式](../logic-apps/logic-apps-create-api-app.md#webhook-triggers)。 hello 訂閱呼叫每當邏輯應用程式不會儲存具有新的 webhook，或從已停用 tooenabled 切換時建立。 hello 取消訂閱呼叫移除並儲存，或從已啟用 toodisabled 切換邏輯應用程式 webhook 觸發程序時進行。

**tooadd hello webhook 觸發程序**

1. 新增 hello **HTTP Webhook** hello 邏輯應用程式中的第一個步驟的觸發程序。
2. 填寫 hello 參數，如 hello webhook 訂閱及取消訂閱的呼叫。

   此步驟會遵循相同模式為 hello hello [HTTP 動作](connectors-native-http.md)格式。

     ![HTTP 觸發程序](./media/connectors-native-webhook/using-trigger.png)

3. 加入至少一個動作。
4. 按一下**儲存**toopublish hello 邏輯應用程式。 此步驟中呼叫 hello 訂閱 hello 回呼所需的 URL tootrigger 端點此邏輯應用程式。
5. 每當 hello 服務會`HTTP POST`toohello 回呼 URL，hello 邏輯應用程式引發，並包含傳入 hello 要求任何資料。

## <a name="use-hello-webhook-action"></a>使用 hello webhook 動作

[*動作*](connectors-overview.md)作業由執行邏輯應用程式中定義的 hello 工作流程。 Webhook 動作會註冊*回呼 URL*與服務等候直到 hello URL 會繼續進行之前呼叫。 hello [」 傳送核准電子郵件 」](connectors-create-api-office365-outlook.md)是連接器遵循此模式的範例。 您可以在任何服務 hello webhook 動作透過擴充此模式。 

以下是示範如何設定中的 webhook 動作 tooset hello 邏輯應用程式的設計工具的範例。 這些步驟假設您已部署或正在存取的 API，遵循 hello [webhook 訂閱及取消訂閱邏輯應用程式中使用的模式](../logic-apps/logic-apps-create-api-app.md#webhook-actions)。 hello 訂閱呼叫邏輯應用程式執行 hello webhook 動作時進行。 hello 取消訂閱呼叫時執行取消等待回應，或應用程式逾時之前 hello 邏輯。

**tooadd webhook 動作**

1. 選擇 [新增步驟] > [新增動作]。

2. 在 [hello] 搜尋方塊中，輸入 「 webhook"toofind hello **HTTP Webhook**動作。

    ![選取查詢動作](./media/connectors-native-webhook/using-action-1.png)

3. 填滿 hello 參數中的 hello webhook 訂閱及取消訂閱呼叫

   此步驟會遵循相同模式為 hello hello [HTTP 動作](connectors-native-http.md)格式。

     ![完整查詢動作](./media/connectors-native-webhook/using-action-2.png)
   
   在執行階段，hello 邏輯應用程式呼叫 hello 訂閱到達該步驟之後的端點。

4. 按一下**儲存**toopublish hello 邏輯應用程式。

## <a name="technical-details"></a>技術詳細資訊

以下是詳細資料的 webhook 支援 hello 觸發程序及動作相關。

## <a name="webhook-triggers"></a>WebHook 觸發程序

| 動作 | 說明 |
| --- | --- |
| HTTP Webhook |訂閱可以呼叫 hello URL toofire 邏輯應用程式所需的回呼 URL tooa 服務。 |

### <a name="trigger-details"></a>觸發程序詳細資料

#### <a name="http-webhook"></a>HTTP Webhook

訂閱可以呼叫 hello URL toofire 邏輯應用程式所需的回呼 URL tooa 服務。
代表必要欄位 * 。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 訂閱方法* |method |訂閱要求的 HTTP 方法 toouse |
| 訂閱 URI* |uri |訂閱要求的 HTTP URI toouse |
| 取消訂閱方法* |method |取消訂閱要求的 HTTP 方法 toouse |
| 取消訂閱 URI* |uri |取消訂閱要求的 HTTP URI toouse |
| 訂閱本文 |body |訂閱的 HTTP 要求本文 |
| 訂閱標頭 |headers |訂閱的 HTTP 要求標頭 |
| 訂閱驗證 |驗證 |HTTP 驗證 toouse 的訂閱。 如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication) |
| 取消訂閱頁面 |body |取消訂閱的 HTTP 要求本文 |
| 取消訂閱標頭 |headers |取消訂閱的 HTTP 要求標頭 |
| 取消訂閱驗證 |驗證 |HTTP 驗證 toouse 用於取消訂閱。 如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication) |

**輸出詳細資料**

Webhook 要求

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| headers |物件 |Webhook 要求標頭 |
| body |物件 |Webhook 要求物件 |
| 狀態碼 |int |Webhook 要求狀態碼 |

## <a name="webhook-actions"></a>Webhook 動作

| 動作 | 說明 |
| --- | --- |
| HTTP Webhook |訂閱回呼 URL tooa 服務可以呼叫 hello URL tooresume 視工作流程步驟。 |

### <a name="action-details"></a>動作詳細資料

#### <a name="http-webhook"></a>HTTP Webhook

訂閱回呼 URL tooa 服務可以呼叫 hello URL tooresume 視工作流程步驟。
代表必要欄位 * 。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 訂閱方法* |method |訂閱要求的 HTTP 方法 toouse |
| 訂閱 URI* |uri |訂閱要求的 HTTP URI toouse |
| 取消訂閱方法* |method |取消訂閱要求的 HTTP 方法 toouse |
| 取消訂閱 URI* |uri |取消訂閱要求的 HTTP URI toouse |
| 訂閱本文 |body |訂閱的 HTTP 要求本文 |
| 訂閱標頭 |headers |訂閱的 HTTP 要求標頭 |
| 訂閱驗證 |驗證 |HTTP 驗證 toouse 的訂閱。 如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication) |
| 取消訂閱頁面 |body |取消訂閱的 HTTP 要求本文 |
| 取消訂閱標頭 |headers |取消訂閱的 HTTP 要求標頭 |
| 取消訂閱驗證 |驗證 |HTTP 驗證 toouse 用於取消訂閱。 如需詳細資訊，[請參閱 HTTP 連接器](connectors-native-http.md#authentication) |

**輸出詳細資料**

Webhook 要求

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| headers |物件 |Webhook 要求標頭 |
| body |物件 |Webhook 要求物件 |
| 狀態碼 |int |Webhook 要求狀態碼 |

## <a name="next-steps"></a>後續步驟

* [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)
* [尋找其他連接器](apis-list.md)