---
title: "aaaAzure AD.NET web 應用程式使用者入門 |Microsoft 文件"
description: "建置與 Azure AD 整合來進行登入的 .NET MVC Web 應用程式。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="6e01b-103">使用 Azure AD 來進行 ASP.NET Web 應用程式登入和登出</span><span class="sxs-lookup"><span data-stu-id="6e01b-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="6e01b-104">藉由提供單一登入和登出只有幾行程式碼，Azure Active Directory (Azure AD) 可簡化您 toooutsource web 應用程式身分識別管理。</span><span class="sxs-lookup"><span data-stu-id="6e01b-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="6e01b-105">您可以使用.NET (OWIN) 中介軟體 hello Microsoft 開啟 Web 介面的實作來登入和移出 ASP.NET web 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="6e01b-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="6e01b-106">社群導向 OWIN 中介軟體包含在 .NET Framework 4.5 中。</span><span class="sxs-lookup"><span data-stu-id="6e01b-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="6e01b-107">本文將說明如何 toouse OWIN 至：</span><span class="sxs-lookup"><span data-stu-id="6e01b-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="6e01b-108">登入 tooweb hello 身分識別提供者以使用 Azure AD 的應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="6e01b-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="6e01b-109">顯示部分使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="6e01b-109">Display some user information.</span></span>
* <span data-ttu-id="6e01b-110">登入超出 hello 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="6e01b-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="6e01b-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="6e01b-111">Before you get started</span></span>
* <span data-ttu-id="6e01b-112">下載 hello[應用程式的基本架構](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip)或下載 hello[完成的範例](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="6e01b-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="6e01b-113">您也需要哪些 tooregister hello 應用程式中的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6e01b-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="6e01b-114">如果您還沒有 Azure AD 租用戶[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="6e01b-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="6e01b-115">當您準備好時，後續 hello 程序在 hello 接下來四個區段。</span><span class="sxs-lookup"><span data-stu-id="6e01b-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="6e01b-116">步驟 1： 使用 Azure AD 註冊 hello 新應用程式</span><span class="sxs-lookup"><span data-stu-id="6e01b-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="6e01b-117">tooset tooauthenticate hello 應用程式的使用者，第一次該租用戶中登錄執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6e01b-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="6e01b-118">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6e01b-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6e01b-119">Hello 頂端列上，按一下您的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6e01b-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="6e01b-120">在 hello**目錄**清單中，選取 hello Active Directory 租用戶想 tooregister hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e01b-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="6e01b-121">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="6e01b-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="6e01b-122">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6e01b-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="6e01b-123">請遵循 hello 提示新 toocreate **Web 應用程式和/或 WebAPI**。</span><span class="sxs-lookup"><span data-stu-id="6e01b-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="6e01b-124">**名稱**描述 hello 應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="6e01b-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="6e01b-125">**登入 URL**是 hello hello 應用程式基底 URL。</span><span class="sxs-lookup"><span data-stu-id="6e01b-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="6e01b-126">hello 基本架構的預設 URL 為 https://localhost:44320 /。</span><span class="sxs-lookup"><span data-stu-id="6e01b-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="6e01b-127">Hello 註冊完成之後，Azure AD 會指派給 hello 應用程式是唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="6e01b-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="6e01b-128">複製 hello 下一節中的 hello 應用程式頁面 toouse hello 值。</span><span class="sxs-lookup"><span data-stu-id="6e01b-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="6e01b-129">從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="6e01b-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="6e01b-130">hello**應用程式識別碼 URI**是 hello 應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="6e01b-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="6e01b-131">hello 命名慣例是`https://<tenant-domain>/<app-name>`(例如， `https://contoso.onmicrosoft.com/my-first-aad-app`)。</span><span class="sxs-lookup"><span data-stu-id="6e01b-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="6e01b-132">步驟 2： 設定 hello 應用程式 toouse hello OWIN 驗證管線</span><span class="sxs-lookup"><span data-stu-id="6e01b-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="6e01b-133">在此步驟中，您可以設定 hello OWIN 中介軟體 toouse hello OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="6e01b-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6e01b-134">您使用 OWIN tooissue 登入和登出要求、 管理使用者工作階段、 取得使用者資訊等等。</span><span class="sxs-lookup"><span data-stu-id="6e01b-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="6e01b-135">toobegin，利用 hello Package Manager Console 中新增 hello OWIN 中介軟體 NuGet 封裝 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="6e01b-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="6e01b-136">OWIN 啟動 「 類別 toohello 專案呼叫的 tooadd `Startup.cs`hello 專案上按一下滑鼠右鍵、 選取**新增**，選取**新項目**，然後搜尋**OWIN**。</span><span class="sxs-lookup"><span data-stu-id="6e01b-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="6e01b-137">hello OWIN 中介軟體會叫用 hello **Configuration(...)** hello 應用程式啟動時的方法。</span><span class="sxs-lookup"><span data-stu-id="6e01b-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="6e01b-138">也變更 hello 類別宣告`public partial class Startup`。</span><span class="sxs-lookup"><span data-stu-id="6e01b-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="6e01b-139">我們已在另一個檔案中為您實作此類別的一部分。</span><span class="sxs-lookup"><span data-stu-id="6e01b-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="6e01b-140">在 hello **Configuration(...)**方法，呼叫太**ConfgureAuth(...)** tooset hello 應用程式的驗證設定。</span><span class="sxs-lookup"><span data-stu-id="6e01b-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="6e01b-141">開啟 hello App_Start\Startup.Auth.cs 檔案，並接著實作 hello **ConfigureAuth(...)**方法。</span><span class="sxs-lookup"><span data-stu-id="6e01b-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="6e01b-142">hello 的參數中提供*OpenIDConnectAuthenticationOptions*做為 hello 與 Azure AD 的應用程式 toocommunicate 座標。</span><span class="sxs-lookup"><span data-stu-id="6e01b-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="6e01b-143">您也需要 tooset 出的 cookie 驗證，因為 hello OpenID Connect 中介軟體 hello 背景中使用 cookie。</span><span class="sxs-lookup"><span data-stu-id="6e01b-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="6e01b-144">Hello hello 專案根目錄中開啟 hello web.config 檔案，然後輸入 hello 中的 hello 組態值`<appSettings>`> 一節。</span><span class="sxs-lookup"><span data-stu-id="6e01b-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="6e01b-145">`ida:ClientId`: hello GUID hello 從複製在 Azure 入口網站 」 步驟 1： 註冊 hello 新應用程式與 Azure AD。 」</span><span class="sxs-lookup"><span data-stu-id="6e01b-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="6e01b-146">`ida:Tenant`: hello 名稱，您的 Azure AD 租用戶 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="6e01b-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="6e01b-147">`ida:PostLogoutRedirectUri`: hello 指標，會告訴 Azure AD，使用者應該重新導向之後登出要求順利完成。</span><span class="sxs-lookup"><span data-stu-id="6e01b-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="6e01b-148">步驟 3： 使用 OWIN tooissue 登入和登出要求 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="6e01b-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="6e01b-149">hello 應用程式是現在已正確設定的 toocommunicate 與 Azure AD 使用 hello OpenID Connect 的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="6e01b-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6e01b-150">OWIN 已經處理過所有 hello 製作驗證訊息、 驗證 Azure ad 的權杖和維護使用者工作階段的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6e01b-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="6e01b-151">所有會維持為您的使用者是 toogive 方式 toosign 中的並登出。</span><span class="sxs-lookup"><span data-stu-id="6e01b-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="6e01b-152">您可以使用存取特定網頁前授權在您控制站 toorequire 使用者 toosign 中的標記。</span><span class="sxs-lookup"><span data-stu-id="6e01b-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="6e01b-153">toodo，開啟 Controllers\HomeController.cs，，然後加入 hello`[Authorize]`標記 toohello 有關控制站。</span><span class="sxs-lookup"><span data-stu-id="6e01b-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="6e01b-154">您也可以在程式碼中使用從 OWIN toodirectly 發出驗證要求。</span><span class="sxs-lookup"><span data-stu-id="6e01b-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="6e01b-155">toodo，請開啟 Controllers\AccountController.cs。</span><span class="sxs-lookup"><span data-stu-id="6e01b-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="6e01b-156">然後，在 hello SignIn() 和 Signout 動作，會發出 OpenID Connect 的挑戰和登出要求。</span><span class="sxs-lookup"><span data-stu-id="6e01b-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="6e01b-157">開啟 _layout.cshtml\_LoginPartial.cshtml tooshow hello 使用者 hello 應用程式登入和登出連結和 tooprint 出檢視中的 hello 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="6e01b-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="6e01b-158">步驟 4：顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="6e01b-158">Step 4: Display user information</span></span>
<span data-ttu-id="6e01b-159">它會驗證使用者使用 OpenID Connect，Azure AD 會傳回 id_token toohello 應用程式包含 「 宣告 」 或有關 hello 使用者判斷提示。</span><span class="sxs-lookup"><span data-stu-id="6e01b-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="6e01b-160">您可以使用這些宣告 toopersonalize hello 應用程式執行 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="6e01b-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="6e01b-161">開啟 hello Controllers\HomeController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="6e01b-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="6e01b-162">您可以在 hello 透過您控制站存取 hello 使用者宣告`ClaimsPrincipal.Current`安全性主體物件。</span><span class="sxs-lookup"><span data-stu-id="6e01b-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="6e01b-163">建置並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e01b-163">Build and run hello app.</span></span> <span data-ttu-id="6e01b-164">如果您尚未使用 onmicrosoft.com 網域的租用戶中建立新的使用者，現在是 hello 時間 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="6e01b-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="6e01b-165">方式如下：</span><span class="sxs-lookup"><span data-stu-id="6e01b-165">Here's how:</span></span>

  <span data-ttu-id="6e01b-166">a.</span><span class="sxs-lookup"><span data-stu-id="6e01b-166">a.</span></span> <span data-ttu-id="6e01b-167">使用該使用者登入，並請注意如何 hello 使用者的身分識別會反映在 hello 頂端列。</span><span class="sxs-lookup"><span data-stu-id="6e01b-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="6e01b-168">b.</span><span class="sxs-lookup"><span data-stu-id="6e01b-168">b.</span></span> <span data-ttu-id="6e01b-169">登出，然後在您的租用戶中以另一個使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="6e01b-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="6e01b-170">c.</span><span class="sxs-lookup"><span data-stu-id="6e01b-170">c.</span></span> <span data-ttu-id="6e01b-171">如果想再多進行一些操作，您還可以註冊並執行此應用程式的另一個執行個體 (使用其自己的 clientId)，然後監看單一登入的運作情況。</span><span class="sxs-lookup"><span data-stu-id="6e01b-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e01b-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e01b-172">Next steps</span></span>
<span data-ttu-id="6e01b-173">如需參考，請參閱[hello 完成範例](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)（不含您的組態值）。</span><span class="sxs-lookup"><span data-stu-id="6e01b-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="6e01b-174">您現在可以繼續 toomore 進階主題。</span><span class="sxs-lookup"><span data-stu-id="6e01b-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="6e01b-175">例如，嘗試[使用 Azure AD 來保護 Web API](active-directory-devquickstarts-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="6e01b-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
