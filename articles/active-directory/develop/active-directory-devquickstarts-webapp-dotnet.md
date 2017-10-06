---
title: "aaaAzure AD.NET web 應用程式使用者入門 |Microsoft 文件"
description: "建置與 Azure AD 整合來進行登入的 .NET MVC Web 應用程式。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>使用 Azure AD 來進行 ASP.NET Web 應用程式登入和登出
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

藉由提供單一登入和登出只有幾行程式碼，Azure Active Directory (Azure AD) 可簡化您 toooutsource web 應用程式身分識別管理。 您可以使用.NET (OWIN) 中介軟體 hello Microsoft 開啟 Web 介面的實作來登入和移出 ASP.NET web 應用程式的使用者。 社群導向 OWIN 中介軟體包含在 .NET Framework 4.5 中。 本文將說明如何 toouse OWIN 至：

* 登入 tooweb hello 身分識別提供者以使用 Azure AD 的應用程式的使用者。
* 顯示部分使用者資訊。
* 登入超出 hello 應用程式的使用者。

## <a name="before-you-get-started"></a>開始之前
* 下載 hello[應用程式的基本架構](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip)或下載 hello[完成的範例](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)。
* 您也需要哪些 tooregister hello 應用程式中的 Azure AD 租用戶。 如果您還沒有 Azure AD 租用戶[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

當您準備好時，後續 hello 程序在 hello 接下來四個區段。

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>步驟 1： 使用 Azure AD 註冊 hello 新應用程式
tooset tooauthenticate hello 應用程式的使用者，第一次該租用戶中登錄執行 hello 下列：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶名稱。 在 hello**目錄**清單中，選取 hello Active Directory 租用戶想 tooregister hello 應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 請遵循 hello 提示新 toocreate **Web 應用程式和/或 WebAPI**。
  * **名稱**描述 hello 應用程式 toousers。
  * **登入 URL**是 hello hello 應用程式基底 URL。 hello 基本架構的預設 URL 為 https://localhost:44320 /。
6. Hello 註冊完成之後，Azure AD 會指派給 hello 應用程式是唯一的應用程式識別碼。 複製 hello 下一節中的 hello 應用程式頁面 toouse hello 值。
7. 從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。 hello**應用程式識別碼 URI**是 hello 應用程式的唯一識別碼。 hello 命名慣例是`https://<tenant-domain>/<app-name>`(例如， `https://contoso.onmicrosoft.com/my-first-aad-app`)。

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>步驟 2： 設定 hello 應用程式 toouse hello OWIN 驗證管線
在此步驟中，您可以設定 hello OWIN 中介軟體 toouse hello OpenID Connect 驗證通訊協定。 您使用 OWIN tooissue 登入和登出要求、 管理使用者工作階段、 取得使用者資訊等等。

1. toobegin，利用 hello Package Manager Console 中新增 hello OWIN 中介軟體 NuGet 封裝 toohello 專案。

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. OWIN 啟動 「 類別 toohello 專案呼叫的 tooadd `Startup.cs`hello 專案上按一下滑鼠右鍵、 選取**新增**，選取**新項目**，然後搜尋**OWIN**。 hello OWIN 中介軟體會叫用 hello **Configuration(...)** hello 應用程式啟動時的方法。
3. 也變更 hello 類別宣告`public partial class Startup`。 我們已在另一個檔案中為您實作此類別的一部分。 在 hello **Configuration(...)**方法，呼叫太**ConfgureAuth(...)** tooset hello 應用程式的驗證設定。  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. 開啟 hello App_Start\Startup.Auth.cs 檔案，並接著實作 hello **ConfigureAuth(...)**方法。 hello 的參數中提供*OpenIDConnectAuthenticationOptions*做為 hello 與 Azure AD 的應用程式 toocommunicate 座標。 您也需要 tooset 出的 cookie 驗證，因為 hello OpenID Connect 中介軟體 hello 背景中使用 cookie。

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. Hello hello 專案根目錄中開啟 hello web.config 檔案，然後輸入 hello 中的 hello 組態值`<appSettings>`> 一節。
  * `ida:ClientId`: hello GUID hello 從複製在 Azure 入口網站 」 步驟 1： 註冊 hello 新應用程式與 Azure AD。 」
  * `ida:Tenant`: hello 名稱，您的 Azure AD 租用戶 (例如 contoso.onmicrosoft.com)。
  * `ida:PostLogoutRedirectUri`: hello 指標，會告訴 Azure AD，使用者應該重新導向之後登出要求順利完成。

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>步驟 3： 使用 OWIN tooissue 登入和登出要求 tooAzure AD
hello 應用程式是現在已正確設定的 toocommunicate 與 Azure AD 使用 hello OpenID Connect 的驗證通訊協定。 OWIN 已經處理過所有 hello 製作驗證訊息、 驗證 Azure ad 的權杖和維護使用者工作階段的詳細資料。 所有會維持為您的使用者是 toogive 方式 toosign 中的並登出。

1. 您可以使用存取特定網頁前授權在您控制站 toorequire 使用者 toosign 中的標記。 toodo，開啟 Controllers\HomeController.cs，，然後加入 hello`[Authorize]`標記 toohello 有關控制站。

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. 您也可以在程式碼中使用從 OWIN toodirectly 發出驗證要求。 toodo，請開啟 Controllers\AccountController.cs。 然後，在 hello SignIn() 和 Signout 動作，會發出 OpenID Connect 的挑戰和登出要求。

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. 開啟 _layout.cshtml\_LoginPartial.cshtml tooshow hello 使用者 hello 應用程式登入和登出連結和 tooprint 出檢視中的 hello 使用者的名稱。

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a>步驟 4：顯示使用者資訊
它會驗證使用者使用 OpenID Connect，Azure AD 會傳回 id_token toohello 應用程式包含 「 宣告 」 或有關 hello 使用者判斷提示。 您可以使用這些宣告 toopersonalize hello 應用程式執行 hello 下列動作：

1. 開啟 hello Controllers\HomeController.cs 檔案。 您可以在 hello 透過您控制站存取 hello 使用者宣告`ClaimsPrincipal.Current`安全性主體物件。

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. 建置並執行 hello 應用程式。 如果您尚未使用 onmicrosoft.com 網域的租用戶中建立新的使用者，現在是 hello 時間 toodo 因此。 方式如下：

  a. 使用該使用者登入，並請注意如何 hello 使用者的身分識別會反映在 hello 頂端列。

  b. 登出，然後在您的租用戶中以另一個使用者身分登入。

  c. 如果想再多進行一些操作，您還可以註冊並執行此應用程式的另一個執行個體 (使用其自己的 clientId)，然後監看單一登入的運作情況。

## <a name="next-steps"></a>後續步驟
如需參考，請參閱[hello 完成範例](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)（不含您的組態值）。

您現在可以繼續 toomore 進階主題。 例如，嘗試[使用 Azure AD 來保護 Web API](active-directory-devquickstarts-webapi-dotnet.md)。

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
