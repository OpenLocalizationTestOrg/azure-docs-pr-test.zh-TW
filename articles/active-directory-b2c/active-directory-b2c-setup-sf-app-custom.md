---
title: "Azure Active Directory B2C︰使用自訂原則新增 Salesforce SAML 提供者 | Microsoft Docs"
description: "深入了解如何 toocreate 和管理 Azure Active Directory B2C 的自訂原則。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C︰使用 Salesforce 帳戶透過 SAML 來登入

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

本文章將示範如何 toouse[自訂原則](active-directory-b2c-overview-custom.md)tooset 組成特定的 Salesforce 組織中使用者的登入。

## <a name="prerequisites"></a>必要條件

### <a name="azure-ad-b2c-setup"></a>Azure AD B2C 設定

請確定您已完成所有可為您示範如何太 hello 步驟[開始使用自訂原則](active-directory-b2c-get-started-custom.md)中 Azure Active Directory B2C (Azure AD B2C)。

其中包含：

* 建立 Azure AD B2C 租用戶。
* 建立 Azure AD B2C 應用程式。
* 註冊兩個原則引擎應用程式。
* 設定金鑰。
* 設定 hello 入門套件。

### <a name="salesforce-setup"></a>Salesforce 設定

在本文中，我們假設您已完成 hello 下列：

