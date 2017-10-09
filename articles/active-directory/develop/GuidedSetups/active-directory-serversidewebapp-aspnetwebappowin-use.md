---
title: "aaaAzure AD v2 ASP.NET Web 伺服器快速入門-使用 |Microsoft 文件"
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
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>加入控制器 toohandle 登入和登出要求

這個步驟顯示如何 toocreate 新的控制器 tooexpose 登入和登出的方法。

1.  以滑鼠右鍵按一下 hello`Controllers`資料夾，然後選取`Add` > `Controller`
2.  選取 `MVC (.NET version) Controller – Empty`。
3.  按一下 [新增]
4.  將它命名為 `HomeController`，然後按一下 [新增]
5.  新增*OWIN*參考 toohello 類別：

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
起始驗證要求，透過程式碼中加入以下 toohandle 登入和登出 tooyour 控制器的 hello 兩個方法：
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
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

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>在 使用者 透過登入 按鈕建立 hello 應用程式首頁 toosign

在 Visual Studio 中，建立新檢視 tooadd hello 登入 按鈕，並顯示在驗證後的使用者資訊：

1.  以滑鼠右鍵按一下 hello`Views\Home`資料夾，然後選取`Add View`
2.  將它命名為 `Index`
3.  新增下列 HTML，其中包括 hello 登入 按鈕，toohello 檔案的 hello:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
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
### <a name="more-information"></a>相關資訊
> 此頁面會以 SVG 格式新增一個具有黑色背景的登入按鈕：<br/>![使用 Microsoft 登入](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> 如需詳細的登入按鈕，請移 toohello[本頁](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "的商標指導")。
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>新增控制器 toodisplay 使用者宣告
此控制站會示範使用 hello hello`[Authorize]`屬性 tooprotect 控制站。 這個屬性會限制只允許已驗證的使用者存取 toohello 控制站。 下列程式碼的 hello hello 屬性 toodisplay 使用者宣告擷取 hello 登入的一部分使用。

1.  以滑鼠右鍵按一下 hello`Controllers`資料夾：`Add` > `Controller`
2.  選取 `MVC {version} Controller – Empty`。
3.  按一下 [新增]
4.  將它命名為 `ClaimsController`
5.  Hello 程式碼取代這會加入控制器類別與 hello 的以下的程式碼的 hello`[Authorize]`屬性 toohello 類別：

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>相關資訊
> 因為 hello hello 使用`[Authorize]`如果 hello 使用者通過驗證，才可執行屬性，此控制站的所有方法。 如果 hello 使用者未經過驗證，且嘗試 tooaccess hello 控制站，OWIN 會起始驗證要求，並強制 hello 使用者 tooauthenticate。 hello 探討 hello 上面的程式碼的宣告集合的 hello `ClaimsPrincipal.Current` hello 使用者的權杖中包含的特定使用者屬性的執行個體。 這些屬性包括 hello 使用者的完整名稱和使用者名稱，以及 hello 全域使用者識別碼的主體。 它也包含 hello*租用戶識別碼*，代表 hello 使用者的組織識別碼 hello。 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>建立檢視 toodisplay hello 使用者的宣告

在 Visual Studio 中，建立新的檢視在網頁中的 toodisplay hello 使用者的宣告：

1.  以滑鼠右鍵按一下 hello`Views\Claims`資料夾和：`Add View`
2.  將它命名為 `Index`
3.  加入下列 HTML toohello 檔 hello:

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
