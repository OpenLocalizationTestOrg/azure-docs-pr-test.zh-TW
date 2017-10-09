---
title: "aaaError （& s) 例外狀況處理-Azure 邏輯應用程式 |Microsoft 文件"
description: "Azure Logic Apps 中的錯誤和例外狀況處理模式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>處理 Azure Logic Apps 中的錯誤和例外狀況

Azure 邏輯應用程式提供豐富的工具和模式 toohelp 您確定您的整合是強固且彈性地防止失敗。 任何整合架構其中 hello 挑戰，可確保確定 tooappropriately 控制代碼的停機時間，或從相依系統問題。 邏輯應用程式會處理錯誤的第一級的體驗，讓您 hello 需 tooact 上例外狀況和錯誤在工作流程中的工具。

## <a name="retry-policies"></a>重試原則

重試原則是 hello 最基本的例外狀況和錯誤處理的類型。 如果初始的要求已逾時或失敗 (429 會導致任何要求或 5xx 回應)，此原則會定義 hello 動作是否應該重試。 根據預設，所有動作會在 20 秒的間隔內另外再試 4 次。 因此，如果收到 hello 第一個要求`500 Internal Server Error`20 秒的回應，hello 工作流程引擎暫停，並嘗試再次 hello 要求。 如果所有重試之後, hello 回應仍是例外狀況或失敗，hello 工作流程會繼續和標記 hello 做為動作狀態`Failed`。

您可以設定的重試原則在 hello**輸入**特定動作。 例如，您可以設定重試原則 tootry 4 次最多 1 小時間隔。 如需輸入屬性的完整詳細資料，請參閱[工作流程動作與觸發程序][retryPolicyMSDN]。

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

如果您想要您 HTTP 動作 tooretry 4 次，並等候 10 分鐘後，每個嘗試之間，您可以使用下列定義 hello:

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

如需有關支援語法的詳細資訊，請參閱 hello[重試原則工作流程動作和觸發程序 」 一節][retryPolicyMSDN]。

## <a name="catch-failures-with-hello-runafter-property"></a>攔截 hello RunAfter 屬性的失敗

邏輯應用程式的每個動作宣告 hello 動作啟動，例如工作流程中排序 hello 步驟前必須完成的動作。 在 hello 動作定義中，這種排序稱為 hello`runAfter`屬性。 這個屬性是物件，描述哪些動作和動作狀態執行 hello 動作。 根據預設，所有的動作，透過 hello 邏輯應用程式的設計工具加入設定太`runAfter`如果 hello hello 上一個步驟前一個步驟`Succeeded`。 不過，您可以自訂此值 toofire 動作當上一個動作都有`Failed`， `Skipped`，或一組可能的這些值。 如果您想 tooadd 項目 tooa 指定 Service Bus 主題的特定動作之後`Insert_Row`失敗，您可以使用下列的 hello`runAfter`組態：

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

請注意 hello`runAfter`屬性如果 hello 設定 toofire`Insert_Row`動作`Failed`。 如果 hello 動作狀態是 toorun hello 動作`Succeeded`， `Failed`，或`Skipped`，使用下列語法：

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> 前一個動作失敗之後所執行並順利完成的動作會標示為 `Succeeded`。 這意味著如果您已成功在工作流程時，攔截所有失敗 hello 執行本身標示為`Succeeded`。

## <a name="scopes-and-results-tooevaluate-actions"></a>範圍和結果 tooevaluate 動作

您可以在個別的動作之後執行的 toohow 類似，您可以也動作組成群組內[範圍](../logic-apps/logic-apps-loops-and-scopes.md)，其做為動作的邏輯群組。 領域都是適合用來組織您的邏輯應用程式的動作，以及用於在領域的 hello 狀態上執行彙總的評估。 在範圍中的所有動作都完成後，請 hello 範圍本身會接收狀態。 hello 領域狀態決定以 hello 做為測試回合的相同準則。 如果執行分支中的 hello 最後一個動作是`Failed`或`Aborted`，hello 狀態是`Failed`。

toofire hello 範圍內發生任何失敗的特定動作，您可以使用`runAfter`範圍標示為`Failed`。 如果*任何*hello 範圍中的動作失敗、 執行之後的範圍可讓您建立單一動作 toocatch 失敗。

### <a name="getting-hello-context-of-failures-with-results"></a>取得 hello 內容失敗，將結果

