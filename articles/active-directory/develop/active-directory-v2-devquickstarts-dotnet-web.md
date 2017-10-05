---
title: "Azure AD v2.0 .NET Web 應用程式登入入門 | Microsoft Docs"
description: "如何建置可使用個人 Microsoft 帳戶及工作或學校帳戶登入使用者的 .NET MVC Web 應用程式。"
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="99f63-103">將登入新增至 .NET MVC Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="99f63-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="99f63-104">v2.0 端點可讓您快速地將驗證新增至您的 Web 應用程式，同時支援個人 Microsoft 帳戶以及工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="99f63-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="99f63-105">在 ASP.NET Web 應用程式中，您可以使用隨附於 .NET Framework 4.5 的 Microsoft OWIN 中介軟體來完成此項作業。</span><span class="sxs-lookup"><span data-stu-id="99f63-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="99f63-106">v2.0 端點並非支援每個 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="99f63-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="99f63-107">如果要判斷是否應該使用 v2.0 端點，請閱讀 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="99f63-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="99f63-108">現在，我們將組建使用 OWIN 將使用者登入、顯示使用者的部分相關資訊，以及將使用者登出應用程式的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99f63-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="99f63-109">下載</span><span class="sxs-lookup"><span data-stu-id="99f63-109">Download</span></span>
<span data-ttu-id="99f63-110">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet)上。</span><span class="sxs-lookup"><span data-stu-id="99f63-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="99f63-111">若要遵循執行，您可以 [用 .zip 格式下載應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ，或複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="99f63-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="99f63-112">本教學課程最後也會提供完整的應用程式。</span><span class="sxs-lookup"><span data-stu-id="99f63-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="99f63-113">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="99f63-113">Register an app</span></span>
<span data-ttu-id="99f63-114">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="99f63-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="99f63-115">請確定：</span><span class="sxs-lookup"><span data-stu-id="99f63-115">Make sure to:</span></span>

