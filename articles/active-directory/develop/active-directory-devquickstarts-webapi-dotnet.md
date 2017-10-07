---
title: "aaaAzure AD.NET web API 開始使用 |Microsoft 文件"
description: "如何 toobuild.NET MVC web 應用程式開發介面，與整合 Azure AD 進行驗證和授權。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>使用來自 Azure AD 的持有者權杖來保護 Web API
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

如果您正在建置 tooprotected 資源提供存取的應用程式，您需要 tooknow tooprevent 未經授權存取 toothose 資源的方式。
Azure Active Directory (Azure AD) 可更容易及直接 toohelp 只有幾行程式碼使用 OAuth 2.0 承載的存取權杖來保護 web API。

在 ASP.NET web 應用程式，您可以使用 hello 社群導向 OWIN 中介軟體包含在.NET Framework 4.5 中的 hello Microsoft 實作，以完成這項保護。 這裡我們將使用 OWIN toobuild"tooDo 清單 」 web API 的：

* 指定要保護哪些 API。
* 驗證 hello web 應用程式開發介面呼叫包含的有效存取權杖。

toobuild hello tooDo 清單應用程式開發介面，您必須先：

1. 向 Azure AD 註冊應用程式。
2. 設定 hello 應用程式 toouse hello OWIN 驗證管線。
3. 設定用戶端應用程式 toocall hello web API。

啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)。 每一個都是 Visual Studio 2013 解決方案。 您也需要哪些 tooregister 中的 Azure AD 租用戶應用程式。 如果沒有，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

## <a name="step-1-register-an-application-with-azure-ad"></a>步驟 1︰向 Azure AD 註冊應用程式
toohelp 來保護您的應用程式，先 toocreate 應用程式需要在您的租用戶與 Azure AD 提供幾項重要的資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. Hello 頂端列上，按一下您的帳戶。 在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。

3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。

4. 按一下 [應用程式註冊]，然後選取 [新增]。

5. 依照 hello 提示，並建立新**Web 應用程式和/或 Web API**。
  * **名稱**描述應用程式 toousers。 輸入**tooDo 清單服務**。
  * **重新導向 Uri**為配置和字串的組合，Azure AD 使用的 tooreturn 任何權杖已要求您的應用程式。 請為此值輸入 `https://localhost:44321/` 。

6. 從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。 輸入租用戶特定識別碼。 例如，輸入 `https://contoso.onmicrosoft.com/TodoListService`。

7. 儲存 hello 組態。 讓 hello 入口網站保持開啟，因為您還需要 tooregister 用戶端應用程式儘速。

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>步驟 2： 設定 hello 應用程式 toouse hello OWIN 驗證管線
toovalidate 連入要求和權杖，您需要 tooset 註冊您的應用程式 toocommunicate 與 Azure AD。

1. toobegin，開啟 hello 方案，並使用 Package Manager Console hello 新增 hello OWIN 中介軟體 NuGet 封裝 toohello TodoListService 專案。

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. 新增稱為 OWIN 啟動 「 類別 toohello TodoListService 專案`Startup.cs`。  以滑鼠右鍵按一下 hello 專案、 選取**新增** > **新項目**，然後搜尋**OWIN**。 hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。

3. 也變更 hello 類別宣告`public partial class Startup`。 我們已在另一個檔案中為您實作此類別的一部分。 在 hello`Configuration(…)`方法，呼叫太`ConfgureAuth(…)`tooset 註冊 web 應用程式的驗證。

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. 開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(…)`方法。 hello 參數中提供`WindowsAzureActiveDirectoryBearerAuthenticationOptions`將做為您的應用程式 toocommunicate 與 Azure AD 的座標。

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. 現在您可以使用`[Authorize]`屬性 toohelp 保護您的控制站和 JSON Web Token (JWT) 承載驗證的動作。 裝飾 hello`Controllers\TodoListController.cs`授權標記的類別。 這會強制在 hello 使用者 toosign 才能存取該頁面。

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    當授權的呼叫者已成功叫用一個 hello `TodoListController` Api，hello 動作可能會需要存取 tooinformation hello 呼叫者的相關。 OWIN 提供透過 hello hello 持有人權杖內存取 toohello 宣告`ClaimsPrincpal`物件。  

6. Web 應用程式開發介面的共通需求是 toovalidate hello 「 範圍 」 hello 權杖中。 這可確保該 hello 使用者同意 toohello 權限需要的 tooaccess hello tooDo 清單服務。

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. 開啟 hello `web.config` hello hello TodoListService 專案根目錄中的檔案，並在 hello 中輸入您的組態值`<appSettings>`> 一節。
  * `ida:Tenant`這是您的 Azure AD 租用戶-例如 contoso.onmicrosoft.com hello 名稱。
  * `ida:Audience`是 hello 您輸入 hello Azure 入口網站中的 hello 應用程式的應用程式識別碼 URI。

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>步驟 3： 設定用戶端應用程式和執行 hello 服務
您可以看到在動作中的 hello tooDo 清單服務之前，您需要 tooconfigure hello tooDo 清單用戶端，讓它可以從 Azure AD 取得權杖，並讓呼叫 toohello 服務。

1. 返回 toohello [Azure 入口網站](https://portal.azure.com)。

2. 在 Azure AD 租用戶中建立新的應用程式，然後選取**原生用戶端應用程式**hello 產生的提示字元中。
  * **名稱**描述應用程式 toousers。
  * 輸入`http://TodoListClient/`hello**重新導向 Uri**值。

3. 完成註冊之後，Azure AD 會指派唯一的應用程式識別碼 tooyour 應用程式。 您將需要此值在 hello 下一個步驟中，因此將它複製從 hello 應用程式頁面。

4. 從 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。 找出並選取 hello tooDo 清單服務，並將 hello**存取 TodoListService**權限下的**委派的權限**，然後按一下**完成**。

5. 在 Visual Studio 中開啟`App.config`在 hello TodoListClient 專案，然後輸入 hello 中的 設定值`<appSettings>`> 一節。

  * `ida:Tenant`這是您的 Azure AD 租用戶-例如 contoso.onmicrosoft.com hello 名稱。
  * `ida:ClientId`這是您所複製的 hello Azure 入口網站的 hello 應用程式識別碼。
  * `todo:TodoListResourceId`為 hello hello tooDo hello Azure 入口網站中輸入的清單服務應用程式的應用程式識別碼 URI。

## <a name="next-steps"></a>後續步驟
最後，清除、建置及執行每個專案。 如果您還沒有這麼做，現在是 hello 時間 toocreate 新的使用者，您租用戶中具有 *。 onmicrosoft.com 網域。 登入 toohello tooDo 清單用戶端與該使用者，並加入一些工作 toohello 使用者待辦事項清單。

參考，完成的 hello 範例 （不含您的組態值） 會提供[GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)。 您現在可以移動 toomore 身分識別案例。

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
