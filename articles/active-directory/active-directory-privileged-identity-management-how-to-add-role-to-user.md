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
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a><span data-ttu-id="c93e8-103">Azure 的 AD Privileged Identity Management： 如何 tooadd 或移除使用者角色</span><span class="sxs-lookup"><span data-stu-id="c93e8-103">Azure AD Privileged Identity Management: How tooadd or remove a user role</span></span>
<span data-ttu-id="c93e8-104">使用 Azure Active Directory (AD)，全域系統管理員 （或公司系統管理員） 可以更新哪些使用者**永久**tooroles 指派 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c93e8-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned tooroles in Azure AD.</span></span> <span data-ttu-id="c93e8-105">做法是使用 PowerShell Cmdlet，如 `Add-MsolRoleMember` 和 `Remove-MsolRoleMember`。</span><span class="sxs-lookup"><span data-stu-id="c93e8-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="c93e8-106">中所述，也可以使用 Azure 傳統入口網站 hello[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="c93e8-106">Or they can use hello Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="c93e8-107">hello Azure AD Privileged Identity Management 的應用程式可讓 toomake 永久的角色指派，以及特殊權限的角色系統管理員。</span><span class="sxs-lookup"><span data-stu-id="c93e8-107">hello Azure AD Privileged Identity Management application allows privileged role administrators toomake permanent role assignments, as well.</span></span> <span data-ttu-id="c93e8-108">此外，特殊權限角色系統管理員可以讓使用者 **有資格**扮演系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="c93e8-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="c93e8-109">當他們需要它，而且一旦完成後及其權限到期。 然後，合格的系統管理員可以啟動 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="c93e8-109">An eligible admin can activate hello role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a><span data-ttu-id="c93e8-110">管理與 PIM hello Azure 入口網站中的角色</span><span class="sxs-lookup"><span data-stu-id="c93e8-110">Manage roles with PIM in hello Azure portal</span></span>
<span data-ttu-id="c93e8-111">在您組織中，您可以指定使用者 toodifferent 系統管理角色在 Azure AD 中，Office 365，及其他 Microsoft 服務和應用程式。</span><span class="sxs-lookup"><span data-stu-id="c93e8-111">In your organization, you can assign users toodifferent administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="c93e8-112">需 hello 可用角色的詳細資訊，請參閱[角色在 Azure AD PIM](active-directory-privileged-identity-management-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="c93e8-112">More details on hello available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="c93e8-113">tooadd] 或 [移除角色，使用 Privileged Identity Management 的使用者顯示 hello PIM 儀表板。</span><span class="sxs-lookup"><span data-stu-id="c93e8-113">tooadd or remove a user in a role using Privileged Identity Management, bring up hello PIM dashboard.</span></span> <span data-ttu-id="c93e8-114">然後按一下 hello**中系統管理員角色的使用者**按鈕，或選取特定的角色 （例如全域系統管理員） 從 hello roles 資料表。</span><span class="sxs-lookup"><span data-stu-id="c93e8-114">Then either click hello **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from hello roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="c93e8-115">如果您尚未啟用 PIM hello Azure 入口網站中尚未，請移至太[開始使用 Azure AD PIM](active-directory-privileged-identity-management-getting-started.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c93e8-115">If you haven't enabled PIM in hello Azure portal yet, go too[Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="c93e8-116">如果您想 toogive PIM 需要 hello 使用者 toohave 會進一步說明中的 hello 角色本身的其他使用者存取 tooPIM [toogive 如何存取 tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。</span><span class="sxs-lookup"><span data-stu-id="c93e8-116">If you want toogive another user access tooPIM itself, hello roles which PIM requires hello user toohave are described further in [how toogive access tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-tooa-role"></a><span data-ttu-id="c93e8-117">新增使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="c93e8-117">Add a user tooa role</span></span>
1. <span data-ttu-id="c93e8-118">在 hello [Azure 入口網站](https://portal.azure.com/)，選取 hello **Azure AD Privileged Identity Management** hello 儀表板上的磚。</span><span class="sxs-lookup"><span data-stu-id="c93e8-118">In hello [Azure portal](https://portal.azure.com/), select hello **Azure AD Privileged Identity Management** tile on hello dashboard.</span></span>
2. <span data-ttu-id="c93e8-119">選取 [管理特殊權限角色] 。</span><span class="sxs-lookup"><span data-stu-id="c93e8-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="c93e8-120">在 hello**角色摘要**資料表，您想要 toomanage 選取 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="c93e8-120">In hello **Role summary** table, select hello role you want toomanage.</span></span>
4. <span data-ttu-id="c93e8-121">在 hello 角色 刀鋒視窗中，選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="c93e8-121">In hello role blade, select **Add**.</span></span>
5. <span data-ttu-id="c93e8-122">按一下**選取使用者**，並搜尋 hello hello 使用者**選取使用者**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c93e8-122">Click **Select users** and search for hello user on hello **Select users** blade.</span></span>  
6. <span data-ttu-id="c93e8-123">從 hello 搜尋結果清單中，選取 hello 使用者並按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="c93e8-123">Select hello user from hello search results list, and click **Done**.</span></span>
7. <span data-ttu-id="c93e8-124">按一下**確定**toosave 選取項目。</span><span class="sxs-lookup"><span data-stu-id="c93e8-124">Click **OK** toosave your selection.</span></span> <span data-ttu-id="c93e8-125">您已選取的 hello 使用者會出現在 hello 適合 hello 角色清單。</span><span class="sxs-lookup"><span data-stu-id="c93e8-125">hello user you have selected will appear in hello list as eligible for hello role.</span></span>

> [!NOTE]
> <span data-ttu-id="c93e8-126">角色中的新使用者，才適合 hello 預設的角色。</span><span class="sxs-lookup"><span data-stu-id="c93e8-126">New users in a role are only eligible for hello role by default.</span></span> <span data-ttu-id="c93e8-127">如果您想永久 toomake hello 角色，請按一下 [hello] 清單中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="c93e8-127">If you want toomake hello role permanent, click hello user in hello list.</span></span> <span data-ttu-id="c93e8-128">hello 使用者的資訊會出現在新的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c93e8-128">hello user's information will appear in a new blade.</span></span> <span data-ttu-id="c93e8-129">選取**讓權限**hello 使用者資訊 功能表中。</span><span class="sxs-lookup"><span data-stu-id="c93e8-129">Select **Make perm** in hello user information menu.</span></span>  
> <span data-ttu-id="c93e8-130">如果使用者無法註冊的 Azure Multi-factor Authentication (MFA)，或使用 Microsoft 帳戶 (通常@outlook.com)，您需要 toomake 它們永久的所有角色。</span><span class="sxs-lookup"><span data-stu-id="c93e8-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need toomake them permanent in all their roles.</span></span> <span data-ttu-id="c93e8-131">符合資格的系統管理員 」 會詢問在啟用期間 tooregister MFA。</span><span class="sxs-lookup"><span data-stu-id="c93e8-131">Eligible admins are asked tooregister for MFA during activation.</span></span>

<span data-ttu-id="c93e8-132">既然 hello 使用者有資格的角色，讓他們知道他們可以啟動它，根據 toohello 指示[如何 tooactivate 或停用角色](active-directory-privileged-identity-management-how-to-activate-role.md)。</span><span class="sxs-lookup"><span data-stu-id="c93e8-132">Now that hello user is eligible for a role, let them know that they can activate it according toohello instructions in [How tooactivate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="c93e8-133">從角色移除使用者</span><span class="sxs-lookup"><span data-stu-id="c93e8-133">Remove a user from a role</span></span>
<span data-ttu-id="c93e8-134">您可以將使用者從合格角色指派中移除，但請務必一律至少保留一個永久全域系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="c93e8-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="c93e8-135">從角色，請遵循這些步驟 tooremove 特定的使用者：</span><span class="sxs-lookup"><span data-stu-id="c93e8-135">Follow these steps tooremove a specific user from a role:</span></span>

1. <span data-ttu-id="c93e8-136">瀏覽 toohello 角色 hello 角色清單中的，選取 hello Azure AD PIM 儀表板中的角色，或是按一下 hello**中系統管理員角色的使用者** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c93e8-136">Navigate toohello role in hello role list either by selecting a role in hello Azure AD PIM dashboard or by clicking on hello **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="c93e8-137">按一下 hello hello 使用者清單中的使用者。</span><span class="sxs-lookup"><span data-stu-id="c93e8-137">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="c93e8-138">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="c93e8-138">Click **Remove**.</span></span> <span data-ttu-id="c93e8-139">訊息會要求您 tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="c93e8-139">A message will ask you tooconfirm.</span></span>
4. <span data-ttu-id="c93e8-140">按一下**是**tooremove hello hello 使用者角色。</span><span class="sxs-lookup"><span data-stu-id="c93e8-140">Click **Yes** tooremove hello role from hello user.</span></span>

<span data-ttu-id="c93e8-141">如果您不確定哪些使用者仍然需要其角色指派，則您可以[開始 hello 角色存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="c93e8-141">If you're not sure which users still need their role assignments, then you can [start an access review for hello role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c93e8-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c93e8-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

