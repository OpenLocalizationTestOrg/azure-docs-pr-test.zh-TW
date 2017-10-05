---
title: Azure AD B2C | Microsoft Docs
description: "如何使用 Azure Active Directory B2C 建置 .NET Web API，並使用 OAuth 2.0 存取權杖進行驗證加以保護。"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="c84e5-103">Azure Active Directory B2C：建置 .NET Web API</span><span class="sxs-lookup"><span data-stu-id="c84e5-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="c84e5-104">透過 Azure Active Directory (Azure AD) B2C，您可以使用 OAuth 2.0 存取權杖來保護 Web API。</span><span class="sxs-lookup"><span data-stu-id="c84e5-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="c84e5-105">這些權杖可讓您的用戶端應用程式對 API 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="c84e5-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="c84e5-106">本文將說明如何建立 .NET MVC「待辦事項清單」API，以便用戶端應用程式的使用者進行 CRUD 工作。</span><span class="sxs-lookup"><span data-stu-id="c84e5-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="c84e5-107">Web API 會使用 Azure AD B2C 進行保護，只允許已驗證的使用者管理他們的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="c84e5-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="c84e5-108">建立 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="c84e5-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="c84e5-109">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="c84e5-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="c84e5-110">目錄是適用於所有使用者、app、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="c84e5-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="c84e5-111">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。</span><span class="sxs-lookup"><span data-stu-id="c84e5-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="c84e5-112">用戶端應用程式和 Web API 必須使用相同的 Azure AD B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="c84e5-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="c84e5-113">建立 Web API</span><span class="sxs-lookup"><span data-stu-id="c84e5-113">Create a web API</span></span>

<span data-ttu-id="c84e5-114">接著，您必須在 B2C 目錄中建立 Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c84e5-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="c84e5-115">這會提供必要資訊給 Azure AD，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="c84e5-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="c84e5-116">若要建立應用程式，請遵循 [這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="c84e5-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="c84e5-117">請務必：</span><span class="sxs-lookup"><span data-stu-id="c84e5-117">Be sure to:</span></span>

* <span data-ttu-id="c84e5-118">在應用程式中加入 **Web 應用程式**或 **Web API**。</span><span class="sxs-lookup"><span data-stu-id="c84e5-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="c84e5-119">使用 Web 應用程式的 [重新導向 URI] `https://localhost:44332/`。</span><span class="sxs-lookup"><span data-stu-id="c84e5-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="c84e5-120">這是適用於此程式碼範例的 Web 應用程式用戶端的預設位置。</span><span class="sxs-lookup"><span data-stu-id="c84e5-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="c84e5-121">複製指派給您的應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="c84e5-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="c84e5-122">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="c84e5-122">You'll need it later.</span></span>
* <span data-ttu-id="c84e5-123">在 [應用程式識別碼 URI] 中輸入應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c84e5-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="c84e5-124">透過 [發佈的範圍] 功能表新增權限。</span><span class="sxs-lookup"><span data-stu-id="c84e5-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="c84e5-125">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="c84e5-125">Create your policies</span></span>

<span data-ttu-id="c84e5-126">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="c84e5-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="c84e5-127">您必須建立原則，才能與 Azure AD B2C 通訊。</span><span class="sxs-lookup"><span data-stu-id="c84e5-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="c84e5-128">我們建議使用合併的註冊/登入原則 (如[原則參考文章](active-directory-b2c-reference-policies.md)所述)。</span><span class="sxs-lookup"><span data-stu-id="c84e5-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="c84e5-129">建立原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="c84e5-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="c84e5-130">選擇 [顯示名稱]  和原則中的其他註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="c84e5-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="c84e5-131">針對每個原則選擇 [顯示名稱] 和 [物件識別碼] 宣告做為應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="c84e5-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="c84e5-132">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="c84e5-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="c84e5-133">在您建立每個原則之後，請複製原則的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="c84e5-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="c84e5-134">您稍後需要用到此原則名稱。</span><span class="sxs-lookup"><span data-stu-id="c84e5-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="c84e5-135">當您成功建立原則之後，就可以開始建置您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c84e5-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="c84e5-136">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="c84e5-136">Download the code</span></span>

