---
title: "Azure Active Directory B2C︰使用自訂原則新增 ADFS 作為 SAML 識別提供者"
description: "如何 tooarticle ADFS 2016 使用 SAML 通訊協定和自訂原則設定"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C︰使用自訂原則新增 ADFS 作為 SAML 識別提供者

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

本文章向您示範如何 tooenable 登入使用者從 ADFS 帳戶透過 hello 使用[自訂原則](active-directory-b2c-overview-custom.md)。

## <a name="prerequisites"></a>必要條件

完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。

這些步驟包括：

1.  建立 ADFS 信賴憑證者信任。
2.  加入 hello ADFS Relying Party Trust 憑證 tooAzure AD B2C。
3.  新增宣告提供者 tooa 原則。
4.  註冊 hello ADFS 帳戶宣告提供者 tooa 使用者之旅。
5.  上傳 hello 原則 tooan Azure AD B2C 租用戶，並進行測試。

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate 的宣告感知信賴憑證者信任

toouse ADFS 中 Azure Active Directory (Azure AD) B2C 身分識別提供者，您需要 toocreate ADFS 信賴憑證者信任和提供 hello 正確的參數。

tooadd 新的信賴憑證者合作對象 hello AD FS 管理嵌入式管理單元使用信任，然後手動設定 hello，執行下列程序，在同盟伺服器上的 hello。

