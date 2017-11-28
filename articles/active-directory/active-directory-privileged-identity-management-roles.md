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
# <a name="different-administrative-role-in-azure-active-directory-pim"></a><span data-ttu-id="14f6a-103">Azure Active Directory PIM 中不同的系統管理角色</span><span class="sxs-lookup"><span data-stu-id="14f6a-103">Different administrative role in Azure Active Directory PIM</span></span>
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

<span data-ttu-id="14f6a-104">您可以將使用者指派您組織中 toodifferent 系統管理角色在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="14f6a-104">You can assign users in your organization toodifferent administrative roles in Azure AD.</span></span> <span data-ttu-id="14f6a-105">這些角色指派會控制哪些工作，例如加入或移除使用者或變更服務設定，hello 使用者位於無法 tooperform Office 365 和其他 Microsoft 線上服務和連接的應用程式的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="14f6a-105">These role assignments control which tasks, such as adding or removing users or changing service settings, hello users are able tooperform on Azure AD, Office 365 and other Microsoft Online Services and connected applications.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="14f6a-106">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="14f6a-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="14f6a-107">全域管理員可以更新哪些使用者**永久**在 Azure AD 中使用 PowerShell cmdlet，例如指派 tooroles`Add-MsolRoleMember`和`Remove-MsolRoleMember`，或透過 hello 傳統入口網站中所述[指派系統管理員角色在 Azure Active Directory](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="14f6a-107">A global administrator can update which users are **permanently** assigned tooroles in Azure AD, using PowerShell cmdlets such as `Add-MsolRoleMember` and `Remove-MsolRoleMember`, or through hello classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="14f6a-108">Azure AD Privileged Identity Management (PIM) 可管理以特殊權限存取 Azure AD 中之使用者的原則。</span><span class="sxs-lookup"><span data-stu-id="14f6a-108">Azure AD Privileged Identity Management (PIM) manages policies for privileged access for users in Azure AD.</span></span> <span data-ttu-id="14f6a-109">PIM 在 Azure AD 中指派使用者 tooone 或多個角色，而且您可以指派有人 toobe 永久在 hello 角色或合格 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="14f6a-109">PIM assigns users tooone or more roles in Azure AD, and you can assign someone toobe permanently in hello role, or eligible for hello role.</span></span> <span data-ttu-id="14f6a-110">當使用者會永久指派 tooa 角色，或啟動符合資格的角色指派，則他們可以管理 Azure Active Directory、 Office 365 和其他應用程式與 hello 分派 tootheir 角色的權限。</span><span class="sxs-lookup"><span data-stu-id="14f6a-110">When a user is permanently assigned tooa role, or activates an eligible role assignment, then they can manage Azure Active Directory, Office 365, and other applications with hello permissions assigned tootheir roles.</span></span>

<span data-ttu-id="14f6a-111">沒有任何差異在提供與符合資格的角色指派永久與 toosomeone hello 存取。</span><span class="sxs-lookup"><span data-stu-id="14f6a-111">There's no difference in hello access given toosomeone with a permanent versus an eligible role assignment.</span></span> <span data-ttu-id="14f6a-112">hello 只是某些人，不需要存取之所有 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="14f6a-112">hello only difference is that some people don't need that access all hello time.</span></span> <span data-ttu-id="14f6a-113">它們會進行適合 hello 角色，而且可以將其開啟和關閉時所需。</span><span class="sxs-lookup"><span data-stu-id="14f6a-113">They are made eligible for hello role, and can turn it on and off whenever they need to.</span></span>

## <a name="roles-managed-in-pim"></a><span data-ttu-id="14f6a-114">PIM 中管理的角色</span><span class="sxs-lookup"><span data-stu-id="14f6a-114">Roles managed in PIM</span></span>
<span data-ttu-id="14f6a-115">Privileged 的 Identity Management 可讓您指派使用者 toocommon 系統管理員角色，包括：</span><span class="sxs-lookup"><span data-stu-id="14f6a-115">Privileged Identity Management lets you assign users toocommon administrator roles, including:</span></span>

