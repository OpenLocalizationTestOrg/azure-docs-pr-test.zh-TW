---
title: "aaaAzure Privileged Identity Management 核准工作流程 |Microsoft 文件"
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
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="7b225-103">核准 (預覽)</span><span class="sxs-lookup"><span data-stu-id="7b225-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="7b225-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7b225-104">Overview</span></span>

<span data-ttu-id="7b225-105">具有 Privileged Identity Management 的核准，您可以設定來啟動角色 toorequire 核准，並選擇一個或多個使用者或群組為委派的核准者。</span><span class="sxs-lookup"><span data-stu-id="7b225-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="7b225-106">如何保留讀取 toolearn tooconfigure 角色選取核准者。</span><span class="sxs-lookup"><span data-stu-id="7b225-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="7b225-107">請記住，這項功能仍處於開發階段，而您可能會遇到 Bug。</span><span class="sxs-lookup"><span data-stu-id="7b225-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="7b225-108">hello 功能，包括文字和命名慣例可能會有所變更，而且不應視為最後。</span><span class="sxs-lookup"><span data-stu-id="7b225-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="7b225-109">重要術語</span><span class="sxs-lookup"><span data-stu-id="7b225-109">Key Terminology</span></span>

<span data-ttu-id="7b225-110">*符合資格的角色使用者*– 符合資格的角色的使用者是使用已被指派為合格 tooan Azure AD 角色您組織內 （角色需要啟用）。</span><span class="sxs-lookup"><span data-stu-id="7b225-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="7b225-111">*委派核准者*：委派核准者是您 Azure AD 內的一或多個個人或群組，其負責核准啟用角色的要求。</span><span class="sxs-lookup"><span data-stu-id="7b225-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="7b225-112">案例</span><span class="sxs-lookup"><span data-stu-id="7b225-112">Scenarios</span></span>

<span data-ttu-id="7b225-113">hello 私人預覽支援下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b225-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="7b225-114">**身為特殊權限角色管理員 (PRA)，您可以：**</span><span class="sxs-lookup"><span data-stu-id="7b225-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="7b225-115">啟用特定角色的核准</span><span class="sxs-lookup"><span data-stu-id="7b225-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="7b225-116">指定核准者 tooapprove 要求使用者和/或群組</span><span class="sxs-lookup"><span data-stu-id="7b225-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="7b225-117">檢視所有特殊權限角色的要求和核准歷程記錄</span><span class="sxs-lookup"><span data-stu-id="7b225-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="7b225-118">**身為指定的核准者，您可以：**</span><span class="sxs-lookup"><span data-stu-id="7b225-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="7b225-119">檢視待決的核准 (要求)</span><span class="sxs-lookup"><span data-stu-id="7b225-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="7b225-120">核准或拒絕提高角色權限 (單一和/或大量) 的要求</span><span class="sxs-lookup"><span data-stu-id="7b225-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="7b225-121">提供我的核准/拒絕理由</span><span class="sxs-lookup"><span data-stu-id="7b225-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="7b225-122">**身為合格角色使用者，您可以：**</span><span class="sxs-lookup"><span data-stu-id="7b225-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="7b225-123">要求啟用需要核准的角色</span><span class="sxs-lookup"><span data-stu-id="7b225-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="7b225-124">檢視要求 tooactivate hello 狀態</span><span class="sxs-lookup"><span data-stu-id="7b225-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="7b225-125">如果已核准啟用，在 Azure AD 中完成您的工作</span><span class="sxs-lookup"><span data-stu-id="7b225-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="7b225-126">導覽</span><span class="sxs-lookup"><span data-stu-id="7b225-126">Navigation</span></span>

<span data-ttu-id="7b225-127">我們已更新 hello 瀏覽 toosupport 核准</span><span class="sxs-lookup"><span data-stu-id="7b225-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="7b225-128">hello 預設登陸頁面會提供方便的方式存取 tooinformation 有關 PIM 和 hello 新核准文件。</span><span class="sxs-lookup"><span data-stu-id="7b225-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="7b225-129">我們也針對 PIM [我的稽核歷程記錄] 的所有使用者新增了新的區段。</span><span class="sxs-lookup"><span data-stu-id="7b225-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="7b225-130">您可以在這裡找到所有 hello 資訊相關 tooyour 身分識別。</span><span class="sxs-lookup"><span data-stu-id="7b225-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="7b225-131">這包括所有擱置中和已完成要求，任何有關 hello 要求您解決時，所做的決策和您過去的角色啟用在一個方便的位置。</span><span class="sxs-lookup"><span data-stu-id="7b225-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="7b225-132">啟用特定角色的核准</span><span class="sxs-lookup"><span data-stu-id="7b225-132">Enable approval for specific roles</span></span>

