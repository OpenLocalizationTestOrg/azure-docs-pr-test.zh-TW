---
title: "aaaProtect Web API 後端 API 管理 Azure Active Directory 與 |Microsoft 文件"
description: "深入了解如何 tooprotect Web API 後端 API 管理與 Azure Active Directory。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>如何 tooprotect Web API 後端，使用 Azure Active Directory 與 API 管理
hello 下列影片示範如何 toobuild Web API 後端，然後使用 Azure Active Directory 與 API 管理使用 OAuth 2.0 通訊協定加以保護。  本文章提供概觀和步驟 hello 視訊中的 hello 的其他資訊。 這段 24 分鐘的視訊示範如何：

* 使用 AAD 建置 Web API 後端以及保護安全 - 從 1:30 開始
* Hello API 匯入 API 管理-開始 7:10
* 設定 hello 開發人員入口網站 toocall hello API-開始 9:09
* 設定桌面應用程式 toocall hello API-開始 18:08
* 設定 JWT 驗證原則 toopre-授權要求數-開始 20:47

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>建立 Azure AD 目錄
使用 Azure Active Directory 必須先備份您的 Web API 的 toosecure AAD 租用戶。 在這段視訊中，使用名為 **APIMDemo** 的租用戶。 toocreate AAD 租用戶登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)按一下**新增**->**應用程式服務**->**Active目錄**->**目錄**->**自訂建立**。 

![Azure Active Directory][api-management-create-aad-menu]

此範例會一同建立名為 **APIMDemo** 的目錄與名為 **DemoAPIM.onmicrosoft.com** 的預設網域。這個目錄會使用整個 hello 視訊。

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>建立由 Azure Active Directory 保護的 Web API 服務
在此步驟中，Web API 後端會使用 Visual Studio 2013 建立。 Hello 視訊的這個步驟會在 1:30。 toocreate Web API 後端專案在 Visual Studio 中，按一下**檔案**->**新增**->**專案**，然後選擇  **ASP.NET 網頁應用程式**從 hello **Web**範本清單。 在這個視訊 hello 專案命名為**APIMAADDemo**。 按一下**確定**toocreate hello 專案。 

![Visual Studio][api-management-new-web-app]

按一下**Web API**從 hello**從範本清單中選取**toocreate Web API 專案。 按一下 Azure Directory Authentication tooconfigure**變更驗證**。

![新增專案][api-management-new-project]

按一下**組織帳戶**，並指定 hello**網域**的 AAD 租用戶。 在此範例 hello 網域是**DemoAPIM.onmicrosoft.com**。 您可以從 hello 取得您目錄中的 hello 網域**網域**您目錄的索引標籤。

![網域][api-management-aad-domains]

在 hello 中設定所需的 hello**變更驗證**對話方塊，按一下**確定**。

![變更驗證][api-management-change-authentication]

當您按一下**確定**Visual Studio 將會嘗試 tooregister 應用程式與 Azure AD 目錄，而且可能會提示的 toosign 中由 Visual Studio。 使用您目錄的系統管理帳戶登入。

![登入 tooVisual Studio][api-management-sign-in-vidual-studio]

tooconfigure 這個專案與 Azure Web 應用程式開發介面檢查 hello 方塊**hello 雲端中的主機**，然後按一下**確定**。

![新增專案][api-management-new-project-cloud]

您可能會提示的 toosign tooAzure 中,，然後您可以設定 hello Web 應用程式。

![設定][api-management-configure-web-app]

此範例指定了一個名為 **APIMAADDemo** 的新 **App Service 方案**。

按一下**確定**tooconfigure hello Web 應用程式，並建立 hello 專案。

## <a name="add-hello-code-toohello-web-api-project"></a>新增 hello 程式碼 toohello Web API 專案
hello hello 視訊中的下一個步驟將加入 hello 程式碼 toohello Web API 專案。 這個步驟從 4:35 開始。

在此範例中的 hello Web API 實作使用模型和控制器的基本計算機服務。 tooadd hello 模型 hello 服務，以滑鼠右鍵按一下**模型**中**方案總管 中**選擇**新增**，**類別**。 Hello 類別命名`CalcInput`按一下**新增**。

新增下列 hello`using`陳述式 toohello 頂端 hello`CalcInput.cs`檔案。

```c#
using Newtonsoft.Json;
```

取代下列程式碼的 hello hello 產生類別。

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

以滑鼠右鍵按一下 [方案總管] 中的 [控制器]，然後選擇 [新增] -> [控制器]。 按一下 [Web API 2 控制器 - 空白]，然後按一下 [新增]。 型別**CalcController** hello 控制器命名，然後按一下**新增**。

