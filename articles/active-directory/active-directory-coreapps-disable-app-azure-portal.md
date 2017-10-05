---
title: "在 Azure Active Directory 中停用企業應用程式的使用者登入 | Microsoft Docs"
description: "如何在 Azure Active Directory 中停用企業應用程式，讓任何使用者都無法登入它"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="b8e4a-103">在 Azure Active Directory 中停用企業應用程式的使用者登入</span><span class="sxs-lookup"><span data-stu-id="b8e4a-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="b8e4a-104">在 Azure Active Directory (Azure AD) 中，您可以輕鬆停用企業應用程式，讓任何使用者都無法登入它。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b8e4a-105">您必須具備適當的權限，才能管理企業應用程式，而且必須是目錄的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="b8e4a-106">如何停用使用者登入？</span><span class="sxs-lookup"><span data-stu-id="b8e4a-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="b8e4a-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="b8e4a-108">選取 [更多服務]，在文字方塊中輸入 **Azure Active Directory**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="b8e4a-109">在 [Azure Active Directory -  directoryname] 刀鋒視窗 (也就是您所管理目錄的 Azure AD 刀鋒視窗) 上，選取 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![開啟企業應用程式](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="b8e4a-111">在 [企業應用程式] 刀鋒視窗上，選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="b8e4a-112">您會看到一份您可以管理的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="b8e4a-113">在 [企業應用程式 - 所有應用程式]  刀鋒視窗上，選取一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="b8e4a-114">在 [appname] 刀鋒視窗 (亦即標題中含有所選應用程式名稱的刀鋒視窗) 上，選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![選取所有應用程式命令](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="b8e4a-116">在 [appname - 屬性] 刀鋒視窗上，針對 [啟用以讓使用者登入?] 選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="b8e4a-117">選取 [儲存]  命令。</span><span class="sxs-lookup"><span data-stu-id="b8e4a-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8e4a-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8e4a-118">Next steps</span></span>
* [<span data-ttu-id="b8e4a-119">查看我的所有群組</span><span class="sxs-lookup"><span data-stu-id="b8e4a-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="b8e4a-120">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="b8e4a-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="b8e4a-121">從企業應用程式中移除使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="b8e4a-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="b8e4a-122">變更企業應用程式的名稱或標誌</span><span class="sxs-lookup"><span data-stu-id="b8e4a-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
