---
title: "aaaAzure AD v2.0.NET web 應用程式登入使用者入門 |Microsoft 文件"
description: "如何 toobuild.NET MVC Web 應用程式的使用者使用簽署兩個人的 Microsoft 帳戶和工作或學校帳戶。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="b5641-103">新增登入 tooan.NET MVC web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b5641-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="b5641-104">與 hello v2.0 端點，您可以快速加入具有兩個個人 Microsoft 帳戶的支援，以及工作或學校帳戶的驗證 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5641-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="b5641-105">在 ASP.NET Web 應用程式中，您可以使用隨附於 .NET Framework 4.5 的 Microsoft OWIN 中介軟體來完成此項作業。</span><span class="sxs-lookup"><span data-stu-id="b5641-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="b5641-106">並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="b5641-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="b5641-107">toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="b5641-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="b5641-108">這裡我們會建置 web 應用程式使用 OWIN toosign hello 使用者顯示中的 hello 使用者的一些資訊和符號 hello 使用者登出 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5641-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="b5641-109">下載</span><span class="sxs-lookup"><span data-stu-id="b5641-109">Download</span></span>
<span data-ttu-id="b5641-110">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="b5641-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="b5641-111">您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip)或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="b5641-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="b5641-112">在本教學課程的 hello 結尾處提供 hello 完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5641-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="b5641-113">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="b5641-113">Register an app</span></span>
<span data-ttu-id="b5641-114">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="b5641-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="b5641-115">請確定：</span><span class="sxs-lookup"><span data-stu-id="b5641-115">Make sure to:</span></span>

* <span data-ttu-id="b5641-116">複製下 hello**應用程式識別碼**指派 tooyour 應用程式，您將需要它過期。</span><span class="sxs-lookup"><span data-stu-id="b5641-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="b5641-117">新增 hello **Web**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5641-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="b5641-118">輸入正確的 hello**重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="b5641-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="b5641-119">hello 重新導向 uri 表示的 tooAzure AD 其中應該導向驗證回應-此教學課程中的 hello 預設為`https://localhost:44326/`。</span><span class="sxs-lookup"><span data-stu-id="b5641-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="b5641-120">安裝及設定 OWIN 驗證</span><span class="sxs-lookup"><span data-stu-id="b5641-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="b5641-121">在這裡，我們會將設定 hello OWIN 中介軟體 toouse hello OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b5641-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="b5641-122">OWIN 將會使用的 tooissue 登入和登出要求、 管理 hello 使用者工作階段，以及取得 hello 使用者，在其他項目之間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b5641-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="b5641-123">toobegin，開啟 hello `web.config` hello hello 專案根目錄中的檔案，並在 hello 中輸入您的應用程式組態值`<appSettings>`> 一節。</span><span class="sxs-lookup"><span data-stu-id="b5641-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="b5641-124">hello`ida:ClientId`為 hello**應用程式識別碼**指派 tooyour hello 註冊入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5641-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="b5641-125">hello`ida:RedirectUri`為 hello**重新導向 Uri** hello 入口網站中輸入。</span><span class="sxs-lookup"><span data-stu-id="b5641-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="b5641-126">接下來，加入 hello OWIN 中介軟體 NuGet 封裝 toohello 專案使用 Package Manager Console hello。</span><span class="sxs-lookup"><span data-stu-id="b5641-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="b5641-127">新增 < OWIN 啟動類別 > toohello 專案呼叫`Startup.cs`右 hello 專案上的按一下-->**新增** --> **新項目**--> 搜尋"OWIN"。</span><span class="sxs-lookup"><span data-stu-id="b5641-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="b5641-128">hello OWIN 中介軟體將會叫用 hello`Configuration(...)`方法，當您啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5641-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="b5641-129">也變更 hello 類別宣告`public partial class Startup`-我們已實作了此類別的一部分，另一個檔案中。</span><span class="sxs-lookup"><span data-stu-id="b5641-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="b5641-130">在 hello`Configuration(...)`方法，請呼叫 tooConfigureAuth(...) tooset 向上驗證 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b5641-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. <span data-ttu-id="b5641-131">開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="b5641-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="b5641-132">hello 的參數中提供`OpenIdConnectAuthenticationOptions`將做為您的應用程式 toocommunicate 與 Azure AD 的座標。</span><span class="sxs-lookup"><span data-stu-id="b5641-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="b5641-133">您也必須設定的 Cookie 驗證 tooset-hello OpenID Connect 中介軟體會使用 cookie hello 涵蓋下方。</span><span class="sxs-lookup"><span data-stu-id="b5641-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a><span data-ttu-id="b5641-134">傳送驗證要求</span><span class="sxs-lookup"><span data-stu-id="b5641-134">Send authentication requests</span></span>
<span data-ttu-id="b5641-135">您的應用程式已正確設定的 toocommunicate 與 hello v2.0 端點使用 hello OpenID Connect 的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b5641-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="b5641-136">OWIN 已處理所有 hello 醜陋詳細的製作驗證訊息、 驗證 Azure ad 的權杖和維護使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="b5641-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="b5641-137">所有會維持為您的使用者是 toogive 方式 toosign 中的並登出。</span><span class="sxs-lookup"><span data-stu-id="b5641-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="b5641-138">您可以使用授權標記中控制站 toorequire 使用者登入時存取某一頁之前。</span><span class="sxs-lookup"><span data-stu-id="b5641-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="b5641-139">開啟`Controllers\HomeController.cs`，並加入 hello`[Authorize]`標記 toohello 有關控制站。</span><span class="sxs-lookup"><span data-stu-id="b5641-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="b5641-140">您也可以在程式碼中使用從 OWIN toodirectly 發出驗證要求。</span><span class="sxs-lookup"><span data-stu-id="b5641-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="b5641-141">開啟 `Controllers\AccountController.cs`。</span><span class="sxs-lookup"><span data-stu-id="b5641-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="b5641-142">在 hello SignIn() 和 Signout 動作，會發出 OpenID Connect 的挑戰和登出要求，分別。</span><span class="sxs-lookup"><span data-stu-id="b5641-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="b5641-143">現在，請開啟 `Views\Shared\_LoginPartial.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="b5641-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="b5641-144">這是您將在其中顯示 hello 使用者在您的應用程式登入和登出連結，並列印出檢視中的 hello 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="b5641-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
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

