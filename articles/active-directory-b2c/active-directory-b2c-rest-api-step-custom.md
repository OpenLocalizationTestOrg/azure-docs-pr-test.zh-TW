---
title: "Azure Active Directory B2C：使用 REST API 宣告交換作為協調流程步驟 | Microsoft Docs"
description: "關於已與 API 整合之 Azure Active Directory B2C 自訂原則的主題"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟

hello 識別體驗架構 (IEF) 構成 Azure Active Directory B2C (Azure AD B2C) 可讓 hello 身分識別開發人員 toointegrate 與 rest 式 API，在使用者之旅互動。  

在本逐步解說 hello 最後，將無法 toocreate 互動 RESTful 服務的 Azure AD B2C 使用者旅程。

hello IEF 宣告中傳送資料，並接收回宣告中的資料。 hello REST API 宣告 exchange:

- 可以設計成協調流程步驟。
- 可以觸發外部動作。 例如，它可以在外部資料庫中記錄一個事件。
- 可以是使用的 toofetch 的值，然後將它儲存在 hello 使用者資料庫。

您可以使用收到 hello 宣告稍後 toochange hello 流程的執行。

您也可以設計 hello 互動身分驗證設定檔。 如需詳細資訊，請參閱[逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為使用者輸入的驗證](active-directory-b2c-rest-api-validation-custom.md)。

當使用者執行設定檔編輯時，我們想要則 hello 案例：

1. 查閱外部系統中的 hello 使用者。
2. 收到 hello 縣 （市） 在已註冊該使用者。
3. 傳回當做宣告該屬性 toohello 應用程式。

## <a name="prerequisites"></a>必要條件

- Sign-up/登入中, 所述的本機帳戶的 Azure AD B2C 租用戶設定 toocomplete[入門](active-directory-b2c-get-started-custom.md)。
- 使用 REST API 端點 toointeract。 本逐步解說使用簡單的 Azure 函式應用程式 Webhook 作為範例。
- *建議*： 完整 hello [REST API 宣告交換逐步解說中的為每個驗證步驟](active-directory-b2c-rest-api-validation-custom.md)。

## <a name="step-1-prepare-hello-rest-api-function"></a>步驟 1： 準備 hello REST API 函式

> [!NOTE]
> 安裝程式的 REST API 函式是在這篇文章 hello 範圍之外。 [Azure 函數](https://docs.microsoft.com/azure/azure-functions/functions-reference)toocreate hello 雲端中的 rest 式服務提供絕佳的工具組。

我們已將接收的宣告稱為 Azure 函式設定`email`，然後傳回 hello 宣告和`city`hello 分派值是`Redmond`。 hello 範例 Azure 函式位於[GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)。

hello `userMessage` hello Azure 函式傳回的宣告是選擇性的在此內容中，而且 hello IEF 將會忽略它。 您可以使用它的訊息傳遞 toohello 應用程式，並稍後所述 toohello 使用者。

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Azure 的函式應用程式可容易 tooget hello 函式 URL，包括 hello 識別碼 hello 特定函式。 在此情況下，hello URL 是： https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==。 您可以使用它來測試。

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>步驟 2： 設定 hello RESTful API 宣告交換為技術 TrustFrameworExtensions.xml 檔案中設定檔

技術的設定檔是 hello 的 hello exchange 以 hello RESTful 服務所需的完整設定。 開啟 hello TrustFrameworkExtensions.xml 檔案並加入下列 XML 程式碼片段 hello hello`<ClaimsProvider>`項目。

> [!NOTE]
> 在下列 XML，RESTful 的提供者的 hello`Version=1.0.0.0`即稱為 hello 通訊協定。 將其視為與 hello 外部服務互動的 hello 函式。 <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

hello`<InputClaims>`項目會定義會將傳送嗨 IEF toohello REST 服務的 hello 宣告。 在此範例中，hello hello 宣告的內容`givenName`toohello REST 服務以傳送 hello 宣告`email`。  

hello`<OutputClaims>`項目會定義 hello 宣告該 hello IEF 就會預期收到來自 hello REST 服務。 Hello 數目所接收的宣告，不論 hello IEF 將會使用僅限於識別這裡。 在此範例中，宣告收到`city`將對應的 tooan IEF 宣告呼叫`city`。

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>步驟 3： 加入 hello 新宣告`city`toohello TrustFrameworkExtensions.xml 檔案結構描述

hello 宣告`city`尚未定義任何地方我們的結構描述中。 因此，加入在 hello 項目內定義`<BuildingBlocks>`。 您可以找到這個 hello hello TrustFrameworkExtensions.xml 檔案開頭處的項目。

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>步驟 4： 為協調流程中的步驟設定檔編輯使用者旅程中 TrustFrameworkExtensions.xml 包含 hello REST 服務宣告交換

將步驟加入 toohello 設定檔編輯使用者之旅，hello 使用者之後，驗證 （協調流程的步驟 1-4 hello 下列 XML 中），且 hello 使用者提供更新的 hello 設定檔資訊 （步驟 5）。

> [!NOTE]
> 有許多的使用案例，其中 hello REST API 呼叫可用來當作協調流程步驟。 在協調流程的步驟中，它可用來當作更新 tooan 外部系統使用者順利完成的工作，像是第一次註冊之後，或為設定檔更新 tookeep 資訊同步。 在此情況下，它是使用的 tooaugment hello 資訊之後，編輯 hello 設定檔中提供 toohello 應用程式。

複製 hello 設定檔編輯使用者之旅 XML 程式碼從 hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml 檔案內 hello`<UserJourneys>`項目。 請在 步驟 6 hello 修改。

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> 如果 hello 順序不符合您的版本，請確定您以 hello 步驟 hello 之前插入 hello 程式碼`ClaimsExchange`類型`SendClaims`。

hello hello 使用者作業的最終 XML 看起來應該像這樣：

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>步驟 5： 加入 hello 宣告`city`tooyour 信賴憑證者的合作對象原則檔案，因此會傳送 hello 宣告 tooyour 應用程式

編輯您 ProfileEdit.xml 信賴憑證者的合作對象 (RP) 檔和修改 hello`<TechnicalProfile Id="PolicyProfile">`元素 tooadd hello 下列： `<OutputClaim ClaimTypeReferenceId="city" />`。

您將加入 hello 新宣告之後，hello 技術設定檔看起來像這樣：

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>步驟 6：上傳您的變更和測試

覆寫 hello 現有 hello 原則版本。

1.  (選擇性:)儲存 hello 現有版本 （下載） 的延伸模組檔案後再繼續。 tookeep hello 初始複雜性低，我們建議您不要上傳多個版本的 hello 延伸模組檔案。
2.  (選擇性:)藉由變更命名新版 hello 原則編輯檔案的 hello 原則識別碼 hello `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`。
3.  上傳 hello 延伸模組檔案。
4.  Hello 原則編輯 RP 檔案上傳。
5.  使用**立即執行**tootest hello 原則。 Hello IEF 檢閱 hello 語彙基元傳回 toohello 應用程式。

如果所有項目已正確設定時，hello 權杖會包含 hello 新宣告`city`，hello 值`Redmond`。

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>後續步驟

[使用 REST API 來作為驗證步驟](active-directory-b2c-rest-api-validation-custom.md)

[修改 hello 設定檔編輯 toogather 的其他資訊從您的使用者](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
