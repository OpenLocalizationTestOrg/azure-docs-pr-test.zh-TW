---
title: "Azure Active Directory 使用者自動帳戶佈建 tooSaaS 應用程式報告 |Microsoft 文件"
description: "了解如何 toocheck hello 狀態的使用者自動帳戶佈建工作，以及如何 tootroubleshoot hello 佈建之個別使用者。"
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
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a><span data-ttu-id="f52de-103">教學課程︰關於使用者帳戶自動佈建的報告</span><span class="sxs-lookup"><span data-stu-id="f52de-103">Tutorial: Reporting on automatic user account provisioning</span></span>


<span data-ttu-id="f52de-104">Azure Active Directory 包含[佈建服務的使用者帳戶](active-directory-saas-app-provisioning.md)可協助自動化 hello 佈建的 SaaS 應用程式和目的端對端的身分識別生命週期的 hello 的其他系統中的使用者帳戶解除佈建管理。</span><span class="sxs-lookup"><span data-stu-id="f52de-104">Azure Active Directory includes a [user account provisioning service](active-directory-saas-app-provisioning.md) that helps automate hello provisioning de-provisioning of user accounts in SaaS apps and other systems, for hello purpose of end-to-end identity lifecycle management.</span></span> <span data-ttu-id="f52de-105">Azure AD 支援預先整合的使用者佈建所有 hello 應用程式和系統的 hello 「 精選 」 一節中的 hello 連接器[Azure AD 應用程式庫](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)。</span><span class="sxs-lookup"><span data-stu-id="f52de-105">Azure AD supports pre-integrated user provisioning connectors for all of hello applications and systems in hello "Featured" section of hello [Azure AD application gallery](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).</span></span>

<span data-ttu-id="f52de-106">本文說明如何 toocheck hello 狀態的佈建作業之後他們已設定，以及如何 tootroubleshoot hello 佈建的個別使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="f52de-106">This article describes how toocheck hello status of provisioning jobs after they have been set up, and how tootroubleshoot hello provisioning of individual users and groups.</span></span>

## <a name="overview"></a><span data-ttu-id="f52de-107">概觀</span><span class="sxs-lookup"><span data-stu-id="f52de-107">Overview</span></span>

