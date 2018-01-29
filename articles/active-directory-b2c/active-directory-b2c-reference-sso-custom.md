---
title: "使用自訂原則的 SSO 工作階段管理 - Azure AD B2C | Microsoft Docs"
description: "了解如何在 Azure AD B2C 中使用自訂原則管理 SSO 工作階段。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: mtillman
editor: parakhj
ms.assetid: 809f6000-2e52-43e4-995d-089d85747e1f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2017
ms.author: parja
ms.openlocfilehash: 676b277ae3fbf4554838eee70c5d3e2d8e12c33d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="azure-ad-b2c-single-sign-on-sso-session-management"></a>Azure AD B2C：單一登入 (SSO) 工作階段管理

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Azure AD B2C 可讓系統管理員在已驗證使用者之後控制 Azure AD B2C 與使用者的互動方式。 這是透過 SSO 工作階段管理完成。 例如，系統管理員可以控制是否顯示選取的身分識別提供者，或是否需要再輸入一次本機帳戶詳細資料。 本文說明如何設定 Azure AD B2C 的 SSO 設定。

## <a name="overview"></a>概觀

SSO 工作階段管理有兩個部分。 第一個是處理使用者與 Azure AD B2C 的直接互動，另一個則是處理使用者與外部合作對象 (例如 Facebook) 的互動。 Azure AD B2C 不會覆寫或略過外部合作對象可能保留的 SSO 工作階段。 會「記住」透過 Azure AD B2C 到達外部合作對象的路徑，這樣就不需要重新提示使用者選取其社交或企業身分識別提供者。 最終 SSO 決策是由外部合作對象所決定。

## <a name="how-does-it-work"></a>運作方式

SSO 工作階段管理使用相同的語意，作為自訂原則中的其他任何技術設定檔。 執行協調流程步驟時，會查詢與步驟建立關聯的技術設定檔是否有 `UseTechnicalProfileForSessionManagement` 參考。 如果有的話，接著會檢查參考的 SSO 工作階段提供者，以查看使用者是否為工作階段參與者。 如果是這樣，則會使用 SSO 工作階段提供者來重新擴展工作階段。 同樣地，執行協調流程步驟完成時，如果已指定 SSO 工作階段提供者，則會使用提供者來將資訊儲存在工作階段中。

Azure AD B2C 已定義許多可使用的 SSO 工作階段提供者：

* NoopSSOSessionProvider
* DefaultSSOSessionProvider
* ExternalLoginSSOSessionProvider
* SamlSSOSessionProvider

SSO 管理類別是使用技術設定檔的 `<UseTechnicalProfileForSessionManagement ReferenceId=“{ID}" />` 項目所指定。

### <a name="noopssosessionprovider"></a>NoopSSOSessionProvider

顧名思議，此提供者不會執行任何作業。 此提供者可以用於隱藏特定技術設定檔的 SSO 行為。

### <a name="defaultssosessionprovider"></a>DefaultSSOSessionProvider

此提供者可以用於儲存工作階段中的宣告。 此提供者通常是在用於管理本機帳戶的技術設定檔中進行參照。 

```XML
<TechnicalProfile Id="SM-AAD">
    <DisplayName>Session Mananagement Provider</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.SSO.DefaultSSOSessionProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <PersistedClaims>
        <PersistedClaim ClaimTypeReferenceId="objectId" />
        <PersistedClaim ClaimTypeReferenceId="newUser" />
        <PersistedClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" />
    </PersistedClaims>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="objectIdFromSession" DefaultValue="true" />
    </OutputClaims>
</TechnicalProfile>
```

若要在工作階段中新增宣告，請使用技術設定檔的 `<PersistedClaims>` 項目。 使用提供者重新擴展工作階段時，會將持續性的宣告新增至宣告包。 `<OutputClaims>` 用來從工作階段中擷取宣告。

### <a name="externalloginssosessionprovider"></a>ExternalLoginSSOSessionProvider

此提供者用來隱藏「選擇身分識別提供者」畫面。 它通常是在針對外部身分識別提供者 (例如 Facebook) 所設定的技術設定檔中所參照。 

```XML
<TechnicalProfile Id="SM-SocialLogin">
    <DisplayName>Session Mananagement Provider</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.SSO.ExternalLoginSSOSessionProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</TechnicalProfile>
```

### <a name="samlssosessionprovider"></a>SamlSSOSessionProvider

此提供者用於管理應用程式之間的 Azure AD B2C SAML 工作階段，以及外部 SAML 身分識別提供者。

```XML
<TechnicalProfile Id="SM-Reflector-SAML">
    <DisplayName>Session Management Provider</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.SSO.SamlSSOSessionProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
        <Item Key="IncludeSessionIndex">false</Item>
        <Item Key="RegisterServiceProviders">false</Item>
    </Metadata>
</TechnicalProfile>
```

技術設定檔中有兩個中繼資料項目：

| Item | 預設值 | 可能的值 | 說明
| --- | --- | --- | --- |
| IncludeSessionIndex | true | true/false | 指出應該儲存工作階段索引的提供者。 |
| RegisterServiceProviders | true | true/false | 指出提供者應該註冊所有已發行判斷提示的 SAML 服務提供者。 |

使用提供者來儲存 SAML 身分識別提供者工作階段時，上述項目應該都是 false。 使用提供者來儲存 B2C SAML 工作階段時，上述項目應該是 true，或是予以省略，因為預設值是 true。

>[!NOTE]
> SAML 工作階段登出需要 `SessionIndex` 和 `NameID` 才能完成。

## <a name="next-steps"></a>後續步驟

歡迎您提供任何意見和建議！ 如果您對本主題有任何問題，請使用標記 ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c) 張貼至 Stack Overflow。 如需功能要求，請在[意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)中票選它們。

