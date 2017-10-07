---
title: "aaaAudit 活動報告會在 hello Azure Active Directory 入口網站 |Microsoft 文件"
description: "簡介 toohello 稽核 hello Azure Active Directory 入口網站中的活動報告"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="fc86e-103">稽核 hello Azure Active Directory 入口網站中的活動報告</span><span class="sxs-lookup"><span data-stu-id="fc86e-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="fc86e-104">您可以使用 Azure Active Directory (Azure AD) 中的報表，取得您需要您的環境執行的方式 toodetermine hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="fc86e-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="fc86e-105">hello Azure AD 中的報表架構包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc86e-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="fc86e-106">**活動**</span><span class="sxs-lookup"><span data-stu-id="fc86e-106">**Activity**</span></span> 
    - <span data-ttu-id="fc86e-107">**登入活動**– hello 使用量資訊的受管理的應用程式和使用者登入活動</span><span class="sxs-lookup"><span data-stu-id="fc86e-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="fc86e-108">**稽核記錄** - 關於使用者和群組管理、受管理應用程式和目錄活動的系統活動資訊。</span><span class="sxs-lookup"><span data-stu-id="fc86e-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="fc86e-109">**安全性**</span><span class="sxs-lookup"><span data-stu-id="fc86e-109">**Security**</span></span> 
    - <span data-ttu-id="fc86e-110">**高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。</span><span class="sxs-lookup"><span data-stu-id="fc86e-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="fc86e-111">如需詳細資訊，請參閱＜有風險的登入＞。</span><span class="sxs-lookup"><span data-stu-id="fc86e-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="fc86e-112">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc86e-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="fc86e-113">如需詳細資訊，請參閱＜標幟為有風險的使用者＞。</span><span class="sxs-lookup"><span data-stu-id="fc86e-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="fc86e-114">本主題提供 hello 稽核活動的概觀。</span><span class="sxs-lookup"><span data-stu-id="fc86e-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="fc86e-115">誰可以存取 hello 資料？</span><span class="sxs-lookup"><span data-stu-id="fc86e-115">Who can access hello data?</span></span>
* <span data-ttu-id="fc86e-116">Hello 安全性系統管理員或安全性 Reader 角色中的使用者</span><span class="sxs-lookup"><span data-stu-id="fc86e-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="fc86e-117">全域管理員</span><span class="sxs-lookup"><span data-stu-id="fc86e-117">Global Admins</span></span>
* <span data-ttu-id="fc86e-118">個別使用者 (非系統管理員) 可以看到自己的活動</span><span class="sxs-lookup"><span data-stu-id="fc86e-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="fc86e-119">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="fc86e-119">Audit logs</span></span>

<span data-ttu-id="fc86e-120">Azure Active Directory 中的 hello 稽核記錄檔提供的相容性的系統活動記錄。</span><span class="sxs-lookup"><span data-stu-id="fc86e-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="fc86e-121">稽核資料您第一個項目點 tooall 是**稽核記錄檔**在 hello**活動**區段**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="fc86e-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="fc86e-122">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/61.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="fc86e-123">稽核記錄的預設清單檢視顯示︰</span><span class="sxs-lookup"><span data-stu-id="fc86e-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="fc86e-124">hello 日期和時間 hello 出現項目</span><span class="sxs-lookup"><span data-stu-id="fc86e-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="fc86e-125">hello 啟動器 / 動作項目 (*人員*) 的活動</span><span class="sxs-lookup"><span data-stu-id="fc86e-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="fc86e-126">hello 活動 (*什麼*)</span><span class="sxs-lookup"><span data-stu-id="fc86e-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="fc86e-127">hello 目標</span><span class="sxs-lookup"><span data-stu-id="fc86e-127">hello target</span></span>

<span data-ttu-id="fc86e-128">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/18.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="fc86e-129">您可以自訂 hello 清單檢視中，依序按一下**資料行**hello 工具列中。</span><span class="sxs-lookup"><span data-stu-id="fc86e-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="fc86e-130">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/19.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="fc86e-131">這可讓您 toodisplay 其他欄位，或移除已顯示的欄位。</span><span class="sxs-lookup"><span data-stu-id="fc86e-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="fc86e-132">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/21.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="fc86e-133">依序按一下 hello 清單檢視中的項目，您會取得所有可用的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fc86e-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="fc86e-134">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/22.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="fc86e-135">篩選稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="fc86e-135">Filtering audit logs</span></span>

<span data-ttu-id="fc86e-136">向下 hello toonarrow 報告資料 tooa 層級，適用於您，您可以篩選 hello 稽核資料，使用下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc86e-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="fc86e-137">日期範圍</span><span class="sxs-lookup"><span data-stu-id="fc86e-137">Date range</span></span>
- <span data-ttu-id="fc86e-138">啟動者 (執行者)</span><span class="sxs-lookup"><span data-stu-id="fc86e-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="fc86e-139">類別</span><span class="sxs-lookup"><span data-stu-id="fc86e-139">Category</span></span>
- <span data-ttu-id="fc86e-140">活動資源類型</span><span class="sxs-lookup"><span data-stu-id="fc86e-140">Activity resource type</span></span>
- <span data-ttu-id="fc86e-141">活動</span><span class="sxs-lookup"><span data-stu-id="fc86e-141">Activity</span></span>

