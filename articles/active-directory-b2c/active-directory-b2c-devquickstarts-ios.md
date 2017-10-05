---
title: "使用 iOS 應用程式取得權杖 - Azure AD B2C | Microsoft Docs"
description: "本文將說明如何建立 iOS 應用程式，以使用 AppAuth 和 Azure Active Directory B2C 來管理使用者身分識別和驗證使用者。"
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
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="2884f-103">Azure AD B2C︰使用 iOS 應用程式登入</span><span class="sxs-lookup"><span data-stu-id="2884f-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="2884f-104">Microsoft 身分識別平台會使用開放式標準，例如 OAuth2 和 OpenID Connect。</span><span class="sxs-lookup"><span data-stu-id="2884f-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="2884f-105">使用開放式標準通訊協定讓開發人員在選取程式庫來與我們的服務整合時，有更多的選擇。</span><span class="sxs-lookup"><span data-stu-id="2884f-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="2884f-106">我們提供本逐步解說和其他類似的逐步解說，協助開發人員撰寫應用程式來連線至 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="2884f-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="2884f-107">大部分實作 [RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)的程式庫都能連線至 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="2884f-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="2884f-108">Microsoft 並不提供第三方程式庫的修正程式，也尚未審查這些程式庫。</span><span class="sxs-lookup"><span data-stu-id="2884f-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="2884f-109">此範例使用已藉由 Azure AD B2C 在基本案例中進行過相容性測試的第三方程式庫，稱為 AppAuth。</span><span class="sxs-lookup"><span data-stu-id="2884f-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="2884f-110">問題和功能要求應導向到程式庫的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="2884f-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="2884f-111">如需詳細資訊，請參閱 [本篇文章](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)。</span><span class="sxs-lookup"><span data-stu-id="2884f-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="2884f-112">如果您是 OAuth2 或 OpenID Connect 新手，此範例組態可能不太適合您。</span><span class="sxs-lookup"><span data-stu-id="2884f-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="2884f-113">建議您查看 [我們在此記載的通訊協定簡短概觀](active-directory-b2c-reference-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="2884f-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="2884f-114">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="2884f-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="2884f-115">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="2884f-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="2884f-116">目錄就是您所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="2884f-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="2884f-117">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="2884f-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="2884f-118">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="2884f-118">Create an application</span></span>
<span data-ttu-id="2884f-119">接著，您必須在 B2C 目錄中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="2884f-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="2884f-120">應用程式註冊會提供必要資訊給 Azure AD，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="2884f-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="2884f-121">如果要建立行動應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="2884f-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="2884f-122">請務必：</span><span class="sxs-lookup"><span data-stu-id="2884f-122">Be sure to:</span></span>

* <span data-ttu-id="2884f-123">在應用程式中加入**原生用戶端**。</span><span class="sxs-lookup"><span data-stu-id="2884f-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="2884f-124">複製指派給您的應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="2884f-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="2884f-125">您稍後需要此 GUID。</span><span class="sxs-lookup"><span data-stu-id="2884f-125">You need this GUID later.</span></span>
* <span data-ttu-id="2884f-126">使用自訂配置設定**重新導向 URI** (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)。</span><span class="sxs-lookup"><span data-stu-id="2884f-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="2884f-127">您稍後需要此 URI。</span><span class="sxs-lookup"><span data-stu-id="2884f-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="2884f-128">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="2884f-128">Create your policies</span></span>
<span data-ttu-id="2884f-129">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="2884f-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="2884f-130">此應用程式包含一個身分識別體驗：合併登入和註冊。</span><span class="sxs-lookup"><span data-stu-id="2884f-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="2884f-131">建立此原則，如[原則參考文章](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)所述。</span><span class="sxs-lookup"><span data-stu-id="2884f-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="2884f-132">建立此原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="2884f-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="2884f-133">在 [註冊屬性] 下方，選取 [顯示名稱] 屬性。</span><span class="sxs-lookup"><span data-stu-id="2884f-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="2884f-134">您也可以選取其他屬性。</span><span class="sxs-lookup"><span data-stu-id="2884f-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="2884f-135">在 [應用程式宣告] 下方，選取 [顯示名稱] 和 [使用者的物件識別碼] 宣告。</span><span class="sxs-lookup"><span data-stu-id="2884f-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="2884f-136">您也可以選取其他宣告。</span><span class="sxs-lookup"><span data-stu-id="2884f-136">You can select other claims as well.</span></span>
* <span data-ttu-id="2884f-137">在您建立每個原則之後，請複製原則的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="2884f-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="2884f-138">當您儲存原則時，原則名稱前面會加上 `b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="2884f-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="2884f-139">您稍後需要用到此原則名稱。</span><span class="sxs-lookup"><span data-stu-id="2884f-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="2884f-140">建立您的原則後，就可以開始建置您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2884f-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="2884f-141">下載範例程式碼</span><span class="sxs-lookup"><span data-stu-id="2884f-141">Download the sample code</span></span>
<span data-ttu-id="2884f-142">我們[在 GitHub 上](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)提供一個使用 AppAuth 和 Azure AD B2C 的操作範例。</span><span class="sxs-lookup"><span data-stu-id="2884f-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="2884f-143">您可以下載程式碼並執行。</span><span class="sxs-lookup"><span data-stu-id="2884f-143">You can download the code and run it.</span></span> <span data-ttu-id="2884f-144">若要使用自己的 Azure AD B2C 租用戶，請依照 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) 中的指示。</span><span class="sxs-lookup"><span data-stu-id="2884f-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="2884f-145">此範例由 [GitHub 上的 iOS AppAuth 專案](https://github.com/openid/AppAuth-iOS)依照 README 指示建立。</span><span class="sxs-lookup"><span data-stu-id="2884f-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="2884f-146">如需此範例和程式庫運作方式的詳細資訊，請參考 GitHub 上的 AppAuth README。</span><span class="sxs-lookup"><span data-stu-id="2884f-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="2884f-147">修改您的應用程式來使用 Azure AD B2C 和 AppAuth</span><span class="sxs-lookup"><span data-stu-id="2884f-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="2884f-148">AppAuth 支援 iOS 7 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="2884f-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="2884f-149">不過，若要在 Google 上支援社交登入，需要有 SFSafariViewController，而這需要 iOS 9 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2884f-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="2884f-150">組態</span><span class="sxs-lookup"><span data-stu-id="2884f-150">Configuration</span></span>

<span data-ttu-id="2884f-151">您可以指定授權端點和權杖端點 URI，以設定與 Azure AD B2C 通訊。</span><span class="sxs-lookup"><span data-stu-id="2884f-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="2884f-152">若要產生這些 URI，您需要下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="2884f-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="2884f-153">租用戶識別碼 (例如，contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="2884f-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="2884f-154">原則名稱 (例如，B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="2884f-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="2884f-155">取代下列 URL 中的 Tenant\_ID 和Policy\_Name，即可產生權杖端點 URI︰</span><span class="sxs-lookup"><span data-stu-id="2884f-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="2884f-156">取代下列 URL 中的 Tenant\_ID 和Policy\_Name，即可產生授權端點 URI︰</span><span class="sxs-lookup"><span data-stu-id="2884f-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="2884f-157">執行下列程式碼來建立 AuthorizationServiceConfiguration 物件︰</span><span class="sxs-lookup"><span data-stu-id="2884f-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="2884f-158">授權</span><span class="sxs-lookup"><span data-stu-id="2884f-158">Authorizing</span></span>

<span data-ttu-id="2884f-159">設定或擷取授權服務組態之後，就可以建構授權要求。</span><span class="sxs-lookup"><span data-stu-id="2884f-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="2884f-160">若要建立要求，您需要下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="2884f-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="2884f-161">用戶端識別碼 (例如，00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="2884f-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="2884f-162">使用自訂配置的重新導向 URI (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="2884f-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="2884f-163">這兩個項目應該已在您[註冊應用程式](#create-an-application)時儲存。</span><span class="sxs-lookup"><span data-stu-id="2884f-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="2884f-164">若要設定應用程式以處理使用自訂配置的 URI 重新導向，您需要更新 Info.pList 中的 [URL 配置] 清單︰</span><span class="sxs-lookup"><span data-stu-id="2884f-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="2884f-165">開啟 Info.pList。</span><span class="sxs-lookup"><span data-stu-id="2884f-165">Open Info.pList.</span></span>
* <span data-ttu-id="2884f-166">將滑鼠停留在像是 [套件組合 OS 類型代碼] 的資料列，然後按一下 \+ 符號。</span><span class="sxs-lookup"><span data-stu-id="2884f-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="2884f-167">重新命名新的資料列 [URL 類型]。</span><span class="sxs-lookup"><span data-stu-id="2884f-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="2884f-168">按一下 [URL 類型] 左邊的箭頭以開啟樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="2884f-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="2884f-169">按一下 [項目 0] 左邊的箭頭以開啟樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="2884f-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="2884f-170">將 [項目 0] 下方的第一個項目重新命名為 [URL 配置]。</span><span class="sxs-lookup"><span data-stu-id="2884f-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="2884f-171">按一下 [URL 配置] 左邊的箭頭以開啟樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="2884f-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="2884f-172">在 [值] 資料行中，[URL 配置] 下方的 [項目 0] 左邊有一個空白欄位。</span><span class="sxs-lookup"><span data-stu-id="2884f-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="2884f-173">將此值設為應用程式的唯一配置。</span><span class="sxs-lookup"><span data-stu-id="2884f-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="2884f-174">建立 OIDAuthorizationRequest 物件時，此值必須符合 redirectURL 中使用的配置。</span><span class="sxs-lookup"><span data-stu-id="2884f-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="2884f-175">在我們的範例中，我們使用配置 'com.onmicrosoft.fabrikamb2c.exampleapp'。</span><span class="sxs-lookup"><span data-stu-id="2884f-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="2884f-176">有關如何完成此程序的其餘部分，請參閱 [AppAuth 指南](https://openid.github.io/AppAuth-iOS/)。</span><span class="sxs-lookup"><span data-stu-id="2884f-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="2884f-177">如果您需要快速開始使用一個可操作的應用程式，請參閱[我們的範例](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)。</span><span class="sxs-lookup"><span data-stu-id="2884f-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="2884f-178">請依照 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) 中的步驟，輸入自己的 Azure AD B2C 組態。</span><span class="sxs-lookup"><span data-stu-id="2884f-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="2884f-179">我們歡迎意見反應和建議！</span><span class="sxs-lookup"><span data-stu-id="2884f-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="2884f-180">如果您無法完成此主題，或者有改進此內容的建議，非常歡迎您在頁面底部提供意見反應。</span><span class="sxs-lookup"><span data-stu-id="2884f-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="2884f-181">對於功能要求，請將它們新增到 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="2884f-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