* <span data-ttu-id="99f63-116">將指派給您應用程式的 **應用程式識別碼** 複製起來，您很快會需要用到這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="99f63-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="99f63-117">為您的應用程式新增 **Web** 平台。</span><span class="sxs-lookup"><span data-stu-id="99f63-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="99f63-118">輸入正確的 **重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="99f63-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="99f63-119">重新導向 URI 會向 Azure AD 指出驗證回應應導向的位置，本教學課程的預設為 `https://localhost:44326/`。</span><span class="sxs-lookup"><span data-stu-id="99f63-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="99f63-120">安裝及設定 OWIN 驗證</span><span class="sxs-lookup"><span data-stu-id="99f63-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="99f63-121">在這裡，我們將設定 OWIN 中介軟體使用 OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="99f63-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="99f63-122">OWIN 將用來發出登入和登出要求、管理使用者的工作階段，以及取得使用者相關資訊等其他作業。</span><span class="sxs-lookup"><span data-stu-id="99f63-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="99f63-123">若要開始，請開啟專案根目錄中的 `web.config` 檔案，並在 `<appSettings>` 區段中輸入應用程式的組態值。</span><span class="sxs-lookup"><span data-stu-id="99f63-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="99f63-124">`ida:ClientId` 是在註冊入口網站中指派給應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="99f63-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="99f63-125">`ida:RedirectUri` 是您在入口網站中輸入的 **重新導向 URI** 。</span><span class="sxs-lookup"><span data-stu-id="99f63-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="99f63-126">接下來，使用 Package Manager Console 將Next, add the OWIN 中介軟體 NuGet 套件新增到專案中。</span><span class="sxs-lookup"><span data-stu-id="99f63-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="99f63-127">將「OWIN 啟動類別」新增至名為 `Startup.cs` 的專案。以滑鼠右鍵按一下專案 --> [新增]  -->  [新增項目] --> 搜尋 "OWIN"。</span><span class="sxs-lookup"><span data-stu-id="99f63-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="99f63-128">OWIN 中介軟體將會在應用程式啟動時叫用 `Configuration(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="99f63-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="99f63-129">將類別宣告變更為 `public partial class Startup` ，我們已為您在另一個檔案中實作了此類別的一部分。</span><span class="sxs-lookup"><span data-stu-id="99f63-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="99f63-130">在 `Configuration(...)` 方法中，請呼叫 ConfigureAuth(...)，為您的 Web 應用程式設定驗證。</span><span class="sxs-lookup"><span data-stu-id="99f63-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="99f63-131">開啟檔案 `App_Start\Startup.Auth.cs` 並實作 `ConfigureAuth(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="99f63-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="99f63-132">您在 `OpenIdConnectAuthenticationOptions` 中所提供的參數將會做為您的應用程式與 Azure AD 進行通訊的座標使用。</span><span class="sxs-lookup"><span data-stu-id="99f63-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="99f63-133">您還必須設定 Cookie 驗證，OpenID Connect 中介軟體會在表面下使用 Cookie。</span><span class="sxs-lookup"><span data-stu-id="99f63-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="99f63-134">傳送驗證要求</span><span class="sxs-lookup"><span data-stu-id="99f63-134">Send authentication requests</span></span>
<span data-ttu-id="99f63-135">您的應用程式現在已正確設定，將使用 OpenID Connect 驗證通訊協定與 v2.0 端點通訊。</span><span class="sxs-lookup"><span data-stu-id="99f63-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="99f63-136">OWIN 已經處理所有製作驗證訊息、驗證 Azure AD 的權杖和維護使用者工作階段的瑣碎詳細資料。</span><span class="sxs-lookup"><span data-stu-id="99f63-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="99f63-137">剩餘的工作就是提供使用者一個登入和登出的方式。</span><span class="sxs-lookup"><span data-stu-id="99f63-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="99f63-138">您可以在控制器中使用授權標籤，要求使用者在存取特定頁面時登入。</span><span class="sxs-lookup"><span data-stu-id="99f63-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="99f63-139">開啟 `Controllers\HomeController.cs`，並在 [關於] 控制器中加入 `[Authorize]` 標籤。</span><span class="sxs-lookup"><span data-stu-id="99f63-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="99f63-140">您也可以使用 OWIN 從程式碼中直接發出驗證要求。</span><span class="sxs-lookup"><span data-stu-id="99f63-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="99f63-141">開啟 `Controllers\AccountController.cs`。</span><span class="sxs-lookup"><span data-stu-id="99f63-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="99f63-142">在 SignIn() 和 SignOut() 動作中，將分別發出 OpenID Connect 挑戰和登出要求。</span><span class="sxs-lookup"><span data-stu-id="99f63-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="99f63-143">現在，請開啟 `Views\Shared\_LoginPartial.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="99f63-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="99f63-144">這裡是您向使用者顯示應用程式的登入和登出連結，以及在檢視中列印出使用者名稱的位置。</span><span class="sxs-lookup"><span data-stu-id="99f63-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="99f63-145">顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="99f63-145">Display user information</span></span>
<span data-ttu-id="99f63-146">使用 OpenID Connect 來驗證使用者時，v2.0 端點會將 id_token 傳回給包含使用者相關宣告或判斷提示的應用程式。</span><span class="sxs-lookup"><span data-stu-id="99f63-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="99f63-147">您可以使用這些宣告來個人化應用程式：</span><span class="sxs-lookup"><span data-stu-id="99f63-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="99f63-148">開啟 `Controllers\HomeController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="99f63-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="99f63-149">您可以透過 `ClaimsPrincipal.Current` 安全性主體物件來存取控制器中的使用者宣告。</span><span class="sxs-lookup"><span data-stu-id="99f63-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="99f63-150">執行</span><span class="sxs-lookup"><span data-stu-id="99f63-150">Run</span></span>
<span data-ttu-id="99f63-151">最後，建置並執行您的應用程式！</span><span class="sxs-lookup"><span data-stu-id="99f63-151">Finally, build and run your app!</span></span>   <span data-ttu-id="99f63-152">使用個人 Microsoft 帳戶或工作或學校帳戶登入，並注意上方導覽列中使用者身分識別的反映狀態。</span><span class="sxs-lookup"><span data-stu-id="99f63-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="99f63-153">您的 Web 應用程式現在使用業界標準的通訊協定保護，可以使用個人與工作/學校帳戶來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="99f63-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="99f63-154">如需參考， [此處以 .zip 格式提供](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip)完整範例 (不含您的組態值)，您也可以從 GitHub 將其複製：</span><span class="sxs-lookup"><span data-stu-id="99f63-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="99f63-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99f63-155">Next steps</span></span>
<span data-ttu-id="99f63-156">您現在可以進入更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="99f63-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="99f63-157">您可以嘗試：</span><span class="sxs-lookup"><span data-stu-id="99f63-157">You may want to try:</span></span>

[<span data-ttu-id="99f63-158">使用 v2.0 端點保護 Web API >></span><span class="sxs-lookup"><span data-stu-id="99f63-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="99f63-159">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="99f63-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="99f63-160">v2.0 開發人員指南 >></span><span class="sxs-lookup"><span data-stu-id="99f63-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="99f63-161">StackOverflow "azure-active-directory" 標籤 >></span><span class="sxs-lookup"><span data-stu-id="99f63-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="99f63-162">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="99f63-162">Get security updates for our products</span></span>
<span data-ttu-id="99f63-163">我們鼓勵您造訪 [此頁面](https://technet.microsoft.com/security/dd252948) 並訂閱資訊安全摘要報告警示，以在安全性事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="99f63-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
