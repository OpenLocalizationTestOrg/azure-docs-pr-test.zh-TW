---
title: "Azure Active Directory B2C︰使用自訂原則新增 Microsoft 帳戶 (MSA) 作為識別提供者"
description: "透過 OpenID 連線 (OIDC) 通訊協定使用 Microsoft 作為識別提供者的範例"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C︰使用自訂原則新增 Microsoft 帳戶 (MSA) 作為識別提供者

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

本文章將示範如何 tooenable 登入的使用者，從 Microsoft 帳戶 (MSA) 藉由使用 hello[自訂原則](active-directory-b2c-overview-custom.md)。

## <a name="prerequisites"></a>必要條件
完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。

這些步驟包括：

1.  建立 Microsoft 帳戶應用程式。
2.  加入 hello Microsoft 帳戶應用程式金鑰 tooAzure AD B2C
3.  新增宣告提供者 tooa 原則
4.  註冊 hello Microsoft 帳戶宣告提供者 tooa 使用者旅程
5.  上傳 hello 原則 tooan Azure AD B2C 租用戶，並進行測試

## <a name="create-a-microsoft-account-application"></a>建立 Microsoft 帳戶應用程式
身分識別提供者，在 Azure Active Directory (Azure AD) B2C 的 toouse Microsoft 帳戶，您需要 toocreate Microsoft 帳戶應用程式，並提供與 hello 正確的參數。 您需要 Microsoft 帳戶。 如果您沒有該帳戶，請瀏覽 [https://www.live.com/](https://www.live.com/)。

1.  移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)並以您的 Microsoft 帳戶認證登入。
2.  按一下 [新增應用程式] 。

    ![Microsoft 帳戶 - 新增應用程式](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  提供應用程式的 [名稱]、[連絡人電子郵件]、取消核取 [讓我們幫助您開始]，然後按一下 [建立]。

    ![Microsoft 帳戶 - 註冊您的應用程式](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  複製 hello 值**應用程式識別碼**。您需要它 tooconfigure Microsoft 帳戶做為身分識別提供者租用戶中。

    ![Microsoft 帳戶-應用程式識別碼的值複製 hello](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  按一下 [新增平台]

    ![Microsoft 帳戶 - 新增平台](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  從 hello 平台清單中選擇**Web**。

    ![Microsoft 帳戶-hello 平台清單中選擇 Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**重新導向 Uri**欄位。 使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。

    ![Microsoft 帳戶 - 設定重新導向 URL](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  按一下**產生新的密碼**下 hello**應用程式密碼**> 一節。 複製顯示在螢幕上的 hello 新密碼。 您需要它 tooconfigure Microsoft 帳戶做為身分識別提供者租用戶中。 此密碼是重要的安全性認證。

    ![Microsoft 帳戶 - 產生新密碼](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft 帳戶-複製 hello 新密碼](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  指出核取 hello 方塊**Live SDK 支援**下 hello**進階選項**> 一節。 按一下 [儲存] 。

    ![Microsoft 帳戶 - Live SDK 支援](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>新增 hello Microsoft 帳戶應用程式金鑰 tooAzure AD B2C
使用 Microsoft 帳戶的同盟需要 Microsoft 帳戶 tootrust Azure AD B2C 代表 hello 應用程式用戶端密碼。 Azure AD B2C 租用戶中的您 Microsoft 帳戶應用程式 secert 需要 toostore:   

1.  移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構**
2.  選取**原則機碼**tooview hello 金鑰用於您的租用戶。
3.  按一下 [+新增]。
4.  針對 [選項] 使用 [手動]。
5.  針對 [名稱] 使用 `MSASecret`。  
    hello 前置詞`B2C_1A_`可能會自動加入。
6.  在 hello**密碼**方塊中，輸入您的 Microsoft 應用程式密碼，從 https://apps.dev.microsoft.com
7.  針對 [金鑰使用方法] 使用 [簽章]。
8.  按一下 [建立] 
9.  確認您已建立 hello 金鑰`B2C_1A_MSASecret`。

## <a name="add-a-claims-provider-in-your-extension-policy"></a>在擴充原則中新增宣告提供者
如果您希望使用者 toosign 使用 Microsoft 帳戶，您會需要的宣告提供者 toodefine Microsoft 帳戶。 換句話說，您需要 toospecify 與 Azure AD B2C 通訊的端點。 hello 端點提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。

定義 Microsoft 帳戶作為宣告提供者，方法是在擴充原則檔案中新增 `<ClaimsProvider>` 節點：

1.  從您的工作目錄中開啟 hello 擴充原則檔 (TrustFrameworkExtensions.xml)。 如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。
2.  尋找 hello`<ClaimsProviders>`區段
3.  加入下列 XML 程式碼片段在 hello`ClaimsProviders`項目：

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  使用您的 Microsoft 帳戶應用程式用戶端識別碼來取代 `client_id` 值

5.  儲存 hello 檔案。

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>註冊 hello Microsoft 帳戶宣告提供者 tooSign 註冊或登入使用者之旅

此時，hello 身分識別提供者已設定，但不是可在任何 hello sign-up/登入畫面。 現在您需要 tooadd hello Microsoft 帳戶身分識別提供者 tooyour 使用者`SignUpOrSignIn`使用者之旅。 toomake 它可用，我們建立的現有的範本使用者旅程重複。  然後我們會加入 hello Microsoft 帳戶的身分識別提供者：

> [!NOTE]
>
>如果您先前複製 hello`<UserJourneys>`基底檔案的原則 toohello 延伸模組檔案中的項目`TrustFrameworkExtensions.xml`，您可以略過 toothis > 一節。

1.  開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。
2.  尋找 hello`<UserJourneys>`項目，並複製 hello 整個內容`<UserJourneys>`節點。
3.  開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。 如果 hello 項目不存在，請加入一個參考。
4.  貼上 hello 整個內容`<UserJournesy>`您複製 hello 的子系的節點`<UserJourneys>`項目。

### <a name="display-hello-button"></a>顯示 hello 按鈕
hello`<ClaimsProviderSelections>`項目會定義 hello 宣告提供者選擇的選項清單以及它們的順序。  `<ClaimsProviderSelection>`項目是 sign-up/登入頁面上的類似 tooan 身分識別提供者按鈕。 如果您將加入`<ClaimsProviderSelection>`的 Microsoft 帳戶的項目，新的按鈕顯示落在 hello 頁面上的使用者。 tooadd 這個項目：

1.  尋找 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`hello 您複製的使用者歷程中。
2.  找出 hello`<OrchestrationStep>`包含的節點`Order="1"`
3.  在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>連結 hello 按鈕 tooan 動作
既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。 hello 動作，在此情況下，為 Microsoft 帳戶 tooreceive 與 Azure AD B2C toocommunicate 語彙基元。 藉由連結的 Microsoft 帳戶的宣告提供者的 hello 技術設定檔連結 hello 按鈕 tooan 動作：

1.  尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。
2.  在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * 請確定 hello`Id`具有相同的值為 hello `TargetClaimsExchangeId` hello 前面一節中
>   * 請確定`TechnicalProfileReferenceId`設定您建立舊版 (MSA-OIDC) toohello 技術設定檔的識別碼。

## <a name="upload-hello-policy-tooyour-tenant"></a>上傳 hello 原則 tooyour 租用戶
1.  在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。
2.  選取 [識別體驗架構]。
3.  開啟 hello**所有原則**刀鋒視窗。
4.  選取 [上傳原則]。
5.  請檢查**如果存在的話，請覆寫 hello 原則**方塊。
6.  **上傳**TrustFrameworkExtensions.xml，並確定它不會通過 hello 驗證

## <a name="test-hello-custom-policy-by-using-run-now"></a>使用 立即執行測試 hello 自訂原則

1.  開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。
> [!NOTE]
>
>**現在就執行**需要至少一個應用程式 toobe 預先 hello 租用戶上。 如何 tooregister 應用程式，請參閱的 toolearn hello Azure AD B2C[開始](active-directory-b2c-get-started.md)文章或 hello[應用程式註冊](active-directory-b2c-app-registration.md)發行項。
2.  開啟**B2C_1A_signup_signin**，hello 上載的信賴憑證者 (rp) 自訂原則。 選取 [立即執行]。
3.  您應該能夠 toosign 中使用的 Microsoft 帳戶。

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[選用]註冊 hello Microsoft 帳戶宣告提供者 tooProfile 編輯使用者旅程
您可能會想 tooadd hello Microsoft 帳戶身分識別提供者也 tooyour 使用者`ProfileEdit`使用者之旅。 toomake 提供，我們可以重覆 hello 最後的兩個步驟：

### <a name="display-hello-button"></a>顯示 hello 按鈕
1.  開啟 hello 原則 (例如，TrustFrameworkExtensions.xml) 的延伸模組檔案。
2.  尋找 hello`<UserJourney>`節點包含`Id="ProfileEdit"`hello 您複製的使用者歷程中。
3.  找出 hello`<OrchestrationStep>`包含的節點`Order="1"`
4.  在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>連結 hello 按鈕 tooan 動作
1.  尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。
2.  在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>使用 立即執行測試 hello 自訂設定檔編輯原則
1.  開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。
2.  開啟**B2C_1A_ProfileEdit**，hello 上載的信賴憑證者 (rp) 自訂原則。 選取 [立即執行]。
3.  您應該能夠 toosign 中使用的 Microsoft 帳戶。

## <a name="download-hello-complete-policy-files"></a>下載 hello 完整的原則檔案
選擇性： 我們建議您建置您使用您自己的自訂原則檔完成的 hello 開始使用自訂原則逐步執行，而不是使用這些範例檔案之後的案例。  [參考的範例原則檔案](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
