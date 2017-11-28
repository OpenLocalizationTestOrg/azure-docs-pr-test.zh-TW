---
title: "aaaAzure AD Windows Phone 開始使用 |Microsoft 文件"
description: "Toobuild Windows Phone 應用程式整合與 Azure AD 進行登入，並呼叫 Azure AD 保護應用程式開發介面使用 OAuth 的方式。"
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="cef78-103">整合 Azure AD 與 Windows Phone 應用程式</span><span class="sxs-lookup"><span data-stu-id="cef78-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="cef78-104">Visual Studio 2017 不支援 Windows Phone 8.1 和舊版專案。</span><span class="sxs-lookup"><span data-stu-id="cef78-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="cef78-105">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="cef78-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="cef78-106">如果您正在開發 Windows Phone 8.1 應用程式，Azure AD，使其簡單又直接您 tooauthenticate 為您的使用者使用其 Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cef78-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="cef78-107">它也可讓您的應用程式 toosecurely 取用任何 web API 受到 Azure AD，例如 hello Office 365 Api 或 hello Azure API。</span><span class="sxs-lookup"><span data-stu-id="cef78-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="cef78-108">此程式碼範例會使用 ADAL 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="cef78-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="cef78-109">Hello 最新技術，您可能會想 tooinstead 再試一次我們[Windows 通用教學課程中使用 ADAL v3.0](active-directory-devquickstarts-windowsstore.md)。</span><span class="sxs-lookup"><span data-stu-id="cef78-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="cef78-110">如果您確實要建置適用於 Windows Phone 8.1 的應用程式，這是 hello 正確的位置。</span><span class="sxs-lookup"><span data-stu-id="cef78-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="cef78-111">ADAL v2.0 仍完整支援，且 hello 開發應用程式 agianst Windows Phone 8.1 建議的方法來使用 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="cef78-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="cef78-112">對於.NET 原生用戶端需要 tooaccess 受保護的資源，Azure AD 會提供 Active Directory 驗證程式庫或 ADAL hello。</span><span class="sxs-lookup"><span data-stu-id="cef78-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="cef78-113">ADAL 的生活中的唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cef78-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="cef78-114">toodemonstrate 多麼容易，所以這裡，我們將建立 「 目錄搜尋程式 「 Windows Phone 8.1 應用程式的：</span><span class="sxs-lookup"><span data-stu-id="cef78-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="cef78-115">取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cef78-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="cef78-116">搜尋目錄以尋找具有指定 UPN 的使用者。</span><span class="sxs-lookup"><span data-stu-id="cef78-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="cef78-117">將使用者登出。</span><span class="sxs-lookup"><span data-stu-id="cef78-117">Signs users out.</span></span>