<span data-ttu-id="7b225-133">tooenable 核准對於特定的角色，請先選取從 hello 左方瀏覽的目錄角色。</span><span class="sxs-lookup"><span data-stu-id="7b225-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="7b225-134">尋找並選取 hello 左側瀏覽目錄角色中的設定</span><span class="sxs-lookup"><span data-stu-id="7b225-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="7b225-135">選取 [特殊權限角色]：</span><span class="sxs-lookup"><span data-stu-id="7b225-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="7b225-136">選取 [啟用] 在 hello 需要核准章節：</span><span class="sxs-lookup"><span data-stu-id="7b225-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="7b225-137">一旦啟用，hello 刀鋒視窗會展開 tooshow hello 下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="7b225-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="7b225-138">如果您不指定任何核准者，hello PRA(s) 變成 hello 預設核准者。</span><span class="sxs-lookup"><span data-stu-id="7b225-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="7b225-139">PRA(s) 就是所有的啟用要求此角色的必要的 tooapprove。</span><span class="sxs-lookup"><span data-stu-id="7b225-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="7b225-140">指定核准者 tooapprove 要求使用者和/或群組</span><span class="sxs-lookup"><span data-stu-id="7b225-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="7b225-141">toodelegate 核准按一下 hello 選項太 「 選取核准者 」:</span><span class="sxs-lookup"><span data-stu-id="7b225-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="7b225-142">刀鋒視窗中選取的核准者 hello 載入時，您可能會搜尋特定使用者或群組使用 hello 搜尋列 hello 上方，或從 hello 預先填入的清單中選取，然後按一下 「 選取 」 完成時：</span><span class="sxs-lookup"><span data-stu-id="7b225-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="7b225-143">注意︰您可以同時選取多個使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="7b225-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="7b225-144">您的選擇會顯示在選取的核准者的 hello 清單中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7b225-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="7b225-145">tooremove 核准者，只要按一下 hello 移除按鈕下一步 tootheir 的名稱。</span><span class="sxs-lookup"><span data-stu-id="7b225-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="7b225-146">tooadd 其他核准者，重複 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="7b225-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="7b225-147">檢視所有特殊權限角色的要求和核准歷程記錄</span><span class="sxs-lookup"><span data-stu-id="7b225-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="7b225-148">對於所有特殊權限的角色，tooview 要求和核准歷程記錄選取稽核歷程從 hello 儀表板：</span><span class="sxs-lookup"><span data-stu-id="7b225-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="7b225-149">您可以 hello 依排序資料的動作，並尋找"Approved 啟用"</span><span class="sxs-lookup"><span data-stu-id="7b225-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="7b225-150">檢視待決的核准 (要求)</span><span class="sxs-lookup"><span data-stu-id="7b225-150">View pending approvals (requests)</span></span>

<span data-ttu-id="7b225-151">身為委派核准者，當要求正在等待您的核准時，您將會收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="7b225-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="7b225-152">tooview hello PIM 入口網站，從 hello （在 hello 新的瀏覽） 的儀表板選取 hello 「 暫止核准要求 」 索引標籤中的這些要求左導覽列。</span><span class="sxs-lookup"><span data-stu-id="7b225-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="7b225-153">您將在該處看到一份等待核准的要求清單：</span><span class="sxs-lookup"><span data-stu-id="7b225-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="7b225-154">核准或拒絕提高角色權限 (單一和/或大量) 的要求</span><span class="sxs-lookup"><span data-stu-id="7b225-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="7b225-155">選取您想 tooapprove 或拒絕的 hello 要求，再按一下對應於您的決定動作列中的 hello 按鈕：</span><span class="sxs-lookup"><span data-stu-id="7b225-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="7b225-156">提供我的核准/拒絕理由</span><span class="sxs-lookup"><span data-stu-id="7b225-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="7b225-157">這將會開啟新的刀鋒視窗 tooapprove 或拒絕多個要求一次。</span><span class="sxs-lookup"><span data-stu-id="7b225-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="7b225-158">輸入您的決策，讓您的理由，並按一下核准 （或拒絕） 在 hello 底部或 hello 刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="7b225-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="7b225-159">Hello 狀態符號 hello 要求程序完成時，會反映您所做的決定 （在此範例中，hello 決策是核准）：</span><span class="sxs-lookup"><span data-stu-id="7b225-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="7b225-160">要求啟用需要核准的角色</span><span class="sxs-lookup"><span data-stu-id="7b225-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="7b225-161">要求需要核准，可能會起始從 hello 舊 PIM 瀏覽或 hello 新瀏覽角色的啟用，為 hello 程序會維持為角色啟動 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="7b225-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="7b225-162">從 hello 要啟動之角色的清單，只需選取角色：</span><span class="sxs-lookup"><span data-stu-id="7b225-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="7b225-163">如果特殊權限角色需要 Multi-Factor Authentication，系統將提示您先完成該工作：</span><span class="sxs-lookup"><span data-stu-id="7b225-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="7b225-164">完成之後，按一下 [啟用] 並提供理由 (如有必要)：</span><span class="sxs-lookup"><span data-stu-id="7b225-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="7b225-165">hello 要求者會看到通知，hello 要求正在等待核准：</span><span class="sxs-lookup"><span data-stu-id="7b225-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="7b225-166">檢視連線的要求 tooactivate hello 狀態</span><span class="sxs-lookup"><span data-stu-id="7b225-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="7b225-167">從新的瀏覽必須存取檢視的暫止要求 tooactivate hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="7b225-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="7b225-168">從 hello 左的導覽列中，選取 hello 「 我的要求 」 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="7b225-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="7b225-169">hello 要求狀態太預設 「 擱置 」，但您可以切換所有 toosee 或拒絕要求。</span><span class="sxs-lookup"><span data-stu-id="7b225-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="7b225-170">如果已核准啟用，在 Azure AD 中完成您的工作</span><span class="sxs-lookup"><span data-stu-id="7b225-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="7b225-171">Hello 要求獲得核准後，一旦 hello 角色作用中，您就可以進行任何需要的工作，此角色。</span><span class="sxs-lookup"><span data-stu-id="7b225-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="7b225-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b225-172">Next steps</span></span>

<span data-ttu-id="7b225-173">您的意見反應會很有價值 toous。</span><span class="sxs-lookup"><span data-stu-id="7b225-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="7b225-174">請隨時可用 tooshare 註解或意見反應與我們這裡 ！</span><span class="sxs-lookup"><span data-stu-id="7b225-174">Please feel free tooshare comments or feedback with us here!</span></span>
