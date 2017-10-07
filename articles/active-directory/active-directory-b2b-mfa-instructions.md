---
title: "Azure Active Directory B2B 共同作業的使用者存取 aaaConditional |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的選擇性存取 tooyour 公司應用程式支援 multi-factor authentication (MFA)"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>B2B 共同作業使用者的條件式存取

## <a name="multi-factor-authentication-for-b2b-users"></a>B2B 使用者的多重要素驗證
在使用 Azure AD B2B 共同作業的情況下，組織會為 B2B 使用者強制執行 Multi-Factor Authentication (MFA) 原則。 這些原則可以強制執行在 hello 租用戶、 應用程式或個別使用者層級 hello 啟用這兩項全職員工和 hello 組織成員的方式相同。 在 hello 資源組織會強制執行 MFA 原則。

範例：
1. 公司 A 中的系統管理員或資訊工作者邀請使用者從公司 B tooan 應用程式*Foo*公司 a。
2. 應用程式*Foo*公司 A 是設定的 toorequire MFA 上存取。
3. 當從公司 B 的 hello 使用者嘗試 tooaccess 應用程式*Foo*在 hello 公司租用戶，它們是要求 toocomplete MFA 挑戰。
4. hello 使用者可以設定其 MFA 搭配公司，並選擇其 MFA 選項。
5. 此案例對任何身分識別 (例如 Azure AD 或 MSA，若公司 B 的使用者使用社交識別碼來驗證) 都有效
6. 公司 A 必須有足夠支援 MFA 的 Azure AD Premium 授權。 hello 使用者從公司 B 會消耗公司 a 本授權條款

hello 邀請其他租用戶負責一律為 MFA hello 夥伴組織，使用者即使 hello 夥伴組織具有 MFA 功能。

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>為 B2B 共同作業使用者設定 MFA
如何在 toodiscover 如何輕鬆是 tooset mfa B2B 共同作業的使用者，請參閱下列視訊 hello:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>方案兌換的 B2B 使用者 MFA 體驗
請參閱下列動畫 toosee hello 兌換經驗 hello:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>B2B 共同作業使用者的 MFA 重設
目前，hello 系統管理員可以要求 B2B 共同作業的使用者 tooproof 向上一次只能藉由使用下列 PowerShell 指令程式的 hello:

1. 連接 tooAzure AD

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. 取得具有證明方法的所有使用者

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  下列是一個範例：

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. 一次重設特定使用者 toorequire hello B2B 共同作業使用者 tooset 提升方法的 hello MFA 方法。 範例：

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>我們要為什麼在 hello 資源的租用戶執行 MFA？

在 hello 目前版本中，MFA 一定是在 hello 資源的租用戶，如可預測性的原因。 例如，假設 Contoso 使用者 (Sally) 是受邀的 tooFabrikam 並 Fabrikam B2B 使用者啟用 MFA。

如果 Contoso 啟用 App1 但不是 App2 的 MFA 原則，然後如果我們看一下 hello Contoso MFA 宣告在 hello 權杖中，我們可能會看到下列問題的 hello:

* 第 1 天：使用者有 Contoso 的 MFA 並存取 App1，Fabrikam 不顯示其他 MFA 提示。

* 第 2 天： hello 使用者存取應用程式 2，在 Contoso，因此，現在存取 Fabrikam 時，它們必須那里註冊 MFA。

此程序可能會造成混淆，並可能導致 toodrop 中登入完成。

此外，即使 Contoso 的 MFA 功能，它不一定 hello 案例 hello Fabrikam 會信任 hello Contoso MFA 原則。

最後，資源租用戶 MFA 也適用於 MSA 和社交識別碼，以及未設定 MFA 的合作夥伴組織。

因此，MFA B2B 使用者 hello 建議是 tooalways hello 邀請租用戶中要求使用 MFA。 這項需求可能會導致 toodouble MFA，在某些情況下，但存取 hello 邀請其他租用戶，每當 hello 使用者體驗是可預測： Sally 必須與 hello 邀請其他租用戶註冊 MFA。

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>B2B 使用者的裝置型、位置型及風險型條件式存取。

當 Contoso 可讓其公司資料的裝置型條件式存取原則時，未受管理 Contoso 和與 hello Contoso 裝置原則不相容的裝置將無法存取。

如果 hello B2B 使用者的裝置不是由 Contoso 管理，B2B 使用者從 hello 夥伴組織的存取權會封鎖這些原則會強制執行任何內容中。 不過，Contoso 可以建立排除清單包含特定的夥伴使用者 tooexclude 從 hello 裝置型條件式存取原則。

#### <a name="location-based-conditional-access-for-b2b"></a>B2B 的位置型條件式存取

以位置為基礎的條件式存取原則可以強制執行 B2B 使用者若 hello 邀請其他組織能夠 toocreate 受信任的 IP 位址範圍的定義夥伴組織。

#### <a name="risk-based-conditional-access-for-b2b"></a>B2B 的風險型條件式存取

目前，風險依據登入的原則無法套用的 tooB2B 使用者因為 hello 風險評估在 hello B2B 使用者的主要組織中執行。

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure Active Directory B2B 共同作業問題進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory 中應用程式管理的文章索引](active-directory-apps-index.md)
