---
title: "Azure Active Directory B2C︰使用 Android 應用程式取得權杖 | Microsoft Docs"
description: "這篇文章將示範如何 toocreate AppAuth 使用 Azure Active Directory B2C toomanage 使用者身分識別和驗證使用者的 Android 應用程式。"
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
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="44647-103">Azure AD B2C︰使用 Android 應用程式登入</span><span class="sxs-lookup"><span data-stu-id="44647-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="44647-104">hello Microsoft 識別身分平台中使用 OAuth2 和 OpenID Connect 等的開放標準。</span><span class="sxs-lookup"><span data-stu-id="44647-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="44647-105">這可讓開發人員 tooleverage 他們希望 toointegrate 與我們的服務的任何文件庫。</span><span class="sxs-lookup"><span data-stu-id="44647-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="44647-106">tooaid 使用我們的平台與其他程式庫開發人員，我們已經撰寫這個一個 toodemonstrate 像幾個逐步解說如何 tooconfigure 第 3 個合作對象文件庫 tooconnect toohello Microsoft 識別平台。</span><span class="sxs-lookup"><span data-stu-id="44647-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="44647-107">實作的大部分程式庫[hello RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)將會無法 tooconnect toohello Microsoft 識別身分平台。</span><span class="sxs-lookup"><span data-stu-id="44647-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="44647-108">Microsoft 並不提供第三方程式庫的修正程式，也尚未審查這些程式庫。</span><span class="sxs-lookup"><span data-stu-id="44647-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="44647-109">這個範例會使用稱為基本案例中的相容性，以 hello Azure AD B2C AppAuth 已測試的第 3 個合作對象程式庫。</span><span class="sxs-lookup"><span data-stu-id="44647-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="44647-110">問題和功能要求應該導向的 toohello 程式庫的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="44647-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="44647-111">如需詳細資訊，請參閱[這篇文章](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)。</span><span class="sxs-lookup"><span data-stu-id="44647-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="44647-112">如果您是新 tooOAuth2 或 OpenID Connect 此範例組態中的許多可能不會更有意義 tooyou。</span><span class="sxs-lookup"><span data-stu-id="44647-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="44647-113">我們建議您查看簡短[我們已記載的 hello 通訊協定概觀](active-directory-b2c-reference-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="44647-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="44647-114">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="44647-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="44647-115">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="44647-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="44647-116">目錄為所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="44647-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="44647-117">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="44647-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="44647-118">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="44647-118">Create an application</span></span>

<span data-ttu-id="44647-119">接下來，您需要 toocreate 應用程式中 B2C 目錄。</span><span class="sxs-lookup"><span data-stu-id="44647-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="44647-120">提供 Azure AD 需要 toocommunicate 安全地與您的應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="44647-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="44647-121">toocreate 行動裝置應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="44647-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="44647-122">請務必：</span><span class="sxs-lookup"><span data-stu-id="44647-122">Be sure to:</span></span>

* <span data-ttu-id="44647-123">包含**原生用戶端**hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="44647-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="44647-124">複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="44647-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="44647-125">稍後您將會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="44647-125">You will need this later.</span></span>
* <span data-ttu-id="44647-126">設定原生用戶端**重新導向 URI** (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)。</span><span class="sxs-lookup"><span data-stu-id="44647-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="44647-127">稍後您也會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="44647-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="44647-128">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="44647-128">Create your policies</span></span>

<span data-ttu-id="44647-129">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="44647-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="44647-130">此應用程式包含一個身分識別體驗：合併登入和註冊。</span><span class="sxs-lookup"><span data-stu-id="44647-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="44647-131">您將 toocreate 需要這項原則，如中所述[原則參考文件](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)。</span><span class="sxs-lookup"><span data-stu-id="44647-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="44647-132">當您建立 hello 原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="44647-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="44647-133">選擇 hello**顯示名稱**做為註冊的屬性，在您的原則。</span><span class="sxs-lookup"><span data-stu-id="44647-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="44647-134">選擇 hello**顯示名稱**和**物件識別碼**中每個原則的應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="44647-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="44647-135">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="44647-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="44647-136">複製 hello**名稱**的每個原則建立之後。</span><span class="sxs-lookup"><span data-stu-id="44647-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="44647-137">就不應有 hello 前置詞`b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="44647-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="44647-138">稍後您將需要 hello 原則名稱。</span><span class="sxs-lookup"><span data-stu-id="44647-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="44647-139">您已建立您的原則之後，您便準備好 toobuild 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="44647-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="44647-140">下載 hello 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="44647-140">Download hello sample code</span></span>

<span data-ttu-id="44647-141">我們[在 GitHub 上](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)提供一個使用 AppAuth 和 Azure AD B2C 的操作範例。</span><span class="sxs-lookup"><span data-stu-id="44647-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="44647-142">您可以下載 hello 程式碼，並執行它。</span><span class="sxs-lookup"><span data-stu-id="44647-142">You can download hello code and run it.</span></span> <span data-ttu-id="44647-143">您可以快速地開始使用您自己的應用程式使用您自己的 Azure AD B2C 組態 hello 中的 hello 指示[README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="44647-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="44647-144">hello 範例是修改所提供的 hello 範例[AppAuth](https://openid.github.io/AppAuth-Android/)。</span><span class="sxs-lookup"><span data-stu-id="44647-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="44647-145">請瀏覽其頁面 toolearn 更多關於 AppAuth 和它的功能。</span><span class="sxs-lookup"><span data-stu-id="44647-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="44647-146">修改您應用程式 toouse Azure AD B2C AppAuth 與</span><span class="sxs-lookup"><span data-stu-id="44647-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="44647-147">AppAuth 支援 Android API 16 (Jellybean) 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="44647-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="44647-148">我們建議使用 API 23 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="44647-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="44647-149">組態</span><span class="sxs-lookup"><span data-stu-id="44647-149">Configuration</span></span>

<span data-ttu-id="44647-150">藉由其中一個指定的 hello 探索 URI 或藉由指定 hello 授權端點和權杖的端點 Uri，您可以設定與 Azure AD B2C 通訊。</span><span class="sxs-lookup"><span data-stu-id="44647-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="44647-151">在任一情況下，您需要下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="44647-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="44647-152">租用戶識別碼 (例如，contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="44647-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="44647-153">原則名稱 (例如，B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="44647-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="44647-154">如果您選擇 tooautomatically 探索 hello 授權和語彙基元端點 Uri，您必須從 hello 探索 URI toofetch 資訊。</span><span class="sxs-lookup"><span data-stu-id="44647-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="44647-155">URI 可以由取代 hello 租用戶產生的 hello 探索\_識別碼和 hello 原則\_hello 下列 URL 中的名稱：</span><span class="sxs-lookup"><span data-stu-id="44647-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="44647-156">然後，您可以取得 hello 授權和語彙基元端點 Uri，並執行 hello 下列建立 AuthorizationServiceConfiguration 物件：</span><span class="sxs-lookup"><span data-stu-id="44647-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

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
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="44647-157">不使用探索 tooobtain hello 授權和語彙基元端點 Uri 時，您也可以指定它們明確取代 hello 租用戶\_識別碼和 hello 原則\_下列 hello URL 名稱：</span><span class="sxs-lookup"><span data-stu-id="44647-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="44647-158">執行下列程式碼 toocreate hello AuthorizationServiceConfiguration 物件：</span><span class="sxs-lookup"><span data-stu-id="44647-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="44647-159">授權</span><span class="sxs-lookup"><span data-stu-id="44647-159">Authorizing</span></span>

<span data-ttu-id="44647-160">設定或擷取授權服務組態之後，就可以建構授權要求。</span><span class="sxs-lookup"><span data-stu-id="44647-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="44647-161">toocreate hello 要求，您將需要下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="44647-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="44647-162">用戶端識別碼 (例如，00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="44647-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="44647-163">使用自訂配置的重新導向 URI (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="44647-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="44647-164">這兩個項目應該已在您[註冊應用程式](#create-an-application)時儲存。</span><span class="sxs-lookup"><span data-stu-id="44647-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="44647-165">請參閱 toohello [AppAuth 指南](https://openid.github.io/AppAuth-Android/)上 toocomplete hello hello 程序的其餘部分的方式。</span><span class="sxs-lookup"><span data-stu-id="44647-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="44647-166">如果您需要 tooquickly 開始使用工作應用程式，請簽出[我們的範例](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)。</span><span class="sxs-lookup"><span data-stu-id="44647-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="44647-167">Hello 中的 hello 步驟[README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter 您自己的 Azure AD B2C 組態。</span><span class="sxs-lookup"><span data-stu-id="44647-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="44647-168">我們一定是開啟 toofeedback，以及建議 ！</span><span class="sxs-lookup"><span data-stu-id="44647-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="44647-169">如果您有本主題中，任何問題，或有改善此內容的建議，我們非常感謝您在 hello hello 頁面底部的意見反應。</span><span class="sxs-lookup"><span data-stu-id="44647-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="44647-170">功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="44647-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

