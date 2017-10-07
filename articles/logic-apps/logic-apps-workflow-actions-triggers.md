---
title: "aaaWorkflow 動作和觸發程序-Azure 邏輯應用程式 |Microsoft 文件"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Azure Logic Apps 的工作流程動作和觸發程序

邏輯應用程式是由觸發程序和動作所組成。 觸發程序有六種類型。 每種類型各有不同的介面和行為。 您也可以了解其他詳細資料藉由查看 hello 詳細資料的 hello[工作流程定義語言](logic-apps-workflow-definition-language.md)。  
  
深入了解觸發程序和動作和您如何使用它們 toobuild 邏輯應用程式 tooimprove toolearn 上讀取，您的商務程序和工作流程。  
  
### <a name="triggers"></a>觸發程序  

觸發程序指定 hello 呼叫可以起始邏輯應用程式工作流程的執行。 以下是 hello 兩種不同方式 tooinitiate 執行的工作流程：  
  
-   輪詢觸發程序  

-   推入觸發程序的呼叫 hello[工作流程服務 REST API](https://docs.microsoft.com/rest/api/logic/workflows)  
  
所有觸發程序都包含下列最上層元素︰  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>觸發程序類型和其輸入  

您可以使用下列類型的觸發程序︰
  
-   **要求**\-您 toocall 的端點可讓 hello 邏輯應用程式  
  
-   **循環** \- 根據定義的排程來引發  
  
-   **HTTP** \- 輪詢 HTTP Web 端點。 hello HTTP 結束點必須符合 tooa 特定觸發合約\-使用 202\-非同步模式，或藉由傳回陣列  
  
-   **ApiConnection** \-像 hello HTTP 輪詢觸發，不過，它會利用 hello [Microsoft 管理 Api](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \-會開啟一個端點，類似 toohello 手動觸發程序，不過，它也會呼叫 tooa 出指定 URL tooregister 和取消註冊  
  
-   **ApiConnectionWebhook** \-運作一樣 hello HTTPWebhook 觸發程序，利用 hello Microsoft 管理 Api       
    每種觸發程序類型都會有一組不同的行為定義**輸入**。  
  
## <a name="request-trigger"></a>要求觸發程序  

這個觸發程序做為端點，透過 HTTP 要求 tooinvoke 呼叫應用程式邏輯。 要求觸發程序看起來就像下面這個範例︰  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

此外，還有一個稱為**結構描述**的選擇性屬性：  
  
|元素名稱|必要|說明|  
|----------------|------------|---------------|  
|結構描述|否|JSON 結構描述驗證 hello 連入要求。 很有用，可幫助知道哪些屬性 tooreference 後續的工作流程步驟。|

tooinvoke 此端點，您需要 toocall hello *listCallbackUrl*應用程式開發介面。 請參閱[工作流程服務 REST API](https://docs.microsoft.com/rest/api/logic/workflows)。  
  
## <a name="recurrence-trigger"></a>循環觸發程序  

循環觸發程序是會根據定義的排程來執行的觸發程序。 這類觸發程序看起來可能就像下面這個範例︰  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

如您所見，它是簡單的方式 toorun 工作流程。  
  
|元素名稱|必要|說明|  
|----------------|------------|---------------|  
|frequency|是|頻率 hello 執行觸發程序。 只能使用下列其中一個可能值︰秒、分鐘、小時、天、週、月或年|  
|interval|是|Hello 給 hello 循環頻率間隔|  
|startTime|否|如果提供 startTime 時未指定 UTC 時差，則會使用此 timeZone。|  
|timeZone|no|如果提供 startTime 時未指定 UTC 時差，則會使用此 timeZone。|  
  
您也可以排定觸發程序 toostart 執行在 hello 未來在某個時間點。 例如，如果您想要每週會報告每週的星期一 toostart 您可以排定 hello 邏輯應用程式 toostart 每星期一藉由建立 hello 下列觸發程序：  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>HTTP 觸發程序  

HTTP 觸發程序輪詢指定的端點，並檢查 hello 回應 toodetermine，是否應該要執行 hello 工作流程。 hello 輸入物件會使用參數需要 tooconstruct HTTP 呼叫 hello 組：  
  
|元素名稱|必要|說明|類型|  
|----------------|------------|---------------|--------|  
|method|yes|可以是其中一個 hello 遵循 HTTP 方法： GET、 POST、 PUT、 DELETE、 修補程式或標頭|String|  
|uri|yes|hello http 或 https 端點時所呼叫。 最大值為 2 KB。|String|  
|查詢|否|物件，代表 hello 查詢參數 tooadd toohello URL。 例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。|Object|  
|headers|否|物件，表示每個 toohello 要求會傳送 hello 標頭。 例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Object|  
|body|否|物件，表示傳送 toohello 端點的 hello 裝載。|Object|  
|RetryPolicy|否|物件，可讓您自訂 hello 重試行 4xx 或 5xx 錯誤。|Object|  
|驗證|否|代表 hello 要求的 hello 方法應該進行驗證。 如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)。 除了排程器外，還有一個支援的屬性︰`authority`。根據預設，在未指定時這個值會是 `https://login.windows.net`，但您可以使用不同的受眾，例如 `https://login.windows\-ppe.net`|Object|  
  
hello HTTP 觸發程序需要使用與邏輯應用程式特定的模式 toowork hello HTTP API tooconform。 它需要 hello 下列欄位：  
  
|Response|說明|  
|------------|---------------|  
|狀態碼|狀態碼 200\(確定\)toocause 執行。 其他任何狀態碼則不會導致執行。|  
|Retry\-after 標頭|Hello 邏輯應用程式會再次輪詢 hello 端點之前的秒數。|  
|位置標頭|hello URL toocall hello 下一次輪詢間隔。 如果未指定，會使用 hello 原始 URL。|  
  
以下是不同要求類型所具有之不同行為的一些範例︰  
  
|Response code|Retry\-After|行為|  
|-----------------|----------------|------------|  
|200|無\(\)|不是有效觸發，重試\-之後輪詢 hello 下一個要求永遠不會是必要項目，或其他 hello 引擎。|  
|202|60|不會觸發 hello 工作流程。 hello 下一次嘗試就會發生在一分鐘內。|  
|200|10|執行 hello 流程時，並在 10 秒後再次檢查詳細內容。|  
|400|無\(\)|不正確的要求，不會執行 hello 工作流程。 如果沒有任何**重試原則**定義，則會使用 hello 預設原則。 已達到重試的 hello 次數之後，hello 觸發程序都不再有效。|  
|500|無\(\)|伺服器錯誤時，不會執行 hello 工作流程。  如果沒有任何**重試原則**定義，則會使用 hello 預設原則。 已達到重試的 hello 次數之後，hello 觸發程序都不再有效。|  
  
hello HTTP 觸發程序的輸出類似下列範例：  
  
|元素名稱|說明|類型|  
|----------------|---------------|--------|  
|headers|hello http 回應的 hello 標頭。|Object|  
|body|hello hello http 回應主體。|Object|  
  
## <a name="api-connection-trigger"></a>API 連線觸發程序  

hello API 連線觸發程序是在其基本功能類似 toohello 的 HTTP 觸發程序。 不過，hello 參數識別 hello 動作是不同的。 下列是一個範例：  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|元素名稱|必要|類型|說明|  
|----------------|------------|--------|---------------|  
|主機|是||hello ApiApp 裝載閘道和識別碼。|  
|method|是|String|可以是其中一個 hello 遵循 HTTP 方法：**取得**， **POST**，**放**，**刪除**，**修補**，或**標頭**|  
|查詢|否|Object|代表 hello 查詢參數 toobe 加入 toohello URL。 例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。|  
|headers|否|Object|代表每個 toohello 要求會傳送 hello 標頭。 例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|否|Object|表示傳送 toohello 端點的 hello 裝載。|  
|RetryPolicy|否|Object|可讓您 toocustomize hello 重試行 4xx 或 5xx 錯誤。|  
|驗證|否|Object|代表 hello 要求的 hello 方法應該進行驗證。 如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
主機的 hello 屬性包括：  
  
|元素名稱|必要|說明|  
|----------------|------------|---------------|  
|api runtimeUrl|是|hello 端點 hello 的受管理應用程式開發介面。|  
|連線名稱||必須參考 tooa 參數呼叫`$connection`和 hello hello 工作流程使用的受管理的 hello API 連線名稱。|
  
hello API 連線觸發程序的輸出如下：
  
|元素名稱|類型|說明|  
|----------------|--------|---------------|  
|headers|Object|hello http 回應的 hello 標頭。|  
|body|Object|hello hello http 回應主體。|  
  
## <a name="httpwebhook-trigger"></a>HTTPWebhook 觸發程序  

hello HTTPWebhook 觸發程序會開啟端點，類似 toohello 手動觸發程序，但 hello HTTPWebhook 觸發程序也會呼叫 tooa 出指定 URL tooregister 及取消註冊。 HTTPWebhook 觸發程序看起來可能就像下面這個範例︰  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

許多這些區段是選擇性的並且 hello Webhook hello 行為取決於哪些區段會提供或省略。  
Webhook hello 屬性如下所示：  
  
|元素名稱|必要|說明|  
|----------------|------------|---------------|  
|訂閱|否|hello 傳出 hello 觸發程序會建立並執行 hello 初始註冊時所呼叫的要求。|  
|取消訂閱|否|hello 刪除 hello 觸發程序時，連出要求。|  
  
-   **訂閱**hello 連出 toostart 接聽 tooevents 所做的呼叫。 此呼叫會啟動以 hello 執行相同的 hello 標準 HTTP 動作的參數集合。 進行任何時間 hello 這個傳出呼叫工作流程以任何方式，例如，每當 hello 認證會復原變更，或 hello 觸發程序的輸入參數的變更。
  
    此呼叫 toosupport，有一個新的函式： `@listCallbackUrl()`。 這個函式會針對此工作流程中的這個特定觸發程序傳回唯一 URL。 它代表 hello 使用 hello REST 服務的 hello 端點的唯一識別碼。  
  
-   **取消訂閱**受到呼叫的時機是當作業將此觸發程序轉譯為無效時，包括︰  
  
    -   刪除或停用 hello 觸發程序  
  
    -   刪除或停用 hello 工作流程  
  
    -   刪除或停用 hello 訂用帳戶  
  
    hello 邏輯應用程式會自動呼叫 hello 取消動作。 hello 參數 toothis 函式會將相同 hello 為 hello HTTP 觸發程序。  
  
    hello hello HTTPWebhook 觸發程序的輸出是 hello hello 連入要求內容：  
  
|元素名稱|類型|說明|  
|-----------------|--------|---------------|  
|headers|Object|hello http 要求的 hello 標頭。|  
|body|Object|hello hello http 要求主體。|  

Webhook 動作的限制可以在 hello 中指定相同的方式[HTTP 非同步限制](#asynchronous-limits)。
  

## <a name="conditions"></a>條件  

任何觸發程序，您可以使用一或多個條件 toodetermine 是否 hello 工作流程應執行或未執行。 例如：  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

在此情況下，hello 報表時 hello 工作流程的唯一觸發程序`sendReports`參數設定 tootrue。 最後，條件可能會參考 hello hello 觸發程序的狀態碼。 例如，您只能在網站傳回狀態碼 500 時啟動工作流程，如下所示︰
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> 當任何運算式參考 hello hello 觸發程序的狀態碼\(以任何方式\)，hello 預設行為\(觸發程序只能在 200\(確定\)\)取代。 例如，如果您想 tootrigger 狀態碼 200 和狀態碼 「 201 上的，您有 tooinclude:`@or(equals(triggers().code, 200),equals(triggers().code,201))`做為您的條件。  
  
## <a name="start-multiple-runs-for-a-request"></a>為要求啟動多個執行

針對單一要求中，多個回合關閉 tookick`splitOn`非常有用，例如，當您想 toopoll 可以有多個新項目，輪詢間隔之間的端點。
  
與`splitOn`，指定 hello 屬性內包含的項目，其中每個您想要的 hello 陣列的 hello 回應裝載 toouse toostart hello 觸發程序執行。 例如，假設您有應用程式開發介面會傳回下列回應 hello:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
邏輯應用程式只需要 hello 資料列內容，因此您可以建構在觸發程序，如下列範例：  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
然後，在 hello 工作流程定義、`@triggerBody().name`傳回`mycoolrow`hello 第一次執行，並`another row`hello 第二個執行。 hello 觸發程序的輸出看起來像此範例中：  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

因此，如果您使用`SplitOn`，您無法取得 hello 內容以外的 hello 陣列在此情況下，hello`Status`欄位。  
  
> [!NOTE]  
> 在此範例中，我們使用 hello`?`運算子 toobe 無法 tooavoid 失敗如果 hello`Rows`屬性不存在。 
  
## <a name="single-run-instance"></a>單一執行的執行個體

您可以設定具有循環屬性 tooonly 火災，如果已完成所有作用中執行的觸發程序。 如果正在執行時，就會發生排程的循環，hello 觸發程序會略過，並等待，直到 hello 下一個排程的循環間隔 toocheck 一次。

您可以設定此設定，透過 hello 作業選項：

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>類型和輸入  

動作有許多類型，且各有各的獨特行為。 集合動作可在自身當中包含其他許多動作。

### <a name="standard-actions"></a>標準動作  

-   **HTTP** 這個動作會呼叫 HTTP Web 端點。  
  
-   **ApiConnection** \-此動作的行為方式與 hello HTTP 動作，但使用 hello Microsoft 管理的 Api。  
  
-   **ApiConnectionWebhook** \-像 HTTPWebhook，但使用 hello Microsoft 管理的 Api。  
  
-   **回應** \- 這個動作會定義連入呼叫的回應。  
  
-   **等候** \- 這個簡單的動作會等候固定時間量或直到某個特定時間。  
  
-   **工作流程** \- 這個動作代表巢狀工作流程。  

-   **函式** \- 這個動作代表 Azure Function。

### <a name="collection-actions"></a>集合動作

-   **範圍** \- 這個動作是其他動作的邏輯群組。

-   **條件**\-這個動作會評估運算式，並執行 hello 對應的結果分支。

-   **ForEach** \- 這個迴圈動作會逐一查看陣列並對每個項目執行內部動作。

-   **直到**\-此迴圈的動作會執行內部的動作，直到條件結果 tootrue。
  
每種動作類型都有一組可定義動作行為的不同**輸入**。  
  
## <a name="http-action"></a>HTTP 動作  

HTTP 動作呼叫指定的端點，並檢查 hello 回應 toodetermine，是否應該執行 hello 工作流程。 hello**輸入**物件會使用參數需要的 tooconstruct hello HTTP 呼叫 hello 組：  
  
|元素名稱|必要|類型|說明|  
|----------------|------------|--------|---------------|  
|method|是|String|可以是其中一個 hello 遵循 HTTP 方法：**取得**， **POST**，**放**，**刪除**，**修補**，或**標頭**|  
|uri|是|String|hello http 或 https 端點時所呼叫。 最大長度為 2 KB。|  
|查詢|否|Object|代表 hello 查詢參數 tooadd toohello URL。 例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。|  
|headers|否|Object|代表每個 toohello 要求會傳送 hello 標頭。 例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|否|Object|表示傳送 toohello 端點的 hello 裝載。|  
|RetryPolicy|否|Object|可讓您自訂 hello 重試行 4xx 或 5xx 錯誤。|  
|operationsOptions|否|String|定義特殊的行為 toooverride hello 組。|  
|驗證|否|Object|代表 hello 要求的 hello 方法應該進行驗證。 如需此物件的詳細資訊，請參閱[排程器輸出驗證](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)。 除了排程器外，還有一個支援的屬性︰`authority`。 根據預設，在未指定時這會是 `https://login.windows.net`，但您可以使用不同的受眾，例如 `https://login.windows\-ppe.net`|  
  
HTTP 動作 \(和 API 連線\) 動作支援重試原則。 重試原則會套用 toointermittent 失敗，是做為特性與 HTTP 狀態碼 408、 429 和 5xx，加法 tooany 連線例外狀況。 說明此原則使用 hello *retryPolicy*物件定義如下所示：
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
hello ISO 8601 格式指定 hello 重試間隔。 在此時間間隔具有預設的 20 秒，最小值，而 hello 最大值為一小時。 hello 預設值和最大重試計數為四個小時。 如果未指定 hello 重試原則定義，`fixed`策略會搭配預設重試計數和間隔值。 toodisable hello 重試原則，將其類型設定太`None`。  
  
例如，hello 下列動作重試擷取 hello 最新消息兩次，如果有斷斷續續地發生失敗，總共有三個執行中，每個嘗試之間會有 30 秒延遲：  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>非同步模式

根據預設，所有以 HTTP 為基礎的動作支援 hello 標準的非同步作業模式。 因此如果 hello 遠端伺服器指出該 hello 要求已接受以進行處理，202 的\(接受\)回應 hello Logic Apps 引擎會持續輪詢 hello 直到到達終端機 hello 回應的位置標頭中指定的 URL狀態\(非\-202 回應\)。  
  
toodisable hello 非同步行為先前所述，設定`DisableAsyncPattern`hello 動作輸入中的選項。 在此情況下，hello 動作的 hello 輸出根據 hello 初始 202 回應 hello 伺服器。  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>非同步限制

非同步模式可限制其持續時間 tooa 特定時間間隔中。  如果 hello 時間間隔超過期限而未到達終止狀態，將會標示 hello hello 動作狀態`Cancelled`的代碼`ActionTimedOut`。  採用 ISO 8601 格式指定 hello 限制逾時。  限制可以指定以 hello，請使用下列語法：

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>API 連線  

API 連線是參考 Microsoft 管理之連接器的動作。
這個動作需要參考 tooa 有效連接，以及有關 hello API 和所需的參數。

|元素名稱|必要|類型|說明|  
|----------------|------------|--------|---------------|  
|主機|是|Object|表示 hello 連接器資訊，例如 hello runtimeUrl 和參考 toohello 連接物件|
|method|是|String|可以是其中一個 hello 遵循 HTTP 方法：**取得**， **POST**，**放**，**刪除**，**修補**，或**標頭**|  
|路徑|是|String|hello 應用程式開發介面作業的 hello 路徑。|  
|查詢|否|Object|代表 hello 查詢參數 tooadd toohello URL。 例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。|  
|headers|否|Object|代表每個 toohello 要求會傳送 hello 標頭。 例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|否|Object|表示傳送 toohello 端點的 hello 裝載。|  
|RetryPolicy|否|Object|可讓您自訂 hello 重試行 4xx 或 5xx 錯誤。|  
|operationsOptions|否|String|定義特殊的行為 toooverride hello 組。|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>API 連線 Webhook 動作

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Webhook 動作的限制可以在 hello 中指定相同的方式[HTTP 非同步限制](#asynchronous-limits)。
  
## <a name="response-action"></a>回應動作  

此動作的類型包含從 HTTP 要求的 hello 整個回應內容，並包含 statusCode、 本文和標頭：  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
hello 回應動作有特殊限制不適用 tooother 動作。 具體而言：  
  
-   回應動作無法平行定義中，因為具決定性的回應 toohello 連入要求為必要項。  
  
-   如果收到回應 hello 連入要求之後，將到達回應動作，hello 動作會被視為失敗\(衝突\)，且如此一來，執行 hello `Failed`。  
  
-   具有回應動作的工作流程在其觸發程序中不能有 `splitOn`，因為一個呼叫就會導致許多個執行。 如此一來，這應該驗證 hello 資料流程時 PUT 和不正確的要求可能的原因。  
  
## <a name="wait-action"></a>等候動作  

hello`wait`動作暫止工作流程執行 hello 指定時間間隔。 例如，toowait 15 分鐘，您可以使用此程式碼片段：  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
或者，toowait 特定時間點，直到您可以使用此範例：  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> hello 等候持續時間可能是使用可以指定 hello**間隔**物件或 hello**直到**物件，但非兩者。  
  
|名稱|必要|類型|說明|  
|--------|------------|--------|---------------|  
|interval|否|Object|hello 等候一段時間為基礎的持續時間。|  
|間隔單位|是|String|下列其中一個間隔︰秒、分鐘、小時、天、週、月、年。|  
|間隔計數|是|String|根據給定內部單位 hello 持續時間。|  
|直到|否|Object|hello 等候以時間為基礎的點上的持續時間。|  
|直到時間戳記|是|String|字串 &#124; hello hello 等候到期時的 UTC 時間點。|  

## <a name="query-action"></a>查詢動作

hello`query`動作可讓您篩選條件所根據的陣列。 例如，tooselect 數字大於 2，您可以使用：

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

hello 輸出 hello`query`動作是陣列，其中具有 hello 輸入陣列中滿足 hello 條件的項目。

> [!NOTE]
> 如果沒有任何值滿足 hello`where`條件，hello 結果為空陣列。

|名稱|必要|類型|說明|
|--------|------------|--------|---------------|
|from|是|陣列|hello 來源陣列。|
|其中|是|String|hello 條件 tooapply tooeach hello 來源陣列元素。|

## <a name="select-action"></a>選取動作

hello`select`動作可讓您在規劃新的值陣列的每個項目。
例如，tooconvert 的數字讀入陣列物件的陣列，您可以使用：

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

hello 的 hello 輸出`select`動作是陣列，其中具有 hello 由相同的基數為 hello 輸入的陣列，其中每個元素轉換成定義的 hello`select`屬性。 Hello 輸入是空的陣列，如果 hello 輸出也會為空陣列。

|名稱|必要|類型|說明|
|--------|------------|--------|---------------|
|from|是|陣列|hello 來源陣列。|
|選取|是|任意|hello 投影 tooapply tooeach hello 來源陣列元素。|

## <a name="terminate-action"></a>終止動作

hello 終止動作停止執行 hello 工作流程執行時，中止執行中的任何動作，並略過任何其餘的動作。 比方說，tooterminate 狀態執行**失敗**，您可以使用下列程式碼片段的 hello:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> 已完成的動作不會受到 hello 終止動作。

|名稱|必要|類型|說明|
|--------|------------|--------|---------------|
|runStatus|是|String|hello 目標執行狀態。 **失敗**或**取消**。|
|runError|否|Object|hello 錯誤詳細資料。 只支援當**runStatus**設定得**失敗**。|
|runError 代碼|否|String|hello 執行錯誤的程式碼。|
|runError 訊息|否|String|hello 執行錯誤訊息。|

## <a name="compose-action"></a>撰寫動作

hello 撰寫動作可讓您建構任意的物件。 hello hello 輸出撰寫動作是 hello 結果評估其輸入。 例如，您可以使用 hello 撰寫多個動作的動作 toomerge 輸出：

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> hello**撰寫**動作可以使用的 tooconstruct 任何輸出，包括物件、 陣列和任何其他原生支援的邏輯應用程式，例如 XML 和二進位的型別。

## <a name="table-action"></a>資料表動作

hello`table`可讓您的項目插入陣列 tooconvert **CSV**或**HTML**資料表。

假設 @triggerBody() 是

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

並讓 hello 動作定義為

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

會產生上述 hello

<table><thead><tr><th>id</th><th>名稱</th></tr></thead><tbody><tr><td>0</td><td>apples</td></tr><tr><td>1</td><td>oranges</td></tr></tbody></table>"

在順序 toocustomize hello 資料表中，您可以明確地指定 hello 資料行。 例如：

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

會產生上述 hello

<table><thead><tr><th>產生識別碼</th><th>說明</th></tr></thead><tbody><tr><td>0</td><td>fresh apples</td></tr><tr><td>1</td><td>fresh oranges</td></tr></tbody></table>"

如果 hello`from`屬性值為空陣列，hello 輸出，則為空的資料表。

|名稱|必要|類型|說明|
|--------|------------|--------|---------------|
|from|是|陣列|hello 來源陣列。|
|format|是|String|hello 格式，或是**CSV**或**HTML**。|
|columns|否|陣列|hello 資料行。 允許 hello 資料表 toooverride hello 預設的圖形。|
|資料行標頭|否|String|hello 資料行標頭的 hello。|
|資料行值|是|String|hello hello 資料行值。|

## <a name="workflow-action"></a>工作流程動作   

|名稱|必要|類型|說明|  
|--------|------------|--------|---------------|  
|主機識別碼|是|String|您想 toocall hello 工作流程 hello 資源 ID。|  
|主機 triggerName|是|String|hello 想 tooinvoke hello 觸發程序名稱。|  
|查詢|否|Object|代表 hello 查詢參數 tooadd toohello URL。 例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。|  
|headers|否|Object|代表每個 toohello 要求會傳送 hello 標頭。 例如，tooset hello 語言和類型的要求：`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|否|Object|表示傳送 toohello 端點 hello 裝載。|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Hello 工作流程上進行存取檢查\(更具體來說，hello 觸發程序\)，表示您需要存取 toohello 工作流程。  
  
hello 輸出從 hello`workflow`動作根據您定義在 hello `response` hello 子工作流程中的動作。 如果未定義任何`response`動作，然後 hello 輸出是空的。  

## <a name="function-action"></a>函式動作   

|名稱|必要|類型|說明|  
|--------|------------|--------|---------------|  
|函式識別碼|是|String|您想 tooinvoke 的 hello 函式 hello 資源 ID。|  
|method|否|String|hello HTTP 方法使用 tooinvoke hello 函式。 若未指定，則其預設值為 `POST`。|  
|查詢|否|Object|代表 hello 查詢參數 tooadd toohello URL。 例如，`"queries" : { "api-version": "2015-02-01" }`新增`?api-version=2015-02-01`toohello URL。|  
|headers|否|Object|代表每個 toohello 要求會傳送 hello 標頭。 例如，tooset hello 語言和類型的要求： `"headers" : { "Accept-Language": "en-us" }`。|  
|body|否|Object|表示傳送 toohello 端點 hello 裝載。|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

當您儲存 hello 邏輯應用程式時，我們會執行某些檢查參考的 hello 函式：
-   您需要 toohave access toohello 函式。
-   僅允許使用標準 HTTP 觸發程序或一般 JSON Webhook 觸發程序。
-   它不應定義任何路由。
-   只允許使用「函式」和「匿名」授權層級。

擷取、 快取，且在執行階段使用 hello 觸發程序 URL。 因此如果任何作業會導致快取的 hello URL 無效，hello 動作便會在執行階段。 此 toowork 儲存 hello 邏輯應用程式，這將導致邏輯應用程式 tooretrieve 並再次快取 hello 觸發程序的 URL。

## <a name="collection-actions-scopes-and-loops"></a>集合動作 (範圍和迴圈)

某些動作類型可以在自身當中包含動作。 在集合中的參考動作，可直接之外 hello 集合參考。 如果您在某個範圍中定義了 `http`，`@body('http')` 仍會在工作流程中的任何位置保持有效。 在集合中的動作可以`runAfter`內其他動作 hello 相同的集合。

## <a name="scope-action"></a>範圍動作

hello`scope`動作可讓您以邏輯方式群組動作工作流程中的。

|名稱|必要|類型|說明|  
|--------|------------|--------|---------------|  
|動作|是|Object|內部動作 tooexecute hello 範圍內|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>ForEach 動作

這個迴圈動作會逐一查看陣列並對每個項目執行內部動作。 根據預設，平行 （20 執行以平行方式一次） 執行 hello foreach 迴圈 」。 您可以設定執行規則使用 hello`operationOptions`參數。

|名稱|必要|類型|說明|  
|--------|------------|--------|---------------|  
|動作|是|Object|Hello 迴圈內的內部動作 tooexecute|
|foreach|是|字串|透過 hello 陣列 tooiterate|
|operationOptions|no|string|行為的任何作業選項。 目前只支援`sequential`tooexecute 反覆項目以循序方式 （預設行為是平行）|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>直到動作

此迴圈的動作會執行內部的動作，直到條件結果 tootrue 為止。

|名稱|必要|類型|說明|  
|--------|------------|--------|---------------|  
|動作|是|Object|Hello 迴圈內的內部動作 tooexecute|
|expression|是|字串|每個反覆項目之後的 hello 運算式 tooevaluate|
|limit|yes|Object|必須定義 hello 迴圈-至少一個限制的 hello 限制|
|計數|no|int|hello toohello 數目限制可以執行的反覆項目|
|timeout|no|字串|hello 多久它應該循環逾時。  ISO 8601 格式|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>條件 - If 動作

hello`If`動作可讓您評估條件，以及執行分支，根據是否 hello 運算式評估太`true`。

|名稱|必要|類型|說明|  
|--------|------------|--------|---------------|  
|動作|是|Object|當運算式評估過的內部動作 tooexecute`true`|
|expression|是|字串|hello 運算式 tooevaluate|
|else|no|Object|當運算式評估過的內部動作 tooexecute`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
hello 下表顯示條件如何在動作中使用運算式的範例：  
  
|JSON 值|結果|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|會評估 tootrue 任何值會導致此狀況 toopass。 僅支援布林運算式。 其他 tooconvert 類型 tooBoolean，使用函數`empty`， `equals`。|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|支援比較函式。 如 hello 範例，hello 動作時才執行 act1 hello 輸出大於 hello 臨界值。|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|邏輯函數也會支援的 toocreate 巢狀布林運算式。 在此情況下，hello 動作執行 hello 臨界值高於或低於 100 的 act1 hello 輸出時。|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|如果陣列沒有任何項目，您可以使用陣列函式 toocheck。 在此情況下，hello 動作執行時 hello 錯誤陣列是空的。| 
|`"expression": "parameters('hasSpecialAction')"`|錯誤 - 不是有效條件，因為條件必須有 @。|  
  
如果條件評估成功，hello 條件標示為`Succeeded`。 動作內任一 hello`actions`或`else`物件的評估太`Succeeded`時執行，且成功，`Failed`時執行，且失敗，或`Skipped`時不會執行該分支。

## <a name="next-steps"></a>後續步驟

[工作流程服務 REST API](https://docs.microsoft.com/rest/api/logic/workflows)