* <span data-ttu-id="14f6a-116">**全域管理員**（也就是公司系統管理員） 具有存取 tooall 系統管理功能。</span><span class="sxs-lookup"><span data-stu-id="14f6a-116">**Global administrator** (also known as Company administrator) has access tooall administrative features.</span></span> <span data-ttu-id="14f6a-117">您可以在組織中擁有多個全域管理員。</span><span class="sxs-lookup"><span data-stu-id="14f6a-117">You can have more than one global admin in your organization.</span></span> <span data-ttu-id="14f6a-118">自動註冊 toopurchase Office 365 的 hello 人員會變成全域管理員。</span><span class="sxs-lookup"><span data-stu-id="14f6a-118">hello person who signs up toopurchase Office 365 automatically becomes a global admin.</span></span>
* <span data-ttu-id="14f6a-119"> 可以管理 Azure AD PIM，以及更新其他使用者的角色指派。</span><span class="sxs-lookup"><span data-stu-id="14f6a-119">**Privileged role administrator** manages Azure AD PIM and updates role assignments for other users.</span></span>  
* <span data-ttu-id="14f6a-120"> 負責採購、管理訂用帳戶、管理支援票證，以及監控服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="14f6a-120">**Billing administrator** makes purchases, manages subscriptions, manages support tickets, and monitors service health.</span></span>
* <span data-ttu-id="14f6a-121"> 可以重設密碼、管理服務要求，以及監控服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="14f6a-121">**Password administrator** resets passwords, manages service requests, and monitors service health.</span></span> <span data-ttu-id="14f6a-122">密碼管理員是有限的 tooresetting 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="14f6a-122">Password admins are limited tooresetting passwords for users.</span></span>
* <span data-ttu-id="14f6a-123"> 可以管理服務要求，以及監控服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="14f6a-123">**Service administrator** manages service requests and monitors service health.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="14f6a-124">如果您使用 Office 365，然後再指派 hello 服務系統管理員角色 tooa 使用者，第一次指派 hello 使用者的系統管理權限 tooa 服務，例如 Exchange Online。</span><span class="sxs-lookup"><span data-stu-id="14f6a-124">If you are using Office 365, then before assigning hello service admin role tooa user, first assign hello user administrative permissions tooa service, such as Exchange Online.</span></span>
  > 
  > 
* <span data-ttu-id="14f6a-125"> 可以重設密碼、監控服務健全狀況，以及管理使用者帳戶、使用者群組和服務要求。</span><span class="sxs-lookup"><span data-stu-id="14f6a-125">**User management administrator** resets passwords, monitors service health, and manages user accounts, user groups, and service requests.</span></span> <span data-ttu-id="14f6a-126">hello 使用者管理管理員無法刪除全域管理員，建立其他系統管理員角色，或重設計費、 全域和服務系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="14f6a-126">hello user management admin can’t delete a global admin, create other admin roles, or reset passwords for billing, global, and service admins.</span></span>
* <span data-ttu-id="14f6a-127">**Exchange 系統管理員**hello Exchange 系統管理中心 (EAC)，透過擁有管理存取 tooExchange 線上，而且可以在 Exchange Online 中執行幾乎任何工作。</span><span class="sxs-lookup"><span data-stu-id="14f6a-127">**Exchange administrator** has administrative access tooExchange Online through hello Exchange admin center (EAC), and can perform almost any task in Exchange Online.</span></span>
* <span data-ttu-id="14f6a-128">**SharePoint 管理員**hello SharePoint Online 系統管理中心，透過擁有管理存取 tooSharePoint 線上，而且可以在 SharePoint Online 中執行幾乎任何工作。</span><span class="sxs-lookup"><span data-stu-id="14f6a-128">**SharePoint administrator** has administrative access tooSharePoint Online through hello SharePoint Online admin center, and can perform almost any task in SharePoint Online.</span></span>
* <span data-ttu-id="14f6a-129">**商務系統管理員的 Skype** hello Skype 的商務系統管理中心，透過具有商務的系統管理存取權 tooSkype，可以幾乎任何工作在執行 Skype for Business Online。</span><span class="sxs-lookup"><span data-stu-id="14f6a-129">**Skype for Business administrator** has administrative access tooSkype for Business through hello Skype for Business admin center, and can perform almost any task in Skype for Business Online.</span></span>

