---
title: "aaaOpenAPI Azure 函式中的中繼資料 |Microsoft 文件"
description: "Azure Functions 中的 OpenAPI 支援概觀"
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
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Azure Functions 中的 OpenAPI 2.0 中繼資料支援 (預覽)
OpenAPI 2.0 (先前稱為 Swagger) Azure 函式中的中繼資料支援是預覽功能，您可以使用 toowrite OpenAPI 2.0 定義函式應用程式內。 您接著可以使用 hello 函式應用程式來裝載該檔案。

[OpenAPI 中繼資料](http://swagger.io/)可讓主控 REST API toobe 函式供各種不同的其他軟體。 此軟體包含 Microsoft 供應項目，例如 PowerApps 和 hello [Azure App Service API 應用程式功能](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier)，例如協力廠商開發人員工具[郵差](https://www.getpostman.com/docs/importing_swagger)，和[許多更多封裝](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>我們建議您從 hello[快速入門教學課程](./functions-api-definition-getting-started.md)然後有關特定功能的詳細資訊傳回 toothis 文件 toolearn。

## <a name="enable"></a>啟用 OpenAPI 定義支援
您可以設定所有 OpenAPI 上 hello **API 定義**中函式應用程式的頁面**平台功能**。

tooenable hello 產生託管的 OpenAPI 定義和快速入門的定義中，設定**API 定義來源**太**函式 （預覽）**。 **外部 URL**允許函式 toouse OpenAPI 定義裝載存放在其他地方。

## <a name="generate-definition"></a> 從您的函式中繼資料產生 Swagger 基本架構
範本可協助您開始撰寫第一個 OpenAPI 定義。 hello 定義範本功能會建立疏鬆 OpenAPI 定義使用 hello function.json 檔案中的 hello 的所有中繼資料，每個 HTTP 觸發程序函式。 您將需要 toofill 中的詳細資訊，您的 API，從 hello 相關[OpenAPI 規格](http://swagger.io/specification/)，例如要求和回應的範本。

如需逐步指示，請參閱 hello[快速入門教學課程](./functions-api-definition-getting-started.md)。

### <a name="templates"></a>可用範本

|名稱| 描述 |
|:-----|:-----|
|已產生的定義|OpenAPI 具有定義 hello 最大數量來推斷從 hello 函式的現有中繼資料的資訊。|

### <a name="quickstart-details"></a>產生的 hello 定義中包含的中繼資料

下列表格代表 hello hello Azure 入口網站設定和 function.json 中的對應資料，所以產生的對應的 toohello Swagger 基本架構。

|Swagger.json|入口網站 UI|Function.json|
|:----|:-----|:-----|
|[Host](http://swagger.io/specification/#fixed-fields-15)|**函式應用程式設定** > **App Service 設定** > **概觀** > **URL**|不存在
|[Paths](http://swagger.io/specification/#paths-object-29)|[整合] > [選取的 HTTP 方法]|繫結：路由
|[Path Item](http://swagger.io/specification/#path-item-object-32)|[整合] > [路由範本]|繫結：方法
|[安全性](http://swagger.io/specification/#security-scheme-object-112)|**金鑰**|不存在|
|operationID*|**路由 + 允許的動詞**|路由 + 允許的動詞|

\*只需要整合與 PowerApps 和流程 hello 作業識別碼。
> [!NOTE]
> hello x ms 摘要延伸模組提供邏輯應用程式、 PowerApps，以及流程中的顯示名稱。
>
> 詳細資訊，請參閱 toolearn[自訂您的 Swagger 定義 powerapps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/)。

## <a name="CICD"></a>使用 CI/CD tooset 應用程式開發介面定義

 您必須啟用應用程式開發介面定義裝載 hello 入口網站中啟用原始檔控制 toomodify 您從原始檔控制的應用程式開發介面定義之前。 遵循下列指示：

1. 瀏覽過**API 定義 （預覽）**函式應用程式設定中。
  1. 設定**API 定義來源**太**函式**。
  1. 按一下**產生應用程式開發介面定義範本**然後**儲存**toocreate 稍後修改的範本定義。
  1. 請注意您的 API 定義 URL 和金鑰。
1. [設定持續整合/持續部署 (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements)。
2. 在原始檔控制中的 \site\wwwroot\.azurefunctions\swagger\swagger.json 修改 swagger.json。

現在，tooswagger.json 在您的儲存機制中所裝載的應用程式函式，在 hello API 定義 URL 的變更，並記下的索引鍵步驟 1.c。

## <a name="next-steps"></a>後續步驟
* [入門教學課程](functions-api-definition-getting-started.md)。 請嘗試我們的逐步解說 toosee OpenAPI 中定義的動作。
* [Azure Functions GitHub 存放庫](https://github.com/Azure/Azure-Functions/)。 簽出 hello 函式儲存機制 toogive 我們 hello API 定義支援預覽的意見反應。 針對您想要更新的 toosee 的任何項目進行 GitHub 問題。
* [Azure Functions 開發人員參考](functions-reference.md)。 深入了解如何撰寫函式程式碼及定義觸發程序和繫結。