* 註冊 Salesforce 帳戶。 您可以註冊[免費的開發人員版本帳戶](https://developer.salesforce.com/signup)。
* 為您的 Salesforce 組織[設定網域](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0)。

## <a name="set-up-salesforce-so-users-can-federate"></a>設定 Salesforce，讓使用者可以建立同盟

toohelp 與 Salesforce 的 Azure AD B2C 通訊，您需要 tooget hello Salesforce 中繼資料 URL。

### <a name="set-up-salesforce-as-an-identity-provider"></a>將 Salesforce 設定為識別提供者

> [!NOTE]
> 在本文中，我們假設您使用 [Salesforce Lightning 經驗](https://developer.salesforce.com/page/Lightning_Experience_FAQ)。

1. [登入 tooSalesforce](https://login.salesforce.com/)。 
2. 於 hello 上左功能表中，在**設定**，依序展開**識別**，然後按一下**身分識別提供者**。
3. 按一下 [啟用識別提供者]。
4. 在下**選取 hello 憑證**，選取您想要使用 Azure AD B2C Salesforce toouse toocommunicate hello 憑證。 （您可以使用 hello 預設憑證）。按一下 [儲存] 。 

### <a name="create-a-connected-app-in-salesforce"></a>在 Salesforce 中建立連線應用程式

1. 在 hello**身分識別提供者**頁面上，移過**服務提供者**。
2. 按一下 [現在透過連線應用程式建立服務提供者]**。**按一下這裡。
3. 在下**基本資訊**，輸入您已連線的應用程式所需的 hello 值。
4. 在下**Web 應用程式設定**，選取 hello**啟用 SAML**核取方塊。
5. 在 hello**實體識別碼**欄位中，輸入下列 URL 的 hello。 請確定您取代 hello 值`tenantName`。
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. 在 hello **ACS URL**欄位中，輸入下列 URL 的 hello。 請確定您取代 hello 值`tenantName`。
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. 保留所有其他設定的 hello 預設值。
8. 捲動 toohello hello 清單底部，然後按一下**儲存**。

### <a name="get-hello-metadata-url"></a>取得 hello 中繼資料 URL

1. 在您連接的應用程式的 hello 概觀頁面上，按一下 **管理**。
2. 複製 hello 值**中繼資料探索端點**，並將其儲存。 您將在本文稍後使用它。

### <a name="set-up-salesforce-users-toofederate"></a>設定 Salesforce 使用者 toofederate

1. 在 hello**管理**頁面已連線的應用程式移過**設定檔**。
2. 按一下 [管理設定檔]。
3. Hello 設定檔 （或使用者群組） 選取您想使用 Azure AD B2C toofederate。 身為系統管理員，選取 hello**系統管理員**核取方塊，以便您可以使用您的 Salesforce 帳戶同盟。

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>產生 Azure AD B2C 的簽署憑證

由 Azure AD B2C 簽署 tooSalesforce 需要 toobe 傳送要求。 toogenerate 簽署的憑證，開啟 Azure PowerShell，然後再執行下列命令的 hello。

> [!NOTE]
> 請確定您更新 hello 頂端的兩行程式碼中 hello 租用戶名稱和密碼。

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>新增 hello SAML 簽章憑證 tooAzure AD B2C

上傳簽署的憑證 tooyour Azure AD B2C 租用戶的 hello: 

1. 移 tooyour Azure AD B2C 租用戶。 按一下 [設定]  >  [身分識別體驗架構]  >  [原則金鑰]。
2. 按一下 [+新增]，然後：
    1. 按一下 [選項]  >  [上傳]。
    2. 輸入**名稱** (例如，SAMLSigningCert)。 hello 前置詞*B2C_1A_*會自動加入 toohello 金鑰的名稱。
    3. tooselect 憑證，請選取**上傳檔案控制項**。 
    4. 輸入您在 hello PowerShell 指令碼中設定的 hello 憑證的密碼。
3. 按一下 [建立] 。
4. 請確認您已建立金鑰 (例如，B2C_1A_SAMLSigningCert)。 記下 hello 完整名稱 (包括*B2C_1A_*)。 您將參考 toothis 稍後 hello 原則中的索引鍵。

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>建立基底原則中的 hello Salesforce SAML 宣告提供者

您需要 toodefine Salesforce 的宣告提供者，使用者可以使用登入 Salesforce。 換句話說，您需要 Azure AD B2C 將與其通訊的 toospecify hello 端點。 hello 端點將*提供*一組*宣告*Azure AD B2C 使用特定的使用者已驗證的 tooverify。 toodo，新增`<ClaimsProvider>`salesforce 原則的 hello 延伸模組檔案中：

1. 在您的工作目錄中開啟 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)。
2. 尋找 hello `<ClaimsProviders>` > 一節。 如果不存在，則會建立 hello 根節點下。
3. 新增 `<ClaimsProvider>`：

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

在 hello`<ClaimsProvider>`節點：

1. 變更 hello 值`<Domain>`tooa 區別的唯一值`<ClaimsProvider>`來自其他身分識別提供者。
2. 更新 hello 值`<DisplayName>`tooa hello 的顯示名稱宣告提供者。 目前不使用此值。

### <a name="update-hello-technical-profile"></a>更新 hello 技術設定檔

tooget SAML 權杖中來自 Salesforce，定義 Azure AD B2C 將 Azure Active Directory (Azure AD) 搭配使用 toocommunicate hello 通訊協定。 這樣在 hello`<TechnicalProfile>`元素`<ClaimsProvider>`:

1. 更新 hello 識別碼 hello`<TechnicalProfile>`節點。 這個識別碼是使用的 toorefer toothis 技術 hello 原則的其他部分的設定檔。
2. 更新 hello 值`<DisplayName>`。 這個值會顯示在 hello 登入您的登入頁面上按鈕。
3. 更新 hello 值`<Description>`。
4. Salesforce 使用 hello SAML 2.0 通訊協定。 請確定該 hello 值`<Protocol>`是**SAML2**。

更新 hello `<Metadata>` hello 前面 XML tooreflect hello 設定特定的 Salesforce 帳戶中一節。 在 hello XML，更新 hello 中繼資料值：

1. 更新 hello 值`<Item Key="PartnerEntity">`以您先前複製的 hello Salesforce 中繼資料 URL。 它有下列格式的 hello: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. 在 hello`<CryptographicKeys>`區段中，兩個執行個體的更新 hello 值`StorageReferenceId`toohello hello 索引鍵，您的簽署憑證 (例如，B2C_1A_SAMLSigningCert) 的名稱。

### <a name="upload-hello-extension-file-for-verification"></a>上傳 hello 進行驗證的延伸模組檔案

您的原則現在已設定，讓 Azure AD B2C 知道如何與 Salesforce toocommunicate。 嘗試上傳您的原則，並不包含任何問題為止 tooverify hello 延伸模組檔案。 原則的 tooupload hello 延伸模組檔案：

1. 在 您的 Azure AD B2C 租用戶移 toohello**所有原則**刀鋒視窗。
2. 選取 hello**如果存在的話，請覆寫 hello 原則**核取方塊。
3. 上傳 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)。 請確定它不會驗證失敗。

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>註冊 hello Salesforce SAML 宣告提供者 tooa 使用者旅程

接下來，新增的使用者皆 Salesforce SAML 身分識別提供者 tooone hello。 此時，hello 身分識別提供者已設定，但它並不適用於任何 hello 使用者註冊或登入頁面。 tooadd hello 身分識別提供者 tooa 登入頁面上，首先，建立現有的範本使用者旅程的重複。 然後，修改 hello 範本，讓它也有 hello Azure AD 身分識別提供者。

1. 開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。
2. 尋找 hello`<UserJourneys>`項目，然後按一下 複製 hello 整個`<UserJourney>`值，包括 Id ="SignUpOrSignIn"。
3. 開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)。 尋找 hello`<UserJourneys>`項目。 如果 hello 項目不存在，請建立一個。
4. 貼上 hello 整個複製`<UserJourney>`做為子系的 hello`<UserJourneys>`項目。
5. 重新命名新的 hello hello 識別碼`<UserJourney>`(例如，SignUpOrSignUsingContoso)。

