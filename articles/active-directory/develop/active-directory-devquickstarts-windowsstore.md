---
title: "aaaAzure AD Windows 市集開始使用 |Microsoft 文件"
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
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="63a34-103">將 Azure AD 與 Windows 市集應用程式整合</span><span class="sxs-lookup"><span data-stu-id="63a34-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="63a34-104">Visual Studio 2017 不支援 Windows Store 8.1 和舊版專案。</span><span class="sxs-lookup"><span data-stu-id="63a34-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="63a34-105">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="63a34-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="63a34-106">如果您正在開發 hello Windows 市集應用程式，Azure Active Directory (Azure AD)，使其簡單又直接 tooauthenticate 您的使用者使用其 Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="63a34-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="63a34-107">藉由整合與 Azure AD，應用程式可以安全地使用任何 web 應用程式開發介面中受到 Azure AD，例如 Office 365 Api hello 或 hello Azure API。</span><span class="sxs-lookup"><span data-stu-id="63a34-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="63a34-108">針對 Windows 市集桌面應用程式需要 tooaccess 受保護的資源，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="63a34-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="63a34-109">hello 的 ADAL 的唯一目的是 toomake 輕鬆 hello 應用程式 tooget 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="63a34-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="63a34-110">toodemonstrate 多麼容易的是，本文將說明如何 toobuild DirectorySearcher Windows 市集應用程式的：</span><span class="sxs-lookup"><span data-stu-id="63a34-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="63a34-111">取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。</span><span class="sxs-lookup"><span data-stu-id="63a34-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="63a34-112">搜尋目錄以尋找具有指定使用者主體名稱 (UPN) 的使用者。</span><span class="sxs-lookup"><span data-stu-id="63a34-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="63a34-113">將使用者登出。</span><span class="sxs-lookup"><span data-stu-id="63a34-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="63a34-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="63a34-114">Before you get started</span></span>
* <span data-ttu-id="63a34-115">下載 hello[基本架構專案](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip)，或下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="63a34-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="63a34-116">每一個下載項目都是 Visual Studio 2015 解決方案。</span><span class="sxs-lookup"><span data-stu-id="63a34-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="63a34-117">您也需要哪些 toocreate 使用者和註冊 hello 應用程式中的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="63a34-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="63a34-118">如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="63a34-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="63a34-119">當您準備好時，後續 hello 程序在 hello 接下來三個區段。</span><span class="sxs-lookup"><span data-stu-id="63a34-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="63a34-120">步驟 1： 註冊 hello DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="63a34-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="63a34-121">tooenable hello 應用程式 tooget 語彙基元，您必須先 tooregister 在您的 Azure AD 租用戶，並授與權限 tooaccess hello Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="63a34-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="63a34-122">方式如下：</span><span class="sxs-lookup"><span data-stu-id="63a34-122">Here's how:</span></span>