<span data-ttu-id="fc86e-142">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/23.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="fc86e-143">hello**日期範圍**篩選器可讓 tooyou toodefine hello 的時間範圍內傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="fc86e-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="fc86e-144">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="fc86e-144">Possible values are:</span></span>

- <span data-ttu-id="fc86e-145">1 個月</span><span class="sxs-lookup"><span data-stu-id="fc86e-145">1 month</span></span>
- <span data-ttu-id="fc86e-146">7 天</span><span class="sxs-lookup"><span data-stu-id="fc86e-146">7 days</span></span>
- <span data-ttu-id="fc86e-147">24 小時</span><span class="sxs-lookup"><span data-stu-id="fc86e-147">24 hours</span></span>
- <span data-ttu-id="fc86e-148">自訂</span><span class="sxs-lookup"><span data-stu-id="fc86e-148">Custom</span></span>

<span data-ttu-id="fc86e-149">當您選取自訂時間範圍時，可以設定開始時間和結束時間。</span><span class="sxs-lookup"><span data-stu-id="fc86e-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="fc86e-150">hello**由起始**篩選器可讓您 toodefine 演員姓名或其通用主要名稱 (UPN)。</span><span class="sxs-lookup"><span data-stu-id="fc86e-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="fc86e-151">hello**類別**篩選器可讓您的下列篩選器的 hello tooselect 其中一個：</span><span class="sxs-lookup"><span data-stu-id="fc86e-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="fc86e-152">全部</span><span class="sxs-lookup"><span data-stu-id="fc86e-152">All</span></span>
- <span data-ttu-id="fc86e-153">核心類別</span><span class="sxs-lookup"><span data-stu-id="fc86e-153">Core category</span></span>
- <span data-ttu-id="fc86e-154">核心目錄</span><span class="sxs-lookup"><span data-stu-id="fc86e-154">Core directory</span></span>
- <span data-ttu-id="fc86e-155">自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="fc86e-155">Self-service password management</span></span>
- <span data-ttu-id="fc86e-156">自助式群組管理</span><span class="sxs-lookup"><span data-stu-id="fc86e-156">Self-service group management</span></span>
- <span data-ttu-id="fc86e-157">帳戶佈建 - 自動密碼變換</span><span class="sxs-lookup"><span data-stu-id="fc86e-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="fc86e-158">受邀的使用者</span><span class="sxs-lookup"><span data-stu-id="fc86e-158">Invited users</span></span>
- <span data-ttu-id="fc86e-159">MIM 服務</span><span class="sxs-lookup"><span data-stu-id="fc86e-159">MIM service</span></span>
- <span data-ttu-id="fc86e-160">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="fc86e-160">Identity Protection</span></span>
- <span data-ttu-id="fc86e-161">B2C</span><span class="sxs-lookup"><span data-stu-id="fc86e-161">B2C</span></span>

<span data-ttu-id="fc86e-162">hello**活動資源類型**篩選器可讓您 tooselect hello 下列其中一種篩選：</span><span class="sxs-lookup"><span data-stu-id="fc86e-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="fc86e-163">全部</span><span class="sxs-lookup"><span data-stu-id="fc86e-163">All</span></span> 
- <span data-ttu-id="fc86e-164">群組</span><span class="sxs-lookup"><span data-stu-id="fc86e-164">Group</span></span>
- <span data-ttu-id="fc86e-165">目錄</span><span class="sxs-lookup"><span data-stu-id="fc86e-165">Directory</span></span>
- <span data-ttu-id="fc86e-166">User</span><span class="sxs-lookup"><span data-stu-id="fc86e-166">User</span></span>
- <span data-ttu-id="fc86e-167">應用程式</span><span class="sxs-lookup"><span data-stu-id="fc86e-167">Application</span></span>
- <span data-ttu-id="fc86e-168">原則</span><span class="sxs-lookup"><span data-stu-id="fc86e-168">Policy</span></span>
- <span data-ttu-id="fc86e-169">裝置</span><span class="sxs-lookup"><span data-stu-id="fc86e-169">Device</span></span>
- <span data-ttu-id="fc86e-170">其他</span><span class="sxs-lookup"><span data-stu-id="fc86e-170">Other</span></span>

<span data-ttu-id="fc86e-171">當您選取**群組**為**活動資源類型**，tooalso 取得額外的篩選條件分類，可讓您提供**來源**:</span><span class="sxs-lookup"><span data-stu-id="fc86e-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="fc86e-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc86e-172">Azure AD</span></span>
- <span data-ttu-id="fc86e-173">O365</span><span class="sxs-lookup"><span data-stu-id="fc86e-173">O365</span></span>