![新增控制器][api-management-add-controller]

新增下列 hello`using`陳述式 toohello 頂端 hello`CalcController.cs`檔案。

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

取代下列程式碼的 hello hello 產生控制器類別。 此程式碼會實作 hello `Add`， `Subtract`， `Multiply`，和`Divide`hello 基本計算機 API 的作業。

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

按**F6** toobuild 及驗證 hello 解決方案。

## <a name="publish-hello-project-tooazure"></a>發行 hello 專案 tooAzure
這個步驟 hello Visual Studio 專案是發行的 tooAzure。 此步驟的視訊 hello 開頭 5:45。

toopublish hello 專案 tooAzure、 以滑鼠右鍵按一下 hello **APIMAADDemo**專案在 Visual Studio 中，選擇**發行**。 保持 hello hello 預設設定**發行 Web**對話方塊，按一下**發行**。

![Web 發佈][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>授與權限 toohello Azure AD 後端服務應用程式
Hello 後端服務的新應用程式會建立在 Azure AD 目錄 hello 設定的一部分，以及發佈的 Web API 專案的程序。 在此步驟中的 hello 視訊，開始 6:13，權限會授與 toohello Web API 後端。

![應用程式][api-management-aad-backend-app]

按一下 hello hello 應用程式 tooconfigure hello 所需的權限名稱。 瀏覽 toohello**設定** 索引標籤並捲動 toohello**權限 tooother 應用程式**> 一節。 按一下 hello**應用程式權限**旁邊的下拉式清單**Windows** **Azure Active Directory**，核取方塊 hello**讀取目錄資料**，然後按一下**儲存**。

![新增權限][api-management-aad-add-permissions]

> [!NOTE]
> 如果**Windows** **Azure Active Directory**是並未列在 權限 tooother 應用程式之下，按一下**新增應用程式**並將它加入從 hello 清單。
> 
> 

請記下 hello**應用程式識別碼 URI** hello API 管理開發人員入口網站設定 Azure AD 應用程式時，在後續步驟中使用。

![App 識別碼 URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Hello Web 應用程式開發介面匯入 API 管理
應用程式開發介面會在 hello API 發行者入口網站，可從 hello Azure 入口網站存取設定。 tooreach，按一下 **發行者入口網站**從您的 API 管理服務的 hello 工具列。 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[管理您的第一個應用程式開發介面][Manage your first API]教學課程。

![發行者入口網站][api-management-management-console]

作業可以是[手動加入 tooAPIs](api-management-howto-add-operations.md)，或可以匯入。 在這段視訊中從 6:40 開始，運算會以 Swagger 格式匯入。

建立名為`calcapi.json`與下列內容，並將它儲存 tooyour 電腦。 請確定該 hello`host`屬性指向 tooyour Web API 後端。 在此範例中使用 `"host": "apimaaddemo.azurewebsites.net"` 。

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

tooimport hello 計算機 API 中，按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**匯入 API**。

![匯入 API 按鈕][api-management-import-api]

執行下列步驟 tooconfigure hello [小算盤] 應用程式開發介面的 hello。

1. 按一下**檔案從**，瀏覽 toohello`calculator.json`檔案儲存，然後按一下 hello **Swagger**選項按鈕。
2. 型別**calc**到 hello **Web API URL 尾碼**文字方塊。
3. 按一下 hello**產品 （選擇性）**方塊，然後選擇**入門**。
4. 按一下**儲存**tooimport hello 應用程式開發介面。

![Add new API][api-management-import-new-api]

一旦匯入 hello API 時，hello hello api 摘要頁面會顯示 hello 發行者入口網站中。

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>從 hello 開發人員入口網站未順利呼叫 hello API
此時，hello 應用程式開發介面已匯入 API 管理，但無法尚未成功從呼叫 hello 開發人員入口網站是 Azure AD 驗證受到 hello 後端服務。 這示範於 hello 視訊開始使用 hello 步驟 7:40。

按一下**開發人員入口網站**從 hello 右上方 hello 發行者入口網站。

![開發人員入口網站][api-management-developer-portal-menu]

按一下**Api**按一下 hello**計算機**應用程式開發介面。

![開發人員入口網站][api-management-dev-portal-apis]

按一下 [試試看] 。

![試試看][api-management-dev-portal-try-it]

按一下**傳送**並記下的 hello 回應狀態**401 未授權**。

![傳送][api-management-dev-portal-send-401]

hello 要求是未經授權的因為 hello 後端 API 受到 Azure Active Directory。 在之前成功呼叫 hello API hello 開發人員入口網站必須先設定的 tooauthorize 開發人員使用 OAuth 2.0。 Hello 下列各節說明此程序。

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Hello 開發人員入口網站註冊為 AAD 應用程式
設定 hello 開發人員入口網站 tooauthorize 開發人員使用 OAuth 2.0 hello 第一個步驟是 tooregister hello 開發人員入口網站為 AAD 應用程式。 這示範開始 8:27 hello 視訊中。

瀏覽 toohello Azure AD 租用戶的這段影片中，在此範例中的 hello 第一個步驟中**APIMDemo**並瀏覽 toohello**應用程式** 索引標籤。

![新增應用程式][api-management-aad-new-application-devportal]

按一下 hello**新增**按鈕 toocreate 新的 Azure Active Directory 應用程式，然後選擇**加入我組織正在開發的應用程式**。

![新增應用程式][api-management-new-aad-application-menu]

選擇**Web 應用程式和/或 Web API**，輸入名稱，然後按一下 hello 下一步箭頭。 在此範例中使用 **APIMDeveloperPortal**。

![新增應用程式][api-management-aad-new-application-devportal-1]

如**登入 URL**輸入您的 API 管理服務的 hello URL，然後附加`/signin`。 在此範例中使用 `https://contoso5.portal.azure-api.net/signin` 。

如**應用程式識別碼 URL**輸入您的 API 管理服務的 hello URL，然後附加一些獨特的字元。 這些字元可以是任何想要的字元，在此範例中使用 `https://contoso5.portal.azure-api.net/dp`。 當 hello 預期**應用程式屬性**所設定，請按一下 hello 核取記號 toocreate hello 應用程式。

![新增應用程式][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>設定 API 管理 OAuth 2.0 授權伺服器
hello 下一個步驟是 tooconfigure API 管理中的 OAuth 2.0 授權伺服器。 此步驟會示範 hello 視訊開始 9:43。

按一下**安全性**hello API 管理 hello 左側，按一下功能表**OAuth 2.0**，然後按一下**新增授權**伺服器。

![新增授權伺服器][api-management-add-authorization-server]

中輸入名稱和選擇性描述 hello**名稱**和**描述**欄位。 這些欄位是 hello API 管理服務執行個體內使用的 tooidentify hello OAuth 2.0 授權伺服器。 在此範例中使用**授權伺服器示範**。 稍後當您指定用來驗證應用程式開發介面的 OAuth 2.0 伺服器 toobe，您會選取此名稱。

Hello**用戶端註冊頁面 URL**輸入預留位置的值，例如`http://localhost`。  hello**用戶端註冊頁面 URL**點 toohello 頁面上的使用者可以使用 toocreate 並且支援帳戶的使用者管理的 OAuth 2.0 提供者設定自己的帳戶。 在此範例中，使用者沒有建立和設定自己的帳戶，因此使用預留位置。

![新增授權伺服器][api-management-add-authorization-server-1]

接著，指定 [授權端點 URL] 和 [權杖端點 URL]。

![授權伺服器][api-management-add-authorization-server-1a]

這些值可以取自 hello**應用程式端點**hello hello 開發人員入口網站建立 AAD 應用程式頁面。 tooaccess hello 端點瀏覽 toohello**設定**hello AAD 應用程式索引標籤上，按一下 **檢視端點**。

![應用程式][api-management-aad-devportal-application]

![檢視端點][api-management-aad-view-endpoints]

複製 hello **OAuth 2.0 授權端點**並將它貼到 hello**授權端點 URL**文字方塊。

![新增授權伺服器][api-management-add-authorization-server-2]

複製 hello **OAuth 2.0 權杖端點**並將它貼到 hello**語彙基元端點 URL**文字方塊。

![新增授權伺服器][api-management-add-authorization-server-2a]

此外 toopasting hello 權杖端點，新增名為的其他主體參數**資源**並用 hello 值 hello**應用程式識別碼 URI**從 hello hello 後端服務的 AAD 應用程式建立發行 hello Visual Studio 專案時。

![App 識別碼 URI][api-management-aad-sso-uri]

接下來，指定 hello 用戶端認證。 這些是您想要的 hello 資源的 hello 認證 tooaccess，在此情況下 hello 開發人員入口網站。

![用戶端認證][api-management-client-credentials]

tooget hello**用戶端識別碼**，瀏覽 toohello**設定**hello hello 開發人員入口網站和複製 hello 的 AAD 應用程式 索引標籤**用戶端識別碼**。

tooget hello**用戶端密碼**按一下 hello**選取持續時間**下拉式清單中 hello**金鑰**區段，並指定間隔。 在此範例中使用 1 年。

![用戶端識別碼][api-management-aad-client-id]

按一下**儲存**toosave hello 組態和顯示 hello 金鑰。 

> [!IMPORTANT]
> 記下此金鑰。 一旦您關閉 hello Azure Active Directory 設定 視窗中，無法再次顯示 hello 索引鍵。
> 
> 

複製 hello 金鑰 toohello 剪貼簿，交換器後 toohello 發行者入口網站將 hello 金鑰貼至 hello**用戶端密碼**文字方塊中，按一下 **儲存**。

![新增授權伺服器][api-management-add-authorization-server-3]

緊接 hello 用戶端認證是授權碼授與。 複製此授權程式碼和參數後 tooyour Azure AD 開發人員入口網站應用程式設定 頁面上，並將 hello 授權授與貼入 hello**回覆 URL**欄位，然後按一下**儲存**一次。

![回覆 URL][api-management-aad-reply-url]

hello 下一個步驟是 tooconfigure hello hello 開發人員入口網站 AAD 應用程式權限。 按一下**應用程式權限**和核取方塊 hello**讀取目錄資料**。 按一下**儲存**toosave 這變更此項目，然後再按一下**新增應用程式**。

![新增權限][api-management-add-devportal-permissions]

按一下 hello 搜尋圖示，型別**APIM** hello 到開頭 方塊中，選取**APIMAADDemo**，按一下 hello 核取記號 toosave。

![新增權限][api-management-aad-add-app-permissions]

按一下**委派的權限**如**APIMAADDemo**和核取方塊 hello**存取 APIMAADDemo**，然後按一下**儲存**。 這可讓 hello 開發人員入口網站應用程式 tooaccess hello 後端服務。

![新增權限][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>啟用 hello [小算盤] 應用程式開發介面的 OAuth 2.0 使用者授權
既然 hello OAuth 2.0 的伺服器設定，您可以指定它在您的應用程式開發介面的 hello 安全性設定。 此步驟會示範 hello 視訊開始： 14:30。

按一下**Api**在 hello 左的窗格中，然後按一下**計算機**tooview 並設定其設定。

![計算機 API][api-management-calc-api]

瀏覽 toohello**安全性**索引標籤上，檢查 hello **OAuth 2.0**核取方塊，選取 hello 所需的授權伺服器從 hello**授權伺服器**下拉式清單中，按一下**儲存**。

![計算機 API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>已成功從 hello 開發人員入口網站中呼叫 hello [小算盤] 應用程式開發介面
既然 hello 應用程式開發介面上設定了 hello OAuth 2.0 授權，其作業可以順利呼叫從 hello 開發人員中心。 此步驟會示範 hello 視訊開始 15:00。

瀏覽後 toohello**加入兩個整數**hello 計算機服務中的 hello 開發人員入口網站按一下 操作的**試試**。 請注意 hello 中的新項目 hello**授權**區段您剛才加入的對應 toohello 授權伺服器。

![計算機 API][api-management-calc-authorization-server]

選取**授權碼**從 hello 授權下拉式清單，然後輸入 hello 帳戶 toouse hello 認證。 如果您已經登入 hello 可能不會提示您的帳戶。

![計算機 API][api-management-devportal-authorization-code]

按一下**傳送**和附註 hello**回應狀態**的**200 確定**和 hello hello 回應的內容中的 hello 作業的結果。

![計算機 API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>設定桌面應用程式 toocall hello 應用程式開發介面
hello hello 視訊中的下一個程序會從 16:30，然後設定簡單的桌面應用程式 toocall hello 應用程式開發介面。 hello 第一個步驟是 tooregister hello 桌面應用程式在 Azure AD 中的，並提供存取 toohello 目錄和 toohello 後端服務。 18:25 在沒有呼叫 hello [小算盤] 應用程式開發介面作業 hello 桌面應用程式的示範。

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>設定 JWT 驗證原則 toopre-授權要求
hello hello 視訊中的最後一個程序會從 20:48，然後為您示範如何 toouse hello[驗證 JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT)原則 toopre-驗證每個傳入要求的 hello 存取權杖，以授權要求。 如果 hello 要求未經過驗證的 JWT 原則 hello，hello 要求封鎖的 API 管理，並不會傳遞 toohello 後端。

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

如需的設定和使用此原則的另一個示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too13:50 向前快轉。 向前快轉 too15:00 toosee hello 原則在 hello 原則編輯器中設定，然後示範從 hello 開發人員入口網站及 hello 未呼叫作業的 too18:50 所需授權權杖。

## <a name="next-steps"></a>後續步驟
* 查看更多有關 API 管理的 [視訊](https://azure.microsoft.com/documentation/videos/index/?services=api-management) 。
* 針對其他方式 toosecure 後端服務，請參閱[相互憑證驗證](api-management-howto-mutual-certificates.md)。

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
