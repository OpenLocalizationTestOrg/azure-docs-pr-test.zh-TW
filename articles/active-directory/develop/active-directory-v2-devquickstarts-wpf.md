---
title: "aaaAzure Active Directory v2.0.NET 原生應用程式 |Microsoft 文件"
description: "如何 toobuild.NET 原生應用程式的使用者使用簽署兩個人的 Microsoft 帳戶和工作或學校帳戶。"
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="c11d3-103">新增登入 tooa Windows 桌面應用程式</span><span class="sxs-lookup"><span data-stu-id="c11d3-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="c11d3-104">與 hello hello v2.0 端點，您可以快速加入驗證 tooyour 傳統型應用程式支援這兩個個人 Microsoft 帳戶和工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="c11d3-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="c11d3-105">它也可讓您的應用程式 toosecurely 通訊與後端 web 應用程式開發介面，以及[hello Microsoft Graph](https://graph.microsoft.io)和幾個 hello [Office 365 統一的 Api](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2)。</span><span class="sxs-lookup"><span data-stu-id="c11d3-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="c11d3-106">並非所有的 Azure Active Directory (AD) 的案例和功能都受到 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="c11d3-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="c11d3-107">toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="c11d3-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="c11d3-108">如[在裝置執行.NET 原生應用程式](active-directory-v2-flows.md#mobile-and-native-apps)，Azure AD 提供 Microsoft 身分識別驗證程式庫或 MSAL hello。</span><span class="sxs-lookup"><span data-stu-id="c11d3-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="c11d3-109">MSAL 的生活中的唯一目的是的 toomake 輕鬆的應用程式 tooget 權杖呼叫 web 服務。</span><span class="sxs-lookup"><span data-stu-id="c11d3-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="c11d3-110">toodemonstrate 多麼容易，所以這裡我們將建置.NET WPF 待辦事項清單應用程式的：</span><span class="sxs-lookup"><span data-stu-id="c11d3-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="c11d3-111">符號 hello 中的使用者 （& s) 取得存取權杖使用 hello [OAuth 2.0 驗證通訊協定](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="c11d3-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="c11d3-112">安全地呼叫受 OAuth 2.0 保護的後端待辦事項清單 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c11d3-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="c11d3-113">符號 hello 使用者登出。</span><span class="sxs-lookup"><span data-stu-id="c11d3-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="c11d3-114">下載範例程式碼</span><span class="sxs-lookup"><span data-stu-id="c11d3-114">Download sample code</span></span>
<span data-ttu-id="c11d3-115">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="c11d3-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="c11d3-116">您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip)或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="c11d3-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="c11d3-117">在本教學課程的 hello 結尾處提供 hello 完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="c11d3-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="c11d3-118">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="c11d3-118">Register an app</span></span>
<span data-ttu-id="c11d3-119">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="c11d3-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="c11d3-120">請確定：</span><span class="sxs-lookup"><span data-stu-id="c11d3-120">Make sure to:</span></span>

* <span data-ttu-id="c11d3-121">複製下 hello**應用程式識別碼**指派 tooyour 應用程式，您將需要它過期。</span><span class="sxs-lookup"><span data-stu-id="c11d3-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="c11d3-122">新增 hello**行動**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c11d3-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="c11d3-123">安裝和設定 MSAL</span><span class="sxs-lookup"><span data-stu-id="c11d3-123">Install & Configure MSAL</span></span>
<span data-ttu-id="c11d3-124">您現在有了已向 Microsoft 註冊的應用程式，可以安裝 MSAL 並撰寫與您身分識別相關的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c11d3-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="c11d3-125">為了讓 MSAL toobe 無法 toocommunicate hello v2.0 端點，您需要 tooprovide 它與您的應用程式註冊的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="c11d3-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="c11d3-126">藉由加入使用 Package Manager Console hello MSAL toohello TodoListClient 專案開始。</span><span class="sxs-lookup"><span data-stu-id="c11d3-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="c11d3-127">在 hello TodoListClient 專案中，開啟`app.config`。</span><span class="sxs-lookup"><span data-stu-id="c11d3-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="c11d3-128">取代 hello 中的項目 hello hello 值`<appSettings>`區段 tooreflect hello 值的輸入 hello 應用程式註冊入口網站。</span><span class="sxs-lookup"><span data-stu-id="c11d3-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="c11d3-129">每當使用 MSAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="c11d3-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="c11d3-130">hello`ida:ClientId`為 hello**應用程式識別碼**您複製從 hello 入口網站應用程式。</span><span class="sxs-lookup"><span data-stu-id="c11d3-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="c11d3-131">在 hello TodoList 服務專案中，開啟`web.config`hello hello 專案根目錄中。</span><span class="sxs-lookup"><span data-stu-id="c11d3-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="c11d3-132">取代 hello`ida:Audience`相同值與 hello**應用程式識別碼**從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c11d3-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="c11d3-133">使用 MSAL tooget 語彙基元</span><span class="sxs-lookup"><span data-stu-id="c11d3-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="c11d3-134">hello MSAL 背後的基本原則是每當您的應用程式需要存取權杖，您只需呼叫`app.AcquireToken(...)`，和 MSAL 沒有 hello rest。</span><span class="sxs-lookup"><span data-stu-id="c11d3-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="c11d3-135">在 hello`TodoListClient`專案中，開啟`MainWindow.xaml.cs`並找出 hello`OnInitialized(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="c11d3-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="c11d3-136">hello 第一個步驟是您的應用程式的 tooinitialize `PublicClientApplication` -MSAL 的主要的類別，代表原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="c11d3-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="c11d3-137">這是您用來傳遞 MSAL hello 座標需要 toocommunicate 與 Azure AD，並告訴它如何 toocache 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c11d3-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="c11d3-138">Hello 應用程式啟動時，我們想 toocheck，請參閱是否 hello 使用者已登入 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c11d3-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="c11d3-139">不過，我們還不想 tooinvoke 登入 UI-我們要 hello 使用者，因此按一下 [登入] toodo。</span><span class="sxs-lookup"><span data-stu-id="c11d3-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="c11d3-140">此外在 hello`OnInitialized(...)`方法：</span><span class="sxs-lookup"><span data-stu-id="c11d3-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="c11d3-141">如果 hello 使用者未登入，而且使用者按一下 [登入] 按鈕 hello，我們想 tooinvoke 登入 UI，並擁有 hello 使用者輸入其認證。</span><span class="sxs-lookup"><span data-stu-id="c11d3-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="c11d3-142">實作 hello 登入按鈕處理常式：</span><span class="sxs-lookup"><span data-stu-id="c11d3-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="c11d3-143">如果 hello 使用者成功登入時，MSAL 會接收和快取權杖，而且您可以繼續 toocall hello`GetTodoList()`方法進行部署。</span><span class="sxs-lookup"><span data-stu-id="c11d3-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="c11d3-144">所有使用者的工作時已離開 tooget 為 tooimplement hello`GetTodoList()`方法。</span><span class="sxs-lookup"><span data-stu-id="c11d3-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="c11d3-145">執行</span><span class="sxs-lookup"><span data-stu-id="c11d3-145">Run</span></span>
<span data-ttu-id="c11d3-146">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c11d3-146">Congratulations!</span></span> <span data-ttu-id="c11d3-147">您現在擁有可運作的.NET WPF 應用程式具有 hello 能力 tooauthenticate 使用者 （& s) 安全地呼叫使用 OAuth 2.0 的 Web Api。</span><span class="sxs-lookup"><span data-stu-id="c11d3-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="c11d3-148">執行您的兩個專案，並以個人的 Microsoft 或工作/學校的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="c11d3-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="c11d3-149">加入工作 toothat 使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="c11d3-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="c11d3-150">先登出，再重新登入為另一個使用者 tooview 其待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="c11d3-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="c11d3-151">關閉 hello 應用程式，並重新執行。</span><span class="sxs-lookup"><span data-stu-id="c11d3-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="c11d3-152">請注意如何 hello 使用者工作階段會保持不變-這是因為 hello app 會快取在本機檔案的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c11d3-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="c11d3-153">MSAL 可輕鬆 tooincorporate 常見的身分識別功能到應用程式使用個人和工作帳戶。</span><span class="sxs-lookup"><span data-stu-id="c11d3-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="c11d3-154">它會為您的快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，重新整理過期的權杖與多個負責 hello 中途的所有工作。</span><span class="sxs-lookup"><span data-stu-id="c11d3-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="c11d3-155">您只需 tooknow 是單一的應用程式開發介面呼叫， `app.AcquireTokenAsync(...)`。</span><span class="sxs-lookup"><span data-stu-id="c11d3-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="c11d3-156">如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip)，或您可以將其複製從 GitHub:</span><span class="sxs-lookup"><span data-stu-id="c11d3-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="c11d3-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c11d3-157">Next steps</span></span>
<span data-ttu-id="c11d3-158">您現在可以進入更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="c11d3-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="c11d3-159">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="c11d3-159">You may want tootry:</span></span>

* [<span data-ttu-id="c11d3-160">保護與 hello v2.0 端點 hello TodoListService Web API</span><span class="sxs-lookup"><span data-stu-id="c11d3-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="c11d3-161">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c11d3-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="c11d3-162">hello v2.0 開發人員指南 >></span><span class="sxs-lookup"><span data-stu-id="c11d3-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="c11d3-163">StackOverflow "msal" 標籤 >></span><span class="sxs-lookup"><span data-stu-id="c11d3-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="c11d3-164">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="c11d3-164">Get security updates for our products</span></span>
<span data-ttu-id="c11d3-165">我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。</span><span class="sxs-lookup"><span data-stu-id="c11d3-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

