---
title: "Azure Active Directory B2C︰使用自訂原則新增 Google+ 作為 OAuth2 識別提供者"
description: "透過 OAuth2 通訊協定使用 Google+ 作為識別提供者的範例"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C︰使用自訂原則新增 Google+ 作為 OAuth2 識別提供者

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

本指南也說明如何 tooenable 登入的使用者從透過 hello 使用 Google + 帳戶[自訂原則](active-directory-b2c-overview-custom.md)。

## <a name="prerequisites"></a>必要條件

完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。

這些步驟包括：

1.  建立 Google+ 帳戶應用程式。
2.  加入 hello Google + 帳戶應用程式金鑰 tooAzure AD B2C
3.  新增宣告提供者 tooa 原則
4.  註冊 hello Google + 帳戶宣告提供者 tooa 使用者旅程
5.  上傳 hello 原則 tooan Azure AD B2C 租用戶，並進行測試

## <a name="create-a-google-account-application"></a>建立 Google+ 帳戶應用程式
toouse Google + B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate Google + 應用程式和提供 hello 正確的參數。 您可以在這裡註冊 Google+ 應用程式：[https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)

1.  移 toohello [Google 開發人員主控台](https://console.developers.google.com/)並以您的 Google + 帳戶認證登入。
2.  按一下 [建立專案]，輸入 [專案名稱]，接著按一下 [建立]。

3.  按一下 hello**專案功能表**。

    ![Google+ 帳戶 - 選取專案](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  按一下 hello  **+**   按鈕。

    ![Google+ 帳戶 - 建立新的專案](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  輸入 專案名稱，然後按一下建立。

    ![Google+ 帳戶 - 新增專案](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  等候 hello 專案已就緒，然後按一下 hello**專案功能表**。

    ![Google + 帳戶-等候新的專案準備好 toouse](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  按一下專案名稱。

    ![Google + 帳戶-選取 hello 新專案](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  按一下**API Manager** ，然後按一下**認證**在 hello 左瀏覽。
9.  按一下 hello **OAuth 同意畫面**hello 頂端的索引標籤。

    ![Google+ 帳戶 - 設定 OAuth 同意畫面](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  選取或指定有效的**電子郵件地址**、提供**產品名稱**，然後按一下 [儲存]。

    ![Google+ - 應用程式認證](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  按一下 [新增認證]，然後選擇 [OAuth 用戶端識別碼]。

    ![Google+ - 建立新的應用程式認證](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  在 [應用程式類型] 下方，選取 [Web 應用程式]。

    ![Google+ - 選取應用程式類型](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  提供**名稱**針對您的應用程式中，輸入`https://login.microsoftonline.com`在 hello**授權 JavaScript origins**欄位，和`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**授權重新導向 Uri**欄位。 使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。 hello **{tenant}**值會區分大小寫。 按一下 [建立] 。

    ![Google+ - 提供授權的 JavaScript 來源及重新導向 URI](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  複製的 hello 值**用戶端識別碼**和**用戶端密碼**。 您需要這兩個 tooconfigure Google + 身分識別提供者租用戶中。 **用戶端密碼** 是重要的安全性認證。

    ![Google +-複製 hello 值的用戶端識別碼和用戶端密碼](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>新增 hello Google + 帳戶應用程式金鑰 tooAzure AD B2C
同盟與 Google + 帳戶會代表 hello 應用程式需要 Google + 帳戶 tootrust Azure AD B2C 用戶端密碼。 您需要 toostore Azure AD B2C 租用戶中的您 Google + 應用程式密碼：  

1.  移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構**
2.  選取**原則機碼**tooview hello 金鑰用於您的租用戶。
3.  按一下 [+新增]。
4.  針對 [選項] 使用 [手動]。
5.  針對 [名稱] 使用 `GoogleSecret`。  
    hello 前置詞`B2C_1A_`可能會自動加入。
6.  在 hello**密碼**方塊中，輸入您的 Microsoft 應用程式密碼，從 https://apps.dev.microsoft.com
7.  針對 [金鑰使用方法] 使用 [簽章]。
8.  按一下 [建立] 
9.  確認您已建立 hello 金鑰`B2C_1A_GoogleSecret`。

## <a name="add-a-claims-provider-in-your-extension-policy"></a>在擴充原則中新增宣告提供者

如果您希望使用者 toosign 使用 Google + 帳戶，您會需要 toodefine Google + 帳戶做為宣告提供者。 換句話說，您需要 toospecify 與 Azure AD B2C 通訊的端點。 hello 端點提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。

定義 Google+ 帳戶作為宣告提供者，方法是在擴充原則檔案中新增 `<ClaimsProvider>` 節點：

1.  從您的工作目錄中開啟 hello 擴充原則檔 (TrustFrameworkExtensions.xml)。 如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。
2.  尋找 hello`<ClaimsProviders>`區段
3.  加入下列 XML 程式碼片段在 hello hello`ClaimsProviders`項目和取代`client_id`與 Google + 帳戶應用程式用戶端識別碼 hello 檔案在儲存之前的值。  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>註冊 hello Google + 帳戶宣告提供者 tooSign 註冊或登入使用者之旅

已設定 hello 身分識別提供者。  不過，它不是可在任何 hello sign-up/登入畫面。 Hello Google + 帳戶身分識別提供者 tooyour 將使用者加入`SignUpOrSignIn`使用者之旅。 toomake 它可用，我們建立的現有的範本使用者旅程重複。  然後我們新增 hello Google + 帳戶身分識別提供者：

>[!NOTE]
>
>如果您要複製 hello`<UserJourneys>`項目從您的原則 toohello 延伸模組檔案 (TrustFrameworkExtensions.xml) 的基底的檔案，您可以略過 toothis > 一節。

1.  開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。
2.  尋找 hello`<UserJourneys>`項目，並複製 hello 整個內容`<UserJourneys>`節點。
3.  開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。 如果 hello 項目不存在，請加入一個參考。
4.  貼上 hello 整個內容`<UserJournesy>`您複製 hello 的子系的節點`<UserJourneys>`項目。

### <a name="display-hello-button"></a>顯示 hello 按鈕
hello`<ClaimsProviderSelections>`項目會定義 hello 宣告提供者選擇的選項清單以及它們的順序。  `<ClaimsProviderSelection>`項目是 sign-up/登入頁面上的類似 tooan 身分識別提供者按鈕。 如果您將加入`<ClaimsProviderSelection>`Google + 帳戶項目，新的按鈕顯示落在 hello 頁面上的使用者。 tooadd 這個項目：

1.  尋找 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`hello 您複製的使用者歷程中。
2.  找出 hello`<OrchestrationStep>`包含的節點`Order="1"`
3.  在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>連結 hello 按鈕 tooan 動作
既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。 hello 動作，在此情況下，為 Azure AD B2C toocommunicate 與 Google + 帳戶 tooreceive 語彙基元。

1.  尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。
2.  在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * 請確定 hello`Id`具有相同的值為 hello `TargetClaimsExchangeId` hello 前面一節中
> * 請確定`TechnicalProfileReferenceId`設定您建立舊版 (Google-OAUTH) toohello 技術設定檔的識別碼。

## <a name="upload-hello-policy-tooyour-tenant"></a>上傳 hello 原則 tooyour 租用戶
1.  在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。
2.  選取 [識別體驗架構]。
3.  開啟 hello**所有原則**刀鋒視窗。
4.  選取 [上傳原則]。
5.  請檢查**如果存在的話，請覆寫 hello 原則**方塊。
6.  **上傳**TrustFrameworkExtensions.xml，並確定它不會通過 hello 驗證

## <a name="test-hello-custom-policy-by-using-run-now"></a>使用 立即執行測試 hello 自訂原則
1.  開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。

    >[!NOTE]
    >
    >    **現在就執行**需要至少一個應用程式 toobe 預先 hello 租用戶上。 
    >    如何 tooregister 應用程式，請參閱的 toolearn hello Azure AD B2C[開始](active-directory-b2c-get-started.md)文章或 hello[應用程式註冊](active-directory-b2c-app-registration.md)發行項。


2.  開啟**B2C_1A_signup_signin**，hello 上載的信賴憑證者 (rp) 自訂原則。 選取 [立即執行]。
3.  您應該能夠使用 Google + 帳戶 toosign。

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[選用]註冊 hello Google + 帳戶宣告提供者 tooProfile 編輯使用者旅程
您可能會想 tooadd hello Google + 帳戶身分識別提供者也 tooyour 使用者`ProfileEdit`使用者之旅。 toomake 提供，我們可以重覆 hello 最後的兩個步驟：

### <a name="display-hello-button"></a>顯示 hello 按鈕
1.  開啟 hello 原則 (例如，TrustFrameworkExtensions.xml) 的延伸模組檔案。
2.  尋找 hello`<UserJourney>`節點包含`Id="ProfileEdit"`hello 您複製的使用者歷程中。
3.  找出 hello`<OrchestrationStep>`包含的節點`Order="1"`
4.  在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>連結 hello 按鈕 tooan 動作
1.  尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。
2.  在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>使用 立即執行測試 hello 自訂設定檔編輯原則

1.  開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。
2.  開啟**B2C_1A_ProfileEdit**，hello 上載的信賴憑證者 (rp) 自訂原則。 選取 [立即執行]。
3.  您應該能夠使用 Google + 帳戶 toosign。

## <a name="download-hello-complete-policy-files"></a>下載 hello 完整的原則檔案
選擇性： 我們建議您建置您使用您自己的自訂原則檔完成的 hello 開始使用自訂原則逐步執行，而不是使用這些範例檔案之後的案例。  [參考的範例原則檔案](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
