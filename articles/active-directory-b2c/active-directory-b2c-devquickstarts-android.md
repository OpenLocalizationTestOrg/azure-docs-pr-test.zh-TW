---
title: "Azure Active Directory B2C︰使用 Android 應用程式取得權杖 | Microsoft Docs"
description: "本文將說明如何建立 Android 應用程式，以使用 AppAuth 和 Azure Active Directory B2C 來管理使用者身分識別和驗證使用者。"
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="ff9c4-103">Azure AD B2C︰使用 Android 應用程式登入</span><span class="sxs-lookup"><span data-stu-id="ff9c4-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="ff9c4-104">Microsoft 身分識別平台會使用開放式標準，例如 OAuth2 和 OpenID Connect。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="ff9c4-105">這可讓開發人員運用他們想要與我們的服務整合的任何程式庫。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="ff9c4-106">為了協助開發人員使用我們的平台搭配其他程式庫，我們撰寫了幾個逐步解說，示範如何設定第三方程式庫以連線至 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="ff9c4-107">大部分實作 [RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749) 的程式庫都能連接到 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="ff9c4-108">Microsoft 並不提供第三方程式庫的修正程式，也尚未審查這些程式庫。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="ff9c4-109">此範例使用已藉由 Azure AD B2C 在基本案例中進行過相容性測試的第三方程式庫，稱為 AppAuth。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="ff9c4-110">問題和功能要求應導向到程式庫的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="ff9c4-111">如需詳細資訊，請參閱[這篇文章](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="ff9c4-112">如果您是 OAuth2 或 OpenID Connect 新手，此範例組態可能諸多不太適合您。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="ff9c4-113">建議您查看 [我們在此記載的通訊協定簡短概觀](active-directory-b2c-reference-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="ff9c4-114">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="ff9c4-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="ff9c4-115">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="ff9c4-116">目錄為所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="ff9c4-117">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="ff9c4-118">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="ff9c4-118">Create an application</span></span>

<span data-ttu-id="ff9c4-119">接著，您必須在 B2C 目錄中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="ff9c4-120">這會提供必要資訊給 Azure AD，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="ff9c4-121">如果要建立行動應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="ff9c4-122">請務必：</span><span class="sxs-lookup"><span data-stu-id="ff9c4-122">Be sure to:</span></span>

* <span data-ttu-id="ff9c4-123">在應用程式中加入**原生用戶端**。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="ff9c4-124">複製指派給您的應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="ff9c4-125">稍後您將會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-125">You will need this later.</span></span>
* <span data-ttu-id="ff9c4-126">設定原生用戶端**重新導向 URI** (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="ff9c4-127">稍後您也會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ff9c4-128">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="ff9c4-128">Create your policies</span></span>

<span data-ttu-id="ff9c4-129">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ff9c4-130">此應用程式包含一個身分識別體驗：合併登入和註冊。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="ff9c4-131">您必須建立此原則，如[原則參考文章](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)所述。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="ff9c4-132">建立此原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="ff9c4-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="ff9c4-133">在原則中選擇 [顯示名稱] 做為註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="ff9c4-134">在每個原則中，選擇 [顯示名稱] 和 [物件識別碼] 應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="ff9c4-135">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="ff9c4-136">在您建立每個原則之後，請複製原則的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="ff9c4-137">其前置詞應該為 `b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="ff9c4-138">您稍後需要用到此原則名稱。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ff9c4-139">建立您的原則後，就可以開始建置您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="ff9c4-140">下載範例程式碼</span><span class="sxs-lookup"><span data-stu-id="ff9c4-140">Download the sample code</span></span>

<span data-ttu-id="ff9c4-141">我們[在 GitHub 上](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)提供一個使用 AppAuth 和 Azure AD B2C 的操作範例。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="ff9c4-142">您可以下載程式碼並執行。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-142">You can download the code and run it.</span></span> <span data-ttu-id="ff9c4-143">您可以依照 [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) 中的指示，使用您自己的 Azure AD B2C 組態，快速開始使用您自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="ff9c4-144">這個範例修改自 [AppAuth](https://openid.github.io/AppAuth-Android/) 提供的範例。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="ff9c4-145">請瀏覽其頁面，以深入了解 AppAuth 和相關功能。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="ff9c4-146">修改您的應用程式來使用 Azure AD B2C 和 AppAuth</span><span class="sxs-lookup"><span data-stu-id="ff9c4-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="ff9c4-147">AppAuth 支援 Android API 16 (Jellybean) 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="ff9c4-148">我們建議使用 API 23 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="ff9c4-149">組態</span><span class="sxs-lookup"><span data-stu-id="ff9c4-149">Configuration</span></span>

<span data-ttu-id="ff9c4-150">您可以指定探索 URI，或指定授權端點和權杖端點 URI，以設定與 Azure AD B2C 通訊。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="ff9c4-151">不論何者，您都需要下列資訊：</span><span class="sxs-lookup"><span data-stu-id="ff9c4-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="ff9c4-152">租用戶識別碼 (例如，contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="ff9c4-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="ff9c4-153">原則名稱 (例如，B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="ff9c4-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="ff9c4-154">如果您選擇自動探索授權和權杖端點 URI，您必須從探索 URI 擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="ff9c4-155">取代下列 URL 中的 Tenant\_ID 和Policy\_Name，即可產生探索 URI︰</span><span class="sxs-lookup"><span data-stu-id="ff9c4-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="ff9c4-156">然後，您可以取得授權和權杖端點 URI，並執行下列命令來建立 AuthorizationServiceConfiguration 物件︰</span><span class="sxs-lookup"><span data-stu-id="ff9c4-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="ff9c4-157">除了使用探索來取得授權和權杖端點 URI，您也可以取代下列 URL 中的 Tenant\_ID 和 Policy\_Name，以明確指定它們︰</span><span class="sxs-lookup"><span data-stu-id="ff9c4-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="ff9c4-158">執行下列程式碼來建立 AuthorizationServiceConfiguration 物件︰</span><span class="sxs-lookup"><span data-stu-id="ff9c4-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="ff9c4-159">授權</span><span class="sxs-lookup"><span data-stu-id="ff9c4-159">Authorizing</span></span>

<span data-ttu-id="ff9c4-160">設定或擷取授權服務組態之後，就可以建構授權要求。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="ff9c4-161">若要建立要求，您需要下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="ff9c4-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="ff9c4-162">用戶端識別碼 (例如，00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="ff9c4-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="ff9c4-163">使用自訂配置的重新導向 URI (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="ff9c4-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="ff9c4-164">這兩個項目應該已在您[註冊應用程式](#create-an-application)時儲存。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="ff9c4-165">有關如何完成此程序的其餘部分，請參閱 [AppAuth 指南](https://openid.github.io/AppAuth-Android/)。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="ff9c4-166">如果您需要快速開始使用一個可操作的應用程式，請參閱[我們的範例](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="ff9c4-167">請依照 [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) 中的步驟，輸入自己的 Azure AD B2C 組態。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="ff9c4-168">我們歡迎意見反應和建議！</span><span class="sxs-lookup"><span data-stu-id="ff9c4-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="ff9c4-169">如果您無法完成此主題，或者有改進此內容的建議，非常歡迎您在頁面底部提供意見反應。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="ff9c4-170">對於功能要求，請將它們新增到 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="ff9c4-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

