---
title: "Azure AD .NET Web API 入門 | Microsoft Docs"
description: "如何建置與 Azure AD 整合來進行驗證和授權的 .NET MVC Web API。"
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="ec0a8-103">使用來自 Azure AD 的持有者權杖來保護 Web API</span><span class="sxs-lookup"><span data-stu-id="ec0a8-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ec0a8-104">如果您要建置可存取受保護資源的應用程式，您必須知道如何防止這些資源遭受不當存取。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="ec0a8-105">Azure Active Directory (Azure AD) 只需幾行程式碼，即可使用 OAuth 2.0 持有人權杖，以既簡單又直接的方式保護 Web API。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="ec0a8-106">在 ASP.NET Web 應用程式中，您可以透過使用 Microsoft 的社群導向 OWIN 中介軟體 (包含在 .NET Framework 4.5 中) 實作，來完成這項規劃。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="ec0a8-107">這裡會使用 OWIN 建置「待辦事項清單」Web API：</span><span class="sxs-lookup"><span data-stu-id="ec0a8-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="ec0a8-108">指定要保護哪些 API。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="ec0a8-109">驗證 Web API 呼叫是否包含有效的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="ec0a8-110">若要建置「待辦事項清單」API，您必須先：</span><span class="sxs-lookup"><span data-stu-id="ec0a8-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="ec0a8-111">向 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="ec0a8-112">設定應用程式以使用 OWIN 驗證管線。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="ec0a8-113">設定用戶端應用程式以呼叫 Web API。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="ec0a8-114">若要開始使用，請[下載應用程式基本架構](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip)或[下載完整的範例](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ec0a8-115">每一個都是 Visual Studio 2013 解決方案。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="ec0a8-116">您還需要一個可供註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="ec0a8-117">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="ec0a8-118">步驟 1︰向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="ec0a8-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="ec0a8-119">若要協助保護您的應用程式，您必須先在您的租用戶中建立應用程式，然後提供 Azure AD 幾個重要的資訊。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="ec0a8-120">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ec0a8-121">在頂端列中，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-121">On the top bar, click your account.</span></span> <span data-ttu-id="ec0a8-122">在 [目錄] 清單中，選擇您要註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="ec0a8-123">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="ec0a8-124">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="ec0a8-125">依照提示並建立新的「Web 應用程式和/或 Web API」。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="ec0a8-126">[名稱] 可向使用者描述您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-126">**Name** describes your application to users.</span></span> <span data-ttu-id="ec0a8-127">輸入**待辦事項清單服務**。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="ec0a8-128">「重新導向 Uri」是配置與字串的組合，Azure AD 會用它來傳回應用程式所要求的任何權杖。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="ec0a8-129">請為此值輸入 `https://localhost:44321/` 。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="ec0a8-130">從應用程式的 [設定]  ->  [屬性] 頁面，更新應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="ec0a8-131">輸入租用戶特定識別碼。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="ec0a8-132">例如，輸入 `https://contoso.onmicrosoft.com/TodoListService`。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="ec0a8-133">儲存組態。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-133">Save the configuration.</span></span> <span data-ttu-id="ec0a8-134">讓入口網站保持開啟，因為您很快就必須一併註冊用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="ec0a8-135">步驟 2：設定應用程式以使用 OWIN 驗證管線</span><span class="sxs-lookup"><span data-stu-id="ec0a8-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="ec0a8-136">若要驗證連入要求和權杖，您必須設定讓應用程式與 Azure AD 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="ec0a8-137">若要開始進行，請開啟方案，然後使用「封裝管理器主控台」將 OWIN 中介軟體 NuGet 套件新增到 TodoListService 專案中。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="ec0a8-138">將 OWIN 啟動類別加入至名為 `Startup.cs`的 TodoListService 專案。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="ec0a8-139">在專案上按一下滑鼠右鍵，選取 [新增] > [新增項目]，然後搜尋 **OWIN**。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="ec0a8-140">OWIN 中介軟體將會在應用程式啟動時叫用 `Configuration(…)` 方法。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="ec0a8-141">將類別宣告變更為 `public partial class Startup`。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="ec0a8-142">我們已在另一個檔案中為您實作此類別的一部分。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="ec0a8-143">請在 `Configuration(…)` 方法中，呼叫 `ConfgureAuth(…)` 來為您的 Web 應用程式設定驗證。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="ec0a8-144">開啟檔案 `App_Start\Startup.Auth.cs` 並實作 `ConfigureAuth(…)` 方法。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="ec0a8-145">您在 `WindowsAzureActiveDirectoryBearerAuthenticationOptions` 中提供的參數會作為供應用程式與 Azure AD 進行通訊的座標。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="ec0a8-146">現在，您可以使用 `[Authorize]` 屬性以「JSON Web 權杖」(JWT) 持有者驗證協助保護您的控制器和動作。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="ec0a8-147">使用授權標記裝飾 `Controllers\TodoListController.cs` 類別。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="ec0a8-148">這樣會強制使用者在存取該頁面之前必須先登入。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="ec0a8-149">當授權的呼叫者成功叫用其中一個 `TodoListController` API 時，此動作可能需要存取呼叫者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="ec0a8-150">OWIN 可讓您透過 `ClaimsPrincpal` 物件存取持有人權杖內部的宣告。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="ec0a8-151">Web API 的一個常見需求是驗證權杖中是否有「範圍」存在。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="ec0a8-152">這可確保使用者已對存取「待辦事項清單服務」所需的權限表示同意。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="ec0a8-153">開啟 TodoListService 專案根目錄中的 `web.config` 檔案，然後在 `<appSettings>` 區段中輸入您的組態值。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="ec0a8-154">`ida:Tenant` 是您 Azure AD 租用戶的名稱 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="ec0a8-155">`ida:Audience` 是您在 Azure 入口網站中輸入之應用程式的「應用程式識別碼 URI」。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="ec0a8-156">步驟 3：設定用戶端應用程式並執行服務</span><span class="sxs-lookup"><span data-stu-id="ec0a8-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="ec0a8-157">在看到「待辦事項清單服務」運作之前，您必須設定「待辦事項清單」用戶端，以便讓它能夠從 Azure AD 取得權杖，並對服務進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="ec0a8-158">回到 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ec0a8-159">在 Azure AD 租用戶中建立新的應用程式，然後在產生的提示中選取 [ **原生用戶端應用程式** ]。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="ec0a8-160">[名稱] 可向使用者描述您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="ec0a8-161">請輸入 `http://TodoListClient/` 作為 [重新導向 Uri] 的值。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="ec0a8-162">完成註冊之後，Azure AD 會為應用程式指派一個唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="ec0a8-163">您會在後續小節中用到這個值，所以請從應用程式頁面中複製此值。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="ec0a8-164">從 [設定] 頁面中，選取 [必要權限]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="ec0a8-165">找出並選取 [待辦事項清單服務]，在 [委派的權限] 底下新增 [存取 TodoListService] 權限，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="ec0a8-166">在 Visual Studio 中，開啟 TodoListClient 專案中的 `App.config`，然後在 `<appSettings>` 區段中輸入您的組態值。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="ec0a8-167">`ida:Tenant` 是您 Azure AD 租用戶的名稱 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="ec0a8-168">`ida:ClientId` 是您從 Azure 入口網站中複製的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="ec0a8-169">`todo:TodoListResourceId` 是您在 Azure 入口網站中輸入之「待辦事項清單服務」應用程式的「應用程式識別碼 URI」。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec0a8-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec0a8-170">Next steps</span></span>
<span data-ttu-id="ec0a8-171">最後，清除、建置及執行每個專案。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="ec0a8-172">如果您還沒有這麼做，現在正是使用 *.onmicrosoft.com 網域在租用戶中建立新使用者的好時機。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="ec0a8-173">使用該使用者來登入「待辦事項清單」用戶端，然後在使用者的待辦清單中新增一些工作。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="ec0a8-174">如需參考資料，請參閱 [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip) 中的完整範例 (不含您的組態值)。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ec0a8-175">您現在可以繼續前進到更多的身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="ec0a8-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
