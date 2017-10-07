---
title: "Azure Active Directory B2C： 了解 hello 入門組件的自訂原則 |Microsoft 文件"
description: "Azure Active Directory B2C 自訂原則的主題"
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
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>了解 hello hello Azure AD B2C 自訂原則入門組件的自訂原則

此區段會列出所有 hello 核心項目所隨附 hello hello B2C_1A_base 原則**入門套件**和，可用來撰寫您自己的原則，透過的 hello hello 繼承*B2C_1A_base_擴充功能原則*。

因此，它多特別著重於 hello 已經定義過了宣告類型、 宣告轉換、 內容定義、 宣告提供者與他們技術下列設定檔，而 hello 核心使用者皆。

> [!IMPORTANT]
> Microsoft 不做任何明示明示或默示，以下提供尊重 toohello 資訊。 任何時候 (GA 當下、之前或之後) 皆有可能導入變更。

您自己的原則和 hello B2C_1A_base_extensions 原則可以覆寫這些定義，並視需要提供額外的擴充此父原則。

hello hello 核心項目*B2C_1A_base 原則*是宣告類型、 宣告轉換和內容的定義。 這些項目可以很容易遭受 hello 與您自己以及的原則中所參考的 toobe *B2C_1A_base_extensions 原則*。

## <a name="claims-schemas"></a>宣告結構描述

此宣告結構描述分為三個部分︰

1.  第一個區段會列出所需的 hello 使用者皆 toowork 正確 hello 最小宣告。
2.  第二個區段列出 hello 所需的查詢字串參數的宣告，和其他特殊參數 toobe 傳遞 tooother 宣告提供者，特別是 login.microsoftonline.com 進行驗證。 **請勿修改這些宣告**。
3.  和第三個區段會列出任何額外的選擇性宣告可收集來自 hello 使用者最後 hello 目錄中儲存並登入期間傳送權杖中。 本節中，可以加入新宣告型別 toobe hello 使用者從收集及/或傳送嗨權杖中。

> [!IMPORTANT]
> hello 宣告結構描述包含某些宣告，例如密碼和使用者名稱的限制。 hello 信任架構 (TF) 原則會視為其他宣告提供者中的 Azure AD 和其所有的限制會在 hello premium 原則和模型化。 原則可以修改的 tooadd 更多的限制，或其他宣告提供者用於認證存放裝置，將有它自己的限制。

hello 可用宣告類型如下所示。

### <a name="claims-that-are-required-for-hello-user-journeys"></a>所需的 hello 使用者皆宣告

hello 下列宣告所需的使用者皆 toowork 正確：

| 宣告類型 | 說明 |
|-------------|-------------|
| UserId | 使用者名稱 |
| signInName | 登入名稱 |
| tenantId | 在 Azure AD B2C Premium hello 使用者物件的租用戶識別碼 (ID) |
| objectId | 在 Azure AD B2C Premium hello 使用者物件的物件識別碼 (ID) |
| *password* | 密碼 |
| newPassword | |
| reenterPassword | |
| passwordPolicies | Azure AD B2C Premium toodetermine 密碼強度、 到期和其他內容所使用的密碼原則。 |
| *sub* | |
| alternativeSecurityId | |
| identityProvider | |
| displayName | |
| strongAuthenticationPhoneNumber | 使用者的電話號碼 |
| Verified.strongAuthenticationPhoneNumber | |
| email | 可以使用的 toocontact hello 使用者的電子郵件地址 |
| signInNamesInfo.emailAddress | 可用在 toosign hello 使用者的電子郵件地址。 |
| otherMails | 可以使用的 toocontact hello 使用者的電子郵件地址 |
| userPrincipalName | Hello Azure AD B2C Premium 中所儲存的使用者名稱 |
| upnUserName | 用來建立使用者主體名稱的使用者名稱 |
| mailNickName | 使用者的郵件 nick 名稱儲存在 Azure AD B2C Premium hello |
| newUser | |
| executed-SelfAsserted-Input | 指定屬性是否已收集來自 hello 使用者宣告 |
| executed-PhoneFactor-Input | 指定新的電話號碼是否收集來自 hello 使用者宣告 |
| authenticationSource | 指定是否 hello 使用者已驗證在社交身分識別提供者、 login.microsoftonline.com 或本機帳戶 |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>查詢字串參數和其他特殊參數所需的宣告

hello 下列宣告是特殊的參數 （包括某些查詢字串參數） tooother 宣告提供者上的必要的 toopass:

| 宣告類型 | 說明 |
|-------------|-------------|
| nux | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| nca | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| prompt | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| mkt | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| lc | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| grant_type | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| scope | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| client_id | 特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數 |
| objectIdFromSession | 已擷取 hello 預設工作階段管理提供者 tooindicate hello 物件識別碼，所提供的參數，從 SSO 工作階段 |
| isActiveMFASession | 參數所提供 hello MFA 工作階段管理 tooindicate hello 使用者具有作用中的 MFA 工作階段 |

### <a name="additional-optional-claims-that-can-be-collected"></a>其他可以收集的 (選擇性) 宣告

