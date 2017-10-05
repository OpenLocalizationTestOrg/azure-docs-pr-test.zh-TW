---
title: "開始使用 Azure AD Windows Phone | Microsoft Docs"
description: "如何建置 Windows Phone 應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
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
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="f3003-103">整合 Azure AD 與 Windows Phone 應用程式</span><span class="sxs-lookup"><span data-stu-id="f3003-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="f3003-104">Visual Studio 2017 不支援 Windows Phone 8.1 和舊版專案。</span><span class="sxs-lookup"><span data-stu-id="f3003-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="f3003-105">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="f3003-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="f3003-106">如果您正在開發 Windows Phone 8.1 應用程式，Azure AD 可讓您簡單又直截了當以 Active Directory 帳戶驗證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="f3003-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="f3003-107">它也可讓您的應用程式安全地使用任何受 Azure AD 保護的 Web API，例如 Office 365 API 或 Azure API。</span><span class="sxs-lookup"><span data-stu-id="f3003-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="f3003-108">此程式碼範例會使用 ADAL 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="f3003-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="f3003-109">若要最新技術，您可以改為嘗試 [使用 ADAL 3.0 版的 Windows Universal 教學課程](active-directory-devquickstarts-windowsstore.md)。</span><span class="sxs-lookup"><span data-stu-id="f3003-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="f3003-110">如果您確實要建置適用於 Windows Phone 8.1 的應用程式，則這是正確位置。</span><span class="sxs-lookup"><span data-stu-id="f3003-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="f3003-111">ADAL 2.0 版仍受到完整支援，並且是使用 Azure AD 來針對 Windows Phone 8.1 開發應用程式的建議方式。</span><span class="sxs-lookup"><span data-stu-id="f3003-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="f3003-112">對於需要存取受保護資源的 .NET 原生用戶端，Azure AD 提供 Active Directory 驗證程式庫 (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="f3003-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="f3003-113">ADAL 存在的唯一目的是為了讓您的應用程式輕鬆取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="f3003-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="f3003-114">為了示範究竟有多麼簡單，我們將建置一個可執行下列動作的「目錄搜尋程式」Windows Phone 8.1 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f3003-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="f3003-115">使用 [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)取得呼叫 Azure AD Graph API 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="f3003-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="f3003-116">搜尋目錄以尋找具有指定 UPN 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f3003-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="f3003-117">將使用者登出。</span><span class="sxs-lookup"><span data-stu-id="f3003-117">Signs users out.</span></span>

