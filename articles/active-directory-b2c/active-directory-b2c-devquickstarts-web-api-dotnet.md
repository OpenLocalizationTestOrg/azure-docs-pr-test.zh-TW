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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="801bc-103">Azure AD B2C：從 .NET Web 應用程式呼叫 .NET Web API</span><span class="sxs-lookup"><span data-stu-id="801bc-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="801bc-104">藉由使用 Azure AD B2C，您可以加入功能強大的身分識別管理功能 tooyour web 應用程式和 web Api。</span><span class="sxs-lookup"><span data-stu-id="801bc-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="801bc-105">本文將告訴您如何 toorequest 存取權杖和進行呼叫，從 「 待辦事項清單 」 的.NET web 應用程式 tooa.NET web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="801bc-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="801bc-106">本文並未涵蓋如何 tooimplement 登入、 註冊和使用 Azure AD B2C 管理設定檔。</span><span class="sxs-lookup"><span data-stu-id="801bc-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="801bc-107">它著重在呼叫 web Api 之後 hello 使用者已經過驗證。</span><span class="sxs-lookup"><span data-stu-id="801bc-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="801bc-108">如果您尚未執行此動作，您應該：</span><span class="sxs-lookup"><span data-stu-id="801bc-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="801bc-109">開始使用 [.NET Web 應用程式](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="801bc-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="801bc-110">開始使用 [.NET Web API](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="801bc-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="801bc-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="801bc-111">Prerequisite</span></span>

<span data-ttu-id="801bc-112">toobuild web 應用程式呼叫 web api，您需要：</span><span class="sxs-lookup"><span data-stu-id="801bc-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="801bc-113">[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="801bc-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="801bc-114">[註冊 Web API](active-directory-b2c-app-registration.md#register-a-web-api)。</span><span class="sxs-lookup"><span data-stu-id="801bc-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="801bc-115">[註冊 Web 應用程式](active-directory-b2c-app-registration.md#register-a-web-app)。</span><span class="sxs-lookup"><span data-stu-id="801bc-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="801bc-116">[設定原則](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="801bc-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="801bc-117">[授與 hello web 應用程式的權限 toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions)。</span><span class="sxs-lookup"><span data-stu-id="801bc-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="801bc-118">hello 用戶端應用程式和 web API 必須使用 hello 相同的 Azure AD B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="801bc-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="801bc-119">下載 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="801bc-119">Download hello code</span></span>

<span data-ttu-id="801bc-120">本教學課程中的 hello 程式碼維護在[GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)。</span><span class="sxs-lookup"><span data-stu-id="801bc-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="801bc-121">您可以藉由執行複製 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="801bc-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="801bc-122">下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="801bc-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="801bc-123">hello 方案檔包含兩個專案：`TaskWebApp`和`TaskService`。</span><span class="sxs-lookup"><span data-stu-id="801bc-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="801bc-124">`TaskWebApp`是 hello 使用者 MVC web 應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="801bc-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="801bc-125">`TaskService`是 hello 應用程式後端 web API，儲存每個使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="801bc-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="801bc-126">這份文件未涵蓋關於建立 hello `TaskWebApp` web 應用程式或 hello `TaskService` web api。</span><span class="sxs-lookup"><span data-stu-id="801bc-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="801bc-127">toolearn 如何 toobuild hello.NET web 應用程式使用 Azure AD B2C，請參閱我們[.NET web 應用程式教學課程](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。</span><span class="sxs-lookup"><span data-stu-id="801bc-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="801bc-128">請參閱的 toolearn toobuild hello.NET web 應用程式開發介面使用 Azure AD B2C，保護我們[.NET web API 教學課程](active-directory-b2c-devquickstarts-api-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="801bc-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="801bc-129">更新 Azure AD B2C hello 組態</span><span class="sxs-lookup"><span data-stu-id="801bc-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="801bc-130">我們的範例是設定的 toouse hello 原則和用戶端識別碼我們示範租用戶。</span><span class="sxs-lookup"><span data-stu-id="801bc-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="801bc-131">如果您想要 toouse 自己的租用戶：</span><span class="sxs-lookup"><span data-stu-id="801bc-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="801bc-132">開啟`web.config`在 hello`TaskService`專案和 hello 值取代</span><span class="sxs-lookup"><span data-stu-id="801bc-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="801bc-133">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="801bc-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="801bc-134">`ida:ClientId`：使用您的 Web API 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="801bc-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="801bc-135">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="801bc-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="801bc-136">開啟`web.config`在 hello`TaskWebApp`專案和 hello 值取代</span><span class="sxs-lookup"><span data-stu-id="801bc-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="801bc-137">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="801bc-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="801bc-138">`ida:ClientId`：使用您的 Web 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="801bc-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="801bc-139">`ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="801bc-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="801bc-140">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="801bc-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="801bc-141">`ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱</span><span class="sxs-lookup"><span data-stu-id="801bc-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="801bc-142">`ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱</span><span class="sxs-lookup"><span data-stu-id="801bc-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="801bc-143">要求及儲存存取權杖</span><span class="sxs-lookup"><span data-stu-id="801bc-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="801bc-144">指定 hello 權限</span><span class="sxs-lookup"><span data-stu-id="801bc-144">Specify hello permissions</span></span>

<span data-ttu-id="801bc-145">順序 toomake hello 呼叫 toohello web API 中，您需要 tooauthenticate hello 使用者 （使用您 sign-up/登入的原則） 和[接收存取權杖](active-directory-b2c-access-tokens.md)從 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="801bc-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="801bc-146">在順序 tooreceive 存取權杖，您必須先指定您想要 hello 存取語彙基元 toogrant hello 權限。</span><span class="sxs-lookup"><span data-stu-id="801bc-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="801bc-147">hello 權限會指定在 hello`scope`參數，當您進行 hello 要求 toohello`/authorize`端點。</span><span class="sxs-lookup"><span data-stu-id="801bc-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="801bc-148">比方說，存取權杖以 hello 的 「 讀取 」 權限 toohello 資源應用程式具有 tooacquire hello 應用程式識別碼 URI `https://contoso.onmicrosoft.com/tasks`，hello 範圍會`https://contoso.onmicrosoft.com/tasks/read`。</span><span class="sxs-lookup"><span data-stu-id="801bc-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="801bc-149">在我們的範例，請開啟 hello 檔 toospecify hello 範圍`App_Start\Startup.Auth.cs`並定義 hello `Scope` OpenIdConnectAuthenticationOptions 中的變數。</span><span class="sxs-lookup"><span data-stu-id="801bc-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="801bc-150">交換存取權杖的 hello 授權碼</span><span class="sxs-lookup"><span data-stu-id="801bc-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="801bc-151">使用者完成 hello 註冊或登入體驗之後，您的應用程式就會從 Azure AD B2C 收到授權碼。</span><span class="sxs-lookup"><span data-stu-id="801bc-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="801bc-152">hello OWIN OpenID Connect 中介軟體會儲存 hello 程式碼，但不是將其交換存取權杖。</span><span class="sxs-lookup"><span data-stu-id="801bc-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="801bc-153">您可以使用 hello [MSAL 文件庫](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)toomake hello exchange。</span><span class="sxs-lookup"><span data-stu-id="801bc-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="801bc-154">在我們的範例中，我們設定通知回撥到 hello OpenID Connect 中介軟體時收到授權碼。</span><span class="sxs-lookup"><span data-stu-id="801bc-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="801bc-155">Hello 回呼中我們會使用語彙基元的 MSAL tooexchange hello 程式碼，以及儲存至 hello 快取的 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="801bc-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

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

## <a name="calling-hello-web-api"></a><span data-ttu-id="801bc-156">呼叫 hello web API</span><span class="sxs-lookup"><span data-stu-id="801bc-156">Calling hello web API</span></span>

<span data-ttu-id="801bc-157">本章節將討論如何在收到 toouse hello token sign-up/使用登入 Azure AD B2C 順序 tooaccess hello web API。</span><span class="sxs-lookup"><span data-stu-id="801bc-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="801bc-158">擷取儲存的 hello 權杖 hello 控制站</span><span class="sxs-lookup"><span data-stu-id="801bc-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="801bc-159">hello`TasksController`負責與 hello web API 進行通訊及傳送 HTTP 要求 toohello API tooread，建立及刪除的工作。</span><span class="sxs-lookup"><span data-stu-id="801bc-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="801bc-160">Hello 應用程式開發介面由 Azure AD B2C 受保護，所以您會需要您在 hello 上述步驟中儲存的 toofirst 擷取 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="801bc-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

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

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="801bc-161">讀取 hello web API 中的工作</span><span class="sxs-lookup"><span data-stu-id="801bc-161">Read tasks from hello web API</span></span>

<span data-ttu-id="801bc-162">當您有語彙基元時，您可以將它附加 toohello HTTP `GET` hello 中的要求`Authorization`標頭 toosecurely 呼叫`TaskService`:</span><span class="sxs-lookup"><span data-stu-id="801bc-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="801bc-163">建立及刪除 hello web 應用程式開發介面上的工作</span><span class="sxs-lookup"><span data-stu-id="801bc-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="801bc-164">後續相同模式時您所傳送的 hello`POST`和`DELETE`要求 toohello web API，從 hello 快取使用 MSAL tooretrieve hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="801bc-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="801bc-165">執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="801bc-165">Run hello sample app</span></span>

<span data-ttu-id="801bc-166">最後，建置並執行兩個 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="801bc-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="801bc-167">註冊和登入，並建立 hello 登入的使用者進行的工作。</span><span class="sxs-lookup"><span data-stu-id="801bc-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="801bc-168">請登出應用程式，再以不同的使用者身分登入，</span><span class="sxs-lookup"><span data-stu-id="801bc-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="801bc-169">然後為該使用者建立工作。</span><span class="sxs-lookup"><span data-stu-id="801bc-169">Create tasks for that user.</span></span> <span data-ttu-id="801bc-170">請注意 hello 工作預存每位使用者在 hello API，因為 hello API 會從收到 hello 語彙基元擷取 hello 使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="801bc-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="801bc-171">也可以嘗試播放 hello 的領域。</span><span class="sxs-lookup"><span data-stu-id="801bc-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="801bc-172">移除 hello 權限太 「 寫入 」，然後再次嘗試新增一項工作。</span><span class="sxs-lookup"><span data-stu-id="801bc-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="801bc-173">您只需要確定 toosign 每次變更 hello 範圍外。</span><span class="sxs-lookup"><span data-stu-id="801bc-173">Just make sure toosign out each time you change hello scope.</span></span>