<span data-ttu-id="f52de-108">佈建的連接器是設定主要是使用和設定 hello [Azure 管理入口網站](https://portal.azure.com)，由下列 hello[提供文件](active-directory-saas-tutorial-list.md)hello 應用程式使用者帳戶佈建的位置所需。</span><span class="sxs-lookup"><span data-stu-id="f52de-108">Provisioning connectors are primarily set up and configured using hello [Azure management portal](https://portal.azure.com), by following hello [provided documentation](active-directory-saas-tutorial-list.md) for hello application where user account provisioning is desired.</span></span> <span data-ttu-id="f52de-109">應用程式的佈建作業在設定好並開始執行後，您就可以使用下列兩種方法之一來獲得這些作業的報告︰</span><span class="sxs-lookup"><span data-stu-id="f52de-109">Once configured and running, provisioning jobs for an application can be reported on using one of two methods:</span></span>

* <span data-ttu-id="f52de-110">**Azure 管理入口網站**-本文主要說明從 hello 擷取報表資訊[Azure 管理入口網站](https://portal.azure.com)，以提供同時佈建摘要報表，以及詳細的佈建稽核記錄檔中的特定應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52de-110">**Azure management portal** - This article primarily describes retrieving report information from hello [Azure management portal](https://portal.azure.com), which provides both a provisioning summary report as well as detailed provisioning audit logs for a given application.</span></span>

* <span data-ttu-id="f52de-111">**稽核 API** -Azure Active Directory 也提供 API 以程式設計方式擷取 hello 詳細佈建可讓稽核記錄檔稽核。</span><span class="sxs-lookup"><span data-stu-id="f52de-111">**Audit API** - Azure Active Directory also provides an Audit API that enables programmatic retrieval of hello detailed provisioning audit logs.</span></span> <span data-ttu-id="f52de-112">請參閱[Azure Active Directory 稽核應用程式開發介面參考](active-directory-reporting-api-audit-reference.md)的文件特定 toousing 這個 API。</span><span class="sxs-lookup"><span data-stu-id="f52de-112">See [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md) for documentation specific toousing this API.</span></span> <span data-ttu-id="f52de-113">雖然本文未特別涵蓋如何 toouse hello API，其詳細說明 hello 類型的佈建 hello 稽核記錄檔中記錄的事件。</span><span class="sxs-lookup"><span data-stu-id="f52de-113">While this article does not specifically cover how toouse hello API, it does detail hello types of provisioning events that are recorded in hello audit log.</span></span>

### <a name="definitions"></a><span data-ttu-id="f52de-114">定義</span><span class="sxs-lookup"><span data-stu-id="f52de-114">Definitions</span></span>

<span data-ttu-id="f52de-115">本文使用 hello 下列條款，定義如下：</span><span class="sxs-lookup"><span data-stu-id="f52de-115">This article uses hello following terms, defined below:</span></span>

* <span data-ttu-id="f52de-116">**來源系統**-hello 儲存機制的 hello Azure AD 佈建服務的使用者同步處理。</span><span class="sxs-lookup"><span data-stu-id="f52de-116">**Source System** - hello repository of users that hello Azure AD provisioning service synchronizes from.</span></span> <span data-ttu-id="f52de-117">Azure Active Directory 是 hello 大部分的 hello 來源系統預先整合 [佈建連接器，不過有一些例外狀況 (範例： Workday 輸入同步處理)。</span><span class="sxs-lookup"><span data-stu-id="f52de-117">Azure Active Directory is hello source system for hello majority of pre-integrated provisioning connectors, however there are some exceptions (example: Workday Inbound Synchronization).</span></span>

* <span data-ttu-id="f52de-118">**目標系統**-hello 儲存機制的 hello Azure AD 佈建服務的使用者同步處理與。</span><span class="sxs-lookup"><span data-stu-id="f52de-118">**Target System** - hello repository of users that hello Azure AD provisioning service synchronizes to.</span></span> <span data-ttu-id="f52de-119">這通常是 SaaS 應用程式 (範例： Salesforce、 ServiceNow、 Google Apps、 dropbox 企業版)，但在某些情況下可能會在內部部署系統，例如 Active Directory (範例： Workday 輸入同步處理 tooActive 目錄)。</span><span class="sxs-lookup"><span data-stu-id="f52de-119">This is typically a SaaS application (examples: Salesforce, ServiceNow, Google Apps, Dropbox for Business), but in some cases can be an on-premises system such as Active Directory (example: Workday Inbound Synchronization tooActive Directory).</span></span>


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a><span data-ttu-id="f52de-120">開始佈建 hello Azure 管理入口網站從報表</span><span class="sxs-lookup"><span data-stu-id="f52de-120">Getting provisioning reports from hello Azure management portal</span></span>

<span data-ttu-id="f52de-121">tooget 佈建報表資訊，為給定的應用程式，開始啟動 hello [Azure 管理入口網站](https://portal.azure.com)和瀏覽 toohello 企業應用程式的設定佈建。</span><span class="sxs-lookup"><span data-stu-id="f52de-121">tooget provisioning report information for a given application, start by launching hello [Azure management portal](https://portal.azure.com) and browsing toohello Enterprise Application for which provisioning is configured.</span></span> <span data-ttu-id="f52de-122">例如，如果您要佈建使用者 tooLinkedIn 提高權限，是 hello 導覽路徑 toohello 應用程式詳細資料：</span><span class="sxs-lookup"><span data-stu-id="f52de-122">For example, if you are provisioning users tooLinkedIn Elevate, hello navigation path toohello application details is:</span></span>

<span data-ttu-id="f52de-123">**Azure Active Directory > 企業應用程式 > 所有應用程式 > LinkedIn Elevate**</span><span class="sxs-lookup"><span data-stu-id="f52de-123">**Azure Active Directory > Enterprise Applications > All applications > LinkedIn Elevate**</span></span>

<span data-ttu-id="f52de-124">從這裡，您可以存取 hello 佈建摘要報表和 hello 佈建的稽核記錄，同時如下所述。</span><span class="sxs-lookup"><span data-stu-id="f52de-124">From here, you can access both hello Provisioning summary report, and hello provisioning audit logs, both described below.</span></span>


### <a name="provisioning-summary-report"></a><span data-ttu-id="f52de-125">佈建摘要報告</span><span class="sxs-lookup"><span data-stu-id="f52de-125">Provisioning summary report</span></span>

<span data-ttu-id="f52de-126">hello 佈建摘要報表會顯示在 [hello**佈建**索引標籤上指定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52de-126">hello provisioning summary report is visible in hello **Provisioning** tab for given application.</span></span> <span data-ttu-id="f52de-127">位於 hello 同步處理詳細資料] 區段下方**設定**，並提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="f52de-127">It is located in hello Synchronization Details section underneath **Settings**, and provides hello following information:</span></span>

* <span data-ttu-id="f52de-128">hello 總數的使用者和群組的已同步處理，並目前正在進行佈建 hello 來源系統與 hello 目標系統之間的範圍中。</span><span class="sxs-lookup"><span data-stu-id="f52de-128">hello total number of users and/groups that have been synchronized and are currently in scope for provisioning between hello source system and hello target system.</span></span>

* <span data-ttu-id="f52de-129">已執行 hello 上次 hello 同步處理。</span><span class="sxs-lookup"><span data-stu-id="f52de-129">hello last time hello synchronization was run.</span></span> <span data-ttu-id="f52de-130">在完成完整的同步處理之後，系統通常每隔 20 到 40 分鐘就會進行一次同步處理。</span><span class="sxs-lookup"><span data-stu-id="f52de-130">Synchronizations typically occur every 20-40 minutes, after a full synchronization has completed.</span></span>

* <span data-ttu-id="f52de-131">是否已完成初次的完整同步處理。</span><span class="sxs-lookup"><span data-stu-id="f52de-131">Whether or not an initial full synchronization has been completed.</span></span>

* <span data-ttu-id="f52de-132">已佈建程序的 hello 放置於隔離，以及哪些 hello hello 隔離狀態是例如 (因為 tooinvalid 系統管理員認證的目標系統的失敗 toocommunicate)</span><span class="sxs-lookup"><span data-stu-id="f52de-132">Whether or not hello provisioning process has been placed in quarantine, and what hello reason for hello quarantine status is (e.g. failure toocommunicate with target system due tooinvalid admin credentials)</span></span>

<span data-ttu-id="f52de-133">hello 佈建摘要報表應該 hello 第一個位置 admins 外觀 toocheck hello hello 佈建作業的操作健全狀況。</span><span class="sxs-lookup"><span data-stu-id="f52de-133">hello provisioning summary report should be hello first place admins look toocheck on hello operational health of hello provisioning job.</span></span>

 ![摘要報告](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a><span data-ttu-id="f52de-135">佈建稽核記錄</span><span class="sxs-lookup"><span data-stu-id="f52de-135">Provisioning audit logs</span></span>
<span data-ttu-id="f52de-136">Hello 佈建服務所執行的所有活動都會都記錄在 hello Azure AD 稽核記錄，就可以在 hello 檢視**稽核記錄檔**] 索引標籤下 hello**帳戶佈建**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="f52de-136">All activities performed by hello provisioning service are recorded in hello Azure AD audit logs, which can be viewed in hello **Audit logs** tab under hello **Account Provisioning** category.</span></span> <span data-ttu-id="f52de-137">所記錄的活動事件類型包括︰</span><span class="sxs-lookup"><span data-stu-id="f52de-137">Logged activity event types include:</span></span>

* <span data-ttu-id="f52de-138">**匯入事件**-「 匯入 」 事件會記錄每次 hello Azure AD 佈建服務擷取個別使用者或群組的相關資訊的來源系統或目標系統。</span><span class="sxs-lookup"><span data-stu-id="f52de-138">**Import events** - An "import" event is recorded each time hello Azure AD provisioning service retrieves information about an individual user or group from a source system or target system.</span></span> <span data-ttu-id="f52de-139">同步處理期間，使用者會從擷取 hello 來源系統首先，使用 hello 結果記錄為 「 匯入 」 事件。</span><span class="sxs-lookup"><span data-stu-id="f52de-139">During synchronization, users are retrieved from hello source system first, with hello results recorded as "import" events.</span></span> <span data-ttu-id="f52de-140">如果它們存在 hello 結果也會記錄為 「 匯入 」 事件具有相符識別碼的 hello 擷取使用者然後會針對 hello 目標系統 toocheck 查詢 hello。</span><span class="sxs-lookup"><span data-stu-id="f52de-140">hello matching IDs of hello retrieved users are then queried against hello target system toocheck if they exist, with hello results also recorded as "import" events.</span></span> <span data-ttu-id="f52de-141">這些事件會記錄所有對應的使用者屬性以及它們在 hello 事件時間的 hello hello Azure AD 佈建服務所看到的值。</span><span class="sxs-lookup"><span data-stu-id="f52de-141">These events record all mapped user attributes and their values that were seen by hello Azure AD provisioning service at hello time of hello event.</span></span> 

* <span data-ttu-id="f52de-142">**同步處理規則事件**-這些事件報告的 hello 屬性對應規則的 hello 結果和任何設定範圍的篩選器之後使用者資料已匯入和評估 hello 來源與目標系統。</span><span class="sxs-lookup"><span data-stu-id="f52de-142">**Synchronization rule events** - These events report on hello results of hello attribute mapping rules and any configured scoping filters, after user data has been imported and evaluated from hello source and target systems.</span></span> <span data-ttu-id="f52de-143">例如，如果來源系統中的使用者會被視為在範圍內的佈建，toobe 視為 toonot 存在於 hello 目標系統，然後 hello 使用者此事件記錄將會佈建 hello 目標系統中。</span><span class="sxs-lookup"><span data-stu-id="f52de-143">For example, if a user in a source system is deemed toobe in scope for provisioning, and deemed toonot exist in hello target system, then this event records that hello user will be provisioned in hello target system.</span></span> 

* <span data-ttu-id="f52de-144">**匯出事件**-「 匯出 」 事件會記錄每次 hello Azure AD 佈建服務會將使用者帳戶或群組物件 tooa 目標系統。</span><span class="sxs-lookup"><span data-stu-id="f52de-144">**Export events** - An "export" event is recorded each time hello Azure AD provisioning service writes a user account or group object tooa target system.</span></span> <span data-ttu-id="f52de-145">這些事件會記錄所有的使用者屬性與值撰寫 hello Azure AD 佈建服務的 hello 事件 hello 次。</span><span class="sxs-lookup"><span data-stu-id="f52de-145">These events record all user attributes and their values that were written by hello Azure AD provisioning service at hello time of hello event.</span></span> <span data-ttu-id="f52de-146">如果寫入 hello 使用者帳戶或群組物件 toohello 目標系統時發生錯誤，它將會顯示於此。</span><span class="sxs-lookup"><span data-stu-id="f52de-146">If there was an error while writing hello user account or group object toohello target system, it will be displayed here.</span></span>

* <span data-ttu-id="f52de-147">**處理委付事件**-escrows 程序時，會發生 hello 佈建服務發生失敗時嘗試的作業，並開始 tooretry hello 作業，以輪詢間隔的時間。</span><span class="sxs-lookup"><span data-stu-id="f52de-147">**Process escrow events** - Process escrows occur when hello provisioning service encounters a failure while attempting an operation, and begins tooretry hello operation on a back-off interval of time.</span></span> <span data-ttu-id="f52de-148">每當服務淘汰佈建作業時，就會記錄下「委付」事件。</span><span class="sxs-lookup"><span data-stu-id="f52de-148">An "escrow" event is recorded each time a provisioning operation was retired.</span></span>

<span data-ttu-id="f52de-149">查看個別的使用者佈建事件，當 hello 事件通常會發生順序如下：</span><span class="sxs-lookup"><span data-stu-id="f52de-149">When looking at provisioning events for an individual user, hello events normally occur in this order:</span></span>

1. <span data-ttu-id="f52de-150">匯入事件： 從 hello 來源系統擷取使用者。</span><span class="sxs-lookup"><span data-stu-id="f52de-150">Import event: User is retrieved from hello source system.</span></span>

2. <span data-ttu-id="f52de-151">匯入事件： 目標系統是查詢的 toocheck hello hello 擷取使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="f52de-151">Import event: Target system is queried toocheck for hello existence of hello retrieved user.</span></span>

3. <span data-ttu-id="f52de-152">同步處理規則的事件： 來源和目標系統中的使用者資料進行評估 hello 設定屬性對應規則及範圍設定篩選 toodetermine 什麼動作，如果有的話，應該執行。</span><span class="sxs-lookup"><span data-stu-id="f52de-152">Synchronization rule event: User data from source and target systems are evaluated against hello configured attribute mapping rules and scoping filters toodetermine what action, if any, should be performed.</span></span>

4. <span data-ttu-id="f52de-153">匯出事件： hello 同步處理規則的事件可讓您指定動作應該是如果 hello hello 動作結果會記錄在匯出事件，然後執行 （例如加入、 更新、 刪除）。</span><span class="sxs-lookup"><span data-stu-id="f52de-153">Export event: If hello synchronization rule event dictated that an action should be performed (e.g. Add, Update, Delete), then hello results of hello action are recorded in an Export event.</span></span>

![建立 Azure AD 測試使用者](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a><span data-ttu-id="f52de-155">查閱特定使用者的佈建事件</span><span class="sxs-lookup"><span data-stu-id="f52de-155">Looking up provisioning events for a specific user</span></span>

<span data-ttu-id="f52de-156">hello hello 佈建稽核記錄檔的最常見使用案例是 toocheck hello 佈建個別使用者帳戶的狀態。</span><span class="sxs-lookup"><span data-stu-id="f52de-156">hello most common use case for hello provisioning audit logs is toocheck hello provisioning status of an individual user account.</span></span> <span data-ttu-id="f52de-157">toolook hello 最後一個佈建的事件特定使用者：</span><span class="sxs-lookup"><span data-stu-id="f52de-157">toolook up hello last provisioning events for a specific user:</span></span>

1. <span data-ttu-id="f52de-158">移 toohello**稽核記錄檔**> 一節。</span><span class="sxs-lookup"><span data-stu-id="f52de-158">Go toohello **Audit logs** section.</span></span>

2. <span data-ttu-id="f52de-159">從 hello**類別**功能表上，選取**帳戶佈建**。</span><span class="sxs-lookup"><span data-stu-id="f52de-159">From hello **Category** menu, select **Account Provisioning**.</span></span>

3. <span data-ttu-id="f52de-160">在 [hello**日期範圍**功能表中，您想要 toosearch，選取 hello 日期範圍</span><span class="sxs-lookup"><span data-stu-id="f52de-160">In hello **Date Range** menu, select hello date range you want toosearch,</span></span>

4. <span data-ttu-id="f52de-161">在 [hello**搜尋**列上，輸入您想針對 toosearch hello 使用者 hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="f52de-161">In hello **Search** bar, enter hello user ID of hello user you wish toosearch for.</span></span> <span data-ttu-id="f52de-162">hello 的識別碼值的格式應該符合您選取的項目為 hello hello 屬性對應設定 （例如 userPrincipalName 或員工 ID 編號） 中的主要符合 ID。</span><span class="sxs-lookup"><span data-stu-id="f52de-162">hello format of ID value should match whatever you selected as hello primary matching ID in hello attribute mapping configuration (e.g. userPrincipalName or employee ID number).</span></span> <span data-ttu-id="f52de-163">所需的 hello ID 值會顯示 hello 目標資料行中。</span><span class="sxs-lookup"><span data-stu-id="f52de-163">hello ID value required will be visible in hello Target(s) column.</span></span>

5. <span data-ttu-id="f52de-164">按下 Enter toosearch。</span><span class="sxs-lookup"><span data-stu-id="f52de-164">Press Enter toosearch.</span></span> <span data-ttu-id="f52de-165">會先傳回最新的佈建事件 hello。</span><span class="sxs-lookup"><span data-stu-id="f52de-165">hello most recent provisioning events will be returned first.</span></span>

6. <span data-ttu-id="f52de-166">如果傳回的事件，請注意 hello 活動型別和是否成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="f52de-166">If events are returned, note hello activity types and whether they succeeded or failed.</span></span> <span data-ttu-id="f52de-167">如果不傳回任何結果，則表示 hello 使用者不存在，或尚未偵測到的 hello 佈建程序，如果完整的同步處理尚未完成。</span><span class="sxs-lookup"><span data-stu-id="f52de-167">If no results are returned, then it means hello user either does not exist, or has not yet been detected by hello provisioning process if a full sync has not yet completed.</span></span>

7. <span data-ttu-id="f52de-168">按一下個別事件 tooview 擴充詳細資料，包括所有的使用者內容已擷取、 評估，或撰寫為 hello 事件的一部分。</span><span class="sxs-lookup"><span data-stu-id="f52de-168">Click on individual events tooview extended details, including all user properties that were retrieved, evaluated, or written as part of hello event.</span></span>


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a><span data-ttu-id="f52de-169">檢視佈建稽核記錄檔的 hello 的秘訣</span><span class="sxs-lookup"><span data-stu-id="f52de-169">Tips for viewing hello provisioning audit logs</span></span>

<span data-ttu-id="f52de-170">Hello Azure 入口網站中的最佳可讀性，選取 [hello**資料行**按鈕，並選擇這些資料行：</span><span class="sxs-lookup"><span data-stu-id="f52de-170">For best readability in hello Azure portal, select hello **Columns** button and choose these columns:</span></span>

* <span data-ttu-id="f52de-171">**日期**-顯示 hello 日期 hello 事件發生的情況。</span><span class="sxs-lookup"><span data-stu-id="f52de-171">**Date** - Shows hello date hello event occurred.</span></span>
* <span data-ttu-id="f52de-172">**目標**-顯示 hello 應用程式名稱和使用者識別碼的 hello 主旨 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="f52de-172">**Target(s)** - Shows hello app name and user ID that are hello subjects of hello event.</span></span>
* <span data-ttu-id="f52de-173">**活動**-hello 活動型別，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="f52de-173">**Activity** - hello activity type, as described previously.</span></span>
* <span data-ttu-id="f52de-174">**狀態**-是否 hello 事件成功與否。</span><span class="sxs-lookup"><span data-stu-id="f52de-174">**Status** - Whether hello event succeeded or not.</span></span>
* <span data-ttu-id="f52de-175">**狀態原因**-hello 佈建事件中發生什麼情況的摘要。</span><span class="sxs-lookup"><span data-stu-id="f52de-175">**Status Reason** - A summary of what happened in hello provisioning event.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="f52de-176">疑難排解</span><span class="sxs-lookup"><span data-stu-id="f52de-176">Troubleshooting</span></span>

<span data-ttu-id="f52de-177">佈建摘要的報表和稽核記錄檔的 hello 扮演重要的角色，協助疑難排解各種不同的使用者帳戶佈建問題的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="f52de-177">hello provisioning summary report and audit logs play a key role helping admins troubleshoot various user account provisioning issues.</span></span>

<span data-ttu-id="f52de-178">如需如何以案例為基礎指引 tootroubleshoot 自動使用者佈建，請參閱[設定和佈建使用者 tooan 應用程式的問題](active-directory-application-provisioning-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="f52de-178">For scenario-based guidance on how tootroubleshoot automatic user provisioning, see [Problems configuring and provisioning users tooan application](active-directory-application-provisioning-content-map.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f52de-179">其他資源</span><span class="sxs-lookup"><span data-stu-id="f52de-179">Additional Resources</span></span>

* [<span data-ttu-id="f52de-180">管理企業應用程式的使用者帳戶佈建</span><span class="sxs-lookup"><span data-stu-id="f52de-180">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="f52de-181">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f52de-181">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
