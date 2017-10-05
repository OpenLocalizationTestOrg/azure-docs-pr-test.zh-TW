---
title: "Azure Active Directory 入口網站中的稽核活動報告 | Microsoft Docs"
description: "介紹 Azure Active Directory 入口網站中的稽核活動報告"
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
ms.openlocfilehash: f2d0332d815c82d7d47625e020de2e9c5099deeb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="3486a-103">Azure Active Directory 入口網站中的稽核活動報告</span><span class="sxs-lookup"><span data-stu-id="3486a-103">Audit activity reports in the Azure Active Directory portal</span></span> 

<span data-ttu-id="3486a-104">透過 Azure Active Directory 中的報告，您可以取得判斷您的環境執行狀況所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="3486a-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="3486a-105">Azure AD 中的報告架構包含下列元件：</span><span class="sxs-lookup"><span data-stu-id="3486a-105">The reporting architecture in Azure AD consists of the following components:</span></span>

- <span data-ttu-id="3486a-106">**活動**</span><span class="sxs-lookup"><span data-stu-id="3486a-106">**Activity**</span></span> 
    - <span data-ttu-id="3486a-107">**登入活動** – 受管理應用程式和使用者登入活動的使用情況相關資訊</span><span class="sxs-lookup"><span data-stu-id="3486a-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="3486a-108">**稽核記錄** - 關於使用者和群組管理、受管理應用程式和目錄活動的系統活動資訊。</span><span class="sxs-lookup"><span data-stu-id="3486a-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="3486a-109">**安全性**</span><span class="sxs-lookup"><span data-stu-id="3486a-109">**Security**</span></span> 
    - <span data-ttu-id="3486a-110">**有風險的登入** - 有風險的登入表示非使用者帳戶合法擁有者的某人嘗試登入。</span><span class="sxs-lookup"><span data-stu-id="3486a-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="3486a-111">如需詳細資訊，請參閱＜有風險的登入＞。</span><span class="sxs-lookup"><span data-stu-id="3486a-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="3486a-112">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3486a-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="3486a-113">如需詳細資訊，請參閱＜標幟為有風險的使用者＞。</span><span class="sxs-lookup"><span data-stu-id="3486a-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="3486a-114">本主題提供稽核活動的概觀。</span><span class="sxs-lookup"><span data-stu-id="3486a-114">This topic gives you an overview of the audit activities.</span></span>
 
## <a name="who-can-access-the-data"></a><span data-ttu-id="3486a-115">誰可以存取資料？</span><span class="sxs-lookup"><span data-stu-id="3486a-115">Who can access the data?</span></span>
* <span data-ttu-id="3486a-116">具有安全性系統管理員或安全性讀取器角色的使用者</span><span class="sxs-lookup"><span data-stu-id="3486a-116">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="3486a-117">全域管理員</span><span class="sxs-lookup"><span data-stu-id="3486a-117">Global Admins</span></span>
* <span data-ttu-id="3486a-118">個別使用者 (非系統管理員) 可以看到自己的活動</span><span class="sxs-lookup"><span data-stu-id="3486a-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="3486a-119">稽核記錄</span><span class="sxs-lookup"><span data-stu-id="3486a-119">Audit logs</span></span>

<span data-ttu-id="3486a-120">Azure Active Directory 中的稽核記錄會提供符合規範的系統活動記錄。</span><span class="sxs-lookup"><span data-stu-id="3486a-120">The audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="3486a-121">所有稽核資料的第一個進入點是 [Azure Active Directory] 的 [活動] 區段中的 [稽核記錄]。</span><span class="sxs-lookup"><span data-stu-id="3486a-121">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="3486a-122">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/61.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="3486a-123">稽核記錄的預設清單檢視顯示︰</span><span class="sxs-lookup"><span data-stu-id="3486a-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="3486a-124">發生時間與日期</span><span class="sxs-lookup"><span data-stu-id="3486a-124">the date and time of the occurrence</span></span>
- <span data-ttu-id="3486a-125">活動的啟動器/動作項目 (對象)</span><span class="sxs-lookup"><span data-stu-id="3486a-125">the initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="3486a-126">活動 (項目)</span><span class="sxs-lookup"><span data-stu-id="3486a-126">the activity (*what*)</span></span> 
- <span data-ttu-id="3486a-127">目標</span><span class="sxs-lookup"><span data-stu-id="3486a-127">the target</span></span>

