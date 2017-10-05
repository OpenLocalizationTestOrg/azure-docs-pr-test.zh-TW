---
title: "Azure Active Directory v2.0 Android 應用程式 | Microsoft Docs"
description: "如何建置可使用個人 Microsoft 帳戶及公司或學校帳戶登入使用者，並使用協力廠商程式庫呼叫圖形 API 的 Android 應用程式。"
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="ba5bc-103">使用 v2.0 端點透過圖形 API 將登入新增至使用協力廠商程式庫的 Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="ba5bc-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="ba5bc-104">Microsoft 身分識別平台會使用開放式標準，例如 OAuth2 和 OpenID Connect。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="ba5bc-105">開發人員可以使用任何想要的程式庫，來與我們的服務整合。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="ba5bc-106">為了協助開發人員使用我們的平台搭配其他程式庫，我們撰寫了數篇逐步解說，示範如何設定協力廠商程式庫以連接到 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="ba5bc-107">大部分實作 [RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749) 的程式庫都能連接到 Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="ba5bc-108">使用此篇逐步解說建立的應用程式，使用者可以使用圖形 API 來登入其組織，然後在組織中搜尋自己。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="ba5bc-109">如果您是 OAuth2 或 OpenID Connect 新手，此範例組態可能不太適合您。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="ba5bc-110">建議您閱讀 [2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)以瞭解背景。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="ba5bc-111">我們的平台中有些功能沒有採用 OAuth2 或 OpenID Connect 標準的運算式 (例如條件式存取和 Intune 原則管理)，所以會要求您使用開放原始碼 Microsoft Azure 身分識別程式庫。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="ba5bc-112">v2.0 端點並未支援所有的 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="ba5bc-113">若要判斷是否應該使用 v2.0 端點，請閱讀相關的 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="ba5bc-114">從 GitHub 下載程式碼</span><span class="sxs-lookup"><span data-stu-id="ba5bc-114">Download the code from GitHub</span></span>
<span data-ttu-id="ba5bc-115">本教學課程的程式碼保留在 [GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2)。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="ba5bc-116">若要遵循執行，您可以[用 .zip 格式下載應用程式的基本架構](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip)，或複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="ba5bc-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="ba5bc-117">您也可以下載範例，並立即開始著手使用︰</span><span class="sxs-lookup"><span data-stu-id="ba5bc-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="ba5bc-118">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="ba5bc-118">Register an app</span></span>
<span data-ttu-id="ba5bc-119">在[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)建立新的應用程式，或遵循[如何註冊應用程式與 v2.0 端點](active-directory-v2-app-registration.md)的詳細步驟進行。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="ba5bc-120">請確定：</span><span class="sxs-lookup"><span data-stu-id="ba5bc-120">Make sure to:</span></span>

