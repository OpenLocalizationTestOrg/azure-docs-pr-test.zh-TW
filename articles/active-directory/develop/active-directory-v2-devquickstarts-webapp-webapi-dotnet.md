---
title: "aaaAzure AD v2.0.NET web 應用程式呼叫 API 開始使用 |Microsoft 文件"
description: "Toobuild.NET MVC Web 應用程式呼叫 web 服務使用個人 Microsoft 帳戶和工作或學校帳戶登入。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="9fae3-103">從 .NET Web 應用程式呼叫 Web API</span><span class="sxs-lookup"><span data-stu-id="9fae3-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="9fae3-104">Hello v2.0 端點，您可以快速新增驗證 tooyour web 應用程式與 web 應用程式開發介面支援這兩個個人 Microsoft 帳戶與工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="9fae3-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="9fae3-105">我們將在此處建置 MVC Web 應用程式，借 Microsoft OWIN 中介軟體之力，使用 OpenID Connect 登入使用者。</span><span class="sxs-lookup"><span data-stu-id="9fae3-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="9fae3-106">hello web 應用程式會取得 OAuth 2.0 存取權杖的 web 應用程式開發介面所允許的 OAuth 2.0 保護建立、 讀取和刪除上一個指定的使用者的 「 待辦事項清單 」。</span><span class="sxs-lookup"><span data-stu-id="9fae3-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="9fae3-107">本教學課程將主要著重在使用 MSAL tooacquire 並描述完整的 web 應用程式中使用存取權杖[這裡](active-directory-v2-flows.md#web-apps)。</span><span class="sxs-lookup"><span data-stu-id="9fae3-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="9fae3-108">做為必要條件，您可能想 toofirst 深入了解如何太[新增登入 tooa 基本 web 應用程式](active-directory-v2-devquickstarts-dotnet-web.md)或如何太[正確保護 webApi</](active-directory-v2-devquickstarts-dotnet-api.md)。</span><span class="sxs-lookup"><span data-stu-id="9fae3-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9fae3-109">並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="9fae3-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="9fae3-110">toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="9fae3-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="9fae3-111">下載範例程式碼</span><span class="sxs-lookup"><span data-stu-id="9fae3-111">Download sample code</span></span>
<span data-ttu-id="9fae3-112">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="9fae3-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="9fae3-113">您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip)或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="9fae3-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="9fae3-114">或者，您可以[下載為.zip 的 hello 完成應用程式](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip)或再製 hello 完成應用程式：</span><span class="sxs-lookup"><span data-stu-id="9fae3-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="9fae3-115">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="9fae3-115">Register an app</span></span>
<span data-ttu-id="9fae3-116">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="9fae3-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9fae3-117">請確定：</span><span class="sxs-lookup"><span data-stu-id="9fae3-117">Make sure to:</span></span>

