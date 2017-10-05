---
title: "使用 Azure AD v2.0 端點將登入新增至 iOS 應用程式 | Microsoft Docs"
description: "如何建置可使用個人 Microsoft 帳戶及公司或學校帳戶登入使用者的 iOS 應用程式 (採用協力廠商程式庫)。"
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="49b34-103">使用 v2.0 端點，透過圖形 API 將登入新增至使用協力廠商程式庫的 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="49b34-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="49b34-104">Microsoft 身分識別平台會使用開放式標準，例如 OAuth2 和 OpenID Connect。</span><span class="sxs-lookup"><span data-stu-id="49b34-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="49b34-105">開發人員可以使用任何想要的程式庫，來與我們的服務整合。</span><span class="sxs-lookup"><span data-stu-id="49b34-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="49b34-106">為了協助開發人員使用我們的平台搭配其他程式庫，我們撰寫了數篇逐步解說，示範如何設定協力廠商程式庫以連接到 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="49b34-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="49b34-107">大部分實作 [RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749) 的程式庫都能連接到 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="49b34-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="49b34-108">使用此篇逐步解說建立的應用程式，使用者可以使用圖形 API 來登入其組織，然後在組織中搜尋其他人。</span><span class="sxs-lookup"><span data-stu-id="49b34-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="49b34-109">如果您是 OAuth2 或 OpenID Connect 新手，此範例組態可能不太適合您。</span><span class="sxs-lookup"><span data-stu-id="49b34-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="49b34-110">建議您閱讀 [v2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)以瞭解背景。</span><span class="sxs-lookup"><span data-stu-id="49b34-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="49b34-111">我們的平台中有些功能沒有採用 OAuth2 或 OpenID Connect 標準的運算式 (例如條件式存取和 Intune 原則管理)，所以會要求您使用開放原始碼 Microsoft Azure 身分識別程式庫。</span><span class="sxs-lookup"><span data-stu-id="49b34-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="49b34-112">v2.0 端點並未支援所有的 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="49b34-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="49b34-113">若要判斷是否應該使用 v2.0 端點，請閱讀相關的 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="49b34-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="49b34-114">從 GitHub 下載程式碼</span><span class="sxs-lookup"><span data-stu-id="49b34-114">Download code from GitHub</span></span>
<span data-ttu-id="49b34-115">本教學課程的程式碼保留在 [GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2)。</span><span class="sxs-lookup"><span data-stu-id="49b34-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="49b34-116">若要遵循執行，您可以 [用 .zip 格式下載應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ，或複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="49b34-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="49b34-117">您也可以下載範例，並立即開始著手使用︰</span><span class="sxs-lookup"><span data-stu-id="49b34-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="49b34-118">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="49b34-118">Register an app</span></span>
<span data-ttu-id="49b34-119">在[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)建立新的應用程式，或遵循[如何註冊應用程式與 v2.0 端點](active-directory-v2-app-registration.md)的詳細步驟進行。</span><span class="sxs-lookup"><span data-stu-id="49b34-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="49b34-120">請確定：</span><span class="sxs-lookup"><span data-stu-id="49b34-120">Make sure to:</span></span>

