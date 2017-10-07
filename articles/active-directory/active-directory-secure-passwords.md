---
title: "aaaAzure AD 分層密碼安全性 |Microsoft 文件"
description: "說明 Azure AD 如何強制執行強式密碼，及保護使用者密碼免遭網路罪犯破解。"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>多層式方法 tooAzure AD 密碼安全性

本文將告訴您您的 Azure Active Directory (Azure AD) 或 Microsoft 帳戶可以依照使用者或系統管理員 tooprotect 身分的一些最佳作法。

 > [!NOTE]
 > Azure AD 系統管理員可以重設使用者密碼使用 hello 文件中的 hello 指引[Azure Active Directory 中的使用者重設 hello 密碼](active-directory-users-reset-password-azure-portal.md)。
 >
 > 使用者可以重設自己的密碼使用 hello 文件中的 hello 指引[我忘記密碼 Azure AD 說明](active-directory-passwords-update-your-own-password.md)。
 >

## <a name="password-requirements"></a>密碼需求

Azure AD 會併入 hello 遵循一般的方法 toosecuring 密碼：

* 密碼長度需求
* 密碼複雜性需求
* 一般和定期密碼到期

如需 Azure Active Directory 中重設密碼資訊，請參閱 hello 主題[Azure AD 自助式密碼重設 hello IT 專業人員](active-directory-passwords.md)。

## <a name="azure-ad-password-protections"></a>Azure AD 密碼保護

Azure AD 與 Microsoft 帳戶系統使用已知的業界 hello 方法 tooensure 安全保護的使用者和系統管理員的密碼，包括：

* 動態禁用的密碼
* 智慧型密碼鎖定

根據目前的研究的密碼管理的相關資訊，請參閱 hello 白皮書[密碼指引](http://aka.ms/passwordguidance)。

### <a name="dynamically-banned-passwords"></a>動態禁用的密碼

Azure AD 和 Microsoft 帳戶藉由動態禁用常見密碼來提供密碼保護。 hello Azure 識別碼識別身分保護小組定期分析禁止的密碼清單，防止使用者選取常使用的密碼。 此服務是使用 tooAzure AD 和 hello Microsoft 帳戶服務的客戶。

建立密碼時, 很重要的系統管理員 tooencourage 使用者 toochoose 密碼片語包含字母、 數字、 字元或單字的唯一組合。 這種方式有助於幾乎不可能 toobe 危害但方便使用者 tooremember toomake 使用者密碼。

#### <a name="password-breaches"></a>密碼漏洞

Microsoft 正在一律 toostay 前面網路罪犯的一個步驟。

hello Azure AD Identity Protection 小組持續會分析常使用的密碼。 網路罪犯也使用類似的策略 tooinform 其攻擊，例如建置[彩虹資料表](https://en.wikipedia.org/wiki/Rainbow_table)的破解密碼雜湊。

Microsoft 會持續分析[資料缺口](https://www.privacyrights.org/data-breaches)toomaintain 動態更新禁止的密碼清單中，以確保會禁止易受攻擊的密碼，才能實際威脅 tooAzure AD 客戶。 如需我們目前的安全性工作的詳細資訊，請參閱 hello [Microsoft 安全性智慧報表](https://www.microsoft.com/security/sir/default.aspx)。

### <a name="smart-password-lockout"></a>智慧型密碼鎖定

當 Azure AD 偵測到潛在的網路罪犯嘗試 toohack 到使用者密碼時，我們會鎖定 hello 智慧密碼鎖定的使用者帳戶。 Azure AD 設計 toodetermine hello 風險與特定登入工作階段相關聯。 然後使用 hello 最新的安全性資料，我們套用鎖定語意 toostop e-security 威脅。

如果使用者已鎖定超出 Azure AD，其螢幕看起來類似 toohello 遵循的其中一個：

  ![Azure AD 遭到鎖定](./media/active-directory-secure-passwords/locked-out-azuread.png)

針對其他 Microsoft 帳戶，其螢幕看起來類似 toohello 遵循的其中一個：

  ![Microsoft 帳戶遭到鎖定](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

如需 Azure Active Directory 中重設密碼資訊，請參閱 hello 主題[Azure AD 自助式密碼重設 hello IT 專業人員](active-directory-passwords.md)。

  >[!NOTE]
  >如果您是 Azure AD 管理員，您可能會想 toouse[用 Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid 讓使用者完全建立傳統的密碼。
  >

## <a name="next-steps"></a>後續步驟

* [如何 tooupdate 您自己的密碼](active-directory-passwords-update-your-own-password.md)
* [hello Azure 身分識別管理的基本概念](fundamentals-identity.md)
* [密碼重設活動報告](active-directory-passwords-reporting.md)


