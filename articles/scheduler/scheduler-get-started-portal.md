---
title: "開始在 Azure 入口網站中使用 Azure 排程器 | Microsoft Docs"
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
ms.openlocfilehash: 3861ee121ed1c4d086ea81640e84d924d7d17ea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="3d489-103">開始在 Azure 入口網站中使用 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="3d489-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="3d489-104">在 Azure 排程器中建立排程作業很簡單。</span><span class="sxs-lookup"><span data-stu-id="3d489-104">It's easy to create scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="3d489-105">在本教學課程中，您將了解如何建立作業。</span><span class="sxs-lookup"><span data-stu-id="3d489-105">In this tutorial, you'll learn how to create a job.</span></span> <span data-ttu-id="3d489-106">您也將學習排程器的監視和管理功能。</span><span class="sxs-lookup"><span data-stu-id="3d489-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="3d489-107">建立工作</span><span class="sxs-lookup"><span data-stu-id="3d489-107">Create a job</span></span>
1. <span data-ttu-id="3d489-108">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="3d489-108">Sign in to [Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="3d489-109">按一下 [+新增] > 在搜尋方塊中輸入*排程器* > 在結果中選取 [排程器] > 按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="3d489-109">Click **+New** > type *Scheduler* in the search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="3d489-110">讓我們使用 GET 要求建立只要點擊 http://www.microsoft.com/ 的工作。</span><span class="sxs-lookup"><span data-stu-id="3d489-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="3d489-111">在 [排程器作業]  畫面中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3d489-111">In the **Scheduler Job** screen, enter the following information:</span></span>
   
   1. <span data-ttu-id="3d489-112">**名稱：** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="3d489-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="3d489-113">**訂用帳戶：** 您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3d489-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="3d489-114">**作業集合：**選取現有的作業集合，或按一下 [建立新項目] > 輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="3d489-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="3d489-115">接下來，在 [動作設定] 中，定義下列值：</span><span class="sxs-lookup"><span data-stu-id="3d489-115">Next, in **Action Settings**, define the following values:</span></span>
   
   1. <span data-ttu-id="3d489-116">**動作類型：** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="3d489-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="3d489-117">**方法：** `GET`</span><span class="sxs-lookup"><span data-stu-id="3d489-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="3d489-118">**URL：** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="3d489-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="3d489-119">最後，讓我們定義排程。</span><span class="sxs-lookup"><span data-stu-id="3d489-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="3d489-120">作業可以定義為一次性的工作，但我們挑選週期性排程：</span><span class="sxs-lookup"><span data-stu-id="3d489-120">The job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="3d489-121">**週期**：`Recurring`</span><span class="sxs-lookup"><span data-stu-id="3d489-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="3d489-122">**開始**：今天的日期</span><span class="sxs-lookup"><span data-stu-id="3d489-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="3d489-123">**重複頻率**：`12 Hours`</span><span class="sxs-lookup"><span data-stu-id="3d489-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="3d489-124">**結束於**：今天日期的前兩天</span><span class="sxs-lookup"><span data-stu-id="3d489-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="3d489-125">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="3d489-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="3d489-126">管理和監視作業</span><span class="sxs-lookup"><span data-stu-id="3d489-126">Manage and monitor jobs</span></span>
<span data-ttu-id="3d489-127">建立作業之後，它會出現在主要 Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="3d489-127">Once a job is created, it appears in the main Azure dashboard.</span></span> <span data-ttu-id="3d489-128">按一下作業，即會開啟新視窗並顯示下列索引標籤：</span><span class="sxs-lookup"><span data-stu-id="3d489-128">Click the job and a new window opens with the following tabs:</span></span>

1. <span data-ttu-id="3d489-129">屬性</span><span class="sxs-lookup"><span data-stu-id="3d489-129">Properties</span></span>  
2. <span data-ttu-id="3d489-130">動作設定</span><span class="sxs-lookup"><span data-stu-id="3d489-130">Action Settings</span></span>  
3. <span data-ttu-id="3d489-131">排程</span><span class="sxs-lookup"><span data-stu-id="3d489-131">Schedule</span></span>  
4. <span data-ttu-id="3d489-132">歷程記錄</span><span class="sxs-lookup"><span data-stu-id="3d489-132">History</span></span>
5. <span data-ttu-id="3d489-133">使用者</span><span class="sxs-lookup"><span data-stu-id="3d489-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="3d489-134">屬性</span><span class="sxs-lookup"><span data-stu-id="3d489-134">Properties</span></span>
<span data-ttu-id="3d489-135">這些唯讀屬性說明排程器作業的管理中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3d489-135">These read-only properties describe the management metadata for the Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="3d489-136">動作設定</span><span class="sxs-lookup"><span data-stu-id="3d489-136">Action settings</span></span>
<span data-ttu-id="3d489-137">按一下 [作業]  畫面中的作業，可讓您設定該作業。</span><span class="sxs-lookup"><span data-stu-id="3d489-137">Clicking on a job in the **Jobs** screen allows you to configure that job.</span></span> <span data-ttu-id="3d489-138">如果您沒有在快速建立精靈中進行進階設定，這可讓您設定它們。</span><span class="sxs-lookup"><span data-stu-id="3d489-138">This lets you configure advanced settings, if you didn't configure them in the quick-create wizard.</span></span>

<span data-ttu-id="3d489-139">對於所有的動作類型，您可以變更重試原則和錯誤動作。</span><span class="sxs-lookup"><span data-stu-id="3d489-139">For all action types, you may change the retry policy and the error action.</span></span>

<span data-ttu-id="3d489-140">對於 HTTP 和 HTTPS 工作動作類型，您可能會將方法變更為任何允許的 HTTP 動詞。</span><span class="sxs-lookup"><span data-stu-id="3d489-140">For HTTP and HTTPS job action types, you may change the method to any allowed HTTP verb.</span></span> <span data-ttu-id="3d489-141">您也可以新增、刪除或變更標頭和基本驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="3d489-141">You may also add, delete, or change the headers and basic authentication information.</span></span>

<span data-ttu-id="3d489-142">對於儲存體佇列動作類型，您可能變更儲存體帳戶、佇列名稱、SAS 權杖和主體。</span><span class="sxs-lookup"><span data-stu-id="3d489-142">For storage queue action types, you may change the storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="3d489-143">對於服務匯流排動作類型，您可以變更命名空間、主題/佇列路徑、驗證設定、傳輸類型、訊息屬性和訊息本文。</span><span class="sxs-lookup"><span data-stu-id="3d489-143">For service bus action types, you may change the namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="3d489-144">排程</span><span class="sxs-lookup"><span data-stu-id="3d489-144">Schedule</span></span>
<span data-ttu-id="3d489-145">如果您想要變更您在快速建立精靈中建立的排程，這可讓您重新設定排程。</span><span class="sxs-lookup"><span data-stu-id="3d489-145">This lets you reconfigure the schedule, if you'd like to change the schedule you created in the quick-create wizard.</span></span>

<span data-ttu-id="3d489-146">這是 [在作業中建置複雜的排程和進階週期](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="3d489-146">This is an opportunity to build [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="3d489-147">您可以變更開始日期和時間、週期排程，以及結束日期和時間 (如果工作重複發生。)</span><span class="sxs-lookup"><span data-stu-id="3d489-147">You may change the start date and time, recurrence schedule, and the end date and time (if the job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="3d489-148">歷程記錄</span><span class="sxs-lookup"><span data-stu-id="3d489-148">History</span></span>
<span data-ttu-id="3d489-149">[歷程記錄]  索引標籤為選取的作業顯示系統中每次執行作業時選取的度量。</span><span class="sxs-lookup"><span data-stu-id="3d489-149">The **History** tab displays selected metrics for every job execution in the system for the selected job.</span></span> <span data-ttu-id="3d489-150">這些度量提供有關排程器健全狀況的即時值：</span><span class="sxs-lookup"><span data-stu-id="3d489-150">These metrics provide real-time values regarding the health of your Scheduler:</span></span>

1. <span data-ttu-id="3d489-151">狀態</span><span class="sxs-lookup"><span data-stu-id="3d489-151">Status</span></span>  
2. <span data-ttu-id="3d489-152">詳細資料</span><span class="sxs-lookup"><span data-stu-id="3d489-152">Details</span></span>  
3. <span data-ttu-id="3d489-153">重試次數</span><span class="sxs-lookup"><span data-stu-id="3d489-153">Retry attempts</span></span>
4. <span data-ttu-id="3d489-154">發生次數：第 1 次、第 2 次、第 3 次等。</span><span class="sxs-lookup"><span data-stu-id="3d489-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="3d489-155">執行開始時間</span><span class="sxs-lookup"><span data-stu-id="3d489-155">Start time of execution</span></span>  
6. <span data-ttu-id="3d489-156">執行結束時間</span><span class="sxs-lookup"><span data-stu-id="3d489-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="3d489-157">您可以按一下執行來檢視 [記錄詳細資料] ，包括每次執行的完整回應。</span><span class="sxs-lookup"><span data-stu-id="3d489-157">You can click on a run to view its **History Details**, including the whole response for every execution.</span></span> <span data-ttu-id="3d489-158">此對話方塊也可讓您將回應複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="3d489-158">This dialog box also allows you to copy the response to the clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="3d489-159">使用者</span><span class="sxs-lookup"><span data-stu-id="3d489-159">Users</span></span>
<span data-ttu-id="3d489-160">Azure 角色型存取控制 (RBAC) 可以對 Azure 排程器進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="3d489-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="3d489-161">若要了解如何使用 [使用者] 索引標籤，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="3d489-161">To learn how to use the Users tab, refer to [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="3d489-162">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3d489-162">See also</span></span>
 [<span data-ttu-id="3d489-163">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="3d489-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="3d489-164">排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="3d489-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="3d489-165">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="3d489-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="3d489-166">如何使用 Azure 排程器建立複雜的排程和進階週期</span><span class="sxs-lookup"><span data-stu-id="3d489-166">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="3d489-167">排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="3d489-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="3d489-168">排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="3d489-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="3d489-169">排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="3d489-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="3d489-170">排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="3d489-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="3d489-171">排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="3d489-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

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
