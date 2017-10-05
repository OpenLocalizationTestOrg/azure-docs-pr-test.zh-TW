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
# <a name="different-administrative-role-in-azure-active-directory-pim"></a><span data-ttu-id="47e45-103">Azure Active Directory PIM 中不同的系統管理角色</span><span class="sxs-lookup"><span data-stu-id="47e45-103">Different administrative role in Azure Active Directory PIM</span></span>
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

<span data-ttu-id="47e45-104">您可以將組織中的使用者指派給 Azure AD 內的不同系統管理角色。</span><span class="sxs-lookup"><span data-stu-id="47e45-104">You can assign users in your organization to different administrative roles in Azure AD.</span></span> <span data-ttu-id="47e45-105">這些角色指派控制使用者可以在 Azure AD、Office 365 和其他 Microsoft Online Services 與連線的應用程式執行哪些工作，像是新增或移除使用者或變更服務設定。</span><span class="sxs-lookup"><span data-stu-id="47e45-105">These role assignments control which tasks, such as adding or removing users or changing service settings, the users are able to perform on Azure AD, Office 365 and other Microsoft Online Services and connected applications.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="47e45-106">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="47e45-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="47e45-107">全域管理員可以使用 PowerShell Cmdlet (例如 `Add-MsolRoleMember` 和 `Remove-MsolRoleMember`) 或如[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)中所述透過傳統入口網站，更新要將哪些使用者「永久」指派給 Azure AD 中的角色。</span><span class="sxs-lookup"><span data-stu-id="47e45-107">A global administrator can update which users are **permanently** assigned to roles in Azure AD, using PowerShell cmdlets such as `Add-MsolRoleMember` and `Remove-MsolRoleMember`, or through the classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="47e45-108">Azure AD Privileged Identity Management (PIM) 可管理以特殊權限存取 Azure AD 中之使用者的原則。</span><span class="sxs-lookup"><span data-stu-id="47e45-108">Azure AD Privileged Identity Management (PIM) manages policies for privileged access for users in Azure AD.</span></span> <span data-ttu-id="47e45-109">PIM 會將使用者指派給 Azure AD 中的一或多個角色，您可以指派某位使用者永久擔任該角色，或是將其指派成符合該角色資格。</span><span class="sxs-lookup"><span data-stu-id="47e45-109">PIM assigns users to one or more roles in Azure AD, and you can assign someone to be permanently in the role, or eligible for the role.</span></span> <span data-ttu-id="47e45-110">將使用者永久指派給某個角色或是啟用合格角色指派時，他們便可以使用指派給他們角色的權限來管理 Azure Active Directory、Office 365 及其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="47e45-110">When a user is permanently assigned to a role, or activates an eligible role assignment, then they can manage Azure Active Directory, Office 365, and other applications with the permissions assigned to their roles.</span></span>

<span data-ttu-id="47e45-111">使用者不論是具有永久角色指派還是合格角色指派，獲得的存取權並無差異。</span><span class="sxs-lookup"><span data-stu-id="47e45-111">There's no difference in the access given to someone with a permanent versus an eligible role assignment.</span></span> <span data-ttu-id="47e45-112">唯一的差異在於有些使用者並不一直需要該存取權。</span><span class="sxs-lookup"><span data-stu-id="47e45-112">The only difference is that some people don't need that access all the time.</span></span> <span data-ttu-id="47e45-113">他們已被設為該角色的合格使用者，因此可以隨時視需要開啟或關閉該角色。</span><span class="sxs-lookup"><span data-stu-id="47e45-113">They are made eligible for the role, and can turn it on and off whenever they need to.</span></span>

## <a name="roles-managed-in-pim"></a><span data-ttu-id="47e45-114">PIM 中管理的角色</span><span class="sxs-lookup"><span data-stu-id="47e45-114">Roles managed in PIM</span></span>
<span data-ttu-id="47e45-115">Privileged Identity Management 可讓您將使用者指派給常見的系統管理員角色，包括︰</span><span class="sxs-lookup"><span data-stu-id="47e45-115">Privileged Identity Management lets you assign users to common administrator roles, including:</span></span>

