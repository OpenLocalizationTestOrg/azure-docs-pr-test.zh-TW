---
title: "aaaGet Azure 入口網站中開始使用 Azure 排程器 |Microsoft 文件"
description: "開始在 Azure 入口網站中使用 Azure 排程器"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="6a34f-103">開始在 Azure 入口網站中使用 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="6a34f-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="6a34f-104">它是 Azure 排程器中的簡單 toocreate 排程工作。</span><span class="sxs-lookup"><span data-stu-id="6a34f-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="6a34f-105">在此教學課程中，您將學習如何 toocreate 作業。</span><span class="sxs-lookup"><span data-stu-id="6a34f-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="6a34f-106">您也將學習排程器的監視和管理功能。</span><span class="sxs-lookup"><span data-stu-id="6a34f-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="6a34f-107">建立工作</span><span class="sxs-lookup"><span data-stu-id="6a34f-107">Create a job</span></span>
1. <span data-ttu-id="6a34f-108">登入太[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6a34f-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="6a34f-109">按一下**+ 新增**> 類型*排程器*hello [搜尋] 方塊中 > 選取**排程器**結果中 > 按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="6a34f-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="6a34f-110">讓我們使用 GET 要求建立只要點擊 http://www.microsoft.com/ 的工作。</span><span class="sxs-lookup"><span data-stu-id="6a34f-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="6a34f-111">在 hello**排程器工作**畫面上，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="6a34f-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="6a34f-112">**名稱：** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="6a34f-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="6a34f-113">**訂用帳戶：** 您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a34f-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="6a34f-114">**作業集合：**選取現有的作業集合，或按一下 [建立新項目] > 輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="6a34f-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="6a34f-115">接下來，在**動作設定**，定義 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="6a34f-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="6a34f-116">**動作類型：** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="6a34f-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="6a34f-117">**方法：** `GET`</span><span class="sxs-lookup"><span data-stu-id="6a34f-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="6a34f-118">**URL：** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="6a34f-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="6a34f-119">最後，讓我們定義排程。</span><span class="sxs-lookup"><span data-stu-id="6a34f-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="6a34f-120">hello 作業可定義為一次性工作，但我們挑選週期性排程：</span><span class="sxs-lookup"><span data-stu-id="6a34f-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="6a34f-121">**週期**：`Recurring`</span><span class="sxs-lookup"><span data-stu-id="6a34f-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="6a34f-122">**開始**：今天的日期</span><span class="sxs-lookup"><span data-stu-id="6a34f-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="6a34f-123">**重複頻率**：`12 Hours`</span><span class="sxs-lookup"><span data-stu-id="6a34f-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="6a34f-124">**結束於**：今天日期的前兩天</span><span class="sxs-lookup"><span data-stu-id="6a34f-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="6a34f-125">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="6a34f-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="6a34f-126">管理和監視作業</span><span class="sxs-lookup"><span data-stu-id="6a34f-126">Manage and monitor jobs</span></span>
<span data-ttu-id="6a34f-127">一旦建立工作時，它會出現在 hello 主要的 Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="6a34f-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="6a34f-128">按一下 hello 工作及新視窗隨即開啟並 hello 下列索引標籤：</span><span class="sxs-lookup"><span data-stu-id="6a34f-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="6a34f-129">屬性</span><span class="sxs-lookup"><span data-stu-id="6a34f-129">Properties</span></span>  
2. <span data-ttu-id="6a34f-130">動作設定</span><span class="sxs-lookup"><span data-stu-id="6a34f-130">Action Settings</span></span>  
3. <span data-ttu-id="6a34f-131">排程</span><span class="sxs-lookup"><span data-stu-id="6a34f-131">Schedule</span></span>  
4. <span data-ttu-id="6a34f-132">歷程記錄</span><span class="sxs-lookup"><span data-stu-id="6a34f-132">History</span></span>
5. <span data-ttu-id="6a34f-133">使用者</span><span class="sxs-lookup"><span data-stu-id="6a34f-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="6a34f-134">屬性</span><span class="sxs-lookup"><span data-stu-id="6a34f-134">Properties</span></span>
<span data-ttu-id="6a34f-135">唯讀屬性說明 hello 排程器工作的 hello 管理中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6a34f-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="6a34f-136">動作設定</span><span class="sxs-lookup"><span data-stu-id="6a34f-136">Action settings</span></span>
<span data-ttu-id="6a34f-137">按一下 上一 hello 的工作**作業**螢幕可讓您工作的 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="6a34f-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="6a34f-138">這可讓您設定進階的設定，如果您沒有 hello 中進行設定快速建立精靈。</span><span class="sxs-lookup"><span data-stu-id="6a34f-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="6a34f-139">對於所有的動作類型，您可以變更 hello 重試原則和 hello 錯誤動作。</span><span class="sxs-lookup"><span data-stu-id="6a34f-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="6a34f-140">對於 HTTP 和 HTTPS 工作動作類型，您可以變更 hello 方法 tooany 允許 HTTP 指令動詞。</span><span class="sxs-lookup"><span data-stu-id="6a34f-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="6a34f-141">您也可以新增、 刪除或變更 hello 標頭和基本驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="6a34f-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="6a34f-142">對於儲存體佇列動作類型，您可以變更 hello 儲存體帳戶、 佇列名稱、 SAS 權杖和主體。</span><span class="sxs-lookup"><span data-stu-id="6a34f-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="6a34f-143">服務匯流排動作類型，您可以變更 hello 命名空間、 主題/佇列路徑、 驗證設定、 傳輸類型、 訊息屬性和訊息內文。</span><span class="sxs-lookup"><span data-stu-id="6a34f-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="6a34f-144">排程</span><span class="sxs-lookup"><span data-stu-id="6a34f-144">Schedule</span></span>
<span data-ttu-id="6a34f-145">這可讓您重新設定 hello 排程，如果您想要建立 hello toochange hello 排程快速建立精靈。</span><span class="sxs-lookup"><span data-stu-id="6a34f-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="6a34f-146">這是有機會 toobuild[複雜的排程與您的工作中的進階循環](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="6a34f-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="6a34f-147">您可以變更 hello 開始日期和時間、 週期性排程和 hello 結束日期和時間 （如果 hello 週期性工作。）</span><span class="sxs-lookup"><span data-stu-id="6a34f-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="6a34f-148">歷程記錄</span><span class="sxs-lookup"><span data-stu-id="6a34f-148">History</span></span>
<span data-ttu-id="6a34f-149">hello**記錄**索引標籤會顯示 hello 選取作業的 hello 系統中的選定的度量的每項工作執行。</span><span class="sxs-lookup"><span data-stu-id="6a34f-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="6a34f-150">這些度量會提供有關您的排程器 hello 健全狀況的即時值：</span><span class="sxs-lookup"><span data-stu-id="6a34f-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="6a34f-151">狀態</span><span class="sxs-lookup"><span data-stu-id="6a34f-151">Status</span></span>  
2. <span data-ttu-id="6a34f-152">詳細資料</span><span class="sxs-lookup"><span data-stu-id="6a34f-152">Details</span></span>  
3. <span data-ttu-id="6a34f-153">重試次數</span><span class="sxs-lookup"><span data-stu-id="6a34f-153">Retry attempts</span></span>
4. <span data-ttu-id="6a34f-154">發生次數：第 1 次、第 2 次、第 3 次等。</span><span class="sxs-lookup"><span data-stu-id="6a34f-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="6a34f-155">執行開始時間</span><span class="sxs-lookup"><span data-stu-id="6a34f-155">Start time of execution</span></span>  
6. <span data-ttu-id="6a34f-156">執行結束時間</span><span class="sxs-lookup"><span data-stu-id="6a34f-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="6a34f-157">您可以按一下執行 tooview 其**詳細歷程記錄**，包括 hello 每個執行完整的回應。</span><span class="sxs-lookup"><span data-stu-id="6a34f-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="6a34f-158">此對話方塊也可讓您 toocopy hello 回應 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="6a34f-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="6a34f-159">使用者</span><span class="sxs-lookup"><span data-stu-id="6a34f-159">Users</span></span>
<span data-ttu-id="6a34f-160">Azure 角色型存取控制 (RBAC) 可以對 Azure 排程器進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="6a34f-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="6a34f-161">如何 toouse hello 使用者 索引標籤，請參閱太 toolearn[所有存取控制](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="6a34f-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="6a34f-162">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6a34f-162">See also</span></span>
 [<span data-ttu-id="6a34f-163">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="6a34f-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="6a34f-164">排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="6a34f-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="6a34f-165">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="6a34f-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="6a34f-166">排程 toobuild 複雜的方式與進階循環使用 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="6a34f-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="6a34f-167">排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="6a34f-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="6a34f-168">排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="6a34f-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="6a34f-169">排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="6a34f-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="6a34f-170">排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="6a34f-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="6a34f-171">排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="6a34f-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
