---
title: "aaaHow toocomplete 存取檢閱 |Microsoft 文件"
description: "您在 Azure AD Privileged Identity Management 啟動存取檢閱後，了解如何 toocomplete 它並檢視 hello 結果"
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
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="26cb3-103">如何 toocomplete 存取檢閱在 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="26cb3-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="26cb3-104">在 [開始安全性檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)之後，特殊權限角色管理員就可以檢閱特殊權限存取權。</span><span class="sxs-lookup"><span data-stu-id="26cb3-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="26cb3-105">Azure AD Privileged Identity Management (PIM) 將會自動傳送電子郵件提示使用者 tooreview 其存取權。</span><span class="sxs-lookup"><span data-stu-id="26cb3-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="26cb3-106">如果使用者未取得電子郵件，您可以傳送 hello 說明[如何 tooperform 安全性檢閱](active-directory-privileged-identity-management-how-to-perform-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="26cb3-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="26cb3-107">Hello 安全性檢閱時間已經結束，或 hello 的所有使用者都完成其自我檢閱之後，請遵循在這個發行項 toomanage hello 檢閱中的 hello 步驟，並查看 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="26cb3-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="26cb3-108">管理安全性檢閱</span><span class="sxs-lookup"><span data-stu-id="26cb3-108">Manage security reviews</span></span>
1. <span data-ttu-id="26cb3-109">移 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello **Azure AD Privileged Identity Management**儀表板上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="26cb3-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="26cb3-110">選取 hello**存取檢閱**hello 儀表板的區段。</span><span class="sxs-lookup"><span data-stu-id="26cb3-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="26cb3-111">選取您想 toomanage hello 存取檢閱。</span><span class="sxs-lookup"><span data-stu-id="26cb3-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="26cb3-112">Hello 存取檢閱的詳細資料 刀鋒視窗中，有數字的選項，來管理該檢閱。</span><span class="sxs-lookup"><span data-stu-id="26cb3-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![PIM 存取權檢閱按鈕 - 螢幕擷取畫面][1]

### <a name="remind"></a><span data-ttu-id="26cb3-114">提醒</span><span class="sxs-lookup"><span data-stu-id="26cb3-114">Remind</span></span>
<span data-ttu-id="26cb3-115">如果設定存取檢閱使 hello 使用者檢閱本身，hello**提醒**按鈕送出通知。</span><span class="sxs-lookup"><span data-stu-id="26cb3-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="26cb3-116">停止</span><span class="sxs-lookup"><span data-stu-id="26cb3-116">Stop</span></span>
<span data-ttu-id="26cb3-117">所有存取檢閱都有結束日期，但是您可以使用 hello**停止**按鈕 toofinish 早期它。</span><span class="sxs-lookup"><span data-stu-id="26cb3-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="26cb3-118">如果尚未經過這次檢閱任何使用者，他們不是能 tooafter 停止 hello 檢閱。</span><span class="sxs-lookup"><span data-stu-id="26cb3-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="26cb3-119">在停止檢閱之後，即無法重新開始該檢閱。</span><span class="sxs-lookup"><span data-stu-id="26cb3-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="26cb3-120">套用</span><span class="sxs-lookup"><span data-stu-id="26cb3-120">Apply</span></span>
<span data-ttu-id="26cb3-121">存取檢閱已完成之後，是因為您達到 hello 結束日期，或手動停止它 hello**套用**按鈕實作 hello hello 檢閱結果。</span><span class="sxs-lookup"><span data-stu-id="26cb3-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="26cb3-122">如果使用者的存取被拒 hello 檢閱中，這會是 hello 步驟，將會移除其角色指派。</span><span class="sxs-lookup"><span data-stu-id="26cb3-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="26cb3-123">匯出</span><span class="sxs-lookup"><span data-stu-id="26cb3-123">Export</span></span>
<span data-ttu-id="26cb3-124">若要手動 tooapply hello hello 安全性檢閱結果，您可以匯出 hello 檢閱。</span><span class="sxs-lookup"><span data-stu-id="26cb3-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="26cb3-125">hello**匯出**按鈕開始下載 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="26cb3-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="26cb3-126">您可以管理在 Excel 或其他程式，開啟 CSV 檔案中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="26cb3-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="26cb3-127">刪除</span><span class="sxs-lookup"><span data-stu-id="26cb3-127">Delete</span></span>
<span data-ttu-id="26cb3-128">如果您不感興趣 hello 進一步檢閱任何，將它刪除。</span><span class="sxs-lookup"><span data-stu-id="26cb3-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="26cb3-129">hello**刪除**按鈕會移除 hello PIM 應用程式中的 hello 檢閱。</span><span class="sxs-lookup"><span data-stu-id="26cb3-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26cb3-130">您不會收到警告，就會刪除之前，因此請確定您想要檢閱的 toodelete。</span><span class="sxs-lookup"><span data-stu-id="26cb3-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="26cb3-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26cb3-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
