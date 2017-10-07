---
title: "aaaAzure AD v2.0.NET web 應用程式登入使用者入門 |Microsoft 文件"
description: "如何 toobuild.NET MVC Web 應用程式的使用者使用簽署兩個人的 Microsoft 帳戶和工作或學校帳戶。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>新增登入 tooan.NET MVC web 應用程式
與 hello v2.0 端點，您可以快速加入具有兩個個人 Microsoft 帳戶的支援，以及工作或學校帳戶的驗證 tooyour web 應用程式。  在 ASP.NET Web 應用程式中，您可以使用隨附於 .NET Framework 4.5 的 Microsoft OWIN 中介軟體來完成此項作業。

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
>
>

 這裡我們會建置 web 應用程式使用 OWIN toosign hello 使用者顯示中的 hello 使用者的一些資訊和符號 hello 使用者登出 hello 應用程式。

## <a name="download"></a>下載
此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet)。  您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip)或再製 hello 基本架構：

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

在本教學課程的 hello 結尾處提供 hello 完成應用程式。

## <a name="register-an-app"></a>註冊應用程式
在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。  請確定：

* 複製下 hello**應用程式識別碼**指派 tooyour 應用程式，您將需要它過期。
* 新增 hello **Web**平台應用程式。
* 輸入正確的 hello**重新導向 URI**。 hello 重新導向 uri 表示的 tooAzure AD 其中應該導向驗證回應-此教學課程中的 hello 預設為`https://localhost:44326/`。

## <a name="install--configure-owin-authentication"></a>安裝及設定 OWIN 驗證
在這裡，我們會將設定 hello OWIN 中介軟體 toouse hello OpenID Connect 驗證通訊協定。  OWIN 將會使用的 tooissue 登入和登出要求、 管理 hello 使用者工作階段，以及取得 hello 使用者，在其他項目之間的相關資訊。

1. toobegin，開啟 hello `web.config` hello hello 專案根目錄中的檔案，並在 hello 中輸入您的應用程式組態值`<appSettings>`> 一節。

  * hello`ida:ClientId`為 hello**應用程式識別碼**指派 tooyour hello 註冊入口網站中的應用程式。
  * hello`ida:RedirectUri`為 hello**重新導向 Uri** hello 入口網站中輸入。

2. 接下來，加入 hello OWIN 中介軟體 NuGet 封裝 toohello 專案使用 Package Manager Console hello。

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. 新增 < OWIN 啟動類別 > toohello 專案呼叫`Startup.cs`右 hello 專案上的按一下-->**新增** --> **新項目**--> 搜尋"OWIN"。  hello OWIN 中介軟體將會叫用 hello`Configuration(...)`方法，當您啟動應用程式。
4. 也變更 hello 類別宣告`public partial class Startup`-我們已實作了此類別的一部分，另一個檔案中。  在 hello`Configuration(...)`方法，請呼叫 tooConfigureAuth(...) tooset 向上驗證 web 應用程式  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. 開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(...)`方法。  hello 的參數中提供`OpenIdConnectAuthenticationOptions`將做為您的應用程式 toocommunicate 與 Azure AD 的座標。  您也必須設定的 Cookie 驗證 tooset-hello OpenID Connect 中介軟體會使用 cookie hello 涵蓋下方。

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.
        
                                             ClientId = clientId,
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a>傳送驗證要求
您的應用程式已正確設定的 toocommunicate 與 hello v2.0 端點使用 hello OpenID Connect 的驗證通訊協定。  OWIN 已處理所有 hello 醜陋詳細的製作驗證訊息、 驗證 Azure ad 的權杖和維護使用者工作階段。  所有會維持為您的使用者是 toogive 方式 toosign 中的並登出。

- 您可以使用授權標記中控制站 toorequire 使用者登入時存取某一頁之前。  開啟`Controllers\HomeController.cs`，並加入 hello`[Authorize]`標記 toohello 有關控制站。
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- 您也可以在程式碼中使用從 OWIN toodirectly 發出驗證要求。  開啟 `Controllers\AccountController.cs`。  在 hello SignIn() 和 Signout 動作，會發出 OpenID Connect 的挑戰和登出要求，分別。

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- 現在，請開啟 `Views\Shared\_LoginPartial.cshtml`。  這是您將在其中顯示 hello 使用者在您的應用程式登入和登出連結，並列印出檢視中的 hello 使用者的名稱。

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a>顯示使用者資訊
驗證時使用 OpenID Connect 使用者，hello v2.0 端點會傳回包含宣告或有關 hello 使用者判斷提示的 id_token toohello 應用程式。  您可以使用這些宣告 toopersonalize 您的應用程式：

- 開啟 hello`Controllers\HomeController.cs`檔案。  您可以在 hello 透過您控制站存取 hello 使用者宣告`ClaimsPrincipal.Current`安全性主體物件。

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a>執行
最後，建置並執行您的應用程式！   使用個人 Microsoft 帳戶或工作或學校帳戶，登入，並注意 hello 使用者的身分識別會反映在 hello 上方導覽列中的方式。  您的 Web 應用程式現在使用業界標準的通訊協定保護，可以使用個人與工作/學校帳戶來驗證使用者。

如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip)，或您可以將其複製從 GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>後續步驟
您現在可以進入更進階的主題。  您可能想 tootry:

[保護 Web Api</與 hello hello v2.0 端點 >>](active-directory-devquickstarts-webapi-dotnet.md)

如需其他資源，請參閱：

* [hello v2.0 開發人員指南 >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" 標籤 >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>取得產品的安全性更新
我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。
