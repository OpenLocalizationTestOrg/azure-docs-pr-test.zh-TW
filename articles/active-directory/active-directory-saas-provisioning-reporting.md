---
title: "關於 Azure Active Directory 自動對 SaaS 應用程式佈建使用者帳戶的報告 | Microsoft Docs"
description: "了解如何檢查使用者帳戶自動佈建作業的狀態，以及如何針對個別使用者的佈建進行疑難排解。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 86b9a3d93745045904c6038583b9bc6ebac5667e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a><span data-ttu-id="e2630-103">教學課程︰關於使用者帳戶自動佈建的報告</span><span class="sxs-lookup"><span data-stu-id="e2630-103">Tutorial: Reporting on automatic user account provisioning</span></span>


<span data-ttu-id="e2630-104">Azure Active Directory 含有[使用者帳戶佈建服務](active-directory-saas-app-provisioning.md)，可協助您在 SaaS 應用程式和其他系統中自動佈建和解除佈建使用者帳戶，以便進行端對端的身分識別生命週期管理。</span><span class="sxs-lookup"><span data-stu-id="e2630-104">Azure Active Directory includes a [user account provisioning service](active-directory-saas-app-provisioning.md) that helps automate the provisioning de-provisioning of user accounts in SaaS apps and other systems, for the purpose of end-to-end identity lifecycle management.</span></span> <span data-ttu-id="e2630-105">對於 [Azure AD 應用程式庫](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)之 [精選] 區段中的所有應用程式和系統，Azure AD 支援已預先整合的使用者佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="e2630-105">Azure AD supports pre-integrated user provisioning connectors for all of the applications and systems in the "Featured" section of the [Azure AD application gallery](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).</span></span>

<span data-ttu-id="e2630-106">本文會說明如何在佈建作業設定好之後檢查其狀態，以及如何針對個別使用者和群組的佈建進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="e2630-106">This article describes how to check the status of provisioning jobs after they have been set up, and how to troubleshoot the provisioning of individual users and groups.</span></span>

## <a name="overview"></a><span data-ttu-id="e2630-107">概觀</span><span class="sxs-lookup"><span data-stu-id="e2630-107">Overview</span></span>

