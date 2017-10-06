---
title: "Active Directory B2C aaaAzure |Microsoft 文件"
description: "如何 toobuild sign-up/登入、 具有 web 應用程式設定檔編輯及使用 Azure Active Directory B2C 重設密碼。"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>建立支援 Azure Active Directory B2C 註冊、登入、設定檔編輯及密碼重設的 ASP.NET Web 應用程式

本教學課程說明如何：

> [!div class="checklist"]
> * 新增 Azure AD B2C 身分識別功能 tooyour web 應用程式
> * 在您的 Azure AD B2C 目錄中註冊 Web 應用程式
> * 為您的 Web 應用程式建立使用者註冊/登入、編輯設定檔和密碼重設原則

## <a name="prerequisites"></a>必要條件

- 您必須連接您 B2C 租用戶 tooan Azure 帳戶。 您可以在[這裡](https://azure.microsoft.com/en-us/)建立免費的 Azure 帳戶。
- 您需要[Microsoft Visual Studio](https://www.visualstudio.com/)或類似的程式 tooview 和修改 hello 範例程式碼。

## <a name="create-an-azure-ad-b2c-directory"></a>建立 Azure AD B2C 目錄

您必須先建立目錄或租用戶，才可使用 Azure AD B2C。 目錄就是您所有使用者、應用程式、群組等項目的容器。 如果您還沒有此資源，請先建立 B2C 目錄，再繼續進行本指南。

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> 您需要 tooconnect hello B2C 租用戶 tooyour Azure 訂用帳戶。 選取之後**建立**，選取 hello**連結現有的 Azure AD B2C 租用戶 toomy Azure 訂用帳戶**選項，然後在 hello **Azure AD B2C 租用戶**下拉式清單中，選取您想要 tooassociate hello 租用戶。

## <a name="create-and-register-an-application"></a>建立並註冊應用程式

接下來，您需要 toocreate 和 B2C 目錄中註冊 hello 應用程式。 這會提供 Azure AD B2C 需要 toosecurely 資訊與您的應用程式通訊。 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

完成後，您的應用程式設定中會有 API 與原生應用程式。

## <a name="create-policies-on-your-b2c-tenant"></a>在 B2C 租用戶上建立原則

在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。 此程式碼範例包含三種身分識別體驗：**註冊和登入**、**設定檔編輯**和**密碼重設**。  Hello 中所述，您會需要 toocreate 一個原則的每個類型，[原則參考文件](active-directory-b2c-reference-policies.md)。 每個原則，是原則的確定 tooselect hello 顯示名稱屬性或宣告，以及 toocopy 下 hello 中的名稱以供稍後使用。

### <a name="add-your-identity-providers"></a>新增識別提供者

從您的設定中，選取 [識別提供者]，然後選擇 [使用者名稱註冊] 或 [電子郵件註冊]。

### <a name="create-a-sign-up-and-sign-in-policy"></a>建立註冊與登入原則

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>建立設定檔編輯原則

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>建立密碼重設原則

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

建立您的原則之後，您便準備好 toobuild 您的應用程式。

## <a name="download-hello-sample-code"></a>下載 hello 範例程式碼

本教學課程中的 hello 程式碼維護在[GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)。 您可以藉由執行複製 hello 範例：

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。 hello 方案檔包含兩個專案：`TaskWebApp`和`TaskService`。 `TaskWebApp`是 hello hello 使用者的 MVC web 應用程式互動。 `TaskService`是 hello 應用程式後端 web API，儲存每個使用者的待辦事項清單。 本文將只會討論 hello`TaskWebApp`應用程式。 toolearn 如何 toobuild`TaskService`使用 Azure AD B2C，請參閱[我們.NET web api 教學課程](active-directory-b2c-devquickstarts-api-dotnet.md)。

## <a name="update-code-toouse-your-tenant-and-policies"></a>更新程式碼 toouse 租用戶和原則

我們的範例是設定的 toouse hello 原則和用戶端識別碼我們示範租用戶。 tooconnect 它 tooyour 自己的租用戶，您需要 tooopen`web.config`在 hello`TaskWebApp`專案，並取代 hello 下列值：

* `ida:Tenant`：使用您的租用戶名稱
* `ida:ClientId`：使用您的 Web 應用程式識別碼
* `ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰
* `ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱
* `ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱
* `ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱

## <a name="launch-hello-app"></a>啟動 hello 應用程式
從 Visual Studio 內啟動 hello 應用程式。 瀏覽 toohello 待辦事項清單] 索引標籤，然後注意 hello URl 是： https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id =*YourclientID*...

註冊 hello 應用程式使用您的電子郵件地址或使用者名稱。 登出，然後再次登入並編輯 hello 設定檔或 hello 密碼重設。 請登出應用程式，再以不同的使用者身分登入， 

## <a name="add-social-idps"></a>新增社交 IDP

目前，hello 應用程式支援使用只有使用者註冊和登入**本機帳戶**; B2C 目錄中儲存的帳戶，使用使用者名稱和密碼。 藉由使用 Azure AD B2C，您可以新增對其他 **身分識別提供者** (IDP) 的支援，但不需變更任何程式碼。

tooadd 社交 IDPs tooyour 應用程式中，遵循開始 hello 詳細這些文章中的指示。 針對每個 IDP 想 toosupport，您必須在該系統 tooregister 應用程式，並取得用戶端識別碼。

* [將 Facebook 設定為 IDP](active-directory-b2c-setup-fb-app.md)
* [將 Google 設定為 IDP](active-directory-b2c-setup-goog-app.md)
* [將 Amazon 設定為 IDP](active-directory-b2c-setup-amzn-app.md)
* [將 LinkedIn 設定為 IDP](active-directory-b2c-setup-li-app.md)

您將加入之後 hello 身分識別提供者 tooyour B2C 目錄中，編輯每個有三個原則 tooinclude hello 新 IDPs，hello 中所述[原則參考文件](active-directory-b2c-reference-policies.md)。 儲存您的原則之後，請再次執行 hello 應用程式。  您應該會看到新 IDPs 加入為登入並註冊選項，在每個身分識別體驗中的 hello。

您可以試驗您的原則，並觀察 hello 範例應用程式上的效果。 新增或移除 IDP、管理應用程式宣告，或變更註冊屬性。 試驗到您能夠了解原則、驗證要求和 OWIN 如何結合在一起為止。

## <a name="sample-code-walkthrough"></a>範例程式碼逐步解說
下列各節的 hello 顯示 hello 範例應用程式程式碼的設定方式。 您日後開發應用程式時，可以將此程式碼當作指引。

### <a name="add-authentication-support"></a>新增驗證支援

您現在可以設定您的應用程式 toouse Azure AD B2C。 您的應用程式會藉由傳送 OpenID Connect 驗證要求，來與 Azure AD B2C 通訊。 hello 要求聽寫 hello 使用者體驗您的應用程式想 tooexecute 藉由指定 hello 原則。 您可以使用 Microsoft 的 OWIN 程式庫 toosend 這些要求，執行原則、 管理使用者工作階段，等等。

#### <a name="install-owin"></a>安裝 OWIN

toobegin，使用 Visual Studio Package Manager Console hello 新增 hello OWIN 中介軟體 NuGet 封裝 toohello 專案。

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>新增 OWIN 啟動類別

新增 OWIN 啟動類別 toohello API 呼叫`Startup.cs`。  以滑鼠右鍵按一下 hello 專案、 選取**新增**和**新項目**，然後搜尋 OWIN。 hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。

在我們的範例中，我們變更 hello 類別宣告太`public partial class Startup`和實作 hello hello 類別中的其他部分`App_Start\Startup.Auth.cs`。 內部 hello`Configuration`方法中，我們加入呼叫太`ConfigureAuth`，定義在`Startup.Auth.cs`。 Hello 修改之後`Startup.cs`看起來像 hello 面：

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>設定 hello 驗證中介軟體

開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(...)`方法。 hello 的參數中提供`OpenIdConnectAuthenticationOptions`做為您的應用程式 toocommunicate 與 Azure AD B2C 的座標。 如果您未指定特定參數，它會使用 hello 預設值。 例如，我們不指定 hello`ResponseType`在 hello 範例中，因此 hello 預設值`code id_token`將用於每個外寄要求 tooAzure AD B2C 中。

您也需要設定的 cookie 驗證 tooset。 hello OpenID Connect 中介軟體會使用 cookie toomaintain 使用者工作階段，以及其他項目。

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

在`OpenIdConnectAuthenticationOptions`以上版本，我們會定義一組特定 hello OpenID Connect 中介軟體所收到的通知的回呼函式。 這些行為透過定義`OpenIdConnectAuthenticationNotifications`物件，並儲存到 hello`Notifications`變數。 在我們的範例中，我們會定義三個不同的回呼，視 hello 事件而定。

### <a name="using-different-policies"></a>使用不同的原則

hello`RedirectToIdentityProvider`通知時會觸發 tooAzure AD B2C 提出要求。 在 [hello 回呼函式`OnRedirectToIdentityProvider`，我們會檢查在傳出呼叫，如果我們想要 toouse hello 不同的原則。 在密碼重設或編輯設定檔的順序 toodo，您需要 toouse hello 對應原則，例如 hello 密碼重設原則，而不是 hello 預設 「 註冊或登入 」 原則。

在我們的範例中，當使用者想 tooreset hello 密碼，或編輯 hello 設定檔，我們會加入 hello 原則我們偏好 toouse 到 hello OWIN 內容。 您可以藉由 hello 下列來完成：

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

您可以實作 hello 回呼函式和`OnRedirectToIdentityProvider`執行 hello 下列動作：

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>處理授權碼

hello`AuthorizationCodeReceived`通知收到授權碼時觸發。 hello OpenID Connect 中介軟體不支援交換代碼的存取權杖。 您可以手動交換 hello hello 語彙基元中的回呼函式的程式碼。 如需詳細資訊，請查看 hello[文件](active-directory-b2c-devquickstarts-web-api-dotnet.md)，說明如何。

### <a name="handling-errors"></a>處理錯誤

hello`AuthenticationFailed`驗證失敗時，會觸發通知。 回呼方法時，您可以處理 hello 錯誤，在您希望的位置。 不過，您應該加入 hello 錯誤碼檢查`AADB2C90118`。 Hello hello 「 註冊或登入 」 的原則執行期間 hello 使用者擁有 hello 機會 tooselect**忘記密碼？**連結。 在此情況下，Azure AD B2C 傳送您的應用程式的錯誤代碼，表示您的應用程式應該要改用 hello 密碼重設原則的要求。

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>傳送驗證要求 tooAzure AD

您的應用程式是現在已正確設定與 Azure AD B2C toocommunicate 使用 hello OpenID Connect 的驗證通訊協定。 OWIN 管理 hello 製作驗證訊息，驗證來自 Azure AD B2C，語彙基元和維護使用者工作階段的詳細的資料。 所有仍然是 tooinitiate 每位使用者的流量。

當使用者選取**登向上/登入**，**編輯設定檔**，或**重設密碼**hello web 應用程式，在相關聯的 hello 叫用動作中`Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

您也可以使用 OWIN toosign 出 hello 從 hello 應用程式的使用者。 在 `Controllers\AccountController.cs` 中，我們有︰

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

在加法 tooexplicitly 叫用原則，您可以使用`[Authorize]`標記中的控制站執行原則，如果 hello 使用者未登入。 開啟`Controllers\HomeController.cs`和新增 hello`[Authorize]`標記 toohello 宣告控制站。  OWIN 選取 hello 上次原則設定時 hello`[Authorize]`叫用標記。

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>顯示使用者資訊

當您使用 OpenID Connect 來驗證使用者時，Azure AD B2C 傳回識別碼權杖 toohello 應用程式，其中包含**宣告**。 這些是 hello 使用者判斷提示。 您可以使用宣告 toopersonalize 您的應用程式。

開啟 hello`Controllers\HomeController.cs`檔案。 您可以在 hello 透過您控制站存取使用者宣告`ClaimsPrincipal.Current`安全性主體物件。

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

您可以存取任何宣告，您的應用程式收到 hello 中相同的方式。  收到 hello 應用程式的所有 hello 宣告的清單是可供您在 hello**宣告**頁面。