* <span data-ttu-id="9fae3-118">複製下 hello**應用程式識別碼**指派 tooyour 應用程式，您將需要它過期。</span><span class="sxs-lookup"><span data-stu-id="9fae3-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="9fae3-119">建立**應用程式秘鑰**的 hello**密碼**類型和清單供稍後其值的複本</span><span class="sxs-lookup"><span data-stu-id="9fae3-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="9fae3-120">新增 hello **Web**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9fae3-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="9fae3-121">輸入正確的 hello**重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="9fae3-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="9fae3-122">hello 重新導向 uri 表示的 tooAzure AD 其中應該導向驗證回應-此教學課程中的 hello 預設為`https://localhost:44326/`。</span><span class="sxs-lookup"><span data-stu-id="9fae3-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="9fae3-123">安裝 OWIN</span><span class="sxs-lookup"><span data-stu-id="9fae3-123">Install OWIN</span></span>
<span data-ttu-id="9fae3-124">新增 hello OWIN 中介軟體的 NuGet 封裝 toohello`TodoList-WebApp`專案使用 hello Package Manager Console。</span><span class="sxs-lookup"><span data-stu-id="9fae3-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="9fae3-125">hello OWIN 中介軟體將會使用的 tooissue 登入和登出要求、 管理 hello 使用者工作階段，以及取得 hello 使用者，在其他項目之間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9fae3-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="9fae3-126">中的符號 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="9fae3-126">Sign hello user in</span></span>
<span data-ttu-id="9fae3-127">現在設定 hello OWIN 中介軟體 toouse hello [OpenID Connect 的驗證通訊協定](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="9fae3-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="9fae3-128">開啟 hello`web.config`檔案中的 hello hello 根`TodoList-WebApp`專案，然後輸入您的應用程式組態值在 hello `<appSettings>` > 一節。</span><span class="sxs-lookup"><span data-stu-id="9fae3-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="9fae3-129">hello`ida:ClientId`為 hello**應用程式識別碼**指派 tooyour hello 註冊入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9fae3-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="9fae3-130">hello`ida:ClientSecret`為 hello**應用程式秘鑰**hello 註冊入口網站中建立。</span><span class="sxs-lookup"><span data-stu-id="9fae3-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="9fae3-131">hello`ida:RedirectUri`為 hello**重新導向 Uri** hello 入口網站中輸入。</span><span class="sxs-lookup"><span data-stu-id="9fae3-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="9fae3-132">開啟 hello`web.config`檔案中的 hello hello 根`TodoList-Service`專案，並取代 hello`ida:Audience`與 hello 相同**應用程式識別碼**與以上所述。</span><span class="sxs-lookup"><span data-stu-id="9fae3-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="9fae3-133">開啟 hello 檔案`App_Start\Startup.Auth.cs`並加入`using`hello 上述的程式庫的陳述式。</span><span class="sxs-lookup"><span data-stu-id="9fae3-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="9fae3-134">在 hello 同一個檔案中實作 hello`ConfigureAuth(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="9fae3-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="9fae3-135">hello 的參數中提供`OpenIDConnectAuthenticationOptions`將做為您的應用程式 toocommunicate 與 Azure AD 的座標。</span><span class="sxs-lookup"><span data-stu-id="9fae3-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="9fae3-136">使用 MSAL tooget 存取權杖</span><span class="sxs-lookup"><span data-stu-id="9fae3-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="9fae3-137">在 hello`AuthorizationCodeReceived`通知，我們想要 toouse[一起使用 OpenID Connect 的 OAuth 2.0](active-directory-v2-protocols.md) tooredeem hello authorization_code 的存取語彙基元 toohello 待辦事項清單服務。</span><span class="sxs-lookup"><span data-stu-id="9fae3-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="9fae3-138">MSAL 可為您簡化這個程序：</span><span class="sxs-lookup"><span data-stu-id="9fae3-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="9fae3-139">首先，安裝 MSAL hello 預覽版本：</span><span class="sxs-lookup"><span data-stu-id="9fae3-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="9fae3-140">並加入另一個`using`陳述式 toohello `App_Start\Startup.Auth.cs` MSAL 的檔案。</span><span class="sxs-lookup"><span data-stu-id="9fae3-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="9fae3-141">現在加入新的方法，hello`OnAuthorizationCodeReceived`事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="9fae3-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="9fae3-142">這個處理常式將會使用 MSAL tooacquire 存取語彙基元 toohello 待辦事項清單應用程式開發介面，並會儲存 MSAL 的權杖快取中的 hello 語彙基元供稍後：</span><span class="sxs-lookup"><span data-stu-id="9fae3-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="9fae3-143">在 web 應用程式，MSAL 具有可延伸的權杖快取可使用的 toostore 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="9fae3-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="9fae3-144">這個範例會實作 hello`NaiveSessionCache`使用 http 工作階段儲存體 toocache 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="9fae3-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="9fae3-145">呼叫 hello Web API</span><span class="sxs-lookup"><span data-stu-id="9fae3-145">Call hello Web API</span></span>
<span data-ttu-id="9fae3-146">現在就的開始 tooactually 使用您在步驟 3 中取得的 hello access_token。</span><span class="sxs-lookup"><span data-stu-id="9fae3-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="9fae3-147">開啟 hello web 應用程式的`Controllers\TodoListController.cs`檔案中，這可讓所有 hello CRUD 要求 toohello 待辦事項清單應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="9fae3-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="9fae3-148">您可以使用 MSAL 再次從 toofetch access_tokens hello MSAL 快取此處。</span><span class="sxs-lookup"><span data-stu-id="9fae3-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="9fae3-149">首先，新增`using`MSAL toothis 檔案的陳述式。</span><span class="sxs-lookup"><span data-stu-id="9fae3-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="9fae3-150">在 hello`Index`動作，使用 MSAL`AcquireTokenSilentAsync`方法 tooget access_token 可能是使用的 tooread hello 待辦事項清單服務的資料：</span><span class="sxs-lookup"><span data-stu-id="9fae3-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="9fae3-151">hello 範例再加入 hello 產生語彙基元 toohello HTTP GET 要求做為 hello`Authorization`標頭，哪一個 hello 待辦事項清單服務會使用 tooauthenticate hello 要求。</span><span class="sxs-lookup"><span data-stu-id="9fae3-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="9fae3-152">如果 hello 待辦事項清單服務傳回`401 Unauthorized`回應 hello access_tokens MSAL 中的已經變成無效基於某些原因。</span><span class="sxs-lookup"><span data-stu-id="9fae3-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="9fae3-153">在此情況下，您應該從 hello MSAL 快取中卸除任何 access_tokens，並顯示 hello 使用者，他們可能需要 toosign 同樣地，這將會重新啟動 hello 權杖取得流程中的訊息。</span><span class="sxs-lookup"><span data-stu-id="9fae3-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* <span data-ttu-id="9fae3-154">同樣地，如果 MSAL 因故無法 tooreturn access_token，您應該再次指示中的 hello 使用者 toosign。</span><span class="sxs-lookup"><span data-stu-id="9fae3-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="9fae3-155">這就像擷取任何 `MSALException` 一樣簡單：</span><span class="sxs-lookup"><span data-stu-id="9fae3-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="9fae3-156">hello 完全相同`AcquireTokenSilentAsync`呼叫是在 hello implementd`Create`和`Delete`動作。</span><span class="sxs-lookup"><span data-stu-id="9fae3-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="9fae3-157">在 web 應用程式，您可以使用這個 MSAL 方法 tooget access_tokens，視需要在應用程式中。</span><span class="sxs-lookup"><span data-stu-id="9fae3-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="9fae3-158">MSAL 會為您取得、快取和重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="9fae3-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="9fae3-159">最後，建置並執行您的應用程式！</span><span class="sxs-lookup"><span data-stu-id="9fae3-159">Finally, build and run your app!</span></span>  <span data-ttu-id="9fae3-160">使用 Microsoft 帳戶或 Azure AD 帳戶，登入，並注意 hello 使用者的身分識別會反映在 hello 上方導覽列中的方式。</span><span class="sxs-lookup"><span data-stu-id="9fae3-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="9fae3-161">新增和刪除 toosee hello OAuth 2.0 保護 API 呼叫動作中的 hello 使用者待辦事項清單中的某些項目。</span><span class="sxs-lookup"><span data-stu-id="9fae3-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="9fae3-162">您的 Web 應用程式和 Web API 現在都使用業界標準的通訊協定保護，可以使用個人與工作/學校帳戶來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="9fae3-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="9fae3-163">如需參考，hello 完成 （不含您的組態值） 的範例[此處提供](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="9fae3-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9fae3-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9fae3-164">Next Steps</span></span>
<span data-ttu-id="9fae3-165">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9fae3-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="9fae3-166">hello v2.0 開發人員指南 >></span><span class="sxs-lookup"><span data-stu-id="9fae3-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9fae3-167">StackOverflow "azure-active-directory" 標籤 >></span><span class="sxs-lookup"><span data-stu-id="9fae3-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9fae3-168">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="9fae3-168">Get security updates for our products</span></span>
<span data-ttu-id="9fae3-169">我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。</span><span class="sxs-lookup"><span data-stu-id="9fae3-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

