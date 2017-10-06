---
title: "aaaGetting Started with OpenAPI Azure 函式中的中繼資料 |Microsoft 文件"
description: "開始使用 Azure Functions 中的 OpenAPI 支援"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>建立函數應用程式的 OpenAPI 2.0 (Swagger) 中繼資料 (預覽)

這份文件會引導您建立裝載於 Azure 函式上的簡單 api OpenAPI 定義的 hello 逐步程序。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>OpenAPI (Swagger) 是什麼？
[Swagger 中繼資料](http://swagger.io/)是檔案，定義 hello 功能和作業模式的 API，可讓裝載各種不同的其他軟體所耗用的 REST API toobe 函式。 Microsoft 供應項目要 PowerApps 和[API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier)，以及第 3 個合作對象開發人員工具，例如[郵差](https://www.getpostman.com/docs/importing_swagger)和[許多更多封裝](http://swagger.io/tools/)全部允許使用與您 API toobeSwagger 定義。

## <a name="prepare-function"></a>建立包含簡單 API 的函數
  toocreate OpenAPI 定義，我們必須先 toocreate 具有簡單的應用程式開發介面的函式。 如果您已經有函式的應用程式上裝載的 API，您可以略過直線 toohello 下一節
1. 建立新的函數應用程式。
    1. [Azure 入口網站](https://portal.azure.com) > `+ New` > 搜尋「函數應用程式」
1. 在新的函數應用程式中建立新的 HTTP 觸發程序函數
    1. 系統已經將定義非常簡單之 REST API 的程式碼，預先填入您的函數。
    1. 任何字串做為查詢參數，或在 hello 主體中傳遞 toohello 函式會傳回為"Hello {輸入}"
1. 移 toohello `Integrate` ] 索引標籤的 [新的 HTTP 觸發程序函式
    1. 切換`Allowed HTTP methods`太`Selected methods`
    1. 在 `Selected HTTP methods` 中，取消選取除了 POST 之外的所有動詞。
    ![選取的 HTTP 方法](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. 此步驟日後會簡化您的 API 定義。

## <a name="enable"></a>啟用 API 定義支援
1. 瀏覽過`your function name` > `Platform Features` > `API Definition`
![定義索引標籤](./media/functions-api-definition-getting-started/definitiontab.png)
1. 設定`API Definition Source`太`Function (preview)`
    1. 這個步驟可讓一套應用程式的函式，包括端點 toohost OpenAPI 檔案，從您的函式應用程式定義域，hello 的內嵌複本 OpenAPI 選項[OpenAPI 編輯器](http://editor.swagger.io)，和 快速入門定義產生器。
![已啟用的定義](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>從範本建立 API 定義
1. 按一下 `Generate API Definition template`
    1. 此步驟會掃描您 HTTP 觸發程序函式的函式應用程式，並使用 functions.json toogenerate OpenAPI 文件中的 hello 資訊。
1. 太加入作業物件`paths: /api/yourfunctionroute post:`
    1. hello 快速入門 OpenAPI 文件是完整的 OpenAPI 文件大綱。它需要更多的中繼資料 toobe 完整 OpenAPI 定義，例如作業物件，以及回應範本。
    1. hello 以下的範例作業物件已填滿/會產生取用區段、 參數物件，和回應物件。
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  x-ms-summary 提供 Logic Apps、Flow 和 PowerApps 中的顯示名稱。
    >
    > 簽出[自訂您的 Swagger 定義 powerapps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn 更多。

1. 按一下`save`toosave 變更![加入樣板定義](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>使用 API 定義
1. 複製您`API definition URL`並貼到新的瀏覽器索引標籤 tooview 原始 OpenAPI 文件。
1. 您可以匯入您 OpenAPI 文件 tooany 許多工具進行測試和使用該 URL 的整合。
    1. 許多 Azure 資源都可以 tooautomatically 匯入使用您 OpenAPI doc hello 儲存函式應用程式設定中的 API 定義 URL。 Hello 的一部份`Function`API 定義的來源，我們為您更新該 url。


## <a name="test-definition"></a>使用 hello Swagger UI tootest 您應用程式開發介面的定義
那里正在測試的 hello 內嵌應用程式開發介面定義編輯器 toohello UI 檢視內建的工具。 新增您的 API 金鑰，然後使用 hello`Try this operation`下的每個方法。 hello 工具會使用您的應用程式開發介面定義 tooformat hello 要求和成功的回應會指出您定義正確。

### <a name="steps"></a>步驟：

1. 複製函數 API 金鑰
    1. 在 HTTP 觸發程序函式中可以找到 hello API 金鑰`function name` > `Keys` > `Function Keys` 
  ![功能鍵](./media/functions-api-definition-getting-started/functionkey.png)
1. 瀏覽 toohello`API Definition`頁面。
    1. 按一下`Authenticate`hello 頂端，將您函式的 API 金鑰 toohello 安全性物件。
  ![OpenAPI 金鑰](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. 選取 `/api/yourfunctionroute` > `POST`
1. 按一下`Try it out`並輸入名稱 tootest
1. 您應該會在 `Pretty` 下看到測試結果「成功」
![API 定義測試](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>後續步驟
* [函數中的 OpenAPI 定義概觀](functions-api-definition.md)
  * 閱讀 hello OpenAPI 支援的詳細資訊的完整文件。
* [Azure Functions 開發人員參考](functions-reference.md)  
  * 可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。
* [Azure Functions GitHub 存放庫](https://github.com/Azure/Azure-Functions/)
  * 簽出 hello 函式 GitHub toogive 我們 hello API 定義支援預覽的意見 ！ 針對您想要更新的 toosee 的任何項目進行 GitHub 問題。
