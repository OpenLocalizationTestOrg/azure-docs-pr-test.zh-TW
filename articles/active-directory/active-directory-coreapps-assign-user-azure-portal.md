---
title: "在 Azure Active Directory 中將使用者或群組指派給企業應用程式 | Microsoft Docs"
description: "如何在 Azure Active Directory 中選取企業應用程式以將使用者或群組指派給它"
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
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="d3adc-103">在 Azure Active Directory 中將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="d3adc-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="d3adc-104">在 Azure Active Directory (Azure AD) 中，您可以輕鬆將使用者或群組指派給您的企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3adc-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d3adc-105">您必須具備適當的權限，才能管理企業應用程式，而且必須是目錄的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="d3adc-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="d3adc-106">如何將企業應用程式的存取權指派給使用者？</span><span class="sxs-lookup"><span data-stu-id="d3adc-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="d3adc-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="d3adc-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="d3adc-108">選取 [更多服務]，在文字方塊中輸入 Azure Active Directory，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="d3adc-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="d3adc-109">在 [Azure Active Directory - directoryname] 刀鋒視窗 (也就是您所管理目錄的 Azure AD 刀鋒視窗) 上，選取 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d3adc-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![開啟企業應用程式](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="d3adc-111">在 [企業應用程式] 刀鋒視窗上，選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d3adc-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="d3adc-112">您將會看到一份您可以管理的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d3adc-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="d3adc-113">在 [企業應用程式 - 所有應用程式]  刀鋒視窗上，選取一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3adc-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="d3adc-114">在 [***appname***] 刀鋒視窗 (亦即標題中含有所選應用程式名稱的刀鋒視窗) 上，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d3adc-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![選取所有應用程式命令](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="d3adc-116">在 [***appname*** - 使用者和群組指派] 刀鋒視窗上，選取 [新增] 命令。</span><span class="sxs-lookup"><span data-stu-id="d3adc-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="d3adc-117">在 [新增指派] 刀鋒視窗上，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d3adc-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![將使用者或群組指派給應用程式](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="d3adc-119">在 [使用者和群組] 刀鋒視窗上，從清單中選取一或多個使用者或群組，然後選取刀鋒視窗底部的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3adc-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="d3adc-120">在 [新增指派] 刀鋒視窗上，選取 [角色]。</span><span class="sxs-lookup"><span data-stu-id="d3adc-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="d3adc-121">然後，在 [選取角色] 刀鋒視窗上，選取要套用到所選使用者或群組的角色，然後選取刀鋒視窗底部的 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3adc-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="d3adc-122">在 [新增指派] 刀鋒視窗上，選取刀鋒視窗底部的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d3adc-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="d3adc-123">受指派的使用者或群組將會具備此企業應用程式的所選角色所定義的權限。</span><span class="sxs-lookup"><span data-stu-id="d3adc-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3adc-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3adc-124">Next steps</span></span>
* [<span data-ttu-id="d3adc-125">查看我的所有群組</span><span class="sxs-lookup"><span data-stu-id="d3adc-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d3adc-126">從企業應用程式中移除使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="d3adc-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="d3adc-127">停用企業應用程式的使用者登入</span><span class="sxs-lookup"><span data-stu-id="d3adc-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="d3adc-128">變更企業應用程式的名稱或標誌</span><span class="sxs-lookup"><span data-stu-id="d3adc-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