* <span data-ttu-id="49b34-121">複製所指派給您的「應用程式識別碼」  ，因為您很快就會用到。</span><span class="sxs-lookup"><span data-stu-id="49b34-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="49b34-122">為您的應用程式新增 **行動** 平台。</span><span class="sxs-lookup"><span data-stu-id="49b34-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="49b34-123">複製入口網站的「重新導向 URI」  。</span><span class="sxs-lookup"><span data-stu-id="49b34-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="49b34-124">您必須使用 `urn:ietf:wg:oauth:2.0:oob`的預設值。</span><span class="sxs-lookup"><span data-stu-id="49b34-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="49b34-125">下載 NXOAuth2 協力廠商程式庫並建立工作區</span><span class="sxs-lookup"><span data-stu-id="49b34-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="49b34-126">在此逐步解說中，您將使用 GitHub 提供的 OAuth2Client，這是適用於 Mac OS X 與 iOS 的 OAuth2 程式庫 (Cocoa 與 Cocoa Touch)。</span><span class="sxs-lookup"><span data-stu-id="49b34-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="49b34-127">此程式庫是以 OAuth2 規格的第 10 版草稿為基礎。</span><span class="sxs-lookup"><span data-stu-id="49b34-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="49b34-128">它會實作原生應用程式設定檔，並支援使用者的授權端點。</span><span class="sxs-lookup"><span data-stu-id="49b34-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="49b34-129">您需要上述各項，才能與 Microsoft 身分識別平台整合。</span><span class="sxs-lookup"><span data-stu-id="49b34-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="49b34-130">使用 CocoaPods 將程式庫加入您的專案</span><span class="sxs-lookup"><span data-stu-id="49b34-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="49b34-131">CocoaPods 是 Xcode 專案的相依性管理員。</span><span class="sxs-lookup"><span data-stu-id="49b34-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="49b34-132">它會自動管理上述安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="49b34-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="49b34-133">將下列加入此 Podfile：</span><span class="sxs-lookup"><span data-stu-id="49b34-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="49b34-134">使用 CocoaPods 來載入該 Podfile。</span><span class="sxs-lookup"><span data-stu-id="49b34-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="49b34-135">這會建立您將載入的新 XCode Workspace。</span><span class="sxs-lookup"><span data-stu-id="49b34-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="49b34-136">探索專案結構</span><span class="sxs-lookup"><span data-stu-id="49b34-136">Explore the structure of the project</span></span>
<span data-ttu-id="49b34-137">在基本架構中為專案設定下列結構︰</span><span class="sxs-lookup"><span data-stu-id="49b34-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="49b34-138">具有 UPN 搜尋功能的「主要檢視」</span><span class="sxs-lookup"><span data-stu-id="49b34-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="49b34-139">所選使用者的相關資料的「詳細資料檢視」</span><span class="sxs-lookup"><span data-stu-id="49b34-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="49b34-140">使用者可登入應用程式來查詢圖形的「登入檢視」</span><span class="sxs-lookup"><span data-stu-id="49b34-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="49b34-141">我們會移至基本架構中各種不同的檔案，以加入驗證。</span><span class="sxs-lookup"><span data-stu-id="49b34-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="49b34-142">程式碼的其他部分 (如視覺化程式碼) 與身分識別無關，所以不會提供給您。</span><span class="sxs-lookup"><span data-stu-id="49b34-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="49b34-143">在程式庫中設定 settings.plst 檔案</span><span class="sxs-lookup"><span data-stu-id="49b34-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="49b34-144">在 QuickStart 專案中，開啟 `settings.plist` 檔案。</span><span class="sxs-lookup"><span data-stu-id="49b34-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="49b34-145">取代區段中的元素值，以反映您在 Azure 入口網站中所使用的值。</span><span class="sxs-lookup"><span data-stu-id="49b34-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="49b34-146">每當使用 Active Directory 驗證程式庫時，您的程式碼就會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="49b34-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="49b34-147">`clientId` 是您從入口網站複製的應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="49b34-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="49b34-148">`redirectUri` 是入口網站所提供的重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="49b34-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="49b34-149">在 LoginViewController 中設定 NXOAuth2Client 程式庫</span><span class="sxs-lookup"><span data-stu-id="49b34-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="49b34-150">NXOAuth2Client 程式庫要求設定一些值。</span><span class="sxs-lookup"><span data-stu-id="49b34-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="49b34-151">完成這項工作之後，您可以使用取得的權杖以呼叫圖形 API。</span><span class="sxs-lookup"><span data-stu-id="49b34-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="49b34-152">因為每當需要驗證時都會呼叫 `LoginView` ，所以合理的做法是將組態值放入該檔案中。</span><span class="sxs-lookup"><span data-stu-id="49b34-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="49b34-153">讓我們在 `LoginViewController.m` 檔案中新增一些值，以便針對驗證和授權來設定內容。</span><span class="sxs-lookup"><span data-stu-id="49b34-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="49b34-154">和放在程式碼後面的值有關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="49b34-154">Details about the values follow the code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="49b34-155">讓我們看看程式碼的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="49b34-155">Let's look at details about the code.</span></span>

