---
title: "aaaHow toogive 存取 tooPrivileged 身分識別管理-Azure |Microsoft 文件"
description: "了解如何使用 tooadd 角色 toousers hello Azure Active Directory Privileged Identity Management 延伸讓他們可以管理 PIM。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>提供存取 toomanage Azure AD Privileged Identity Management
hello 全域系統管理員可讓 Azure AD Privileged Identity Management (PIM) 的組織自動取得角色指派，並存取 tooPIM。 不過，預設不會有任何其他人取得寫入存取權，包括其他全域系統管理員。 其他全域管理員、 安全性系統管理員和安全性的讀取器具有唯讀存取 tooAzure AD PIM。 toogive 存取 tooPIM，hello 第一個使用者可以指派給其他人 toohello**特殊權限的角色管理員**角色。 這項指派必須在 PIM 內完成，而且無法透過 PowerShell 或其他入口網站變更。

> [!NOTE]
> 管理 Azure AD PIM 需要 Azure MFA。 因為 Microsoft 帳戶無法註冊 Azure MFA，所以使用 Microsoft 帳戶登入的使用者無法存取 Azure AD PIM。
> 
> 

請確保特殊權限角色管理員角色中永遠至少有兩位使用者，以防一位使用者遭到鎖定或他們的帳戶遭刪除。

## <a name="give-another-user-access-toomanage-pim"></a>授與其他使用者存取 toomanage PIM
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello **Azure AD Privileged Identity Management** hello 儀表板上的應用程式。
2. 選取 [管理特殊權限角色]  >  [特殊權限角色管理員]  >  [新增]。
   
    ![新增特殊權限角色管理員 - 螢幕擷取畫面][1]
3. Hello 新增受管理的使用者 刀鋒視窗，在步驟 1 已完成。 選取步驟 2，**選取使用者**並搜尋您想 tooadd hello 使用者。
   
    ![選取使用者 - 螢幕擷取畫面][2]
4. 從 hello 搜尋結果中，選取 hello 使用者並按一下**完成**。
5. 按一下**確定**toosave 選取項目。 您已選取的 hello 使用者會出現在 hello 特殊權限的角色管理員清單。
   
   * 每當您指派新的角色 toosomeone，它們會自動設定做為合格 tooactivate hello 角色。 如果您想 toomake 它們永久在 hello 角色中，按一下 hello 清單中的 hello 使用者。 選取**進行權限**hello 使用者資訊 功能表中。
6. 傳送 hello 的連結使用者太[開始使用 Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)。

## <a name="remove-another-users-access-rights-for-managing-pim"></a>移除其他使用者管理 PIM 的存取權限
有人 hello 特殊權限的角色系統管理員角色中移除之前，請務必確定仍會指派 tooit 的兩個使用者。

1. Hello PIM 儀表板中按一下 hello 角色**特殊權限的角色管理員**。  將顯示 hello 目前在該角色中的使用者清單。
2. 按一下 hello hello 使用者清單中的使用者。
3. 按一下 [移除] 。  您將會看到確認訊息。
4. 按一下**是**tooremove hello 使用者從 hello 角色。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
