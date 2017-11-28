---
title: "aaaAdd 登入 tooa.NET MVC web 應用程式開發介面使用 hello Azure AD v2.0 端點 |Microsoft 文件"
description: "如何 toobuild.NET MVC Web 應用程式開發介面可接受來自這兩個個人 Microsoft 帳戶的語彙基元和工作或學校帳戶。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="b139a-103">保護 MVC web API</span><span class="sxs-lookup"><span data-stu-id="b139a-103">Secure an MVC web API</span></span>
<span data-ttu-id="b139a-104">使用 Azure Active Directory hello v2.0 端點，您可以保護 Web 應用程式開發介面使用[OAuth 2.0](active-directory-v2-protocols.md)啟用具有兩個人的 Microsoft 帳戶的使用者和工作或學校帳戶 toosecurely 存取 Web API 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="b139a-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="b139a-105">並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="b139a-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="b139a-106">toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="b139a-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="b139a-107">在 ASP.NET Web API 中，您可以使用隨附於 .NET Framework 4.5 的 Microsoft OWIN 中介軟體來完成此項作業。</span><span class="sxs-lookup"><span data-stu-id="b139a-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="b139a-108">這裡我們將使用 OWIN toobuild"tooDo 清單 」 MVC Web API，可讓用戶端 toocreate 與讀取的工作，從使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="b139a-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="b139a-109">hello web API 將會驗證連入要求包含有效存取權杖，並拒絕任何受保護的路由，無法通過驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="b139a-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="b139a-110">這個範例是使用 Visual Studio 2015 建置的。</span><span class="sxs-lookup"><span data-stu-id="b139a-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="b139a-111">下載</span><span class="sxs-lookup"><span data-stu-id="b139a-111">Download</span></span>
<span data-ttu-id="b139a-112">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="b139a-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="b139a-113">您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip)或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="b139a-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="b139a-114">hello 基本架構應用程式簡單的 api，包括所有 hello 未定案程式碼，但是遺漏之所有 hello 身分識別相關的片段。</span><span class="sxs-lookup"><span data-stu-id="b139a-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="b139a-115">若您不想沿著 toofollow，可改為複製或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="b139a-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="b139a-116">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="b139a-116">Register an app</span></span>
<span data-ttu-id="b139a-117">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="b139a-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="b139a-118">請確定：</span><span class="sxs-lookup"><span data-stu-id="b139a-118">Make sure to:</span></span>

