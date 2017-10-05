---
title: Azure Active Directory B2C | Microsoft Docs
description: "如何使用 Azure Active Directory B2C 和 OAuth 2.0 存取權杖，建置 .NET Web 應用程式並呼叫 Web API。"
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
ms.openlocfilehash: 48452eb68f826d1c7aa61d5e5531f941ac1422b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="29489-103">Azure AD B2C：從 .NET Web 應用程式呼叫 .NET Web API</span><span class="sxs-lookup"><span data-stu-id="29489-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="29489-104">使用 Azure AD B2C，您可以將強大的身分識別管理功能新增至 Web 應用程式和 Web API。</span><span class="sxs-lookup"><span data-stu-id="29489-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="29489-105">本文討論如何要求存取權杖，以及從 .NET「待辦事項清單」Web 應用程式呼叫 .NET Web API。</span><span class="sxs-lookup"><span data-stu-id="29489-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="29489-106">本文不涵蓋如何使用 Azure AD B2C 實作登入、註冊和管理設定檔。</span><span class="sxs-lookup"><span data-stu-id="29489-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="29489-107">而會著重在如何在使用者已通過驗證後呼叫 Web API。</span><span class="sxs-lookup"><span data-stu-id="29489-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="29489-108">如果您尚未執行此動作，您應該：</span><span class="sxs-lookup"><span data-stu-id="29489-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="29489-109">開始使用 [.NET Web 應用程式](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="29489-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="29489-110">開始使用 [.NET Web API](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="29489-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="29489-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="29489-111">Prerequisite</span></span>

<span data-ttu-id="29489-112">若要建置呼叫 Web API 的 Web 應用程式，您需要：</span><span class="sxs-lookup"><span data-stu-id="29489-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="29489-113">[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="29489-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="29489-114">[註冊 Web API](active-directory-b2c-app-registration.md#register-a-web-api)。</span><span class="sxs-lookup"><span data-stu-id="29489-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="29489-115">[註冊 Web 應用程式](active-directory-b2c-app-registration.md#register-a-web-app)。</span><span class="sxs-lookup"><span data-stu-id="29489-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="29489-116">[設定原則](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="29489-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="29489-117">[為 Web 應用程式授與權限以使用 Web API](active-directory-b2c-access-tokens.md#publishing-permissions)。</span><span class="sxs-lookup"><span data-stu-id="29489-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29489-118">用戶端應用程式和 Web API 必須使用相同的 Azure AD B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="29489-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="29489-119">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="29489-119">Download the code</span></span>

<span data-ttu-id="29489-120">本教學課程的程式碼保留在 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi) 上。</span><span class="sxs-lookup"><span data-stu-id="29489-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="29489-121">您可以藉由執行下列作業來複製範例︰</span><span class="sxs-lookup"><span data-stu-id="29489-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="29489-122">下載範例程式碼後，請開啟 Visual Studio .sln 檔案開始進行。</span><span class="sxs-lookup"><span data-stu-id="29489-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="29489-123">您的方案現在包含兩個專案：`TaskWebApp``TaskService`。</span><span class="sxs-lookup"><span data-stu-id="29489-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="29489-124">`TaskWebApp` 是使用者所互動的 MVC Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29489-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="29489-125">`TaskService` 是應用程式的後端 Web API，其會儲存每位使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="29489-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="29489-126">本文未涵蓋建置 `TaskWebApp` Web 應用程式或 `TaskService` Web API。</span><span class="sxs-lookup"><span data-stu-id="29489-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="29489-127">若要了解如何使用 Azure AD B2C 建置 .NET Web 應用程式，請參閱 [.NET Web 應用程式教學課程](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。</span><span class="sxs-lookup"><span data-stu-id="29489-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="29489-128">若要了解如何使用 Azure AD B2C 建置 .NET Web API，請參閱 [.NET Web API 教學課程](active-directory-b2c-devquickstarts-api-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="29489-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="29489-129">更新 Azure AD B2C 組態</span><span class="sxs-lookup"><span data-stu-id="29489-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="29489-130">我們的範例已設定成使用示範租用戶的原則和用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="29489-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="29489-131">如果您想要使用自己的租用戶：</span><span class="sxs-lookup"><span data-stu-id="29489-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="29489-132">在 `TaskService` 專案中開啟 `web.config`，並取代下列各項的值：</span><span class="sxs-lookup"><span data-stu-id="29489-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="29489-133">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="29489-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="29489-134">`ida:ClientId`：使用您的 Web API 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="29489-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="29489-135">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="29489-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="29489-136">在 `TaskWebApp` 專案中開啟 `web.config`，並取代下列各項的值：</span><span class="sxs-lookup"><span data-stu-id="29489-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="29489-137">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="29489-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="29489-138">`ida:ClientId`：使用您的 Web 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="29489-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="29489-139">`ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="29489-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="29489-140">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="29489-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="29489-141">`ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱</span><span class="sxs-lookup"><span data-stu-id="29489-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="29489-142">`ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱</span><span class="sxs-lookup"><span data-stu-id="29489-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="29489-143">要求及儲存存取權杖</span><span class="sxs-lookup"><span data-stu-id="29489-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="29489-144">指定權限</span><span class="sxs-lookup"><span data-stu-id="29489-144">Specify the permissions</span></span>

<span data-ttu-id="29489-145">若要呼叫 Web API，您必須驗證使用者 (使用您的註冊/登入原則) 並從 Azure AD B2C [接收存取權杖](active-directory-b2c-access-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="29489-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="29489-146">若要接收存取權杖，您必須先指定您想要授與存取權杖的權限。</span><span class="sxs-lookup"><span data-stu-id="29489-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="29489-147">當您對 `/authorize` 端點提出要求時，權限是指定於 `scope` 參數中。</span><span class="sxs-lookup"><span data-stu-id="29489-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="29489-148">例如，若要取得具備資源應用程式 (其應用程式識別碼 URI 為 `https://contoso.onmicrosoft.com/tasks`) 之「讀取」權限的存取權杖，則範圍會是 `https://contoso.onmicrosoft.com/tasks/read`。</span><span class="sxs-lookup"><span data-stu-id="29489-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="29489-149">若要在我們的範例中指定範圍，請開啟檔案 `App_Start\Startup.Auth.cs`，並在 OpenIdConnectAuthenticationOptions 中定義 `Scope` 變數。</span><span class="sxs-lookup"><span data-stu-id="29489-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="29489-150">交換存取權杖的授權碼</span><span class="sxs-lookup"><span data-stu-id="29489-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="29489-151">使用者完成註冊或登入體驗之後，您的應用程式將會收到來自 Azure AD B2C 的授權碼。</span><span class="sxs-lookup"><span data-stu-id="29489-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="29489-152">OWIN OpenID Connect 中介軟體將儲存此授權碼，但不會針對存取權杖進行交換。</span><span class="sxs-lookup"><span data-stu-id="29489-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="29489-153">您可以使用 [MSAL 程式庫 (英文)](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) 進行交換。</span><span class="sxs-lookup"><span data-stu-id="29489-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="29489-154">在我們的範例中，我們設定了每次收到授權碼時對 OpenID Connect 中介軟體的回呼通知。</span><span class="sxs-lookup"><span data-stu-id="29489-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="29489-155">在回呼中，我們使用 MSAL 來交換權杖的授權碼，並將權杖儲存到快取。</span><span class="sxs-lookup"><span data-stu-id="29489-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="29489-156">呼叫 Web API</span><span class="sxs-lookup"><span data-stu-id="29489-156">Calling the web API</span></span>

<span data-ttu-id="29489-157">本節將討論如何使用註冊/登入期間所收到的權杖與 Azure AD B2C，以便存取 Web API。</span><span class="sxs-lookup"><span data-stu-id="29489-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="29489-158">擷取控制器中已儲存的權杖</span><span class="sxs-lookup"><span data-stu-id="29489-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="29489-159">`TasksController` 負責與 Web API 通訊，並傳送 HTTP 要求給 API 來讀取、建立和刪除工作。</span><span class="sxs-lookup"><span data-stu-id="29489-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="29489-160">因為 API 受到 Azure AD B2C 的保護，您必須先擷取您在上一個步驟中儲存的權杖。</span><span class="sxs-lookup"><span data-stu-id="29489-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="29489-161">從 Web API 讀取工作</span><span class="sxs-lookup"><span data-stu-id="29489-161">Read tasks from the web API</span></span>

<span data-ttu-id="29489-162">當您擁有權杖之後，就可以把權杖附加 HTTP `GET` 要求的 `Authorization` 標頭中，以安全地呼叫 `TaskService`：</span><span class="sxs-lookup"><span data-stu-id="29489-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="29489-163">在 Web API 上建立及刪除工作</span><span class="sxs-lookup"><span data-stu-id="29489-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="29489-164">請遵循與您傳送 `POST` 和 `DELETE` 要求給 Web API 時的相同模式，使用 MSAL 從快取擷取存取權杖。</span><span class="sxs-lookup"><span data-stu-id="29489-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="29489-165">執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="29489-165">Run the sample app</span></span>

<span data-ttu-id="29489-166">最後，建置並執行這兩個應用程式。</span><span class="sxs-lookup"><span data-stu-id="29489-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="29489-167">註冊和登入，並為登入的使用者建立工作。</span><span class="sxs-lookup"><span data-stu-id="29489-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="29489-168">請登出應用程式，再以不同的使用者身分登入，</span><span class="sxs-lookup"><span data-stu-id="29489-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="29489-169">然後為該使用者建立工作。</span><span class="sxs-lookup"><span data-stu-id="29489-169">Create tasks for that user.</span></span> <span data-ttu-id="29489-170">您會發現，這些工作在 API 上是依照使用者來儲存的 ，因為 API 會從自己收到的權杖中擷取使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="29489-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="29489-171">也可以嘗試使用範圍。</span><span class="sxs-lookup"><span data-stu-id="29489-171">Also try playing with the scopes.</span></span> <span data-ttu-id="29489-172">移除「寫入」的權限，然後嘗試新增一項工作。</span><span class="sxs-lookup"><span data-stu-id="29489-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="29489-173">只需確定每次您變更範圍時會登出。</span><span class="sxs-lookup"><span data-stu-id="29489-173">Just make sure to sign out each time you change the scope.</span></span>

