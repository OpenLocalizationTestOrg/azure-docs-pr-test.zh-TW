---
title: "aaaAzure AD B2C |Microsoft 文件"
description: "如何使用 Azure Active Directory B2C 的.NET Web 應用程式開發介面 toobuild 保護使用 OAuth 2.0 存取權杖來進行驗證。"
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
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="ede92-103">Azure Active Directory B2C：建置 .NET Web API</span><span class="sxs-lookup"><span data-stu-id="ede92-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="ede92-104">透過 Azure Active Directory (Azure AD) B2C，您可以使用 OAuth 2.0 存取權杖來保護 Web API。</span><span class="sxs-lookup"><span data-stu-id="ede92-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="ede92-105">這些語彙基元可讓您的用戶端應用程式 tooauthenticate toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="ede92-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="ede92-106">本文章將示範如何 toocreate.NET MVC 「 待辦事項清單 」 應用程式開發介面可讓使用者在您的用戶端的應用程式 tooCRUD 工作。</span><span class="sxs-lookup"><span data-stu-id="ede92-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="ede92-107">hello web API 使用 Azure AD B2C 保護，並且只允許已驗證的使用者 toomanage 其待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="ede92-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="ede92-108">建立 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="ede92-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="ede92-109">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="ede92-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="ede92-110">目錄是適用於所有使用者、app、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="ede92-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="ede92-111">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。</span><span class="sxs-lookup"><span data-stu-id="ede92-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="ede92-112">hello 用戶端應用程式和 web API 必須使用 hello 相同的 Azure AD B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="ede92-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="ede92-113">建立 Web API</span><span class="sxs-lookup"><span data-stu-id="ede92-113">Create a web API</span></span>

<span data-ttu-id="ede92-114">接下來，您需要 toocreate web API 應用程式中 B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="ede92-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="ede92-115">提供 Azure AD，它需要 toosecurely 通訊與您的應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="ede92-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="ede92-116">toocreate 的應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="ede92-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="ede92-117">請務必：</span><span class="sxs-lookup"><span data-stu-id="ede92-117">Be sure to:</span></span>

* <span data-ttu-id="ede92-118">包含**web 應用程式**或**web API** hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ede92-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="ede92-119">使用 hello**重新導向 URI** `https://localhost:44332/` hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ede92-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="ede92-120">這是 hello hello web 應用程式用戶端，此程式碼範例預設位置。</span><span class="sxs-lookup"><span data-stu-id="ede92-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="ede92-121">複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ede92-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="ede92-122">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="ede92-122">You'll need it later.</span></span>
* <span data-ttu-id="ede92-123">在 [應用程式識別碼 URI] 中輸入應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ede92-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="ede92-124">新增權限透過 hello**發行領域**功能表。</span><span class="sxs-lookup"><span data-stu-id="ede92-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ede92-125">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="ede92-125">Create your policies</span></span>

<span data-ttu-id="ede92-126">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="ede92-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ede92-127">您必須使用 Azure AD B2C 原則 toocommunicate toocreate。</span><span class="sxs-lookup"><span data-stu-id="ede92-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="ede92-128">我們建議使用 hello 結合 sign-up/登入原則 hello 中所述[原則參考文件](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="ede92-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ede92-129">建立原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="ede92-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="ede92-130">選擇 [顯示名稱]  和原則中的其他註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="ede92-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="ede92-131">針對每個原則選擇 [顯示名稱] 和 [物件識別碼] 宣告做為應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="ede92-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="ede92-132">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="ede92-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="ede92-133">複製 hello**名稱**的每個原則建立之後。</span><span class="sxs-lookup"><span data-stu-id="ede92-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="ede92-134">稍後您將需要 hello 原則名稱。</span><span class="sxs-lookup"><span data-stu-id="ede92-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ede92-135">您已成功建立 hello 原則之後，您便準備好 toobuild 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ede92-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="ede92-136">下載 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="ede92-136">Download hello code</span></span>