<span data-ttu-id="49b34-156">第一個字串是用於 `scopes`。</span><span class="sxs-lookup"><span data-stu-id="49b34-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="49b34-157">`User.Read` 值可讓您讀取已登入使用者的基本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49b34-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="49b34-158">您可以在 [Microsoft Graph 權限範圍](https://graph.microsoft.io/docs/authorization/permission_scopes)，深入了解所有可用範圍。</span><span class="sxs-lookup"><span data-stu-id="49b34-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="49b34-159">對於 `authURL`、`loginURL`、`bhh` 及 `tokenURL`，您應該使用上面提供的值。</span><span class="sxs-lookup"><span data-stu-id="49b34-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="49b34-160">如果您使用開放原始碼 Microsoft Azure 身分識別程式庫，我們會使用中繼資料端點為您提取此資料。</span><span class="sxs-lookup"><span data-stu-id="49b34-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="49b34-161">我們已努力完成為您擷取這些值的工作。</span><span class="sxs-lookup"><span data-stu-id="49b34-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="49b34-162">`keychain` 值是一個容器，NXOAuth2Client 程式庫將用來建立金鑰鏈來儲存您的權杖。</span><span class="sxs-lookup"><span data-stu-id="49b34-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="49b34-163">如果您想要取得跨多個應用程式的單一登入 (SSO)，可以在每個應用程式中指定相同的金鑰鏈，以及要求在您的 XCode 權利中使用該金鑰鏈。</span><span class="sxs-lookup"><span data-stu-id="49b34-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="49b34-164">這會在 Apple 文件中說明。</span><span class="sxs-lookup"><span data-stu-id="49b34-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="49b34-165">這些值的其餘部分都必須使用此程式庫，並且為您建立位置，即可將這些值送至內容。</span><span class="sxs-lookup"><span data-stu-id="49b34-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="49b34-166">建立 URL 快取</span><span class="sxs-lookup"><span data-stu-id="49b34-166">Create a URL cache</span></span>
<span data-ttu-id="49b34-167">在載入檢視之後，一律會呼叫 `(void)viewDidLoad()`，其內部的下列程式碼會裝填快取以供我們使用。</span><span class="sxs-lookup"><span data-stu-id="49b34-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="49b34-168">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="49b34-168">Add the following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="49b34-169">建立用於登入的 Web 檢視</span><span class="sxs-lookup"><span data-stu-id="49b34-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="49b34-170">Web 檢視可提示使用者提供其他因素 (例如已設定的簡訊) 或將錯誤訊息傳回給使用者。</span><span class="sxs-lookup"><span data-stu-id="49b34-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="49b34-171">您將在此處設定 Web 檢視，然後撰寫程式碼，以從身分識別服務處理將會在 Web 檢視中發生的回呼。</span><span class="sxs-lookup"><span data-stu-id="49b34-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="49b34-172">覆寫 Web 檢視方法來處理驗證</span><span class="sxs-lookup"><span data-stu-id="49b34-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="49b34-173">如先前所述，當使用者需要登入時，若要告訴 Web 檢視發生什麼情況，您可以將下列程式碼貼上。</span><span class="sxs-lookup"><span data-stu-id="49b34-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="49b34-174">撰寫程式碼來處理 OAuth2 要求的結果</span><span class="sxs-lookup"><span data-stu-id="49b34-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="49b34-175">下列程式碼會處理從 Web 檢視傳回的 redirectURL。</span><span class="sxs-lookup"><span data-stu-id="49b34-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="49b34-176">如果驗證未成功，此程式碼將會再試一次。</span><span class="sxs-lookup"><span data-stu-id="49b34-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="49b34-177">同時，程式庫會提供錯誤，讓您可在主控台中查看或以非同步方式處理。</span><span class="sxs-lookup"><span data-stu-id="49b34-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="49b34-178">設定 OAuth 內容 (稱為「帳戶存放區」)</span><span class="sxs-lookup"><span data-stu-id="49b34-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="49b34-179">您可以針對您想要從應用程式存取的每個服務，在共用帳戶存放區上呼叫 `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` 。</span><span class="sxs-lookup"><span data-stu-id="49b34-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="49b34-180">帳戶類型是字串，其可做為特定服務的識別碼。</span><span class="sxs-lookup"><span data-stu-id="49b34-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="49b34-181">因為您要存取圖形 API，所以程式碼會將其視為 `"myGraphService"`。</span><span class="sxs-lookup"><span data-stu-id="49b34-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="49b34-182">接著，您要設定觀察者，以在權杖發生任何變更時告訴您。</span><span class="sxs-lookup"><span data-stu-id="49b34-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="49b34-183">在您取得權杖之後，可讓使用者回到 `masterView`。</span><span class="sxs-lookup"><span data-stu-id="49b34-183">After you get the token, you return the user back to the `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="49b34-184">設定 MasterView 以從圖形 API 搜尋和顯示使用者</span><span class="sxs-lookup"><span data-stu-id="49b34-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="49b34-185">在方格中顯示所傳回資料的 Master-View-Controller (MVC) 應用程式出本逐步解說的範圍，而且有許多說明如何建置的線上教學課程。</span><span class="sxs-lookup"><span data-stu-id="49b34-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="49b34-186">此程式碼全都在基本架構檔案中。</span><span class="sxs-lookup"><span data-stu-id="49b34-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="49b34-187">不過，您必須在此 MVC 應用程式中處理一些事項︰</span><span class="sxs-lookup"><span data-stu-id="49b34-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="49b34-188">當使用者在搜尋欄位中輸入資料時進行攔截</span><span class="sxs-lookup"><span data-stu-id="49b34-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="49b34-189">將資料的物件提供給 MasterView，以便在格線中顯示結果</span><span class="sxs-lookup"><span data-stu-id="49b34-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="49b34-190">我們會在下方進行這些動作。</span><span class="sxs-lookup"><span data-stu-id="49b34-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="49b34-191">加入檢查以查看您是否已經登入</span><span class="sxs-lookup"><span data-stu-id="49b34-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="49b34-192">如果使用者未登入，應用程式沒什麼作為，所以檢查快取中是否已有權杖會是明智之舉。</span><span class="sxs-lookup"><span data-stu-id="49b34-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="49b34-193">如果沒有，您可重新導向至 LoginView 以讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="49b34-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="49b34-194">如果您還記得，在檢視載入時執行動作的最佳方式，就是使用 Apple 提供的 `viewDidLoad()` 方法。</span><span class="sxs-lookup"><span data-stu-id="49b34-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="49b34-195">在收到資料時更新資料表檢視</span><span class="sxs-lookup"><span data-stu-id="49b34-195">Update the Table View when data is received</span></span>
<span data-ttu-id="49b34-196">當圖形 API 傳回資料時，您必須顯示該資料。</span><span class="sxs-lookup"><span data-stu-id="49b34-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="49b34-197">為了簡單起見，以下是可更新資料表的全部程式碼。</span><span class="sxs-lookup"><span data-stu-id="49b34-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="49b34-198">您可以直接在 MVC 未定案程式碼中貼上正確的值。</span><span class="sxs-lookup"><span data-stu-id="49b34-198">You can just paste the right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="49b34-199">提供有人在搜尋欄位中輸入資料時呼叫圖形 API 的方法</span><span class="sxs-lookup"><span data-stu-id="49b34-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="49b34-200">使用者在方塊中輸入搜尋資料時，您需要將該資料塞到圖形 API。</span><span class="sxs-lookup"><span data-stu-id="49b34-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="49b34-201">您將在下列程式碼建置的 `GraphAPICaller` 類別，會將查閱功能從展示當中分離出來。</span><span class="sxs-lookup"><span data-stu-id="49b34-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="49b34-202">現在，讓我們撰寫會將任何搜尋字元送入圖形 API 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="49b34-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="49b34-203">我們的做法是提供稱為 `lookupInGraph`的方法，其採用我們想要搜尋的字串。</span><span class="sxs-lookup"><span data-stu-id="49b34-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="49b34-204">撰寫協助程式類別以存取圖形 API</span><span class="sxs-lookup"><span data-stu-id="49b34-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="49b34-205">這是我們應用程式的核心。</span><span class="sxs-lookup"><span data-stu-id="49b34-205">This is the core of our application.</span></span> <span data-ttu-id="49b34-206">而其餘就是將程式碼插入 Apple 提供的預設 MVC 模式，您在這裡撰寫的程式碼會在使用者輸入時查詢圖形，然後傳回該資料時。</span><span class="sxs-lookup"><span data-stu-id="49b34-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="49b34-207">程式碼如下所示，而後面還有其詳細說明。</span><span class="sxs-lookup"><span data-stu-id="49b34-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="49b34-208">建立新的 Objective C 標頭檔</span><span class="sxs-lookup"><span data-stu-id="49b34-208">Create a new Objective C header file</span></span>
<span data-ttu-id="49b34-209">將檔案命名為 `GraphAPICaller.h`，然後新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="49b34-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="49b34-210">如您所見，指定的方法會取得字串並傳回 completionBlock。</span><span class="sxs-lookup"><span data-stu-id="49b34-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="49b34-211">此 completionBlock (如您所猜測) 提供的物件會隨著使用者搜尋，即時填入資料，藉此更新資料表。</span><span class="sxs-lookup"><span data-stu-id="49b34-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="49b34-212">建立新的 Objective C 檔案</span><span class="sxs-lookup"><span data-stu-id="49b34-212">Create a new Objective C file</span></span>
<span data-ttu-id="49b34-213">將檔案命名為 `GraphAPICaller.m`，然後新增下列方法。</span><span class="sxs-lookup"><span data-stu-id="49b34-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="49b34-214">我們會詳細解說這個方法。</span><span class="sxs-lookup"><span data-stu-id="49b34-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="49b34-215">此程式碼的核心在於 `NXOAuth2Request`，該方法會採用您已經在 settings.plist 檔案中定義的參數。</span><span class="sxs-lookup"><span data-stu-id="49b34-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="49b34-216">第一個步驟是建構正確的圖形 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="49b34-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="49b34-217">因為您正在呼叫 `/users`，所以您會將它附加到圖形 API 資源和版本來進行指定。</span><span class="sxs-lookup"><span data-stu-id="49b34-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="49b34-218">因為這些都會隨著 API 演進而改變，所以合理的做法是將這些放在外部設定檔案。</span><span class="sxs-lookup"><span data-stu-id="49b34-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="49b34-219">接下來，您需要指定您也會提供給圖形 API 呼叫的參數。</span><span class="sxs-lookup"><span data-stu-id="49b34-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="49b34-220">切記  不要將參數放在資源端點中，因為它會在執行階段針對所有非 URI 符合字元而虛設。</span><span class="sxs-lookup"><span data-stu-id="49b34-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="49b34-221">必須在參數中提供所有的查詢程式碼。</span><span class="sxs-lookup"><span data-stu-id="49b34-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="49b34-222">您可能發現這會呼叫您尚未撰寫的 `convertParamsToDictionary` 方法。</span><span class="sxs-lookup"><span data-stu-id="49b34-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="49b34-223">讓我們立即在檔案的結尾這樣做︰</span><span class="sxs-lookup"><span data-stu-id="49b34-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="49b34-224">接下來，我們將使用 `NXOAuth2Request` 方法，以從 API 取回 JSON 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="49b34-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="49b34-225">最後，來看看您要如何將資料傳回至 MasterViewController。</span><span class="sxs-lookup"><span data-stu-id="49b34-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="49b34-226">資料會以序列化方式傳回，而且該資料必須還原序列化並載入 MainViewController 可取用的物件。</span><span class="sxs-lookup"><span data-stu-id="49b34-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="49b34-227">基於此目的，基本架構具有的 `User.m/h` 檔案可以建立使用者物件。</span><span class="sxs-lookup"><span data-stu-id="49b34-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="49b34-228">您會以圖形中的資訊填入該使用者物件。</span><span class="sxs-lookup"><span data-stu-id="49b34-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-the-sample"></a><span data-ttu-id="49b34-229">執行範例</span><span class="sxs-lookup"><span data-stu-id="49b34-229">Run the sample</span></span>
<span data-ttu-id="49b34-230">如果您使用基本架構或遵循本逐步解說，則您的應用程式現在應會執行。</span><span class="sxs-lookup"><span data-stu-id="49b34-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="49b34-231">啟動模擬器，然後按一下 [登入]  以使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="49b34-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="49b34-232">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="49b34-232">Get security updates for our product</span></span>
<span data-ttu-id="49b34-233">我們鼓勵您造訪 [安全性 TechCenter](https://technet.microsoft.com/security/dd252948) 並訂閱資訊安全摘要報告警示，以在安全性事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="49b34-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