<span data-ttu-id="c84e5-137">本教學課程的程式碼保留在 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi) 上。</span><span class="sxs-lookup"><span data-stu-id="c84e5-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="c84e5-138">您可以藉由執行下列作業來複製範例︰</span><span class="sxs-lookup"><span data-stu-id="c84e5-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="c84e5-139">下載範例程式碼後，請開啟 Visual Studio .sln 檔案開始進行。</span><span class="sxs-lookup"><span data-stu-id="c84e5-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="c84e5-140">您的方案現在包含兩個專案：`TaskWebApp``TaskService`。</span><span class="sxs-lookup"><span data-stu-id="c84e5-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="c84e5-141">`TaskWebApp` 是使用者所互動的 MVC Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c84e5-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="c84e5-142">`TaskService` 是應用程式的後端 Web API，其會儲存每位使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="c84e5-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="c84e5-143">本文只會討論 `TaskService` 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c84e5-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="c84e5-144">若要了解如何使用 Azure AD B2C 建置 `TaskWebApp`，請參閱 [.NET Web 應用程式教學課程](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。</span><span class="sxs-lookup"><span data-stu-id="c84e5-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="c84e5-145">更新 Azure AD B2C 組態</span><span class="sxs-lookup"><span data-stu-id="c84e5-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="c84e5-146">我們的範例已設定成使用示範租用戶的原則和用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="c84e5-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="c84e5-147">如果您想要使用自己的租用戶，您必須執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="c84e5-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="c84e5-148">在 `TaskService` 專案中開啟 `web.config`，並取代下列各項的值：</span><span class="sxs-lookup"><span data-stu-id="c84e5-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="c84e5-149">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="c84e5-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="c84e5-150">`ida:ClientId`：使用您的 Web API 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="c84e5-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="c84e5-151">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="c84e5-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="c84e5-152">在 `TaskWebApp` 專案中開啟 `web.config`，並取代下列各項的值：</span><span class="sxs-lookup"><span data-stu-id="c84e5-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="c84e5-153">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="c84e5-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="c84e5-154">`ida:ClientId`：使用您的 Web 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="c84e5-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="c84e5-155">`ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="c84e5-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="c84e5-156">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="c84e5-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="c84e5-157">`ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱</span><span class="sxs-lookup"><span data-stu-id="c84e5-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="c84e5-158">`ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱</span><span class="sxs-lookup"><span data-stu-id="c84e5-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="c84e5-159">保護 API</span><span class="sxs-lookup"><span data-stu-id="c84e5-159">Secure the API</span></span>

<span data-ttu-id="c84e5-160">當您有可呼叫 API 的用戶端時，您可以使用 OAuth 2.0 持有人權杖來保護 API (例如 `TaskService`)。</span><span class="sxs-lookup"><span data-stu-id="c84e5-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="c84e5-161">這可確保唯有要求具備持有人權杖時，API 的每個要求才有效。</span><span class="sxs-lookup"><span data-stu-id="c84e5-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="c84e5-162">您的 API 可以使用 Microsoft 的 Open Web Interface for .NET (OWIN) 程式庫來接受並驗證持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="c84e5-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="c84e5-163">安裝 OWIN</span><span class="sxs-lookup"><span data-stu-id="c84e5-163">Install OWIN</span></span>

<span data-ttu-id="c84e5-164">首先，使用 Visual Studio Package Manager Console 來安裝 OWIN OAuth 驗證管線。</span><span class="sxs-lookup"><span data-stu-id="c84e5-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="c84e5-165">這會安裝 OWIN 中介軟體，以便接受並驗證持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="c84e5-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="c84e5-166">新增 OWIN 啟動類別</span><span class="sxs-lookup"><span data-stu-id="c84e5-166">Add an OWIN startup class</span></span>

