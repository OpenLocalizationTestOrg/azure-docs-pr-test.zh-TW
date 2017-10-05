---
title: "如何開始存取權檢閱 | Microsoft Docs"
description: "了解如何使用 Azure Privileged Identity Management 應用程式為特殊權限身分識別建立存取權檢閱。"
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
ms.openlocfilehash: 2b516e2f05aa883c5e37f5864e5ee8a2b37d3a46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="c0226-103">如何在 Azure AD Privileged Identity Management 中開始存取權檢閱</span><span class="sxs-lookup"><span data-stu-id="c0226-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="c0226-104">當使用者擁有不再需要的特殊存取權時，角色指派就會變成「過時」。</span><span class="sxs-lookup"><span data-stu-id="c0226-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="c0226-105">為了降低與這些過時的角色指派相關聯的風險，特殊權限角色管理員應該定期檢閱使用者獲授與的角色。</span><span class="sxs-lookup"><span data-stu-id="c0226-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="c0226-106">本文件涵蓋在 Azure AD Privileged Identity Management (PIM) 中開始存取權檢閱的步驟。</span><span class="sxs-lookup"><span data-stu-id="c0226-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="c0226-107">開始存取權檢閱</span><span class="sxs-lookup"><span data-stu-id="c0226-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="c0226-108">如果您尚未在 Azure 入口網站的儀表板中新增 PIM 應用程式，請參閱[開始使用 Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="c0226-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="c0226-109">在 PIM 應用程式的主頁面，有三種方式可以開始存取權檢閱︰</span><span class="sxs-lookup"><span data-stu-id="c0226-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="c0226-110">[存取權檢閱] > [新增]</span><span class="sxs-lookup"><span data-stu-id="c0226-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="c0226-111">[角色] > [檢閱] 按鈕</span><span class="sxs-lookup"><span data-stu-id="c0226-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="c0226-112">從角色清單中選取要檢閱的特定角色 > [檢閱] 按鈕</span><span class="sxs-lookup"><span data-stu-id="c0226-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="c0226-113">按一下 [檢閱] 按鈕時，隨即會顯示 [開始存取檢閱] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c0226-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="c0226-114">您將在此刀鋒視窗上為檢閱設定名稱和時間限制、選擇要檢閱的角色，以及決定將由誰執行檢閱。</span><span class="sxs-lookup"><span data-stu-id="c0226-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![開始存取權檢閱 - 螢幕擷取畫面][1]

### <a name="configure-the-review"></a><span data-ttu-id="c0226-116">設定檢閱</span><span class="sxs-lookup"><span data-stu-id="c0226-116">Configure the review</span></span>
<span data-ttu-id="c0226-117">若要建立存取權檢閱，您需要為它命名並設定開始和結束日期。</span><span class="sxs-lookup"><span data-stu-id="c0226-117">To create an access review, you need to name it and set a start and end date.</span></span>

![設定檢閱 - 螢幕擷取畫面][2]

<span data-ttu-id="c0226-119">為檢閱設定足夠的時間長度，以便讓使用者能夠完成檢閱。</span><span class="sxs-lookup"><span data-stu-id="c0226-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="c0226-120">如果您在結束日期之前即完成檢閱，您一律可以提早停止檢閱。</span><span class="sxs-lookup"><span data-stu-id="c0226-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="c0226-121">選取要檢閱的角色</span><span class="sxs-lookup"><span data-stu-id="c0226-121">Choose a role to review</span></span>
<span data-ttu-id="c0226-122">每個檢閱只針對一個角色。</span><span class="sxs-lookup"><span data-stu-id="c0226-122">Each review focuses on only one role.</span></span> <span data-ttu-id="c0226-123">除非您是從特定的角色刀鋒視窗開始存取權檢閱，否則您現在將必須選擇一個角色。</span><span class="sxs-lookup"><span data-stu-id="c0226-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="c0226-124">瀏覽至 [檢閱角色成員資格] </span><span class="sxs-lookup"><span data-stu-id="c0226-124">Navigate to **Review role membership**</span></span>
   
    ![檢閱角色成員資格 - 螢幕擷取畫面][3]
2. <span data-ttu-id="c0226-126">從清單中選擇一個角色。</span><span class="sxs-lookup"><span data-stu-id="c0226-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="c0226-127">決定將由誰執行檢閱</span><span class="sxs-lookup"><span data-stu-id="c0226-127">Decide who will perform the review</span></span>
<span data-ttu-id="c0226-128">執行檢閱的選項有三個。</span><span class="sxs-lookup"><span data-stu-id="c0226-128">There are three options for performing a review.</span></span> <span data-ttu-id="c0226-129">您可以將檢閱指派給其他人來完成、可以自行進行檢閱，或者可以讓每個使用者檢閱自己的存取權。</span><span class="sxs-lookup"><span data-stu-id="c0226-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="c0226-130">瀏覽至 [選取檢閱者] </span><span class="sxs-lookup"><span data-stu-id="c0226-130">Navigate to **Select reviewers**</span></span>
   
    ![選取檢閱者 - 螢幕擷取畫面][4]
2. <span data-ttu-id="c0226-132">選擇其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="c0226-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="c0226-133">**選取檢閱者**︰如果您不知道誰需要存取權，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="c0226-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="c0226-134">使用此選項，您可以指派資源擁有者或群組管理員完成檢閱。</span><span class="sxs-lookup"><span data-stu-id="c0226-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="c0226-135">**我**︰如果您想要預覽存取權檢閱如何運作，或是想要代表無法檢閱的人員執行檢閱，此選項會相當有用。</span><span class="sxs-lookup"><span data-stu-id="c0226-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="c0226-136">**成員自我檢閱**：若要讓使用者檢閱自己的角色指派，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="c0226-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="c0226-137">開始檢閱</span><span class="sxs-lookup"><span data-stu-id="c0226-137">Start the review</span></span>
<span data-ttu-id="c0226-138">最後，您可以選擇是否要要求使用者在核准其存取權時提供原因。</span><span class="sxs-lookup"><span data-stu-id="c0226-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="c0226-139">請依喜好新增檢閱描述，然後選取 [開始] 。</span><span class="sxs-lookup"><span data-stu-id="c0226-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="c0226-140">請確定讓使用者知道有等待他們執行的存取權檢閱，並示範 [如何執行存取權檢閱](active-directory-privileged-identity-management-how-to-perform-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="c0226-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="c0226-141">管理存取權檢閱</span><span class="sxs-lookup"><span data-stu-id="c0226-141">Manage the access review</span></span>
<span data-ttu-id="c0226-142">當檢閱者在完成其檢閱時，您可以在 Azure AD PIM 儀表板的 [存取權檢閱] 區段中追蹤其進度。</span><span class="sxs-lookup"><span data-stu-id="c0226-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="c0226-143">在 [完成檢閱](active-directory-privileged-identity-management-how-to-complete-review.md)之前，不會變更目錄中的任何存取權限。</span><span class="sxs-lookup"><span data-stu-id="c0226-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="c0226-144">在檢閱期間結束之前，您都可以提醒使用者完成其檢閱，或是從 [存取權檢閱] 區段提前停止檢閱。</span><span class="sxs-lookup"><span data-stu-id="c0226-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="c0226-145">PIM 目錄</span><span class="sxs-lookup"><span data-stu-id="c0226-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
