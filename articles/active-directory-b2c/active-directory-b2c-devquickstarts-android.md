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
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C︰使用 Android 應用程式登入

hello Microsoft 識別身分平台中使用 OAuth2 和 OpenID Connect 等的開放標準。 這可讓開發人員 tooleverage 他們希望 toointegrate 與我們的服務的任何文件庫。 tooaid 使用我們的平台與其他程式庫開發人員，我們已經撰寫這個一個 toodemonstrate 像幾個逐步解說如何 tooconfigure 第 3 個合作對象文件庫 tooconnect toohello Microsoft 識別平台。 實作的大部分程式庫[hello RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)將會無法 tooconnect toohello Microsoft 識別身分平台。

> [!WARNING]
> Microsoft 並不提供第三方程式庫的修正程式，也尚未審查這些程式庫。 這個範例會使用稱為基本案例中的相容性，以 hello Azure AD B2C AppAuth 已測試的第 3 個合作對象程式庫。 問題和功能要求應該導向的 toohello 程式庫的開放原始碼專案。 如需詳細資訊，請參閱[這篇文章](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)。  
>
>

如果您是新 tooOAuth2 或 OpenID Connect 此範例組態中的許多可能不會更有意義 tooyou。 我們建議您查看簡短[我們已記載的 hello 通訊協定概觀](active-directory-b2c-reference-protocols.md)。

## <a name="get-an-azure-ad-b2c-directory"></a>取得 Azure AD B2C 目錄

您必須先建立目錄或租用戶，才可使用 Azure AD B2C。 目錄為所有使用者、應用程式、群組等項目的容器。 如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。

## <a name="create-an-application"></a>建立應用程式

接下來，您需要 toocreate 應用程式中 B2C 目錄。 提供 Azure AD 需要 toocommunicate 安全地與您的應用程式的資訊。 toocreate 行動裝置應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。 請務必：

* 包含**原生用戶端**hello 應用程式中。
* 複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。 稍後您將會需要此資訊。
* 設定原生用戶端**重新導向 URI** (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)。 稍後您也會需要此資訊。

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>建立您的原則

在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。 此應用程式包含一個身分識別體驗：合併登入和註冊。 您將 toocreate 需要這項原則，如中所述[原則參考文件](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)。 當您建立 hello 原則時，請務必：

* 選擇 hello**顯示名稱**做為註冊的屬性，在您的原則。
* 選擇 hello**顯示名稱**和**物件識別碼**中每個原則的應用程式宣告。 您也可以選擇其他宣告。
* 複製 hello**名稱**的每個原則建立之後。 就不應有 hello 前置詞`b2c_1_`。  稍後您將需要 hello 原則名稱。

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

您已建立您的原則之後，您便準備好 toobuild 您的應用程式。

## <a name="download-hello-sample-code"></a>下載 hello 範例程式碼

我們[在 GitHub 上](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)提供一個使用 AppAuth 和 Azure AD B2C 的操作範例。 您可以下載 hello 程式碼，並執行它。 您可以快速地開始使用您自己的應用程式使用您自己的 Azure AD B2C 組態 hello 中的 hello 指示[README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md)。

hello 範例是修改所提供的 hello 範例[AppAuth](https://openid.github.io/AppAuth-Android/)。 請瀏覽其頁面 toolearn 更多關於 AppAuth 和它的功能。

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>修改您應用程式 toouse Azure AD B2C AppAuth 與

> [!NOTE]
> AppAuth 支援 Android API 16 (Jellybean) 和更新版本。 我們建議使用 API 23 和更新版本。
>

### <a name="configuration"></a>組態

藉由其中一個指定的 hello 探索 URI 或藉由指定 hello 授權端點和權杖的端點 Uri，您可以設定與 Azure AD B2C 通訊。 在任一情況下，您需要下列資訊的 hello:

* 租用戶識別碼 (例如，contoso.onmicrosoft.com)
* 原則名稱 (例如，B2C\_1\_SignUpIn)

如果您選擇 tooautomatically 探索 hello 授權和語彙基元端點 Uri，您必須從 hello 探索 URI toofetch 資訊。 URI 可以由取代 hello 租用戶產生的 hello 探索\_識別碼和 hello 原則\_hello 下列 URL 中的名稱：

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

然後，您可以取得 hello 授權和語彙基元端點 Uri，並執行 hello 下列建立 AuthorizationServiceConfiguration 物件：

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

不使用探索 tooobtain hello 授權和語彙基元端點 Uri 時，您也可以指定它們明確取代 hello 租用戶\_識別碼和 hello 原則\_下列 hello URL 名稱：

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

執行下列程式碼 toocreate hello AuthorizationServiceConfiguration 物件：

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>授權

設定或擷取授權服務組態之後，就可以建構授權要求。 toocreate hello 要求，您將需要下列資訊的 hello:

* 用戶端識別碼 (例如，00000000-0000-0000-0000-000000000000)
* 使用自訂配置的重新導向 URI (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

這兩個項目應該已在您[註冊應用程式](#create-an-application)時儲存。

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

請參閱 toohello [AppAuth 指南](https://openid.github.io/AppAuth-Android/)上 toocomplete hello hello 程序的其餘部分的方式。 如果您需要 tooquickly 開始使用工作應用程式，請簽出[我們的範例](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)。 Hello 中的 hello 步驟[README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter 您自己的 Azure AD B2C 組態。

我們一定是開啟 toofeedback，以及建議 ！ 如果您有本主題中，任何問題，或有改善此內容的建議，我們非常感謝您在 hello hello 頁面底部的意見反應。 功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。

