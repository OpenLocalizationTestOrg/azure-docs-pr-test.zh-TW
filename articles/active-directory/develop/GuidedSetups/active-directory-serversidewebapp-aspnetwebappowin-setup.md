---
title: "aaaAzure AD v2 ASP.NET Web 伺服器快速入門-安裝 |Microsoft 文件"
description: "使用 OpenID Connect 標準，搭配傳統網頁瀏覽器型應用程式，在 ASP.NET 方案上實作 Microsoft 登入"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>設定專案

本節顯示 hello 步驟 tooinstall，並設定在 ASP.NET 專案使用 OpenID Connect hello 驗證管線透過 OWIN 中介軟體。 

> 改為偏好 toodownload 這個範例的 Visual Studio 專案嗎？ [下載專案](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip)並略過 toohello[組態步驟](#create-an-application-express)tooconfigure hello 程式碼範例，然後再執行。

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>建立 ASP.NET 專案

> 1. 在 Visual Studio 中：`File` > `New` > `Project`<br/>
> 2. 在 *Visual C#\Web* 底下，選取 `ASP.NET Web Application (.NET Framework)`。
> 3. 為您的應用程式命名並按一下 [確定]
> 4. 選取`Empty`和選取 hello 核取方塊 tooadd`MVC`參考
<!--end-collapse-->

## <a name="add-authentication-components"></a>新增驗證元件

1. 在 Visual Studio 中：`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. 新增*OWIN 中介軟體 NuGet 封裝*hello 封裝管理員主控台 視窗中輸入 hello 下列：

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>關於這些程式庫

>上述的 hello 程式庫可讓單一登入 (SSO) 使用 OpenID Connect 透過 cookie 為基礎的驗證。 在完成驗證，並代表 hello 使用者 hello token 傳送 tooyour 應用程式之後，OWIN 中介軟體會建立工作階段 cookie。 hello 瀏覽器然後會使用此 cookie 在後續的要求 hello 使用者不需要 tooretype 因此其密碼，並需要任何額外的驗證。
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>設定 hello 驗證管線
使用的 toocreate OWIN 中介軟體啟動類別 tooconfigure OpenID Connect 驗證，則 hello 步驟。 此類別將會在您的 IIS 處理序啟動時自動執行。

> 如果您的專案沒有`Startup.cs`hello 根資料夾中的檔案：<br/>
> 1. Hello 專案根資料夾上按一下滑鼠右鍵： >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. 將它命名為 `Startup.cs`

> 請確定選取的 hello 類別 OWIN 啟動類別而不是標準 C# 類別。 確認此檢查，如果您看到`[assembly: OwinStartup(typeof({NameSpace}.Startup))]`上方 hello 命名空間。


1. 新增*OWIN*和*Microsoft.IdentityModel*太參考`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
啟動類別取代為下列程式碼 hello:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>相關資訊

> hello 的參數中提供*OpenIDConnectAuthenticationOptions*做為 hello 與 Azure AD 的應用程式 toocommunicate 座標。 由於 hello OpenID Connect 中介軟體會使用 cookie hello 背景中，您也需要 tooset 出的 cookie 驗證 hello 上方顯示的程式碼。 hello *ValidateIssuer*值會告訴 OpenIdConnect toonot 限制存取 tooone 特定組織。
<!--end-collapse-->