* <span data-ttu-id="b139a-119">複製下 hello**應用程式識別碼**指派 tooyour 應用程式，您將需要它過期。</span><span class="sxs-lookup"><span data-stu-id="b139a-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="b139a-120">本 Visual Studio 方案也包含了「TodoListClient」，這是一個簡單的 WPF 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b139a-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="b139a-121">hello TodoListClient 是如何在使用者登入時使用的 toodemonstrate，且用戶端可以發出如何要求 tooyour Web API。</span><span class="sxs-lookup"><span data-stu-id="b139a-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="b139a-122">在此情況下，hello TodoListClient 和 hello TodoListService 都由 hello 相同的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b139a-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="b139a-123">tooconfigure hello TodoListClient，您也應該：</span><span class="sxs-lookup"><span data-stu-id="b139a-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="b139a-124">新增 hello**行動**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b139a-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="b139a-125">安裝 OWIN</span><span class="sxs-lookup"><span data-stu-id="b139a-125">Install OWIN</span></span>
<span data-ttu-id="b139a-126">既然您已註冊的應用程式，您需要 tooset 註冊您的應用程式 toocommunicate hello v2.0 與中的端點順序 toovalidate 連入要求 （& s） 權杖。</span><span class="sxs-lookup"><span data-stu-id="b139a-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="b139a-127">toobegin，開啟 hello 方案，並加入 hello OWIN 中介軟體 NuGet 封裝 toohello TodoListService 專案使用 Package Manager Console hello。</span><span class="sxs-lookup"><span data-stu-id="b139a-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="b139a-128">設定 OAuth 驗證</span><span class="sxs-lookup"><span data-stu-id="b139a-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="b139a-129">新增稱為 OWIN 啟動 「 類別 toohello TodoListService 專案`Startup.cs`。</span><span class="sxs-lookup"><span data-stu-id="b139a-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="b139a-130">--> Hello 專案上的按一下滑鼠右鍵**新增** --> **新項目**--> 搜尋"OWIN"。</span><span class="sxs-lookup"><span data-stu-id="b139a-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="b139a-131">hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="b139a-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="b139a-132">也變更 hello 類別宣告`public partial class Startup`-我們已實作了此類別的一部分，另一個檔案中。</span><span class="sxs-lookup"><span data-stu-id="b139a-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="b139a-133">在 hello`Configuration(…)`方法，請呼叫 tooConfgureAuth(...) tooset 註冊 web 應用程式的驗證。</span><span class="sxs-lookup"><span data-stu-id="b139a-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="b139a-134">開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(…)`方法，將設定從 hello v2.0 端點的 hello Web API tooaccept 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="b139a-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="b139a-135">現在您可以使用`[Authorize]`屬性 tooprotect 您控制站和 OAuth 2.0 承載驗證的動作。</span><span class="sxs-lookup"><span data-stu-id="b139a-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="b139a-136">裝飾 hello`Controllers\TodoListController.cs`授權標記的類別。</span><span class="sxs-lookup"><span data-stu-id="b139a-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="b139a-137">這會強制在 hello 使用者 toosign 才能存取該頁面。</span><span class="sxs-lookup"><span data-stu-id="b139a-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="b139a-138">當授權的呼叫者已成功叫用一個 hello `TodoListController` Api，hello 動作可能會需要存取 tooinformation hello 呼叫者的相關。</span><span class="sxs-lookup"><span data-stu-id="b139a-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="b139a-139">OWIN 提供透過 hello hello 持有人權杖內存取 toohello 宣告`ClaimsPrincpal`物件。</span><span class="sxs-lookup"><span data-stu-id="b139a-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="b139a-140">最後，開啟 hello `web.config` hello hello TodoListService 專案根目錄中的檔案，並在 hello 中輸入您的組態值`<appSettings>`> 一節。</span><span class="sxs-lookup"><span data-stu-id="b139a-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="b139a-141">您`ida:Audience`為 hello**應用程式識別碼**您輸入 hello 入口網站中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b139a-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="b139a-142">Hello 用戶端應用程式設定</span><span class="sxs-lookup"><span data-stu-id="b139a-142">Configure hello client app</span></span>
<span data-ttu-id="b139a-143">您可以看到在動作中的 hello Todo 清單服務之前，您需要 tooconfigure hello Todo 清單用戶端，所以它可以從 hello v2.0 端點取得權杖，並進行呼叫 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="b139a-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="b139a-144">在 hello TodoListClient 專案中，開啟`App.config`並輸入您設定的值在 hello `<appSettings>` > 一節。</span><span class="sxs-lookup"><span data-stu-id="b139a-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="b139a-145">您`ida:ClientId`您複製從 hello 入口網站應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="b139a-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="b139a-146">最後，清除、建置並執行每個專案！</span><span class="sxs-lookup"><span data-stu-id="b139a-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="b139a-147">您現在已有 .NET MVC Web API，可從個人 Microsoft 帳戶及公司或學校帳戶接受權杖。</span><span class="sxs-lookup"><span data-stu-id="b139a-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="b139a-148">登入 hello TodoListClient，並呼叫 web api tooadd 工作 toohello 使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="b139a-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="b139a-149">如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip)，或您可以將其複製從 GitHub:</span><span class="sxs-lookup"><span data-stu-id="b139a-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="b139a-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b139a-150">Next steps</span></span>
<span data-ttu-id="b139a-151">您現在可以繼續探索其他主題。</span><span class="sxs-lookup"><span data-stu-id="b139a-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="b139a-152">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="b139a-152">You may want tootry:</span></span>

[<span data-ttu-id="b139a-153">從 Web 應用程式呼叫 Web API >></span><span class="sxs-lookup"><span data-stu-id="b139a-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="b139a-154">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b139a-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="b139a-155">hello v2.0 開發人員指南 >></span><span class="sxs-lookup"><span data-stu-id="b139a-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="b139a-156">StackOverflow "azure-active-directory" 標籤 >></span><span class="sxs-lookup"><span data-stu-id="b139a-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="b139a-157">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="b139a-157">Get security updates for our products</span></span>
<span data-ttu-id="b139a-158">我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。</span><span class="sxs-lookup"><span data-stu-id="b139a-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
