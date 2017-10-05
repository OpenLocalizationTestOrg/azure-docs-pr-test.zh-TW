---
title: "如何授與對 Privileged Identity Management 的存取權 - Azure | Microsoft Docs"
description: "了解如何使用 Azure Active Directory Privileged Identity Management 擴充功能為使用者加入角色，以便他們可以管理 PIM。"
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
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="e46b1-103">授與存取權以管理 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e46b1-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="e46b1-104">為組織啟用 Azure AD Privileged Identity Management (PIM) 的全域系統管理員會自動取得角色指派及 PIM 的存取權。</span><span class="sxs-lookup"><span data-stu-id="e46b1-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="e46b1-105">不過，預設不會有任何其他人取得寫入存取權，包括其他全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e46b1-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="e46b1-106">其他全域系統管理員、安全性管理員及安全性讀取者具有 Azure AD PIM 的唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="e46b1-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="e46b1-107">若要授與對 PIM 的存取權，第一位使用者可以將其他使用者指派給「特殊權限角色管理員」  角色。</span><span class="sxs-lookup"><span data-stu-id="e46b1-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="e46b1-108">這項指派必須在 PIM 內完成，而且無法透過 PowerShell 或其他入口網站變更。</span><span class="sxs-lookup"><span data-stu-id="e46b1-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="e46b1-109">管理 Azure AD PIM 需要 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="e46b1-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="e46b1-110">因為 Microsoft 帳戶無法註冊 Azure MFA，所以使用 Microsoft 帳戶登入的使用者無法存取 Azure AD PIM。</span><span class="sxs-lookup"><span data-stu-id="e46b1-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="e46b1-111">請確保特殊權限角色管理員角色中永遠至少有兩位使用者，以防一位使用者遭到鎖定或他們的帳戶遭刪除。</span><span class="sxs-lookup"><span data-stu-id="e46b1-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="e46b1-112">授與另一位使用者存取權以管理 PIM</span><span class="sxs-lookup"><span data-stu-id="e46b1-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="e46b1-113">登入 [Azure 入口網站](https://portal.azure.com/)，然後在儀表板上選取 **Azure AD Privileged Identity Management** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e46b1-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="e46b1-114">選取 [管理特殊權限角色]  >  [特殊權限角色管理員]  >  [新增]。</span><span class="sxs-lookup"><span data-stu-id="e46b1-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![新增特殊權限角色管理員 - 螢幕擷取畫面][1]
3. <span data-ttu-id="e46b1-116">在 [新增受管理的使用者] 刀鋒視窗上，步驟 1 已經完成。</span><span class="sxs-lookup"><span data-stu-id="e46b1-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="e46b1-117">請選取步驟 2 [選取使用者]  ，然後搜尋您想要新增的使用者。</span><span class="sxs-lookup"><span data-stu-id="e46b1-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![選取使用者 - 螢幕擷取畫面][2]
4. <span data-ttu-id="e46b1-119">從搜尋結果中選取使用者，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="e46b1-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="e46b1-120">按一下 [確定]  以儲存您的選取項目。</span><span class="sxs-lookup"><span data-stu-id="e46b1-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="e46b1-121">您選取的使用者將會出現在特殊權限角色管理員清單中。</span><span class="sxs-lookup"><span data-stu-id="e46b1-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="e46b1-122">每當您指派新角色給某位使用者時，系統都會自動將他們設定成符合啟用該角色的資格。</span><span class="sxs-lookup"><span data-stu-id="e46b1-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="e46b1-123">如果您想要將使用者在該角色中設為永久，請按一下清單中的該使用者。</span><span class="sxs-lookup"><span data-stu-id="e46b1-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="e46b1-124">在使用者資訊功能表中選取 [設為永久]  。</span><span class="sxs-lookup"><span data-stu-id="e46b1-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="e46b1-125">將 [開始使用 Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)連結傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="e46b1-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="e46b1-126">移除其他使用者管理 PIM 的存取權限</span><span class="sxs-lookup"><span data-stu-id="e46b1-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="e46b1-127">將某人自特殊權限角色管理員角色移除之前，請確保該角色仍有兩位指派的使用者。</span><span class="sxs-lookup"><span data-stu-id="e46b1-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="e46b1-128">在 PIM 儀表板中，按一下 [特殊權限角色管理員] 角色。</span><span class="sxs-lookup"><span data-stu-id="e46b1-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="e46b1-129">該角色的目前使用者清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="e46b1-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="e46b1-130">按一下使用者清單中的使用者。</span><span class="sxs-lookup"><span data-stu-id="e46b1-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="e46b1-131">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="e46b1-131">Click on **Remove**.</span></span>  <span data-ttu-id="e46b1-132">您將會看到確認訊息。</span><span class="sxs-lookup"><span data-stu-id="e46b1-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="e46b1-133">按一下 [是]  以將使用者從角色中移除。</span><span class="sxs-lookup"><span data-stu-id="e46b1-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="e46b1-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e46b1-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
