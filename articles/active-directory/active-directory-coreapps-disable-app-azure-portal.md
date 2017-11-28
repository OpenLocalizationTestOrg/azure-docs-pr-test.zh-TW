---
title: "aaaDisable 使用者登入 Azure Active Directory 中的企業應用程式 |Microsoft 文件"
description: "如何 toodisable 企業應用程式，讓任何使用者可能登入 Azure Active Directory 中 tooit"
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
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="be41d-103">在 Azure Active Directory 中停用企業應用程式的使用者登入</span><span class="sxs-lookup"><span data-stu-id="be41d-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="be41d-104">它是簡單 toodisable 企業應用程式，因此沒有任何使用者可能登入 Azure Active Directory (Azure AD) 中的 tooit。</span><span class="sxs-lookup"><span data-stu-id="be41d-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="be41d-105">您必須擁有 hello 適當的權限 toomanage hello 企業應用程式，，您必須是全域管理員的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="be41d-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="be41d-106">如何停用使用者登入？</span><span class="sxs-lookup"><span data-stu-id="be41d-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="be41d-107">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="be41d-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="be41d-108">選取**更多服務**，輸入**Azure Active Directory**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="be41d-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="be41d-109">在 hello **Azure Active Directory** -  ***directoryname***刀鋒視窗 （也就是 hello Azure AD 刀鋒視窗中您所管理的 hello 目錄），選取**的企業應用程式**.</span><span class="sxs-lookup"><span data-stu-id="be41d-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![開啟企業應用程式](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="be41d-111">在 hello**企業應用程式**刀鋒視窗中，選取**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="be41d-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="be41d-112">您會看到一份可以管理的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be41d-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="be41d-113">在 hello**企業應用程式的所有應用程式**刀鋒視窗中，選取一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="be41d-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="be41d-114">在 hello ***appname***刀鋒視窗 （也就是 hello 刀鋒視窗中的 hello hello 標題中的 hello 選應用程式的名稱），選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="be41d-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![選取 hello 所有應用程式的命令](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="be41d-116">在 hello ***appname*** - **屬性**刀鋒視窗中，選取**否**如**toosign 中的使用者啟用？**。</span><span class="sxs-lookup"><span data-stu-id="be41d-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="be41d-117">選取 hello**儲存**命令。</span><span class="sxs-lookup"><span data-stu-id="be41d-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be41d-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be41d-118">Next steps</span></span>
* [<span data-ttu-id="be41d-119">查看我的所有群組</span><span class="sxs-lookup"><span data-stu-id="be41d-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="be41d-120">指派使用者或群組的 tooan 企業應用程式</span><span class="sxs-lookup"><span data-stu-id="be41d-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="be41d-121">從企業應用程式中移除使用者或群組指派</span><span class="sxs-lookup"><span data-stu-id="be41d-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="be41d-122">變更 hello 名稱或企業應用程式的標誌</span><span class="sxs-lookup"><span data-stu-id="be41d-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