中的成員資格**管理員**，或在 hello 本機電腦上同等 hello 最小必要的 toocomplete 此程序。 檢閱使用 hello 適當的帳戶詳細資料和群組成員資格[本機與網域預設群組](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  在 [伺服器管理員] 中按一下 [工具]，然後選取 [ADFS 管理]。

2.  按一下 [新增信賴憑證者信任]。
    ![新增信賴憑證者信任](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  在 hello ** 褖畫惎**頁面上，選擇**宣告感知**按一下**啟動**。
    ![在 [hello 歡迎使用] 頁面上選擇 [宣告感知](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  在 hello**選取資料來源**頁面上，按一下**手動輸入 hello 信賴憑證者的合作對象相關資料**，然後按一下**下一步**。
    ![輸入 hello 信賴憑證者相關資料](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  在 hello**指定顯示名稱**頁面上，輸入中的名稱**顯示名稱**下**備忘稿**輸入此信賴憑證者信任的描述，然後按一下**下一步**.
    ![指定顯示名稱和注意事項](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  選用。 如果您有選擇性的權杖加密憑證，然後在 hello**設定憑證**頁面上，按一下**瀏覽**toolocate 您憑證檔案，然後按一下**下一步**.
    ![設定憑證](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  在 hello**設定 URL**頁面上，選取 hello**啟用 hello SAML 2.0 WebSSO 通訊協定的支援**核取方塊。 在下**信賴憑證者合作對象 SAML 2.0 SSO 服務 URL**，輸入此信賴憑證者信任，hello 安全性聲明標記語言 (SAML) 服務端點 URL，然後按一下**下一步**。  Hello**信賴憑證者合作對象 SAML 2.0 SSO 服務 URL**，貼上 hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`。 {Tenant} 取代為您的租用戶名稱 (例如，contosob2c.onmicrosoft.com) 和 hello {原則} 取代為您擴充功能的原則名稱 (例如，B2C_1A_TrustFrameworkExtensions)。
    > [!IMPORTANT]
    >hello 原則名稱為 hello 其中一個，在此情況下，它是繼承自 signup_or_signin 原則： `B2C_1A_TrustFrameworkExtensions`。
    >例如 hello URL 可能是： https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**。

    ![信賴憑證者 SAML 2.0 SSO 服務 URL](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. 在 hello**設定識別碼**頁面上，指定 hello 相同的 URL hello 先前步驟中，按一下**新增**tooadd 它們 toohello 清單，然後再按**下一步**。
    ![信賴憑證者信任識別碼](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  在 hello**選擇的存取控制原則**選取原則，然後按一下 **下一步**。
    ![選擇存取控制原則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  在 [hello**準備 tooAdd 信任**頁面上，檢閱 hello 設定，然後按一下**下一步]** toosave 您信賴憑證者信任資訊。
    ![儲存您的信賴憑證者信任資訊](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  在 [hello**完成**頁面上，按一下**關閉**，此動作會自動顯示 hello**編輯宣告規則**] 對話方塊。
    ![編輯宣告規則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. 按一下 [新增規則] 。  
      ![新增規則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  在 [宣告規則範本] 中，選取 [傳送 LDAP 屬性作為宣告]。
    ![選取傳送 LDAP 屬性作為宣告範本規則](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  提供**宣告規則名稱**。 Hello**屬性存放區**選取**選取 Active Directory**新增 hello 下列宣告，然後按一下 **完成**和**確定**。
    ![設定規則屬性](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  在 伺服器管理員 中，選取**信賴憑證者信任**選取 hello 信賴憑證者信任您所建立，然後按一下 **屬性**。
    ![信賴憑證者編輯屬性](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  其中一個 hello 信賴憑證者的合作對象信任 （B2C 示範） 屬性] 視窗按一下**簽章**索引標籤上，按一下 [**新增**。  
    ![設定簽章](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  新增簽章憑證 (.cert 檔案，不含私密金鑰)。  
    ![新增簽章憑證](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  在 [hello 信賴憑證者合作對象信任 （B2C 示範） 屬性] 視窗上按一下**進階**索引標籤，然後變更 hello**安全雜湊演算法**太**sha-1**，按一下**確定**.  
    ![設定安全雜湊演算法 tooSHA 1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>新增 hello ADFS 帳戶應用程式金鑰 tooAzure AD B2C
使用 ADFS 帳戶的同盟需要 ADFS 帳戶 tootrust Azure AD B2C 代表 hello 應用程式用戶端密碼。 您需要 toostore ADFS 憑證在 Azure AD B2C 租用戶中。 

1.  移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構**
2.  選取**原則機碼**tooview hello 金鑰用於您的租用戶。
3.  按一下 [+新增]。
4.  針對 [選項] 使用 [上傳]。
5.  針對 [名稱] 使用 `ADFSSamlCert`。  
    hello 前置詞`B2C_1A_`可能會自動加入。
6.  在 hello 檔案上傳，* * 選取私密金鑰憑證.pfx 檔案。 注意： 這個憑證 （含 hello 私密金鑰） 應該 hello 核發，會用於 hello ADFS 信賴憑證者的合作對象的同一個。
![上傳原則金鑰](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  按一下 [建立] 
8.  確認您已建立 hello 金鑰`B2C_1A_ADFSSamlCert`。

## <a name="add-a-claims-provider-in-your-extension-policy"></a>在擴充原則中新增宣告提供者
如果您希望使用者 toosign 使用 ADFS 帳戶，您會需要 toodefine ADFS 帳戶做為宣告提供者。 換句話說，您需要 toospecify 與 Azure AD B2C 通訊的端點。 hello 端點提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。

定義 ADFS 作為宣告提供者，方法是在擴充原則檔案中新增 `<ClaimsProvider>` 節點：

1. 從您的工作目錄中開啟 hello 擴充原則檔 (TrustFrameworkExtensions.xml)。 如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。
2. 尋找 hello`<ClaimsProviders>`區段
3. 加入下列 XML 程式碼片段在 hello hello`ClaimsProviders`項目和取代`identityProvider`DNS （任意值，指出您的網域），然後儲存 hello 檔案。 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>註冊 hello ADFS 帳戶宣告提供者 tooSign 註冊或登入使用者之旅
此時，hello 身分識別提供者已設定。  不過，它不是可在任何 hello sign-up/登入畫面。 現在您需要 tooadd hello ADFS 帳戶身分識別提供者 tooyour 使用者`SignUpOrSignIn`使用者之旅。 toomake 它可用，我們建立的現有的範本使用者旅程重複。  然後，我們修改它使其包含 hello ADFS 身分識別提供者：
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。
2.  尋找 hello`<UserJourneys>`項目，並複製 hello 整個內容`<UserJourneys>`節點。
3.  開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。 如果 hello 項目不存在，請加入一個參考。
4.  貼上 hello 整個內容`<UserJournesy>`您複製 hello 的子系的節點`<UserJourneys>`項目。

### <a name="display-hello-button"></a>顯示 hello 按鈕
hello`<ClaimsProviderSelections>`項目會定義 hello 宣告提供者選擇的選項清單以及它們的順序。  `<ClaimsProviderSelection>`項目是 sign-up/登入頁面上的類似 tooan 身分識別提供者按鈕。 如果您將加入`<ClaimsProviderSelection>`ADFS 帳戶項目，新的按鈕顯示落在 hello 頁面上的使用者。 tooadd 這個項目：

1.  尋找 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`hello 您複製的使用者歷程中。
2.  找出 hello`<OrchestrationStep>`包含的節點`Order="1"`
3.  在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>連結 hello 按鈕 tooan 動作

既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。 hello 動作，在此情況下，為 Azure AD B2C toocommunicate 與 ADFS 帳戶 tooreceive 語彙基元。 連結 hello 按鈕 tooan 動作連結 hello 技術設定檔的 ADFS 帳戶宣告提供者：

1.  尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。
2.  在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * 請確定 hello`Id`具有相同的值為 hello `TargetClaimsExchangeId` hello 前面一節中。
> * 請確定`TechnicalProfileReferenceId`設定您建立舊版 (Contoso-SAML2) toohello 技術設定檔。

## <a name="upload-hello-policy-tooyour-tenant"></a>上傳 hello 原則 tooyour 租用戶
1.  在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。
2.  選取 [識別體驗架構]。
3.  開啟 hello**所有原則**刀鋒視窗。
4.  選取 [上傳原則]。
5.  請檢查**如果存在的話，請覆寫 hello 原則**方塊。
6.  **上傳**TrustFrameworkExtensions.xml，並確定它不會通過 hello 驗證

## <a name="test-hello-custom-policy-by-using-run-now"></a>使用 立即執行測試 hello 自訂原則
1.  開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。
2.  開啟**B2C_1A_signup_signin**，hello 上載的信賴憑證者 (rp) 自訂原則。 選取 [立即執行]。
3.  您應該能夠使用 ADFS 帳戶 toosign。

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[選用]註冊 hello ADFS 帳戶宣告提供者 tooProfile 編輯使用者旅程
您可能會想 tooadd hello ADFS 帳戶身分識別提供者也 tooyour 使用者`ProfileEdit`使用者之旅。 toomake 提供，我們可以重覆 hello 最後的兩個步驟：

### <a name="display-hello-button"></a>顯示 hello 按鈕
1.  開啟 hello 原則 (例如，TrustFrameworkExtensions.xml) 的延伸模組檔案。
2.  尋找 hello`<UserJourney>`節點包含`Id="ProfileEdit"`hello 您複製的使用者歷程中。
3.  找出 hello`<OrchestrationStep>`包含的節點`Order="1"`
4.  在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>連結 hello 按鈕 tooan 動作
1.  尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。
2.  在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>使用 立即執行測試 hello 自訂設定檔編輯原則
1.  開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。
2.  開啟**B2C_1A_ProfileEdit**，hello 上載的信賴憑證者 (rp) 自訂原則。 選取 [立即執行]。
3.  您應該能夠使用 ADFS 帳戶 toosign。

## <a name="download-hello-complete-policy-files"></a>下載 hello 完整的原則檔案
選擇性： 我們建議您建置您的案例完成的 hello 開始使用自訂原則逐步解說之後使用您自己的自訂原則檔案。 [原則範例檔案僅供參考](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