<span data-ttu-id="cef78-118">toobuild hello 完整運作應用程式，您將需要：</span><span class="sxs-lookup"><span data-stu-id="cef78-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="cef78-119">向 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cef78-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="cef78-120">安裝及設定 ADAL。</span><span class="sxs-lookup"><span data-stu-id="cef78-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="cef78-121">使用來自 Azure AD 的 ADAL tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cef78-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="cef78-122">啟動，tooget[下載基本架構的專案](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="cef78-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="cef78-123">每一個都是 Visual Studio 2013 解決方案。</span><span class="sxs-lookup"><span data-stu-id="cef78-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="cef78-124">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="cef78-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="cef78-125">如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="cef78-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="cef78-126">1.註冊 hello 目錄搜尋程式應用程式</span><span class="sxs-lookup"><span data-stu-id="cef78-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="cef78-127">tooenable 您應用程式 tooget 語彙基元中，您必須先在您的 Azure AD 租用戶 tooregister，並授與權限 tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="cef78-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="cef78-128">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="cef78-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cef78-129">Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="cef78-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="cef78-130">按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="cef78-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="cef78-131">按一下 [應用程式註冊]，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cef78-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="cef78-132">依照 hello 提示，並建立新**原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cef78-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="cef78-133">hello**名稱**hello 的應用程式將會描述您應用程式 tooend 使用者</span><span class="sxs-lookup"><span data-stu-id="cef78-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="cef78-134">hello**重新導向 Uri**是配置和字串的組合，Azure AD 將會使用 tooreturn 權杖回應。</span><span class="sxs-lookup"><span data-stu-id="cef78-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="cef78-135">現在請先輸入預留位置值，例如 `http://DirectorySearcher`。</span><span class="sxs-lookup"><span data-stu-id="cef78-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="cef78-136">我們稍後將會取代此值。</span><span class="sxs-lookup"><span data-stu-id="cef78-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="cef78-137">完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="cef78-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="cef78-138">您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cef78-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="cef78-139">從 hello**設定**頁面上，選擇**必要的使用權限**選擇**新增**。</span><span class="sxs-lookup"><span data-stu-id="cef78-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="cef78-140">選取 hello **Microsoft Graph**為 hello 應用程式開發介面，並加入 hello**讀取目錄資料**權限下的**委派的權限**。</span><span class="sxs-lookup"><span data-stu-id="cef78-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="cef78-141">這會讓使用者您應用程式 tooquery hello Graph API。</span><span class="sxs-lookup"><span data-stu-id="cef78-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="cef78-142">2.安裝和設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="cef78-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="cef78-143">既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="cef78-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="cef78-144">為了讓 ADAL toobe 無法 toocommunicate 與 Azure AD，您需要 tooprovide 它與您的應用程式註冊的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="cef78-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="cef78-145">藉由加入使用 Package Manager Console hello ADAL toohello DirectorySearcher 專案開始。</span><span class="sxs-lookup"><span data-stu-id="cef78-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="cef78-146">在 hello DirectorySearcher 專案中，開啟`MainPage.xaml.cs`。</span><span class="sxs-lookup"><span data-stu-id="cef78-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="cef78-147">Hello 中的 hello 值取代為`Config Values`區域 tooreflect hello 值的輸入 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cef78-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="cef78-148">每當使用 ADAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="cef78-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="cef78-149">hello`tenant`是 hello Azure AD 租用戶，例如 contoso.onmicrosoft.com 網域</span><span class="sxs-lookup"><span data-stu-id="cef78-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="cef78-150">hello`clientId`是 hello clientId 您複製從 hello 入口網站應用程式。</span><span class="sxs-lookup"><span data-stu-id="cef78-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="cef78-151">您現在會需要您的 Windows Phone 應用程式的 toodiscover hello 回呼 uri。</span><span class="sxs-lookup"><span data-stu-id="cef78-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="cef78-152">在 hello 中這一行設定中斷點`MainPage`方法：</span><span class="sxs-lookup"><span data-stu-id="cef78-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="cef78-153">執行 hello 應用程式，並複製擱置在一旁的 hello 值`redirectUri`hello 中斷點叫用時。</span><span class="sxs-lookup"><span data-stu-id="cef78-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="cef78-154">您應該會看到類似下面的畫面</span><span class="sxs-lookup"><span data-stu-id="cef78-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="cef78-155">在 [hello**設定**hello Azure 管理入口網站中，於應用程式] 索引標籤，以取代 hello hello 值**RedirectUri**具有這個值。</span><span class="sxs-lookup"><span data-stu-id="cef78-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="cef78-156">3.使用 ADAL tooGet 語彙基元從 AAD</span><span class="sxs-lookup"><span data-stu-id="cef78-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="cef78-157">hello ADAL 背後的基本原則是，只要您的應用程式需要存取權杖，它只會呼叫`authContext.AcquireToken(…)`，ADAL 沒有 hello rest 和。</span><span class="sxs-lookup"><span data-stu-id="cef78-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="cef78-158">hello 第一個步驟是您的應用程式的 tooinitialize `AuthenticationContext` -ADAL 的主要類別。</span><span class="sxs-lookup"><span data-stu-id="cef78-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="cef78-159">這是您用來傳遞 ADAL hello 座標需要 toocommunicate 與 Azure AD，並告訴它如何 toocache 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cef78-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="cef78-160">立即找出 hello `Search(...)` hello 使用者 cliks hello hello 應用程式的 UI 中的 「 搜尋 」 按鈕時將會叫用的方法。</span><span class="sxs-lookup"><span data-stu-id="cef78-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="cef78-161">這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello GET 要求 Azure AD Graph API toohello tooquery。</span><span class="sxs-lookup"><span data-stu-id="cef78-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="cef78-162">但是順序 tooquery hello Graph API，在中，您需要在 hello access_token tooinclude`Authorization`要求標頭的 hello-這是 ADAL 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="cef78-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="cef78-163">如果需要互動式驗證，ADAL 會使用 Windows Phone Web 驗證代理人 」 (WAB) 和[接續模型](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/)toodisplay hello Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="cef78-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="cef78-164">當 hello 使用者登入時，您的應用程式需要 toopass ADAL hello 結果的 hello WAB 互動。</span><span class="sxs-lookup"><span data-stu-id="cef78-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="cef78-165">這很簡單，只實作 hello`ContinueWebAuthentication`介面：</span><span class="sxs-lookup"><span data-stu-id="cef78-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="cef78-166">現在時間 toouse hello`AuthenticationResult`傳回 tooyour 應用程式的 ADAL。</span><span class="sxs-lookup"><span data-stu-id="cef78-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="cef78-167">在 hello`QueryGraph(...)`回呼，附加 hello access_token 貴用戶取得 toohello hello 授權標頭中的 GET 要求：</span><span class="sxs-lookup"><span data-stu-id="cef78-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="cef78-168">您也可以使用 hello`AuthenticationResult`物件 toodisplay hello 使用者應用程式中的資訊。</span><span class="sxs-lookup"><span data-stu-id="cef78-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="cef78-169">在 [hello`QueryGraph(...)`方法中，使用 hello 結果 tooshow hello 使用者的識別碼在 hello] 頁面上：</span><span class="sxs-lookup"><span data-stu-id="cef78-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="cef78-170">最後，您可以使用 ADAL toosign hello 使用者登出的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cef78-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="cef78-171">Hello 使用者按一下 hello 「 登出 」 按鈕時，我們想要太 hello 下一個呼叫的 tooensure`AcquireTokenSilentAsync(...)`將會失敗。</span><span class="sxs-lookup"><span data-stu-id="cef78-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="cef78-172">使用 ADAL，這非常簡單，只要清除 hello 權杖快取項目：</span><span class="sxs-lookup"><span data-stu-id="cef78-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="cef78-173">恭喜！</span><span class="sxs-lookup"><span data-stu-id="cef78-173">Congratulations!</span></span> <span data-ttu-id="cef78-174">您現在擁有可運作的 Windows Phone 應用程式具有 hello 能力 tooauthenticate 使用者、 安全地呼叫 Web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="cef78-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="cef78-175">如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。</span><span class="sxs-lookup"><span data-stu-id="cef78-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="cef78-176">執行 DirectorySearcher 應用程式，並使用其中一個使用者登入。</span><span class="sxs-lookup"><span data-stu-id="cef78-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="cef78-177">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="cef78-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="cef78-178">關閉 hello 應用程式，並重新執行。</span><span class="sxs-lookup"><span data-stu-id="cef78-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="cef78-179">請注意如何 hello 使用者工作階段會保持不變。</span><span class="sxs-lookup"><span data-stu-id="cef78-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="cef78-180">登出，再以另一個使用者身分重新登入。</span><span class="sxs-lookup"><span data-stu-id="cef78-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="cef78-181">ADAL 可讓您輕鬆 tooincorporate 所有這些常見的身分識別功能到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cef78-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="cef78-182">它會為您的快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，重新整理過期的權杖與多個負責 hello 中途的所有工作。</span><span class="sxs-lookup"><span data-stu-id="cef78-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="cef78-183">您只需 tooknow 是單一的應用程式開發介面呼叫， `authContext.AcquireToken*(…)`。</span><span class="sxs-lookup"><span data-stu-id="cef78-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="cef78-184">已完成的 hello 範例 （不含您的組態值） 所提供，供您參考[這裡](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="cef78-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="cef78-185">您現在可以移動 tooadditional 身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="cef78-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="cef78-186">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="cef78-186">You may want tootry:</span></span>

[<span data-ttu-id="cef78-187">使用 Azure AD 保護 .NET Web API >></span><span class="sxs-lookup"><span data-stu-id="cef78-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