雖然攔截失敗從範圍非常有用，您可能也想內容 toohelp 您了解確切的動作失敗，任何錯誤或已傳回狀態碼。 hello`@result()`工作流程函式提供有關 hello 結果的範圍中的所有動作內容。

`@result()`接受單一參數，領域名稱，並傳回所有 hello 動作會從該範圍內的陣列。 這些動作物件包含相同屬性，hello hello`@actions()`輸出物件，包括動作的開始時間、 動作的結束時間、 動作狀態、 輸入動作、 動作相互關聯識別碼和動作。 toosend 內容中無法在範圍內的任何動作，您可以輕易地配對`@result()`函式與`runAfter`。

tooexecute 動作*每個*範圍中的動作，`Failed`結果 tooactions 篩選 hello 陣列失敗，您所能配對`@result()`與**[篩選陣列](../connectors/connectors-native-query.md)**動作和 **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** 迴圈。 您可以使用 hello 篩選的結果的陣列，並使用 hello 每個失敗執行的動作**ForEach**迴圈。 以下是範例，後面接著 hello 範圍內傳送 HTTP POST 要求與 hello 回應主體失敗的任何動作的詳細說明`My_Scope`。

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

以下是會發生什麼情況的詳細逐步解說 toodescribe:

1. tooget hello 結果內的所有動作`My_Scope`，hello**篩選陣列**動作篩選條件`@result('My_Scope')`。

2. hello 條件**篩選陣列**可以是任何`@result()`也有狀態相等的項目`Failed`。 這種狀況篩選 hello 陣列的所有動作結果`My_Scope`tooan 陣列只含失敗的動作結果。

3. 執行**每個**動作 hello**篩選陣列**輸出。 此步驟會對之前篩選的每個失敗動作結果執行動作。

    如果在 hello 範圍內的單一動作失敗、 hello hello 中的動作`foreach`只執行一次。 
    許多失敗動作會對每個失敗造成一個動作。

4. HTTP POST 傳送嗨`foreach`回應主體的項目或`@item()['outputs']['body']`。 hello`@result()`項目 圖形是 hello 相同為 hello`@actions()`圖形，並可以剖析 hello 相同的方式。

5. 包含兩個具有 hello 失敗的動作名稱的自訂標頭`@item()['name']`hello 失敗執行的用戶端追蹤 ID `@item()['clientTrackingId']`。

如需參考，以下是在單一範例`@result()`項目，顯示 hello `name`， `body`，和`clientTrackingId`剖析的 hello 前一個範例中的屬性。 在 `foreach` 之外，`@result()` 會傳回這些物件的陣列。

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

tooperform 不同的例外狀況處理模式，您可以使用先前顯示的 hello 運算式。 您可能會選擇 tooexecute 單一的例外狀況處理可接受 hello 整個篩選的陣列失敗次數、 hello 範圍外的動作，並移除 hello `foreach`。 您也可以包含其他有用的屬性，從 hello`@result()`先前所示的回應。

## <a name="azure-diagnostics-and-telemetry"></a>Azure 診斷和遙測

hello 先前模式很好的方法 toohandle 錯誤和例外狀況，在執行中，但您也可以識別並回應 tooerrors 執行本身的 hello 與無關。 
[Azure 診斷](../logic-apps/logic-apps-monitor-your-logic-apps.md)提供簡單的方式 toosend，所有的工作流程 （包括所有執行和動作的狀態） 的事件 tooan Azure 儲存體帳戶或 Azure 事件中心。 tooevaluate 執行狀態，您可以監視 hello 記錄檔和度量，或將它們發佈至任何您偏好的監視工具。 其中一個可能的選項是 toostream 所有 hello 事件至 Azure 事件中心透過[Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)。 在 Stream Analytics 中，您可以撰寫任何異常、 平均值或失敗關閉的即時查詢從 hello 診斷記錄檔。 串流分析可輕鬆地輸出 tooother 資料來源，例如佇列、 主題、 SQL、 Azure Cosmos DB、 和 Power BI。

## <a name="next-steps"></a>後續步驟

* [看看客戶如何使用 Azure Logic Apps 建置錯誤處理](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [尋找其他 Logic Apps 範例和案例](../logic-apps/logic-apps-examples-and-scenarios.md)
* [了解 toocreate 自動化部署邏輯應用程式的方式](../logic-apps/logic-apps-create-deploy-template.md)
* [使用 Visual Studio 建置和部署邏輯應用程式](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
