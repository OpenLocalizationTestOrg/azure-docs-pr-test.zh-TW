---
title: "aaaAdd 登入 tooa.NET MVC web 應用程式開發介面使用 hello Azure AD v2.0 端點 |Microsoft 文件"
description: "如何 toobuild.NET MVC Web 應用程式開發介面可接受來自這兩個個人 Microsoft 帳戶的語彙基元和工作或學校帳戶。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>保護 MVC web API
使用 Azure Active Directory hello v2.0 端點，您可以保護 Web 應用程式開發介面使用[OAuth 2.0](active-directory-v2-protocols.md)啟用具有兩個人的 Microsoft 帳戶的使用者和工作或學校帳戶 toosecurely 存取 Web API 的存取權杖。

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
>
>

在 ASP.NET Web API 中，您可以使用隨附於 .NET Framework 4.5 的 Microsoft OWIN 中介軟體來完成此項作業。  這裡我們將使用 OWIN toobuild"tooDo 清單 」 MVC Web API，可讓用戶端 toocreate 與讀取的工作，從使用者的待辦事項清單。  hello web API 將會驗證連入要求包含有效存取權杖，並拒絕任何受保護的路由，無法通過驗證的要求。  這個範例是使用 Visual Studio 2015 建置的。

## <a name="download"></a>下載
此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet)。  您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip)或再製 hello 基本架構：

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

hello 基本架構應用程式簡單的 api，包括所有 hello 未定案程式碼，但是遺漏之所有 hello 身分識別相關的片段。 若您不想沿著 toofollow，可改為複製或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip)。

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>註冊應用程式
在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。  請確定：

* 複製下 hello**應用程式識別碼**指派 tooyour 應用程式，您將需要它過期。

本 Visual Studio 方案也包含了「TodoListClient」，這是一個簡單的 WPF 應用程式。  hello TodoListClient 是如何在使用者登入時使用的 toodemonstrate，且用戶端可以發出如何要求 tooyour Web API。  在此情況下，hello TodoListClient 和 hello TodoListService 都由 hello 相同的應用程式。  tooconfigure hello TodoListClient，您也應該：

* 新增 hello**行動**平台應用程式。

## <a name="install-owin"></a>安裝 OWIN
既然您已註冊的應用程式，您需要 tooset 註冊您的應用程式 toocommunicate hello v2.0 與中的端點順序 toovalidate 連入要求 （& s） 權杖。

* toobegin，開啟 hello 方案，並加入 hello OWIN 中介軟體 NuGet 封裝 toohello TodoListService 專案使用 Package Manager Console hello。

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>設定 OAuth 驗證
* 新增稱為 OWIN 啟動 「 類別 toohello TodoListService 專案`Startup.cs`。  --> Hello 專案上的按一下滑鼠右鍵**新增** --> **新項目**--> 搜尋"OWIN"。  hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。
* 也變更 hello 類別宣告`public partial class Startup`-我們已實作了此類別的一部分，另一個檔案中。  在 hello`Configuration(…)`方法，請呼叫 tooConfgureAuth(...) tooset 註冊 web 應用程式的驗證。

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* 開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(…)`方法，將設定從 hello v2.0 端點的 hello Web API tooaccept 語彙基元。

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* 現在您可以使用`[Authorize]`屬性 tooprotect 您控制站和 OAuth 2.0 承載驗證的動作。  裝飾 hello`Controllers\TodoListController.cs`授權標記的類別。  這會強制在 hello 使用者 toosign 才能存取該頁面。

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* 當授權的呼叫者已成功叫用一個 hello `TodoListController` Api，hello 動作可能會需要存取 tooinformation hello 呼叫者的相關。  OWIN 提供透過 hello hello 持有人權杖內存取 toohello 宣告`ClaimsPrincpal`物件。  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* 最後，開啟 hello `web.config` hello hello TodoListService 專案根目錄中的檔案，並在 hello 中輸入您的組態值`<appSettings>`> 一節。
  * 您`ida:Audience`為 hello**應用程式識別碼**您輸入 hello 入口網站中的 hello 應用程式。

## <a name="configure-hello-client-app"></a>Hello 用戶端應用程式設定
您可以看到在動作中的 hello Todo 清單服務之前，您需要 tooconfigure hello Todo 清單用戶端，所以它可以從 hello v2.0 端點取得權杖，並進行呼叫 toohello 服務。

* 在 hello TodoListClient 專案中，開啟`App.config`並輸入您設定的值在 hello `<appSettings>` > 一節。
  * 您`ida:ClientId`您複製從 hello 入口網站應用程式識別碼。

最後，清除、建置並執行每個專案！  您現在已有 .NET MVC Web API，可從個人 Microsoft 帳戶及公司或學校帳戶接受權杖。  登入 hello TodoListClient，並呼叫 web api tooadd 工作 toohello 使用者的待辦事項清單。

如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip)，或您可以將其複製從 GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>後續步驟
您現在可以繼續探索其他主題。  您可能想 tootry:

[從 Web 應用程式呼叫 Web API >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

如需其他資源，請參閱：

* [hello v2.0 開發人員指南 >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" 標籤 >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>取得產品的安全性更新
我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。
