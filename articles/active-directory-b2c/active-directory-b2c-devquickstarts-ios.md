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
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C︰使用 iOS 應用程式登入

hello Microsoft 識別身分平台中使用 OAuth2 和 OpenID Connect 等的開放標準。 使用開放標準的通訊協定提供開發人員選項，選取 與我們的服務程式庫 toointegrate 時。 我們提供了本逐步解說，以及其他類似 tooaid 開發人員撰寫連接 toohello Microsoft 身分識別平台的應用程式。 實作的大部分程式庫[hello RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)無法 tooconnect toohello Microsoft 身分識別平台。

> [!WARNING]
> Microsoft 並不提供第三方程式庫的修正程式，也尚未審查這些程式庫。 這個範例會使用稱為 AppAuth 已測試的基本案例中以 hello Azure AD B2C 的相容性的協力廠商程式庫。 問題和功能要求應該導向的 toohello 程式庫的開放原始碼專案。 如需詳細資訊，請參閱 [本篇文章](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)。
>
>

如果您是新 tooOAuth2 或 OpenID Connect，此範例組態中的許多可能不會更有意義 tooyou。 我們建議您查看簡短[我們已記載的 hello 通訊協定概觀](active-directory-b2c-reference-protocols.md)。

## <a name="get-an-azure-ad-b2c-directory"></a>取得 Azure AD B2C 目錄
您必須先建立目錄或租用戶，才可使用 Azure AD B2C。 目錄就是您所有使用者、應用程式、群組等項目的容器。 如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。

## <a name="create-an-application"></a>建立應用程式
接下來，您需要 toocreate 應用程式中 B2C 目錄。 hello 應用程式註冊可讓 Azure AD 需要 toocommunicate 安全地與您的應用程式的資訊。 toocreate 行動裝置應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。 請務必：

* 包含**原生用戶端**hello 應用程式中。
* 複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。 您稍後需要此 GUID。
* 使用自訂配置設定**重新導向 URI** (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)。 您稍後需要此 URI。

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>建立您的原則
在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。 此應用程式包含一個身分識別體驗：合併登入和註冊。 建立此原則，如[原則參考文章](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)所述。 當您建立 hello 原則時，請務必：

* 在下**註冊屬性**，選取 hello 屬性**顯示名稱**。  您也可以選取其他屬性。
* 在下**應用程式宣告**，選取 hello 宣告**顯示名稱**和**使用者的物件識別碼**。 您也可以選取其他宣告。
* 複製 hello**名稱**的每個原則建立之後。 原則名稱前面會加上`b2c_1_`當您儲存 hello 原則。  您稍後需要 hello 原則名稱。

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

您已建立您的原則之後，您便準備好 toobuild 您的應用程式。

## <a name="download-hello-sample-code"></a>下載 hello 範例程式碼
我們[在 GitHub 上](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)提供一個使用 AppAuth 和 Azure AD B2C 的操作範例。 您可以下載 hello 程式碼，並執行它。 toouse 您自己的 Azure AD B2C 租用戶，遵循 hello hello 指示[README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md)。

此範例建立遵照 hello 讀我檔案由 hello [GitHub 上的 iOS AppAuth 專案](https://github.com/openid/AppAuth-iOS)。 如需有關 hello 範例與 hello 程式庫的運作方式的詳細資訊，參考 hello AppAuth GitHub 上的讀我檔案。

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>修改您應用程式 toouse Azure AD B2C AppAuth 與

> [!NOTE]
> AppAuth 支援 iOS 7 及更新版本。  不過，toosupport 社交登入 Google，SFSafariViewController 上的需要這需要 iOS 9 或更高版本。
>

### <a name="configuration"></a>組態

您可以設定與 Azure AD B2C 通訊，藉由指定 hello 授權端點和權杖的端點 Uri。  toogenerate 這些 Uri，您需要下列資訊的 hello:
* 租用戶識別碼 (例如，contoso.onmicrosoft.com)
* 原則名稱 (例如，B2C\_1\_SignUpIn)

hello URI 可以由取代產生的權杖端點 hello 租用戶\_識別碼和 hello 原則\_hello 下列 URL 中的名稱：

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

hello URI 可以由取代產生的授權端點 hello 租用戶\_識別碼和 hello 原則\_hello 下列 URL 中的名稱：

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

執行下列程式碼 toocreate hello AuthorizationServiceConfiguration 物件：

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>授權

設定或擷取授權服務組態之後，就可以建構授權要求。 toocreate hello 要求，您需要下列資訊的 hello:  
* 用戶端識別碼 (例如，00000000-0000-0000-0000-000000000000)
* 使用自訂配置的重新導向 URI (例如，com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

這兩個項目應該已在您[註冊應用程式](#create-an-application)時儲存。

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

tooset 註冊您的應用程式 toohandle hello 重新導向 toohello URI 與 hello 自訂配置，您會需要 'URL 配置' tooupdate hello 清單程式 Info.pList 中：
* 開啟 Info.pList。
* 將滑鼠停留在像是 '配套 OS 類型程式碼' 的資料列，然後按一下 hello\+符號。
* 重新命名 hello 新資料列 'URL 的類型'。
* 按一下 hello 箭號 toohello 左邊的 URL 類型' tooopen hello 樹狀結構。
* 按一下 hello 箭號 toohello 左 '項目 0' tooopen hello 樹狀結構。
* 重新命名項目 0 too'URL 配置底下的第一個項目。
* 按一下 hello 箭號 toohello 左邊的樹狀目錄中 tooopen hello ' 的 URL 結構描述 '。
* 在 hello 'Value' 資料行，沒有空白欄位 toohello 左邊 '的 URL 結構描述' 之下的 ' 項目 0'。  設定 hello 值 tooyour 應用程式的唯一配置。  hello 值必須符合建立 hello OIDAuthorizationRequest 物件時用於 redirectURL hello 配置。  在我們的範例中，我們使用 hello 配置 'com.onmicrosoft.fabrikamb2c.exampleapp'。

請參閱 toohello [AppAuth 指南](https://openid.github.io/AppAuth-iOS/)上 toocomplete hello hello 程序的其餘部分的方式。 如果您需要 tooquickly 開始使用工作應用程式，請簽出[我們的範例](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)。 Hello 中的 hello 步驟[README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter 您自己的 Azure AD B2C 組態。

我們一定是開啟 toofeedback，以及建議 ！ 如果您有本主題中，任何問題，或有改善此內容的建議，我們非常感謝您在 hello hello 頁面底部的意見反應。 功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。