### <a name="display-hello-identity-provider-button"></a>顯示 hello 身分識別提供者 按鈕

hello`<ClaimsProviderSelection>`項目是在註冊或登入頁面類似 tooan 身分識別提供者 按鈕。 藉由新增`<ClaimsProviderSelection>`salesforce 的項目，新的按鈕會顯示當使用者 toothis 頁面。 toodisplay hello 身分識別提供者按鈕：

1. 在 hello`<UserJourney>`您所建立，在此找到 hello`<OrchestrationStep>`與`Order="1"`。
2. 加入下列 XML 的 hello:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. 設定`TargetClaimsExchangeId`tooa 邏輯值。 我們建議下列 hello 相同慣例與其他人 (例如，  *\[ClaimProviderName\]Exchange*)。

### <a name="link-hello-identity-provider-button-tooan-action"></a>連結 hello 身分識別提供者按鈕 tooan 動作

既然您已備妥身分識別提供者 按鈕，請將它連結 tooan 動作。 在此情況下，hello 動作是 Azure AD B2C toocommunicate 與 Salesforce tooreceive SAML 權杖。 您可以藉由連結 hello 技術設定檔的 Salesforce SAML 宣告提供者：

1. 在 hello`<UserJourney>`節點、 尋找 hello`<OrchestrationStep>`與`Order="2"`。
2. 加入下列 XML 的 hello:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. 更新`Id`toohello 相同的值，是您稍早用於`TargetClaimsExchangeId`。
4. 更新`TechnicalProfileReferenceId`toohello `Id` hello 技術的設定檔您稍早建立 (例如，ContosoProfile)。

### <a name="upload-hello-updated-extension-file"></a>上傳 hello 更新延伸模組檔案

您已完成修改 hello 延伸模組檔案。 儲存並上傳這個檔案。 請確定所有驗證都成功。

### <a name="update-hello-relying-party-file"></a>更新 hello 信賴憑證者的合作對象檔案

接下來，更新 hello 信賴憑證者 (rp) 檔案來起始 hello 您所建立的使用者歷程：

1. 在您的工作目錄中建立一份 SignUpOrSignIn.xml 複本。 然後，將它重新命名 (例如，SignUpOrSignInWithAAD.xml)。
2. 開啟 hello 新檔案並更新 hello`PolicyId`屬性`<TrustFrameworkPolicy>`包含唯一值。 這是原則的您 (例如，SignUpOrSignInWithAAD) hello 名稱。
3. 修改 hello`ReferenceId`屬性`<DefaultUserJourney>`toomatch hello `Id` hello 新使用者作業 （例如 SignUpOrSignUsingContoso） 建立。
4. 儲存您的變更，然後上傳 hello 檔案。

## <a name="test-and-troubleshoot"></a>測試及疑難排解

tootest hello 自訂原則，您只要上傳，hello Azure 入口網站中 toohello 原則 刀鋒視窗的 **立即執行**。 如果失敗，請參閱[針對自訂原則進行疑難排解](active-directory-b2c-troubleshoot-custom.md)。

## <a name="next-steps"></a>後續步驟

提供意見反應太[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)。
