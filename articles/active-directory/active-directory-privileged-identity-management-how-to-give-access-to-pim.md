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
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="54cf9-103">提供存取 toomanage Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="54cf9-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="54cf9-104">hello 全域系統管理員可讓 Azure AD Privileged Identity Management (PIM) 的組織自動取得角色指派，並存取 tooPIM。</span><span class="sxs-lookup"><span data-stu-id="54cf9-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="54cf9-105">不過，預設不會有任何其他人取得寫入存取權，包括其他全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="54cf9-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="54cf9-106">其他全域管理員、 安全性系統管理員和安全性的讀取器具有唯讀存取 tooAzure AD PIM。</span><span class="sxs-lookup"><span data-stu-id="54cf9-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="54cf9-107">toogive 存取 tooPIM，hello 第一個使用者可以指派給其他人 toohello**特殊權限的角色管理員**角色。</span><span class="sxs-lookup"><span data-stu-id="54cf9-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="54cf9-108">這項指派必須在 PIM 內完成，而且無法透過 PowerShell 或其他入口網站變更。</span><span class="sxs-lookup"><span data-stu-id="54cf9-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="54cf9-109">管理 Azure AD PIM 需要 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="54cf9-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="54cf9-110">因為 Microsoft 帳戶無法註冊 Azure MFA，所以使用 Microsoft 帳戶登入的使用者無法存取 Azure AD PIM。</span><span class="sxs-lookup"><span data-stu-id="54cf9-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="54cf9-111">請確保特殊權限角色管理員角色中永遠至少有兩位使用者，以防一位使用者遭到鎖定或他們的帳戶遭刪除。</span><span class="sxs-lookup"><span data-stu-id="54cf9-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="54cf9-112">授與其他使用者存取 toomanage PIM</span><span class="sxs-lookup"><span data-stu-id="54cf9-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="54cf9-113">登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello **Azure AD Privileged Identity Management** hello 儀表板上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="54cf9-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="54cf9-114">選取 [管理特殊權限角色]  >  [特殊權限角色管理員]  >  [新增]。</span><span class="sxs-lookup"><span data-stu-id="54cf9-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![新增特殊權限角色管理員 - 螢幕擷取畫面][1]
3. <span data-ttu-id="54cf9-116">Hello 新增受管理的使用者 刀鋒視窗，在步驟 1 已完成。</span><span class="sxs-lookup"><span data-stu-id="54cf9-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="54cf9-117">選取步驟 2，**選取使用者**並搜尋您想 tooadd hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="54cf9-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![選取使用者 - 螢幕擷取畫面][2]
4. <span data-ttu-id="54cf9-119">從 hello 搜尋結果中，選取 hello 使用者並按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="54cf9-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="54cf9-120">按一下**確定**toosave 選取項目。</span><span class="sxs-lookup"><span data-stu-id="54cf9-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="54cf9-121">您已選取的 hello 使用者會出現在 hello 特殊權限的角色管理員清單。</span><span class="sxs-lookup"><span data-stu-id="54cf9-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="54cf9-122">每當您指派新的角色 toosomeone，它們會自動設定做為合格 tooactivate hello 角色。</span><span class="sxs-lookup"><span data-stu-id="54cf9-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="54cf9-123">如果您想 toomake 它們永久在 hello 角色中，按一下 hello 清單中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="54cf9-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="54cf9-124">選取**進行權限**hello 使用者資訊 功能表中。</span><span class="sxs-lookup"><span data-stu-id="54cf9-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="54cf9-125">傳送 hello 的連結使用者太[開始使用 Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="54cf9-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="54cf9-126">移除其他使用者管理 PIM 的存取權限</span><span class="sxs-lookup"><span data-stu-id="54cf9-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="54cf9-127">有人 hello 特殊權限的角色系統管理員角色中移除之前，請務必確定仍會指派 tooit 的兩個使用者。</span><span class="sxs-lookup"><span data-stu-id="54cf9-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="54cf9-128">Hello PIM 儀表板中按一下 hello 角色**特殊權限的角色管理員**。</span><span class="sxs-lookup"><span data-stu-id="54cf9-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="54cf9-129">將顯示 hello 目前在該角色中的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="54cf9-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="54cf9-130">按一下 hello hello 使用者清單中的使用者。</span><span class="sxs-lookup"><span data-stu-id="54cf9-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="54cf9-131">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="54cf9-131">Click on **Remove**.</span></span>  <span data-ttu-id="54cf9-132">您將會看到確認訊息。</span><span class="sxs-lookup"><span data-stu-id="54cf9-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="54cf9-133">按一下**是**tooremove hello 使用者從 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="54cf9-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="54cf9-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54cf9-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
