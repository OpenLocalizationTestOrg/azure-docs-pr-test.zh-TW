---
title: "Azure Active Directory B2B 共同作業使用者的 aaaProperties |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的使用者屬性可進行設定"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Azure Active Directory B2B 共同作業使用者的屬性

Azure Active Directory (Azure AD) 企業對企業 (B2B) 共同作業使用者是 UserType = [來賓] 的使用者。 此 guest 使用者通常是來自夥伴組織，且 hello 邀請目錄中，預設的權限有限。

根據 hello 邀請組織的需求，Azure AD B2B 共同作業的使用者可以是其中一種 hello 下列帳戶狀態：

- 狀態 1： 位於外部的 Azure AD 執行個體，並代表 hello 邀請組織中有 guest 使用者。 在此情況下，hello B2B 使用者登入使用所屬 toohello 受邀租用戶的 Azure AD 帳戶。 如果 hello 夥伴組織不使用 Azure AD，仍會建立在 Azure AD 中的 hello guest 使用者。 hello 需求是，它們兌換邀請其 Azure AD 會驗證電子郵件地址。 此排列也稱為 Just-In-Time (JIT) 租用或「熱門」租用。

- 狀態 2： 主目錄中的 Microsoft 帳戶，並代表 hello 主機組織中有 guest 使用者。 在此情況下，hello guest 使用者帳戶登入 Microsoft。 hello 受邀使用者的社交身分識別 (google.com 或類似)，提供兌換這不 Microsoft 帳戶，會建立為 Microsoft 帳戶。

- 狀態 3: Hello 主機組織的內部部署 Active Directory 中的主目錄和同步處理與 hello 主機組織的 Azure AD。 在此版本中，您必須使用 PowerShell toomanually 變更 hello UserType 這類使用者的 hello 雲端中。

- 狀態 4： 位於主機組織的 Azure AD 與 UserType = 客體和主機 hello 的組織管理的認證。

  ![顯示 hello 邀請者縮寫](media/active-directory-b2b-user-properties/redemption-diagram.png)


現在，讓我們來看看狀態 1 中 Azure AD B2B 共同作業使用者在 Azure AD 中的外觀。

### <a name="before-invitation-redemption"></a>邀請兌換之前

![優惠兌換之前](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>邀請兌換之後

![優惠兌換之後](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Hello Azure AD B2B 共同作業的使用者之索引鍵屬性
### <a name="usertype"></a>UserType
這個屬性表示 hello 使用者 toohello 主機租用戶的 hello 關聯的性。 此屬性可以包含兩個值：
- 成員： 這個值表示 hello 主機組織的員工和 hello 公司的薪資中的使用者。 比方說，這位使用者必須要有 toohave 存取僅限 toointernal 站台。 這位使用者就不會被認為是外部共同作業人員。

- 客體： 這個值表示不會被視為內部 toohello 公司，例如外部共同作業者、 夥伴、 客戶或類似使用者的使用者。 這類使用者不是預期的 tooreceive 總裁的內部備忘或接收公司的好處，例如。

  > [!NOTE]
  > hello UserType 都有任何關聯 toohow hello 使用者登入時，hello 目錄角色的 hello 使用者等等。 這個屬性只是指出 hello 使用者的關聯性 toohello 主機組織，並允許 hello 組織 tooenforce 原則相依於這個屬性。

### <a name="source"></a>來源
這個屬性會指出 hello 使用者如何登入。

- 受邀使用者︰此使用者已受邀請，但尚未兌換邀請。

- 外部的 Active Directory： 此使用者位於外部組織，並使用所屬 toohello 另一個組織的 Azure AD 帳戶驗證。 這種類型的登入對應 tooState 1。

- Microsoft 帳戶：此使用者位於 Microsoft 帳戶，並使用 Microsoft 帳戶進行驗證。 這種類型的登入對應 tooState 2。

- Windows Server Active Directory： 此使用者已登入從所屬 toothis 組織在內部部署 Active Directory。 這種類型的登入對應 tooState 3。

- Azure Active Directory： 使用所屬 toothis 組織的 Azure AD 帳戶來驗證此使用者。 這種類型的登入對應 tooState 4。
  > [!NOTE]
  > Source 和 UserType 是獨立的屬性。 Source 的值不代表特定的 UserType 值。

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Azure AD B2B 使用者是否可新增為成員而非來賓？
一般而言，Azure AD B2B 使用者和來賓使用者的意義相同。 因此，Azure AD B2B 共同作業使用者依預設是新增為具有 UserType = [來賓] 的使用者。 不過，在某些情況下，hello 夥伴組織會也屬於較大的組織 toowhich hello 主機組織的成員。 如果是這樣，hello 主機組織可能會想 tootreat hello 做為成員，而不是客體的夥伴組織中的使用者。 使用 hello Azure AD B2B 邀請管理員 Api tooadd 或邀請 hello 夥伴組織 toohello 主機組織成員身分的使用者。

## <a name="filter-for-guest-users-in-hello-directory"></a>Guest 使用者在 hello 目錄中的篩選條件

![篩選來賓使用者](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>轉換 UserType
目前，它可能會從成員 tooGuest，反之亦然使用者 tooconvert UserType 使用 PowerShell。 不過，hello UserType 屬性應該 toorepresent hello 使用者的關聯性 toohello 組織。 因此，只有在 hello 使用者 toohello 組織的 hello 性關聯有變化，應該變更 hello 這個屬性的值。 如果 hello 的 hello 使用者的關聯性變更時，應該問題，例如是否應該變更 hello 使用者主要名稱 (UPN)，處理？ Hello 使用者應該繼續 toohave 存取 toohello 相同的資源嗎？ 是否應指派信箱？ 因此，我們不建議使用 PowerShell 為不可部分完成的活動變更 hello UserType。 此外，為免使用 PowerShell 讓這個屬性成為不可變屬性，我們不建議採用此值的相依性。

## <a name="remove-guest-user-limitations"></a>移除來賓使用者限制
可能有您希望 toogive 您來賓使用者的權限的情況。 您可以新增來賓使用者 tooany 角色並甚至移除 hello 預設來賓使用者限制中的 hello 目錄 toogive 相同權限做為成員的使用者 hello。

如此，來賓使用者 hello 公司目錄中的獲得便關閉 hello 預設來賓使用者限制可能 tooturn hello 相同成員使用者權限。

![移除來賓使用者限制](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [新增 B2B 共同作業使用者 tooa 角色](active-directory-b2b-add-guest-to-role.md)
* [委派 B2B 共同作業邀請](active-directory-b2b-delegate-invitations.md)
* [B2B 共同作業使用者稽核和報告](active-directory-b2b-auditing-and-reporting.md)
* [動態群組與 B2B 共同作業](active-directory-b2b-dynamic-groups.md)
* [B2B 共同作業程式碼與 PowerShell 範例](active-directory-b2b-code-samples.md)
* [設定適用於 B2B 共同作業的 SaaS 應用程式](active-directory-b2b-configure-saas-apps.md)
* [B2B 共同作業使用者權杖](active-directory-b2b-user-token.md)
* [B2B 共同作業使用者宣告對應](active-directory-b2b-claims-mapping.md)
* [Office 365 外部共用](active-directory-b2b-o365-external-user.md)
* [B2B 共同作業目前的限制](active-directory-b2b-current-limitations.md)
