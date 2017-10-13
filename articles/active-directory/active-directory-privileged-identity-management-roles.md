---
title: "Azure AD Privileged Identity Management 中的角色 | Microsoft Docs"
description: "了解要針對具備 Azure 特殊權限身分識別管理擴充功能的特殊權限身分識別使用哪些角色。"
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
ms.openlocfilehash: c20aca4202319154b01d6398570f745636120f49
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Azure Active Directory PIM 中不同的系統管理角色
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

您可以將組織中的使用者指派給 Azure AD 內的不同系統管理角色。 這些角色指派控制使用者可以在 Azure AD、Office 365 和其他 Microsoft Online Services 與連線的應用程式執行哪些工作，像是新增或移除使用者或變更服務設定。  

> [!IMPORTANT]
> Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。

全域管理員可以使用 PowerShell Cmdlet (例如 `Add-MsolRoleMember` 和 `Remove-MsolRoleMember`) 或如[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)中所述透過傳統入口網站，更新要將哪些使用者「永久」指派給 Azure AD 中的角色。

Azure AD Privileged Identity Management (PIM) 可管理以特殊權限存取 Azure AD 中之使用者的原則。 PIM 會將使用者指派給 Azure AD 中的一或多個角色，您可以指派某位使用者永久擔任該角色，或是將其指派成符合該角色資格。 將使用者永久指派給某個角色或是啟用合格角色指派時，他們便可以使用指派給他們角色的權限來管理 Azure Active Directory、Office 365 及其他應用程式。

使用者不論是具有永久角色指派還是合格角色指派，獲得的存取權並無差異。 唯一的差異在於有些使用者並不一直需要該存取權。 他們已被設為該角色的合格使用者，因此可以隨時視需要開啟或關閉該角色。

## <a name="roles-managed-in-pim"></a>PIM 中管理的角色
Privileged Identity Management 可讓您將使用者指派給常見的系統管理員角色，包括︰

*  (也稱為公司系統管理員) 可以存取所有系統管理功能。 您可以在組織中擁有多個全域管理員。 註冊購買 Office 365 的人員會自動成為全域管理員。
*  可以管理 Azure AD PIM，以及更新其他使用者的角色指派。  
*  負責採購、管理訂用帳戶、管理支援票證，以及監控服務健全狀況。
*  可以重設密碼、管理服務要求，以及監控服務健全狀況。 密碼管理員只能重設使用者的密碼。
*  可以管理服務要求，以及監控服務健全狀況。
  
  > [!NOTE]
  > 如果您使用 Office 365，則在指派服務管理員角色給使用者之前，請先將服務 (例如 Exchange Online) 的系統管理權限指派給使用者。
  > 
  > 
*  可以重設密碼、監控服務健全狀況，以及管理使用者帳戶、使用者群組和服務要求。 使用者管理管理員無法刪除全域管理員、建立其他管理員角色，或重設計費、全域和服務管理員的密碼。
*  具有透過 Exchange 系統管理中心 (EAC) 存取 Exchange Online 的系統管理權限，並可在 Exchange Online 執行幾乎所有工作。
*  具有透過 SharePoint Online 系統管理中心存取 SharePoint Online 的系統管理權限，並可在 SharePoint Online 執行幾乎所有工作。
*  具有透過「商務用 Skype」系統管理中心存取「商務用 Skype」的系統管理權限，並可在「商務用 Skype Online」執行幾乎所有工作。

如需有關[在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)和[在 Office 365 中指派管理員角色](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504)的更多詳細資料，請閱讀這些文章。

<!--**PLACEHOLDER: The above article may not be the one we want since PIM gets roles from places other that Office 365**-->


您可以透過 PIM [將這些角色指派給使用者](active-directory-privileged-identity-management-how-to-add-role-to-user.md)，讓使用者可以[在需要時啟用角色](active-directory-privileged-identity-management-how-to-activate-role.md)。

如果您想要將存取權授與另一位使用者，使他可以在 PIM 本身中進行管理， [如何授與對 PIM 的存取權](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)有進一步說明 PIM 要求使用者必須具備哪些角色。

<!-- ## The PIM Security Administrator Role **PLACEHOLDER: Need description of the Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>PIM 中未管理的角色
Exchange Online 或 SharePoint Online 內的角色 (除了前面提及的角色外) 並不會出現在 Azure AD 中，因此您不會在 PIM 中看到。 如需有關在這些 Office 365 服務中變更細部角色指派的詳細資訊，請參閱 [Office 365 中的權限](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d)。

Azure 訂用帳戶和資源群組也不會出現在 Azure AD 中。 若要管理 Azure 訂用帳戶，請參閱 [如何新增或變更 Azure 管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)，如需有關 Azure RBAC 的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

<!--**The above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>使用者角色和登入
對於某些 Microsoft 服務和應用程式來說，將使用者指派給角色可能還不足以讓該使用者成為管理員。

使用者若要存取 Azure 傳統入口網站，就必須是 Azure 訂用帳戶的服務管理員或共同管理員，即使使用者不需要管理 Azure 訂用帳戶也是如此。  例如，若要在傳統入口網站中管理 Azure AD 的組態設定，使用者必須身兼 Azure AD 中的全域管理員和 Azure 訂用帳戶上的訂用帳戶共同管理員。  若要了解如何將使用者新增到 Azure 訂用帳戶，請參閱 [如何新增或變更 Azure 管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)。

使用者若要存取 Microsoft Online Services，可能也必須已獲指派授權才能開啟服務的入口網站或執行系統管理工作。

## <a name="assign-a-license-to-a-user-in-azure-ad"></a>將授權指派給 Azure AD 中的使用者
1. 使用全域管理員帳戶或共同管理員帳戶登入 [Azure 傳統入口網站](http://manage.windowsazure.com) 。
2. 從主功能表中選取 [所有項目]  。
3. 選取您想要使用的目錄，且該目錄會含有與它相關聯的授權。
4. 選取 [授權] 。 隨即會出現可用的授權清單。
5. 選取包含您要散發之授權的授權方案。
6. 選取 [指派使用者] 。
7. 選取您想要指派授權的使用者。
8. 按一下 [指派]  按鈕。  使用者現在已可以登入 Azure。

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>後續步驟
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

