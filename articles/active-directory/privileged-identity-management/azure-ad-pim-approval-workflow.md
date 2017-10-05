---
title: "Azure Privileged Identity Management 核准工作流程 | Microsoft Docs"
description: "了解 Privileged Identity Management (PIM) 中的核准工作流程"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="49887-103">核准 (預覽)</span><span class="sxs-lookup"><span data-stu-id="49887-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="49887-104">概觀</span><span class="sxs-lookup"><span data-stu-id="49887-104">Overview</span></span>

<span data-ttu-id="49887-105">利用 Privileged Identity Management 的核准，您可以將角色設定為需要核准才能啟用，並選擇一或多個使用者或群組做為委派核准者。</span><span class="sxs-lookup"><span data-stu-id="49887-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="49887-106">請繼續閱讀，以了解如何設定角色和選取核准者。</span><span class="sxs-lookup"><span data-stu-id="49887-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="49887-107">請記住，這項功能仍處於開發階段，而您可能會遇到 Bug。</span><span class="sxs-lookup"><span data-stu-id="49887-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="49887-108">包括文字和命名慣例在內的功能均有可能變更，不應將其視為最終結果。</span><span class="sxs-lookup"><span data-stu-id="49887-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="49887-109">重要術語</span><span class="sxs-lookup"><span data-stu-id="49887-109">Key Terminology</span></span>

<span data-ttu-id="49887-110">*合格角色使用者*：合格角色使用者是您組織內已在符合資格時指派給 Azure AD 角色的使用者 (角色需要啟用)。</span><span class="sxs-lookup"><span data-stu-id="49887-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="49887-111">*委派核准者*：委派核准者是您 Azure AD 內的一或多個個人或群組，其負責核准啟用角色的要求。</span><span class="sxs-lookup"><span data-stu-id="49887-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="49887-112">案例</span><span class="sxs-lookup"><span data-stu-id="49887-112">Scenarios</span></span>

<span data-ttu-id="49887-113">私人預覽支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="49887-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="49887-114">**身為特殊權限角色管理員 (PRA)，您可以：**</span><span class="sxs-lookup"><span data-stu-id="49887-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="49887-115">啟用特定角色的核准</span><span class="sxs-lookup"><span data-stu-id="49887-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="49887-116">指定核准者使用者和/或群組來核准要求</span><span class="sxs-lookup"><span data-stu-id="49887-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="49887-117">檢視所有特殊權限角色的要求和核准歷程記錄</span><span class="sxs-lookup"><span data-stu-id="49887-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="49887-118">**身為指定的核准者，您可以：**</span><span class="sxs-lookup"><span data-stu-id="49887-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="49887-119">檢視待決的核准 (要求)</span><span class="sxs-lookup"><span data-stu-id="49887-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="49887-120">核准或拒絕提高角色權限 (單一和/或大量) 的要求</span><span class="sxs-lookup"><span data-stu-id="49887-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="49887-121">提供我的核准/拒絕理由</span><span class="sxs-lookup"><span data-stu-id="49887-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="49887-122">**身為合格角色使用者，您可以：**</span><span class="sxs-lookup"><span data-stu-id="49887-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="49887-123">要求啟用需要核准的角色</span><span class="sxs-lookup"><span data-stu-id="49887-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="49887-124">檢視要啟用之要求的狀態</span><span class="sxs-lookup"><span data-stu-id="49887-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="49887-125">如果已核准啟用，在 Azure AD 中完成您的工作</span><span class="sxs-lookup"><span data-stu-id="49887-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="49887-126">導覽</span><span class="sxs-lookup"><span data-stu-id="49887-126">Navigation</span></span>

<span data-ttu-id="49887-127">我們已更新導覽來支援核准</span><span class="sxs-lookup"><span data-stu-id="49887-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="49887-128">預設的登陸頁面讓您能夠方便存取有關 PIM 和新核准文件的資訊。</span><span class="sxs-lookup"><span data-stu-id="49887-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="49887-129">我們也針對 PIM [我的稽核歷程記錄] 的所有使用者新增了新的區段。</span><span class="sxs-lookup"><span data-stu-id="49887-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="49887-130">您可以在此處找到與您身分識別相關的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="49887-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="49887-131">這包括您的所有待決和完成的要求、您對於所解決之要求所做出的任何決策，以及您過去在某一個便利位置中的所有角色啟用。</span><span class="sxs-lookup"><span data-stu-id="49887-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="49887-132">啟用特定角色的核准</span><span class="sxs-lookup"><span data-stu-id="49887-132">Enable approval for specific roles</span></span>

