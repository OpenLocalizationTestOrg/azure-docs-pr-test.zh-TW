---
title: "aaaAzure Active Directory v2.0 Android 應用程式 |Microsoft 文件"
description: "如何 toobuild Android 應用程式登入使用者使用個人 Microsoft 帳戶和工作或學校帳戶和呼叫 hello Graph API 透過協力廠商文件庫。"
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="90966-103">新增登入 tooan Android 應用程式使用 Graph API 使用 hello v2.0 端點使用協力廠商程式庫</span><span class="sxs-lookup"><span data-stu-id="90966-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="90966-104">hello Microsoft 識別身分平台中使用 OAuth2 和 OpenID Connect 等的開放標準。</span><span class="sxs-lookup"><span data-stu-id="90966-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="90966-105">開發人員可以使用任何文件庫，他們想 toointegrate 與我們的服務。</span><span class="sxs-lookup"><span data-stu-id="90966-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="90966-106">toohelp 開發人員會使用我們的平台與其他程式庫，我們已經撰寫這個一個 toodemonstrate 像幾個逐步解說如何 tooconfigure 協力廠商程式庫 tooconnect toohello Microsoft 識別平台。</span><span class="sxs-lookup"><span data-stu-id="90966-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="90966-107">實作的大部分程式庫[hello RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)可以連接 toohello Microsoft 識別平台。</span><span class="sxs-lookup"><span data-stu-id="90966-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="90966-108">這個逐步解說會建立 hello 應用程式，使用者可以登入 tootheir 組織，然後搜尋自行在組織中使用 hello Graph API。</span><span class="sxs-lookup"><span data-stu-id="90966-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="90966-109">如果您是新 tooOAuth2 或 OpenID Connect，此範例組態中的許多可能不會有意義 tooyou。</span><span class="sxs-lookup"><span data-stu-id="90966-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="90966-110">建議您閱讀 [2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)以瞭解背景。</span><span class="sxs-lookup"><span data-stu-id="90966-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="90966-111">平台的 hello OAuth2 或 OpenID Connect 標準，例如條件式存取和 Intune 原則管理 中的運算式具有某些功能需要您 toouse 我們的開放原始碼 Microsoft Azure 身分識別的程式庫。</span><span class="sxs-lookup"><span data-stu-id="90966-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="90966-112">hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。</span><span class="sxs-lookup"><span data-stu-id="90966-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="90966-113">toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="90966-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="90966-114">從 GitHub 下載 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="90966-114">Download hello code from GitHub</span></span>
<span data-ttu-id="90966-115">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2)。</span><span class="sxs-lookup"><span data-stu-id="90966-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="90966-116">您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip)或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="90966-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="90966-117">您也可以下載 hello 範例，並立即開始：</span><span class="sxs-lookup"><span data-stu-id="90966-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="90966-118">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="90966-118">Register an app</span></span>
<span data-ttu-id="90966-119">建立新的應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或遵循 hello 詳細的步驟，網址[如何 tooregister 應用程式，但 hello v2.0 端點](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="90966-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="90966-120">請確定：</span><span class="sxs-lookup"><span data-stu-id="90966-120">Make sure to:</span></span>

* <span data-ttu-id="90966-121">複製 hello**應用程式識別碼**這是指派的 tooyour 應用程式因為很快就需要它。</span><span class="sxs-lookup"><span data-stu-id="90966-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="90966-122">新增 hello**行動**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="90966-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="90966-123">注意： hello 應用程式註冊入口網站提供**重新導向 URI**值。</span><span class="sxs-lookup"><span data-stu-id="90966-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="90966-124">不過，在此範例中必須使用 hello 預設值為`https://login.microsoftonline.com/common/oauth2/nativeclient`。</span><span class="sxs-lookup"><span data-stu-id="90966-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="90966-125">下載 hello NXOAuth2 協力廠商程式庫，並建立工作區</span><span class="sxs-lookup"><span data-stu-id="90966-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="90966-126">這個逐步解說中，您將使用 hello OIDCAndroidLib 從 GitHub，是根據 hello Google 的 OpenID Connect 的程式碼的 OAuth2 程式庫。</span><span class="sxs-lookup"><span data-stu-id="90966-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="90966-127">它會實作 hello 原生應用程式設定檔，並支援 hello 的 hello 使用者的授權端點。</span><span class="sxs-lookup"><span data-stu-id="90966-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="90966-128">這些是您將需要 toointegrate hello Microsoft 身分識別平台的所有 hello 項目時。</span><span class="sxs-lookup"><span data-stu-id="90966-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="90966-129">複製 hello OIDCAndroidLib 儲存機制 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="90966-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="90966-131">設定您的 Android Studio 環境</span><span class="sxs-lookup"><span data-stu-id="90966-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="90966-132">建立新的 Android Studio 專案，並接受 hello hello 精靈中的預設值。</span><span class="sxs-lookup"><span data-stu-id="90966-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![在 Android Studio 中建立新專案](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![目標 Android 裝置](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![加入活動 toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="90966-136">tooset 您專案的模組，向上移動 hello 複製儲存機制 toohello 專案位置。</span><span class="sxs-lookup"><span data-stu-id="90966-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="90966-137">您可以也建立 hello 專案與然後複製它直接 toohello 專案位置。</span><span class="sxs-lookup"><span data-stu-id="90966-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![專案模組](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="90966-139">使用 [hello] 內容功能表或使用 hello Ctrl + Alt + Maj + S 捷徑，請開啟 hello 專案模組設定。</span><span class="sxs-lookup"><span data-stu-id="90966-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![專案模組設定](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="90966-141">移除 hello 預設應用程式的模組，因為您只想 hello 專案容器設定。</span><span class="sxs-lookup"><span data-stu-id="90966-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![hello 預設應用程式的模組](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="90966-143">匯入模組，從 hello 複製儲存機制 toohello 目前專案。</span><span class="sxs-lookup"><span data-stu-id="90966-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="90966-144">![匯入 gradle 專案](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG)![建立新的模組網頁](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="90966-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="90966-145">重複上述步驟 hello`oidlib-sample`模組。</span><span class="sxs-lookup"><span data-stu-id="90966-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="90966-146">檢查 hello oidclib 相依性 hello`oidlib-sample`模組。</span><span class="sxs-lookup"><span data-stu-id="90966-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![oidclib hello oidlib 範例模組上的相依性](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="90966-148">按一下 [確定]  並等候 gradle 同步處理。</span><span class="sxs-lookup"><span data-stu-id="90966-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="90966-149">您的 settings.gradle 應如下所示：</span><span class="sxs-lookup"><span data-stu-id="90966-149">Your settings.gradle should look like:</span></span>
   
    ![settings.gradle 的螢幕擷取畫面](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="90966-151">建置 hello 範例應用程式 toomake 確定正確地執行該 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="90966-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="90966-152">您將不會無法 toouse 這與 Azure Active Directory 尚未。</span><span class="sxs-lookup"><span data-stu-id="90966-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="90966-153">我們需要 tooconfigure 部份端點第一次。</span><span class="sxs-lookup"><span data-stu-id="90966-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="90966-154">這是 tooensure 我們開始自訂 hello 範例應用程式之前，您不需要 Android Studio 問題。</span><span class="sxs-lookup"><span data-stu-id="90966-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="90966-155">建置並執行`oidlib-sample`做為在 Android Studio 中的 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="90966-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![oidlib-sample 建置進度](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="90966-157">刪除 hello`app `時您 hello 模組從專案中移除 hello 因為 Android Studio 安全性並不會刪除它所保留的目錄。</span><span class="sxs-lookup"><span data-stu-id="90966-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![包含 hello 應用程式目錄的檔案結構](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="90966-159">開啟 hello**編輯組態**hello 模組從 hello 專案中移除時，也左功能表 tooremove hello 執行設定。</span><span class="sxs-lookup"><span data-stu-id="90966-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="90966-160">![編輯設定功能表](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![執行應用程式設定](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="90966-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="90966-161">設定 hello 端點的 hello 範例</span><span class="sxs-lookup"><span data-stu-id="90966-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="90966-162">既然您已擁有 hello`oidlib-sample`成功執行，讓編輯某些端點 tooget 這個與 Azure Active Directory 的工作。</span><span class="sxs-lookup"><span data-stu-id="90966-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="90966-163">設定您的用戶端藉由編輯 hello oidc_clientconf.xml 檔案</span><span class="sxs-lookup"><span data-stu-id="90966-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="90966-164">因為您正在使用 OAuth2 流程只有 tooget 語彙基元，並呼叫 hello Graph API，設定 hello 用戶端 toodo OAuth2 只。</span><span class="sxs-lookup"><span data-stu-id="90966-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="90966-165">後面的範例中會示範 OIDC。</span><span class="sxs-lookup"><span data-stu-id="90966-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="90966-166">設定您所收到 hello 註冊入口網站的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="90966-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="90966-167">下列設定以其中一個 hello 您重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="90966-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="90966-168">設定您的範圍，您需要在順序 tooaccess hello Graph API。</span><span class="sxs-lookup"><span data-stu-id="90966-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="90966-169">hello`User.Read`值`oidc_scopes`可讓您 tooread hello 基本設定檔 hello 登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="90966-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="90966-170">您可以進一步了解在的 hello 可用範圍[Microsoft Graph 權限範圍](https://graph.microsoft.io/docs/authorization/permission_scopes)。</span><span class="sxs-lookup"><span data-stu-id="90966-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="90966-171">如果您想要 OpenID Connect 中有關 `openid` 或 `offline_access` 範圍的說明，請參閱 [2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)。</span><span class="sxs-lookup"><span data-stu-id="90966-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="90966-172">編輯 hello oidc_endpoints.xml 檔案設定用戶端端點</span><span class="sxs-lookup"><span data-stu-id="90966-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="90966-173">開啟 hello`oidc_endpoints.xml`檔案並製作 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="90966-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="90966-174">如果您使用 OAuth2 做為通訊協定，則不得變更這些端點。</span><span class="sxs-lookup"><span data-stu-id="90966-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="90966-175">hello 端點`userInfoEndpoint`和`revocationEndpoint`目前不支援 Azure Active directory。</span><span class="sxs-lookup"><span data-stu-id="90966-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="90966-176">如果您離開的 hello 預設 example.com 值，則您會收到它們都不在 hello 範例:-)</span><span class="sxs-lookup"><span data-stu-id="90966-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="90966-177">設定圖形 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="90966-177">Configure a Graph API call</span></span>
* <span data-ttu-id="90966-178">開啟 hello`HomeActivity.java`檔案並製作 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="90966-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="90966-179">以下的簡單圖形 API 呼叫會傳回我們的資訊。</span><span class="sxs-lookup"><span data-stu-id="90966-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="90966-180">這些是您需要 toodo 所有 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="90966-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="90966-181">執行 hello`oidlib-sample`應用程式，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="90966-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="90966-182">您已成功通過驗證之後，請選取 hello**要求受保護資源**按鈕 tootest 您呼叫 toohello Graph API。</span><span class="sxs-lookup"><span data-stu-id="90966-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="90966-183">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="90966-183">Get security updates for our product</span></span>
<span data-ttu-id="90966-184">建議您 tooget 安全性事件通知所造訪 hello[資訊安全技術中心](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。</span><span class="sxs-lookup"><span data-stu-id="90966-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

