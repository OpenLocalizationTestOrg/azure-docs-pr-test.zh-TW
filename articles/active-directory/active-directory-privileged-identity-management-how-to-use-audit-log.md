---
title: "如何使用 Azure AD Privileged Identity Management 中的稽核記錄檔 | Microsoft Docs"
description: "了解如何在 Azure 特殊權限身分識別管理擴充功能中使用稽核記錄。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="2d662-103">使用 PIM 中的稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="2d662-103">Using the audit log in PIM</span></span>
<span data-ttu-id="2d662-104">您可以使用 Privileged Identity Management (PIM) 稽核記錄，來查看指定期間內的所有使用者指派與啟用。</span><span class="sxs-lookup"><span data-stu-id="2d662-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="2d662-105">如果您想要查看租用戶活動 (包括系統管理員、使用者和同步處理活動) 的完整稽核歷程記錄，您可以使用 [Azure Active Directory 存取和使用情況報告](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="2d662-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="2d662-106">瀏覽至稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="2d662-106">Navigate to the audit log</span></span>
<span data-ttu-id="2d662-107">從 [Azure 入口網站](https://portal.azure.com)儀表板選取 [Azure AD Privileged Identity Management] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d662-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="2d662-108">從該處，按一下 PIM 儀表板中的 [管理特殊權限角色] > [稽核歷程記錄] 來存取稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="2d662-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="2d662-109">稽核記錄圖表</span><span class="sxs-lookup"><span data-stu-id="2d662-109">The audit log graph</span></span>
<span data-ttu-id="2d662-110">您可以使用稽核記錄，在折線圖中檢視啟用總數、每天最大啟用數目，以及每天平均啟用數目。</span><span class="sxs-lookup"><span data-stu-id="2d662-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="2d662-111">如果稽核記錄中有一個以上的角色，您也可以依角色篩選資料。</span><span class="sxs-lookup"><span data-stu-id="2d662-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="2d662-112">使用 [時間]、[動作] 和 [角色] 按鈕來排序記錄。</span><span class="sxs-lookup"><span data-stu-id="2d662-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="2d662-113">稽核記錄清單</span><span class="sxs-lookup"><span data-stu-id="2d662-113">The audit log list</span></span>
<span data-ttu-id="2d662-114">稽核記錄清單中的欄如下：</span><span class="sxs-lookup"><span data-stu-id="2d662-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="2d662-115">**要求者** - 要求啟用或變更角色的使用者。</span><span class="sxs-lookup"><span data-stu-id="2d662-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="2d662-116">如果值為「Azure 系統」，請檢查 Azure 稽核記錄檔以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2d662-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="2d662-117">**使用者** - 啟用角色或被指派給角色的使用者。</span><span class="sxs-lookup"><span data-stu-id="2d662-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="2d662-118">**角色** - 使用者所指派或啟用的角色。</span><span class="sxs-lookup"><span data-stu-id="2d662-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="2d662-119">**動作** - 要求者所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="2d662-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="2d662-120">這可包括指派、解除指派、啟用或停用。</span><span class="sxs-lookup"><span data-stu-id="2d662-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="2d662-121">**時間** - 動作發生的時間。</span><span class="sxs-lookup"><span data-stu-id="2d662-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="2d662-122">**推理** - 如果在啟用過程中於 [原因] 欄位輸入任何文字，則它將會顯示於此處。</span><span class="sxs-lookup"><span data-stu-id="2d662-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="2d662-123">**到期** - 只與角色啟用相關。</span><span class="sxs-lookup"><span data-stu-id="2d662-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="2d662-124">篩選稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="2d662-124">Filter the audit log</span></span>
<span data-ttu-id="2d662-125">您可以按一下 [篩選]  按鈕，來篩選稽核記錄中顯示的資訊。</span><span class="sxs-lookup"><span data-stu-id="2d662-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="2d662-126">隨即會出現 [更新圖表參數]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d662-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="2d662-127">設定篩選之後，請按一下 [更新]  來篩選記錄中的資料。</span><span class="sxs-lookup"><span data-stu-id="2d662-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="2d662-128">如果資料並未立即出現，請重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="2d662-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="2d662-129">變更日期範圍</span><span class="sxs-lookup"><span data-stu-id="2d662-129">Change the date range</span></span>
<span data-ttu-id="2d662-130">使用 [今天]、[過去一週]、[過去一個月] 或 [自訂] 按鈕來變更稽核記錄的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="2d662-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="2d662-131">當您選擇 [自訂] 按鈕時，將會看見可指定記錄日期範圍的 [開始] 日期欄位和 [結束] 日期欄位。</span><span class="sxs-lookup"><span data-stu-id="2d662-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="2d662-132">您可以使用 MM/DD/YYYY 格式輸入日期，或者按一下 [月曆]  圖示並從月曆中選擇日期。</span><span class="sxs-lookup"><span data-stu-id="2d662-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="2d662-133">變更記錄中包含的角色</span><span class="sxs-lookup"><span data-stu-id="2d662-133">Change the roles included in the log</span></span>
<span data-ttu-id="2d662-134">選取或取消選取每個角色旁邊的 [角色]  核取方塊，即可將其納入記錄或排除在記錄之外。</span><span class="sxs-lookup"><span data-stu-id="2d662-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="2d662-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d662-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

