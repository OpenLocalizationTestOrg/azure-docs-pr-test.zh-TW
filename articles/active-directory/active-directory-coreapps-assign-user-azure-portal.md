---
title: "aaaAssign 的使用者或群組 tooan 企業應用程式在 Azure Active Directory |Microsoft 文件"
description: "如何在 Azure Active Directory 使用者或群組 tooit 企業應用程式 tooassign tooselect"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="210bf-103">指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="210bf-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="210bf-104">它是簡單 tooassign 使用者或群組 tooyour 企業應用程式的 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="210bf-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="210bf-105">您必須擁有 hello 適當的權限 toomanage hello 企業應用程式，，您必須是全域管理員的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="210bf-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="210bf-106">如何指派使用者存取 tooan 企業應用程式？</span><span class="sxs-lookup"><span data-stu-id="210bf-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="210bf-107">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="210bf-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="210bf-108">選取**更多服務**，在 [hello] 文字方塊中，輸入 Azure Active Directory，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="210bf-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="210bf-109">在 hello **Azure Active Directory- *directoryname*** 刀鋒視窗 （也就是 hello Azure AD 刀鋒視窗中您所管理的 hello 目錄），選取**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="210bf-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![開啟企業應用程式](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="210bf-111">在 hello**企業應用程式**刀鋒視窗中，選取**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="210bf-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="210bf-112">您會看到一份可以管理的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="210bf-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="210bf-113">在 hello**企業應用程式的所有應用程式**刀鋒視窗中，選取一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="210bf-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="210bf-114">在 hello ***appname***刀鋒視窗 （也就是 hello 刀鋒視窗中的 hello hello 標題中的 hello 選應用程式的名稱），選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="210bf-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![選取 hello 所有應用程式的命令](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="210bf-116">在 hello ***appname*** **-使用者和群組指派**刀鋒視窗中，選取 hello**新增**命令。</span><span class="sxs-lookup"><span data-stu-id="210bf-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="210bf-117">在 hello**將作業加入**刀鋒視窗中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="210bf-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![指派使用者或群組的 toohello 應用程式](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="210bf-119">在 hello**使用者和群組**刀鋒視窗中，選取一或多個使用者或群組從 hello 清單，然後選取 hello**選取**在 hello hello 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="210bf-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="210bf-120">在 hello**將作業加入**刀鋒視窗中，選取**角色**。</span><span class="sxs-lookup"><span data-stu-id="210bf-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="210bf-121">然後，在 hello**選取角色**刀鋒視窗中，選取角色 tooapply toohello 選取使用者或群組，然後選取 hello**確定**在 hello hello 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="210bf-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="210bf-122">在 hello**將作業加入**刀鋒視窗中，選取 hello**指派**在 hello hello 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="210bf-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="210bf-123">hello 指派使用者或群組將具有所選取的角色 hello 這個企業應用程式定義的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="210bf-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="210bf-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="210bf-124">Next steps</span></span>
* [<span data-ttu-id="210bf-125">查看我的所有群組</span><span class="sxs-lookup"><span data-stu-id="210bf-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="210bf-126">從企業應用程式中移除使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="210bf-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="210bf-127">停用企業應用程式的使用者登入</span><span class="sxs-lookup"><span data-stu-id="210bf-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="210bf-128">變更 hello 名稱或企業應用程式的標誌</span><span class="sxs-lookup"><span data-stu-id="210bf-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