<span data-ttu-id="14f6a-130">如需有關[在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)和[在 Office 365 中指派管理員角色](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504)的更多詳細資料，請閱讀這些文章。</span><span class="sxs-lookup"><span data-stu-id="14f6a-130">Read these articles for more details about [assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) and [assigning admin roles in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).</span></span>

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


<span data-ttu-id="14f6a-131">您可以從 PIM，[指派給這些角色 tooa 使用者](active-directory-privileged-identity-management-how-to-add-role-to-user.md)如此 hello 使用者[啟用 hello 角色在需要時](active-directory-privileged-identity-management-how-to-activate-role.md)。</span><span class="sxs-lookup"><span data-stu-id="14f6a-131">From PIM, you can [assign these roles tooa user](active-directory-privileged-identity-management-how-to-add-role-to-user.md) so that hello user can [activate hello role when needed](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

<span data-ttu-id="14f6a-132">如果您想 toogive PIM 本身，PIM 需要 hello 使用者 toohave 會進一步說明中的 hello 角色中的另一個使用者存取 toomanage [toogive 如何存取 tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。</span><span class="sxs-lookup"><span data-stu-id="14f6a-132">If you want toogive another user access toomanage in PIM itself, hello roles which PIM requires hello user toohave are described further in [how toogive access tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a><span data-ttu-id="14f6a-133">PIM 中未管理的角色</span><span class="sxs-lookup"><span data-stu-id="14f6a-133">Roles not managed in PIM</span></span>
<span data-ttu-id="14f6a-134">Exchange Online 或 SharePoint Online 內的角色 (除了前面提及的角色外) 並不會出現在 Azure AD 中，因此您不會在 PIM 中看到。</span><span class="sxs-lookup"><span data-stu-id="14f6a-134">Roles within Exchange Online or SharePoint Online, except for those mentioned above, are not represented in Azure AD and so are not visible in PIM.</span></span> <span data-ttu-id="14f6a-135">如需有關在這些 Office 365 服務中變更細部角色指派的詳細資訊，請參閱 [Office 365 中的權限](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d)。</span><span class="sxs-lookup"><span data-stu-id="14f6a-135">For more information on changing fine-grained role assignments in these Office 365 services, see [Permissions in Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).</span></span>

<span data-ttu-id="14f6a-136">Azure 訂用帳戶和資源群組也不會出現在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="14f6a-136">Azure subscriptions and resource groups are also not represented in Azure AD.</span></span> <span data-ttu-id="14f6a-137">toomanage Azure 訂用帳戶，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)，如需有關 Azure rbac 進行，請參閱[所有存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="14f6a-137">toomanage Azure subscriptions, see [How tooadd or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md) and for more information on Azure RBAC see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a><span data-ttu-id="14f6a-138">使用者角色和登入</span><span class="sxs-lookup"><span data-stu-id="14f6a-138">User roles and signing in</span></span>
<span data-ttu-id="14f6a-139">某些 Microsoft 服務和應用程式，將使用者 tooa 角色指派可能不是足夠 tooenable 該使用者 toobe 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="14f6a-139">For some Microsoft services and applications, assigning a user tooa role may not be sufficient tooenable that user toobe an administrator.</span></span>

<span data-ttu-id="14f6a-140">存取 toohello Azure 傳統入口網站需要 hello 使用者是服務系統管理員或 Azure 訂用帳戶的共同管理員，即使 hello 使用者不需要 toomanage hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="14f6a-140">Access toohello Azure classic portal requires hello user be a service administrator or co-administrator on an Azure subscription, even if hello user does not need toomanage hello Azure subscriptions.</span></span>  <span data-ttu-id="14f6a-141">例如，toomanage hello 傳統入口網站，使用者在 Azure AD 的組態設定必須是 Azure AD 中的全域管理員和 Azure 訂用帳戶的訂用帳戶共同管理員。</span><span class="sxs-lookup"><span data-stu-id="14f6a-141">For example, toomanage configuration settings for Azure AD in hello classic portal, a user must be both a global administrator in Azure AD and a subscription co-administrator on an Azure subscription.</span></span>  <span data-ttu-id="14f6a-142">如何 tooadd 使用者 tooAzure 訂用帳戶，請參閱的 toolearn[如何 tooadd 或變更的 Azure 系統管理員角色](../billing/billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="14f6a-142">toolearn how tooadd users tooAzure subscriptions, see [How tooadd or change Azure administrator roles](../billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="14f6a-143">線上服務可能需要存取 tooMicrosoft hello 也為使用者指派授權才能開啟 hello 服務入口網站或執行系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="14f6a-143">Access tooMicrosoft Online Services may require hello user also be assigned a license before they can open hello service's portal or perform administrative tasks.</span></span>

## <a name="assign-a-license-tooa-user-in-azure-ad"></a><span data-ttu-id="14f6a-144">在 Azure AD 中指派給授權 tooa 使用者</span><span class="sxs-lookup"><span data-stu-id="14f6a-144">Assign a license tooa user in Azure AD</span></span>
1. <span data-ttu-id="14f6a-145">登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com)與全域管理員帳戶或共同管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="14f6a-145">Sign in toohello [Azure classic portal](http://manage.windowsazure.com) with a global administrator account or a co-administrator account.</span></span>
2. <span data-ttu-id="14f6a-146">選取**所有項目**從 hello 主功能表。</span><span class="sxs-lookup"><span data-stu-id="14f6a-146">Select **All Items** from hello main menu.</span></span>
3. <span data-ttu-id="14f6a-147">選取您想要與 toowork 和，具有授權與其相關聯的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="14f6a-147">Select hello directory you want toowork with and that has licenses associated with it.</span></span>
4. <span data-ttu-id="14f6a-148">選取 [授權] 。</span><span class="sxs-lookup"><span data-stu-id="14f6a-148">Select **Licenses**.</span></span> <span data-ttu-id="14f6a-149">可用的授權 hello 清單會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="14f6a-149">hello list of available licenses will appear.</span></span>
5. <span data-ttu-id="14f6a-150">選取包含您想 toodistribute hello 授權 hello 授權計劃。</span><span class="sxs-lookup"><span data-stu-id="14f6a-150">Select hello license plan which contains hello licenses that you want toodistribute.</span></span>
6. <span data-ttu-id="14f6a-151">選取 [指派使用者] 。</span><span class="sxs-lookup"><span data-stu-id="14f6a-151">Select **Assign Users**.</span></span>
7. <span data-ttu-id="14f6a-152">選取 hello 使用者想授權 tooassign 至。</span><span class="sxs-lookup"><span data-stu-id="14f6a-152">Select hello user that you want tooassign a license to.</span></span>
8. <span data-ttu-id="14f6a-153">按一下 hello**指派**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="14f6a-153">Click hello **Assign** button.</span></span>  <span data-ttu-id="14f6a-154">hello 使用者現在可以登入 tooAzure 中。</span><span class="sxs-lookup"><span data-stu-id="14f6a-154">hello user can now sign in tooAzure.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="14f6a-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14f6a-155">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

