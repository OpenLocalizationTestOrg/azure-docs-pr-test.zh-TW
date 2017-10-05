---
title: "在 Azure Active Directory 中從企業應用程式移除使用者或群組指派 | Microsoft Docs"
description: "如何在 Azure Active Directory 中從企業應用程式移除使用者或群組的存取權指派"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="82fee-103">在 Azure Active Directory 中從企業應用程式移除使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="82fee-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="82fee-104">在 Azure Active Directory (Azure AD) 中，針對已獲指派其中一個企業應用程式存取權的使用者或群組，您可以輕鬆移除已指派的存取權。</span><span class="sxs-lookup"><span data-stu-id="82fee-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="82fee-105">您必須具備適當的權限，才能管理企業應用程式，而且必須是目錄的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="82fee-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="82fee-106">如何移除使用者或群組指派？</span><span class="sxs-lookup"><span data-stu-id="82fee-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="82fee-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="82fee-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="82fee-108">選取 [更多服務]，在文字方塊中輸入 **Azure Active Directory**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="82fee-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="82fee-109">在 [Azure Active Directory - directoryname] 刀鋒視窗 (也就是您所管理目錄的 Azure AD 刀鋒視窗) 上，選取 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="82fee-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![開啟企業應用程式](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="82fee-111">在 [企業應用程式] 刀鋒視窗上，選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="82fee-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="82fee-112">您將會看到一份您可以管理的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="82fee-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="82fee-113">在 [企業應用程式 - 所有應用程式]  刀鋒視窗上，選取一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="82fee-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="82fee-114">在 [***appname***] 刀鋒視窗 (亦即標題中含有所選應用程式名稱的刀鋒視窗) 上，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="82fee-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![選取使用者或群組](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="82fee-116">在 [***appname*** - 使用者和群組指派] 刀鋒視窗上，選取一或多個使用者或群組，然後選取 [移除] 命令。</span><span class="sxs-lookup"><span data-stu-id="82fee-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="82fee-117">出現提示時，請確認您的決定。</span><span class="sxs-lookup"><span data-stu-id="82fee-117">Confirm your decision at the prompt.</span></span>

    ![選取 [移除] 命令](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="82fee-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82fee-119">Next steps</span></span>
* [<span data-ttu-id="82fee-120">查看我的所有群組</span><span class="sxs-lookup"><span data-stu-id="82fee-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="82fee-121">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="82fee-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="82fee-122">停用企業應用程式的使用者登入</span><span class="sxs-lookup"><span data-stu-id="82fee-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="82fee-123">變更企業應用程式的名稱或標誌</span><span class="sxs-lookup"><span data-stu-id="82fee-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
