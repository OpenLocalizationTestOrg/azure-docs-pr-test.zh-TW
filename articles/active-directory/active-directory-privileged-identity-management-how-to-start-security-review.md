---
title: "aaaHow toostart 存取檢閱 |Microsoft 文件"
description: "了解如何 toocreate 存取檢閱特殊權限的身分識別與 hello Azure Privileged Identity Management 的應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="2dc89-103">如何 toostart 存取檢閱在 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2dc89-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="2dc89-104">當使用者擁有不再需要的特殊存取權時，角色指派就會變成「過時」。</span><span class="sxs-lookup"><span data-stu-id="2dc89-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="2dc89-105">在這些過時的角色指派與相關訂單 tooreduce hello 風險，特殊權限的角色系統管理員應該定期檢閱 hello 角色已獲得使用者。</span><span class="sxs-lookup"><span data-stu-id="2dc89-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="2dc89-106">本文件涵蓋 hello 存取檢閱啟動 Azure AD Privileged Identity Management (PIM) 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="2dc89-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="2dc89-107">開始存取權檢閱</span><span class="sxs-lookup"><span data-stu-id="2dc89-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="2dc89-108">如果您沒有在 hello Azure 入口網站中加入 hello PIM 應用程式 tooyour 儀表板，請參閱中的 hello 步驟[開始使用 Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="2dc89-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="2dc89-109">從 hello PIM 應用程式主頁面上，有三種方式 toostart 存取檢閱：</span><span class="sxs-lookup"><span data-stu-id="2dc89-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="2dc89-110">[存取權檢閱] > [新增]</span><span class="sxs-lookup"><span data-stu-id="2dc89-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="2dc89-111">[角色] > [檢閱] 按鈕</span><span class="sxs-lookup"><span data-stu-id="2dc89-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="2dc89-112">選取 hello 特定角色 toobe 檢閱從 hello 角色清單 >**檢閱**按鈕</span><span class="sxs-lookup"><span data-stu-id="2dc89-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="2dc89-113">當您按一下 hello**檢閱**按鈕，hello**開始存取檢閱**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="2dc89-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="2dc89-114">在這個刀鋒視窗中，您正在進行 tooconfigure hello 檢閱的名稱和時間限制選擇角色 tooreview，並且決定誰可以執行 hello 檢閱。</span><span class="sxs-lookup"><span data-stu-id="2dc89-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![開始存取權檢閱 - 螢幕擷取畫面][1]

### <a name="configure-hello-review"></a><span data-ttu-id="2dc89-116">設定 hello 檢閱</span><span class="sxs-lookup"><span data-stu-id="2dc89-116">Configure hello review</span></span>
<span data-ttu-id="2dc89-117">toocreate 存取檢閱，您需要 tooname 它並設為開始和結束日期。</span><span class="sxs-lookup"><span data-stu-id="2dc89-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![設定檢閱 - 螢幕擷取畫面][2]

<span data-ttu-id="2dc89-119">請檢閱久，使用者 toocomplete hello hello 長度。</span><span class="sxs-lookup"><span data-stu-id="2dc89-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="2dc89-120">如果您完成 hello 結束日期之前，您可以一律停駐 hello 檢閱早期。</span><span class="sxs-lookup"><span data-stu-id="2dc89-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="2dc89-121">選擇角色 tooreview</span><span class="sxs-lookup"><span data-stu-id="2dc89-121">Choose a role tooreview</span></span>
<span data-ttu-id="2dc89-122">每個檢閱只針對一個角色。</span><span class="sxs-lookup"><span data-stu-id="2dc89-122">Each review focuses on only one role.</span></span> <span data-ttu-id="2dc89-123">除非您從特定的角色 刀鋒視窗中啟動 hello 存取檢閱，您將現在需要 toochoose 角色。</span><span class="sxs-lookup"><span data-stu-id="2dc89-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="2dc89-124">瀏覽過**檢視角色成員資格**</span><span class="sxs-lookup"><span data-stu-id="2dc89-124">Navigate too**Review role membership**</span></span>
   
    ![檢閱角色成員資格 - 螢幕擷取畫面][3]
2. <span data-ttu-id="2dc89-126">Hello 清單中選擇一個角色。</span><span class="sxs-lookup"><span data-stu-id="2dc89-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="2dc89-127">決定誰可以執行 hello 檢閱</span><span class="sxs-lookup"><span data-stu-id="2dc89-127">Decide who will perform hello review</span></span>
<span data-ttu-id="2dc89-128">執行檢閱的選項有三個。</span><span class="sxs-lookup"><span data-stu-id="2dc89-128">There are three options for performing a review.</span></span> <span data-ttu-id="2dc89-129">您可以指派 hello 檢閱 toosomeone else toocomplete，您可以自行操作，或您可以檢閱其本身存取每位使用者。</span><span class="sxs-lookup"><span data-stu-id="2dc89-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="2dc89-130">瀏覽過**選取檢閱者**</span><span class="sxs-lookup"><span data-stu-id="2dc89-130">Navigate too**Select reviewers**</span></span>
   
    ![選取檢閱者 - 螢幕擷取畫面][4]
2. <span data-ttu-id="2dc89-132">選擇其中一個 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="2dc89-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="2dc89-133">**選取檢閱者**︰如果您不知道誰需要存取權，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="2dc89-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="2dc89-134">使用此選項，您可以指派 hello 檢閱 tooa 資源擁有者或群組管理員 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="2dc89-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="2dc89-135">**我**： 如果您想 toopreview 如何存取檢閱工作，或您想 tooreview 代表人員無法。</span><span class="sxs-lookup"><span data-stu-id="2dc89-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="2dc89-136">**成員檢閱本身**： 使用這個選項 toohave hello 使用者檢閱他們自己的角色指派。</span><span class="sxs-lookup"><span data-stu-id="2dc89-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="2dc89-137">開始 hello 檢閱</span><span class="sxs-lookup"><span data-stu-id="2dc89-137">Start hello review</span></span>
<span data-ttu-id="2dc89-138">最後，您擁有 hello 選項 toorequire 使用者提供的原因，如果他們同意其存取權。</span><span class="sxs-lookup"><span data-stu-id="2dc89-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="2dc89-139">如果需要，新增 hello 檢閱的描述，然後選取**啟動**。</span><span class="sxs-lookup"><span data-stu-id="2dc89-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="2dc89-140">請確定您讓使用者知道，正在等候存取檢閱，並顯示它們[如何 tooperform 存取檢閱](active-directory-privileged-identity-management-how-to-perform-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="2dc89-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="2dc89-141">管理 hello 存取檢閱</span><span class="sxs-lookup"><span data-stu-id="2dc89-141">Manage hello access review</span></span>
<span data-ttu-id="2dc89-142">Hello 檢閱者完成 hello Azure AD PIM 儀表板中的檢視時，您可以追蹤 hello 進度，在 hello 存取檢閱 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2dc89-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="2dc89-143">沒有存取權限將會變更在 hello 目錄，直到[hello 檢閱完成](active-directory-privileged-identity-management-how-to-complete-review.md)。</span><span class="sxs-lookup"><span data-stu-id="2dc89-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="2dc89-144">直到 hello 檢閱時間已經結束，您可以提醒使用者 toocomplete 他們檢閱，或停止 hello 檢閱早期 hello 存取從檢閱 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2dc89-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="2dc89-145">PIM 目錄</span><span class="sxs-lookup"><span data-stu-id="2dc89-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
