---
title: "aaaAzure AD.NET web API 開始使用 |Microsoft 文件"
description: "如何 toobuild.NET MVC web 應用程式開發介面，與整合 Azure AD 進行驗證和授權。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="16a24-103">使用來自 Azure AD 的持有者權杖來保護 Web API</span><span class="sxs-lookup"><span data-stu-id="16a24-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="16a24-104">如果您正在建置 tooprotected 資源提供存取的應用程式，您需要 tooknow tooprevent 未經授權存取 toothose 資源的方式。</span><span class="sxs-lookup"><span data-stu-id="16a24-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="16a24-105">Azure Active Directory (Azure AD) 可更容易及直接 toohelp 只有幾行程式碼使用 OAuth 2.0 承載的存取權杖來保護 web API。</span><span class="sxs-lookup"><span data-stu-id="16a24-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="16a24-106">在 ASP.NET web 應用程式，您可以使用 hello 社群導向 OWIN 中介軟體包含在.NET Framework 4.5 中的 hello Microsoft 實作，以完成這項保護。</span><span class="sxs-lookup"><span data-stu-id="16a24-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="16a24-107">這裡我們將使用 OWIN toobuild"tooDo 清單 」 web API 的：</span><span class="sxs-lookup"><span data-stu-id="16a24-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="16a24-108">指定要保護哪些 API。</span><span class="sxs-lookup"><span data-stu-id="16a24-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="16a24-109">驗證 hello web 應用程式開發介面呼叫包含的有效存取權杖。</span><span class="sxs-lookup"><span data-stu-id="16a24-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="16a24-110">toobuild hello tooDo 清單應用程式開發介面，您必須先：</span><span class="sxs-lookup"><span data-stu-id="16a24-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="16a24-111">向 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="16a24-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="16a24-112">設定 hello 應用程式 toouse hello OWIN 驗證管線。</span><span class="sxs-lookup"><span data-stu-id="16a24-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="16a24-113">設定用戶端應用程式 toocall hello web API。</span><span class="sxs-lookup"><span data-stu-id="16a24-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="16a24-114">啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="16a24-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="16a24-115">每一個都是 Visual Studio 2013 解決方案。</span><span class="sxs-lookup"><span data-stu-id="16a24-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="16a24-116">您也需要哪些 tooregister 中的 Azure AD 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="16a24-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="16a24-117">如果沒有，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="16a24-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="16a24-118">步驟 1︰向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="16a24-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="16a24-119">toohelp 來保護您的應用程式，先 toocreate 應用程式需要在您的租用戶與 Azure AD 提供幾項重要的資訊。</span><span class="sxs-lookup"><span data-stu-id="16a24-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="16a24-120">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="16a24-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="16a24-121">Hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="16a24-121">On hello top bar, click your account.</span></span> <span data-ttu-id="16a24-122">在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="16a24-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="16a24-123">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="16a24-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="16a24-124">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="16a24-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="16a24-125">依照 hello 提示，並建立新**Web 應用程式和/或 Web API**。</span><span class="sxs-lookup"><span data-stu-id="16a24-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="16a24-126">**名稱**描述應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="16a24-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="16a24-127">輸入**tooDo 清單服務**。</span><span class="sxs-lookup"><span data-stu-id="16a24-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="16a24-128">**重新導向 Uri**為配置和字串的組合，Azure AD 使用的 tooreturn 任何權杖已要求您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="16a24-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="16a24-129">請為此值輸入 `https://localhost:44321/` 。</span><span class="sxs-lookup"><span data-stu-id="16a24-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="16a24-130">從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="16a24-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="16a24-131">輸入租用戶特定識別碼。</span><span class="sxs-lookup"><span data-stu-id="16a24-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="16a24-132">例如，輸入 `https://contoso.onmicrosoft.com/TodoListService`。</span><span class="sxs-lookup"><span data-stu-id="16a24-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="16a24-133">儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="16a24-133">Save hello configuration.</span></span> <span data-ttu-id="16a24-134">讓 hello 入口網站保持開啟，因為您還需要 tooregister 用戶端應用程式儘速。</span><span class="sxs-lookup"><span data-stu-id="16a24-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="16a24-135">步驟 2： 設定 hello 應用程式 toouse hello OWIN 驗證管線</span><span class="sxs-lookup"><span data-stu-id="16a24-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="16a24-136">toovalidate 連入要求和權杖，您需要 tooset 註冊您的應用程式 toocommunicate 與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="16a24-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="16a24-137">toobegin，開啟 hello 方案，並使用 Package Manager Console hello 新增 hello OWIN 中介軟體 NuGet 封裝 toohello TodoListService 專案。</span><span class="sxs-lookup"><span data-stu-id="16a24-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="16a24-138">新增稱為 OWIN 啟動 「 類別 toohello TodoListService 專案`Startup.cs`。</span><span class="sxs-lookup"><span data-stu-id="16a24-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="16a24-139">以滑鼠右鍵按一下 hello 專案、 選取**新增** > **新項目**，然後搜尋**OWIN**。</span><span class="sxs-lookup"><span data-stu-id="16a24-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="16a24-140">hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="16a24-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="16a24-141">也變更 hello 類別宣告`public partial class Startup`。</span><span class="sxs-lookup"><span data-stu-id="16a24-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="16a24-142">我們已在另一個檔案中為您實作此類別的一部分。</span><span class="sxs-lookup"><span data-stu-id="16a24-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="16a24-143">在 hello`Configuration(…)`方法，呼叫太`ConfgureAuth(…)`tooset 註冊 web 應用程式的驗證。</span><span class="sxs-lookup"><span data-stu-id="16a24-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="16a24-144">開啟 hello 檔案`App_Start\Startup.Auth.cs`並實作 hello`ConfigureAuth(…)`方法。</span><span class="sxs-lookup"><span data-stu-id="16a24-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="16a24-145">hello 參數中提供`WindowsAzureActiveDirectoryBearerAuthenticationOptions`將做為您的應用程式 toocommunicate 與 Azure AD 的座標。</span><span class="sxs-lookup"><span data-stu-id="16a24-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="16a24-146">現在您可以使用`[Authorize]`屬性 toohelp 保護您的控制站和 JSON Web Token (JWT) 承載驗證的動作。</span><span class="sxs-lookup"><span data-stu-id="16a24-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="16a24-147">裝飾 hello`Controllers\TodoListController.cs`授權標記的類別。</span><span class="sxs-lookup"><span data-stu-id="16a24-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="16a24-148">這會強制在 hello 使用者 toosign 才能存取該頁面。</span><span class="sxs-lookup"><span data-stu-id="16a24-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="16a24-149">當授權的呼叫者已成功叫用一個 hello `TodoListController` Api，hello 動作可能會需要存取 tooinformation hello 呼叫者的相關。</span><span class="sxs-lookup"><span data-stu-id="16a24-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="16a24-150">OWIN 提供透過 hello hello 持有人權杖內存取 toohello 宣告`ClaimsPrincpal`物件。</span><span class="sxs-lookup"><span data-stu-id="16a24-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="16a24-151">Web 應用程式開發介面的共通需求是 toovalidate hello 「 範圍 」 hello 權杖中。</span><span class="sxs-lookup"><span data-stu-id="16a24-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="16a24-152">這可確保該 hello 使用者同意 toohello 權限需要的 tooaccess hello tooDo 清單服務。</span><span class="sxs-lookup"><span data-stu-id="16a24-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="16a24-153">開啟 hello `web.config` hello hello TodoListService 專案根目錄中的檔案，並在 hello 中輸入您的組態值`<appSettings>`> 一節。</span><span class="sxs-lookup"><span data-stu-id="16a24-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="16a24-154">`ida:Tenant`這是您的 Azure AD 租用戶-例如 contoso.onmicrosoft.com hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="16a24-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="16a24-155">`ida:Audience`是 hello 您輸入 hello Azure 入口網站中的 hello 應用程式的應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="16a24-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="16a24-156">步驟 3： 設定用戶端應用程式和執行 hello 服務</span><span class="sxs-lookup"><span data-stu-id="16a24-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="16a24-157">您可以看到在動作中的 hello tooDo 清單服務之前，您需要 tooconfigure hello tooDo 清單用戶端，讓它可以從 Azure AD 取得權杖，並讓呼叫 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="16a24-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="16a24-158">返回 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="16a24-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="16a24-159">在 Azure AD 租用戶中建立新的應用程式，然後選取**原生用戶端應用程式**hello 產生的提示字元中。</span><span class="sxs-lookup"><span data-stu-id="16a24-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="16a24-160">**名稱**描述應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="16a24-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="16a24-161">輸入`http://TodoListClient/`hello**重新導向 Uri**值。</span><span class="sxs-lookup"><span data-stu-id="16a24-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="16a24-162">完成註冊之後，Azure AD 會指派唯一的應用程式識別碼 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16a24-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="16a24-163">您將需要此值在 hello 下一個步驟中，因此將它複製從 hello 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="16a24-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="16a24-164">從 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="16a24-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="16a24-165">找出並選取 hello tooDo 清單服務，並將 hello**存取 TodoListService**權限下的**委派的權限**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="16a24-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="16a24-166">在 Visual Studio 中開啟`App.config`在 hello TodoListClient 專案，然後輸入 hello 中的 設定值`<appSettings>`> 一節。</span><span class="sxs-lookup"><span data-stu-id="16a24-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="16a24-167">`ida:Tenant`這是您的 Azure AD 租用戶-例如 contoso.onmicrosoft.com hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="16a24-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="16a24-168">`ida:ClientId`這是您所複製的 hello Azure 入口網站的 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="16a24-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="16a24-169">`todo:TodoListResourceId`為 hello hello tooDo hello Azure 入口網站中輸入的清單服務應用程式的應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="16a24-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16a24-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16a24-170">Next steps</span></span>
<span data-ttu-id="16a24-171">最後，清除、建置及執行每個專案。</span><span class="sxs-lookup"><span data-stu-id="16a24-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="16a24-172">如果您還沒有這麼做，現在是 hello 時間 toocreate 新的使用者，您租用戶中具有 *。 onmicrosoft.com 網域。</span><span class="sxs-lookup"><span data-stu-id="16a24-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="16a24-173">登入 toohello tooDo 清單用戶端與該使用者，並加入一些工作 toohello 使用者待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="16a24-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="16a24-174">參考，完成的 hello 範例 （不含您的組態值） 會提供[GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="16a24-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="16a24-175">您現在可以移動 toomore 身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="16a24-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