<span data-ttu-id="3486a-128">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/18.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="3486a-129">您可以按一下工具列中的 [資料行] 來自訂清單檢視。</span><span class="sxs-lookup"><span data-stu-id="3486a-129">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="3486a-130">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/19.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="3486a-131">這可讓您顯示其他欄位，或移除已顯示的欄位。</span><span class="sxs-lookup"><span data-stu-id="3486a-131">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="3486a-132">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/21.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="3486a-133">按一下清單檢視中的項目，即可取得所有可用的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3486a-133">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="3486a-134">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/22.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="3486a-135">篩選稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="3486a-135">Filtering audit logs</span></span>

<span data-ttu-id="3486a-136">若要將報告的資料縮小至您適用的層級，您可以使用下列欄位篩選稽核資料︰</span><span class="sxs-lookup"><span data-stu-id="3486a-136">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="3486a-137">日期範圍</span><span class="sxs-lookup"><span data-stu-id="3486a-137">Date range</span></span>
- <span data-ttu-id="3486a-138">啟動者 (執行者)</span><span class="sxs-lookup"><span data-stu-id="3486a-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="3486a-139">類別</span><span class="sxs-lookup"><span data-stu-id="3486a-139">Category</span></span>
- <span data-ttu-id="3486a-140">活動資源類型</span><span class="sxs-lookup"><span data-stu-id="3486a-140">Activity resource type</span></span>
- <span data-ttu-id="3486a-141">活動</span><span class="sxs-lookup"><span data-stu-id="3486a-141">Activity</span></span>

<span data-ttu-id="3486a-142">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/23.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="3486a-143">**日期範圍**篩選條件可讓您定義傳回資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="3486a-143">The **date range** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="3486a-144">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="3486a-144">Possible values are:</span></span>

- <span data-ttu-id="3486a-145">1 個月</span><span class="sxs-lookup"><span data-stu-id="3486a-145">1 month</span></span>
- <span data-ttu-id="3486a-146">7 天</span><span class="sxs-lookup"><span data-stu-id="3486a-146">7 days</span></span>
- <span data-ttu-id="3486a-147">24 小時</span><span class="sxs-lookup"><span data-stu-id="3486a-147">24 hours</span></span>
- <span data-ttu-id="3486a-148">自訂</span><span class="sxs-lookup"><span data-stu-id="3486a-148">Custom</span></span>

<span data-ttu-id="3486a-149">當您選取自訂時間範圍時，可以設定開始時間和結束時間。</span><span class="sxs-lookup"><span data-stu-id="3486a-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="3486a-150">**啟動者**篩選條件可讓您定義執行者的名稱或其萬用主體名稱 (UPN)。</span><span class="sxs-lookup"><span data-stu-id="3486a-150">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="3486a-151">**類別**篩選條件可讓您選取下列其中一個篩選條件︰</span><span class="sxs-lookup"><span data-stu-id="3486a-151">The **category** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="3486a-152">全部</span><span class="sxs-lookup"><span data-stu-id="3486a-152">All</span></span>
- <span data-ttu-id="3486a-153">核心類別</span><span class="sxs-lookup"><span data-stu-id="3486a-153">Core category</span></span>
- <span data-ttu-id="3486a-154">核心目錄</span><span class="sxs-lookup"><span data-stu-id="3486a-154">Core directory</span></span>
- <span data-ttu-id="3486a-155">自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="3486a-155">Self-service password management</span></span>
- <span data-ttu-id="3486a-156">自助式群組管理</span><span class="sxs-lookup"><span data-stu-id="3486a-156">Self-service group management</span></span>
- <span data-ttu-id="3486a-157">帳戶佈建 - 自動密碼變換</span><span class="sxs-lookup"><span data-stu-id="3486a-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="3486a-158">受邀的使用者</span><span class="sxs-lookup"><span data-stu-id="3486a-158">Invited users</span></span>
- <span data-ttu-id="3486a-159">MIM 服務</span><span class="sxs-lookup"><span data-stu-id="3486a-159">MIM service</span></span>
- <span data-ttu-id="3486a-160">身分識別保護</span><span class="sxs-lookup"><span data-stu-id="3486a-160">Identity Protection</span></span>
- <span data-ttu-id="3486a-161">B2C</span><span class="sxs-lookup"><span data-stu-id="3486a-161">B2C</span></span>