<span data-ttu-id="49887-133">若要啟用特定角色的核准，請先從左側導覽中選取 [目錄角色]。</span><span class="sxs-lookup"><span data-stu-id="49887-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="49887-134">在 [目錄角色] 左側導覽中尋找並選取 [設定]</span><span class="sxs-lookup"><span data-stu-id="49887-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="49887-135">選取 [特殊權限角色]：</span><span class="sxs-lookup"><span data-stu-id="49887-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="49887-136">在 [要求核准] 區段中選取 [啟用]：</span><span class="sxs-lookup"><span data-stu-id="49887-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="49887-137">啟用之後，刀鋒視窗將展開以顯示下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="49887-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="49887-138">如果您未指定任何核准者，PRA 就會變成預設核准者。</span><span class="sxs-lookup"><span data-stu-id="49887-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="49887-139">需要有 PRA，才能核准此角色的所有啟用要求。</span><span class="sxs-lookup"><span data-stu-id="49887-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="49887-140">指定核准者使用者和/或群組來核准要求</span><span class="sxs-lookup"><span data-stu-id="49887-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="49887-141">若要委派核准，按一下 [選取核准者] 的選項：</span><span class="sxs-lookup"><span data-stu-id="49887-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="49887-142">當 [選取核准者] 刀鋒視窗載入時，您就能使用頂端的搜尋列來搜尋特定使用者或群組，或是從預先填入的清單中加以選取，然後在完成時按一下 [選取]：</span><span class="sxs-lookup"><span data-stu-id="49887-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="49887-143">注意︰您可以同時選取多個使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="49887-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="49887-144">您的選項將出現在所選取的核准者清單中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="49887-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="49887-145">若要移除核准者，只需按一下其名稱旁邊的 [移除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="49887-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="49887-146">若要新增其他核准者，請重複執行此程序。</span><span class="sxs-lookup"><span data-stu-id="49887-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="49887-147">檢視所有特殊權限角色的要求和核准歷程記錄</span><span class="sxs-lookup"><span data-stu-id="49887-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="49887-148">若要檢視所有特殊權限角色的要求和核准歷程記錄，請從儀表板選取 [稽核歷程記錄]：</span><span class="sxs-lookup"><span data-stu-id="49887-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="49887-149">您可以依 [動作] 排序資料，並尋找「已核准啟用」</span><span class="sxs-lookup"><span data-stu-id="49887-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="49887-150">檢視待決的核准 (要求)</span><span class="sxs-lookup"><span data-stu-id="49887-150">View pending approvals (requests)</span></span>

<span data-ttu-id="49887-151">身為委派核准者，當要求正在等待您的核准時，您將會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="49887-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="49887-152">若要在 PIM 入口網站中檢視這些要求，可從儀表板 (在新的導覽中) 選取左側導覽列中的 [等待核准要求] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="49887-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="49887-153">您將在該處看到一份等待核准的要求清單：</span><span class="sxs-lookup"><span data-stu-id="49887-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="49887-154">核准或拒絕提高角色權限 (單一和/或大量) 的要求</span><span class="sxs-lookup"><span data-stu-id="49887-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="49887-155">選取您想要核准或拒絕的要求，然後按一下與您的決策相對應之動作列上的按鈕：</span><span class="sxs-lookup"><span data-stu-id="49887-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="49887-156">提供我的核准/拒絕理由</span><span class="sxs-lookup"><span data-stu-id="49887-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="49887-157">這將開啟新的刀鋒視窗，一次核准或拒絕多個要求。</span><span class="sxs-lookup"><span data-stu-id="49887-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="49887-158">輸入您的決策理由，然後按一下底端或刀鋒視窗中的 [核准] \(或 [拒絕])：</span><span class="sxs-lookup"><span data-stu-id="49887-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="49887-159">當要求程序完成時，狀態符號將會反映您所做的決策 (在此範例中，決策是核准)：</span><span class="sxs-lookup"><span data-stu-id="49887-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="49887-160">要求啟用需要核准的角色</span><span class="sxs-lookup"><span data-stu-id="49887-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="49887-161">要求啟用需要核准的角色可從舊的 PIM 導覽或新的導覽中起始，因為啟用角色的程序仍維持不變。</span><span class="sxs-lookup"><span data-stu-id="49887-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="49887-162">只需從角色清單中選取要啟用的角色：</span><span class="sxs-lookup"><span data-stu-id="49887-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="49887-163">如果特殊權限角色需要 Multi-Factor Authentication，系統將提示您先完成該工作：</span><span class="sxs-lookup"><span data-stu-id="49887-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="49887-164">完成之後，按一下 [啟用] 並提供理由 (如有必要)：</span><span class="sxs-lookup"><span data-stu-id="49887-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="49887-165">要求者將會看到要求正在等待核准的通知：</span><span class="sxs-lookup"><span data-stu-id="49887-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="49887-166">檢視要啟用之要求的狀態</span><span class="sxs-lookup"><span data-stu-id="49887-166">View the status of your request to activate</span></span>

<span data-ttu-id="49887-167">檢視要啟用之要求的狀態，必須從新的導覽中加以存取。</span><span class="sxs-lookup"><span data-stu-id="49887-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="49887-168">從左側導覽列中，選取 [我的要求] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="49887-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="49887-169">要求狀態預設為「待決」，但您可以切換為查看所有或拒絕的要求。</span><span class="sxs-lookup"><span data-stu-id="49887-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="49887-170">如果已核准啟用，在 Azure AD 中完成您的工作</span><span class="sxs-lookup"><span data-stu-id="49887-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="49887-171">要求一經核准，角色即會處於作用中狀態，而您就能繼續進行任何要求此角色的工作。</span><span class="sxs-lookup"><span data-stu-id="49887-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="49887-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49887-172">Next steps</span></span>

<span data-ttu-id="49887-173">您的意見反應對我們非常寶貴。</span><span class="sxs-lookup"><span data-stu-id="49887-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="49887-174">隨時歡迎在此處與我們分享註解或意見反應！</span><span class="sxs-lookup"><span data-stu-id="49887-174">Please feel free to share comments or feedback with us here!</span></span>
