---
title: "如何新增或移除使用者角色 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory Privileged Identity Management 應用程式來將角色新增到特殊權限身分識別。"
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
ms.openlocfilehash: 3ac07bb7b070f44595c099a454b3d0dbc66126c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-privileged-identity-management-how-to-add-or-remove-a-user-role"></a><span data-ttu-id="91d66-103">Azure AD Privileged Identity Management：如何新增或移除使用者角色</span><span class="sxs-lookup"><span data-stu-id="91d66-103">Azure AD Privileged Identity Management: How to add or remove a user role</span></span>
<span data-ttu-id="91d66-104">使用 Azure Active Directory (AD)，全域系統管理員 (或公司系統管理員) 可以更新哪些使用者獲 **永久** 指派 Azure AD 的角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned to roles in Azure AD.</span></span> <span data-ttu-id="91d66-105">做法是使用 PowerShell Cmdlet，如 `Add-MsolRoleMember` 和 `Remove-MsolRoleMember`。</span><span class="sxs-lookup"><span data-stu-id="91d66-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="91d66-106">或者可以依 [在 Azure Active Directory (Azure AD) 中指派系統管理員角色](active-directory-assign-admin-roles.md)中所述，使用 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="91d66-106">Or they can use the Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="91d66-107">Azure AD Privileged Identity Management 應用程式也允許特殊權限角色管理員指派永久的角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-107">The Azure AD Privileged Identity Management application allows privileged role administrators to make permanent role assignments, as well.</span></span> <span data-ttu-id="91d66-108">此外，特殊權限角色系統管理員可以讓使用者 **有資格**扮演系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="91d66-109">合格系統管理員可在需要時啟用角色，而在完成工作之後，其權限就隨即失效。</span><span class="sxs-lookup"><span data-stu-id="91d66-109">An eligible admin can activate the role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-the-azure-portal"></a><span data-ttu-id="91d66-110">在 Azure 入口網站管理使用 PIM 的角色</span><span class="sxs-lookup"><span data-stu-id="91d66-110">Manage roles with PIM in the Azure portal</span></span>
<span data-ttu-id="91d66-111">在您的組織中，您可以將使用者指派給 Azure AD、Office 365 及其他 Microsoft 服務和應用程式中不同的系統管理角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-111">In your organization, you can assign users to different administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="91d66-112">如需可用角色的詳細資訊，請參閱 [Azure AD PIM 中的角色](active-directory-privileged-identity-management-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="91d66-112">More details on the available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="91d66-113">若要新增或移除使用者使用 Privileged Identity Management 的角色，請啟動 PIM 儀表板。</span><span class="sxs-lookup"><span data-stu-id="91d66-113">To add or remove a user in a role using Privileged Identity Management, bring up the PIM dashboard.</span></span> <span data-ttu-id="91d66-114">然後按一下 [系統管理員角色的使用者]  按鈕，或從角色資料表中選取特定角色 (例如全域系統管理員)。</span><span class="sxs-lookup"><span data-stu-id="91d66-114">Then either click the **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from the roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="91d66-115">如果您還沒有在 Azure 入口網站中啟用 PIM，請移至 [開始使用 Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="91d66-115">If you haven't enabled PIM in the Azure portal yet, go to [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="91d66-116">如果您想要讓其他使用者存取 PIM 本身，請參閱 [How to give access to manage Azure AD Privileged Identity Management (如何提供管理  Azure AD Privileged Identity Management 的存取權)](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)，進一步了解 PIM 需要使用者具有哪些角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-116">If you want to give another user access to PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-to-a-role"></a><span data-ttu-id="91d66-117">將使用者新增至角色</span><span class="sxs-lookup"><span data-stu-id="91d66-117">Add a user to a role</span></span>
1. <span data-ttu-id="91d66-118">在 [Azure 入口網站](https://portal.azure.com/)中，於儀表板上選取 [Azure AD Privileged Identity Management] 圖格。</span><span class="sxs-lookup"><span data-stu-id="91d66-118">In the [Azure portal](https://portal.azure.com/), select the **Azure AD Privileged Identity Management** tile on the dashboard.</span></span>
2. <span data-ttu-id="91d66-119">選取 [管理特殊權限角色] 。</span><span class="sxs-lookup"><span data-stu-id="91d66-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="91d66-120">在 [角色摘要]  表格中，選取您想要管理的角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-120">In the **Role summary** table, select the role you want to manage.</span></span>
4. <span data-ttu-id="91d66-121">在 [角色] 刀鋒視窗中，選取 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="91d66-121">In the role blade, select **Add**.</span></span>
5. <span data-ttu-id="91d66-122">按一下 [選取使用者]，然後在 [選取使用者] 刀鋒視窗上搜尋使用者。</span><span class="sxs-lookup"><span data-stu-id="91d66-122">Click **Select users** and search for the user on the **Select users** blade.</span></span>  
6. <span data-ttu-id="91d66-123">從搜尋結果清單中選取使用者，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="91d66-123">Select the user from the search results list, and click **Done**.</span></span>
7. <span data-ttu-id="91d66-124">按一下 [確定]  以儲存您的選取項目。</span><span class="sxs-lookup"><span data-stu-id="91d66-124">Click **OK** to save your selection.</span></span> <span data-ttu-id="91d66-125">您已選取的使用者將會在清單中顯示為該角色的合格使用者。</span><span class="sxs-lookup"><span data-stu-id="91d66-125">The user you have selected will appear in the list as eligible for the role.</span></span>

> [!NOTE]
> <span data-ttu-id="91d66-126">角色中的新使用者預設僅是該角色的合格使用者。</span><span class="sxs-lookup"><span data-stu-id="91d66-126">New users in a role are only eligible for the role by default.</span></span> <span data-ttu-id="91d66-127">如果想要讓角色變成永久，請按一下清單中的使用者。</span><span class="sxs-lookup"><span data-stu-id="91d66-127">If you want to make the role permanent, click the user in the list.</span></span> <span data-ttu-id="91d66-128">該使用者的資訊即會出現在新的刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="91d66-128">The user's information will appear in a new blade.</span></span> <span data-ttu-id="91d66-129">在使用者資訊功能表中，選取 [設為永久]  。</span><span class="sxs-lookup"><span data-stu-id="91d66-129">Select **Make perm** in the user information menu.</span></span>  
> <span data-ttu-id="91d66-130">如果使用者無法註冊的 Azure Multi-factor Authentication (MFA)，或使用 Microsoft 帳戶 (通常@outlook.com)，您需要自行永久的所有角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span></span> <span data-ttu-id="91d66-131">系統會要求合格系統管理員在啟用啟用期間註冊 MFA。</span><span class="sxs-lookup"><span data-stu-id="91d66-131">Eligible admins are asked to register for MFA during activation.</span></span>

<span data-ttu-id="91d66-132">既然使用者有資格扮演某個角色，請讓他們知道他們可以根據[如何啟用或停用角色](active-directory-privileged-identity-management-how-to-activate-role.md)中的指示來啟用角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-132">Now that the user is eligible for a role, let them know that they can activate it according to the instructions in [How to activate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="91d66-133">從角色移除使用者</span><span class="sxs-lookup"><span data-stu-id="91d66-133">Remove a user from a role</span></span>
<span data-ttu-id="91d66-134">您可以將使用者從合格角色指派中移除，但請務必一律至少保留一個永久全域系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="91d66-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="91d66-135">請遵循下列步驟移除角色中的特定使用者︰</span><span class="sxs-lookup"><span data-stu-id="91d66-135">Follow these steps to remove a specific user from a role:</span></span>

1. <span data-ttu-id="91d66-136">在 Azure AD PIM 儀表板中選取一個角色，或按一下 [系統管理員角色的使用者]  按鈕，來瀏覽至角色清單中的角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-136">Navigate to the role in the role list either by selecting a role in the Azure AD PIM dashboard or by clicking on the **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="91d66-137">按一下使用者清單中的使用者。</span><span class="sxs-lookup"><span data-stu-id="91d66-137">Click on the user in the user list.</span></span>
3. <span data-ttu-id="91d66-138">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="91d66-138">Click **Remove**.</span></span> <span data-ttu-id="91d66-139">會出現訊息要求您確認。</span><span class="sxs-lookup"><span data-stu-id="91d66-139">A message will ask you to confirm.</span></span>
4. <span data-ttu-id="91d66-140">按一下 [是]  ，即可從使用者中移除角色。</span><span class="sxs-lookup"><span data-stu-id="91d66-140">Click **Yes** to remove the role from the user.</span></span>

<span data-ttu-id="91d66-141">如果您不確定哪些使用者仍然需要其角色指派，您可以 [開始角色的存取權檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="91d66-141">If you're not sure which users still need their role assignments, then you can [start an access review for the role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91d66-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91d66-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

