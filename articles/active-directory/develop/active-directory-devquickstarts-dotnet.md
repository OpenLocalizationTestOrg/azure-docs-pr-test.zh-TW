---
title: "aaaAzure AD.NET 開始使用 |Microsoft 文件"
description: "Toobuild.NET 的 Windows 桌面應用程式整合與 Azure AD 進行登入，並呼叫 Azure AD 保護應用程式開發介面使用 OAuth 的方式。"
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
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="ce8d6-103">將 Azure AD 整合至 Windows 桌面 WPF 應用程式</span><span class="sxs-lookup"><span data-stu-id="ce8d6-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ce8d6-104">如果您正在開發的桌面應用程式，Azure AD，使其簡單又直接您 tooauthenticate 為您的使用者使用其 Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="ce8d6-105">它也可讓您的應用程式 toosecurely 取用任何 web API 受到 Azure AD，例如 hello Office 365 Api 或 hello Azure API。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="ce8d6-106">對於.NET 原生用戶端需要 tooaccess 受保護的資源，Azure AD 會提供 Active Directory 驗證程式庫或 ADAL hello。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="ce8d6-107">ADAL 的生活中的唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="ce8d6-108">toodemonstrate 多麼容易，所以這裡我們會建置.NET WPF 待辦事項清單應用程式，用的：</span><span class="sxs-lookup"><span data-stu-id="ce8d6-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="ce8d6-109">取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="ce8d6-110">在目錄中搜尋具有指定別名的使用者。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="ce8d6-111">將使用者登出。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-111">Signs users out.</span></span>