<span data-ttu-id="f3003-118">若要建立完整可用的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="f3003-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="f3003-119">向 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3003-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="f3003-120">安裝及設定 ADAL。</span><span class="sxs-lookup"><span data-stu-id="f3003-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="f3003-121">使用 ADAL 來取得 Azure AD 的權杖。</span><span class="sxs-lookup"><span data-stu-id="f3003-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="f3003-122">若要開始使用，請[下載基本架構專案](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip)或[下載完整的範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="f3003-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="f3003-123">每一個都是 Visual Studio 2013 解決方案。</span><span class="sxs-lookup"><span data-stu-id="f3003-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="f3003-124">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f3003-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="f3003-125">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="f3003-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="f3003-126">1.註冊目錄搜尋應用程式</span><span class="sxs-lookup"><span data-stu-id="f3003-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="f3003-127">若要啟用您的應用程式以取得權杖，您必須先在 Azure AD 租用戶中進行註冊，並對其授與存取 Azure AD Graph API 的權限：</span><span class="sxs-lookup"><span data-stu-id="f3003-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="f3003-128">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f3003-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f3003-129">在頂端列上按一下您的帳戶，然後在 [目錄] 清單底下，選擇您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="f3003-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="f3003-130">按一下左側瀏覽區中的 [更多服務]，然後選擇 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f3003-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f3003-131">按一下 [應用程式註冊]，然後選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f3003-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="f3003-132">遵照提示進行，並建立新的 **原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f3003-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="f3003-133">應用程式的 [ **名稱** ] 將對使用者說明您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f3003-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="f3003-134">「 **重新導向 Uri** 」是配置和字串的組合，Azure AD 可用它來傳回權杖回應。</span><span class="sxs-lookup"><span data-stu-id="f3003-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="f3003-135">現在請先輸入預留位置值，例如 `http://DirectorySearcher`。</span><span class="sxs-lookup"><span data-stu-id="f3003-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="f3003-136">我們稍後將會取代此值。</span><span class="sxs-lookup"><span data-stu-id="f3003-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="f3003-137">完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="f3003-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="f3003-138">您會在後續小節中用到這個值，所以請從應用程式索引標籤中複製此值。</span><span class="sxs-lookup"><span data-stu-id="f3003-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="f3003-139">從 [設定] 頁面，選擇 [必要權限]，然後選擇 [加入]。</span><span class="sxs-lookup"><span data-stu-id="f3003-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="f3003-140">選取 [Microsoft Graph] 作為 API，然後在 [委派權限] 底下新增 [讀取目錄資料] 權限。</span><span class="sxs-lookup"><span data-stu-id="f3003-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="f3003-141">這樣做可讓您的應用程式查詢 Graph API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f3003-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="f3003-142">2.安裝和設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="f3003-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="f3003-143">既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3003-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="f3003-144">為了讓 ADAL 能與 Azure AD 通訊，您需要提供一些應用程式註冊的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3003-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="f3003-145">首先，使用 Package Manager Console 將 ADAL 新增到 DirectorySearcher 專案中。</span><span class="sxs-lookup"><span data-stu-id="f3003-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="f3003-146">在 DirectorySearcher 專案中，開啟 `MainPage.xaml.cs`。</span><span class="sxs-lookup"><span data-stu-id="f3003-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="f3003-147">取代 [ `Config Values` ] 區域中的值以反映您在 Azure 入口網站中所輸入的值。</span><span class="sxs-lookup"><span data-stu-id="f3003-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="f3003-148">每當使用 ADAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="f3003-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="f3003-149">`tenant` 是指您的 Azure AD 租用戶網域，例如 contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="f3003-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="f3003-150">`clientId` 是指您從入口網站複製的應用程式 clientId。</span><span class="sxs-lookup"><span data-stu-id="f3003-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="f3003-151">您現在必須找出 Windows Phone 應用程式的回呼 uri。</span><span class="sxs-lookup"><span data-stu-id="f3003-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="f3003-152">在 `MainPage` 方法的這一行上設定中斷點：</span><span class="sxs-lookup"><span data-stu-id="f3003-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="f3003-153">執行應用程式，並在觸及中斷點時複製 `redirectUri` 的值並將其擱置在一旁。</span><span class="sxs-lookup"><span data-stu-id="f3003-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="f3003-154">您應該會看到類似下面的畫面</span><span class="sxs-lookup"><span data-stu-id="f3003-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="f3003-155">回到 Azure 管理入口網站中應用程式的 [設定] 索引標籤上，使用這個值取代 **RedirectUri** 的值。</span><span class="sxs-lookup"><span data-stu-id="f3003-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="f3003-156">3.使用 ADAL 從 AAD 取得權杖</span><span class="sxs-lookup"><span data-stu-id="f3003-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="f3003-157">ADAL 的基本原則是每當您的應用程式需要存取權杖時，它只需呼叫 `authContext.AcquireToken(…)`，ADAL 就會進行其餘工作。</span><span class="sxs-lookup"><span data-stu-id="f3003-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="f3003-158">第一步是初始化應用程式的 `AuthenticationContext` - ADAL 的主要類別。</span><span class="sxs-lookup"><span data-stu-id="f3003-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="f3003-159">您在這裡將 ADAL 與 Azure AD 通訊所需的座標傳給 ADAL，並告訴它如何快取權杖。</span><span class="sxs-lookup"><span data-stu-id="f3003-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="f3003-160">現在請找到 `Search(...)` 方法，這是在使用者按一下應用程式 UI 的 [搜尋] 按鈕時所叫用的方法。</span><span class="sxs-lookup"><span data-stu-id="f3003-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="f3003-161">這個方法會對 Azure AD Graph API 提出 GET 要求，以查詢 UPN 開頭為指定搜尋詞彙的使用者。</span><span class="sxs-lookup"><span data-stu-id="f3003-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="f3003-162">但為了能夠查詢 Graph API，要求的 `Authorization` 標頭必須包含 access_token - ADAL 可以提供這方面的協助。</span><span class="sxs-lookup"><span data-stu-id="f3003-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="f3003-163">如果需要互動式驗證，ADAL 會使用 Windows Phone 的 Web 驗證代理人 (WAB) 和 [接續模型](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) 來顯示 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="f3003-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="f3003-164">當使用者登入時，您的應用程式必須將與 WAB 互動的結果傳遞給 ADAL。</span><span class="sxs-lookup"><span data-stu-id="f3003-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="f3003-165">這和實作 `ContinueWebAuthentication` 介面一樣簡單：</span><span class="sxs-lookup"><span data-stu-id="f3003-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="f3003-166">現在可以開始使用 ADAL 傳回應用程式的 `AuthenticationResult` 。</span><span class="sxs-lookup"><span data-stu-id="f3003-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="f3003-167">在 `QueryGraph(...)` 回呼中，將您取得的 access_token 附加至 GET 要求的授權標頭中：</span><span class="sxs-lookup"><span data-stu-id="f3003-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="f3003-168">您也可以使用 `AuthenticationResult` 物件，在應用程式中顯示使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3003-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="f3003-169">在 `QueryGraph(...)` 方法中，使用此結果在頁面上顯示使用者的識別碼：</span><span class="sxs-lookup"><span data-stu-id="f3003-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="f3003-170">最後，您也可以使用 ADAL 來將使用者登出應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3003-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="f3003-171">當使用者按一下 [登出] 按鈕時，我們想要確保下次呼叫 `AcquireTokenSilentAsync(...)` 時將會失敗。</span><span class="sxs-lookup"><span data-stu-id="f3003-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="f3003-172">有了 ADAL，這會和清除權杖快取一樣簡單：</span><span class="sxs-lookup"><span data-stu-id="f3003-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="f3003-173">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f3003-173">Congratulations!</span></span> <span data-ttu-id="f3003-174">您現在擁有一個能夠驗證使用者、使用 OAuth 2.0 安全地呼叫 Web API，及取得使用者基本資訊的運作中 Windows Phone 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3003-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="f3003-175">如果您還沒有這麼做，現在正是將一些使用者植入租用戶的好時機。</span><span class="sxs-lookup"><span data-stu-id="f3003-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="f3003-176">執行 DirectorySearcher 應用程式，並使用其中一個使用者登入。</span><span class="sxs-lookup"><span data-stu-id="f3003-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="f3003-177">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="f3003-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="f3003-178">關閉並重新執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3003-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="f3003-179">請注意，使用者工作階段會維持不變。</span><span class="sxs-lookup"><span data-stu-id="f3003-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="f3003-180">登出，再以另一個使用者身分重新登入。</span><span class="sxs-lookup"><span data-stu-id="f3003-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="f3003-181">ADAL 可讓您輕鬆地將這些常見的身分識別功能全部納入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3003-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="f3003-182">它會為您處理一切麻煩的事，包括快取管理、OAuth 通訊協定支援、向使用者顯示登入 UI、重新整理過期權杖等等。</span><span class="sxs-lookup"><span data-stu-id="f3003-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="f3003-183">您唯一需要知道的就是單一 API 呼叫， `authContext.AcquireToken*(…)`。</span><span class="sxs-lookup"><span data-stu-id="f3003-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="f3003-184">[這裡](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)提供完成的範例供您參考 (不含您的設定值)。</span><span class="sxs-lookup"><span data-stu-id="f3003-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="f3003-185">您現在可以繼續其他身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="f3003-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="f3003-186">您可以嘗試：</span><span class="sxs-lookup"><span data-stu-id="f3003-186">You may want to try:</span></span>

[<span data-ttu-id="f3003-187">使用 Azure AD 保護 .NET Web API >></span><span class="sxs-lookup"><span data-stu-id="f3003-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

