---
title: "aaaCall，觸發程序，或巢狀工作流程搭配 HTTP 端點的 Azure 邏輯應用程式 |Microsoft 文件"
description: "Azure 邏輯應用程式設定 HTTP 端點 toocall、 觸發程序或巢狀工作流程"
services: logic-apps
keywords: "工作流程, HTTP 端點"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>在邏輯應用程式中透過 HTTP 端點呼叫、觸發或巢狀處理工作流程

您可以在邏輯應用程式中利用原生方式公開同步的 HTTP 端點作為觸發程序，以透過 URL 來觸發或呼叫邏輯應用程式。 您也可以使用可呼叫端點的模式，以在邏輯應用程式中巢狀處理工作流程。

toocreate HTTP 端點，您可以新增這些觸發程序，讓您的 logic apps 可以接收連入要求：

* [要求](../connectors/connectors-native-reqres.md)

* [API 連線 Webhook](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [HTTP Webhook](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > 雖然我們的範例使用 hello**要求**觸發程序，您可以使用任何的 hello 列出 HTTP 觸發程序，而且所有適用的原則即會相同 toohello 其他觸發程序類型。

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>設定邏輯應用程式的 HTTP 端點

toocreate HTTP 端點，新增觸發程序可以接收傳入要求。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。 連線 tooyour 邏輯應用程式，並開啟邏輯應用程式的設計工具。

2. 新增可讓邏輯應用程式接收傳入要求的觸發程序。 例如，新增 hello**要求**觸發程序 tooyour 邏輯應用程式。

3.  在下**要求本文 JSON 結構描述**，您可以選擇輸入如您預期 hello 觸發程序 tooreceive hello 裝載 （資料） 的 JSON 結構描述。

    hello 設計工具會使用此結構描述來產生 tooconsume、 parse 和傳遞資料，從 hello 觸發程序，透過您的工作流程，可以使用邏輯應用程式的權杖。 
    深入了解[從 JSON 結構描述產生的權杖](#generated-tokens)。

    此範例中，輸入 hello hello 設計工具中顯示的結構描述：

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![加入 hello 要求動作][1]

    > [!TIP]
    > 
    > 您可以從這類工具產生的結構描述的範例 JSON 承載， [jsonschema.net](http://jsonschema.net/)，或在 hello**要求**觸發程序藉由選擇**使用範例內容 toogenerate 結構描述**。 
    > 輸入您的範例承載，然後選擇 [完成]。

    例如，此範例裝載︰

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    產生此結構描述︰

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  儲存您的邏輯應用程式。 在下**HTTP POST toothis URL**，您現在應該會發現產生的回呼 URL，如下列範例：

    ![為端點產生的回呼 URL](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    此 URL 包含用於驗證的 hello 查詢參數中的共用存取簽章 (SAS) 金鑰。 
    您也可以從您的邏輯應用程式概觀 hello Azure 入口網站中取得 hello HTTP 端點 URL。 在 [觸發程序記錄] 下方，選取觸發程序：

    ![從 Azure 入口網站取得 HTTP 端點 URL][2]

    或者，您可以取得 hello URL 進行此呼叫：

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>變更觸發程序的 hello HTTP 方法

根據預設，hello**要求**觸發程序需要 HTTP POST 要求，但是您可以使用不同的 HTTP 方法。 

> [!NOTE]
> 您只能指定一種方法類型。

1. 在 [要求] 觸發程序上，選擇 [顯示進階選項]。

2. 開啟 hello**方法**清單。 在此範例中，選取 **GET**，稍後測試 HTTP 端點的 URL。

    > [!NOTE]
    > 您可以選取任何其他 HTTP 方法，或指定專屬邏輯應用程式的自訂方法。

    ![變更 HTTP 方法](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>透過 HTTP 端點 URL 接受參數

當您想 HTTP 端點 URL tooaccept 參數時，自訂觸發程序的相對路徑。

1. 在 [要求] 觸發程序上，選擇 [顯示進階選項]。 

2. 在下**方法**，指定您想要求 toouse hello HTTP 方法。 此範例中，選取 hello**取得**方法，如果您還沒有這麼做，以便您可以測試 HTTP 端點的 URL。

      > [!NOTE]
      > 當您指定觸發程序的相對路徑時，也必須明確地指定觸發程序的 HTTP 方法。

3. 在下**相對路徑**，指定您的 URL 應該接受的比方說，hello 參數的 hello 相對路徑`customers/{customerID}`。

    ![指定 hello HTTP 方法和參數的相對路徑](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse hello 參數，新增**回應**動作 tooyour 邏輯應用程式。 (在觸發程序下方，選擇 [新增步驟] > [新增動作] > [回應])。 

5. 在您的回應**主體**，包括您在觸發程序的相對路徑中指定的 hello 參數 hello token。

    例如，tooreturn `Hello {customerID}`，更新您的回應**主體**與`Hello {customerID token}`。 
    hello 動態內容的清單應該會出現並顯示 hello`customerID`權杖以供您 tooselect。

    ![加入參數 tooresponse 主體](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    您的 [本文] 應該如下列範例所示：

    ![含參數的回應本文](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. 儲存您的邏輯應用程式。 

    您的 HTTP 端點 URL 現在例如包含 hello 相對路徑： 

    https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. 您的 HTTP 端點、 複製和貼上至另一個瀏覽器視窗，hello 更新的 URL，但取代的 tootest`{customerID}`與`123456`，然後按 Enter。

    您的瀏覽器應該顯示下列文字︰ 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>從 JSON 結構描述產生邏輯應用程式的權杖

當您提供的 JSON 結構描述中您**要求**觸發程序、 hello 邏輯應用程式的設計工具會產生語彙基元屬性的該結構描述中。 您接著可以使用這些權杖，透過邏輯應用程式工作流程來傳遞資料。

例如，如果您新增 hello`title`和`name`屬性 tooyour JSON 結構描述，及其語彙基元現在會於稍後步驟中工作流程的可用 toouse。 

以下是 hello 完整的 JSON 結構描述：

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>建立邏輯應用程式的巢狀工作流程

您可以新增其他可接收要求的邏輯應用程式，以在邏輯應用程式中巢狀處理工作流程。 tooinclude 這些邏輯應用程式中，新增 hello **Azure 邏輯應用程式-選擇 Logic Apps 工作流程**動作 tooyour 觸發程序。 您接著可以從合格的邏輯應用程式中進行選取。

![新增另一個邏輯應用程式](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>透過 HTTP 端點呼叫或觸發邏輯應用程式

建立 HTTP 端點之後，您可以觸發透過應用程式邏輯`POST`方法 toohello 完整的 URL。 邏輯應用程式具有直接存取端點的內建支援。

## <a name="reference-content-from-an-incoming-request"></a>參考來自傳入要求的內容

如果 hello 內容型別，則為`application/json`，您可以從 hello 連入要求參考屬性。 否則，內容會被視為單一的二進位單位，您可以將 tooother 應用程式開發介面。 tooreference hello 工作流程內部此內容，您必須轉換該內容。 例如，如果您傳遞`application/xml`內容，您可以使用  `@xpath()` XPath 擷取，或`@json()`轉換 XML tooJSON。 深入了解如何[使用內容類型](../logic-apps/logic-apps-content-type.md)。

tooget hello 輸出從傳入要求，您可以使用 hello`@triggerOutputs()`函式。 hello 輸出看起來就像此範例中：

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

tooaccess hello`body`屬性明確地說，您可以使用 hello`@triggerBody()`捷徑。 

## <a name="respond-toorequests"></a>回應 toorequests

您可以藉由傳回內容 toohello 呼叫端啟動邏輯應用程式的 toorespond toocertain 要求。 tooconstruct hello 狀態碼、 標頭和您的回應主體中，您可以使用 hello**回應**動作。 這個動作可以出現在邏輯應用程式，不只是在您的工作流程的 hello 結尾的任何位置。

> [!NOTE] 
> 如果應用程式邏輯不包含**回應**，回應 hello HTTP 端點*立即*與**202 已接受**狀態。 此外，如 hello 原始要求 tooget hello 回應 hello 回應所需的所有步驟必須內都完成 hello[要求逾時限制](./logic-apps-limits-and-config.md)除非呼叫 hello 做為巢狀的邏輯應用程式的工作流程。 如果沒有回應的情況發生這項限制內，hello 連入要求會逾時並收到 hello HTTP 回應**408 用戶端逾時**。 巢狀的 logic apps hello 父邏輯應用程式會繼續 toowait 完成為止，不論則需要多少時間的回應。

### <a name="construct-hello-response"></a>建構 hello 回應

您可以在 hello 回應主體中包含一個以上的標頭和任何類型的內容。 在我們的範例回應 hello 標頭指定 hello 回應的內容類型`application/json`。 和 hello 主體會包含`title`和`name`根據 hello hello 先前已更新的 JSON 結構描述，**要求**觸發程序。

![HTTP 回應動作][3]

回應具有下列屬性：

| 屬性 | 說明 |
| --- | --- |
| StatusCode |指定回應 toohello 連入要求的 hello HTTP 狀態碼。 此代碼可以是任何以 2xx、4xx 或 5xx 開頭的有效狀態碼。 但是，不允許 3xx 狀態碼。 |
| headers |定義任意數目的標頭 tooinclude hello 回應中。 |
| body |指定本文物件可以是字串、JSON 物件，甚至是上一個步驟中所參考的二進位內容。 |

以下是何種 hello JSON 結構描述，看起來像現在 hello**回應**動作：

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> tooview hello JSON 個完整定義邏輯上的應用程式，hello 邏輯應用程式的設計工具，選擇**程式碼檢視**。

## <a name="q--a"></a>問答集

#### <a name="q-what-about-url-security"></a>問︰URL 安全性如何？

答：Azure 會使用共用存取簽章 (SAS)，安全地產生邏輯應用程式回呼 URL。 這個簽章是以查詢參數的形式傳遞，且必須在引發您的邏輯應用程式之前先驗證。 Azure 會產生 hello 簽章使用的每個邏輯應用程式、 hello 觸發程序名稱和執行的 hello 作業的祕密金鑰的唯一組合。 因此除非有人存取 toohello 秘密邏輯應用程式金鑰，否則他們無法產生有效的簽章。

   > [!IMPORTANT]
   > 生產環境與安全的系統，我們強烈建議針對直接從 hello 瀏覽器呼叫應用程式邏輯，因為：
   > 
   > * hello 共用的存取金鑰會出現在 hello URL。
   > * 您無法管理安全內容的原則，因為 tooshared 網域整個邏輯應用程式的客戶。

#### <a name="q-can-i-configure-http-endpoints-further"></a>問︰我可以進一步設定 HTTP 端點嗎？

答︰可以，HTTP 端點透過 [**API 管理**](../api-management/api-management-key-concepts.md)來支援更進階的設定。 此服務也提供 hello 功能，針對您 tooconsistently 管理您的所有 Api，包括邏輯應用程式、 設定自訂網域名稱、 使用多個驗證方法及詳細資訊，例如：

* [變更 hello 要求方法](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [變更 hello 的 hello 要求的 URL 區段](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* 設定您的 API 管理網域中 hello [Azure 入口網站](https://portal.azure.com/ "Azure 入口網站")
* 設定基本驗證的原則 toocheck

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>問： 什麼變更時從 hello 2014 年 12 月 1 日預覽移轉 hello 結構描述？

答︰以下是這些變更的摘要︰

| 2014 年 12 月 1 日預覽版 | 2016 年 6 月 1 日 |
| --- | --- |
| 按一下 [HTTP 接聽程式] API 應用程式 |按一下 [手動觸發程序] \(不需要 API 應用程式) |
| HTTP 接聽程式設定 [自動傳送回應] |可能包含**回應**動作或不在 hello 工作流程定義 |
| 設定基本或 OAuth 驗證 |透過 API 管理 |
| 設定 HTTP 方法 |在 [顯示進階選項] 下方，選擇 HTTP 方法。 |
| 設定相對路徑 |在 [顯示進階選項] 下方，新增相對路徑。 |
| 透過參考 hello 傳入內容`@triggerOutputs().body.Content` |透過 `@triggerOutputs().body` 參考 |
| **傳送 HTTP 回應**hello HTTP 接聽程式時採取的動作 |按一下**回應 tooHTTP 要求**（沒有 API 應用程式所需） |

## <a name="get-help"></a>取得說明

tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。

## <a name="next-steps"></a>後續步驟

* [撰寫邏輯應用程式定義](./logic-apps-author-definitions.md)
* [處理錯誤和例外狀況](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
