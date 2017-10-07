---
title: "aaaHow toorequire 多重要素驗證 |Microsoft 文件"
description: "了解如何 toorequire multi-factor authentication (MFA) 特殊權限身分識別與 hello Azure Active Directory Privileged Identity Management 延伸模組。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>如何在 Azure AD Privileged Identity Management MFA toorequire
建議您針對所有系統管理員都要求進行多重要素驗證 (MFA)。 這可降低攻擊者危害 tooa 密碼到期 hello 風險。

您可以要求使用者在登入時完成 MFA 挑戰。 hello 部落格文章[Office 365 和 azure MFA 的 MFA](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)比較與 hello hello Microsoft Azure Multi-factor Authentication 供應項目中所包含的功能包含 Office 和 Azure 訂用帳戶的內容。

您也可以要求使用者在啟用 Azure AD PIM 中的角色時，完成 MFA 挑戰。 如此一來，如果它們登入時，hello 使用者未完成的 MFA 挑戰，就會提示的 toodo 是由 PIM。

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>在 Azure AD Privileged Identity Management 中強制啟用 MFA
當您以特殊權限角色管理員的身分管理 PIM 中的身分識別時，您可能會看到建議特殊權限帳戶使用 MFA 的警示。 按一下 [安全性] hello hello PIM 儀表板和的新刀鋒視窗中的警示將會開啟 hello 應該需要 MFA 的系統管理員帳戶的清單。  您可以選取多個角色，然後按一下hello 要求 MFA**修正**] 按鈕，或者您可以按一下 [hello 省略符號 [下一步 tooindividual 角色，然後按一下hello**修正**] 按鈕。

> [!IMPORTANT]
> 現在，Azure MFA 只適用於使用工作或學校帳戶，沒有 Microsoft 帳戶 （通常是個人的帳戶中使用過 toosign tooMicrosoft 服務類似 Skype、 Xbox、 Outlook.com 等。），以滑鼠右鍵。 因為這個緣故，使用 Microsoft 帳戶的任何人都不能合格的系統管理員，因為它們不能使用 MFA tooactivate 及其角色。 如果這些使用者需要 toocontinue 管理使用 Microsoft 帳戶的工作負載，提高其 toopermanent 系統管理員現在。
> 
> 

此外，您可以變更特定角色的 hello MFA 需求 hello hello PIM 儀表板的 [角色] 區段中按一下。 然後按一下 上**設定**hello 角色 刀鋒視窗，然後選取 在**啟用**下多重要素驗證。

## <a name="how-azure-ad-pim-validates-mfa"></a>Azure AD PIM 如何驗證 MFA
在使用者啟用角色時有兩個選項可用來驗證 MFA。

hello 簡單的選項是 toorely 上 Azure MFA 的使用者要啟用特殊權限的角色。 toodo，第一次檢查那些使用者授權，如有必要，且已註冊的 Azure MFA。 有關如何 toodo 這種[開始使用 Azure Multi-factor Authentication hello 定域機組中](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。 它是建議，但並非必要，登入時，設定這些使用者的 Azure AD tooenforce MFA。 這是因為 hello MFA 檢查將會由 Azure AD PIM 本身。

或者，如果使用者驗證內部部署，您可以讓您的身分識別提供者負責進行 MFA。 例如，如果您已設定 AD Federation Services toorequire 智慧卡驗證，才能存取 Azure AD，[與 Azure Multi-factor Authentication Server 和 AD FS 保護雲端資源](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md)包含指示適用於設定 AD FS toosend 宣告 tooAzure AD。 當使用者嘗試 tooactivate 角色時，Azure AD PIM 將接受的 MFA 已經過驗證 hello 使用者在收到 hello 適當的宣告。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