<span data-ttu-id="3486a-162">**活動資源類型**篩選條件可讓您選取下列其中一個篩選條件︰</span><span class="sxs-lookup"><span data-stu-id="3486a-162">The **activity resource type** filter enables you to select one of the following filters:</span></span>

- <span data-ttu-id="3486a-163">全部</span><span class="sxs-lookup"><span data-stu-id="3486a-163">All</span></span> 
- <span data-ttu-id="3486a-164">群組</span><span class="sxs-lookup"><span data-stu-id="3486a-164">Group</span></span>
- <span data-ttu-id="3486a-165">目錄</span><span class="sxs-lookup"><span data-stu-id="3486a-165">Directory</span></span>
- <span data-ttu-id="3486a-166">User</span><span class="sxs-lookup"><span data-stu-id="3486a-166">User</span></span>
- <span data-ttu-id="3486a-167">應用程式</span><span class="sxs-lookup"><span data-stu-id="3486a-167">Application</span></span>
- <span data-ttu-id="3486a-168">原則</span><span class="sxs-lookup"><span data-stu-id="3486a-168">Policy</span></span>
- <span data-ttu-id="3486a-169">裝置</span><span class="sxs-lookup"><span data-stu-id="3486a-169">Device</span></span>
- <span data-ttu-id="3486a-170">其他</span><span class="sxs-lookup"><span data-stu-id="3486a-170">Other</span></span>

<span data-ttu-id="3486a-171">當您選取 [群組] 作為 [活動資源類型] 時，會取得可讓您也提供**來源**的額外篩選條件類別：</span><span class="sxs-lookup"><span data-stu-id="3486a-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span></span>

- <span data-ttu-id="3486a-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="3486a-172">Azure AD</span></span>
- <span data-ttu-id="3486a-173">O365</span><span class="sxs-lookup"><span data-stu-id="3486a-173">O365</span></span>


<span data-ttu-id="3486a-174">**活動**篩選條件是根據您類別和您選取的活動資源類型。</span><span class="sxs-lookup"><span data-stu-id="3486a-174">The **activity** filter is based on the category and Activity resource type selection you make.</span></span> <span data-ttu-id="3486a-175">您可以選取您想要查看的特定活動或選擇全部。</span><span class="sxs-lookup"><span data-stu-id="3486a-175">You can select a specific activity you want to see or choose all.</span></span> 

<span data-ttu-id="3486a-176">您可以使用圖形 API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta 來取得所有稽核活動的清單 (其中，$tenantdomain 是網域名稱)，或請參閱[稽核報告事件](active-directory-reporting-audit-events.md)一文。</span><span class="sxs-lookup"><span data-stu-id="3486a-176">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="3486a-177">稽核記錄快速鍵</span><span class="sxs-lookup"><span data-stu-id="3486a-177">Audit logs shortcuts</span></span>

<span data-ttu-id="3486a-178">除了 **Azure Active Directory** 之外，Azure 入口網站可提供您稽核資料的兩個額外進入點︰</span><span class="sxs-lookup"><span data-stu-id="3486a-178">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span></span>

- <span data-ttu-id="3486a-179">使用者和群組</span><span class="sxs-lookup"><span data-stu-id="3486a-179">Users and groups</span></span>
- <span data-ttu-id="3486a-180">企業應用程式</span><span class="sxs-lookup"><span data-stu-id="3486a-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="3486a-181">使用者和群組稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="3486a-181">Users and groups audit logs</span></span>

<span data-ttu-id="3486a-182">透過以使用者和群組為基礎的稽核報告，可以取得下列問題的解答︰</span><span class="sxs-lookup"><span data-stu-id="3486a-182">With user and group-based audit reports, you can get answers to questions such as:</span></span>

