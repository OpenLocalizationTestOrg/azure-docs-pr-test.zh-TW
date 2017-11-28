---
title: "使用 iOS 應用程式取得權杖 - Azure AD B2C | Microsoft Docs"
description: "這篇文章將示範如何 toocreate AppAuth 使用 Azure Active Directory B2C toomanage 使用者身分識別和驗證使用者的 iOS 應用程式。"
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="f01f1-103">Azure AD B2C︰使用 iOS 應用程式登入</span><span class="sxs-lookup"><span data-stu-id="f01f1-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="f01f1-104">hello Microsoft 識別身分平台中使用 OAuth2 和 OpenID Connect 等的開放標準。</span><span class="sxs-lookup"><span data-stu-id="f01f1-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="f01f1-105">使用開放標準的通訊協定提供開發人員選項，選取 與我們的服務程式庫 toointegrate 時。</span><span class="sxs-lookup"><span data-stu-id="f01f1-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="f01f1-106">我們提供了本逐步解說，以及其他類似 tooaid 開發人員撰寫連接 toohello Microsoft 身分識別平台的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f01f1-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="f01f1-107">實作的大部分程式庫[hello RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)無法 tooconnect toohello Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="f01f1-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="f01f1-108">Microsoft 並不提供第三方程式庫的修正程式，也尚未審查這些程式庫。</span><span class="sxs-lookup"><span data-stu-id="f01f1-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="f01f1-109">這個範例會使用稱為 AppAuth 已測試的基本案例中以 hello Azure AD B2C 的相容性的協力廠商程式庫。</span><span class="sxs-lookup"><span data-stu-id="f01f1-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="f01f1-110">問題和功能要求應該導向的 toohello 程式庫的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="f01f1-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="f01f1-111">如需詳細資訊，請參閱 [本篇文章](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="f01f1-112">如果您是新 tooOAuth2 或 OpenID Connect，此範例組態中的許多可能不會更有意義 tooyou。</span><span class="sxs-lookup"><span data-stu-id="f01f1-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="f01f1-113">我們建議您查看簡短[我們已記載的 hello 通訊協定概觀](active-directory-b2c-reference-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="f01f1-114">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="f01f1-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="f01f1-115">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="f01f1-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="f01f1-116">目錄就是您所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="f01f1-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="f01f1-117">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="f01f1-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="f01f1-118">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="f01f1-118">Create an application</span></span>
<span data-ttu-id="f01f1-119">接下來，您需要 toocreate 應用程式中 B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="f01f1-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="f01f1-120">hello 應用程式註冊可讓 Azure AD 需要 toocommunicate 安全地與您的應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="f01f1-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="f01f1-121">toocreate 行動裝置應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f01f1-122">請務必：</span><span class="sxs-lookup"><span data-stu-id="f01f1-122">Be sure to:</span></span>

* <span data-ttu-id="f01f1-123">包含**原生用戶端**hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f01f1-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="f01f1-124">複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f01f1-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="f01f1-125">您稍後需要此 GUID。</span><span class="sxs-lookup"><span data-stu-id="f01f1-125">You need this GUID later.</span></span>
* <span data-ttu-id="f01f1-126">使用自訂配置設定**重新導向 URI** (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="f01f1-127">您稍後需要此 URI。</span><span class="sxs-lookup"><span data-stu-id="f01f1-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f01f1-128">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="f01f1-128">Create your policies</span></span>
<span data-ttu-id="f01f1-129">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="f01f1-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f01f1-130">此應用程式包含一個身分識別體驗：合併登入和註冊。</span><span class="sxs-lookup"><span data-stu-id="f01f1-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="f01f1-131">建立此原則，如[原則參考文章](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)所述。</span><span class="sxs-lookup"><span data-stu-id="f01f1-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="f01f1-132">當您建立 hello 原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="f01f1-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="f01f1-133">在下**註冊屬性**，選取 hello 屬性**顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="f01f1-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="f01f1-134">您也可以選取其他屬性。</span><span class="sxs-lookup"><span data-stu-id="f01f1-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="f01f1-135">在下**應用程式宣告**，選取 hello 宣告**顯示名稱**和**使用者的物件識別碼**。</span><span class="sxs-lookup"><span data-stu-id="f01f1-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="f01f1-136">您也可以選取其他宣告。</span><span class="sxs-lookup"><span data-stu-id="f01f1-136">You can select other claims as well.</span></span>
* <span data-ttu-id="f01f1-137">複製 hello**名稱**的每個原則建立之後。</span><span class="sxs-lookup"><span data-stu-id="f01f1-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="f01f1-138">原則名稱前面會加上`b2c_1_`當您儲存 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="f01f1-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="f01f1-139">您稍後需要 hello 原則名稱。</span><span class="sxs-lookup"><span data-stu-id="f01f1-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f01f1-140">您已建立您的原則之後，您便準備好 toobuild 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f01f1-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="f01f1-141">下載 hello 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="f01f1-141">Download hello sample code</span></span>
<span data-ttu-id="f01f1-142">我們[在 GitHub 上](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)提供一個使用 AppAuth 和 Azure AD B2C 的操作範例。</span><span class="sxs-lookup"><span data-stu-id="f01f1-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="f01f1-143">您可以下載 hello 程式碼，並執行它。</span><span class="sxs-lookup"><span data-stu-id="f01f1-143">You can download hello code and run it.</span></span> <span data-ttu-id="f01f1-144">toouse 您自己的 Azure AD B2C 租用戶，遵循 hello hello 指示[README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="f01f1-145">此範例建立遵照 hello 讀我檔案由 hello [GitHub 上的 iOS AppAuth 專案](https://github.com/openid/AppAuth-iOS)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="f01f1-146">如需有關 hello 範例與 hello 程式庫的運作方式的詳細資訊，參考 hello AppAuth GitHub 上的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="f01f1-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="f01f1-147">修改您應用程式 toouse Azure AD B2C AppAuth 與</span><span class="sxs-lookup"><span data-stu-id="f01f1-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="f01f1-148">AppAuth 支援 iOS 7 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="f01f1-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="f01f1-149">不過，toosupport 社交登入 Google，SFSafariViewController 上的需要這需要 iOS 9 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f01f1-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="f01f1-150">組態</span><span class="sxs-lookup"><span data-stu-id="f01f1-150">Configuration</span></span>

<span data-ttu-id="f01f1-151">您可以設定與 Azure AD B2C 通訊，藉由指定 hello 授權端點和權杖的端點 Uri。</span><span class="sxs-lookup"><span data-stu-id="f01f1-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="f01f1-152">toogenerate 這些 Uri，您需要下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="f01f1-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="f01f1-153">租用戶識別碼 (例如，contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="f01f1-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="f01f1-154">原則名稱 (例如，B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="f01f1-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="f01f1-155">hello URI 可以由取代產生的權杖端點 hello 租用戶\_識別碼和 hello 原則\_hello 下列 URL 中的名稱：</span><span class="sxs-lookup"><span data-stu-id="f01f1-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="f01f1-156">hello URI 可以由取代產生的授權端點 hello 租用戶\_識別碼和 hello 原則\_hello 下列 URL 中的名稱：</span><span class="sxs-lookup"><span data-stu-id="f01f1-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="f01f1-157">執行下列程式碼 toocreate hello AuthorizationServiceConfiguration 物件：</span><span class="sxs-lookup"><span data-stu-id="f01f1-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="f01f1-158">授權</span><span class="sxs-lookup"><span data-stu-id="f01f1-158">Authorizing</span></span>

<span data-ttu-id="f01f1-159">設定或擷取授權服務組態之後，就可以建構授權要求。</span><span class="sxs-lookup"><span data-stu-id="f01f1-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="f01f1-160">toocreate hello 要求，您需要下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="f01f1-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="f01f1-161">用戶端識別碼 (例如，00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="f01f1-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="f01f1-162">使用自訂配置的重新導向 URI (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="f01f1-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="f01f1-163">這兩個項目應該已在您[註冊應用程式](#create-an-application)時儲存。</span><span class="sxs-lookup"><span data-stu-id="f01f1-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="f01f1-164">tooset 註冊您的應用程式 toohandle hello 重新導向 toohello URI 與 hello 自訂配置，您會需要 'URL 配置' tooupdate hello 清單程式 Info.pList 中：</span><span class="sxs-lookup"><span data-stu-id="f01f1-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="f01f1-165">開啟 Info.pList。</span><span class="sxs-lookup"><span data-stu-id="f01f1-165">Open Info.pList.</span></span>
* <span data-ttu-id="f01f1-166">將滑鼠停留在像是 '配套 OS 類型程式碼' 的資料列，然後按一下 hello\+符號。</span><span class="sxs-lookup"><span data-stu-id="f01f1-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="f01f1-167">重新命名 hello 新資料列 'URL 的類型'。</span><span class="sxs-lookup"><span data-stu-id="f01f1-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="f01f1-168">按一下 hello 箭號 toohello 左邊的 URL 類型' tooopen hello 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="f01f1-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="f01f1-169">按一下 hello 箭號 toohello 左 '項目 0' tooopen hello 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="f01f1-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="f01f1-170">重新命名項目 0 too'URL 配置底下的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="f01f1-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="f01f1-171">按一下 hello 箭號 toohello 左邊的樹狀目錄中 tooopen hello ' 的 URL 結構描述 '。</span><span class="sxs-lookup"><span data-stu-id="f01f1-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="f01f1-172">在 hello 'Value' 資料行，沒有空白欄位 toohello 左邊 '的 URL 結構描述' 之下的 ' 項目 0'。</span><span class="sxs-lookup"><span data-stu-id="f01f1-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="f01f1-173">設定 hello 值 tooyour 應用程式的唯一配置。</span><span class="sxs-lookup"><span data-stu-id="f01f1-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="f01f1-174">hello 值必須符合建立 hello OIDAuthorizationRequest 物件時用於 redirectURL hello 配置。</span><span class="sxs-lookup"><span data-stu-id="f01f1-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="f01f1-175">在我們的範例中，我們使用 hello 配置 'com.onmicrosoft.fabrikamb2c.exampleapp'。</span><span class="sxs-lookup"><span data-stu-id="f01f1-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="f01f1-176">請參閱 toohello [AppAuth 指南](https://openid.github.io/AppAuth-iOS/)上 toocomplete hello hello 程序的其餘部分的方式。</span><span class="sxs-lookup"><span data-stu-id="f01f1-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="f01f1-177">如果您需要 tooquickly 開始使用工作應用程式，請簽出[我們的範例](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="f01f1-178">Hello 中的 hello 步驟[README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter 您自己的 Azure AD B2C 組態。</span><span class="sxs-lookup"><span data-stu-id="f01f1-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="f01f1-179">我們一定是開啟 toofeedback，以及建議 ！</span><span class="sxs-lookup"><span data-stu-id="f01f1-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="f01f1-180">如果您有本主題中，任何問題，或有改善此內容的建議，我們非常感謝您在 hello hello 頁面底部的意見反應。</span><span class="sxs-lookup"><span data-stu-id="f01f1-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="f01f1-181">功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="f01f1-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