* <span data-ttu-id="47e45-116"> (也稱為公司系統管理員) 可以存取所有系統管理功能。</span><span class="sxs-lookup"><span data-stu-id="47e45-116">**Global administrator** (also known as Company administrator) has access to all administrative features.</span></span> <span data-ttu-id="47e45-117">您可以在組織中擁有多個全域管理員。</span><span class="sxs-lookup"><span data-stu-id="47e45-117">You can have more than one global admin in your organization.</span></span> <span data-ttu-id="47e45-118">註冊購買 Office 365 的人員會自動成為全域管理員。</span><span class="sxs-lookup"><span data-stu-id="47e45-118">The person who signs up to purchase Office 365 automatically becomes a global admin.</span></span>
* <span data-ttu-id="47e45-119"> 可以管理 Azure AD PIM，以及更新其他使用者的角色指派。</span><span class="sxs-lookup"><span data-stu-id="47e45-119">**Privileged role administrator** manages Azure AD PIM and updates role assignments for other users.</span></span>  
* <span data-ttu-id="47e45-120"> 負責採購、管理訂用帳戶、管理支援票證，以及監控服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="47e45-120">**Billing administrator** makes purchases, manages subscriptions, manages support tickets, and monitors service health.</span></span>
* <span data-ttu-id="47e45-121"> 可以重設密碼、管理服務要求，以及監控服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="47e45-121">**Password administrator** resets passwords, manages service requests, and monitors service health.</span></span> <span data-ttu-id="47e45-122">密碼管理員只能重設使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="47e45-122">Password admins are limited to resetting passwords for users.</span></span>
* <span data-ttu-id="47e45-123"> 可以管理服務要求，以及監控服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="47e45-123">**Service administrator** manages service requests and monitors service health.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="47e45-124">如果您使用 Office 365，則在指派服務管理員角色給使用者之前，請先將服務 (例如 Exchange Online) 的系統管理權限指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="47e45-124">If you are using Office 365, then before assigning the service admin role to a user, first assign the user administrative permissions to a service, such as Exchange Online.</span></span>
  > 
  > 
* <span data-ttu-id="47e45-125"> 可以重設密碼、監控服務健全狀況，以及管理使用者帳戶、使用者群組和服務要求。</span><span class="sxs-lookup"><span data-stu-id="47e45-125">**User management administrator** resets passwords, monitors service health, and manages user accounts, user groups, and service requests.</span></span> <span data-ttu-id="47e45-126">使用者管理管理員無法刪除全域管理員、建立其他管理員角色，或重設計費、全域和服務管理員的密碼。</span><span class="sxs-lookup"><span data-stu-id="47e45-126">The user management admin can’t delete a global admin, create other admin roles, or reset passwords for billing, global, and service admins.</span></span>
* <span data-ttu-id="47e45-127"> 具有透過 Exchange 系統管理中心 (EAC) 存取 Exchange Online 的系統管理權限，並可在 Exchange Online 執行幾乎所有工作。</span><span class="sxs-lookup"><span data-stu-id="47e45-127">**Exchange administrator** has administrative access to Exchange Online through the Exchange admin center (EAC), and can perform almost any task in Exchange Online.</span></span>
* <span data-ttu-id="47e45-128"> 具有透過 SharePoint Online 系統管理中心存取 SharePoint Online 的系統管理權限，並可在 SharePoint Online 執行幾乎所有工作。</span><span class="sxs-lookup"><span data-stu-id="47e45-128">**SharePoint administrator** has administrative access to SharePoint Online through the SharePoint Online admin center, and can perform almost any task in SharePoint Online.</span></span>
* <span data-ttu-id="47e45-129"> 具有透過「商務用 Skype」系統管理中心存取「商務用 Skype」的系統管理權限，並可在「商務用 Skype Online」執行幾乎所有工作。</span><span class="sxs-lookup"><span data-stu-id="47e45-129">**Skype for Business administrator** has administrative access to Skype for Business through the Skype for Business admin center, and can perform almost any task in Skype for Business Online.</span></span>

<span data-ttu-id="47e45-130">如需有關[在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)和[在 Office 365 中指派管理員角色](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504)的更多詳細資料，請閱讀這些文章。</span><span class="sxs-lookup"><span data-stu-id="47e45-130">Read these articles for more details about [assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) and [assigning admin roles in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).</span></span>

<!--**PLACEHOLDER: The above article may not be the one we want since PIM gets roles from places other that Office 365**-->


<span data-ttu-id="47e45-131">您可以透過 PIM [將這些角色指派給使用者](active-directory-privileged-identity-management-how-to-add-role-to-user.md)，讓使用者可以[在需要時啟用角色](active-directory-privileged-identity-management-how-to-activate-role.md)。</span><span class="sxs-lookup"><span data-stu-id="47e45-131">From PIM, you can [assign these roles to a user](active-directory-privileged-identity-management-how-to-add-role-to-user.md) so that the user can [activate the role when needed](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

<span data-ttu-id="47e45-132">如果您想要將存取權授與另一位使用者，使他可以在 PIM 本身中進行管理， [如何授與對 PIM 的存取權](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)有進一步說明 PIM 要求使用者必須具備哪些角色。</span><span class="sxs-lookup"><span data-stu-id="47e45-132">If you want to give another user access to manage in PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

<!-- ## The PIM Security Administrator Role **PLACEHOLDER: Need description of the Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a><span data-ttu-id="47e45-133">PIM 中未管理的角色</span><span class="sxs-lookup"><span data-stu-id="47e45-133">Roles not managed in PIM</span></span>
<span data-ttu-id="47e45-134">Exchange Online 或 SharePoint Online 內的角色 (除了前面提及的角色外) 並不會出現在 Azure AD 中，因此您不會在 PIM 中看到。</span><span class="sxs-lookup"><span data-stu-id="47e45-134">Roles within Exchange Online or SharePoint Online, except for those mentioned above, are not represented in Azure AD and so are not visible in PIM.</span></span> <span data-ttu-id="47e45-135">如需有關在這些 Office 365 服務中變更細部角色指派的詳細資訊，請參閱 [Office 365 中的權限](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d)。</span><span class="sxs-lookup"><span data-stu-id="47e45-135">For more information on changing fine-grained role assignments in these Office 365 services, see [Permissions in Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).</span></span>

<span data-ttu-id="47e45-136">Azure 訂用帳戶和資源群組也不會出現在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="47e45-136">Azure subscriptions and resource groups are also not represented in Azure AD.</span></span> <span data-ttu-id="47e45-137">若要管理 Azure 訂用帳戶，請參閱 [如何新增或變更 Azure 管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)，如需有關 Azure RBAC 的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="47e45-137">To manage Azure subscriptions, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md) and for more information on Azure RBAC see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

