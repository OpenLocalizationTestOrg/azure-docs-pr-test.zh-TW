---
title: "如何完成存取權檢閱 | Microsoft Docs"
description: "在您於 Azure AD Privileged Identity Management 中開始存取權檢閱之後，了解如何完成它並檢視結果"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="5bb47-103">如何在 Azure AD Privileged Identity Management 中完成存取權檢閱</span><span class="sxs-lookup"><span data-stu-id="5bb47-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="5bb47-104">在 [開始安全性檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)之後，特殊權限角色管理員就可以檢閱特殊權限存取權。</span><span class="sxs-lookup"><span data-stu-id="5bb47-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="5bb47-105">Azure AD Privileged Identity Management (PIM) 會自動傳送電子郵件，提示使用者檢閱其存取權。</span><span class="sxs-lookup"><span data-stu-id="5bb47-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="5bb47-106">如果使用者未收到電子郵件，您可以將 [Azure AD Privileged Identity Management：如何執行安全性檢閱](active-directory-privileged-identity-management-how-to-perform-security-review.md)中的指示傳送給他們。</span><span class="sxs-lookup"><span data-stu-id="5bb47-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="5bb47-107">安全性檢閱時間結束後，或所有使用者都已完成其自我檢閱後，請遵循本文的步驟管理檢閱並查看結果。</span><span class="sxs-lookup"><span data-stu-id="5bb47-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="5bb47-108">管理安全性檢閱</span><span class="sxs-lookup"><span data-stu-id="5bb47-108">Manage security reviews</span></span>
1. <span data-ttu-id="5bb47-109">移至 [Azure 入口網站](https://portal.azure.com/)，然後在儀表板上選取 [Azure AD Privileged Identity Management] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bb47-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="5bb47-110">選取儀表板的 [存取權檢閱]  區段。</span><span class="sxs-lookup"><span data-stu-id="5bb47-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="5bb47-111">選取您想要管理的存取權檢閱。</span><span class="sxs-lookup"><span data-stu-id="5bb47-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="5bb47-112">在存取權檢閱的詳細資料刀鋒視窗上，有一些可管理該檢閱的選項。</span><span class="sxs-lookup"><span data-stu-id="5bb47-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![PIM 存取權檢閱按鈕 - 螢幕擷取畫面][1]

### <a name="remind"></a><span data-ttu-id="5bb47-114">提醒</span><span class="sxs-lookup"><span data-stu-id="5bb47-114">Remind</span></span>
<span data-ttu-id="5bb47-115">如果將存取權檢閱設定成讓使用者自我檢閱，[提醒]  按鈕就會傳送通知。</span><span class="sxs-lookup"><span data-stu-id="5bb47-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="5bb47-116">停止</span><span class="sxs-lookup"><span data-stu-id="5bb47-116">Stop</span></span>
<span data-ttu-id="5bb47-117">所有的存取權檢閱都有結束日期，但是您可以使用 [停止]  按鈕來提早結束檢閱。</span><span class="sxs-lookup"><span data-stu-id="5bb47-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="5bb47-118">如果此時有任何使用者尚未受到檢閱，在您停止檢閱之後，他們將無法受到檢閱。</span><span class="sxs-lookup"><span data-stu-id="5bb47-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="5bb47-119">在停止檢閱之後，即無法重新開始該檢閱。</span><span class="sxs-lookup"><span data-stu-id="5bb47-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="5bb47-120">套用</span><span class="sxs-lookup"><span data-stu-id="5bb47-120">Apply</span></span>
<span data-ttu-id="5bb47-121">在存取權檢閱因您已達到結束日期或手動停止它而完成之後，[套用]  按鈕就會實作該檢閱的結果。</span><span class="sxs-lookup"><span data-stu-id="5bb47-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="5bb47-122">如果使用者的存取權在檢閱中被拒絕，則在這個步驟就會將其角色指派移除。</span><span class="sxs-lookup"><span data-stu-id="5bb47-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="5bb47-123">匯出</span><span class="sxs-lookup"><span data-stu-id="5bb47-123">Export</span></span>
<span data-ttu-id="5bb47-124">如果想要手動套用安全性檢閱的結果，您可以匯出檢閱。</span><span class="sxs-lookup"><span data-stu-id="5bb47-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="5bb47-125">[匯出]  按鈕會開始下載 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="5bb47-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="5bb47-126">您可以在 Excel 或開啟 CSV 檔案的其他程式中管理結果。</span><span class="sxs-lookup"><span data-stu-id="5bb47-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="5bb47-127">刪除</span><span class="sxs-lookup"><span data-stu-id="5bb47-127">Delete</span></span>
<span data-ttu-id="5bb47-128">如果對檢閱不再有任何興趣，請刪除它。</span><span class="sxs-lookup"><span data-stu-id="5bb47-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="5bb47-129">[刪除]  按鈕會將檢閱從 PIM 應用程式中移除。</span><span class="sxs-lookup"><span data-stu-id="5bb47-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bb47-130">刪除執行前，您不會收到警告，因此請務必確定您想要刪除該檢閱。</span><span class="sxs-lookup"><span data-stu-id="5bb47-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5bb47-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bb47-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
