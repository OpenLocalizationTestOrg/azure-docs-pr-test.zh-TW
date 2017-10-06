---
title: "在 Azure AD Privileged Identity Management aaaRoles |Microsoft 文件"
description: "了解哪些角色用於特殊權限的身分識別與 hello Azure Privileged Identity Management 延伸模組。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Azure Active Directory PIM 中不同的系統管理角色
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

您可以將使用者指派您組織中 toodifferent 系統管理角色在 Azure AD 中。 這些角色指派會控制哪些工作，例如加入或移除使用者或變更服務設定，hello 使用者位於無法 tooperform Office 365 和其他 Microsoft 線上服務和連接的應用程式的 Azure AD。  

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。

全域管理員可以更新哪些使用者**永久**在 Azure AD 中使用 PowerShell cmdlet，例如指派 tooroles`Add-MsolRoleMember`和`Remove-MsolRoleMember`，或透過 hello 傳統入口網站中所述[指派系統管理員角色在 Azure Active Directory](active-directory-assign-admin-roles.md)。

Azure AD Privileged Identity Management (PIM) 可管理以特殊權限存取 Azure AD 中之使用者的原則。 PIM 在 Azure AD 中指派使用者 tooone 或多個角色，而且您可以指派有人 toobe 永久在 hello 角色或合格 hello 角色。 當使用者會永久指派 tooa 角色，或啟動符合資格的角色指派，則他們可以管理 Azure Active Directory、 Office 365 和其他應用程式與 hello 分派 tootheir 角色的權限。

沒有任何差異在提供與符合資格的角色指派永久與 toosomeone hello 存取。 hello 只是某些人，不需要存取之所有 hello 時間。 它們會進行適合 hello 角色，而且可以將其開啟和關閉時所需。

## <a name="roles-managed-in-pim"></a>PIM 中管理的角色
Privileged 的 Identity Management 可讓您指派使用者 toocommon 系統管理員角色，包括：

* **全域管理員**（也就是公司系統管理員） 具有存取 tooall 系統管理功能。 您可以在組織中擁有多個全域管理員。 自動註冊 toopurchase Office 365 的 hello 人員會變成全域管理員。
*  可以管理 Azure AD PIM，以及更新其他使用者的角色指派。  
*  負責採購、管理訂用帳戶、管理支援票證，以及監控服務健全狀況。
*  可以重設密碼、管理服務要求，以及監控服務健全狀況。 密碼管理員是有限的 tooresetting 使用者的密碼。
*  可以管理服務要求，以及監控服務健全狀況。
  
  > [!NOTE]
  > 如果您使用 Office 365，然後再指派 hello 服務系統管理員角色 tooa 使用者，第一次指派 hello 使用者的系統管理權限 tooa 服務，例如 Exchange Online。
  > 
  > 
*  可以重設密碼、監控服務健全狀況，以及管理使用者帳戶、使用者群組和服務要求。 hello 使用者管理管理員無法刪除全域管理員，建立其他系統管理員角色，或重設計費、 全域和服務系統管理員密碼。
* **Exchange 系統管理員**hello Exchange 系統管理中心 (EAC)，透過擁有管理存取 tooExchange 線上，而且可以在 Exchange Online 中執行幾乎任何工作。
* **SharePoint 管理員**hello SharePoint Online 系統管理中心，透過擁有管理存取 tooSharePoint 線上，而且可以在 SharePoint Online 中執行幾乎任何工作。
* **商務系統管理員的 Skype** hello Skype 的商務系統管理中心，透過具有商務的系統管理存取權 tooSkype，可以幾乎任何工作在執行 Skype for Business Online。

如需有關[在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)和[在 Office 365 中指派管理員角色](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504)的更多詳細資料，請閱讀這些文章。

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


您可以從 PIM，[指派給這些角色 tooa 使用者](active-directory-privileged-identity-management-how-to-add-role-to-user.md)如此 hello 使用者[啟用 hello 角色在需要時](active-directory-privileged-identity-management-how-to-activate-role.md)。

如果您想 toogive PIM 本身，PIM 需要 hello 使用者 toohave 會進一步說明中的 hello 角色中的另一個使用者存取 toomanage [toogive 如何存取 tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>PIM 中未管理的角色
Exchange Online 或 SharePoint Online 內的角色 (除了前面提及的角色外) 並不會出現在 Azure AD 中，因此您不會在 PIM 中看到。 如需有關在這些 Office 365 服務中變更細部角色指派的詳細資訊，請參閱 [Office 365 中的權限](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

Azure 訂用帳戶和資源群組也不會出現在 Azure AD 中。 toomanage Azure 訂用帳戶，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)，如需有關 Azure rbac 進行，請參閱[所有存取控制](role-based-access-control-configure.md)。

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>使用者角色和登入
某些 Microsoft 服務和應用程式，將使用者 tooa 角色指派可能不是足夠 tooenable 該使用者 toobe 系統管理員。

存取 toohello Azure 傳統入口網站需要 hello 使用者是服務系統管理員或 Azure 訂用帳戶的共同管理員，即使 hello 使用者不需要 toomanage hello Azure 訂用帳戶。  例如，toomanage hello 傳統入口網站，使用者在 Azure AD 的組態設定必須是 Azure AD 中的全域管理員和 Azure 訂用帳戶的訂用帳戶共同管理員。  如何 tooadd 使用者 tooAzure 訂用帳戶，請參閱的 toolearn[如何 tooadd 或變更的 Azure 系統管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)。

線上服務可能需要存取 tooMicrosoft hello 也為使用者指派授權才能開啟 hello 服務入口網站或執行系統管理工作。

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>在 Azure AD 中指派給授權 tooa 使用者
1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com)與全域管理員帳戶或共同管理員帳戶。
2. 選取**所有項目**從 hello 主功能表。
3. 選取您想要與 toowork 和，具有授權與其相關聯的 hello 目錄。
4. 選取 [授權] 。 可用的授權 hello 清單會隨即出現。
5. 選取包含您想 toodistribute hello 授權 hello 授權計劃。
6. 選取 [指派使用者] 。
7. 選取 hello 使用者想授權 tooassign 至。
8. 按一下 hello**指派**] 按鈕。  hello 使用者現在可以登入 tooAzure 中。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

