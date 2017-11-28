---
title: "aaaAzure AD Xamarin 使用者入門 |Microsoft 文件"
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
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="2b434-103">將 Azure AD 整合至 Xamarin 應用程式</span><span class="sxs-lookup"><span data-stu-id="2b434-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="2b434-104">Xamarin 可讓您使用 C# 撰寫可在 iOS、Android 和 Windows (行動裝置和電腦) 上執行的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b434-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="2b434-105">如果您要建置 xamarin 應用程式，Azure Active Directory (Azure AD)，使其具有其 Azure AD 帳戶的簡單 tooauthenticate 使用者。</span><span class="sxs-lookup"><span data-stu-id="2b434-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="2b434-106">hello 應用程式安全地也可以使用任何受 Azure AD，例如 Office 365 Api hello 或 hello Azure 應用程式開發介面的 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="2b434-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="2b434-107">針對需要 tooaccess 受保護資源的 Xamarin 應用程式，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL)。</span><span class="sxs-lookup"><span data-stu-id="2b434-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="2b434-108">hello 的 ADAL 的唯一目的是 toomake 輕鬆的應用程式 tooget 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="2b434-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="2b434-109">是，本文將說明如何輕鬆 toodemonstrate 如何 toobuild DirectorySearcher 應用程式的：</span><span class="sxs-lookup"><span data-stu-id="2b434-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="2b434-110">可在 iOS、Android、Windows 桌面、Windows Phone 和 Windows 市集上執行。</span><span class="sxs-lookup"><span data-stu-id="2b434-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="2b434-111">使用單一的可攜式類別庫 (PCL) tooauthenticate 使用者，並取得 hello Azure AD Graph API 的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="2b434-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="2b434-112">搜尋目錄以尋找具有指定 UPN 的使用者。</span><span class="sxs-lookup"><span data-stu-id="2b434-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="2b434-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="2b434-113">Before you get started</span></span>
* <span data-ttu-id="2b434-114">下載 hello[基本架構專案](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip)，或下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="2b434-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="2b434-115">每一個下載都是 Visual Studio 2013 解決方案。</span><span class="sxs-lookup"><span data-stu-id="2b434-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="2b434-116">您也需要哪些 toocreate 使用者和註冊 hello 應用程式中的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2b434-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="2b434-117">如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="2b434-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="2b434-118">當您準備好時，後續 hello 程序在 hello 接下來四個區段。</span><span class="sxs-lookup"><span data-stu-id="2b434-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="2b434-119">步驟 1：設定您的 Xamarin 開發環境</span><span class="sxs-lookup"><span data-stu-id="2b434-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="2b434-120">因為本教學課程包含 iOS、Android 和 Windows 專案，所以您需要 Visual Studio 和 Xamarin。</span><span class="sxs-lookup"><span data-stu-id="2b434-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="2b434-121">toocreate hello 所需的環境，完成 hello 程序中[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="2b434-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="2b434-122">hello 指示包含正在等待 hello 安裝 toobe 完成時，您可以檢閱 toolearn 深入了解 Xamarin 的資料。</span><span class="sxs-lookup"><span data-stu-id="2b434-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="2b434-123">Hello 安裝程式完成之後，請在 Visual Studio 中開啟 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="2b434-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="2b434-124">您會在其中看到六個專案：五個平台特定專案和一個 PCL，DirectorySearcher.cs，可跨所有平台共用。</span><span class="sxs-lookup"><span data-stu-id="2b434-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="2b434-125">步驟 2： 註冊 hello DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="2b434-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="2b434-126">tooenable hello 應用程式 tooget 語彙基元，您必須先 tooregister 在您的 Azure AD 租用戶，並授與權限 tooaccess hello Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="2b434-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="2b434-127">方式如下：</span><span class="sxs-lookup"><span data-stu-id="2b434-127">Here's how:</span></span>

1. <span data-ttu-id="2b434-128">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2b434-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2b434-129">Hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b434-129">On hello top bar, click your account.</span></span> <span data-ttu-id="2b434-130">然後，在 hello**目錄**清單中，選取 hello Active Directory 租用戶想 tooregister hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b434-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="2b434-131">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="2b434-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="2b434-132">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2b434-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="2b434-133">新的 toocreate**原生用戶端應用程式**，依照 hello 提示。</span><span class="sxs-lookup"><span data-stu-id="2b434-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="2b434-134">**名稱**描述 hello 應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="2b434-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="2b434-135">**重新導向 URI**是配置和字串的組合，Azure AD 使用 tooreturn 權杖回應。</span><span class="sxs-lookup"><span data-stu-id="2b434-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="2b434-136">輸入值，(例如， http://DirectorySearcher )。</span><span class="sxs-lookup"><span data-stu-id="2b434-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="2b434-137">完成註冊之後，Azure AD 會指派給 hello 應用程式是唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="2b434-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="2b434-138">從 hello 複製 hello 值**應用程式**索引標籤上，因為您將需要更新版本。</span><span class="sxs-lookup"><span data-stu-id="2b434-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="2b434-139">在 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="2b434-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="2b434-140">選取**Microsoft Graph**為 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="2b434-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="2b434-141">在下**委派的權限**，新增 hello**讀取目錄資料**權限。</span><span class="sxs-lookup"><span data-stu-id="2b434-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="2b434-142">這個動作可讓 hello 應用程式 tooquery hello Graph API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="2b434-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="2b434-143">步驟 3：安裝及設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="2b434-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="2b434-144">既然您在 Azure AD 中已有應用程式，您現在便可安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b434-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="2b434-145">tooenable ADAL toocommunicate 與 Azure AD，不妨 hello 應用程式註冊的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="2b434-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="2b434-146">使用 Package Manager Console hello 新增 ADAL toohello DirectorySearcher 專案。</span><span class="sxs-lookup"><span data-stu-id="2b434-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

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

    <span data-ttu-id="2b434-147">請注意這兩個程式庫參考會加入 tooeach 專案： hello PCL 部分 ADAL 與平台專屬部分。</span><span class="sxs-lookup"><span data-stu-id="2b434-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="2b434-148">在 hello DirectorySearcherLib 專案中，開啟 DirectorySearcher.cs。</span><span class="sxs-lookup"><span data-stu-id="2b434-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="2b434-149">Hello 類別成員值取代為您輸入 hello Azure 入口網站中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="2b434-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="2b434-150">您的程式碼是指 toothese 值，每當它會使用 ADAL。</span><span class="sxs-lookup"><span data-stu-id="2b434-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="2b434-151">hello*租用戶*hello 網域，您的 Azure AD 租用戶 (例如 contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="2b434-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="2b434-152">hello *clientId* hello hello 應用程式，您所複製 hello 入口網站的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2b434-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="2b434-153">hello *returnUri*是 hello 重新導向在 hello 入口網站 (例如，http://DirectorySearcher) 中所輸入的 URI。</span><span class="sxs-lookup"><span data-stu-id="2b434-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="2b434-154">從 Azure AD 的步驟 4： 使用 ADAL tooget 語彙基元</span><span class="sxs-lookup"><span data-stu-id="2b434-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="2b434-155">幾乎所有的 hello 應用程式的驗證邏輯在於`DirectorySearcher.SearchByAlias(...)`。</span><span class="sxs-lookup"><span data-stu-id="2b434-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="2b434-156">所有 hello 平台專屬專案中，必須是 toopass 內容參數 toohello `DirectorySearcher` PCL。</span><span class="sxs-lookup"><span data-stu-id="2b434-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="2b434-157">開啟 DirectorySearcher.cs，，然後加入新的參數 toohello`SearchByAlias(...)`方法。</span><span class="sxs-lookup"><span data-stu-id="2b434-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="2b434-158">`IPlatformParameters`是 hello 封裝 hello 平台專屬的內容參數物件 ADAL 的需求 tooperform hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="2b434-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="2b434-159">初始化`AuthenticationContext`，這是 hello 的 ADAL 的主要類別。</span><span class="sxs-lookup"><span data-stu-id="2b434-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="2b434-160">此動作將 ADAL hello 協調其需求 toocommunicate 與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="2b434-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="2b434-161">呼叫`AcquireTokenAsync(...)`，它會接受 hello`IPlatformParameters`物件，並叫用 hello 是必要的 tooreturn 語彙基元 toohello 應用程式的驗證流程。</span><span class="sxs-lookup"><span data-stu-id="2b434-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

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

    <span data-ttu-id="2b434-162">`AcquireTokenAsync(...)`第一次嘗試 tooreturn hello 的語彙基元要求而不提示使用者 tooenter 其認證 （透過快取，或重新整理舊的權杖） 的資源 (在本例中的 hello Graph API)。</span><span class="sxs-lookup"><span data-stu-id="2b434-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="2b434-163">在必要時，它會顯示使用者 hello Azure AD 登入頁面之前取得 hello 要求的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="2b434-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="2b434-164">附加 hello 存取語彙基元 toohello Graph API 要求中 hello**授權**標頭：</span><span class="sxs-lookup"><span data-stu-id="2b434-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="2b434-165">這就是 hello `DirectorySearcher` PCL 和 hello 應用程式的身分識別相關的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2b434-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="2b434-166">剩下的就是 toocall hello`SearchByAlias(...)`每個平台檢視中的方法和 tooadd 正確處理程式碼在需要時，hello UI 生命週期。</span><span class="sxs-lookup"><span data-stu-id="2b434-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="2b434-167">Android</span><span class="sxs-lookup"><span data-stu-id="2b434-167">Android</span></span>
1. <span data-ttu-id="2b434-168">Weatherapp，在加入呼叫太`SearchByAlias(...)`hello 按鈕中按一下 處理常式：</span><span class="sxs-lookup"><span data-stu-id="2b434-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="2b434-169">覆寫 hello`OnActivityResult`存留週期方法 tooforward 任何驗證重新導向後 toohello 適當的方法。</span><span class="sxs-lookup"><span data-stu-id="2b434-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="2b434-170">ADAL 針對 Android 中的此項作業提供協助程式方法：</span><span class="sxs-lookup"><span data-stu-id="2b434-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="2b434-171">Windows 桌面</span><span class="sxs-lookup"><span data-stu-id="2b434-171">Windows Desktop</span></span>
<span data-ttu-id="2b434-172">將 MainWindow.xaml.cs 中, 進行呼叫太`SearchByAlias(...)`藉由傳遞`WindowInteropHelper`hello desktop`PlatformParameters`物件：</span><span class="sxs-lookup"><span data-stu-id="2b434-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="2b434-173">iOS</span><span class="sxs-lookup"><span data-stu-id="2b434-173">iOS</span></span>
<span data-ttu-id="2b434-174">在 DirSearchClient_iOSViewController.cs，hello iOS`PlatformParameters`物件會使用參考 toohello 檢視控制器：</span><span class="sxs-lookup"><span data-stu-id="2b434-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="2b434-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="2b434-175">Windows Universal</span></span>
<span data-ttu-id="2b434-176">在 Windows 通用，開啟 MainPage.xaml.cs，然後實作 hello`Search`方法。</span><span class="sxs-lookup"><span data-stu-id="2b434-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="2b434-177">這個方法會視需要共用的專案 tooupdate UI 中使用的 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="2b434-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="2b434-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b434-178">What's next</span></span>
<span data-ttu-id="2b434-179">您現在擁有一個能夠在五個不同平台之間驗證使用者並使用 OAuth 2.0 安全地呼叫 Web API 的運作中 Xamarin 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b434-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="2b434-180">如果您沒有已填入您的租用戶與使用者，現在是 hello 時間 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="2b434-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="2b434-181">執行 DirectorySearcher 應用程式，然後使用其中一個 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="2b434-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="2b434-182">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="2b434-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="2b434-183">ADAL 可讓一般身分識別功能輕鬆 tooincorporate 到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2b434-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="2b434-184">它會負責所有 hello dirty 工作，例如快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，並重新整理過期語彙基元。</span><span class="sxs-lookup"><span data-stu-id="2b434-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="2b434-185">您需要 tooknow 單一 API 呼叫`authContext.AcquireToken*(…)`。</span><span class="sxs-lookup"><span data-stu-id="2b434-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="2b434-186">如需參考，下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)（不含您的組態值）。</span><span class="sxs-lookup"><span data-stu-id="2b434-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="2b434-187">您現在可以移動 tooadditional 身分識別案例。</span><span class="sxs-lookup"><span data-stu-id="2b434-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="2b434-188">例如，嘗試[使用 Azure AD 來保護 .NET Web API](active-directory-devquickstarts-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2b434-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