<!--**The above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a><span data-ttu-id="47e45-138">使用者角色和登入</span><span class="sxs-lookup"><span data-stu-id="47e45-138">User roles and signing in</span></span>
<span data-ttu-id="47e45-139">對於某些 Microsoft 服務和應用程式來說，將使用者指派給角色可能還不足以讓該使用者成為管理員。</span><span class="sxs-lookup"><span data-stu-id="47e45-139">For some Microsoft services and applications, assigning a user to a role may not be sufficient to enable that user to be an administrator.</span></span>

<span data-ttu-id="47e45-140">使用者若要存取 Azure 傳統入口網站，就必須是 Azure 訂用帳戶的服務管理員或共同管理員，即使使用者不需要管理 Azure 訂用帳戶也是如此。</span><span class="sxs-lookup"><span data-stu-id="47e45-140">Access to the Azure classic portal requires the user be a service administrator or co-administrator on an Azure subscription, even if the user does not need to manage the Azure subscriptions.</span></span>  <span data-ttu-id="47e45-141">例如，若要在傳統入口網站中管理 Azure AD 的組態設定，使用者必須身兼 Azure AD 中的全域管理員和 Azure 訂用帳戶上的訂用帳戶共同管理員。</span><span class="sxs-lookup"><span data-stu-id="47e45-141">For example, to manage configuration settings for Azure AD in the classic portal, a user must be both a global administrator in Azure AD and a subscription co-administrator on an Azure subscription.</span></span>  <span data-ttu-id="47e45-142">若要了解如何將使用者新增到 Azure 訂用帳戶，請參閱 [如何新增或變更 Azure 管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="47e45-142">To learn how to add users to Azure subscriptions, see [How to add or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="47e45-143">使用者若要存取 Microsoft Online Services，可能也必須已獲指派授權才能開啟服務的入口網站或執行系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="47e45-143">Access to Microsoft Online Services may require the user also be assigned a license before they can open the service's portal or perform administrative tasks.</span></span>

## <a name="assign-a-license-to-a-user-in-azure-ad"></a><span data-ttu-id="47e45-144">將授權指派給 Azure AD 中的使用者</span><span class="sxs-lookup"><span data-stu-id="47e45-144">Assign a license to a user in Azure AD</span></span>
1. <span data-ttu-id="47e45-145">使用全域管理員帳戶或共同管理員帳戶登入 [Azure 傳統入口網站](http://manage.windowsazure.com) 。</span><span class="sxs-lookup"><span data-stu-id="47e45-145">Sign in to the [Azure classic portal](http://manage.windowsazure.com) with a global administrator account or a co-administrator account.</span></span>
2. <span data-ttu-id="47e45-146">從主功能表中選取 [所有項目]  。</span><span class="sxs-lookup"><span data-stu-id="47e45-146">Select **All Items** from the main menu.</span></span>
3. <span data-ttu-id="47e45-147">選取您想要使用的目錄，且該目錄會含有與它相關聯的授權。</span><span class="sxs-lookup"><span data-stu-id="47e45-147">Select the directory you want to work with and that has licenses associated with it.</span></span>
4. <span data-ttu-id="47e45-148">選取 [授權] 。</span><span class="sxs-lookup"><span data-stu-id="47e45-148">Select **Licenses**.</span></span> <span data-ttu-id="47e45-149">隨即會出現可用的授權清單。</span><span class="sxs-lookup"><span data-stu-id="47e45-149">The list of available licenses will appear.</span></span>
5. <span data-ttu-id="47e45-150">選取包含您要散發之授權的授權方案。</span><span class="sxs-lookup"><span data-stu-id="47e45-150">Select the license plan which contains the licenses that you want to distribute.</span></span>
6. <span data-ttu-id="47e45-151">選取 [指派使用者] 。</span><span class="sxs-lookup"><span data-stu-id="47e45-151">Select **Assign Users**.</span></span>
7. <span data-ttu-id="47e45-152">選取您想要指派授權的使用者。</span><span class="sxs-lookup"><span data-stu-id="47e45-152">Select the user that you want to assign a license to.</span></span>
8. <span data-ttu-id="47e45-153">按一下 [指派]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="47e45-153">Click the **Assign** button.</span></span>  <span data-ttu-id="47e45-154">使用者現在已可以登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="47e45-154">The user can now sign in to Azure.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="47e45-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47e45-155">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