<span data-ttu-id="fc86e-174">hello**活動**篩選根據 hello 類別和活動資源類型進行的選取項目。</span><span class="sxs-lookup"><span data-stu-id="fc86e-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="fc86e-175">您可以選取您想要 toosee 或選擇所有的特定活動。</span><span class="sxs-lookup"><span data-stu-id="fc86e-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="fc86e-176">您可以取得所有的稽核活動 hello 清單使用 auditActivityTypes/tenantdomain/活動 hello Graph API https://graph.windows.net/$？ api 版本 = beta，其中 $tenantdomain = 網域名稱，或參閱 toohello 文章[稽核報告事件](active-directory-reporting-audit-events.md)。</span><span class="sxs-lookup"><span data-stu-id="fc86e-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="fc86e-177">稽核記錄快速鍵</span><span class="sxs-lookup"><span data-stu-id="fc86e-177">Audit logs shortcuts</span></span>

<span data-ttu-id="fc86e-178">此外太**Azure Active Directory**，hello Azure 入口網站為您提供兩個其他的進入點 tooaudit 資料：</span><span class="sxs-lookup"><span data-stu-id="fc86e-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="fc86e-179">使用者和群組</span><span class="sxs-lookup"><span data-stu-id="fc86e-179">Users and groups</span></span>
- <span data-ttu-id="fc86e-180">企業應用程式</span><span class="sxs-lookup"><span data-stu-id="fc86e-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="fc86e-181">使用者和群組稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="fc86e-181">Users and groups audit logs</span></span>

<span data-ttu-id="fc86e-182">與使用者和群組為基礎的稽核報表，您可以取得答案 tooquestions，例如：</span><span class="sxs-lookup"><span data-stu-id="fc86e-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="fc86e-183">哪些類型的更新已套用的 hello 使用者？</span><span class="sxs-lookup"><span data-stu-id="fc86e-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="fc86e-184">有多少使用者已變更？</span><span class="sxs-lookup"><span data-stu-id="fc86e-184">How many users were changed?</span></span>

- <span data-ttu-id="fc86e-185">有多少密碼已變更？</span><span class="sxs-lookup"><span data-stu-id="fc86e-185">How many passwords were changed?</span></span>

- <span data-ttu-id="fc86e-186">系統管理員已在目錄中執行哪些作業？</span><span class="sxs-lookup"><span data-stu-id="fc86e-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="fc86e-187">已加入的 hello 群組有哪些？</span><span class="sxs-lookup"><span data-stu-id="fc86e-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="fc86e-188">群組有成員資格變更嗎？</span><span class="sxs-lookup"><span data-stu-id="fc86e-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="fc86e-189">已變更群組的 hello 擁有者嗎？</span><span class="sxs-lookup"><span data-stu-id="fc86e-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="fc86e-190">Tooa 群組或使用者已指派給哪些授權？</span><span class="sxs-lookup"><span data-stu-id="fc86e-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="fc86e-191">如果您只想 tooreview 稽核相關的 toousers 和群組的資料，您可以找到篩選過的檢視之下**稽核記錄檔**在 hello**活動**區段 hello**使用者和群組**.</span><span class="sxs-lookup"><span data-stu-id="fc86e-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="fc86e-192">此進入點將 [使用者和群組] 作為預先選取的 [活動資源類型]。</span><span class="sxs-lookup"><span data-stu-id="fc86e-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="fc86e-193">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/93.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="fc86e-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="fc86e-194">企業應用程式稽核記錄</span><span class="sxs-lookup"><span data-stu-id="fc86e-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="fc86e-195">與應用程式為基礎的稽核報告，您可以取得答案 tooquestions，例如：</span><span class="sxs-lookup"><span data-stu-id="fc86e-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="fc86e-196">已新增或更新的 hello 應用程式有哪些？</span><span class="sxs-lookup"><span data-stu-id="fc86e-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="fc86e-197">已移除的 hello 應用程式有哪些？</span><span class="sxs-lookup"><span data-stu-id="fc86e-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="fc86e-198">應用程式的服務原則已變更嗎？</span><span class="sxs-lookup"><span data-stu-id="fc86e-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="fc86e-199">Hello 應用程式名稱已經變更？</span><span class="sxs-lookup"><span data-stu-id="fc86e-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="fc86e-200">使用者提供同意 tooan 應用程式？</span><span class="sxs-lookup"><span data-stu-id="fc86e-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="fc86e-201">如果您只想 tooreview 稽核相關的 tooyour 應用程式的資料，您可以找到篩選過的檢視之下**稽核記錄檔**在 hello**活動**區段 hello**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fc86e-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="fc86e-202">此進入點將 [企業應用程式] 當作預先選取的 [活動資源類型]。</span><span class="sxs-lookup"><span data-stu-id="fc86e-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="fc86e-203">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/134.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="fc86e-204">您可以篩選此檢視進一步向下 toojust**群組**或簡稱**使用者**。</span><span class="sxs-lookup"><span data-stu-id="fc86e-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="fc86e-205">![稽核記錄](./media/active-directory-reporting-activity-audit-logs/25.png "稽核記錄")</span><span class="sxs-lookup"><span data-stu-id="fc86e-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="fc86e-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc86e-206">Next steps</span></span>

<span data-ttu-id="fc86e-207">如需報告的概觀，請參閱 hello [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fc86e-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

