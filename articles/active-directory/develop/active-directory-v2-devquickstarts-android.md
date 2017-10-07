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
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>新增登入 tooan Android 應用程式使用 Graph API 使用 hello v2.0 端點使用協力廠商程式庫
hello Microsoft 識別身分平台中使用 OAuth2 和 OpenID Connect 等的開放標準。 開發人員可以使用任何文件庫，他們想 toointegrate 與我們的服務。 toohelp 開發人員會使用我們的平台與其他程式庫，我們已經撰寫這個一個 toodemonstrate 像幾個逐步解說如何 tooconfigure 協力廠商程式庫 tooconnect toohello Microsoft 識別平台。 實作的大部分程式庫[hello RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)可以連接 toohello Microsoft 識別平台。

這個逐步解說會建立 hello 應用程式，使用者可以登入 tootheir 組織，然後搜尋自行在組織中使用 hello Graph API。

如果您是新 tooOAuth2 或 OpenID Connect，此範例組態中的許多可能不會有意義 tooyou。 建議您閱讀 [2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)以瞭解背景。

> [!NOTE]
> 平台的 hello OAuth2 或 OpenID Connect 標準，例如條件式存取和 Intune 原則管理 中的運算式具有某些功能需要您 toouse 我們的開放原始碼 Microsoft Azure 身分識別的程式庫。
> 
> 

hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。

> [!NOTE]
> toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

## <a name="download-hello-code-from-github"></a>從 GitHub 下載 hello 程式碼
此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2)。  您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip)或再製 hello 基本架構：

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

您也可以下載 hello 範例，並立即開始：

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>註冊應用程式
建立新的應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或遵循 hello 詳細的步驟，網址[如何 tooregister 應用程式，但 hello v2.0 端點](active-directory-v2-app-registration.md)。  請確定：

* 複製 hello**應用程式識別碼**這是指派的 tooyour 應用程式因為很快就需要它。
* 新增 hello**行動**平台應用程式。

> 注意： hello 應用程式註冊入口網站提供**重新導向 URI**值。 不過，在此範例中必須使用 hello 預設值為`https://login.microsoftonline.com/common/oauth2/nativeclient`。
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>下載 hello NXOAuth2 協力廠商程式庫，並建立工作區
這個逐步解說中，您將使用 hello OIDCAndroidLib 從 GitHub，是根據 hello Google 的 OpenID Connect 的程式碼的 OAuth2 程式庫。 它會實作 hello 原生應用程式設定檔，並支援 hello 的 hello 使用者的授權端點。 這些是您將需要 toointegrate hello Microsoft 身分識別平台的所有 hello 項目時。

複製 hello OIDCAndroidLib 儲存機制 tooyour 電腦。

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>設定您的 Android Studio 環境
1. 建立新的 Android Studio 專案，並接受 hello hello 精靈中的預設值。
   
    ![在 Android Studio 中建立新專案](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![目標 Android 裝置](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![加入活動 toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset 您專案的模組，向上移動 hello 複製儲存機制 toohello 專案位置。 您可以也建立 hello 專案與然後複製它直接 toohello 專案位置。
   
    ![專案模組](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. 使用 [hello] 內容功能表或使用 hello Ctrl + Alt + Maj + S 捷徑，請開啟 hello 專案模組設定。
   
    ![專案模組設定](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. 移除 hello 預設應用程式的模組，因為您只想 hello 專案容器設定。
   
    ![hello 預設應用程式的模組](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. 匯入模組，從 hello 複製儲存機制 toohello 目前專案。
   
    ![匯入 gradle 專案](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG)![建立新的模組網頁](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. 重複上述步驟 hello`oidlib-sample`模組。
7. 檢查 hello oidclib 相依性 hello`oidlib-sample`模組。
   
    ![oidclib hello oidlib 範例模組上的相依性](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. 按一下 [確定]  並等候 gradle 同步處理。
   
    您的 settings.gradle 應如下所示：
   
    ![settings.gradle 的螢幕擷取畫面](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. 建置 hello 範例應用程式 toomake 確定正確地執行該 hello 範例。
   
    您將不會無法 toouse 這與 Azure Active Directory 尚未。 我們需要 tooconfigure 部份端點第一次。 這是 tooensure 我們開始自訂 hello 範例應用程式之前，您不需要 Android Studio 問題。
10. 建置並執行`oidlib-sample`做為在 Android Studio 中的 hello 目標。
    
    ![oidlib-sample 建置進度](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. 刪除 hello`app `時您 hello 模組從專案中移除 hello 因為 Android Studio 安全性並不會刪除它所保留的目錄。
    
    ![包含 hello 應用程式目錄的檔案結構](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. 開啟 hello**編輯組態**hello 模組從 hello 專案中移除時，也左功能表 tooremove hello 執行設定。
    
    ![編輯設定功能表](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![執行應用程式設定](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>設定 hello 端點的 hello 範例
既然您已擁有 hello`oidlib-sample`成功執行，讓編輯某些端點 tooget 這個與 Azure Active Directory 的工作。

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>設定您的用戶端藉由編輯 hello oidc_clientconf.xml 檔案
1. 因為您正在使用 OAuth2 流程只有 tooget 語彙基元，並呼叫 hello Graph API，設定 hello 用戶端 toodo OAuth2 只。 後面的範例中會示範 OIDC。
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. 設定您所收到 hello 註冊入口網站的用戶端識別碼。
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. 下列設定以其中一個 hello 您重新導向 URI。
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. 設定您的範圍，您需要在順序 tooaccess hello Graph API。
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

hello`User.Read`值`oidc_scopes`可讓您 tooread hello 基本設定檔 hello 登入的使用者。
您可以進一步了解在的 hello 可用範圍[Microsoft Graph 權限範圍](https://graph.microsoft.io/docs/authorization/permission_scopes)。

如果您想要 OpenID Connect 中有關 `openid` 或 `offline_access` 範圍的說明，請參閱 [2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)。

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>編輯 hello oidc_endpoints.xml 檔案設定用戶端端點
* 開啟 hello`oidc_endpoints.xml`檔案並製作 hello 下列變更：
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

如果您使用 OAuth2 做為通訊協定，則不得變更這些端點。

> [!NOTE]
> hello 端點`userInfoEndpoint`和`revocationEndpoint`目前不支援 Azure Active directory。 如果您離開的 hello 預設 example.com 值，則您會收到它們都不在 hello 範例:-)
> 
> 

## <a name="configure-a-graph-api-call"></a>設定圖形 API 呼叫
* 開啟 hello`HomeActivity.java`檔案並製作 hello 下列變更：
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

以下的簡單圖形 API 呼叫會傳回我們的資訊。

這些是您需要 toodo 所有 hello 變更。 執行 hello`oidlib-sample`應用程式，然後按一下**登入**。

您已成功通過驗證之後，請選取 hello**要求受保護資源**按鈕 tootest 您呼叫 toohello Graph API。

## <a name="get-security-updates-for-our-product"></a>取得產品的安全性更新
建議您 tooget 安全性事件通知所造訪 hello[資訊安全技術中心](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。

