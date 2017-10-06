---
title: "Azure Active Directory B2C：使用自訂原則來管理 SSO 和權杖自訂 | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C：使用自訂原則來管理 SSO 和權杖自訂
使用自訂原則，提供您透過內建原則 hello 相同控制您的語彙基元、 工作階段和單一登入 (SSO) 組態。  toolearn 存在每個設定為何，請參閱 hello 文件[這裡](#active-directory-b2c-token-session-sso)。

## <a name="token-lifetimes-and-claims-configuration"></a>權杖存留期和宣告組態
toochange hello 設定後權杖的存留期間，您需要 tooadd`<ClaimsProviders>`元素要 tooimpact hello 信賴憑證者合作對象檔案中的 hello 原則。  hello`<ClaimsProviders>`元素是子系的 hello `<TrustFrameworkPolicy>`。  內部，您將需要 tooput hello 資訊會影響您的權杖存留期。  hello XML 看起來像這樣：

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

**存取權杖存留期**hello 的存取權杖存留期可以透過修改 hello hello 內的值變更`<Item>`以 hello Key ="token_lifetime_secs 」，以秒為單位。  hello 中內建的預設值為 3600 秒 （60 分鐘）。

**識別碼權杖存留期**hello 識別碼權杖存留期可以透過修改 hello hello 內的值變更`<Item>`以 hello Key ="id_token_lifetime_secs 」，以秒為單位。  hello 中內建的預設值為 3600 秒 （60 分鐘）。

**重新整理權杖存留期**要變更 hello 重新整理權杖存留期，請修改內 hello 的 hello 值`<Item>`以 hello Key ="refresh_token_lifetime_secs 」，以秒為單位。  hello 中內建的預設值為 1209600 秒 （14 天）。

**重新整理權杖的滑動視窗存留期**如果您想要 tooset 滑動視窗存留期 tooyour 重新整理權杖，修改內 hello 值`<Item>`以 hello Key ="rolling_refresh_token_lifetime_secs 」，以秒為單位。  hello 中內建的預設值是 7776000 （90 天）。  如果您不想 tooenfore 滑動視窗存留期，取代與這行：
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**簽發者 (iss) 宣告**如果您想 toochange hello 簽發者 (iss) 宣告，請修改 hello 值內 hello`<Item>`以 hello 索引鍵 ="IssuanceClaimPattern"。  hello 適用值為`AuthorityAndTenantGuid`和`AuthorityWithTfp`。

**設定宣告代表原則識別碼**hello 選項將此值設定為 TFP （信任架構原則） 和 ACR （驗證內容參考）。  
我們建議此 tooTFP，toodo 將此設定，請確定 hello`<Item>`以 hello Key ="AuthenticationContextReferenceClaimPattern 」 存在，而且是 hello 值`None`。
在您的 `<OutputClaims>` 項目中，新增這個元素︰
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
ACR，移除 hello`<Item>`以 hello Key ="AuthenticationContextReferenceClaimPattern"。

**主體 (sub) 宣告**時，此選項預設 tooObjectID，如果您想要 tooswitch 這太`Not Supported`，請勿遵循 hello:

換掉此行 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
改用這行︰
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>工作階段行為和 SSO
toochange 您的工作階段行為和 SSO 組態，您需要 tooadd `<UserJourneyBehaviors>` hello 內的項目`<RelyingParty>`項目。  hello`<UserJourneyBehaviors>`項目必須緊接在 hello `<DefaultUserJourney>`。  hello 內您`<UserJourneyBehavors>`項目應該看起來像這樣：

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**單一登入 (SSO) 組態**toochange hello 單一登入設定中，您需要 toomodify hello 值`<SingleSignOn>`。  hello 適用值為`Tenant`， `Application`，`Policy`和`Disabled`。 

**Web 應用程式工作階段存留期 （分鐘）** toochange hello hello web 應用程式工作階段存留期，您需要的 hello toomodify 值`<SessionExpiryInSeconds>`項目。  內建的原則中的 hello 預設值為 86400 秒 （1440 分鐘）。

**Web 應用程式工作階段逾時**toochange hello web 應用程式工作階段逾時，您需要 toomodify hello 值`<SessionExpiryType>`。  hello 適用值為`Absolute`和`Rolling`。
