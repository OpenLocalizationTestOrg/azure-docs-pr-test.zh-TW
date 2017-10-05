---
title: "Azure AD .NET 入門 | Microsoft Docs"
description: "如何建置 .NET Windows 桌面應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="bc43e-103">將 Azure AD 整合至 Windows 桌面 WPF 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc43e-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="bc43e-104">如果您正在開發桌面應用程式，Azure AD 讓使用 Active Directory 帳戶驗證您的使用者變得簡單明瞭。</span><span class="sxs-lookup"><span data-stu-id="bc43e-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="bc43e-105">它也可讓您的應用程式安全地使用任何受 Azure AD 保護的 Web API，例如 Office 365 API 或 Azure API。</span><span class="sxs-lookup"><span data-stu-id="bc43e-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="bc43e-106">對於需要存取受保護資源的 .NET 原生用戶端，Azure AD 提供 Active Directory 驗證程式庫 (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="bc43e-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="bc43e-107">ADAL 存在的唯一目的是讓您的應用程式輕鬆取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bc43e-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="bc43e-108">為了示範究竟多麼簡單，我們將建置一個執行下列動作的 .NET WPF 待辦事項清單應用程式：</span><span class="sxs-lookup"><span data-stu-id="bc43e-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="bc43e-109">使用 [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)取得呼叫 Azure AD Graph API 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bc43e-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="bc43e-110">在目錄中搜尋具有指定別名的使用者。</span><span class="sxs-lookup"><span data-stu-id="bc43e-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="bc43e-111">將使用者登出。</span><span class="sxs-lookup"><span data-stu-id="bc43e-111">Signs users out.</span></span>

