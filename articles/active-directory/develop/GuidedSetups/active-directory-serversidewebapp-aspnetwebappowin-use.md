---
title: "Azure AD v2 ASP.NET Web 伺服器快速入門 - 使用 | Microsoft Docs"
description: "使用 OpenID Connect 標準，搭配傳統網頁瀏覽器型應用程式，在 ASP.NET 方案上實作 Microsoft 登入"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 3b7d29e48c91f40e8782a5e32a52998b815fe331
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="add-a-controller-to-handle-sign-in-and-sign-out-requests"></a><span data-ttu-id="dd824-103">新增控制器以處理登入和登出要求</span><span class="sxs-lookup"><span data-stu-id="dd824-103">Add a controller to handle sign-in and sign-out requests</span></span>

<span data-ttu-id="dd824-104">這個步驟說明如何建立新的控制器來公開登入和登出方法。</span><span class="sxs-lookup"><span data-stu-id="dd824-104">This step shows how to create a new controller to expose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="dd824-105">以滑鼠右鍵按一下 `Controllers` 資料夾並選取 `Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="dd824-105">Right click the `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="dd824-106">選取 `MVC (.NET version) Controller – Empty`。</span><span class="sxs-lookup"><span data-stu-id="dd824-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="dd824-107">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="dd824-107">Click *Add*</span></span>
4.  <span data-ttu-id="dd824-108">將它命名為 `HomeController`，然後按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="dd824-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="dd824-109">新增 *OWIN* 參考至類別：</span><span class="sxs-lookup"><span data-stu-id="dd824-109">Add *OWIN* references to the class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="dd824-110">新增下面兩種方法來透過經由程式碼起始驗證挑戰的方式，處理控制器的登入和登出：</span><span class="sxs-lookup"><span data-stu-id="dd824-110">Add the two methods below to handle sign-in and sign-out to your controller by initiating an authentication challenge via code:</span></span>
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate the SignIn method with the [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-the-apps-home-page-to-sign-in-users-via-a-sign-in-button"></a><span data-ttu-id="dd824-111">建立應用程式的首頁來透過登入按鈕將使用者登入</span><span class="sxs-lookup"><span data-stu-id="dd824-111">Create the app's home page to sign in users via a sign-in button</span></span>

<span data-ttu-id="dd824-112">在 Visual Studio 中建立新的檢視來新增登入按鈕，並在驗證之後顯示使用者資訊：</span><span class="sxs-lookup"><span data-stu-id="dd824-112">In Visual Studio, create a new view to add the sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="dd824-113">以滑鼠右鍵按一下 `Views\Home` 資料夾並選取 `Add View`</span><span class="sxs-lookup"><span data-stu-id="dd824-113">Right click the `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="dd824-114">將它命名為 `Index`</span><span class="sxs-lookup"><span data-stu-id="dd824-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="dd824-115">在以下檔案中新增下列 HTML (包括登入按鈕)：</span><span class="sxs-lookup"><span data-stu-id="dd824-115">Add the following HTML, which includes the sign-in button, to the file:</span></span>

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If the user is not authenticated, display the sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="dd824-116">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="dd824-116">More Information</span></span>
> <span data-ttu-id="dd824-117">此頁面會以 SVG 格式新增一個具有黑色背景的登入按鈕：</span><span class="sxs-lookup"><span data-stu-id="dd824-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="dd824-118">![使用 Microsoft 登入](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="dd824-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="dd824-119">如需更多登入按鈕。請前往[此頁面](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines")。</span><span class="sxs-lookup"><span data-stu-id="dd824-119">For more sign-in buttons, please go to the [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-to-display-users-claims"></a><span data-ttu-id="dd824-120">新增控制器來顯示使用者的宣告</span><span class="sxs-lookup"><span data-stu-id="dd824-120">Add a controller to display user's claims</span></span>
<span data-ttu-id="dd824-121">此控制器示範如何使用 `[Authorize]` 屬性來保護控制器。</span><span class="sxs-lookup"><span data-stu-id="dd824-121">This controller demonstrates the uses of the `[Authorize]` attribute to protect a controller.</span></span> <span data-ttu-id="dd824-122">此屬性會設定限制，只允許經過驗證的使用者存取控制器。</span><span class="sxs-lookup"><span data-stu-id="dd824-122">This attribute restricts access to the controller by only allowing authenticated users.</span></span> <span data-ttu-id="dd824-123">下面的程式碼會利用屬性來顯示在登入過程中擷取的使用者宣告。</span><span class="sxs-lookup"><span data-stu-id="dd824-123">The code below makes use of the attribute to display user claims that were retrieved as part of the sign-in.</span></span>

1.  <span data-ttu-id="dd824-124">以滑鼠右鍵按一下 `Controllers` 資料夾：`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="dd824-124">Right click the `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="dd824-125">選取 `MVC {version} Controller – Empty`。</span><span class="sxs-lookup"><span data-stu-id="dd824-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="dd824-126">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="dd824-126">Click *Add*</span></span>
4.  <span data-ttu-id="dd824-127">將它命名為 `ClaimsController`</span><span class="sxs-lookup"><span data-stu-id="dd824-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="dd824-128">以下面的程式碼取代您控制器類別的程式碼 ，這會將 `[Authorize]` 屬性新增至類別：</span><span class="sxs-lookup"><span data-stu-id="dd824-128">Replace the code of your controller class with the code below - this adds the `[Authorize]` attribute to the class:</span></span>

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims to viewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get the user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // The 'preferred_username' claim can be used for showing the username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // The subject claim can be used to uniquely identify the user across the web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is the unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="dd824-129">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="dd824-129">More Information</span></span>
> <span data-ttu-id="dd824-130">因為使用了 `[Authorize]` 屬性，所以此控制器的所有方法都只能在使用者已通過驗證的情況下才能執行。</span><span class="sxs-lookup"><span data-stu-id="dd824-130">Because of the use of the `[Authorize]` attribute, all methods of this controller can only be executed if the user is authenticated.</span></span> <span data-ttu-id="dd824-131">如果使用者未通過驗證且嘗試存取控制器，OWIN 會起始一個驗證挑戰，並強制使用者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="dd824-131">If the user is not authenticated and tries to access the controller, OWIN will initiate an authentication challenge and force the user to authenticate.</span></span> <span data-ttu-id="dd824-132">上面的程式碼會查看 `ClaimsPrincipal.Current` 執行個體的宣告集合，以尋找使用者權杖中所包含的特定使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="dd824-132">The code above looks at the claims collection of the `ClaimsPrincipal.Current` instance for specific user attributes included in the user’s token.</span></span> <span data-ttu-id="dd824-133">這些屬性包括使用者的完整名稱和使用者名稱，以及全域使用者識別元主體。</span><span class="sxs-lookup"><span data-stu-id="dd824-133">These attributes include the user’s full name and username, as well as the global user identifier subject.</span></span> <span data-ttu-id="dd824-134">它也包含「租用戶識別碼」，這代表使用者所屬組織的識別碼。</span><span class="sxs-lookup"><span data-stu-id="dd824-134">It also contains the *Tenant ID*, which represents the ID for the user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-to-display-the-users-claims"></a><span data-ttu-id="dd824-135">建立檢視來顯示使用者的宣告</span><span class="sxs-lookup"><span data-stu-id="dd824-135">Create a view to display the user's claims</span></span>

<span data-ttu-id="dd824-136">在 Visual Studio 中，建立新的檢視以在網頁中顯示使用者的宣告：</span><span class="sxs-lookup"><span data-stu-id="dd824-136">In Visual Studio, create a new view to display the user's claims in a web page:</span></span>

1.  <span data-ttu-id="dd824-137">以滑鼠右鍵按一下 `Views\Claims` 資料夾，然後按一下：`Add View`</span><span class="sxs-lookup"><span data-stu-id="dd824-137">Right click the `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="dd824-138">將它命名為 `Index`</span><span class="sxs-lookup"><span data-stu-id="dd824-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="dd824-139">將下列 HTML 新增至檔案：</span><span class="sxs-lookup"><span data-stu-id="dd824-139">Add the following HTML to the file:</span></span>

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
