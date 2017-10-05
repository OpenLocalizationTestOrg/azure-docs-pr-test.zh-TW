---
title: "在 Azure Active Directory 中變更企業應用程式的名稱或標誌 | Microsoft Docs"
description: "如何在 Azure Active Directory 中變更自訂企業應用程式的名稱或標誌"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="45bd2-103">在 Azure Active Directory 中變更企業應用程式的名稱或標誌</span><span class="sxs-lookup"><span data-stu-id="45bd2-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="45bd2-104">在 Azure Active Directory (Azure AD) 中，您可以輕鬆變更自訂企業應用程式的名稱或標誌。</span><span class="sxs-lookup"><span data-stu-id="45bd2-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="45bd2-105">您必須具備適當的權限，才能進行這些變更，而且必須是自訂應用程式的建立者。</span><span class="sxs-lookup"><span data-stu-id="45bd2-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="45bd2-106">如何變更企業應用程式的名稱或標誌？</span><span class="sxs-lookup"><span data-stu-id="45bd2-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="45bd2-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="45bd2-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="45bd2-108">選取 [更多服務]，在文字方塊中輸入 **Azure Active Directory**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="45bd2-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="45bd2-109">在 [Azure Active Directory - directoryname] 刀鋒視窗 (也就是您所管理目錄的 Azure AD 刀鋒視窗) 上，選取 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="45bd2-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![開啟企業應用程式](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="45bd2-111">在 [企業應用程式] 刀鋒視窗上，選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="45bd2-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="45bd2-112">您將會看到一份您可以管理的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="45bd2-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="45bd2-113">在 [企業應用程式 - 所有應用程式]  刀鋒視窗上，選取一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="45bd2-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="45bd2-114">在 [appname] 刀鋒視窗 (亦即標題中含有所選應用程式名稱的刀鋒視窗) 上，選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="45bd2-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![選取 [屬性] 命令](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="45bd2-116">在 [***appname*** - 屬性] 刀鋒視窗上，瀏覽要作為新標誌的檔案或編輯應用程式名稱，或同時執行兩者。</span><span class="sxs-lookup"><span data-stu-id="45bd2-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![變更應用程式標誌或名稱屬性命令](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="45bd2-118">選取 [儲存]  命令。</span><span class="sxs-lookup"><span data-stu-id="45bd2-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45bd2-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45bd2-119">Next steps</span></span>
* [<span data-ttu-id="45bd2-120">查看我的所有群組</span><span class="sxs-lookup"><span data-stu-id="45bd2-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="45bd2-121">將使用者或群組指派給企業應用程式</span><span class="sxs-lookup"><span data-stu-id="45bd2-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="45bd2-122">從企業應用程式中移除使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="45bd2-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="45bd2-123">停用企業應用程式的使用者登入</span><span class="sxs-lookup"><span data-stu-id="45bd2-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