hello 下列宣告會從 hello 使用者收集的其他宣告儲存在 hello 目錄中，並傳送嗨權杖中。 如之前所述，新增額外宣告可以是 toothis 清單。

| 宣告類型 | 說明 |
|-------------|-------------|
| givenName | 使用者的名字 (也就是第一個名字) |
| surname | 使用者的姓氏 |
| Extension_picture | 使用者的社交網站相片 |

## <a name="claim-transformations"></a>宣告轉換

hello 可用宣告轉換如下所示。

| 宣告轉換 | 說明 |
|----------------------|-------------|
| CreateOtherMailsFromEmail | |
| CreateRandomUPNUserName | |
| CreateUserPrincipalName | |
| CreateSubjectClaimFromObjectID | |
| CreateSubjectClaimFromAlternativeSecurityId | |
| CreateAlternativeSecurityId | |

## <a name="content-definitions"></a>內容定義

本章節描述 hello hello 中已經宣告過的內容定義*B2C_1A_base*原則。 這些內容的定義是很容易遭受 toobe 參考、 覆寫時，及/或擴充視需要在您的原則也如同 hello *B2C_1A_base_extensions*原則。

| 宣告提供者 | 說明 |
|-----------------|-------------|
| *Facebook* | |
| 本機帳戶登入 | |
| PhoneFactor | |
| *Azure Active Directory* | |
| 自我判斷提示 | |
| 本機帳戶 | |
| *工作階段管理* | |
| Trustframework 原則引擎 | |
| TechnicalProfiles | |
| 權杖簽發者 | |

## <a name="technical-profiles"></a>技術設定檔

本章節描述 hello 技術設定檔已宣告每個宣告提供者在 hello *B2C_1A_base*原則。 這些技術的設定檔是很容易遭受 toobe 進一步參考、 覆寫時，及/或擴充視需要在您的原則也如同 hello *B2C_1A_base_extensions*原則。

### <a name="technical-profiles-for-facebook"></a>Facebook 的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| Facebook-OAUTH | |

### <a name="technical-profiles-for-local-account-signin"></a>本機帳戶登入的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| Login-NonInteractive | |

### <a name="technical-profiles-for-phone-factor"></a>PhoneFactor 的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| PhoneFactor-Input | |
| PhoneFactor-InputOrVerify | |
| PhoneFactor-Verify | |

### <a name="technical-profiles-for-azure-active-directory"></a>Azure Active Directory 的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| AAD-Common | 所包含的設定檔技術 hello 其他 AAD xxx 技術的設定檔 |
| AAD-UserWriteUsingAlternativeSecurityId | 社交登入的技術設定檔 |
| AAD-UserReadUsingAlternativeSecurityId | 社交登入的技術設定檔 |
| AAD-UserReadUsingAlternativeSecurityId-NoError | 社交登入的技術設定檔 |
| AAD-UserWritePasswordUsingLogonEmail | 本機帳戶的技術設定檔 |
| AAD-UserReadUsingEmailAddress | 本機帳戶的技術設定檔 |
| AAD-UserWriteProfileUsingObjectId | 可供使用 objectId 來更新使用者記錄的技術設定檔 |
| AAD-UserWritePhoneNumberUsingObjectId | 可供使用 objectId 來更新使用者記錄的技術設定檔 |
| AAD-UserWritePasswordUsingObjectId | 可供使用 objectId 來更新使用者記錄的技術設定檔 |
| AAD-UserReadUsingObjectId | 技術的設定檔是使用的 tooread 後，資料會驗證使用者 |

### <a name="technical-profiles-for-self-asserted"></a>自我判斷提示的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| SelfAsserted-Social | |
| SelfAsserted-ProfileUpdate | |

### <a name="technical-profiles-for-local-account"></a>本機帳戶的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| LocalAccountSignUpWithLogonEmail | |

### <a name="technical-profiles-for-session-management"></a>工作階段管理的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| SM-Noop | |
| SM-AAD | |
| SM-SocialSignup | 設定檔名稱是正在登之間使用的 toodisambiguate AAD 工作階段設定和登入 |
| SM-SocialLogin | |
| SM-MFA | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Trustframework 原則引擎 TechnicalProfiles 的技術設定檔

目前，沒有技術的設定檔定義 hello **Trustframework 原則引擎 TechnicalProfiles**宣告提供者。

### <a name="technical-profiles-for-token-issuer"></a>權杖簽發者的技術設定檔

| 技術設定檔 | 說明 |
|-------------------|-------------|
| JwtIssuer | |

## <a name="user-journeys"></a>使用者旅程

本章節描述 hello hello 中已經宣告過的使用者皆*B2C_1A_base*原則。 這些使用者皆會受到 toobe 進一步參考、 覆寫時，及/或擴充視需要在您的原則也如同 hello *B2C_1A_base_extensions*原則。

| 使用者旅程 | 說明 |
|--------------|-------------|
| SignUp | |
| SignIn | |
| SignUpOrSignIn | |
| EditProfile | |
| PasswordReset | |