- <span data-ttu-id="3486a-183">使用者已套用哪些類型的更新？</span><span class="sxs-lookup"><span data-stu-id="3486a-183">What types of updates have been applied the users?</span></span>

- <span data-ttu-id="3486a-184">有多少使用者已變更？</span><span class="sxs-lookup"><span data-stu-id="3486a-184">How many users were changed?</span></span>

- <span data-ttu-id="3486a-185">有多少密碼已變更？</span><span class="sxs-lookup"><span data-stu-id="3486a-185">How many passwords were changed?</span></span>

- <span data-ttu-id="3486a-186">系統管理員已在目錄中執行哪些作業？</span><span class="sxs-lookup"><span data-stu-id="3486a-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="3486a-187">已新增的群組為何？</span><span class="sxs-lookup"><span data-stu-id="3486a-187">What are the groups that have been added?</span></span>

- <span data-ttu-id="3486a-188">群組有成員資格變更嗎？</span><span class="sxs-lookup"><span data-stu-id="3486a-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="3486a-189">群組的擁有者已變更嗎？</span><span class="sxs-lookup"><span data-stu-id="3486a-189">Have the owners of group been changed?</span></span>

- <span data-ttu-id="3486a-190">指派給群組或使用者的授權為何？</span><span class="sxs-lookup"><span data-stu-id="3486a-190">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="3486a-191">如果您只想檢閱使用者和群組相關的稽核資料，您可以在 [使用者和群組] 的 [活動] 區段中的 [稽核記錄] 之下找到篩選過的檢視。</span><span class="sxs-lookup"><span data-stu-id="3486a-191">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span></span> <span data-ttu-id="3486a-192">此進入點將 [使用者和群組] 作為預先選取的 [活動資源類型]。</span><span class="sxs-lookup"><span data-stu-id="3486a-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="3486a-193">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/93.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="3486a-194">企業應用程式稽核記錄</span><span class="sxs-lookup"><span data-stu-id="3486a-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="3486a-195">透過以應用程式為基礎的稽核報告，可以取得下列問題的解答︰</span><span class="sxs-lookup"><span data-stu-id="3486a-195">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="3486a-196">已新增或更新的應用程式為何？</span><span class="sxs-lookup"><span data-stu-id="3486a-196">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="3486a-197">已移除的應用程式為何？</span><span class="sxs-lookup"><span data-stu-id="3486a-197">What are the applications that have been removed?</span></span>
* <span data-ttu-id="3486a-198">應用程式的服務原則已變更嗎？</span><span class="sxs-lookup"><span data-stu-id="3486a-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="3486a-199">應用程式的名稱已變更嗎？</span><span class="sxs-lookup"><span data-stu-id="3486a-199">Have the names of applications been changed?</span></span>
* <span data-ttu-id="3486a-200">誰已同意應用程式？</span><span class="sxs-lookup"><span data-stu-id="3486a-200">Who gave consent to an application?</span></span>

<span data-ttu-id="3486a-201">如果您只想檢閱應用程式相關的稽核資料，您可以在 [企業應用程式] 刀鋒視窗的 [活動] 區段中的 [稽核記錄] 之下找到篩選過的檢視。</span><span class="sxs-lookup"><span data-stu-id="3486a-201">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span></span> <span data-ttu-id="3486a-202">此進入點將 [企業應用程式] 當作預先選取的 [活動資源類型]。</span><span class="sxs-lookup"><span data-stu-id="3486a-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="3486a-203">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/134.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="3486a-204">您可以將此檢視進一步向下篩選為只有 [群組] 或只有 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="3486a-204">You can filter this view further down to just **groups** or just **users**.</span></span>

<span data-ttu-id="3486a-205">![稽核記錄檔](./media/active-directory-reporting-activity-audit-logs/25.png "稽核記錄檔")</span><span class="sxs-lookup"><span data-stu-id="3486a-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="3486a-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3486a-206">Next steps</span></span>

<span data-ttu-id="3486a-207">如需報告概觀，請參閱 [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3486a-207">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

