---
title: "透過 HTTP-Azure 邏輯應用程式的任何端點與 aaaCommunicate |Microsoft 文件"
description: "建立可以透過 HTTP 與任何端點通訊的邏輯應用程式"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>開始使用 hello HTTP 動作

以 hello HTTP 動作，您可以擴充工作流程，為您的組織，並透過 HTTP 通訊 tooany 端點。

您可以：

* 建立會在您管理的網站故障時啟動 (觸發程序) 的邏輯應用程式工作流程。
* Tooany 與端點通訊透過 HTTP tooextend 您的工作流程至其他服務。

請參閱 < 開始使用邏輯應用程式中的 hello HTTP 動作 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="use-hello-http-trigger"></a>使用 hello HTTP 觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。 [深入了解觸發程序](connectors-overview.md)。

以下是總 hello HTTP tooset 觸發程序在 hello 邏輯應用程式的設計工具中的範例順序。

1. 邏輯應用程式中加入 hello HTTP 觸發程序。
2. 填入您想 toopoll hello HTTP 端點的 hello 參數。
3. 修改 hello 循環間隔，在它輪詢的頻率。

   hello 邏輯應用程式現在就會引發與每個檢查期間，會傳回任何內容。

   ![HTTP 觸發程序](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Hello HTTP 觸發程序的運作方式

hello HTTP 觸發程序會呼叫 tooHTTP 端點傳送以週期性間隔。 根據預設，會低於 300 任何 HTTP 回應碼會導致邏輯應用程式 toorun。 toospecify 是否應該引發 hello 邏輯應用程式，您可以編輯程式碼檢視中的 hello 邏輯應用程式，並加入條件來評估 hello 之後 HTTP 呼叫。 以下是範例 HTTP 觸發程序引發時 hello 傳回狀態碼是否大於或等於太`400`。

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

關於 hello HTTP 觸發程序參數的完整詳細資料位於[MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger)。

## <a name="use-hello-http-action"></a>使用 hello HTTP 動作

動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 
[深入了解動作](connectors-overview.md)。

1. 選擇 [新增步驟] > [新增動作]。
3. 在 hello 動作搜尋方塊中，輸入**http** toolist hello HTTP 動作。
   
    ![選取 hello HTTP 動作](./media/connectors-native-http/using-action-1.png)

4. 新增 hello HTTP 呼叫的任何必要的參數。
   
    ![完成 hello HTTP 動作](./media/connectors-native-http/using-action-2.png)

5. Hello 設計工具工具列上，按一下**儲存**。 儲存並發行位置 （啟用） 在 hello 邏輯應用程式相同的時間。

## <a name="http-trigger"></a>HTTP 觸發程序
以下是 hello hello 觸發程序，此連接器支援的詳細資料。 hello HTTP 連接器有一個觸發程序。

| 觸發程序 | 說明 |
| --- | --- |
| HTTP |執行 HTTP 呼叫而傳回 hello 回應內容。 |

## <a name="http-action"></a>HTTP 動作
以下是此連接器支援的 hello 動作的 hello 詳細資料。 hello HTTP 連接器有一個可能的動作。

| 動作 | 說明 |
| --- | --- |
| HTTP |執行 HTTP 呼叫而傳回 hello 回應內容。 |

## <a name="http-details"></a>HTTP 詳細資料
hello 下列表格說明必要的 hello 與 hello 動作和 hello 對應輸出的詳細資料與使用 hello 動作相關聯的選擇性輸入的欄位。

#### <a name="http-request"></a>HTTP 要求
hello 如下 hello 動作，使外送 HTTP 要求的輸入的欄位。
標示 * 代表必要欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 方法 * |method |hello HTTP 指令動詞 toouse |
| URI* |uri |hello URI hello HTTP 要求 |
| headers |headers |HTTP 標頭 tooinclude 的 JSON 物件 |
| 內文 |body |hello HTTP 要求主體 |
| 驗證 |驗證 |詳細資料中 hello[驗證](#authentication)區段 |

<br>

#### <a name="output-details"></a>輸出詳細資料
hello 以下是輸出 hello HTTP 回應的詳細資料。

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| headers |物件 |回應標頭 |
| 內文 |物件 |回應物件 |
| Status Code |整數 |HTTP 狀態碼 |

## <a name="authentication"></a>驗證
hello Logic Apps 功能可讓您 toouse 不同類型的 HTTP 端點的驗證。 您可以使用這項驗證以 hello **HTTP**，  **[HTTP + Swagger](connectors-native-http-swagger.md)**，和 **[HTTP Webhook](connectors-native-webhook.md)** 連接器。 hello 下列類型是驗證的可設定：

* [基本驗證](#basic-authentication)
* [用戶端憑證驗證](#client-certificate-authentication)
* [Azure Active Directory (Azure AD) OAuth 驗證](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>基本驗證

hello 接驗證物件所需的基本驗證。
標示 * 代表必要欄位。

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| 類型* |type |驗證類型 (若為基本驗證必須是 `Basic` ) |
| 使用者名稱* |username |使用者名稱 tooauthenticate |
| 密碼* |password |密碼 tooauthenticate |

> [!TIP]
> 如果您想 toouse 無法從 hello 定義擷取密碼時，使用`securestring`參數與 hello `@parameters()`  
> [工作流程定義函式](http://aka.ms/logicappdocs)。

例如：

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>用戶端憑證驗證

hello 下列驗證物件所需的用戶端憑證驗證。 標示 * 代表必要欄位。

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| 類型* |類型 |hello 的驗證類型 (必須是`ClientCertificate`進行 SSL 用戶端憑證) |
| PFX* |pfx |hello hello 個人資訊交換 (PFX) 檔案的 Base64 編碼內容 |
| 密碼* |password |hello 密碼 tooaccess hello PFX 檔案 |

> [!TIP]
> toouse 將不會讀取儲存 hello 邏輯應用程式之後的 hello 定義中的參數，您可以使用`securestring`參數與 hello `@parameters()`  
> [工作流程定義函式](http://aka.ms/logicappdocs)。

例如：

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Azure AD OAuth 驗證
hello 接驗證物件所需的 Azure AD 的 OAuth 驗證。 標示 * 代表必要欄位。

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| 類型* |類型 |hello 的驗證類型 (必須是`ActiveDirectoryOAuth`for Azure AD OAuth) |
| 租用戶* |tenant |hello hello Azure AD 租用戶的租用戶識別碼 |
| 對象* |audience |您要求授權 toouse hello 資源。 例如：`https://management.core.windows.net/` |
| 用戶端識別碼* |clientId |hello hello Azure AD 應用程式的用戶端識別碼 |
| 密碼* |secret |hello 用戶端要求 hello 語彙基元的 hello 密碼 |

> [!TIP]
> 您可以使用`securestring`參數與 hello `@parameters()` [工作流程定義函式](http://aka.ms/logicappdocs)toouse 將不會在儲存之後 hello 定義可讀取的參數。
> 
> 

例如：

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>後續步驟
現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。

