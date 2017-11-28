---
title: "到 iOS 應用程式的 Azure AD aaaIntegrate |Microsoft 文件"
description: "如何 toobuild 與 Azure AD 進行登入並呼叫 Azure AD 整合的 iOS 應用程式會將使用 OAuth 保護應用程式開發介面。"
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
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="c678d-103">將 Azure AD 整合至 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="c678d-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="c678d-104">嘗試的新 hello 預覽[開發人員入口網站](https://identity.microsoft.com/Docs/iOS)，以協助您與 Azure Active Directory 取得啟動且正在執行，在短短幾分鐘內 ！</span><span class="sxs-lookup"><span data-stu-id="c678d-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="c678d-105">hello 開發人員入口網站會引導您完成註冊應用程式與 Azure AD 整合您的程式碼 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="c678d-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="c678d-106">當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。</span><span class="sxs-lookup"><span data-stu-id="c678d-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="c678d-107">Azure Active Directory (Azure AD) 提供 Active Directory 驗證程式庫或 ADAL，hello，iOS 用戶端需要 tooaccess 受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="c678d-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="c678d-108">ADAL 可簡化您的應用程式使用 tooobtain 的存取權杖的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="c678d-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="c678d-109">toodemonstrate 多麼容易的是，在這篇文章中我們建置目標 C 待辦事項清單應用程式，以：</span><span class="sxs-lookup"><span data-stu-id="c678d-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="c678d-110">取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c678d-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="c678d-111">在目錄中搜尋具有指定別名的使用者。</span><span class="sxs-lookup"><span data-stu-id="c678d-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="c678d-112">toobuild hello 完整運作應用程式，您需要：</span><span class="sxs-lookup"><span data-stu-id="c678d-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="c678d-113">向 Azure AD 註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c678d-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="c678d-114">安裝及設定 ADAL。</span><span class="sxs-lookup"><span data-stu-id="c678d-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="c678d-115">使用來自 Azure AD 的 ADAL tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c678d-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="c678d-116">啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="c678d-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="c678d-117">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c678d-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="c678d-118">如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="c678d-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="c678d-119">嘗試的新 hello 預覽[開發人員入口網站](https://identity.microsoft.com/Docs/iOS)，以協助您獲得 Azure AD 在短短幾分鐘內啟動且正在執行。</span><span class="sxs-lookup"><span data-stu-id="c678d-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="c678d-120">hello 開發人員入口網站會引導您完成註冊應用程式與 Azure AD 整合您的程式碼 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="c678d-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="c678d-121">當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。</span><span class="sxs-lookup"><span data-stu-id="c678d-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="c678d-122">1.決定您 iOS 的重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="c678d-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="c678d-123">toosecurely 啟動您的應用程式特定 SSO 案例中，您必須建立*重新導向 URI*以特定的格式。</span><span class="sxs-lookup"><span data-stu-id="c678d-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="c678d-124">重新導向 URI 是 hello 語彙基元傳回 toohello 正確的應用程式要求的它們的使用的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="c678d-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="c678d-125">hello iOS 格式重新導向 URI 是：</span><span class="sxs-lookup"><span data-stu-id="c678d-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="c678d-126">**aap-scheme** - 這已在您的 XCode 專案中註冊。</span><span class="sxs-lookup"><span data-stu-id="c678d-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="c678d-127">它是其他應用程式呼叫您的方式。</span><span class="sxs-lookup"><span data-stu-id="c678d-127">It is how other applications can call you.</span></span> <span data-ttu-id="c678d-128">您可以在 Info.plist -> URL types -> URL Identifier 下找到此項目。</span><span class="sxs-lookup"><span data-stu-id="c678d-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="c678d-129">如果您尚未設定任何一個，建議您建立一個。</span><span class="sxs-lookup"><span data-stu-id="c678d-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="c678d-130">**套件組合識別碼**-這是 「 識別 」 下找到的配套識別碼 hello 取消您的專案設定，在 XCode 中。</span><span class="sxs-lookup"><span data-stu-id="c678d-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="c678d-131">此 QuickStart 程式碼的範例：***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="c678d-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="c678d-132">2.註冊 hello DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="c678d-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="c678d-133">註冊您的應用程式 tooget 語彙基元 tooset，您必須先 tooregister 在您的 Azure AD 租用戶，並授與權限 tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="c678d-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="c678d-134">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c678d-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c678d-135">Hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c678d-135">On hello top bar, click your account.</span></span> <span data-ttu-id="c678d-136">在 hello**目錄**清單中，選擇您想要 tooregister hello Active Directory 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="c678d-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="c678d-137">按一下**更服務**在 hello 最左邊的瀏覽窗格中，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="c678d-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c678d-138">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c678d-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="c678d-139">請遵循 hello 提示新 toocreate**原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c678d-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="c678d-140">hello**名稱**hello 的應用程式描述您的應用程式 tooend 使用者。</span><span class="sxs-lookup"><span data-stu-id="c678d-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="c678d-141">hello**重新導向 Uri**是配置和字串的組合，Azure AD 使用 tooreturn 權杖回應。</span><span class="sxs-lookup"><span data-stu-id="c678d-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="c678d-142">輸入的值，是特定 tooyour 應用程式，而根據 hello 先前重新導向 URI 資訊。</span><span class="sxs-lookup"><span data-stu-id="c678d-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="c678d-143">Hello 註冊完成之後，Azure AD 會指派給您的應用程式是唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c678d-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="c678d-144">您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c678d-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="c678d-145">從 hello**設定**頁面上，選取**必要的使用權限**，然後選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="c678d-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="c678d-146">選取**Microsoft Graph**為 hello 應用程式開發介面，然後再加入 hello**讀取目錄資料**權限下的**委派的權限**。</span><span class="sxs-lookup"><span data-stu-id="c678d-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="c678d-147">這會設定使用者您應用程式 tooquery hello Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="c678d-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="c678d-148">3.安裝及設定 ADAL</span><span class="sxs-lookup"><span data-stu-id="c678d-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="c678d-149">既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。</span><span class="sxs-lookup"><span data-stu-id="c678d-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="c678d-150">您需要 tooprovide ADAL 與 Azure AD toocommunicate，它與您的應用程式註冊的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="c678d-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="c678d-151">開始使用 CocoaPods 加入 ADAL toohello DirectorySearcher 專案。</span><span class="sxs-lookup"><span data-stu-id="c678d-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="c678d-152">加入下列 toothis podfile hello:</span><span class="sxs-lookup"><span data-stu-id="c678d-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="c678d-153">現在使用 CocoaPods 載入 hello podfile。</span><span class="sxs-lookup"><span data-stu-id="c678d-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="c678d-154">此步驟會建立您會載入的新 XCode 工作區。</span><span class="sxs-lookup"><span data-stu-id="c678d-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="c678d-155">在 hello 快速入門專案，開啟 hello plist 檔案`settings.plist`。</span><span class="sxs-lookup"><span data-stu-id="c678d-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="c678d-156">Hello 中的項目 hello 區段 tooreflect hello 您輸入值 hello Azure 入口網站中的 hello 值取代。</span><span class="sxs-lookup"><span data-stu-id="c678d-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="c678d-157">每當您的程式碼使用 ADAL 時，都會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="c678d-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="c678d-158">hello`tenant`是 hello Azure AD 租用戶，例如 contoso.onmicrosoft.com 網域。</span><span class="sxs-lookup"><span data-stu-id="c678d-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="c678d-159">hello `clientId` hello 您複製從 hello 入口網站應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="c678d-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="c678d-160">hello`redirectUri`是您註冊 hello 入口網站中的 hello 重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="c678d-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="c678d-161">4.  使用 ADAL tooget 語彙基元從 Azure AD</span><span class="sxs-lookup"><span data-stu-id="c678d-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="c678d-162">hello ADAL 背後的基本原則是，只要您的應用程式需要存取權杖，它只會呼叫 completionBlock `+(void) getToken : `，ADAL 沒有 hello rest 和。</span><span class="sxs-lookup"><span data-stu-id="c678d-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="c678d-163">在 hello`QuickStart`專案中，開啟`GraphAPICaller.m`並找出 hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` hello 頂端附近的註解。</span><span class="sxs-lookup"><span data-stu-id="c678d-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="c678d-164">這是您傳遞透過 CompletionBlock 時，使用 Azure AD，toocommunicate ADAL hello 座標和告訴它如何 toocache 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c678d-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="c678d-165">現在我們需要 toouse 這個語彙基元 toosearch hello 圖形中的使用者。</span><span class="sxs-lookup"><span data-stu-id="c678d-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="c678d-166">尋找 hello`// TODO: implement SearchUsersList`註解。</span><span class="sxs-lookup"><span data-stu-id="c678d-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="c678d-167">這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello GET 要求 Azure AD Graph API toohello tooquery。</span><span class="sxs-lookup"><span data-stu-id="c678d-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="c678d-168">tooquery hello Azure AD Graph API，您需要在 hello access_token tooinclude `Authorization` hello 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="c678d-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="c678d-169">這就是 ADAL 的切入點。</span><span class="sxs-lookup"><span data-stu-id="c678d-169">This is where ADAL comes in.</span></span>

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

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
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


3. <span data-ttu-id="c678d-170">當您的應用程式藉由呼叫要求語彙基元`getToken(...)`，ADAL 會嘗試 tooreturn 語彙基元不要求 hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="c678d-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="c678d-171">ADAL 會判斷該 hello 使用者需要 toosign tooget 語彙基元中的，如果它會顯示登入 對話方塊、 收集 hello 使用者的認證，以及接著在成功驗證之後傳回語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c678d-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="c678d-172">如果 ADAL 不能 tooreturn 語彙基元因為任何原因，就會擲回`AdalException`。</span><span class="sxs-lookup"><span data-stu-id="c678d-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="c678d-173">hello`AuthenticationResult`物件包含`tokenCacheStoreItem`可以是您的應用程式可能需要使用的 toocollect hello 資訊的物件。</span><span class="sxs-lookup"><span data-stu-id="c678d-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="c678d-174">在 hello 快速入門，`tokenCacheStoreItem`如果驗證已完成，則使用的 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="c678d-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="c678d-175">5.建置並執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c678d-175">5. Build and run hello application</span></span>
<span data-ttu-id="c678d-176">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c678d-176">Congratulations!</span></span> <span data-ttu-id="c678d-177">現在您已經有可用的 iOS 應用程式，可以驗證使用者，安全地使用 OAuth 2.0 來呼叫 Web Api 取得 hello 使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="c678d-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="c678d-178">如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。</span><span class="sxs-lookup"><span data-stu-id="c678d-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="c678d-179">啟動 QuickStart 應用程式，然後使用其中一個使用者登入。</span><span class="sxs-lookup"><span data-stu-id="c678d-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="c678d-180">根據 UPN 搜尋其他使用者。</span><span class="sxs-lookup"><span data-stu-id="c678d-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="c678d-181">關閉 hello 應用程式，並重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="c678d-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="c678d-182">請注意 hello 使用者工作階段會保持不變。</span><span class="sxs-lookup"><span data-stu-id="c678d-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="c678d-183">ADAL 可讓您輕鬆 tooincorporate 所有這些常見的身分識別功能到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c678d-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="c678d-184">它會負責所有 hello dirty 工作，例如快取管理 OAuth 通訊協定支援，呈現給在中，UI toosign hello 使用者和重新整理過期的權杖。</span><span class="sxs-lookup"><span data-stu-id="c678d-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="c678d-185">您只需 tooknow 是單一的應用程式開發介面呼叫， `getToken`。</span><span class="sxs-lookup"><span data-stu-id="c678d-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="c678d-186">如需參考上, 提供 （不含您的組態值） 的 hello 完成範例[GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="c678d-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c678d-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c678d-187">Next steps</span></span>
<span data-ttu-id="c678d-188">您現在可以移動 tooadditional 案例。</span><span class="sxs-lookup"><span data-stu-id="c678d-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="c678d-189">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="c678d-189">You may want tootry:</span></span>

* [<span data-ttu-id="c678d-190">使用 Azure AD 保護 Node.js Web API</span><span class="sxs-lookup"><span data-stu-id="c678d-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="c678d-191">深入了解[如何 tooenable 跨應用程式使用 ADAL 的 iOS 上的 SSO](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="c678d-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

