---
title: "Azure Active Directory v2.0 .NET 原生應用程式 | Microsoft Docs"
description: "如何建置可使用個人 Microsoft 帳戶及工作或學校帳戶登入使用者的 .NET 原生應用程式。"
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
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="35131-103">將登入新增至 Windows 桌面應用程式</span><span class="sxs-lookup"><span data-stu-id="35131-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="35131-104">v2.0 端點可讓您快速地將驗證加入您的桌面應用程式，同時支援個人 Microsoft 帳戶以及工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="35131-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="35131-105">它也可讓您的應用程式安全地與後端 Web API，以及 [Microsoft Graph](https://graph.microsoft.io) 和幾個 [Office 365 統一 API](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="35131-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="35131-106">v2.0 端點並非支援每個 Azure Active Directory (AD) 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="35131-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="35131-107">如果要判斷是否應該使用 v2.0 端點，請閱讀 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="35131-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="35131-108">對於 [在裝置上執行的 .NET 原生應用程式](active-directory-v2-flows.md#mobile-and-native-apps)，Azure AD 提供 Microsoft Identity Authentication Library，或稱 MSAL。</span><span class="sxs-lookup"><span data-stu-id="35131-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="35131-109">MSAL 存在的唯一目的是為了讓您的應用程式輕鬆取得權杖以呼叫 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="35131-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="35131-110">為了示範這有多麼簡單，我們將在此建置一個執行下列動作的 .NET WPF 待辦事項清單應用程式：</span><span class="sxs-lookup"><span data-stu-id="35131-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="35131-111">使用 [OAuth 2.0 驗證通訊協定](active-directory-v2-protocols.md)登入使用者並取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="35131-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="35131-112">安全地呼叫受 OAuth 2.0 保護的後端待辦事項清單 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="35131-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="35131-113">將使用者登出。</span><span class="sxs-lookup"><span data-stu-id="35131-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="35131-114">下載範例程式碼</span><span class="sxs-lookup"><span data-stu-id="35131-114">Download sample code</span></span>
<span data-ttu-id="35131-115">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="35131-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="35131-116">若要遵循執行，您可以 [用 .zip 格式下載應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) ，或複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="35131-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="35131-117">本教學課程最後也會提供完整的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35131-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="35131-118">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="35131-118">Register an app</span></span>
<span data-ttu-id="35131-119">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="35131-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="35131-120">請確定：</span><span class="sxs-lookup"><span data-stu-id="35131-120">Make sure to:</span></span>

* <span data-ttu-id="35131-121">將指派給您應用程式的 **應用程式識別碼** 複製起來，您很快會需要用到這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="35131-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="35131-122">為您的應用程式新增 **行動** 平台。</span><span class="sxs-lookup"><span data-stu-id="35131-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="35131-123">安裝和設定 MSAL</span><span class="sxs-lookup"><span data-stu-id="35131-123">Install & Configure MSAL</span></span>
<span data-ttu-id="35131-124">您現在有了已向 Microsoft 註冊的應用程式，可以安裝 MSAL 並撰寫與您身分識別相關的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35131-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="35131-125">為了讓 MSAL 能與 v2.0 端點通訊，您需要提供一些應用程式註冊的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="35131-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="35131-126">首先，使用 Package Manager Console 將 MSAL 新增到 TodoListClient 專案中。</span><span class="sxs-lookup"><span data-stu-id="35131-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="35131-127">在 TodoListClient 專案中，開啟 `app.config`。</span><span class="sxs-lookup"><span data-stu-id="35131-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="35131-128">取代 `<appSettings>` 區段中的元素值，以反映您在應用程式註冊入口網站中輸入的值。</span><span class="sxs-lookup"><span data-stu-id="35131-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="35131-129">每當使用 MSAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="35131-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="35131-130">`ida:ClientId` 是您從入口網站複製的應用程式的 **應用程式 ID** 。</span><span class="sxs-lookup"><span data-stu-id="35131-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="35131-131">在 TodoList-Service 專案中，開啟專案根目錄中的 `web.config` 。</span><span class="sxs-lookup"><span data-stu-id="35131-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="35131-132">以來自入口網站的相同**應用程式識別碼**取代 `ida:Audience` 值。</span><span class="sxs-lookup"><span data-stu-id="35131-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="35131-133">使用 MSAL 取得權杖</span><span class="sxs-lookup"><span data-stu-id="35131-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="35131-134">MSAL 的基本原則是，每當應用程式需要存取權杖時，您只需呼叫 `app.AcquireToken(...)`，MSAL 就會執行其餘工作。</span><span class="sxs-lookup"><span data-stu-id="35131-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="35131-135">在 `TodoListClient` 專案中，開啟 `MainWindow.xaml.cs` 並找出 `OnInitialized(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="35131-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="35131-136">第一步是初始化應用程式的 `PublicClientApplication` - 代表原生應用程式的 MSAL 主要類別。</span><span class="sxs-lookup"><span data-stu-id="35131-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="35131-137">您在這裡將 ADAL 與 Azure AD 通訊所需的座標傳給 MSAL，並告訴它如何快取權杖。</span><span class="sxs-lookup"><span data-stu-id="35131-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="35131-138">當應用程式啟動時，我們希望檢查並查看使用者是否已登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="35131-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="35131-139">不過，我們不想這個時候叫用登入 UI，而是讓使用者按一下 [登入] 才執行此作業。</span><span class="sxs-lookup"><span data-stu-id="35131-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="35131-140">另在 `OnInitialized(...)` 方法中：</span><span class="sxs-lookup"><span data-stu-id="35131-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
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

* <span data-ttu-id="35131-141">如果使用者未登入而按下 [登入] 按鈕，我們希望叫用登入 UI 並讓使用者輸入其認證。</span><span class="sxs-lookup"><span data-stu-id="35131-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="35131-142">實作登入按鈕處理常式：</span><span class="sxs-lookup"><span data-stu-id="35131-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

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
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
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

* <span data-ttu-id="35131-143">如果使用者成功登入，MSAL 會為您接收和快取權杖，您可以放心大膽地繼續呼叫 `GetTodoList()` 方法。</span><span class="sxs-lookup"><span data-stu-id="35131-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="35131-144">要取得使用者工作的剩餘步驟，是實作 `GetTodoList()` 方法。</span><span class="sxs-lookup"><span data-stu-id="35131-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

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

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

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

## <a name="run"></a><span data-ttu-id="35131-145">執行</span><span class="sxs-lookup"><span data-stu-id="35131-145">Run</span></span>
<span data-ttu-id="35131-146">恭喜！</span><span class="sxs-lookup"><span data-stu-id="35131-146">Congratulations!</span></span> <span data-ttu-id="35131-147">您現在擁有一個運作正常的 .NET WPF 應用程式，可使用 OAuth 2.0 驗證使用者並安全地呼叫 Web API。</span><span class="sxs-lookup"><span data-stu-id="35131-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="35131-148">執行您的兩個專案，並以個人的 Microsoft 或工作/學校的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="35131-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="35131-149">將工作新增到使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="35131-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="35131-150">登出並以其他使用者再次登入，查看其他使用者的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="35131-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="35131-151">關閉並重新執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="35131-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="35131-152">注意使用者的工作階段是否維持不變，這是因為應用程式會快取本機檔案中的權杖。</span><span class="sxs-lookup"><span data-stu-id="35131-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="35131-153">MSAL 可使用個人和工作帳戶，輕鬆地將通用的身分識別功能納入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35131-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="35131-154">它會為您處理一切麻煩的事，包括快取管理、OAuth 通訊協定支援、向使用者顯示登入 UI、重新整理過期權杖等等。</span><span class="sxs-lookup"><span data-stu-id="35131-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="35131-155">您唯一需要知道的就是單一 API 呼叫， `app.AcquireTokenAsync(...)`。</span><span class="sxs-lookup"><span data-stu-id="35131-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="35131-156">如需參考， [此處以 .zip 格式提供](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip)完整範例 (不含您的組態值)，您也可以從 GitHub 予以複製：</span><span class="sxs-lookup"><span data-stu-id="35131-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="35131-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35131-157">Next steps</span></span>
<span data-ttu-id="35131-158">您現在可以進入更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="35131-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="35131-159">您可以嘗試：</span><span class="sxs-lookup"><span data-stu-id="35131-159">You may want to try:</span></span>

* [<span data-ttu-id="35131-160">透過 v2.0 端點保護 TodoListService Web API</span><span class="sxs-lookup"><span data-stu-id="35131-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="35131-161">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="35131-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="35131-162">v2.0 開發人員指南 >></span><span class="sxs-lookup"><span data-stu-id="35131-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="35131-163">StackOverflow "msal" 標籤 >></span><span class="sxs-lookup"><span data-stu-id="35131-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="35131-164">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="35131-164">Get security updates for our products</span></span>
<span data-ttu-id="35131-165">我們鼓勵您造訪 [此頁面](https://technet.microsoft.com/security/dd252948) 並訂閱資訊安全摘要報告警示，以在安全性事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="35131-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

