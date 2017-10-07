---
title: "授權指引 aaaAzure Active Directory B2B 共同作業 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業不需要 Azure AD 付費授權，但您也可以取得付費功能給 B2B 來賓使用者"
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Azure Active Directory B2B 共同作業授權指引

您可以使用 Azure AD B2B 共同作業功能 tooinvite guest 使用者到您的 Azure AD 租用戶 tooallow tooaccess Azure AD 服務以及其他資源組織中。 如果您想 tooprovide 存取 toopaid Azure AD 功能，B2B 共同作業 guest 使用者必須擁有與適當的 Azure AD 授權。 

具體而言：
* Azure AD Free 功能可供來賓使用者使用，且無需額外的授權。
* 如果您想 tooprovide 存取 toopaid Azure AD 功能 tooB2B 使用者時，您必須擁有足夠授權 toosupport 這些 B2B guest 使用者。
* 邀請其他租用戶與 Azure AD 的付費授權擁有 B2B 共同作業使用的權限 tooan 額外五個 B2B 客體受邀使用者 toohello 租用戶。
* hello 客戶擁有 hello 邀請租用戶必須 hello 一個 toodetermine 多少 B2B 共同作業的使用者需要支付 Azure AD 功能。 付費型 Azure AD 的 hello 根據您要為 guest 使用者，您必須擁有足夠的 Azure AD 功能支付授權 toocover B2B 共同作業的使用者 hello 相同 5:1 比率。

會從夥伴公司將 B2B 共同作業來賓使用者新增為使用者，而非貴組織的員工或貴企業集團中不同業務部門的員工。 B2B 來賓使用者可以使用外部認證或貴組織所擁有的認證來登入，如本文中所述。 

換句話說，B2B 授權設定不是由 hello 使用者的驗證方式但而是由 hello 使用者 tooyour 組織 hello 關聯性。 如果這些使用者並非夥伴，就會以不同的授權條款來處理。 不會考慮它們 toobe B2B 共同作業使用者供授權之用，即使其 UserType 會標示為 「 來賓 」。 它們應以一般方式獲得授權，每個使用者獲得一項授權。 這些使用者包括：
* 您的員工
* 使用外部身分識別登入的職員
* 貴企業集團中不同業務部門的員工


## <a name="licensing-examples"></a>授權範例
- 客戶想 tooinvite 100 B2B 共同作業的使用者 tooits Azure AD 租用戶。 hello 客戶指派存取管理和佈建所有使用者，但 50 位使用者也需要 MFA 和條件式存取。 此客戶購買 10 個 Azure AD Basic 授權和 10 Azure AD Premium P1 授權 toocover 這些 B2B 使用者正確。 如果 hello 客戶計畫 toouse 識別身分保護功能與 B2B 使用者，他們必須有 Azure AD Premium P2 授權 toocover hello 受邀使用者在 hello 相同 5:1 比率。
- 客戶有 10 位目前以 Azure AD「進階 P1」授權的員工。 現在，他們會希望 tooinvite 60 B2B 使用者所有需要多重要素驗證 (MFA)。 Hello 5:1 的授權規則，hello 客戶必須有至少 12 的 Azure AD Premium P1 授權 toocover 所有 60 B2B 共同作業的使用者。 因為它們已有 10 個 Premium P1 授權的 10 個員工，有權限 tooinvite 50 B2B 使用者使用 Premium P1 功能，例如 MFA。 在此範例中，然後，他們必須購買 2 額外 Premium P1 授權 toocover hello 剩餘 10 B2B 共同作業的使用者。

> [!NOTE]
> 沒有任何方法，但 tooassign 授權直接 toohello B2B 使用者 tooenable 這些 B2B 共同作業的使用者權限。

hello 客戶擁有 hello 邀請租用戶必須 hello 一個 toodetermine 多少 B2B 共同作業的使用者需要支付 Azure AD 功能。 根據其中支付您想要為 guest 使用者的 Azure AD 功能，您必須擁有足以 Azure AD 的付費 hello 5:1 比例的授權 toocover B2B 共同作業的使用者。 

## <a name="additional-licensing-details"></a>其他授權詳細資料
- 沒有必要 tooactually 指派授權 tooB2B 使用者帳戶。 根據 hello 5:1 比率，授權會自動計算，並報告。
- 如果不是支付 Azure AD 授權存在於 hello 租用戶，每個受邀的使用者取得 hello 權限，hello Azure AD Free edition 提供。
- 如果 B2B 共同作業的使用者已經擁有付費的 Azure AD 授權從他們的組織，它們不會耗用 hello B2B 共同作業授權 hello 邀請其他租用戶的其中一個。

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>進階討論： 什麼是 hello 授權考量，當我們從 「 成員 」 使用您的應用程式開發介面 conglomerate 組織新增使用者？
B2B guest 使用者是從與 hello 主機組織夥伴組織 toowork 受邀的其中一個。 一般而言，任何其他情況都不符合 B2B 資格，即使是使用 B2B 功能也一樣。 讓我們來特別看看兩個案例：

1. 如果主辦組織使用取用者位址來邀請員工
  * 此情節不符合我們的授權原則，不建議使用。

2. 如果主辦組織從另一個集團組織新增使用者
  1. 在此情況下，hello 使用者受邀使用 B2B 應用程式開發介面，但此情況下不傳統上 B2B。 在理想情況下，我們應該有這些組織邀請 hello 其他入使用者為成員 （我們的 API 允許的）。 在此情況下，必須授權 toobe 指派 toothese 它們 tooaccess 資源 hello 邀請組織中的成員。

  2. 某些組織可能會想加入為 「 來賓 」 做為原則的其他組織的使用者 toobe tooadd hello。 這裡有兩個案例：
      * hello conglomerate 組織已使用 Azure AD 並 hello 受邀使用者授權 hello 中另一個組織： 在此情況下，我們不覺得受邀的使用者 tooneed toofollow hello 1:5 公式配置稍早在本文件中。 

      * hello conglomerate 組織未使用 Azure AD 或沒有足夠的授權： 在此情況下，請遵循的 hello 1:5 公式配置稍早在本文件中。

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [針對 Azure Active Directory B2B 共同作業問題進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory 中應用程式管理的文章索引](active-directory-apps-index.md)
