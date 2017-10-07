---
title: "Active Directory B2C aaaAzure |Microsoft 文件"
description: "如何 toobuild.NET Web 應用程式和呼叫 web api 使用 Azure Active Directory B2C 和 OAuth 2.0 存取權杖。"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C：從 .NET Web 應用程式呼叫 .NET Web API

藉由使用 Azure AD B2C，您可以加入功能強大的身分識別管理功能 tooyour web 應用程式和 web Api。 本文將告訴您如何 toorequest 存取權杖和進行呼叫，從 「 待辦事項清單 」 的.NET web 應用程式 tooa.NET web 應用程式開發介面。

本文並未涵蓋如何 tooimplement 登入、 註冊和使用 Azure AD B2C 管理設定檔。 它著重在呼叫 web Api 之後 hello 使用者已經過驗證。 如果您尚未執行此動作，您應該：

* 開始使用 [.NET Web 應用程式](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* 開始使用 [.NET Web API](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>必要條件

toobuild web 應用程式呼叫 web api，您需要：

1. [建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。
2. [註冊 Web API](active-directory-b2c-app-registration.md#register-a-web-api)。
3. [註冊 Web 應用程式](active-directory-b2c-app-registration.md#register-a-web-app)。
4. [設定原則](active-directory-b2c-reference-policies.md)。
5. [授與 hello web 應用程式的權限 toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions)。

> [!IMPORTANT]
> hello 用戶端應用程式和 web API 必須使用 hello 相同的 Azure AD B2C 目錄。
>

## <a name="download-hello-code"></a>下載 hello 程式碼

本教學課程中的 hello 程式碼維護在[GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)。 您可以藉由執行複製 hello 範例：

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。 hello 方案檔包含兩個專案：`TaskWebApp`和`TaskService`。 `TaskWebApp`是 hello 使用者 MVC web 應用程式互動。 `TaskService`是 hello 應用程式後端 web API，儲存每個使用者的待辦事項清單。 這份文件未涵蓋關於建立 hello `TaskWebApp` web 應用程式或 hello `TaskService` web api。 toolearn 如何 toobuild hello.NET web 應用程式使用 Azure AD B2C，請參閱我們[.NET web 應用程式教學課程](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。 請參閱的 toolearn toobuild hello.NET web 應用程式開發介面使用 Azure AD B2C，保護我們[.NET web API 教學課程](active-directory-b2c-devquickstarts-api-dotnet.md)。

### <a name="update-hello-azure-ad-b2c-configuration"></a>更新 Azure AD B2C hello 組態

我們的範例是設定的 toouse hello 原則和用戶端識別碼我們示範租用戶。 如果您想要 toouse 自己的租用戶：

1. 開啟`web.config`在 hello`TaskService`專案和 hello 值取代

    * `ida:Tenant`：使用您的租用戶名稱
    * `ida:ClientId`：使用您的 Web API 應用程式識別碼
    * `ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱

2. 開啟`web.config`在 hello`TaskWebApp`專案和 hello 值取代

    * `ida:Tenant`：使用您的租用戶名稱
    * `ida:ClientId`：使用您的 Web 應用程式識別碼
    * `ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰
    * `ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱
    * `ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱
    * `ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱



## <a name="requesting-and-saving-an-access-token"></a>要求及儲存存取權杖

### <a name="specify-hello-permissions"></a>指定 hello 權限

順序 toomake hello 呼叫 toohello web API 中，您需要 tooauthenticate hello 使用者 （使用您 sign-up/登入的原則） 和[接收存取權杖](active-directory-b2c-access-tokens.md)從 Azure AD B2C。 在順序 tooreceive 存取權杖，您必須先指定您想要 hello 存取語彙基元 toogrant hello 權限。 hello 權限會指定在 hello`scope`參數，當您進行 hello 要求 toohello`/authorize`端點。 比方說，存取權杖以 hello 的 「 讀取 」 權限 toohello 資源應用程式具有 tooacquire hello 應用程式識別碼 URI `https://contoso.onmicrosoft.com/tasks`，hello 範圍會`https://contoso.onmicrosoft.com/tasks/read`。

在我們的範例，請開啟 hello 檔 toospecify hello 範圍`App_Start\Startup.Auth.cs`並定義 hello `Scope` OpenIdConnectAuthenticationOptions 中的變數。

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>交換存取權杖的 hello 授權碼

使用者完成 hello 註冊或登入體驗之後，您的應用程式就會從 Azure AD B2C 收到授權碼。 hello OWIN OpenID Connect 中介軟體會儲存 hello 程式碼，但不是將其交換存取權杖。 您可以使用 hello [MSAL 文件庫](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)toomake hello exchange。 在我們的範例中，我們設定通知回撥到 hello OpenID Connect 中介軟體時收到授權碼。 Hello 回呼中我們會使用語彙基元的 MSAL tooexchange hello 程式碼，以及儲存至 hello 快取的 hello 語彙基元。

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a>呼叫 hello web API

本章節將討論如何在收到 toouse hello token sign-up/使用登入 Azure AD B2C 順序 tooaccess hello web API。

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>擷取儲存的 hello 權杖 hello 控制站

hello`TasksController`負責與 hello web API 進行通訊及傳送 HTTP 要求 toohello API tooread，建立及刪除的工作。 Hello 應用程式開發介面由 Azure AD B2C 受保護，所以您會需要您在 hello 上述步驟中儲存的 toofirst 擷取 hello 語彙基元。

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a>讀取 hello web API 中的工作

當您有語彙基元時，您可以將它附加 toohello HTTP `GET` hello 中的要求`Authorization`標頭 toosecurely 呼叫`TaskService`:

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a>建立及刪除 hello web 應用程式開發介面上的工作

後續相同模式時您所傳送的 hello`POST`和`DELETE`要求 toohello web API，從 hello 快取使用 MSAL tooretrieve hello 存取權杖。

## <a name="run-hello-sample-app"></a>執行 hello 範例應用程式

最後，建置並執行兩個 hello 應用程式。 註冊和登入，並建立 hello 登入的使用者進行的工作。 請登出應用程式，再以不同的使用者身分登入， 然後為該使用者建立工作。 請注意 hello 工作預存每位使用者在 hello API，因為 hello API 會從收到 hello 語彙基元擷取 hello 使用者的身分識別。 也可以嘗試播放 hello 的領域。 移除 hello 權限太 「 寫入 」，然後再次嘗試新增一項工作。 您只需要確定 toosign 每次變更 hello 範圍外。

