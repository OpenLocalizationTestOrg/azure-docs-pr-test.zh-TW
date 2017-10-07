---
title: "aaaHow tooadd 或移除使用者角色 |Microsoft 文件"
description: "了解如何 tooadd 角色 tooprivileged 身分識別與 hello Azure Active Directory Privileged Identity Management 的應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure 的 AD Privileged Identity Management： 如何 tooadd 或移除使用者角色
使用 Azure Active Directory (AD)，全域系統管理員 （或公司系統管理員） 可以更新哪些使用者**永久**tooroles 指派 Azure AD 中。 做法是使用 PowerShell Cmdlet，如 `Add-MsolRoleMember` 和 `Remove-MsolRoleMember`。 中所述，也可以使用 Azure 傳統入口網站 hello[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)。

hello Azure AD Privileged Identity Management 的應用程式可讓 toomake 永久的角色指派，以及特殊權限的角色系統管理員。 此外，特殊權限角色系統管理員可以讓使用者 **有資格**扮演系統管理員角色。 當他們需要它，而且一旦完成後及其權限到期。 然後，合格的系統管理員可以啟動 hello 角色。

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>管理與 PIM hello Azure 入口網站中的角色
在您組織中，您可以指定使用者 toodifferent 系統管理角色在 Azure AD 中，Office 365，及其他 Microsoft 服務和應用程式。  需 hello 可用角色的詳細資訊，請參閱[角色在 Azure AD PIM](active-directory-privileged-identity-management-roles.md)。

tooadd] 或 [移除角色，使用 Privileged Identity Management 的使用者顯示 hello PIM 儀表板。 然後按一下 hello**中系統管理員角色的使用者**按鈕，或選取特定的角色 （例如全域系統管理員） 從 hello roles 資料表。

> [!NOTE]
> 如果您尚未啟用 PIM hello Azure 入口網站中尚未，請移至太[開始使用 Azure AD PIM](active-directory-privileged-identity-management-getting-started.md)如需詳細資訊。

如果您想 toogive PIM 需要 hello 使用者 toohave 會進一步說明中的 hello 角色本身的其他使用者存取 tooPIM [toogive 如何存取 tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。

## <a name="add-a-user-tooa-role"></a>新增使用者 tooa 角色
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取 hello **Azure AD Privileged Identity Management** hello 儀表板上的磚。
2. 選取 [管理特殊權限角色] 。
3. 在 hello**角色摘要**資料表，您想要 toomanage 選取 hello 角色。
4. 在 hello 角色 刀鋒視窗中，選取 **新增**。
5. 按一下**選取使用者**，並搜尋 hello hello 使用者**選取使用者**刀鋒視窗。  
6. 從 hello 搜尋結果清單中，選取 hello 使用者並按一下**完成**。
7. 按一下**確定**toosave 選取項目。 您已選取的 hello 使用者會出現在 hello 適合 hello 角色清單。

> [!NOTE]
> 角色中的新使用者，才適合 hello 預設的角色。 如果您想永久 toomake hello 角色，請按一下 [hello] 清單中的 hello 使用者。 hello 使用者的資訊會出現在新的刀鋒視窗。 選取**讓權限**hello 使用者資訊 功能表中。  
> 如果使用者無法註冊的 Azure Multi-factor Authentication (MFA)，或使用 Microsoft 帳戶 (通常@outlook.com)，您需要 toomake 它們永久的所有角色。 符合資格的系統管理員 」 會詢問在啟用期間 tooregister MFA。

既然 hello 使用者有資格的角色，讓他們知道他們可以啟動它，根據 toohello 指示[如何 tooactivate 或停用角色](active-directory-privileged-identity-management-how-to-activate-role.md)。

## <a name="remove-a-user-from-a-role"></a>從角色移除使用者
您可以將使用者從合格角色指派中移除，但請務必一律至少保留一個永久全域系統管理員使用者。

從角色，請遵循這些步驟 tooremove 特定的使用者：

1. 瀏覽 toohello 角色 hello 角色清單中的，選取 hello Azure AD PIM 儀表板中的角色，或是按一下 hello**中系統管理員角色的使用者** 按鈕。
2. 按一下 hello hello 使用者清單中的使用者。
3. 按一下 [移除] 。 訊息會要求您 tooconfirm。
4. 按一下**是**tooremove hello hello 使用者角色。

如果您不確定哪些使用者仍然需要其角色指派，則您可以[開始 hello 角色存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