* <span data-ttu-id="ba5bc-121">複製所指派給您的「應用程式識別碼」  ，因為您很快就會用到。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="ba5bc-122">為您的應用程式新增 **行動** 平台。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="ba5bc-123">注意︰應用程式註冊入口網站會提供 [重新導向 URI]  值。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="ba5bc-124">不過，在此範例中，您必須使用 `https://login.microsoftonline.com/common/oauth2/nativeclient`的預設值。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="ba5bc-125">下載 NXOAuth2 協力廠商程式庫並建立工作區</span><span class="sxs-lookup"><span data-stu-id="ba5bc-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="ba5bc-126">在此逐步解說中，您將使用 GitHub 中的 OIDCAndroidLib，這個以 Google 的 OpenID Connect 程式碼為基礎的 OAuth2 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="ba5bc-127">它會實作原生應用程式設定檔，並支援使用者的授權端點。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="ba5bc-128">您需要上述各項，才能與 Microsoft 身分識別平台整合。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="ba5bc-129">將 OIDCAndroidLib 儲存機制複製到您的電腦。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="ba5bc-131">設定您的 Android Studio 環境</span><span class="sxs-lookup"><span data-stu-id="ba5bc-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="ba5bc-132">建立新的 Android Studio 專案，並接受精靈中的預設值。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![在 Android Studio 中建立新專案](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![目標 Android 裝置](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![將活動加入行動裝置](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="ba5bc-136">若要設定您的專案模組，請將複製的儲存機制移至專案位置。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="ba5bc-137">您也可以先建立專案，然後將專案直接複製到專案位置。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![專案模組](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="ba5bc-139">使用內容功能表，或使用 Ctrl+Alt+Maj+S 快速鍵，來開啟專案模組設定。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![專案模組設定](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="ba5bc-141">因為您只想要專案容器設定，所以請移除預設的應用程式模組。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![預設應用程式模組](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="ba5bc-143">從複製的儲存機制將模組匯入目前的專案。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="ba5bc-144">![匯入 gradle 專案](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG)![建立新的模組網頁](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="ba5bc-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="ba5bc-145">對 `oidlib-sample` 模組重複執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="ba5bc-146">檢查 `oidlib-sample` 模組上的 oidclib 相依性。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![oidlib-sample 模組的 oidclib 相依性](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="ba5bc-148">按一下 [確定]  並等候 gradle 同步處理。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="ba5bc-149">您的 settings.gradle 應如下所示：</span><span class="sxs-lookup"><span data-stu-id="ba5bc-149">Your settings.gradle should look like:</span></span>
   
    ![settings.gradle 的螢幕擷取畫面](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="ba5bc-151">建置範例應用程式，確定此範例可正確運作。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="ba5bc-152">您尚未能夠將此範例使用於 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="ba5bc-153">我們需要先設定一些端點。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="ba5bc-154">這是為了確保在我們開始自訂範例應用程式前，Android Studio 沒有問題。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="ba5bc-155">在 Android Studio 中建置 `oidlib-sample` 並當作目標執行。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![oidlib-sample 建置進度](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="ba5bc-157">刪除從專案中移除模組時所留下的 `app ` 目錄，因為 Android Studio 會基於安全考量而不刪除它。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![包含應用程式目錄的檔案結構](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="ba5bc-159">開啟 [編輯設定]  功能表，移除從專案中移除模組時所留下的執行組態。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="ba5bc-160">![編輯設定功能表](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![執行應用程式設定](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="ba5bc-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="ba5bc-161">設定範例的端點</span><span class="sxs-lookup"><span data-stu-id="ba5bc-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="ba5bc-162">您現在已順利執行 `oidlib-sample`，讓我們編輯某些端點以便使用於 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="ba5bc-163">編輯 oidc_clientconf.xml 檔案來設定您的用戶端</span><span class="sxs-lookup"><span data-stu-id="ba5bc-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="ba5bc-164">因為您目前只使用 OAuth2 流量來取得權杖及呼叫圖形 API，所以將用戶端設定成只進行 OAuth2。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="ba5bc-165">後面的範例中會示範 OIDC。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="ba5bc-166">設定您從註冊入口網站收到的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="ba5bc-167">如下所示來設定您的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="ba5bc-168">設定您需要的範圍，以便存取 圖形 API。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="ba5bc-169">`oidc_scopes` 中的 `User.Read` 值可讓您讀取已登入使用者的基本設定檔。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="ba5bc-170">您可以在 [Microsoft Graph 權限範圍](https://graph.microsoft.io/docs/authorization/permission_scopes)，深入了解所有可用範圍。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="ba5bc-171">如果您想要 OpenID Connect 中有關 `openid` 或 `offline_access` 範圍的說明，請參閱 [2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="ba5bc-172">編輯 oidc_endpoints.xml 檔案來設定用戶端端點</span><span class="sxs-lookup"><span data-stu-id="ba5bc-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="ba5bc-173">開啟 `oidc_endpoints.xml` 檔案並進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="ba5bc-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="ba5bc-174">如果您使用 OAuth2 做為通訊協定，則不得變更這些端點。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="ba5bc-175">Azure Active Directory 目前不支援 `userInfoEndpoint` 和 `revocationEndpoint` 的端點。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="ba5bc-176">如果您保留這些預設的 example.com 值，您將會不時看到提醒，說明無法在此範例中使用這些值 :-)</span><span class="sxs-lookup"><span data-stu-id="ba5bc-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="ba5bc-177">設定圖形 API 呼叫</span><span class="sxs-lookup"><span data-stu-id="ba5bc-177">Configure a Graph API call</span></span>
* <span data-ttu-id="ba5bc-178">開啟 `HomeActivity.java` 檔案並進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="ba5bc-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="ba5bc-179">以下的簡單圖形 API 呼叫會傳回我們的資訊。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="ba5bc-180">這些全都是您要進行的變更。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="ba5bc-181">執行 `oidlib-sample` 應用程式，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="ba5bc-182">順利通過驗證後，請選取 [要求受保護的資源]  按鈕，以測試您對圖形 API 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="ba5bc-183">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="ba5bc-183">Get security updates for our product</span></span>
<span data-ttu-id="ba5bc-184">我們鼓勵您造訪 [安全性 TechCenter](https://technet.microsoft.com/security/dd252948) 並訂閱資訊安全摘要報告警示，以收到有關安全性事件的通知。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

