---
title: "Azure Active Directory B2C︰使用自訂原則新增 Azure AD 提供者 | Microsoft Docs"
description: "深入了解 Azure Active Directory B2C 自訂原則"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C︰使用 Azure AD 帳戶登入

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

本文章向您示範如何 tooenable 登入使用者從特定的 Azure Active Directory (Azure AD) 組織透過 hello 使用[自訂原則](active-directory-b2c-overview-custom.md)。

## <a name="prerequisites"></a>必要條件

完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。

這些步驟包括：

1. 建立 Azure Active Directory B2C (Azure AD B2C) 租用戶。
2. 建立 Azure AD B2C 應用程式。
3. 註冊兩個原則引擎應用程式。
4. 設定金鑰。
5. 設定 hello 入門套件。

## <a name="create-an-azure-ad-app"></a>建立 Azure AD 應用程式

tooenable 登入的使用者從特定 Azure AD 組織中，您需要 tooregister hello 組織的 Azure AD 租用戶內的應用程式。

>[!NOTE]
> 我們使用"contoso.com"hello 組織的 Azure AD 租用戶和 「 fabrikamb2c.onmicrosoft.com"做為在下列指示的 hello hello Azure AD B2C 租用戶。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
1. 在 hello 頂端列中，選取您的帳戶。 從 hello**目錄**清單中，選擇您想要 tooregister hello 組織的 Azure AD 租用戶應用程式 (contoso.com)。
1. 選取**更多服務**在 hello 左的窗格中，並搜尋 「 應用程式註冊 」。
1. 選取 [新增應用程式註冊]。
1. 輸入應用程式的名稱 (例如，`Azure AD B2C App`)。
1. 選取**Web 應用程式 / 應用程式開發介面**hello 應用程式類型。
1. 如**登入 URL**，輸入下列 URL，hello 其中`yourtenant`取代為您的 Azure AD B2C 租用戶的 hello 名稱 (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. 儲存 hello 應用程式識別碼。
1. 選取新建立的 hello 應用程式。
1. 在 hello**設定**刀鋒視窗中，選取**金鑰**。
1. 建立新的金鑰並且儲存。 您可以將在 hello hello 下一節中的步驟。

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>新增金鑰 tooAzure AD B2C hello Azure AD

您在 Azure AD B2C 租用戶中需要 toostore hello contoso.com 應用程式金鑰。 toodo 這樣：
1. 移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構** > **原則機碼**。
1. 選取 [+新增]。
1. 選取或輸入這些選項：
   * 選取 [手動]。
   * 針對 [名稱]，選擇與您的 Azure AD 租用戶名稱相符的名稱 (例如，`ContosoAppSecret`)。  hello 前置詞`B2C_1A_`會自動加入 toohello 金鑰的名稱。
   * 將應用程式金鑰貼在 hello**密碼**方塊。
   * 選取 [簽章]。
1. 選取 [ **建立**]。
1. 確認您已建立 hello 金鑰`B2C_1A_ContosoAppSecret`。


## <a name="add-a-claims-provider-in-your-base-policy"></a>在基本原則中新增宣告提供者

如果您希望使用者 toosign 使用 Azure AD，您會需要 toodefine Azure AD 的宣告提供者。 換句話說，您需要 toospecify Azure AD B2C 將與其通訊的端點。 hello 端點會提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。 

您可以定義 Azure AD 的宣告提供者加入 Azure AD toohello`<ClaimsProvider>`原則的 hello 延伸模組檔案中的節點：

1. 從您的工作目錄中開啟 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)。
1. 尋找 hello `<ClaimsProviders>` > 一節。 如果不存在，請將它加入 hello 根節點下。
1. 新增 `<ClaimsProvider>` 節點，如下所示︰

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
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

1. 在 hello`<ClaimsProvider>`節點中，更新 hello 值`<Domain>`tooa 唯一值，可以是使用的 toodistinguish 它來自其他身分識別提供者。
1. 在 hello`<ClaimsProvider>`節點中，更新 hello 值`<DisplayName>`hello tooa 易記名稱宣告提供者。 目前不使用此值。

### <a name="update-hello-technical-profile"></a>更新 hello 技術設定檔

tooget hello Azure AD 端點中的語彙基元，您需要 Azure AD B2C，應該使用 Azure AD 使用 toocommunicate toodefine hello 通訊協定。 這是內部 hello`<TechnicalProfile>`元素`<ClaimsProvider>`。
1. 更新 hello 識別碼 hello`<TechnicalProfile>`節點。 這個識別碼是使用的 toorefer toothis 技術 hello 原則的其他部分的設定檔。
1. 更新 hello 值`<DisplayName>`。 此值將會顯示 hello 登入 5d; 按鈕登入畫面上。
1. 更新 hello 值`<Description>`。
1. Azure AD 使用 hello OpenID Connect 通訊協定，因此請確定該 hello 值`<Protocol>`是`"OpenIdConnect"`。

您需要 tooupdate hello `<Metadata>` hello XML 檔案中的區段參考 tooearlier tooreflect hello 組態設定您的特定 Azure AD 租用戶。 在 hello XML 檔案中，更新 hello 中繼資料值，如下所示：

