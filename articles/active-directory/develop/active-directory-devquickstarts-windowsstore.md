---
title: "開始使用 Azure AD Windows 市集 | Microsoft Docs"
description: "建置與 Azure AD 整合來進行登入的 Windows 市集應用程式，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="5b558-103">將 Azure AD 與 Windows 市集應用程式整合</span><span class="sxs-lookup"><span data-stu-id="5b558-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="5b558-104">Visual Studio 2017 不支援 Windows Store 8.1 和舊版專案。</span><span class="sxs-lookup"><span data-stu-id="5b558-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="5b558-105">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="5b558-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="5b558-106">如果您要開發 Windows 市集應用程式，Azure Active Directory (Azure AD) 可讓您簡單又直接地以 Active Directory 帳戶驗證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b558-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="5b558-107">透過與 Azure AD 整合，應用程式便可安全地使用任何受 Azure AD 保護的 Web API，例如 Office 365 API 或 Azure API。</span><span class="sxs-lookup"><span data-stu-id="5b558-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="5b558-108">針對需要存取受保護資源的 Windows 市集傳統型應用程式，Azure AD 提供了「Active Directory 驗證程式庫」(ADAL)。</span><span class="sxs-lookup"><span data-stu-id="5b558-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="5b558-109">ADAL 的唯一目的是要讓應用程式能夠容易取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="5b558-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="5b558-110">為了示範有多麼容易，本文將說明如何建置能夠執行下列操作的 DirectorySearcher Windows 市集應用程式︰</span><span class="sxs-lookup"><span data-stu-id="5b558-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="5b558-111">使用 [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)來取得呼叫 Azure AD Graph API 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="5b558-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="5b558-112">搜尋目錄以尋找具有指定使用者主體名稱 (UPN) 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b558-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="5b558-113">將使用者登出。</span><span class="sxs-lookup"><span data-stu-id="5b558-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="5b558-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="5b558-114">Before you get started</span></span>
* <span data-ttu-id="5b558-115">下載[基本架構專案](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip)或下載[完整的範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="5b558-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="5b558-116">每一個下載項目都是 Visual Studio 2015 解決方案。</span><span class="sxs-lookup"><span data-stu-id="5b558-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="5b558-117">您還需要一個可供建立使用者及註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5b558-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="5b558-118">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="5b558-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="5b558-119">當您準備就緒時，請依照接下來三個小節的程序操作。</span><span class="sxs-lookup"><span data-stu-id="5b558-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="5b558-120">步驟 1：註冊 DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="5b558-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="5b558-121">若要讓應用程式能夠取得權杖，您必須先在 Azure AD 租用戶中註冊該應用程式，然後授與它存取 Azure AD Graph API 的權限。</span><span class="sxs-lookup"><span data-stu-id="5b558-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="5b558-122">方式如下：</span><span class="sxs-lookup"><span data-stu-id="5b558-122">Here's how:</span></span>

1. <span data-ttu-id="5b558-123">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5b558-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5b558-124">在頂端列中，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b558-124">On the top bar, click your account.</span></span> <span data-ttu-id="5b558-125">然後，在 [目錄] 清單下，選取您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5b558-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="5b558-126">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="5b558-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5b558-127">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5b558-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="5b558-128">依照提示操作來建立「原生用戶端應用程式」。</span><span class="sxs-lookup"><span data-stu-id="5b558-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="5b558-129">[名稱] 可向使用者描述該應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b558-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="5b558-130">[重新導向 URI] 是配置與字串的組合，Azure AD 會用它來傳回權杖回應。</span><span class="sxs-lookup"><span data-stu-id="5b558-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="5b558-131">暫時先輸入一個預留位置值 (例如 **http://DirectorySearcher**)。</span><span class="sxs-lookup"><span data-stu-id="5b558-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="5b558-132">您稍後將會取代此值。</span><span class="sxs-lookup"><span data-stu-id="5b558-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="5b558-133">完成註冊之後，Azure AD 會為應用程式指派一個唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="5b558-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="5b558-134">複製 [應用程式] 索引標籤上的值，因為稍後將會需要它。</span><span class="sxs-lookup"><span data-stu-id="5b558-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="5b558-135">在 [設定] 頁面上，選取 [必要權限]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5b558-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="5b558-136">針對 **Azure Active Directory** 應用程式，選取 [Microsoft Graph] 作為 API。</span><span class="sxs-lookup"><span data-stu-id="5b558-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="5b558-137">在 [委派的權限] 下，新增 [以登入使用者的身分存取目錄] 權限。</span><span class="sxs-lookup"><span data-stu-id="5b558-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="5b558-138">這麼做可讓應用程式查詢使用者的 Graph API。</span><span class="sxs-lookup"><span data-stu-id="5b558-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="5b558-139">步驟 2：安裝及設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="5b558-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="5b558-140">既然您在 Azure AD 中已有應用程式，您現在便可安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="5b558-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="5b558-141">若要讓 ADAL 與 Azure AD 進行通訊，請提供它一些應用程式註冊相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5b558-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="5b558-142">藉由使用「套件管理器主控台」，將 ADAL 新增到 DirectorySearcher 專案中。</span><span class="sxs-lookup"><span data-stu-id="5b558-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="5b558-143">在 DirectorySearcher 專案中，開啟 MainPage.xaml.cs。</span><span class="sxs-lookup"><span data-stu-id="5b558-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="5b558-144">使用您在 Azure 入口網站中輸入的值來取代 [組態值] 區域中的值。</span><span class="sxs-lookup"><span data-stu-id="5b558-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="5b558-145">每當您的程式碼使用 ADAL 時，都會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="5b558-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="5b558-146">*tenant* 是您 Azure AD 租用戶的網域 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="5b558-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="5b558-147">*clientId* 是您從入口網站複製的應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="5b558-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="5b558-148">您現在必須找出 Windows 市集應用程式的回呼 URI。</span><span class="sxs-lookup"><span data-stu-id="5b558-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="5b558-149">在 `MainPage` 方法的這一行上設定中斷點：</span><span class="sxs-lookup"><span data-stu-id="5b558-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="5b558-150">建置方案，確認已還原所有封裝參考。</span><span class="sxs-lookup"><span data-stu-id="5b558-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="5b558-151">如果遺失任何封裝，請開啟「NuGet 封裝管理員」，然後將它們還原。</span><span class="sxs-lookup"><span data-stu-id="5b558-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="5b558-152">執行應用程式，然後在到達中斷點時複製 `redirectUri` 的值。</span><span class="sxs-lookup"><span data-stu-id="5b558-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="5b558-153">該值應該看起來如下：</span><span class="sxs-lookup"><span data-stu-id="5b558-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="5b558-154">回到 Azure 入口網站中應用程式的 [設定] 索引標籤上，新增具有上述值的 **RedirectUri**。</span><span class="sxs-lookup"><span data-stu-id="5b558-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="5b558-155">步驟 3：使用 ADAL 從 Azure AD 取得權杖</span><span class="sxs-lookup"><span data-stu-id="5b558-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="5b558-156">ADAL 背後的基本原則就是每當應用程式需要存取權杖時，只要呼叫 `authContext.AcquireToken(…)`，ADAL 就會執行其餘動作。</span><span class="sxs-lookup"><span data-stu-id="5b558-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="5b558-157">將應用程式的 `AuthenticationContext` (亦即 ADAL 的主要類別) 初始化。</span><span class="sxs-lookup"><span data-stu-id="5b558-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="5b558-158">此動作會將 ADAL 與 Azure AD 通訊所需的座標傳遞給 ADAL，並告訴它如何快取權杖。</span><span class="sxs-lookup"><span data-stu-id="5b558-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="5b558-159">找出 `Search(...)` 方法，這是在使用者按一下應用程式 UI 上的 [搜尋] 按鈕時所叫用的方法。</span><span class="sxs-lookup"><span data-stu-id="5b558-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="5b558-160">這個方法會對 Azure AD Graph API 發出 get 要求，以查詢是否有 UPN 開頭為指定搜尋詞彙的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b558-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="5b558-161">若要查詢 Graph API，請將存取權杖包含在該要求的 **Authorization** 標頭中。</span><span class="sxs-lookup"><span data-stu-id="5b558-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="5b558-162">這就是 ADAL 的切入點。</span><span class="sxs-lookup"><span data-stu-id="5b558-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="5b558-163">當應用程式透過呼叫 `AcquireTokenAsync(...)` 來要求權杖時，ADAL 會嘗試在不向使用者要求認證的情況下傳回權杖。</span><span class="sxs-lookup"><span data-stu-id="5b558-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="5b558-164">如果 ADAL 判斷使用者必須登入才能取得權杖，就會顯示登入對話方塊、收集使用者的認證，然後在驗證成功後傳回權杖。</span><span class="sxs-lookup"><span data-stu-id="5b558-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="5b558-165">如果 ADAL 因任何原因而無法傳回權杖，*AuthenticationResult* 狀態就會是錯誤。</span><span class="sxs-lookup"><span data-stu-id="5b558-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="5b558-166">現在可以開始使用您剛才取得的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="5b558-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="5b558-167">此外，請在 `Search(...)` 方法中，將該權杖附加至 Graph API get 要求的 **Authorization** 標頭：</span><span class="sxs-lookup"><span data-stu-id="5b558-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="5b558-168">您可以使用 `AuthenticationResult` 物件以在應用程式中顯示使用者的相關資訊，例如使用者的識別碼：</span><span class="sxs-lookup"><span data-stu-id="5b558-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="5b558-169">您也可以使用 ADAL 將使用者登出應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b558-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="5b558-170">當使用者按一下 [登出] 按鈕時，請確保下次呼叫 `AcquireTokenAsync(...)` 時會顯示登入檢視。</span><span class="sxs-lookup"><span data-stu-id="5b558-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="5b558-171">使用 ADAL 時，此動作就像清除權杖快取一樣簡單：</span><span class="sxs-lookup"><span data-stu-id="5b558-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="5b558-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b558-172">What's next</span></span>
<span data-ttu-id="5b558-173">您現在已擁有一個能夠運作的 Windows 市集應用程式，它可以驗證使用者、使用 OAuth 2.0 來安全地呼叫 Web API，以及取得使用者的相關基本資訊。</span><span class="sxs-lookup"><span data-stu-id="5b558-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="5b558-174">如果您尚未在租用戶中填入使用者，現在便可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="5b558-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="5b558-175">執行 DirectorySearcher 應用程式，然後使用其中一個使用者來登入。</span><span class="sxs-lookup"><span data-stu-id="5b558-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="5b558-176">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="5b558-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="5b558-177">關閉應用程式，然後重新執行它。</span><span class="sxs-lookup"><span data-stu-id="5b558-177">Close the app, and rerun it.</span></span> <span data-ttu-id="5b558-178">請注意，使用者工作階段會維持不變。</span><span class="sxs-lookup"><span data-stu-id="5b558-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="5b558-179">透過按一下滑鼠右鍵以顯示底部列來登出，然後以其他使用者身分重新登入。</span><span class="sxs-lookup"><span data-stu-id="5b558-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="5b558-180">ADAL 可讓您輕鬆地將所有這些常見的身分識別功能納入應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5b558-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="5b558-181">它會為您處理所有麻煩的工作，包括快取管理、OAuth 通訊協定支援、向使用者顯示登入 UI，以及重新整理過期權杖。</span><span class="sxs-lookup"><span data-stu-id="5b558-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="5b558-182">您只需要知道單一 API 呼叫 `authContext.AcquireToken*(…)`。</span><span class="sxs-lookup"><span data-stu-id="5b558-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="5b558-183">如需參考資料，請下載[完整的範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (不含您的組態值)。</span><span class="sxs-lookup"><span data-stu-id="5b558-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="5b558-184">您現在可以繼續其他身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="5b558-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="5b558-185">例如，嘗試[使用 Azure AD 來保護 .NET Web API](active-directory-devquickstarts-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="5b558-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
