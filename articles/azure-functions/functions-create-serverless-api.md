---
title: "使用 Azure 函式的無伺服器 API aaaCreate |Microsoft 文件"
description: "如何 toocreate 無伺服器應用程式開發介面使用 Azure 函式"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>使用 Azure Functions 建立無伺服器 API

在本教學課程中您將學習如何 Azure 函式可讓您 toobuild 高擴充性 Api。 Azure 功能中各種不同的語言，包括 Node.JS、 C# 中，以及更多的端點隨附內建 HTTP 觸發程序和更容易 tooauthor 繫結的集合。 在本教學課程中，您將在您的應用程式開發介面設計自訂 HTTP 觸發程序 toohandle 特定動作。 您也會準備整合 API 與 Azure Functions Proxy，並設定模擬 API，以擴充您的 API。 這些全部都被完成之上 hello 函式無伺服器計算環境中，因此您不需要調整規模資源 tooworry-您可只著重於您應用程式開發介面的邏輯。

## <a name="prerequisites"></a>必要條件 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

hello 產生函式將用於本教學課程的 hello rest。

### <a name="sign-in-tooazure"></a>登入 tooAzure

開啟 hello Azure 入口網站。 toodo，登入太[https://portal.azure.com](https://portal.azure.com)與 Azure 帳戶。

## <a name="customize-your-http-function"></a>自訂 HTTP 函式

根據預設，您 HTTP 觸發的函式是設定的 tooaccept 任何 HTTP 方法。 另外還有 hello 表單的預設 URL `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`。 如果您遵循 hello 快速入門中，然後`<funcname>`可能類似 「 HttpTriggerJS1"。 在本節中，您將修改對 hello 函式 toorespond 只有 tooGET 要求`/api/hello`改為路由。 

瀏覽 tooyour hello Azure 入口網站中的函式。 選取**整合**在 hello 左瀏覽。

![自訂 HTTP 函式](./media/functions-create-serverless-api/customizing-http.png)

使用 HTTP 觸發程序設定 hello 資料表中所指定。

| 欄位 | 範例值 | 說明 |
|---|---|---|
| 允許的 HTTP 方法 | 選取的方法 | 判斷哪些 HTTP 方法可能使用的 tooinvoke 此函式 |
| 選取的 HTTP 方法 | GET | 可讓您只選取的 HTTP 方法 toobe 用 tooinvoke 此函式 |
| 路由範本 | /hello | 決定哪些路由會使用的 tooinvoke 此函式 |

請注意您未包含 hello`/api`基底路徑前置詞在 hello 路由範本中，因為這由全域設定。

按一下 [儲存] 。

您可以在 [Azure Functions HTTP 和 webhook 繫結](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint)中，進一步了解自訂 HTTP 函式。

### <a name="test-your-api"></a>測試您的 API

接著，測試函式 toosee hello 新 API 介面使用它。

在左瀏覽的 hello 的 hello 函式的名稱上按一下瀏覽後 toohello 開發頁面。

按一下**取得函式 URL**和複製 hello URL。 您應該會看到它會使用 hello`/api/hello`現在路由。

Hello URL 複製到新的瀏覽器索引標籤或您慣用的 REST 用戶端。 根據預設，瀏覽器會使用 GET。

執行 hello 函式並確認它可運作。 您可能需要 tooprovide hello 「 名稱 」 參數查詢字串 toosatisfy hello 快速入門的程式碼。

您也可以嘗試呼叫 hello 與另一個 HTTP 方法 tooconfirm hello 函式不會執行的端點。 這麼做，您將需要 toouse REST 用戶端，例如 cURL、 郵差或 Fiddler。

## <a name="proxies-overview"></a>Proxy 概觀

在 hello 下一步 區段中，您就會出現您透過 proxy 的 API。 Azure 的函式 Proxy 是預覽功能，可讓您 tooforward 要求 tooother 資源。 您定義的 HTTP 端點類似 HTTP 觸發程序，但不需要撰寫程式碼 tooexecute，呼叫該端點時，您可以提供 URL tooa 遠端實作。 這可讓您 toocompose 成單一的 API 介面，如用戶端 tooconsume 輕鬆來源的多個應用程式開發介面。 這是特別有用，如果您想 toobuild microservices 為您的 API。

Proxy 可以指向 tooany HTTP 資源，例如：
- Azure Functions 
- [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) 中的 API 應用程式
- [Linux 上的 App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme) 中的 Docker 容器
- 其他任何裝載 API

toolearn 深入了解 proxy，請參閱[使用 Azure （預覽） 的函式 Proxy]。

## <a name="create-your-first-proxy"></a>建立您的第一個 Proxy

在本節中，您將建立新的 proxy 哪些可做為前端 tooyour 整體應用程式開發介面。 

### <a name="setting-up-hello-frontend-environment"></a>設定 hello 前端環境

重覆步驟 hello[建立函式的應用程式](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app)toocreate 新的函式應用程式在您將建立您的 proxy。 這個新的應用程式時，將做為 hello 前端上，我們的 api，以及您先前已編輯的 hello 函式應用程式將做為後端。

瀏覽 tooyour 新前端函式的應用程式在 hello 入口網站。

選取 [Settings] \(設定) 。 然後切換**啟用 Azure 函式 Proxy （預覽）**太 「 On 」。

選取 [平台設定]，然後選擇 [應用程式設定]。

向下捲動太**應用程式設定**並建立新的設定與索引鍵 」 HELLO_HOST"。 設定函式應用程式後端，其值 toohello 主機例如`<YourApp>.azurewebsites.net`。 這是您之前複製測試您的 HTTP 函式時的 hello URL 的一部分。 您將參考此設定在 hello 設定。

> [!NOTE] 
> 應用程式設定被建議 hello 主機組態 tooprevent hello proxy 的硬式編碼環境相依性。 使用應用程式設定時，表示您可以在不同環境間移動 hello proxy 組態，而且 hello 環境專屬的應用程式設定會套用。

按一下 [儲存] 。

### <a name="creating-a-proxy-on-hello-frontend"></a>建立 hello 前端上的 proxy

瀏覽 hello 入口網站中的上一頁 tooyour 前端函式應用程式。

在 [hello 左側導覽中，按一下 hello '+' 下一步] 再加上正負號太"Proxy （預覽） 」。

![建立 Proxy](./media/functions-create-serverless-api/creating-proxy.png)

使用 hello 資料表中所指定的 proxy 設定。

| 欄位 | 範例值 | 說明 |
|---|---|---|
| 名稱 | HelloProxy | 僅用於管理的易記名稱 |
| 路由範本 | /api/hello | 決定哪些路由會使用的 tooinvoke 這個 proxy |
| 後端 URL | https://%HELLO_HOST%/api/hello | 指定應該代理 hello 端點 toowhich hello 要求 |

請注意，Proxy 不提供 hello`/api`基底路徑前置詞，而且此包含在 hello 路由範本。

hello`%HELLO_HOST%`語法會參考您稍早建立的 hello 應用程式設定。 hello 解析 URL 將會為 tooyour 原始函式。

按一下 [建立] 。

藉由複製 hello Proxy URL 並測試它 hello 瀏覽器中，或使用您最愛的 HTTP 用戶端，您可以試用新的 proxy。

## <a name="create-a-mock-api"></a>建立模擬 API

接下來，您將使用 proxy toocreate 模擬的 API，為您的方案。 這可讓用戶端開發 tooprogress，而不需完全實作的 hello 後端。 稍後在開發中，您無法建立新的函式應用程式可支援此邏輯，並重新導向 proxy tooit。

toocreate 這模擬應用程式開發介面中，我們將建立新的 proxy，這次使用 hello[應用程式服務編輯器](https://github.com/projectkudu/kudu/wiki/App-Service-Editor)。 tooget 啟動，瀏覽 tooyour hello 入口網站中的函式應用程式。 選取 [平台功能]，找出 [App Service 編輯器]。 按一下此按鈕會在新的索引標籤中開啟 hello 應用程式服務的編輯器。

選取`proxies.json`在 hello 左瀏覽。 這是用於儲存所有您的 proxy hello 組態 hello 檔案。 如果您使用其中一個 hello[函式的部署方法](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)，這是您將會維護原始檔控制中的 hello 檔案。 toolearn 進一步了解此檔案，請參閱[Proxy 進階組態](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration)。

如果您有跟著到目前為止，您 proxies.json 看起來應該類似下列 hello:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

接下來，您將新增模擬 API。 取代 hello 下列 proxies.json 檔案：

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

這會將新的 proxy，"GetUserByName"，沒有 hello backendUri 內容。 而不是呼叫另一個資源，它會修改 hello Proxy 使用的回應覆寫預設回應。 要求和回應覆寫也可以搭配後端 URL 一起使用。 這是特別有用，當 proxy 處理 tooa 舊有系統，其中，您可能需要 toomodify 標頭、 查詢參數等 toolearn 深入了解要求和回應的覆寫，請參閱[修改要求和回應 Proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses)。

測試您模擬的 API 呼叫 hello`/api/users/{username}`使用瀏覽器或您最愛的 REST 用戶端端點。 要確定 tooreplace _{username}_與字串值，表示使用者名稱。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您學到如何 toobuild 和自訂 Azure 函式上的應用程式開發介面。 您也學到如何 toobring 多個 Api，包括 mocks，同時以統一的 API 介面的形式。 您可以使用這些技術 toobuild，任何複雜度的 Api 時，所有 hello 無伺服器上執行時計算模型提供的 Azure 函式。

hello 下列參考可能會很有用，因為您在開發您的 API，進一步：

- [Azure Functions HTTP 和 webhook 繫結](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [使用 Azure （預覽） 的函式 Proxy]
- [定義 Azure Functions API (預覽)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[使用 Azure （預覽） 的函式 Proxy]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