<span data-ttu-id="bc43e-112">若要建立可完整運作的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="bc43e-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="bc43e-113">向 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc43e-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="bc43e-114">安裝及設定 ADAL。</span><span class="sxs-lookup"><span data-stu-id="bc43e-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="bc43e-115">使用 ADAL 來取得 Azure AD 的權杖。</span><span class="sxs-lookup"><span data-stu-id="bc43e-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="bc43e-116">若要開始使用，請[下載應用程式基本架構](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip)或[下載完整的範例](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="bc43e-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="bc43e-117">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bc43e-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="bc43e-118">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="bc43e-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="bc43e-119">1.註冊 DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc43e-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="bc43e-120">若要讓您的應用程式取得權杖，您必須先在 Azure AD 租用戶中註冊這個應用程式，並授權它存取 Azure AD Graph API：</span><span class="sxs-lookup"><span data-stu-id="bc43e-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="bc43e-121">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bc43e-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bc43e-122">在頂端列上按一下您的帳戶，然後在 [目錄] 清單底下，選擇您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bc43e-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="bc43e-123">按一下左側瀏覽區中的 [更多服務]，然後選擇 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="bc43e-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="bc43e-124">按一下 [應用程式註冊]，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bc43e-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="bc43e-125">遵照提示進行，並建立新的 **原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bc43e-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="bc43e-126">應用程式的 [ **名稱** ] 將對使用者說明您的應用程式</span><span class="sxs-lookup"><span data-stu-id="bc43e-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="bc43e-127">「 **重新導向 URI** 」是配置和字串的組合，Azure AD 可用它來傳回權杖回應。</span><span class="sxs-lookup"><span data-stu-id="bc43e-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="bc43e-128">輸入應用程式特定的值，例如 `http://DirectorySearcher`。</span><span class="sxs-lookup"><span data-stu-id="bc43e-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="bc43e-129">完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="bc43e-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="bc43e-130">您會在後續章節中用到這個值，所以請從應用程式頁面中複製此值。</span><span class="sxs-lookup"><span data-stu-id="bc43e-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="bc43e-131">從 [設定] 頁面，選擇 [必要權限]，然後選擇 [加入]。</span><span class="sxs-lookup"><span data-stu-id="bc43e-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="bc43e-132">選取 [Microsoft Graph] 作為 API，然後在 [委派權限] 底下新增 [讀取目錄資料] 權限。</span><span class="sxs-lookup"><span data-stu-id="bc43e-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="bc43e-133">這樣做可讓您的應用程式查詢 Graph API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="bc43e-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="bc43e-134">2.安裝和設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="bc43e-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="bc43e-135">既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc43e-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="bc43e-136">為了讓 ADAL 能與 Azure AD 通訊，您需要提供一些應用程式註冊的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bc43e-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="bc43e-137">首先，使用 Package Manager Console 將 ADAL 新增到 DirectorySearcher 專案中。</span><span class="sxs-lookup"><span data-stu-id="bc43e-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="bc43e-138">在 DirectorySearcher 專案中，開啟 `app.config`。</span><span class="sxs-lookup"><span data-stu-id="bc43e-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="bc43e-139">取代 `<appSettings>` 區段中的元素值，以反映您在 Azure 入口網站中所輸入的值。</span><span class="sxs-lookup"><span data-stu-id="bc43e-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="bc43e-140">每當使用 ADAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="bc43e-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="bc43e-141">`ida:Tenant` 是指您的 Azure AD 租用戶網域，例如 contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="bc43e-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="bc43e-142">`ida:ClientId` 是指您從入口網站複製的應用程式 clientId。</span><span class="sxs-lookup"><span data-stu-id="bc43e-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="bc43e-143">`ida:RedirectUri` 是您在入口網站中註冊的重新導向 url。</span><span class="sxs-lookup"><span data-stu-id="bc43e-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="bc43e-144">3.  使用 ADAL 從 AAD 取得權杖</span><span class="sxs-lookup"><span data-stu-id="bc43e-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="bc43e-145">ADAL 的基本原則是每當您的應用程式需要存取權杖時，它只需呼叫 `authContext.AcquireTokenAsync(...)`，ADAL 就會進行其餘工作。</span><span class="sxs-lookup"><span data-stu-id="bc43e-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="bc43e-146">在 `DirectorySearcher` 專案中，開啟 `MainWindow.xaml.cs` 並找出 `MainWindow()` 方法。</span><span class="sxs-lookup"><span data-stu-id="bc43e-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="bc43e-147">第一步是初始化應用程式的 `AuthenticationContext` - ADAL 的主要類別。</span><span class="sxs-lookup"><span data-stu-id="bc43e-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="bc43e-148">您在這裡將 ADAL 與 Azure AD 通訊所需的座標傳給 ADAL，並告訴它如何快取權杖。</span><span class="sxs-lookup"><span data-stu-id="bc43e-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="bc43e-149">現在請找到 `Search(...)` 方法，這是在使用者按一下應用程式 UI 的 [搜尋] 按鈕時所叫用的方法。</span><span class="sxs-lookup"><span data-stu-id="bc43e-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="bc43e-150">這個方法會對 Azure AD Graph API 提出 GET 要求，以查詢 UPN 開頭為指定搜尋詞彙的使用者。</span><span class="sxs-lookup"><span data-stu-id="bc43e-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="bc43e-151">但為了能夠查詢 Graph API，要求的 `Authorization` 標頭必須包含 access_token - ADAL 可以提供這方面的協助。</span><span class="sxs-lookup"><span data-stu-id="bc43e-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="bc43e-152">當您的應用程式透過呼叫 `AcquireTokenAsync(...)`要求權杖時，ADAL 會嘗試在不要求使用者認證的情況下傳回權杖。</span><span class="sxs-lookup"><span data-stu-id="bc43e-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="bc43e-153">如果 ADAL 決定使用者需要登入才能取得權杖，它會顯示登入對話方塊、收集使用者的認證，並在成功驗證後傳回權杖。</span><span class="sxs-lookup"><span data-stu-id="bc43e-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="bc43e-154">如果基於任何原因 ADAL 無法傳回權杖，則會擲回 `AdalException`。</span><span class="sxs-lookup"><span data-stu-id="bc43e-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="bc43e-155">請注意，`AuthenticationResult` 物件包含 `UserInfo` 物件，可用來收集您的應用程式可能需要的資訊。</span><span class="sxs-lookup"><span data-stu-id="bc43e-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="bc43e-156">在 DirectorySearcher 中， `UserInfo` 用來以使用者的識別碼自訂應用程式的 UI。</span><span class="sxs-lookup"><span data-stu-id="bc43e-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="bc43e-157">當使用者按一下 [登出] 按鈕時，我們想要確保下次呼叫 `AcquireTokenAsync(...)` 時會要求使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bc43e-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="bc43e-158">有了 ADAL，這會和清除權杖快取一樣簡單：</span><span class="sxs-lookup"><span data-stu-id="bc43e-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="bc43e-159">不過，如果使用者未按一下 [登出] 按鈕，您會想要維護使用者的工作階段，供他們下一次執行 DirectorySearcher 繼續使用。</span><span class="sxs-lookup"><span data-stu-id="bc43e-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="bc43e-160">當應用程式啟動時，您可以在 ADAL 的權杖快取中檢查現有的權杖，並據此更新 UI。</span><span class="sxs-lookup"><span data-stu-id="bc43e-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="bc43e-161">在 `CheckForCachedToken()` 方法中，再次呼叫 `AcquireTokenAsync(...)`，這次傳入 `PromptBehavior.Never` 參數。</span><span class="sxs-lookup"><span data-stu-id="bc43e-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="bc43e-162">`PromptBehavior.Never` 告訴 ADAL 不要提示使用者進行登入，而如果 ADAL 無法傳回權杖，則應該改為擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="bc43e-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="bc43e-163">恭喜！</span><span class="sxs-lookup"><span data-stu-id="bc43e-163">Congratulations!</span></span> <span data-ttu-id="bc43e-164">您現在有一個可運作的 .NET WPF 應用程式，能夠驗證使用者、使用 OAuth 2.0 安全地呼叫 Web API，以及取得使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="bc43e-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="bc43e-165">如果您還沒有這麼做，現在是將一些使用者植入租用戶的時候。</span><span class="sxs-lookup"><span data-stu-id="bc43e-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="bc43e-166">執行 DirectorySearcher 應用程式，並使用其中一個使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bc43e-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="bc43e-167">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="bc43e-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="bc43e-168">關閉並重新執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc43e-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="bc43e-169">請注意，使用者工作階段會維持不變。</span><span class="sxs-lookup"><span data-stu-id="bc43e-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="bc43e-170">登出，再以另一個使用者身分重新登入。</span><span class="sxs-lookup"><span data-stu-id="bc43e-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="bc43e-171">ADAL 可讓您輕鬆地將這些常見的身分識別功能全部納入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc43e-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="bc43e-172">它會為您處理一切麻煩的事，包括快取管理、OAuth 通訊協定支援、向使用者顯示登入 UI、重新整理過期權杖等等。</span><span class="sxs-lookup"><span data-stu-id="bc43e-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="bc43e-173">您唯一需要知道的就是單一 API 呼叫， `authContext.AcquireTokenAsync(...)`。</span><span class="sxs-lookup"><span data-stu-id="bc43e-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="bc43e-174">[這裡](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)提供完成的範例供您參考 (不含您的設定值)。</span><span class="sxs-lookup"><span data-stu-id="bc43e-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="bc43e-175">您現在可以繼續探索其他案例。</span><span class="sxs-lookup"><span data-stu-id="bc43e-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="bc43e-176">您可以嘗試：</span><span class="sxs-lookup"><span data-stu-id="bc43e-176">You may want to try:</span></span>

[<span data-ttu-id="bc43e-177">使用 Azure AD 保護 .NET Web API >></span><span class="sxs-lookup"><span data-stu-id="bc43e-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

