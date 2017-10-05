---
title: "開始使用 Azure AD Xamarin | Microsoft Docs"
description: "建置 Xamarin 應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="bd772-103">將 Azure AD 整合至 Xamarin 應用程式</span><span class="sxs-lookup"><span data-stu-id="bd772-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="bd772-104">Xamarin 可讓您使用 C# 撰寫可在 iOS、Android 和 Windows (行動裝置和電腦) 上執行的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd772-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="bd772-105">如果您正在建置使用 Xamarin 的應用程式，Azure Active Directory (Azure AD) 可讓您簡單地以其 Azure AD 帳戶驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="bd772-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="bd772-106">應用程式也可以安全地使用任何受 Azure AD 保護的 Web API，例如 Office 365 API 或 Azure API。</span><span class="sxs-lookup"><span data-stu-id="bd772-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="bd772-107">對於需要存取受保護資源的 Xamarin 應用程式，Azure AD 提供 Active Directory 驗證程式庫 (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="bd772-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="bd772-108">ADAL 的唯一目的是為了讓應用程式輕鬆取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="bd772-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="bd772-109">為了示範有多麼容易，本文說明如何建置 DirectorySearcher 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="bd772-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="bd772-110">可在 iOS、Android、Windows 桌面、Windows Phone 和 Windows 市集上執行。</span><span class="sxs-lookup"><span data-stu-id="bd772-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="bd772-111">使用單一可攜式類別庫 (PCL) 來驗證使用者並取得 Azure AD Graph API 的權杖。</span><span class="sxs-lookup"><span data-stu-id="bd772-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="bd772-112">搜尋目錄以尋找具有指定 UPN 的使用者。</span><span class="sxs-lookup"><span data-stu-id="bd772-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="bd772-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="bd772-113">Before you get started</span></span>
* <span data-ttu-id="bd772-114">下載[基本架構專案](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip)或下載[完整的範例](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="bd772-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="bd772-115">每一個下載都是 Visual Studio 2013 解決方案。</span><span class="sxs-lookup"><span data-stu-id="bd772-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="bd772-116">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bd772-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="bd772-117">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="bd772-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="bd772-118">當您準備就緒，請遵循接下來四個章節的程序。</span><span class="sxs-lookup"><span data-stu-id="bd772-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="bd772-119">步驟 1：設定您的 Xamarin 開發環境</span><span class="sxs-lookup"><span data-stu-id="bd772-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="bd772-120">因為本教學課程包含 iOS、Android 和 Windows 專案，所以您需要 Visual Studio 和 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="bd772-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="bd772-121">若要建立必要的環境，請完成 MSDN 上[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) 的處理。</span><span class="sxs-lookup"><span data-stu-id="bd772-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="bd772-122">這些指示包含的資料，可供您於等待安裝完成時檢閱，以深入了解 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="bd772-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="bd772-123">完成設定之後，您可以在 Visual Studio 中開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="bd772-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="bd772-124">您會在其中看到六個專案：五個平台特定專案和一個 PCL，DirectorySearcher.cs，可跨所有平台共用。</span><span class="sxs-lookup"><span data-stu-id="bd772-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="bd772-125">步驟 2：註冊 DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="bd772-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="bd772-126">若要讓應用程式取得權杖，您必須先在 Azure AD 租用戶中註冊這個應用程式，並授權它存取 Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="bd772-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="bd772-127">方式如下：</span><span class="sxs-lookup"><span data-stu-id="bd772-127">Here's how:</span></span>

1. <span data-ttu-id="bd772-128">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bd772-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bd772-129">在頂端列中，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd772-129">On the top bar, click your account.</span></span> <span data-ttu-id="bd772-130">然後，在 [目錄] 清單下，選取您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bd772-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="bd772-131">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="bd772-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="bd772-132">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bd772-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="bd772-133">若要建立新的**原生用戶端應用程式**，請遵照提示進行。</span><span class="sxs-lookup"><span data-stu-id="bd772-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="bd772-134">[名稱] 向使用者說明該應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd772-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="bd772-135">[重新導向 URI] 是配置和字串的組合，Azure AD 可用它來傳回權杖回應。</span><span class="sxs-lookup"><span data-stu-id="bd772-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="bd772-136">輸入值，(例如， http://DirectorySearcher )。</span><span class="sxs-lookup"><span data-stu-id="bd772-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="bd772-137">完成註冊之後，Azure AD 會為應用程式指派唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="bd772-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="bd772-138">從 [應用程式] 索引標籤複製值，因為稍後將會需要它。</span><span class="sxs-lookup"><span data-stu-id="bd772-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="bd772-139">在 [設定] 頁面中，選取 [必要的權限]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bd772-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="bd772-140">選取 [Microsoft Graph] 做為 API。</span><span class="sxs-lookup"><span data-stu-id="bd772-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="bd772-141">在 [委派的權限] 下，新增 [讀取目錄資料] 權限。</span><span class="sxs-lookup"><span data-stu-id="bd772-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="bd772-142">這個動作可讓應用程式查詢使用者的圖形 API。</span><span class="sxs-lookup"><span data-stu-id="bd772-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="bd772-143">步驟 3：安裝及設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="bd772-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="bd772-144">既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="bd772-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="bd772-145">若要讓 ADAL 與 Azure AD 進行通訊，請提供它一些應用程式註冊相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bd772-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="bd772-146">使用 Package Manager Console 將 ADAL 新增到 DirectorySearcher 專案中。</span><span class="sxs-lookup"><span data-stu-id="bd772-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="bd772-147">請注意，每個專案會新增兩個程式庫參考：ADAL 的 PCL 部分和平台特定部分。</span><span class="sxs-lookup"><span data-stu-id="bd772-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="bd772-148">在 DirectorySearcherLib 專案中，開啟 DirectorySearcher.cs。</span><span class="sxs-lookup"><span data-stu-id="bd772-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="bd772-149">將類別成員值取代為您在 Azure 入口網站中輸入的值。</span><span class="sxs-lookup"><span data-stu-id="bd772-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="bd772-150">每當使用 ADAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="bd772-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="bd772-151">*tenant* 是您 Azure AD 租用戶的網域 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="bd772-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="bd772-152">ClientId 是您從入口網站複製的應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="bd772-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="bd772-153">ReturnUri 是您在入口網站中輸入的重新導向 URI (例如， http://DirectorySearcher )。</span><span class="sxs-lookup"><span data-stu-id="bd772-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="bd772-154">步驟 4：使用 ADAL 來取得 Azure AD 的權杖</span><span class="sxs-lookup"><span data-stu-id="bd772-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="bd772-155">幾乎所有應用程式的驗證邏輯採用 `DirectorySearcher.SearchByAlias(...)`。</span><span class="sxs-lookup"><span data-stu-id="bd772-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="bd772-156">平台特定專案所需的只是將內容參數傳遞至 `DirectorySearcher` PCL。</span><span class="sxs-lookup"><span data-stu-id="bd772-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="bd772-157">開啟DirectorySearcher.cs，然後將新的參數新增至 `SearchByAlias(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="bd772-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="bd772-158">`IPlatformParameters` 是個內容參數，其中包含 ADAL 必須執行驗證的平台特定物件。</span><span class="sxs-lookup"><span data-stu-id="bd772-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="bd772-159">初始化 `AuthenticationContext`，這是 ADAL 的主要類別。</span><span class="sxs-lookup"><span data-stu-id="bd772-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="bd772-160">這個動作會傳遞它與 Azure AD 通訊所需的 ADAL 座標。</span><span class="sxs-lookup"><span data-stu-id="bd772-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="bd772-161">呼叫 `AcquireTokenAsync(...)`，它可接受 `IPlatformParameters` 物件，並叫用將權杖傳回應用程式所需的驗證流程。</span><span class="sxs-lookup"><span data-stu-id="bd772-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="bd772-162">`AcquireTokenAsync(...)` 會先嘗試為要求的資源 (在此範例中會是圖形 API) 傳回權杖，而不提示使用者輸入其認證 (透過快取或重新整理舊的權杖)。</span><span class="sxs-lookup"><span data-stu-id="bd772-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="bd772-163">必要時，它才會在取得要求的權杖之前，對使用者顯示 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="bd772-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="bd772-164">將存取權杖附加至**授權**標頭中的圖形 API 要求：</span><span class="sxs-lookup"><span data-stu-id="bd772-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="bd772-165">`DirectorySearcher` PCL 和應用程式的身分識別相關程式碼到此告一段落。</span><span class="sxs-lookup"><span data-stu-id="bd772-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="bd772-166">剩下的工作只是在每個平台檢視中呼叫 `SearchByAlias(...)` 方法，並在必要的地方新增程式碼以便正確地處理 UI 生命週期。</span><span class="sxs-lookup"><span data-stu-id="bd772-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="bd772-167">Android</span><span class="sxs-lookup"><span data-stu-id="bd772-167">Android</span></span>
1. <span data-ttu-id="bd772-168">在 MainActivity.cs 中，在按鈕點擊處理常式中新增 `SearchByAlias(...)` 的呼叫：</span><span class="sxs-lookup"><span data-stu-id="bd772-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="bd772-169">覆寫 `OnActivityResult` 生命週期方法，將任何驗證重新導向轉送回到適當的方法。</span><span class="sxs-lookup"><span data-stu-id="bd772-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="bd772-170">ADAL 針對 Android 中的此項作業提供協助程式方法：</span><span class="sxs-lookup"><span data-stu-id="bd772-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="bd772-171">Windows 桌面</span><span class="sxs-lookup"><span data-stu-id="bd772-171">Windows Desktop</span></span>
<span data-ttu-id="bd772-172">在 MainWindow.xaml.cs 中，只需進行 `SearchByAlias(...)` 呼叫，即可在桌面的 `PlatformParameters` 物件中傳遞 `WindowInteropHelper`：</span><span class="sxs-lookup"><span data-stu-id="bd772-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="bd772-173">iOS</span><span class="sxs-lookup"><span data-stu-id="bd772-173">iOS</span></span>
<span data-ttu-id="bd772-174">在 DirSearchClient_iOSViewController.cs 中，iOS `PlatformParameters` 物件會參考檢視控制器︰</span><span class="sxs-lookup"><span data-stu-id="bd772-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="bd772-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="bd772-175">Windows Universal</span></span>
<span data-ttu-id="bd772-176">在 Windows 通用中，開啟 MainPage.xaml.cs，然後實作 `Search` 方法。</span><span class="sxs-lookup"><span data-stu-id="bd772-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="bd772-177">此方法會使用共用專案中的協助程式方法，視需要更新 UI。</span><span class="sxs-lookup"><span data-stu-id="bd772-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="bd772-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd772-178">What's next</span></span>
<span data-ttu-id="bd772-179">您現在擁有一個能夠在五個不同平台之間驗證使用者並使用 OAuth 2.0 安全地呼叫 Web API 的運作中 Xamarin 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd772-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="bd772-180">如果您還沒有這麼做，現在是將使用者植入租用戶的時候。</span><span class="sxs-lookup"><span data-stu-id="bd772-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="bd772-181">執行 DirectorySearcher 應用程式，然後使用其中一個使用者來登入。</span><span class="sxs-lookup"><span data-stu-id="bd772-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="bd772-182">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="bd772-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="bd772-183">ADAL 可讓您輕鬆地將常見的身分識別功能納入應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd772-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="bd772-184">它會為您處理一切麻煩的事，包括快取管理、OAuth 通訊協定支援、向使用者顯示登入 UI，以及重新整理過期權杖。</span><span class="sxs-lookup"><span data-stu-id="bd772-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="bd772-185">您只需要知道單一 API 呼叫 `authContext.AcquireToken*(…)`。</span><span class="sxs-lookup"><span data-stu-id="bd772-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="bd772-186">如需參考資料，請下載[完整的範例](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (不含您的組態值)。</span><span class="sxs-lookup"><span data-stu-id="bd772-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="bd772-187">您現在可以繼續其他身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="bd772-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="bd772-188">例如，嘗試[使用 Azure AD 來保護 .NET Web API](active-directory-devquickstarts-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="bd772-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
