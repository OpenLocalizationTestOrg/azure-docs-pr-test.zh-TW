---
title: "aaaHow toouse hello 稽核登入 Azure AD Privileged Identity Management |Microsoft 文件"
description: "了解如何 toouse hello 稽核登入 hello Azure Privileged Identity Management 延伸模組。"
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
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="9c87a-103">使用 PIM 中的 hello 稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="9c87a-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="9c87a-104">您可以使用 hello 特殊權限身分識別管理 (PIM) 稽核記錄檔 toosee 所有 hello 使用者指派和啟用在給定的時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="9c87a-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="9c87a-105">如果您想 toosee hello 完整的稽核記錄的活動，包括系統管理員、 使用者和同步處理活動，在您的租用戶中，您就可以使用 hello [Azure Active Directory 存取和使用方式報表。](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="9c87a-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="9c87a-106">瀏覽 toohello 稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="9c87a-106">Navigate toohello audit log</span></span>
<span data-ttu-id="9c87a-107">從 hello [Azure 入口網站](https://portal.azure.com)儀表板、 選取 hello **Azure AD Privileged Identity Management**應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c87a-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="9c87a-108">在這裡，即可存取 hello 稽核記錄檔**管理特殊權限的角色** > **稽核歷程**hello PIM 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="9c87a-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="9c87a-109">hello 稽核記錄圖形</span><span class="sxs-lookup"><span data-stu-id="9c87a-109">hello audit log graph</span></span>
<span data-ttu-id="9c87a-110">在折線圖中，您可以使用 hello 稽核記錄檔 tooview hello 啟用總數、 最大啟動每天和每日平均啟用。</span><span class="sxs-lookup"><span data-stu-id="9c87a-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="9c87a-111">您也可以篩選由角色 hello 資料，如果 hello 稽核歷程記錄中有多個角色。</span><span class="sxs-lookup"><span data-stu-id="9c87a-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="9c87a-112">使用 hello**時間**，**動作**，和**角色**按鈕 toosort hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9c87a-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="9c87a-113">hello 稽核記錄檔清單</span><span class="sxs-lookup"><span data-stu-id="9c87a-113">hello audit log list</span></span>
<span data-ttu-id="9c87a-114">hello hello 稽核記錄檔清單中的資料行如下：</span><span class="sxs-lookup"><span data-stu-id="9c87a-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="9c87a-115">**要求者**-hello 使用者 hello 角色啟用或變更要求。</span><span class="sxs-lookup"><span data-stu-id="9c87a-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="9c87a-116">如果 hello 值 「 Azure 系統 」，請檢查 hello Azure 稽核記錄檔，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9c87a-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="9c87a-117">**使用者**-hello 啟動或使用者 tooa 角色指派。</span><span class="sxs-lookup"><span data-stu-id="9c87a-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="9c87a-118">**角色**-hello 角色指派，或由 hello 使用者啟動。</span><span class="sxs-lookup"><span data-stu-id="9c87a-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="9c87a-119">**動作**-hello hello 要求者所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="9c87a-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="9c87a-120">這可包括指派、解除指派、啟用或停用。</span><span class="sxs-lookup"><span data-stu-id="9c87a-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="9c87a-121">**時間**-hello 動作發生時。</span><span class="sxs-lookup"><span data-stu-id="9c87a-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="9c87a-122">**推理**-如果在啟用期間到 hello [原因] 欄位輸入任何文字，它會出現。</span><span class="sxs-lookup"><span data-stu-id="9c87a-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="9c87a-123">**到期** - 只與角色啟用相關。</span><span class="sxs-lookup"><span data-stu-id="9c87a-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="9c87a-124">篩選 hello 稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="9c87a-124">Filter hello audit log</span></span>
<span data-ttu-id="9c87a-125">您可以篩選 hello 資訊會出現在 [hello 稽核記錄檔中依序按一下 hello**篩選**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9c87a-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="9c87a-126">hello**更新圖表參數刀鋒視窗**會出現。</span><span class="sxs-lookup"><span data-stu-id="9c87a-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="9c87a-127">您設定 hello 篩選之後，請按一下**更新**toofilter hello 資料 hello 記錄檔中的。</span><span class="sxs-lookup"><span data-stu-id="9c87a-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="9c87a-128">如果沒有立即顯示 hello 資料，重新整理 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="9c87a-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="9c87a-129">變更 hello 日期範圍</span><span class="sxs-lookup"><span data-stu-id="9c87a-129">Change hello date range</span></span>
<span data-ttu-id="9c87a-130">使用 hello**今天**，**過去一週**，**過去一個月**，或**自訂**按鈕 toochange hello 時間範圍的 hello 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9c87a-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="9c87a-131">當您選擇 hello**自訂** 按鈕，您會獲得**從**日期欄位和**至**日期欄位 toospecify hello 記錄的日期範圍。</span><span class="sxs-lookup"><span data-stu-id="9c87a-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="9c87a-132">您可以以 MM/DD/YYYY 格式輸入 hello 日期，或按一下 hello**行事曆**圖示，並從行事曆選擇日期 hello。</span><span class="sxs-lookup"><span data-stu-id="9c87a-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="9c87a-133">變更包含在 hello 記錄中的 hello 角色</span><span class="sxs-lookup"><span data-stu-id="9c87a-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="9c87a-134">選取或取消選取 hello**角色**核取方塊下一步 tooeach 角色 tooinclude 或排除它從 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="9c87a-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9c87a-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c87a-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