1. 設定`<Item Key="METADATA">`太`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`，其中`yourAzureADtenant`是您的 Azure AD 租用戶名稱 (contoso.com)。
1. 開啟您的瀏覽器並前往 toohello`METADATA`剛更新的 URL。
1. 在 hello 瀏覽器中，尋找 hello 'issuer' 物件並將其值複製。 看起來應該像 hello 下列： `https://sts.windows.net/{tenantId}/`。
1. 貼上 hello 值`<Item Key="ProviderName">`hello XML 檔案中。
1. 設定`<Item Key="client_id">`toohello 從 hello 應用程式註冊的應用程式識別碼。
1. 設定`<Item Key="IdTokenAudience">`toohello 從 hello 應用程式註冊的應用程式識別碼。
1. 請確認`<Item Key="response_types">`設定得`id_token`。
1. 請確認`<Item Key="UsePolicyInRedirectUri">`設定得`false`。

您也需要您您 Azure AD B2C 租用戶 toohello Azure AD 中註冊的 toolink hello Azure AD 密碼`<ClaimsProvider>`資訊：

* 在 hello `<CryptographicKeys>` hello 前面 XML 檔案中區段中，更新 hello 值`StorageReferenceId`toohello 參考識別碼所定義的 hello 密碼 (比方說， `ContosoAppSecret`)。

### <a name="upload-hello-extension-file-for-verification"></a>上傳 hello 進行驗證的延伸模組檔案

現在，您已設定您的原則，讓 Azure AD B2C 知道如何與 Azure AD 目錄 toocommunicate。 嘗試上傳它不會有任何問題到目前為止您原則只 tooconfirm hello 延伸模組檔案。 toodo 因此：

1. 開啟 hello**所有原則**刀鋒視窗，您的 Azure AD B2C 租用戶中。
1. 檢查 hello**如果存在的話，請覆寫 hello 原則**方塊。
1. 上傳 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)，並確保不導致 hello 驗證失敗。

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>註冊 hello Azure AD 的宣告提供者 tooa 使用者旅程

您現在需要 tooadd hello Azure AD 身分識別提供者 tooone 的使用者皆。 此時，hello 身分識別提供者已設定，但不是可在任何 hello sign-up/登入畫面。 toomake 可用，我們將建立的現有的範本使用者作業，複製並修改它，讓它也有 hello Azure AD 身分識別提供者：

1. 開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。
1. 尋找 hello`<UserJourneys>`整個項目，並複製 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`。
1. 開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。 如果 hello 項目不存在，請加入一個參考。
1. 貼上 hello 整個`<UserJourney>`您複製 hello 的子系的節點`<UserJourneys>`項目。
1. 重新命名的新使用者旅程 hello hello 識別碼 (例如，重新命名為`SignUpOrSignUsingContoso`)。

### <a name="display-hello-button"></a>顯示 hello 「 按鈕 」

hello`<ClaimsProviderSelection>`項目是 sign-up/登入畫面上的類似 tooan 身分識別提供者 按鈕。 如果您將加入`<ClaimsProviderSelection>`Azure AD 的項目，新的按鈕顯示落在 hello 頁面上的使用者。 tooadd 這個項目：

1. 尋找 hello`<OrchestrationStep>`節點包含`Order="1"`hello 您剛才建立的使用者歷程中。
1. 加入下列 hello:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. 設定`TargetClaimsExchangeId`tooan 適當的值。 我們建議下列 hello 相同慣例與其他人：  *\[ClaimProviderName\]Exchange*。

### <a name="link-hello-button-tooan-action"></a>連結 hello 按鈕 tooan 動作

既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。 hello 動作，在此情況下，為 Azure AD B2C toocommunicate 與 Azure AD tooreceive 語彙基元。 連結 hello 按鈕 tooan 動作連結的 Azure AD 的宣告提供者的 hello 技術設定檔：

1. 尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。
1. 加入下列 hello:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. 更新`Id`toohello 相同值的`TargetClaimsExchangeId`hello 前面一節中。
1. 更新`TechnicalProfileReferenceId`toohello 識別碼 hello 技術分析您稍早建立 (ContosoProfile)。

### <a name="upload-hello-updated-extension-file"></a>上傳 hello 更新延伸模組檔案

您已完成修改 hello 延伸模組檔案。 將其儲存。 然後上傳 hello 檔案，並確保所有驗證都成功。

### <a name="update-hello-rp-file"></a>更新 hello RP 檔案

您現在需要 tooupdate hello 信賴憑證者 (rp) 檔案將會起始 hello 您剛才建立的使用者歷程：

1. 在您的工作目錄中建立一份 SignUpOrSignIn.xml，並將它重新命名 （例如，將它重新命名 tooSignUpOrSignInWithAAD.xml）。
1. 開啟 hello 新檔案並更新 hello`PolicyId`屬性`<TrustFrameworkPolicy>`包含唯一值 (例如，SignUpOrSignInWithAAD)。 <br> 這將是原則的 hello 名稱 (例如，B2C\_1A\_SignUpOrSignInWithAAD)。
1. 修改 hello`ReferenceId`屬性`<DefaultUserJourney>`hello 建立 (SignUpOrSignUsingContoso) 的新使用者旅程 toomatch hello 識別碼。
1. 儲存您的變更，並上傳 hello 檔案。

## <a name="troubleshooting"></a>疑難排解

測試 hello 剛剛上傳藉由開啟其刀鋒視窗中按的自訂原則**立即執行**。 toodiagnose 問題、 閱讀[疑難排解](active-directory-b2c-troubleshoot-custom.md)。

## <a name="next-steps"></a>後續步驟

提供意見反應太[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)。
