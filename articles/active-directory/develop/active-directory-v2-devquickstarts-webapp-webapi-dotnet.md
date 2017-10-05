---
title: "Azure AD v2.0 .NET Web 應用程式呼叫 API 入門 | Microsoft Docs"
description: "如何建置使用個人 Microsoft 帳戶以及工作或學校帳戶登入，以呼叫 Web 服務的 .NET MVC Web 應用程式。"
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="2c8be-103">從 .NET Web 應用程式呼叫 Web API</span><span class="sxs-lookup"><span data-stu-id="2c8be-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="2c8be-104">透過 v2.0 端點，您可以快速地將驗證加入 Web 應用程式和 Web API，同時支援個人 Microsoft 帳戶以及工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c8be-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="2c8be-105">我們將在此處建置 MVC Web 應用程式，借 Microsoft OWIN 中介軟體之力，使用 OpenID Connect 登入使用者。</span><span class="sxs-lookup"><span data-stu-id="2c8be-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="2c8be-106">Web 應用程式將針對 OAuth 2.0 保護的 Web API 取得 OAuth 2.0 存取權杖，以允許建立、讀取及刪除特定使用者的「待辦事項清單」。</span><span class="sxs-lookup"><span data-stu-id="2c8be-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="2c8be-107">本教學課程主要著重於使用 ADAL 來取得和使用 Web 應用程式中的存取權杖，完整說明載於[這裡](active-directory-v2-flows.md#web-apps)。</span><span class="sxs-lookup"><span data-stu-id="2c8be-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="2c8be-108">建議您先了解如何[將登入新增 Web 應用程式](active-directory-v2-devquickstarts-dotnet-web.md)，或[如何正確保護 Web API](active-directory-v2-devquickstarts-dotnet-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2c8be-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2c8be-109">v2.0 端點並非支援每個 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="2c8be-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="2c8be-110">若要判斷是否應該使用 v2.0 端點，請閱讀相關的 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="2c8be-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="2c8be-111">下載範例程式碼</span><span class="sxs-lookup"><span data-stu-id="2c8be-111">Download sample code</span></span>
<span data-ttu-id="2c8be-112">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="2c8be-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="2c8be-113">若要遵循執行，您可以 [用 .zip 格式下載應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) ，或複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="2c8be-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="2c8be-114">或者，您可以 [將已完成的應用程式下載為 .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ，或複製已完成的應用程式：</span><span class="sxs-lookup"><span data-stu-id="2c8be-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="2c8be-115">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="2c8be-115">Register an app</span></span>
<span data-ttu-id="2c8be-116">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="2c8be-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="2c8be-117">請確定：</span><span class="sxs-lookup"><span data-stu-id="2c8be-117">Make sure to:</span></span>

* <span data-ttu-id="2c8be-118">將指派給您應用程式的 **應用程式識別碼** 複製起來，您很快會需要用到這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="2c8be-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="2c8be-119">建立**密碼**類型的**應用程式祕密**，並複製其值以備後用</span><span class="sxs-lookup"><span data-stu-id="2c8be-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="2c8be-120">為您的應用程式新增 **Web** 平台。</span><span class="sxs-lookup"><span data-stu-id="2c8be-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="2c8be-121">輸入正確的 **重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="2c8be-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="2c8be-122">重新導向 URI 會向 Azure AD 指出驗證回應應導向的位置，本教學課程的預設為 `https://localhost:44326/`。</span><span class="sxs-lookup"><span data-stu-id="2c8be-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="2c8be-123">安裝 OWIN</span><span class="sxs-lookup"><span data-stu-id="2c8be-123">Install OWIN</span></span>
<span data-ttu-id="2c8be-124">請使用封裝管理員主控台，將 OWIN 中介軟體 NuGet 封裝加入 `TodoList-WebApp` 專案。</span><span class="sxs-lookup"><span data-stu-id="2c8be-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="2c8be-125">OWIN 中介軟體將用來發出登入和登出要求、管理使用者的工作階段，以及取得使用者相關資訊等其他作業。</span><span class="sxs-lookup"><span data-stu-id="2c8be-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="2c8be-126">登入使用者</span><span class="sxs-lookup"><span data-stu-id="2c8be-126">Sign the user in</span></span>
<span data-ttu-id="2c8be-127">現在設定 OWIN 中介軟體來使用 [OpenID Connect 驗證通訊協定](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="2c8be-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="2c8be-128">開啟 `TodoList-WebApp` 專案根目錄中的 `web.config` 檔案，並在 `<appSettings>` 區段中輸入應用程式的組態值。</span><span class="sxs-lookup"><span data-stu-id="2c8be-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="2c8be-129">`ida:ClientId` 是在註冊入口網站中指派給應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="2c8be-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="2c8be-130">`ida:ClientSecret` 是您在註冊入口網站中建立的 **應用程式密碼** 。</span><span class="sxs-lookup"><span data-stu-id="2c8be-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="2c8be-131">`ida:RedirectUri` 是您在入口網站中輸入的 **重新導向 URI** 。</span><span class="sxs-lookup"><span data-stu-id="2c8be-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="2c8be-132">開啟 `TodoList-Service` 專案根目錄中的 `web.config` 檔案，並以與上述相同的**應用程式 ID** 取代 `ida:Audience`。</span><span class="sxs-lookup"><span data-stu-id="2c8be-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="2c8be-133">開啟檔案 `App_Start\Startup.Auth.cs`，並加入上述程式庫的 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="2c8be-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="2c8be-134">在相同檔案中實作 `ConfigureAuth(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="2c8be-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="2c8be-135">您在 `OpenIDConnectAuthenticationOptions` 中所提供的參數將會做為您的應用程式與 Azure AD 進行通訊的座標使用。</span><span class="sxs-lookup"><span data-stu-id="2c8be-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="2c8be-136">使用 MSAL 取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="2c8be-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="2c8be-137">在 `AuthorizationCodeReceived` 通知中，我們想要使用與 [OpenID Connect 串聯的 OAuth 2.0](active-directory-v2-protocols.md)，以兌換待辦事項清單服務之存取權杖的 authorization_code。</span><span class="sxs-lookup"><span data-stu-id="2c8be-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="2c8be-138">MSAL 可為您簡化這個程序：</span><span class="sxs-lookup"><span data-stu-id="2c8be-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="2c8be-139">首先，安裝 MSAL 預覽版本：</span><span class="sxs-lookup"><span data-stu-id="2c8be-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="2c8be-140">並針對 MSAL，將另一個 `using` 陳述式新增到 `App_Start\Startup.Auth.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="2c8be-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="2c8be-141">現在，新增一個名為 `OnAuthorizationCodeReceived` 的事件處理常式方法。</span><span class="sxs-lookup"><span data-stu-id="2c8be-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="2c8be-142">此處理常式會使用 MSAL 取得待辦事項清單 API 的存取權杖，並將 MSAL 權杖中的權杖儲存起來以供日後使用：</span><span class="sxs-lookup"><span data-stu-id="2c8be-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="2c8be-143">在 Web Apps 中，MSAL 具有可延伸的權杖快取，可以用來儲存權杖。</span><span class="sxs-lookup"><span data-stu-id="2c8be-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="2c8be-144">這個範例會實作使用 http 工作階段存放區來快取權杖的 `NaiveSessionCache` 。</span><span class="sxs-lookup"><span data-stu-id="2c8be-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="2c8be-145">呼叫 Web API</span><span class="sxs-lookup"><span data-stu-id="2c8be-145">Call the Web API</span></span>
<span data-ttu-id="2c8be-146">現在可以實際使用您在步驟 3 中取得的 access_token。</span><span class="sxs-lookup"><span data-stu-id="2c8be-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="2c8be-147">開啟 Web 應用程式的 `Controllers\TodoListController.cs` 檔案，此檔案可向待辦事項清單 API 提出所有 CRUD 請求。</span><span class="sxs-lookup"><span data-stu-id="2c8be-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="2c8be-148">這裡可再次使用 MSAL，從 MSAL 快取擷取 access_tokens。</span><span class="sxs-lookup"><span data-stu-id="2c8be-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="2c8be-149">首先，將 MSAL 的 `using` 陳述式新增至這個檔案。</span><span class="sxs-lookup"><span data-stu-id="2c8be-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="2c8be-150">在 `Index` 動作中，使用 MSAL 的 `AcquireTokenSilentAsync` 方法取得可用來讀取待辦事項清單服務資料的 access_token：</span><span class="sxs-lookup"><span data-stu-id="2c8be-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="2c8be-151">此範例接下來會將產生的權杖加入 HTTP GET 要求當做 `Authorization` 標頭，讓待辦事項清單服務用來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="2c8be-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="2c8be-152">如果待辦事項清單服務傳回 `401 Unauthorized` 回應，表示 MSAL 的 access_tokens 已因為某些原因而無效。</span><span class="sxs-lookup"><span data-stu-id="2c8be-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="2c8be-153">在此情況下，您應該卸除所有來自 MSAL 快取的 access_tokens，並向使用者顯示訊息告知可能需要再次登入，而這會重新啟動權杖的取得流程。</span><span class="sxs-lookup"><span data-stu-id="2c8be-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="2c8be-154">同樣地，如果 MSAL 因為任何原因而無法傳回 access_token，您也應指示使用者再次登入。</span><span class="sxs-lookup"><span data-stu-id="2c8be-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="2c8be-155">這就像擷取任何 `MSALException` 一樣簡單：</span><span class="sxs-lookup"><span data-stu-id="2c8be-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="2c8be-156">`Create` 和 `Delete` 動作中執行完全一致的 `AcquireTokenSilentAsync` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="2c8be-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="2c8be-157">在 Web 應用程式中，只要應用程式有需要，就可以使用這個 MSAL 方法取得 access_tokens。</span><span class="sxs-lookup"><span data-stu-id="2c8be-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="2c8be-158">MSAL 會為您取得、快取和重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="2c8be-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="2c8be-159">最後，建置並執行您的應用程式！</span><span class="sxs-lookup"><span data-stu-id="2c8be-159">Finally, build and run your app!</span></span>  <span data-ttu-id="2c8be-160">使用 Microsoft 帳戶或 Azure AD 帳戶登入，並注意上方導覽列中的使用者身分識別的反映狀態。</span><span class="sxs-lookup"><span data-stu-id="2c8be-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="2c8be-161">在使用者的 [待辦事項清單] 中加入和刪除某些項目，以查看執行中 OAuth 2.0 保護的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="2c8be-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="2c8be-162">您的 Web 應用程式和 Web API 現在都使用業界標準的通訊協定保護，可以使用個人與工作/學校帳戶來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="2c8be-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="2c8be-163">[這裡提供](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip)完整的範例供您參考 (不含您的設定值)。</span><span class="sxs-lookup"><span data-stu-id="2c8be-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="2c8be-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c8be-164">Next Steps</span></span>
<span data-ttu-id="2c8be-165">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="2c8be-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="2c8be-166">v2.0 開發人員指南 >></span><span class="sxs-lookup"><span data-stu-id="2c8be-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="2c8be-167">StackOverflow "azure-active-directory" 標籤 >></span><span class="sxs-lookup"><span data-stu-id="2c8be-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="2c8be-168">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="2c8be-168">Get security updates for our products</span></span>
<span data-ttu-id="2c8be-169">我們鼓勵您造訪 [此頁面](https://technet.microsoft.com/security/dd252948) 並訂閱資訊安全摘要報告警示，以在安全性事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="2c8be-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

