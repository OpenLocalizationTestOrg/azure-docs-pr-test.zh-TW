---
title: "Active Directory 識別身分保護-aaaAzure 如何 toounblock 使用者 |Microsoft 文件"
description: "了解如何解鎖由 Azure Active Directory Identity Protection 原則所封鎖的使用者。"
services: active-directory
keywords: "Azure Active Directory Identity Protection，解鎖使用者"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory 識別身分保護-如何 toounblock 使用者
與 Azure Active Directory 識別身分保護，您可以設定符合 tooblock 使用者如果 hello 設定條件的原則。 一般而言，封鎖的使用者的連絡人說明服務人員 toobecome 解除封鎖。 本主題說明您可以執行 toounblock 封鎖的使用者的 hello 步驟。

## <a name="determine-hello-reason-for-blocking"></a>判斷有封鎖的 hello 原因
第一個步驟 toounblock 使用者，您必須已封鎖 hello 使用者，因為您的下一個步驟根據原則 toodetermine hello 型別。
使用 Azure Active Directory Identity Protection 時，使用者可能是因登入風險原則或使用者風險原則而遭封鎖。

您可以取得 hello 已封鎖的使用者的登入嘗試期間輸入 toohello 使用者 hello 對話方塊中的 hello 標題的原則類型：

| 原則 | 使用者對話方塊 |
| --- | --- |
| 登入風險 |![封鎖的登入](./media/active-directory-identityprotection-unblock-howto/02.png) |
| 使用者風險 |![封鎖的帳戶](./media/active-directory-identityprotection-unblock-howto/104.png) |

封鎖使用者的類型為︰

* 登入風險原則，也就是可疑的登入
* 使用者風險原則，也就是有風險的帳戶

## <a name="unblocking-suspicious-sign-ins"></a>解鎖可疑的登入
toounblock 可疑的登入，您有下列選項的 hello:

1. **從熟悉的位置或裝置登入** - 可疑的登入會遭封鎖通常是因為使用者嘗試從不熟悉的位置或裝置登入。 您的使用者可以快速判斷是否 hello toosign 在嘗試從熟悉的位置或裝置來封鎖原因。
2. **從原則中排除**-如果您認為，hello 目前您登入的原則設定會造成特定使用者的問題，您可以 hello 使用者排除它。 如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。
3. **停用原則**-如果您認為，原則設定會造成問題的所有使用者，您可以停用 hello 原則。 如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。

## <a name="unblocking-accounts-at-risk"></a>解鎖有風險的帳戶
toounblock 的帳戶有風險，您有下列選項的 hello:

1. **重設密碼**-您可以重設 hello 使用者的密碼。 如需詳細資訊，請參閱 [手動安全密碼重設](active-directory-identityprotection.md#manual-secure-password-reset) 。
2. **關閉所有的風險事件**-hello 使用者風險原則封鎖的使用者，如果已達到設定的 hello 使用者風險層級是否有封鎖存取。 您可以手動關閉已報告的風險事件來降低使用者的風險層級。 如需詳細資訊，請參閱 [手動關閉風險事件](active-directory-identityprotection.md#closing-risk-events-manually)。
3. **從原則中排除**-如果您認為，hello 目前您登入的原則設定會造成特定使用者的問題，您可以 hello 使用者排除它。 如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。
4. **停用原則**-如果您認為，原則設定會造成問題的所有使用者，您可以停用 hello 原則。 如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。

## <a name="next-steps"></a>後續步驟
 您想深入了解 Azure AD Identity Protection tooknow 嗎？ 查看 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。
