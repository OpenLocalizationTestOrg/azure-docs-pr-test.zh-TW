---
title: "Azure AD .NET Web 應用程式入門 | Microsoft Docs"
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="c4caf-103">使用 Azure AD 來進行 ASP.NET Web 應用程式登入和登出</span><span class="sxs-lookup"><span data-stu-id="c4caf-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="c4caf-104">Azure Active Directory (Azure AD) 透過以幾行程式碼提供單一登入和登出功能，讓您能夠輕鬆將 Web 應用程式身分識別管理外包。</span><span class="sxs-lookup"><span data-stu-id="c4caf-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="c4caf-105">您可以藉由使用 Microsoft 的 Open Web Interface for .NET (OWIN) 中介軟體實作，將使用者登入和登出 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4caf-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="c4caf-106">社群導向 OWIN 中介軟體包含在 .NET Framework 4.5 中。</span><span class="sxs-lookup"><span data-stu-id="c4caf-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="c4caf-107">本文說明如何使用 OWIN 來執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="c4caf-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="c4caf-108">藉由使用 Azure AD 作為身分識別提供者，將使用者登入 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4caf-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="c4caf-109">顯示部分使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="c4caf-109">Display some user information.</span></span>
* <span data-ttu-id="c4caf-110">將使用者登出應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4caf-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="c4caf-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="c4caf-111">Before you get started</span></span>
* <span data-ttu-id="c4caf-112">下載[應用程式基本架構](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip)或下載[完整的範例](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="c4caf-113">您還需要一個可供註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c4caf-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="c4caf-114">如果您還沒有 Azure AD 租用戶，請[了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="c4caf-115">當您準備就緒時，請依照接下來四個小節的程序操作。</span><span class="sxs-lookup"><span data-stu-id="c4caf-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="c4caf-116">步驟 1︰向 Azure AD 註冊新的應用程式</span><span class="sxs-lookup"><span data-stu-id="c4caf-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="c4caf-117">若要設定應用程式以驗證使用者，請先藉由執行下列操作，在您的租用戶中註冊該應用程式︰</span><span class="sxs-lookup"><span data-stu-id="c4caf-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="c4caf-118">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c4caf-119">在頂端列中，按一下您的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="c4caf-119">On the top bar, click your account name.</span></span> <span data-ttu-id="c4caf-120">在 [目錄] 清單下，選取您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c4caf-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="c4caf-121">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="c4caf-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c4caf-122">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c4caf-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="c4caf-123">依照提示來建立新的「Web 應用程式和/或 Web API」。</span><span class="sxs-lookup"><span data-stu-id="c4caf-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="c4caf-124">[名稱] 可向使用者描述該應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4caf-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="c4caf-125">[登入 URL] 是應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="c4caf-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="c4caf-126">基本架構的預設 URL 是 https://localhost:44320/。</span><span class="sxs-lookup"><span data-stu-id="c4caf-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="c4caf-127">完成註冊之後，Azure AD 會為應用程式指派一個唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c4caf-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="c4caf-128">請從應用程式頁面複製該值，以在接下來的小節中使用。</span><span class="sxs-lookup"><span data-stu-id="c4caf-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="c4caf-129">從應用程式的 [設定]  ->  [屬性] 頁面，更新應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="c4caf-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="c4caf-130">[應用程式識別碼 URI] 是應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="c4caf-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="c4caf-131">命名慣例是 `https://<tenant-domain>/<app-name>` (例如 `https://contoso.onmicrosoft.com/my-first-aad-app`)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="c4caf-132">步驟 2：設定應用程式以使用 OWIN 驗證管線</span><span class="sxs-lookup"><span data-stu-id="c4caf-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="c4caf-133">在此步驟中，您將設定 OWIN 中介軟體以使用 OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="c4caf-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="c4caf-134">您將使用 OWIN 來發出登入和登出要求、管理使用者工作階段、取得使用者資訊等等。</span><span class="sxs-lookup"><span data-stu-id="c4caf-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="c4caf-135">若要開始進行，請使用「套件管理器主控台」將 OWIN 中介軟體 NuGet 套件新增到專案中。</span><span class="sxs-lookup"><span data-stu-id="c4caf-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="c4caf-136">若要將 OWIN 啟動類別新增到名為 `Startup.cs` 的專案中，請在專案上按一下滑鼠右鍵，依序選取 [新增]、[新增項目]，然後搜尋 **OWIN**。</span><span class="sxs-lookup"><span data-stu-id="c4caf-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="c4caf-137">OWIN 中介軟體會在應用程式啟動時叫用 **Configuration(...)** 方法。</span><span class="sxs-lookup"><span data-stu-id="c4caf-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="c4caf-138">將類別宣告變更為 `public partial class Startup`。</span><span class="sxs-lookup"><span data-stu-id="c4caf-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="c4caf-139">我們已在另一個檔案中為您實作此類別的一部分。</span><span class="sxs-lookup"><span data-stu-id="c4caf-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="c4caf-140">請在 **Configuration(...)** 方法中，呼叫 **ConfgureAuth(...)** 來為應用程式設定驗證。</span><span class="sxs-lookup"><span data-stu-id="c4caf-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="c4caf-141">開啟 App_Start\Startup.Auth.cs 檔案，然後實作 **ConfigureAuth(...)** 方法。</span><span class="sxs-lookup"><span data-stu-id="c4caf-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="c4caf-142">您在 *OpenIDConnectAuthenticationOptions* 中提供的參數會作為供應用程式與 Azure AD 進行通訊的座標。</span><span class="sxs-lookup"><span data-stu-id="c4caf-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="c4caf-143">您還必須設定 Cookie 驗證，因為 OpenID Connect 中介軟體會在背景中使用 Cookie。</span><span class="sxs-lookup"><span data-stu-id="c4caf-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="c4caf-144">開啟專案根目錄中的 web.config 檔案，然後在 `<appSettings>` 區段中輸入組態值。</span><span class="sxs-lookup"><span data-stu-id="c4caf-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="c4caf-145">`ida:ClientId`：您在「步驟 1：向 Azure AD 註冊新的應用程式」中從 Azure 入口網站複製的 GUID。</span><span class="sxs-lookup"><span data-stu-id="c4caf-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="c4caf-146">`ida:Tenant`：您 Azure AD 租用戶的名稱 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="c4caf-147">`ida:PostLogoutRedirectUri`：告訴 Azure AD 在順利完成登出要求後應將使用者重新導向到何處的指標。</span><span class="sxs-lookup"><span data-stu-id="c4caf-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="c4caf-148">步驟 3：使用 OWIN 向 Azure AD 發出登入和登出要求</span><span class="sxs-lookup"><span data-stu-id="c4caf-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="c4caf-149">應用程式現已設定妥當，可使用 OpenID Connect 驗證通訊協定來與 Azure AD 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="c4caf-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="c4caf-150">OWIN 已處理有關製作驗證訊息、驗證來自 Azure AD 的權杖及維護使用者工作階段的一切細節。</span><span class="sxs-lookup"><span data-stu-id="c4caf-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="c4caf-151">剩餘的工作就是提供使用者一個登入和登出的方式。</span><span class="sxs-lookup"><span data-stu-id="c4caf-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="c4caf-152">您可以在控制器中使用授權標籤，以要求使用者在存取特定頁面時先登入。</span><span class="sxs-lookup"><span data-stu-id="c4caf-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="c4caf-153">若要這麼做，請開啟 Controllers\HomeController.cs，然後將 `[Authorize]` 標籤新增到 About 控制器中。</span><span class="sxs-lookup"><span data-stu-id="c4caf-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="c4caf-154">您也可以使用 OWIN 從程式碼中直接發出驗證要求。</span><span class="sxs-lookup"><span data-stu-id="c4caf-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="c4caf-155">若要這麼做，請開啟 Controllers\AccountController.cs。</span><span class="sxs-lookup"><span data-stu-id="c4caf-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="c4caf-156">然後在 SignIn() 和 SignOut() 動作中，發出 OpenID Connect 挑戰和登出要求。</span><span class="sxs-lookup"><span data-stu-id="c4caf-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="c4caf-157">開啟 Views\Shared\_LoginPartial.cshtml 以向使用者顯示應用程式登入和登出連結，並在檢視中列印出使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="c4caf-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="c4caf-158">步驟 4：顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="c4caf-158">Step 4: Display user information</span></span>
<span data-ttu-id="c4caf-159">當 Azure AD 向 OpenID Connect 驗證使用者時，會將包含「宣告」或使用者相關判斷提示的 id_token 傳回給應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4caf-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="c4caf-160">您可以藉由執行下列操作，使用這些宣告將應用程式個人化：</span><span class="sxs-lookup"><span data-stu-id="c4caf-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="c4caf-161">開啟 Controllers\HomeController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="c4caf-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="c4caf-162">您可以透過 `ClaimsPrincipal.Current` 安全性主體物件來存取控制器中的使用者宣告。</span><span class="sxs-lookup"><span data-stu-id="c4caf-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="c4caf-163">建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4caf-163">Build and run the app.</span></span> <span data-ttu-id="c4caf-164">如果您尚未在網域為 onmicrosoft.com 的租用戶中建立新使用者，現在便可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="c4caf-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="c4caf-165">方式如下：</span><span class="sxs-lookup"><span data-stu-id="c4caf-165">Here's how:</span></span>

  <span data-ttu-id="c4caf-166">a.</span><span class="sxs-lookup"><span data-stu-id="c4caf-166">a.</span></span> <span data-ttu-id="c4caf-167">以該使用者身分登入，並注意頂端列上所反映的使用者身分識別。</span><span class="sxs-lookup"><span data-stu-id="c4caf-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="c4caf-168">b.</span><span class="sxs-lookup"><span data-stu-id="c4caf-168">b.</span></span> <span data-ttu-id="c4caf-169">登出，然後在您的租用戶中以另一個使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="c4caf-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="c4caf-170">c.</span><span class="sxs-lookup"><span data-stu-id="c4caf-170">c.</span></span> <span data-ttu-id="c4caf-171">如果想再多進行一些操作，您還可以註冊並執行此應用程式的另一個執行個體 (使用其自己的 clientId)，然後監看單一登入的運作情況。</span><span class="sxs-lookup"><span data-stu-id="c4caf-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4caf-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4caf-172">Next steps</span></span>
<span data-ttu-id="c4caf-173">如需參考資料，請參閱[完整的範例](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (不含您的組態值)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="c4caf-174">您現在可以繼續前進到更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="c4caf-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="c4caf-175">例如，嘗試[使用 Azure AD 來保護 Web API](active-directory-devquickstarts-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="c4caf-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