1. <span data-ttu-id="63a34-123">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="63a34-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="63a34-124">Hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="63a34-124">On hello top bar, click your account.</span></span> <span data-ttu-id="63a34-125">然後，在 hello**目錄**清單中，選取 hello Active Directory 租用戶想 tooregister hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="63a34-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="63a34-126">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="63a34-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="63a34-127">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="63a34-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="63a34-128">請遵循 hello 提示 toocreate**原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="63a34-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="63a34-129">**名稱**描述 hello 應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="63a34-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="63a34-130">**重新導向 URI**是配置和字串的組合，Azure AD 使用 tooreturn 權杖回應。</span><span class="sxs-lookup"><span data-stu-id="63a34-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="63a34-131">暫時先輸入一個預留位置值 (例如 **http://DirectorySearcher**)。</span><span class="sxs-lookup"><span data-stu-id="63a34-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="63a34-132">您稍後將取代 hello 值。</span><span class="sxs-lookup"><span data-stu-id="63a34-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="63a34-133">Hello 註冊完成之後，Azure AD 會指派給 hello 應用程式是唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="63a34-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="63a34-134">複製在 hello hello 值**應用程式**索引標籤上，因為您將需要更新版本。</span><span class="sxs-lookup"><span data-stu-id="63a34-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="63a34-135">在 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="63a34-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="63a34-136">Hello **Azure Active Directory**應用程式中，選取**Microsoft Graph**為 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="63a34-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="63a34-137">在下**委派的權限**，新增 hello **hello 登入的使用者身分存取 hello 目錄**權限。</span><span class="sxs-lookup"><span data-stu-id="63a34-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="63a34-138">如此可讓 hello 應用程式 tooquery hello Graph API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="63a34-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="63a34-139">步驟 2：安裝及設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="63a34-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="63a34-140">既然您在 Azure AD 中已有應用程式，您現在便可安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="63a34-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="63a34-141">tooenable ADAL toocommunicate 與 Azure AD，不妨 hello 應用程式註冊的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="63a34-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="63a34-142">使用 Package Manager Console hello 新增 ADAL toohello DirectorySearcher 專案。</span><span class="sxs-lookup"><span data-stu-id="63a34-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="63a34-143">在 hello DirectorySearcher 專案中，開啟 MainPage.xaml.cs。</span><span class="sxs-lookup"><span data-stu-id="63a34-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="63a34-144">Hello 中的 hello 值取代為**組態值**區域與您輸入 hello Azure 入口網站中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="63a34-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="63a34-145">您的程式碼是指 toothese 值，每當它會使用 ADAL。</span><span class="sxs-lookup"><span data-stu-id="63a34-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="63a34-146">hello*租用戶*hello 網域，您的 Azure AD 租用戶 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="63a34-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="63a34-147">hello *clientId* hello hello 應用程式，您所複製 hello 入口網站的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="63a34-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="63a34-148">您現在會針對 Windows 市集應用程式需要 toodiscover hello 回呼 URI。</span><span class="sxs-lookup"><span data-stu-id="63a34-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="63a34-149">在 hello 中這一行設定中斷點`MainPage`方法：</span><span class="sxs-lookup"><span data-stu-id="63a34-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="63a34-150">建置 hello 方案，並確認封裝的所有參考都會都還原。</span><span class="sxs-lookup"><span data-stu-id="63a34-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="63a34-151">如果遺漏任何套件，請開啟 hello NuGet 封裝管理員，並加以還原。</span><span class="sxs-lookup"><span data-stu-id="63a34-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="63a34-152">執行 hello 應用程式，並將複製的 hello 值`redirectUri`hello 中斷點叫用時。</span><span class="sxs-lookup"><span data-stu-id="63a34-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="63a34-153">hello 值看起來應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="63a34-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="63a34-154">在 [hello**設定**hello Azure 入口網站中的 hello 應用程式] 索引標籤加入**RedirectUri**以 hello 上述值。</span><span class="sxs-lookup"><span data-stu-id="63a34-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="63a34-155">從 Azure AD 的步驟 3： 使用 ADAL tooget 語彙基元</span><span class="sxs-lookup"><span data-stu-id="63a34-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="63a34-156">hello ADAL 背後的基本原則是，每當 hello 應用程式需要存取權杖，它只會呼叫`authContext.AcquireToken(…)`，ADAL 沒有 hello rest 和。</span><span class="sxs-lookup"><span data-stu-id="63a34-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="63a34-157">初始化 hello 應用程式`AuthenticationContext`，這是 hello 的 ADAL 的主要類別。</span><span class="sxs-lookup"><span data-stu-id="63a34-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="63a34-158">這個動作會傳遞 ADAL hello 座標與 Azure AD toocommunicate 地告訴它如何 toocache 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="63a34-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="63a34-159">找出 hello`Search(...)`方法，當使用者按一下 hello 叫用**搜尋**hello 應用程式的 UI 上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="63a34-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="63a34-160">這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello get 要求 Azure AD Graph API toohello tooquery。</span><span class="sxs-lookup"><span data-stu-id="63a34-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="63a34-161">tooquery hello Graph API hello 要求中包含存取權杖**授權**標頭。</span><span class="sxs-lookup"><span data-stu-id="63a34-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="63a34-162">這就是 ADAL 的切入點。</span><span class="sxs-lookup"><span data-stu-id="63a34-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="63a34-163">當 hello 應用程式藉由呼叫要求語彙基元`AcquireTokenAsync(...)`，ADAL 會嘗試 tooreturn 語彙基元不要求 hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="63a34-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="63a34-164">如果 ADAL 會判斷該 hello 使用者需要 toosign tooget 語彙基元中的，它會顯示登入對話方塊中，會收集 hello 使用者的認證，而且在驗證成功後，傳回的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="63a34-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="63a34-165">如果 ADAL 因故無法 tooreturn 語彙基元，hello *AuthenticationResult*是錯誤的狀態。</span><span class="sxs-lookup"><span data-stu-id="63a34-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="63a34-166">現在它是您剛擷取時間 toouse hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="63a34-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="63a34-167">此外在 hello`Search(...)`方法，附加 hello Graph API 中 hello 取得要求的語彙基元 toohello**授權**標頭：</span><span class="sxs-lookup"><span data-stu-id="63a34-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="63a34-168">您可以使用 hello`AuthenticationResult`物件 toodisplay hello 應用程式，例如 hello 使用者的識別碼中的 hello 使用者資訊：</span><span class="sxs-lookup"><span data-stu-id="63a34-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="63a34-169">您也可以使用 ADAL toosign hello 應用程式外的使用者。</span><span class="sxs-lookup"><span data-stu-id="63a34-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="63a34-170">當 hello 使用者按一下 hello**登出**按鈕，請確定該 hello 下一個呼叫太`AcquireTokenAsync(...)`顯示登入的檢視。</span><span class="sxs-lookup"><span data-stu-id="63a34-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="63a34-171">使用 ADAL，此動作非常簡單，只要清除 hello 權杖快取的：</span><span class="sxs-lookup"><span data-stu-id="63a34-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="63a34-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63a34-172">What's next</span></span>
<span data-ttu-id="63a34-173">現在，您會有可運作的 Windows 市集應用程式可以驗證使用者，安全地呼叫 web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="63a34-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="63a34-174">如果您沒有已填入您的租用戶與使用者，現在是 hello 時間 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="63a34-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="63a34-175">執行 DirectorySearcher 應用程式，然後使用其中一個 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="63a34-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="63a34-176">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="63a34-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="63a34-177">關閉 hello 應用程式，並重新執行它。</span><span class="sxs-lookup"><span data-stu-id="63a34-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="63a34-178">請注意如何 hello 使用者工作階段會保持不變。</span><span class="sxs-lookup"><span data-stu-id="63a34-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="63a34-179">以滑鼠右鍵按一下 toodisplay hello 下方列，登出，再以其他使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="63a34-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="63a34-180">ADAL 可讓您輕鬆 tooincorporate 所有 hello 應用程式到這些一般身分識別功能。</span><span class="sxs-lookup"><span data-stu-id="63a34-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="63a34-181">它會負責所有 hello dirty 工作，例如快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，並重新整理過期語彙基元。</span><span class="sxs-lookup"><span data-stu-id="63a34-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="63a34-182">您需要 tooknow 單一 API 呼叫`authContext.AcquireToken*(…)`。</span><span class="sxs-lookup"><span data-stu-id="63a34-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="63a34-183">如需參考，下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)（不含您的組態值）。</span><span class="sxs-lookup"><span data-stu-id="63a34-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="63a34-184">您現在可以移動 tooadditional 身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="63a34-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="63a34-185">例如，嘗試[使用 Azure AD 來保護 .NET Web API](active-directory-devquickstarts-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="63a34-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