<span data-ttu-id="e2630-108">我們主要會使用 [Azure 管理入口網站](https://portal.azure.com)，依照要佈建使用者帳戶之應用程式[所提供的文件](active-directory-saas-tutorial-list.md)來設定佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="e2630-108">Provisioning connectors are primarily set up and configured using the [Azure management portal](https://portal.azure.com), by following the [provided documentation](active-directory-saas-tutorial-list.md) for the application where user account provisioning is desired.</span></span> <span data-ttu-id="e2630-109">應用程式的佈建作業在設定好並開始執行後，您就可以使用下列兩種方法之一來獲得這些作業的報告︰</span><span class="sxs-lookup"><span data-stu-id="e2630-109">Once configured and running, provisioning jobs for an application can be reported on using one of two methods:</span></span>

* <span data-ttu-id="e2630-110">**Azure 管理入口網站** - 本文主要在說明如何從 [Azure 管理入口網站](https://portal.azure.com)擷取報告資訊，以同時獲得佈建摘要報告，以及給定應用程式的詳細佈建稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="e2630-110">**Azure management portal** - This article primarily describes retrieving report information from the [Azure management portal](https://portal.azure.com), which provides both a provisioning summary report as well as detailed provisioning audit logs for a given application.</span></span>

* <span data-ttu-id="e2630-111">**稽核 API** - Azure Active Directory 也會提供稽核 API，以便透過程式擷取詳細的佈建稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="e2630-111">**Audit API** - Azure Active Directory also provides an Audit API that enables programmatic retrieval of the detailed provisioning audit logs.</span></span> <span data-ttu-id="e2630-112">如需此 API 專屬的使用說明文件，請參閱 [Azure Active Directory 稽核 API 參考](active-directory-reporting-api-audit-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="e2630-112">See [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md) for documentation specific to using this API.</span></span> <span data-ttu-id="e2630-113">雖然本文未具體說明如何使用 API，但會詳細說明稽核記錄中所記下的佈建事件類型。</span><span class="sxs-lookup"><span data-stu-id="e2630-113">While this article does not specifically cover how to use the API, it does detail the types of provisioning events that are recorded in the audit log.</span></span>

### <a name="definitions"></a><span data-ttu-id="e2630-114">定義</span><span class="sxs-lookup"><span data-stu-id="e2630-114">Definitions</span></span>

<span data-ttu-id="e2630-115">本文會使用下列詞彙，其定義如下︰</span><span class="sxs-lookup"><span data-stu-id="e2630-115">This article uses the following terms, defined below:</span></span>

* <span data-ttu-id="e2630-116">**來源系統** - Azure AD 佈建服務用來進行同步處理的來源端使用者存放庫。</span><span class="sxs-lookup"><span data-stu-id="e2630-116">**Source System** - The repository of users that the Azure AD provisioning service synchronizes from.</span></span> <span data-ttu-id="e2630-117">已預先整合的佈建連接器大多使用 Azure Active Directory 作為來源系統，但有一些例外 (範例︰Workday 的輸入同步處理)。</span><span class="sxs-lookup"><span data-stu-id="e2630-117">Azure Active Directory is the source system for the majority of pre-integrated provisioning connectors, however there are some exceptions (example: Workday Inbound Synchronization).</span></span>

* <span data-ttu-id="e2630-118">**目標系統** - Azure AD 佈建服務用來進行同步處理的目標端使用者存放庫。</span><span class="sxs-lookup"><span data-stu-id="e2630-118">**Target System** - The repository of users that the Azure AD provisioning service synchronizes to.</span></span> <span data-ttu-id="e2630-119">這通常是 SaaS 應用程式 (範例︰Salesforce、ServiceNow、Google Apps、Dropbox for Business)，但在某些情況下，也可以是 Active Directory 之類的內部部署系統 (範例︰Workday 對 Active Directory 的輸入同步處理)。</span><span class="sxs-lookup"><span data-stu-id="e2630-119">This is typically a SaaS application (examples: Salesforce, ServiceNow, Google Apps, Dropbox for Business), but in some cases can be an on-premises system such as Active Directory (example: Workday Inbound Synchronization to Active Directory).</span></span>


## <a name="getting-provisioning-reports-from-the-azure-management-portal"></a><span data-ttu-id="e2630-120">從 Azure 管理入口網站取得佈建報告</span><span class="sxs-lookup"><span data-stu-id="e2630-120">Getting provisioning reports from the Azure management portal</span></span>

<span data-ttu-id="e2630-121">若要取得給定應用程式的佈建報告資訊，請先啟動 [Azure 管理入口網站](https://portal.azure.com)，然後瀏覽至要設定佈建作業的企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2630-121">To get provisioning report information for a given application, start by launching the [Azure management portal](https://portal.azure.com) and browsing to the Enterprise Application for which provisioning is configured.</span></span> <span data-ttu-id="e2630-122">例如，如果您要在 LinkedIn Elevate 中佈建使用者，則應用程式詳細資料的導覽路徑為︰</span><span class="sxs-lookup"><span data-stu-id="e2630-122">For example, if you are provisioning users to LinkedIn Elevate, the navigation path to the application details is:</span></span>

<span data-ttu-id="e2630-123">**Azure Active Directory > 企業應用程式 > 所有應用程式 > LinkedIn Elevate**</span><span class="sxs-lookup"><span data-stu-id="e2630-123">**Azure Active Directory > Enterprise Applications > All applications > LinkedIn Elevate**</span></span>

<span data-ttu-id="e2630-124">您可以從這裡取得佈建摘要報告和佈建稽核記錄，兩者的說明如下。</span><span class="sxs-lookup"><span data-stu-id="e2630-124">From here, you can access both the Provisioning summary report, and the provisioning audit logs, both described below.</span></span>


### <a name="provisioning-summary-report"></a><span data-ttu-id="e2630-125">佈建摘要報告</span><span class="sxs-lookup"><span data-stu-id="e2630-125">Provisioning summary report</span></span>

<span data-ttu-id="e2630-126">佈建摘要報告顯示在給定應用程式的 [佈建] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="e2630-126">The provisioning summary report is visible in the **Provisioning** tab for given application.</span></span> <span data-ttu-id="e2630-127">它位於 [設定] 底下的 [同步處理詳細資料] 區段中，並且會提供下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="e2630-127">It is located in the Synchronization Details section underneath **Settings**, and provides the following information:</span></span>

* <span data-ttu-id="e2630-128">已同步處理且目前正在來源系統與目標系統之間的佈建範圍內的使用者和群組總數。</span><span class="sxs-lookup"><span data-stu-id="e2630-128">The total number of users and/groups that have been synchronized and are currently in scope for provisioning between the source system and the target system.</span></span>

* <span data-ttu-id="e2630-129">上次執行同步處理的時間。</span><span class="sxs-lookup"><span data-stu-id="e2630-129">The last time the synchronization was run.</span></span> <span data-ttu-id="e2630-130">在完成完整的同步處理之後，系統通常每隔 20 到 40 分鐘就會進行一次同步處理。</span><span class="sxs-lookup"><span data-stu-id="e2630-130">Synchronizations typically occur every 20-40 minutes, after a full synchronization has completed.</span></span>

* <span data-ttu-id="e2630-131">是否已完成初次的完整同步處理。</span><span class="sxs-lookup"><span data-stu-id="e2630-131">Whether or not an initial full synchronization has been completed.</span></span>

* <span data-ttu-id="e2630-132">佈建程序是否已進入隔離狀態，以及造成隔離狀態的原因為何 (例如，由於系統管理認證無效而未能與目標系統通訊)</span><span class="sxs-lookup"><span data-stu-id="e2630-132">Whether or not the provisioning process has been placed in quarantine, and what the reason for the quarantine status is (e.g. failure to communicate with target system due to invalid admin credentials)</span></span>

<span data-ttu-id="e2630-133">系統管理員首先應該看的就是佈建摘要報告，以便了解佈建作業的作業健康情況。</span><span class="sxs-lookup"><span data-stu-id="e2630-133">The provisioning summary report should be the first place admins look to check on the operational health of the provisioning job.</span></span>

 ![摘要報告](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a><span data-ttu-id="e2630-135">佈建稽核記錄</span><span class="sxs-lookup"><span data-stu-id="e2630-135">Provisioning audit logs</span></span>
<span data-ttu-id="e2630-136">佈建服務所執行的活動全都會記錄在 Azure AD 稽核記錄中，您可以在 [帳戶佈建] 類別底下的 [稽核記錄] 索引標籤中檢視這些記錄。</span><span class="sxs-lookup"><span data-stu-id="e2630-136">All activities performed by the provisioning service are recorded in the Azure AD audit logs, which can be viewed in the **Audit logs** tab under the **Account Provisioning** category.</span></span> <span data-ttu-id="e2630-137">所記錄的活動事件類型包括︰</span><span class="sxs-lookup"><span data-stu-id="e2630-137">Logged activity event types include:</span></span>

* <span data-ttu-id="e2630-138">**匯入事件** - Azure AD 佈建服務每次從來源系統或目標系統擷取個別使用者或群組的相關資訊時，就會記錄下「匯入」事件。</span><span class="sxs-lookup"><span data-stu-id="e2630-138">**Import events** - An "import" event is recorded each time the Azure AD provisioning service retrieves information about an individual user or group from a source system or target system.</span></span> <span data-ttu-id="e2630-139">在同步處理期間，服務會先從來源系統擷取使用者，而其結果便會記錄為「匯入」事件。</span><span class="sxs-lookup"><span data-stu-id="e2630-139">During synchronization, users are retrieved from the source system first, with the results recorded as "import" events.</span></span> <span data-ttu-id="e2630-140">接著，服務便會對目標系統查詢所擷取使用者的比對識別碼，以檢查這些使用者是否存在，而其結果也會記錄為「匯入」事件。</span><span class="sxs-lookup"><span data-stu-id="e2630-140">The matching IDs of the retrieved users are then queried against the target system to check if they exist, with the results also recorded as "import" events.</span></span> <span data-ttu-id="e2630-141">這些事件會記錄下 Azure AD 佈建服務在事件發生當下所看到的所有對應使用者屬性與屬性值。</span><span class="sxs-lookup"><span data-stu-id="e2630-141">These events record all mapped user attributes and their values that were seen by the Azure AD provisioning service at the time of the event.</span></span> 

* <span data-ttu-id="e2630-142">**同步處理規則事件** - 這些事件會報告在服務已從來源和目標系統匯入使用者資料並加以評估後，屬性對應規則和任何已設定之範圍篩選的結果。</span><span class="sxs-lookup"><span data-stu-id="e2630-142">**Synchronization rule events** - These events report on the results of the attribute mapping rules and any configured scoping filters, after user data has been imported and evaluated from the source and target systems.</span></span> <span data-ttu-id="e2630-143">例如，如果服務認為來源系統中的使用者位於佈建範圍內，而且不存在於目標系統中，則此事件會記錄下「使用者將佈建到目標系統」。</span><span class="sxs-lookup"><span data-stu-id="e2630-143">For example, if a user in a source system is deemed to be in scope for provisioning, and deemed to not exist in the target system, then this event records that the user will be provisioned in the target system.</span></span> 

* <span data-ttu-id="e2630-144">**匯出事件** - Azure AD 佈建服務每次在目標系統中寫入使用者帳戶或群組物件時，就會記錄下「匯出」事件。</span><span class="sxs-lookup"><span data-stu-id="e2630-144">**Export events** - An "export" event is recorded each time the Azure AD provisioning service writes a user account or group object to a target system.</span></span> <span data-ttu-id="e2630-145">這些事件會記錄下 Azure AD 佈建服務在事件發生當下所寫入的所有使用者屬性與屬性值。</span><span class="sxs-lookup"><span data-stu-id="e2630-145">These events record all user attributes and their values that were written by the Azure AD provisioning service at the time of the event.</span></span> <span data-ttu-id="e2630-146">如果在目標系統中寫入使用者帳戶或群組物件時發生錯誤，則會在此顯示出來。</span><span class="sxs-lookup"><span data-stu-id="e2630-146">If there was an error while writing the user account or group object to the target system, it will be displayed here.</span></span>

* <span data-ttu-id="e2630-147">**處理序委付事件** - 當佈建服務在嘗試進行作業時遇到失敗，系統就會發生處理序委付事件，並開始在輪詢間隔時間重試此作業。</span><span class="sxs-lookup"><span data-stu-id="e2630-147">**Process escrow events** - Process escrows occur when the provisioning service encounters a failure while attempting an operation, and begins to retry the operation on a back-off interval of time.</span></span> <span data-ttu-id="e2630-148">每當服務淘汰佈建作業時，就會記錄下「委付」事件。</span><span class="sxs-lookup"><span data-stu-id="e2630-148">An "escrow" event is recorded each time a provisioning operation was retired.</span></span>

<span data-ttu-id="e2630-149">在查看個別使用者的佈建事件時，其事件的發生順序通常如下︰</span><span class="sxs-lookup"><span data-stu-id="e2630-149">When looking at provisioning events for an individual user, the events normally occur in this order:</span></span>

1. <span data-ttu-id="e2630-150">匯入事件︰從來源系統擷取使用者。</span><span class="sxs-lookup"><span data-stu-id="e2630-150">Import event: User is retrieved from the source system.</span></span>

2. <span data-ttu-id="e2630-151">匯入事件︰查詢目標系統以檢查所擷取的使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="e2630-151">Import event: Target system is queried to check for the existence of the retrieved user.</span></span>

3. <span data-ttu-id="e2630-152">同步處理規則事件︰對所設定的屬性對應規則與範圍篩選評估得自來源和目標系統的使用者資料，以判斷應該執行什麼動作 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="e2630-152">Synchronization rule event: User data from source and target systems are evaluated against the configured attribute mapping rules and scoping filters to determine what action, if any, should be performed.</span></span>

4. <span data-ttu-id="e2630-153">匯出事件︰如果同步處理規則事件指出應執行某動作 (例如，新增、更新或刪除)，則匯出事件中會記錄下該動作的執行結果。</span><span class="sxs-lookup"><span data-stu-id="e2630-153">Export event: If the synchronization rule event dictated that an action should be performed (e.g. Add, Update, Delete), then the results of the action are recorded in an Export event.</span></span>

![建立 Azure AD 測試使用者](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a><span data-ttu-id="e2630-155">查閱特定使用者的佈建事件</span><span class="sxs-lookup"><span data-stu-id="e2630-155">Looking up provisioning events for a specific user</span></span>

<span data-ttu-id="e2630-156">稽核記錄佈建最常見的使用案例是檢查個別使用者帳戶的佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="e2630-156">The most common use case for the provisioning audit logs is to check the provisioning status of an individual user account.</span></span> <span data-ttu-id="e2630-157">若要查閱特定使用者最新的佈建事件：</span><span class="sxs-lookup"><span data-stu-id="e2630-157">To look up the last provisioning events for a specific user:</span></span>

1. <span data-ttu-id="e2630-158">移至 [稽核記錄] 區段。</span><span class="sxs-lookup"><span data-stu-id="e2630-158">Go to the **Audit logs** section.</span></span>

2. <span data-ttu-id="e2630-159">在 [類別] 功能表上選取 [帳戶佈建]。</span><span class="sxs-lookup"><span data-stu-id="e2630-159">From the **Category** menu, select **Account Provisioning**.</span></span>

3. <span data-ttu-id="e2630-160">在 [日期範圍] 功能表上選取您要搜尋的日期範圍。</span><span class="sxs-lookup"><span data-stu-id="e2630-160">In the **Date Range** menu, select the date range you want to search,</span></span>

4. <span data-ttu-id="e2630-161">在 [搜尋] 列上輸入您要搜尋之使用者的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="e2630-161">In the **Search** bar, enter the user ID of the user you wish to search for.</span></span> <span data-ttu-id="e2630-162">識別碼值的格式應該要符合您選取作為屬性對應組態中主要比對識別碼的任何項目 (例如 userPrincipalName 或員工識別碼)。</span><span class="sxs-lookup"><span data-stu-id="e2630-162">The format of ID value should match whatever you selected as the primary matching ID in the attribute mapping configuration (e.g. userPrincipalName or employee ID number).</span></span> <span data-ttu-id="e2630-163">所需的識別碼值會顯示在 [目標] 資料行上。</span><span class="sxs-lookup"><span data-stu-id="e2630-163">The ID value required will be visible in the Target(s) column.</span></span>

5. <span data-ttu-id="e2630-164">按 Enter 鍵以開始搜尋。</span><span class="sxs-lookup"><span data-stu-id="e2630-164">Press Enter to search.</span></span> <span data-ttu-id="e2630-165">最新的佈建事件會最先傳回。</span><span class="sxs-lookup"><span data-stu-id="e2630-165">The most recent provisioning events will be returned first.</span></span>

6. <span data-ttu-id="e2630-166">在事件傳回後，請注意活動類型以及該活動是成功還失敗。</span><span class="sxs-lookup"><span data-stu-id="e2630-166">If events are returned, note the activity types and whether they succeeded or failed.</span></span> <span data-ttu-id="e2630-167">如果未傳回任何結果，則表示使用者不存在，或因為尚未完成完整同步處理，所以佈建程序未能偵測到。</span><span class="sxs-lookup"><span data-stu-id="e2630-167">If no results are returned, then it means the user either does not exist, or has not yet been detected by the provisioning process if a full sync has not yet completed.</span></span>

7. <span data-ttu-id="e2630-168">按一下個別事件可檢視延伸的詳細資料，包括作為事件一部分而擷取、評估或寫入的所有使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="e2630-168">Click on individual events to view extended details, including all user properties that were retrieved, evaluated, or written as part of the event.</span></span>


### <a name="tips-for-viewing-the-provisioning-audit-logs"></a><span data-ttu-id="e2630-169">佈建稽核記錄的檢視秘訣</span><span class="sxs-lookup"><span data-stu-id="e2630-169">Tips for viewing the provisioning audit logs</span></span>

<span data-ttu-id="e2630-170">為了清楚了解記錄，請在 Azure 入口網站中選取 [資料行] 按鈕，然後選擇下列資料行︰</span><span class="sxs-lookup"><span data-stu-id="e2630-170">For best readability in the Azure portal, select the **Columns** button and choose these columns:</span></span>

* <span data-ttu-id="e2630-171">**日期** - 顯示事件的發生日期。</span><span class="sxs-lookup"><span data-stu-id="e2630-171">**Date** - Shows the date the event occurred.</span></span>
* <span data-ttu-id="e2630-172">**目標** - 顯示身為事件主體的應用程式名稱和使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="e2630-172">**Target(s)** - Shows the app name and user ID that are the subjects of the event.</span></span>
* <span data-ttu-id="e2630-173">**活動** - 活動類型，其說明如前。</span><span class="sxs-lookup"><span data-stu-id="e2630-173">**Activity** - The activity type, as described previously.</span></span>
* <span data-ttu-id="e2630-174">**狀態** - 事件是否成功。</span><span class="sxs-lookup"><span data-stu-id="e2630-174">**Status** - Whether the event succeeded or not.</span></span>
* <span data-ttu-id="e2630-175">**狀態原因** - 佈建事件發生經過的摘要。</span><span class="sxs-lookup"><span data-stu-id="e2630-175">**Status Reason** - A summary of what happened in the provisioning event.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="e2630-176">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e2630-176">Troubleshooting</span></span>

<span data-ttu-id="e2630-177">佈建摘要報告和稽核記錄扮演了重要角色，可協助系統管理員針對各種使用者帳戶佈建問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="e2630-177">The provisioning summary report and audit logs play a key role helping admins troubleshoot various user account provisioning issues.</span></span>

<span data-ttu-id="e2630-178">如需透過案例來獲得如何針對自動使用者佈建進行疑難排解的指引，請參閱[為應用程式設定和佈建使用者時發生問題](active-directory-application-provisioning-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="e2630-178">For scenario-based guidance on how to troubleshoot automatic user provisioning, see [Problems configuring and provisioning users to an application](active-directory-application-provisioning-content-map.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e2630-179">其他資源</span><span class="sxs-lookup"><span data-stu-id="e2630-179">Additional Resources</span></span>

* [<span data-ttu-id="e2630-180">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="e2630-180">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="e2630-181">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e2630-181">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