## <a name="display-user-information"></a><span data-ttu-id="b5641-145">顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="b5641-145">Display user information</span></span>
<span data-ttu-id="b5641-146">驗證時使用 OpenID Connect 使用者，hello v2.0 端點會傳回包含宣告或有關 hello 使用者判斷提示的 id_token toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5641-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="b5641-147">您可以使用這些宣告 toopersonalize 您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="b5641-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="b5641-148">開啟 hello`Controllers\HomeController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="b5641-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="b5641-149">您可以在 hello 透過您控制站存取 hello 使用者宣告`ClaimsPrincipal.Current`安全性主體物件。</span><span class="sxs-lookup"><span data-stu-id="b5641-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="b5641-150">執行</span><span class="sxs-lookup"><span data-stu-id="b5641-150">Run</span></span>
<span data-ttu-id="b5641-151">最後，建置並執行您的應用程式！</span><span class="sxs-lookup"><span data-stu-id="b5641-151">Finally, build and run your app!</span></span>   <span data-ttu-id="b5641-152">使用個人 Microsoft 帳戶或工作或學校帳戶，登入，並注意 hello 使用者的身分識別會反映在 hello 上方導覽列中的方式。</span><span class="sxs-lookup"><span data-stu-id="b5641-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="b5641-153">您的 Web 應用程式現在使用業界標準的通訊協定保護，可以使用個人與工作/學校帳戶來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="b5641-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="b5641-154">如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip)，或您可以將其複製從 GitHub:</span><span class="sxs-lookup"><span data-stu-id="b5641-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="b5641-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5641-155">Next steps</span></span>
<span data-ttu-id="b5641-156">您現在可以進入更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="b5641-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="b5641-157">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="b5641-157">You may want tootry:</span></span>

[<span data-ttu-id="b5641-158">保護 Web Api</與 hello hello v2.0 端點 >></span><span class="sxs-lookup"><span data-stu-id="b5641-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="b5641-159">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b5641-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="b5641-160">hello v2.0 開發人員指南 >></span><span class="sxs-lookup"><span data-stu-id="b5641-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="b5641-161">StackOverflow "azure-active-directory" 標籤 >></span><span class="sxs-lookup"><span data-stu-id="b5641-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="b5641-162">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="b5641-162">Get security updates for our products</span></span>
<span data-ttu-id="b5641-163">我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。</span><span class="sxs-lookup"><span data-stu-id="b5641-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