<span data-ttu-id="ede92-137">本教學課程中的 hello 程式碼維護在[GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)。</span><span class="sxs-lookup"><span data-stu-id="ede92-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="ede92-138">您可以藉由執行複製 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="ede92-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="ede92-139">下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="ede92-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="ede92-140">hello 方案檔包含兩個專案：`TaskWebApp`和`TaskService`。</span><span class="sxs-lookup"><span data-stu-id="ede92-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="ede92-141">`TaskWebApp`是 hello 使用者 MVC web 應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="ede92-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="ede92-142">`TaskService`是 hello 應用程式後端 web API，儲存每個使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="ede92-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="ede92-143">本文將只會討論 hello`TaskService`應用程式。</span><span class="sxs-lookup"><span data-stu-id="ede92-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="ede92-144">toolearn 如何 toobuild`TaskWebApp`使用 Azure AD B2C，請參閱[我們.NET web 應用程式教學課程](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。</span><span class="sxs-lookup"><span data-stu-id="ede92-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="ede92-145">更新 Azure AD B2C hello 組態</span><span class="sxs-lookup"><span data-stu-id="ede92-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="ede92-146">我們的範例是設定的 toouse hello 原則和用戶端識別碼我們示範租用戶。</span><span class="sxs-lookup"><span data-stu-id="ede92-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="ede92-147">如果您想要 toouse 自己的租用戶，您必須遵循 toodo hello:</span><span class="sxs-lookup"><span data-stu-id="ede92-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="ede92-148">開啟`web.config`在 hello`TaskService`專案和 hello 值取代</span><span class="sxs-lookup"><span data-stu-id="ede92-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="ede92-149">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="ede92-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="ede92-150">`ida:ClientId`：使用您的 Web API 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="ede92-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="ede92-151">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="ede92-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="ede92-152">開啟`web.config`在 hello`TaskWebApp`專案和 hello 值取代</span><span class="sxs-lookup"><span data-stu-id="ede92-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="ede92-153">`ida:Tenant`：使用您的租用戶名稱</span><span class="sxs-lookup"><span data-stu-id="ede92-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="ede92-154">`ida:ClientId`：使用您的 Web 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="ede92-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="ede92-155">`ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰</span><span class="sxs-lookup"><span data-stu-id="ede92-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="ede92-156">`ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱</span><span class="sxs-lookup"><span data-stu-id="ede92-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="ede92-157">`ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱</span><span class="sxs-lookup"><span data-stu-id="ede92-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="ede92-158">`ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱</span><span class="sxs-lookup"><span data-stu-id="ede92-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="ede92-159">安全 hello 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="ede92-159">Secure hello API</span></span>

<span data-ttu-id="ede92-160">當您有可呼叫 API 的用戶端時，您可以使用 OAuth 2.0 持有人權杖來保護 API (例如 `TaskService`)。</span><span class="sxs-lookup"><span data-stu-id="ede92-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="ede92-161">這可確保每個要求 tooyour API 才會有效 hello 要求是否持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="ede92-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="ede92-162">您的 API 可以使用 Microsoft 的 Open Web Interface for .NET (OWIN) 程式庫來接受並驗證持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="ede92-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="ede92-163">安裝 OWIN</span><span class="sxs-lookup"><span data-stu-id="ede92-163">Install OWIN</span></span>

<span data-ttu-id="ede92-164">開始使用 Visual Studio Package Manager Console hello 安裝 hello OWIN OAuth 驗證管線。</span><span class="sxs-lookup"><span data-stu-id="ede92-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="ede92-165">這會安裝 hello OWIN 中介軟體，將接受和驗證持有者權杖。</span><span class="sxs-lookup"><span data-stu-id="ede92-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="ede92-166">新增 OWIN 啟動類別</span><span class="sxs-lookup"><span data-stu-id="ede92-166">Add an OWIN startup class</span></span>

<span data-ttu-id="ede92-167">新增 OWIN 啟動類別 toohello API 呼叫`Startup.cs`。</span><span class="sxs-lookup"><span data-stu-id="ede92-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="ede92-168">以滑鼠右鍵按一下 hello 專案、 選取**新增**和**新項目**，然後搜尋 OWIN。</span><span class="sxs-lookup"><span data-stu-id="ede92-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="ede92-169">hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="ede92-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="ede92-170">在我們的範例中，我們變更 hello 類別宣告太`public partial class Startup`和實作 hello hello 類別中的其他部分`App_Start\Startup.Auth.cs`。</span><span class="sxs-lookup"><span data-stu-id="ede92-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="ede92-171">內部 hello`Configuration`方法中，我們加入呼叫太`ConfigureAuth`，定義在`Startup.Auth.cs`。</span><span class="sxs-lookup"><span data-stu-id="ede92-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="ede92-172">Hello 修改之後`Startup.cs`看起來像 hello 面：</span><span class="sxs-lookup"><span data-stu-id="ede92-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

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

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="ede92-173">設定 OAuth 2.0 驗證</span><span class="sxs-lookup"><span data-stu-id="ede92-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="ede92-174">開啟 hello 檔案`App_Start\Startup.Auth.cs`，並實作 hello`ConfigureAuth(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="ede92-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="ede92-175">例如，它可能看起來像 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ede92-175">For example, it could look like hello following:</span></span>

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
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="ede92-176">安全 hello 工作控制站</span><span class="sxs-lookup"><span data-stu-id="ede92-176">Secure hello task controller</span></span>

<span data-ttu-id="ede92-177">Hello 應用程式設定的 toouse OAuth 2.0 驗證之後，您可以藉由新增保護您的 web API`[Authorize]`標記 toohello 工作控制站。</span><span class="sxs-lookup"><span data-stu-id="ede92-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="ede92-178">這是其中所有的待辦事項清單操作發生，因此您應該保護 hello 整個控制器 hello 類別層級的 hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="ede92-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="ede92-179">您也可以加入 hello`[Authorize]`標記更細部的掌控 tooindividual 動作。</span><span class="sxs-lookup"><span data-stu-id="ede92-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="ede92-180">Hello 從權杖取得使用者資訊</span><span class="sxs-lookup"><span data-stu-id="ede92-180">Get user information from hello token</span></span>

<span data-ttu-id="ede92-181">`TasksController`將工作儲存在資料庫，其中每個工作都有關聯的使用者，「 擁有 」 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="ede92-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="ede92-182">hello 擁有者由 hello 使用者**物件識別碼**。</span><span class="sxs-lookup"><span data-stu-id="ede92-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="ede92-183">(這就是為什麼需要 tooadd hello 物件識別碼，做為應用程式所有的原則中的宣告。)</span><span class="sxs-lookup"><span data-stu-id="ede92-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="ede92-184">驗證 hello 權杖中的 hello 權限</span><span class="sxs-lookup"><span data-stu-id="ede92-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="ede92-185">Web 應用程式開發介面的共通需求是 toovalidate hello 「 範圍 」 hello 權杖中。</span><span class="sxs-lookup"><span data-stu-id="ede92-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="ede92-186">這可確保該 hello 使用者同意 toohello 權限需要的 tooaccess hello 待辦事項清單服務。</span><span class="sxs-lookup"><span data-stu-id="ede92-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="ede92-187">執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="ede92-187">Run hello sample app</span></span>

<span data-ttu-id="ede92-188">最後，請建置並執行 `TaskWebApp` 和 `TaskService`。</span><span class="sxs-lookup"><span data-stu-id="ede92-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="ede92-189">Hello 使用者待辦事項清單上建立一些工作，並注意如何在保存在 hello API 即使您停止並重新啟動 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ede92-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="ede92-190">編輯您的原則</span><span class="sxs-lookup"><span data-stu-id="ede92-190">Edit your policies</span></span>

<span data-ttu-id="ede92-191">您已有使用 Azure AD B2C 保護應用程式開發介面之後，您可以試驗您登在 /-註冊原則和檢視 hello 效果上 （或短缺） hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="ede92-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="ede92-192">您可以操作 hello hello 原則中的應用程式宣告，並變更用於 hello web API 的 hello 使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="ede92-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="ede92-193">您新增任何宣告將會是可用 tooyour.NET MVC web 應用程式開發介面中 hello`ClaimsPrincipal`物件，如本文稍早所述。</span><span class="sxs-lookup"><span data-stu-id="ede92-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
