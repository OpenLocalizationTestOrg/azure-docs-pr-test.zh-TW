---
title: "在 Azure Active Directory 中檢視我可以管理的所有企業應用程式 |Microsoft Docs"
description: "如何在 Azure Active Directory 中查看您具備管理權限的企業應用程式清單"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: c4fb6f94-34f8-4323-8bd7-a3ee44901f7d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 14b335d14d893640d469508d6f34b4e7ec6bee8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-all-the-enterprise-apps-that-i-can-manage-in-azure-active-directory"></a><span data-ttu-id="ed7f8-103">在 Azure Active Directory 中檢視我可以管理的所有企業應用程式</span><span class="sxs-lookup"><span data-stu-id="ed7f8-103">View all the enterprise apps that I can manage in Azure Active Directory</span></span>
<span data-ttu-id="ed7f8-104">您可以在 Azure Active Directory (Azure AD) 中，管理您的企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed7f8-104">You can manage your enterprise applications in the Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ed7f8-105">這包括檢視您可以管理的應用程式、將使用者或群組指派給應用程式、維護應用程式的屬性 (例如應用程式名稱/標誌)，甚至是停用應用程式，讓任何使用者都無法登入。</span><span class="sxs-lookup"><span data-stu-id="ed7f8-105">This includes viewing the apps you can manage, assigning users or groups to an app, maintaining properties for the app such as the application name/logo, and even disabling an application so that no users can sign in to it.</span></span>

## <a name="how-do-i-view-all-my-apps"></a><span data-ttu-id="ed7f8-106">如何檢視我的所有應用程式？</span><span class="sxs-lookup"><span data-stu-id="ed7f8-106">How do I view all my apps?</span></span>
1. <span data-ttu-id="ed7f8-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="ed7f8-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="ed7f8-108">選取 [更多服務]，在文字方塊中輸入 **Azure Active Directory**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="ed7f8-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="ed7f8-109">在 [Azure Active Directory - ***directoryname***] 刀鋒視窗 (也就是您所管理目錄的 Azure AD 刀鋒視窗) 上，選取 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed7f8-109">On the **Azure Active Directory -** ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![開啟企業應用程式](./media/active-directory-coreapps-view-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="ed7f8-111">在 [企業應用程式] 刀鋒視窗上，選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed7f8-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="ed7f8-112">從這個刀鋒視窗中，您可以選取要管理的應用程式、變更顯示的資料行，或篩選清單以尋找您想要的應用程式 (例如，只檢視已停用的應用程式)。</span><span class="sxs-lookup"><span data-stu-id="ed7f8-112">From this blade you can select apps to manage, change the displayed columns, or filter the list to find that app you want (for example, to view only disabled apps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed7f8-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed7f8-113">Next steps</span></span>
* [<span data-ttu-id="ed7f8-114">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="ed7f8-114">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="ed7f8-115">從企業應用程式中移除使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="ed7f8-115">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="ed7f8-116">停用企業應用程式的使用者登入</span><span class="sxs-lookup"><span data-stu-id="ed7f8-116">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="ed7f8-117">變更企業應用程式的名稱或標誌</span><span class="sxs-lookup"><span data-stu-id="ed7f8-117">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