<span data-ttu-id="c84e5-167">將 OWIN 啟動類別新增至名為 `Startup.cs` 的 API。</span><span class="sxs-lookup"><span data-stu-id="c84e5-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="c84e5-168">以滑鼠右鍵按一下專案，依序選取 [新增] 和 [新增項目]，然後搜尋 OWIN。</span><span class="sxs-lookup"><span data-stu-id="c84e5-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="c84e5-169">OWIN 中介軟體將會在應用程式啟動時叫用 `Configuration(…)` 方法。</span><span class="sxs-lookup"><span data-stu-id="c84e5-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="c84e5-170">在我們的範例中，我們將類別宣告變更為 `public partial class Startup` 並且在 `App_Start\Startup.Auth.cs` 中實作類別的其他部分。</span><span class="sxs-lookup"><span data-stu-id="c84e5-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="c84e5-171">在 `Configuration` 方法中，我們將呼叫新增至 `ConfigureAuth`(其定義於 `Startup.Auth.cs`)。</span><span class="sxs-lookup"><span data-stu-id="c84e5-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="c84e5-172">修改之後，`Startup.cs` 如下所示︰</span><span class="sxs-lookup"><span data-stu-id="c84e5-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="c84e5-173">設定 OAuth 2.0 驗證</span><span class="sxs-lookup"><span data-stu-id="c84e5-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="c84e5-174">開啟 `App_Start\Startup.Auth.cs` 檔案，然後實作 `ConfigureAuth(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="c84e5-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="c84e5-175">例如，它可能如下所示︰</span><span class="sxs-lookup"><span data-stu-id="c84e5-175">For example, it could look like the following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="c84e5-176">保護工作控制器</span><span class="sxs-lookup"><span data-stu-id="c84e5-176">Secure the task controller</span></span>

<span data-ttu-id="c84e5-177">將應用程式設定為使用 OAuth 2.0 驗證之後，只需將 `[Authorize]` 標記加入工作控制器，就能保護您的 Web API。</span><span class="sxs-lookup"><span data-stu-id="c84e5-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="c84e5-178">所有的待辦事項清單操作都會在此控制器中進行，因此您應該在類別層級上保護整個控制器。</span><span class="sxs-lookup"><span data-stu-id="c84e5-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="c84e5-179">您也可以將 `[Authorize]` 標記加入個別的動作，以進行更細微的控制。</span><span class="sxs-lookup"><span data-stu-id="c84e5-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="c84e5-180">從權杖取得使用者資訊</span><span class="sxs-lookup"><span data-stu-id="c84e5-180">Get user information from the token</span></span>

<span data-ttu-id="c84e5-181">`TasksController` 會將工作儲存在資料庫中，而每個工作都有一個「擁有」此工作的相關聯使用者。</span><span class="sxs-lookup"><span data-stu-id="c84e5-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="c84e5-182">擁有者是藉由使用者的**物件識別碼**來識別。</span><span class="sxs-lookup"><span data-stu-id="c84e5-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="c84e5-183">(這就是為什麼您需要在所有原則中新增物件識別碼以做為應用程式宣告的原因)。</span><span class="sxs-lookup"><span data-stu-id="c84e5-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="c84e5-184">驗證權杖中的權限</span><span class="sxs-lookup"><span data-stu-id="c84e5-184">Validate the permissions in the token</span></span>

<span data-ttu-id="c84e5-185">Web API 的一個常見需求是驗證權杖中是否有「範圍」存在。</span><span class="sxs-lookup"><span data-stu-id="c84e5-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="c84e5-186">這可確保使用者已對存取待辦事項清單服務所需的權限表示同意。</span><span class="sxs-lookup"><span data-stu-id="c84e5-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="c84e5-187">執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="c84e5-187">Run the sample app</span></span>

<span data-ttu-id="c84e5-188">最後，請建置並執行 `TaskWebApp` 和 `TaskService`。</span><span class="sxs-lookup"><span data-stu-id="c84e5-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="c84e5-189">在使用者的待辦事項清單中建立一些工作，觀察即使停止並重新啟動用戶端之後，這些工作仍持續存在 API 中。</span><span class="sxs-lookup"><span data-stu-id="c84e5-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="c84e5-190">編輯您的原則</span><span class="sxs-lookup"><span data-stu-id="c84e5-190">Edit your policies</span></span>

<span data-ttu-id="c84e5-191">在您使用 Azure AD B2C 來保護 API 之後，就可以試驗登入/註冊原則，並檢視對 API 產生的效果 (或沒有效果)。</span><span class="sxs-lookup"><span data-stu-id="c84e5-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="c84e5-192">您可以操作原則中的應用程式宣告，然後變更 Web API 中可用的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="c84e5-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="c84e5-193">如本文先前所述，您加入的任何宣告都可在 `ClaimsPrincipal` 物件中供您的 .NET MVC Web API 使用。</span><span class="sxs-lookup"><span data-stu-id="c84e5-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