<span data-ttu-id="ce8d6-112">toobuild hello 完整運作應用程式，您將需要：</span><span class="sxs-lookup"><span data-stu-id="ce8d6-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="ce8d6-113">向 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="ce8d6-114">安裝及設定 ADAL。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="ce8d6-115">使用來自 Azure AD 的 ADAL tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="ce8d6-116">啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="ce8d6-117">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="ce8d6-118">如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="ce8d6-119">1.註冊 hello DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="ce8d6-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="ce8d6-120">tooenable 您應用程式 tooget 語彙基元中，您必須先在您的 Azure AD 租用戶 tooregister，並授與權限 tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="ce8d6-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="ce8d6-121">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ce8d6-122">Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="ce8d6-123">按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ce8d6-124">按一下 [應用程式註冊]，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="ce8d6-125">依照 hello 提示，並建立新**原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="ce8d6-126">hello**名稱**hello 的應用程式將會描述您應用程式 tooend 使用者</span><span class="sxs-lookup"><span data-stu-id="ce8d6-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="ce8d6-127">hello**重新導向 Uri**是配置和字串的組合，Azure AD 將會使用 tooreturn 權杖回應。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="ce8d6-128">輸入值的特定 tooyour 應用程式，例如`http://DirectorySearcher`。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="ce8d6-129">完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="ce8d6-130">您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="ce8d6-131">從 hello**設定**頁面上，選擇**必要的使用權限**選擇**新增**。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="ce8d6-132">選取 hello **Microsoft Graph**為 hello 應用程式開發介面，並加入 hello**讀取目錄資料**權限下的**委派的權限**。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="ce8d6-133">這會讓使用者您應用程式 tooquery hello Graph API。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="ce8d6-134">2.安裝和設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="ce8d6-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="ce8d6-135">既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="ce8d6-136">為了讓 ADAL toobe 無法 toocommunicate 與 Azure AD，您需要 tooprovide 它與您的應用程式註冊的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="ce8d6-137">藉由加入使用 Package Manager Console hello ADAL toohello DirectorySearcher 專案開始。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="ce8d6-138">在 hello DirectorySearcher 專案中，開啟`app.config`。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="ce8d6-139">取代 hello 中的項目 hello hello 值`<appSettings>`區段 tooreflect hello 值的輸入 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="ce8d6-140">每當使用 ADAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="ce8d6-141">hello`ida:Tenant`是 hello Azure AD 租用戶，例如 contoso.onmicrosoft.com 網域</span><span class="sxs-lookup"><span data-stu-id="ce8d6-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="ce8d6-142">hello`ida:ClientId`是 hello clientId 您複製從 hello 入口網站應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="ce8d6-143">hello`ida:RedirectUri`為 hello 重新導向註冊，讓您在 hello 入口網站的 url。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="ce8d6-144">3.  使用 ADAL tooGet 語彙基元從 AAD</span><span class="sxs-lookup"><span data-stu-id="ce8d6-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="ce8d6-145">hello ADAL 背後的基本原則是，只要您的應用程式需要存取權杖，它只會呼叫`authContext.AcquireTokenAsync(...)`，ADAL 沒有 hello rest 和。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="ce8d6-146">在 hello`DirectorySearcher`專案中，開啟`MainWindow.xaml.cs`並找出 hello`MainWindow()`方法。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="ce8d6-147">hello 第一個步驟是您的應用程式的 tooinitialize `AuthenticationContext` -ADAL 的主要類別。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="ce8d6-148">這是您用來傳遞 ADAL hello 座標需要 toocommunicate 與 Azure AD，並告訴它如何 toocache 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="ce8d6-149">立即找出 hello `Search(...)` hello 使用者 cliks hello hello 應用程式的 UI 中的 「 搜尋 」 按鈕時將會叫用的方法。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="ce8d6-150">這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello GET 要求 Azure AD Graph API toohello tooquery。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="ce8d6-151">但是順序 tooquery hello Graph API，在中，您需要在 hello access_token tooinclude`Authorization`要求標頭的 hello-這是 ADAL 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="ce8d6-152">當您的應用程式藉由呼叫要求語彙基元`AcquireTokenAsync(...)`，ADAL 會嘗試 tooreturn 語彙基元不要求 hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="ce8d6-153">ADAL 會判斷該 hello 使用者需要 toosign tooget 語彙基元中的，如果它會顯示登入 對話方塊中，收集 hello 使用者的認證，並傳回驗證成功後的權杖。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="ce8d6-154">如果 ADAL 因故無法 tooreturn 語彙基元，則會擲回`AdalException`。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="ce8d6-155">請注意該 hello`AuthenticationResult`物件包含`UserInfo`可以是您的應用程式可能需要使用的 toocollect 資訊的物件。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="ce8d6-156">在 hello DirectorySearcher，`UserInfo`是使用的 toocustomize hello 應用程式的 UI 與 hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="ce8d6-157">Hello 使用者按一下 hello 「 登出 」 按鈕時，我們想要太 hello 下一個呼叫的 tooensure`AcquireTokenAsync(...)`會要求中的 hello 使用者 toosign。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="ce8d6-158">使用 ADAL，這非常簡單，只要清除 hello 權杖快取項目：</span><span class="sxs-lookup"><span data-stu-id="ce8d6-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="ce8d6-159">不過，如果 hello 使用者不按一下 hello 「 登出 」 按鈕時，您會想 toomaintain hello 使用者工作階段的 hello 下次執行 hello DirectorySearcher。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="ce8d6-160">Hello 應用程式啟動時，您可以檢查 ADAL 的權杖快取中的現有的語彙基元，並據此更新 hello UI。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="ce8d6-161">在 hello`CheckForCachedToken()`方法，讓瀏覽另一個呼叫`AcquireTokenAsync(...)`，傳入 hello 這次`PromptBehavior.Never`參數。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="ce8d6-162">`PromptBehavior.Never`hello 使用者應該不會提示您進行登入，，和 ADAL 應該改為擲回例外狀況是否無法 tooreturn 語彙基元，則會告訴 ADAL。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
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

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="ce8d6-163">恭喜！</span><span class="sxs-lookup"><span data-stu-id="ce8d6-163">Congratulations!</span></span> <span data-ttu-id="ce8d6-164">您現在擁有可運作的.NET WPF 應用程式具有 hello 能力 tooauthenticate 使用者、 安全地呼叫 Web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="ce8d6-165">如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="ce8d6-166">執行 DirectorySearcher 應用程式，並使用其中一個使用者登入。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="ce8d6-167">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="ce8d6-168">關閉 hello 應用程式，並重新執行。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="ce8d6-169">請注意如何 hello 使用者工作階段會保持不變。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="ce8d6-170">登出，再以另一個使用者身分重新登入。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="ce8d6-171">ADAL 可讓您輕鬆 tooincorporate 所有這些常見的身分識別功能到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="ce8d6-172">它會為您的快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，重新整理過期的權杖與多個負責 hello 中途的所有工作。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="ce8d6-173">您只需 tooknow 是單一的應用程式開發介面呼叫， `authContext.AcquireTokenAsync(...)`。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="ce8d6-174">已完成的 hello 範例 （不含您的組態值） 所提供，供您參考[這裡](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="ce8d6-175">您現在可以移動 tooadditional 案例。</span><span class="sxs-lookup"><span data-stu-id="ce8d6-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="ce8d6-176">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="ce8d6-176">You may want tootry:</span></span>

[<span data-ttu-id="ce8d6-177">使用 Azure AD 保護 .NET Web API >></span><span class="sxs-lookup"><span data-stu-id="ce8d6-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

