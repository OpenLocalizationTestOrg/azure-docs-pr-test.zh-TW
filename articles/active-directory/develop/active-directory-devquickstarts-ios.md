---
title: "將 Azure AD 整合至 iOS 應用程式 | Microsoft Docs"
description: "如何建置 iOS 應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="1a1a0-103">將 Azure AD 整合至 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="1a1a0-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="1a1a0-104">試用新[開發人員入口網站](https://identity.microsoft.com/Docs/iOS) 的預覽版本，這可協助您在短短幾分鐘內啟動並執行 Azure Active Directory！</span><span class="sxs-lookup"><span data-stu-id="1a1a0-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="1a1a0-105">開發人員入口網站會引導您完成註冊應用程式並將 Azure AD 整合至您的程式碼的程序。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="1a1a0-106">當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="1a1a0-107">Azure Active Directory (Azure AD) 提供 Active Directory 驗證程式庫 (ADAL) 給需要存取受保護資源的 iOS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="1a1a0-108">ADAL 可簡化您的應用程式用來取得存取權杖的程序。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="1a1a0-109">為了示範究竟多麼簡單，我們會在本文中建置一個可執行下列動作的 Objective C 待辦事項清單應用程式：</span><span class="sxs-lookup"><span data-stu-id="1a1a0-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="1a1a0-110">使用 [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)來取得呼叫 Azure AD Graph API 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="1a1a0-111">在目錄中搜尋具有指定別名的使用者。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="1a1a0-112">若要建立可完整運作的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="1a1a0-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="1a1a0-113">向 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="1a1a0-114">安裝及設定 ADAL。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="1a1a0-115">使用 ADAL 來取得 Azure AD 的權杖。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="1a1a0-116">若要開始使用，請[下載應用程式基本架構](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip)或[下載完整的範例](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="1a1a0-117">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="1a1a0-118">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="1a1a0-119">試用新的[開發人員入口網站](https://identity.microsoft.com/Docs/iOS)預覽版本，這可協助您在短短幾分鐘內啟動並執行 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="1a1a0-120">開發人員入口網站會引導您完成註冊應用程式並將 Azure AD 整合至您的程式碼的程序。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="1a1a0-121">當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="1a1a0-122">1.決定您 iOS 的重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="1a1a0-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="1a1a0-123">為了安全地在特定 SSO 案例啟動您的應用程式，您必須以特定格式建立「重新導向 URI」。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="1a1a0-124">重新導向 URI 可確保應用程式要求的權杖會正確地傳回給它們。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="1a1a0-125">iOS 格式的重新導向 URI：</span><span class="sxs-lookup"><span data-stu-id="1a1a0-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="1a1a0-126">**aap-scheme** - 這已在您的 XCode 專案中註冊。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="1a1a0-127">它是其他應用程式呼叫您的方式。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-127">It is how other applications can call you.</span></span> <span data-ttu-id="1a1a0-128">您可以在 Info.plist -> URL types -> URL Identifier 下找到此項目。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="1a1a0-129">如果您尚未設定任何一個，建議您建立一個。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="1a1a0-130">**bundle-id** - 這是在您的 XCode 專案設定中，[identity] 下可找到的 [Bundle Identifier]。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="1a1a0-131">此 QuickStart 程式碼的範例：***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="1a1a0-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="1a1a0-132">2.註冊 DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="1a1a0-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="1a1a0-133">若要設定應用程式以取得權杖，您必須先在 Azure AD 租用戶中註冊該應用程式，然後授與它存取 Azure AD 圖形 API 的權限：</span><span class="sxs-lookup"><span data-stu-id="1a1a0-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="1a1a0-134">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1a1a0-135">在頂端列中，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-135">On the top bar, click your account.</span></span> <span data-ttu-id="1a1a0-136">在 [目錄] 清單下，選擇您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="1a1a0-137">按一下最左邊瀏覽窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="1a1a0-138">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="1a1a0-139">請遵照提示建立新的 [原生用戶端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="1a1a0-140">應用程式的 [名稱] 對使用者說明您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="1a1a0-141">[重新導向 URI] 是配置與字串的組合，Azure AD 會用它來傳回權杖回應。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="1a1a0-142">根據上面的重新導向 URI 資訊，輸入您的應用程式特有的值。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="1a1a0-143">完成註冊之後，Azure AD 會為應用程式指派一個唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="1a1a0-144">您會在後續小節中用到這個值，所以請從應用程式索引標籤中複製此值。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="1a1a0-145">從 [設定] 頁面中，選取 [必要權限]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="1a1a0-146">選取 [Microsoft Graph] 作為 API，然後在 [委派權限] 底下新增 [讀取目錄資料] 權限。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="1a1a0-147">這會設定您的應用程式以查詢 Azure AD 圖形 API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="1a1a0-148">3.安裝及設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="1a1a0-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="1a1a0-149">既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="1a1a0-150">為了讓 ADAL 能與 Azure AD 通訊，您需要提供一些應用程式註冊的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="1a1a0-151">請從使用 Cocoapods 將 ADAL 新增至 DirectorySearcher 專案開始。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="1a1a0-152">將下列加入此 Podfile：</span><span class="sxs-lookup"><span data-stu-id="1a1a0-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="1a1a0-153">現在使用 CocoaPods 來載入該 Podfile。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="1a1a0-154">此步驟會建立您會載入的新 XCode 工作區。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="1a1a0-155">在 QuickStart 專案中，開啟 plist 檔案 `settings.plist`。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="1a1a0-156">取代區段中的元素值，以反映您在 Azure 入口網站中輸入的值。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="1a1a0-157">每當您的程式碼使用 ADAL 時，都會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="1a1a0-158">`tenant` 是指您的 Azure AD 租用戶網域，例如 contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="1a1a0-159">`clientId` 是您從入口網站複製的應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="1a1a0-160">`redirectUri` 是您在入口網站中註冊的重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="1a1a0-161">4.  使用 ADAL 從 Azure AD 取得權杖</span><span class="sxs-lookup"><span data-stu-id="1a1a0-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="1a1a0-162">ADAL 的基本原則是每當您的應用程式需要存取權杖時，它只需呼叫 completionBlock `+(void) getToken : `，ADAL 就會進行其餘工作。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="1a1a0-163">在 `QuickStart` 專案中，開啟 `GraphAPICaller.m` 並找出接近頂端的 `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` 註解。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="1a1a0-164">您在這裡將 ADAL 與 Azure AD 通訊透過 CompletionBlock 將座標傳給 ADAL，並告訴它如何快取權杖。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="1a1a0-165">現在我們需要使用此權杖搜尋圖形中的使用者。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="1a1a0-166">尋找 `// TODO: implement SearchUsersList` 註解。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="1a1a0-167">這個方法會對 Azure AD Graph API 提出 GET 要求，以查詢 UPN 開頭為指定搜尋詞彙的使用者。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="1a1a0-168">若要查詢 Azure AD 圖形 API，您必須在要求的 `Authorization` 標頭中包含 access_token。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="1a1a0-169">這就是 ADAL 的切入點。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

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
         }];

    }

    ```


3. <span data-ttu-id="1a1a0-170">當應用程式透過呼叫 `getToken(...)` 來要求權杖時，ADAL 會嘗試在不向使用者要求認證的情況下傳回權杖。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="1a1a0-171">如果 ADAL 決定使用者需要登入才能取得權杖，它會顯示可供登入的對話方塊、收集使用者的認證，然後在成功驗證後傳回權杖。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="1a1a0-172">如果 ADAL 基於任何原因無法傳回權杖，則會擲回 `AdalException`。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="1a1a0-173">`AuthenticationResult` 物件包含 `tokenCacheStoreItem` 物件，可用來收集您的應用程式可能需要的資訊。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="1a1a0-174">在 QuickStart 中，`tokenCacheStoreItem` 用來判斷驗證是否已經完成。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="1a1a0-175">5.建置並執行應用程式</span><span class="sxs-lookup"><span data-stu-id="1a1a0-175">5. Build and run the application</span></span>
<span data-ttu-id="1a1a0-176">恭喜！</span><span class="sxs-lookup"><span data-stu-id="1a1a0-176">Congratulations!</span></span> <span data-ttu-id="1a1a0-177">您現在有一個運作中的 iOS 應用程式，可以驗證使用者、使用 OAuth 2.0 安全地呼叫 Web API，以及取得使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="1a1a0-178">如果您還沒有這麼做，現在是將一些使用者植入租用戶的時候。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="1a1a0-179">啟動 QuickStart 應用程式，然後使用其中一個使用者登入。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="1a1a0-180">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="1a1a0-181">關閉應用程式，然後重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="1a1a0-182">請注意，使用者工作階段會維持不變。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="1a1a0-183">ADAL 可讓您輕鬆地將這些常見的身分識別功能全部納入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="1a1a0-184">它會為您處理所有麻煩的工作，包括快取管理、OAuth 通訊協定支援、向使用者顯示 UI 以便登入，以及重新整理過期權杖。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="1a1a0-185">您唯一需要知道的就是單一 API 呼叫， `getToken`。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="1a1a0-186">[GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip) 提供完成的範例供您參考 (不含您的設定值)。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1a1a0-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a1a0-187">Next steps</span></span>
<span data-ttu-id="1a1a0-188">您現在可以繼續探索其他案例。</span><span class="sxs-lookup"><span data-stu-id="1a1a0-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="1a1a0-189">您可以嘗試：</span><span class="sxs-lookup"><span data-stu-id="1a1a0-189">You may want to try:</span></span>

* [<span data-ttu-id="1a1a0-190">使用 Azure AD 保護 Node.js Web API</span><span class="sxs-lookup"><span data-stu-id="1a1a0-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="1a1a0-191">了解[如何使用 ADAL 在 iOS 上啟用跨應用程式的 SSO](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="1a1a0-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

