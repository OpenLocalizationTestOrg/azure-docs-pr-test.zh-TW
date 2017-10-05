---
title: "使用 WebJob 執行背景工作"
description: "了解如何在 Azure Web 應用程式中執行背景工作。"
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="57ea5-103">使用 WebJob 執行背景工作</span><span class="sxs-lookup"><span data-stu-id="57ea5-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="57ea5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="57ea5-104">Overview</span></span>
<span data-ttu-id="57ea5-105">您可以使用下列三種方式，在 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式的 WebJob 中執行程式或指令碼：依需求、連續或根據排程。</span><span class="sxs-lookup"><span data-stu-id="57ea5-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="57ea5-106">使用 WebJob 不會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="57ea5-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="57ea5-107">本文說明如何使用 [Azure 入口網站](https://portal.azure.com)來部署 WebJob。</span><span class="sxs-lookup"><span data-stu-id="57ea5-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="57ea5-108">如需如何使用 Visual Studio 或連續傳遞程序進行部署的相關資訊，請參閱 [如何將 Azure WebJob 部署至 Web 應用程式](websites-dotnet-deploy-webjobs.md)。</span><span class="sxs-lookup"><span data-stu-id="57ea5-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="57ea5-109">Azure WebJobs SDK 能簡化許多 WebJobs 程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="57ea5-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="57ea5-110">如需詳細資訊，請參閱 [什麼是 WebJobs SDK](websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="57ea5-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="57ea5-111">Azure Functions 提供另一種方式，從無伺服器環境或 App Service App 執行程式和指令碼。</span><span class="sxs-lookup"><span data-stu-id="57ea5-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="57ea5-112">如需詳細資訊，請參閱 [Azure Functions 概觀](../azure-functions/functions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="57ea5-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="57ea5-113"><a name="acceptablefiles"></a>指令碼或程式可接受的檔案類型</span><span class="sxs-lookup"><span data-stu-id="57ea5-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="57ea5-114">以下是可接受的檔案類型：</span><span class="sxs-lookup"><span data-stu-id="57ea5-114">The following file types are accepted:</span></span>

* <span data-ttu-id="57ea5-115">.cmd、.bat、.exe (使用 Windows 命令提示字元)</span><span class="sxs-lookup"><span data-stu-id="57ea5-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="57ea5-116">.ps1 (使用 PowerShell)</span><span class="sxs-lookup"><span data-stu-id="57ea5-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="57ea5-117">.sh (使用 Bash)</span><span class="sxs-lookup"><span data-stu-id="57ea5-117">.sh (using bash)</span></span>
* <span data-ttu-id="57ea5-118">.php (使用 PHP)</span><span class="sxs-lookup"><span data-stu-id="57ea5-118">.php (using php)</span></span>
* <span data-ttu-id="57ea5-119">.py (使用 Python)</span><span class="sxs-lookup"><span data-stu-id="57ea5-119">.py (using python)</span></span>
* <span data-ttu-id="57ea5-120">.js (使用 Node)</span><span class="sxs-lookup"><span data-stu-id="57ea5-120">.js (using node)</span></span>
* <span data-ttu-id="57ea5-121">.jar (使用 java)</span><span class="sxs-lookup"><span data-stu-id="57ea5-121">.jar (using java)</span></span>

## <span data-ttu-id="57ea5-122"><a name="CreateOnDemand"></a>在入口網站中建立依需求執行的 WebJob</span><span class="sxs-lookup"><span data-stu-id="57ea5-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="57ea5-123">在 [Azure 入口網站](https://portal.azure.com)的 [Web 應用程式] 刀鋒視窗中，按一下 [所有設定] > [WebJob] 以顯示 [WebJob] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="57ea5-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![WebJob 刀鋒視窗](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="57ea5-125">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="57ea5-125">Click **Add**.</span></span> <span data-ttu-id="57ea5-126">[新增 WebJob] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="57ea5-126">The **Add WebJob** dialog appears.</span></span>
   
    ![新增 WebJob 刀鋒視窗](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="57ea5-128">在 [ **名稱**] 下方提供 WebJob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="57ea5-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="57ea5-129">名稱的開頭必須是字母或數字，而且不能含有 "-" 和 "_" 之外的任何特殊字元。</span><span class="sxs-lookup"><span data-stu-id="57ea5-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="57ea5-130">在 [How to Run] 方塊中選擇 [Run on Demand]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="57ea5-131">在 [ **檔案上傳** ] 方塊中，按一下資料夾圖示，並瀏覽至包含您指令碼的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="57ea5-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="57ea5-132">該 zip 檔案應包含您的可執行檔 (.exe .cmd .bat .sh .php .py .js)，以及執行程式或指令碼所需的任何支援檔案。</span><span class="sxs-lookup"><span data-stu-id="57ea5-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="57ea5-133">選取 [ **建立** ]，將指令碼上傳至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ea5-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="57ea5-134">您為 WebJob 指定的名稱會出現在 [ **WebJob** ] 刀鋒視窗的清單中。</span><span class="sxs-lookup"><span data-stu-id="57ea5-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="57ea5-135">若要執行 WebJob，可在清單中使用滑鼠右鍵按一下它的名稱，然後按一下 [ **執行**]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![執行 WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="57ea5-137"><a name="CreateContinuous"></a>建立連續執行的 WebJob</span><span class="sxs-lookup"><span data-stu-id="57ea5-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="57ea5-138">若要建立連續執行的 WebJob，請依照建立執行一次之 WebJob 的相同步驟，但在 [如何執行] 方塊中選取 [連續]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="57ea5-139">若要開始或停止連續執行的 WebJob，可在清單中使用滑鼠右鍵按一下該 WebJob，然後按一下 [開始] 或 [停止]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="57ea5-140">如果您的 Web 應用程式會執行多個執行個體，則連續執行的 WebJob 將會在您的所有執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="57ea5-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="57ea5-141">依需求和排定的 WebJob 會在 Microsoft Azure 為負載平衡而選取的單一執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="57ea5-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="57ea5-142">若要讓連續 WebJobs 能夠在所有執行個體上可靠地執行，請對 Web 應用程式啟用 [永遠開啟] 組態設定，否則當 SCM 主機網站閒置太久時，其可能會停止執行。</span><span class="sxs-lookup"><span data-stu-id="57ea5-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="57ea5-143"><a name="CreateScheduledCRON"></a>使用 CRON 運算式建立排定的 WebJob</span><span class="sxs-lookup"><span data-stu-id="57ea5-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="57ea5-144">在基本、標準或高階模式中執行的 Web Apps 可使用這項技術，前提是 App 上的 [永遠開啟]  設定需啟用。</span><span class="sxs-lookup"><span data-stu-id="57ea5-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="57ea5-145">若要將依需求 WebJob 設成排定的 WebJob，只要在 WebJob zip 檔案的根目錄加入 `settings.job` 檔案。</span><span class="sxs-lookup"><span data-stu-id="57ea5-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="57ea5-146">此 JSON 檔案應該包含 `schedule` 屬性與 [CRON 運算式](https://en.wikipedia.org/wiki/Cron)，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="57ea5-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="57ea5-147">CRON 運算式由 6 個欄位組成: `{second} {minute} {hour} {day} {month} {day of the week}`。</span><span class="sxs-lookup"><span data-stu-id="57ea5-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="57ea5-148">例如，若要每隔 15 分鐘觸發 WebJob，您的 `settings.job` 必須有：</span><span class="sxs-lookup"><span data-stu-id="57ea5-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="57ea5-149">其他的 CRON 排程範例：</span><span class="sxs-lookup"><span data-stu-id="57ea5-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="57ea5-150">每隔一小時 (也就是每當分鐘的計數是 0)： `0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="57ea5-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="57ea5-151">上午 9 點到下午 5 點之間每隔一小時： `0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="57ea5-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="57ea5-152">每天上午 9:30： `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="57ea5-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="57ea5-153">每個工作日上午 9:30： `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="57ea5-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="57ea5-154">**注意**：從 Visual Studio 部署 WebJob 時，請務必將您的 `settings.job` 檔案屬性標示為 [有更新時才複製 ]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="57ea5-155"><a name="CreateScheduled"></a>使用 Azure 排程器建立排定的 WebJob</span><span class="sxs-lookup"><span data-stu-id="57ea5-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="57ea5-156">以下的替代技術會使用 Azure 排程器。</span><span class="sxs-lookup"><span data-stu-id="57ea5-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="57ea5-157">在此情況下，您的 WebJob 對排程一無所知。</span><span class="sxs-lookup"><span data-stu-id="57ea5-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="57ea5-158">反而是 Azure 排程器會被設定為依排程觸發 WebJob。</span><span class="sxs-lookup"><span data-stu-id="57ea5-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="57ea5-159">Azure 入口網站尚未具備建立排程 WebJob 的能力，但在加入該功能之前，您可以使用 [傳統入口網站](http://manage.windowsazure.com)來執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="57ea5-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="57ea5-160">在[傳統入口網站](http://manage.windowsazure.com)中，移至 WebJob 頁面，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="57ea5-161">在 [如何執行] 方塊中選擇 [依排程執行]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![新增排程工作][NewScheduledJob]
3. <span data-ttu-id="57ea5-163">選擇工作的 [Scheduler Region]  ，然後按一下對話方塊右下角的箭頭以前往下一個畫面。</span><span class="sxs-lookup"><span data-stu-id="57ea5-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="57ea5-164">在 [建立工作] 對話方塊中，選擇您想要的 [週期] 類型：[一次工作] 或 [週期性工作]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![排定週期][SchdRecurrence]
5. <span data-ttu-id="57ea5-166">同時選擇 [啟動] 時間：[現在] 或 [在特定時間]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![排定開始時間][SchdStart]
6. <span data-ttu-id="57ea5-168">如果您想要在特定時間開始，請在 [開始於] 下方選擇開始時間值。</span><span class="sxs-lookup"><span data-stu-id="57ea5-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![排定於特定時間開始][SchdStartOn]
7. <span data-ttu-id="57ea5-170">如果您選擇週期性工作，可以利用 [重複頻率] 選項來指定發生的頻率，以及利用 [結束於] 選項來指定結束時間。</span><span class="sxs-lookup"><span data-stu-id="57ea5-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![排定週期][SchdRecurEvery]
8. <span data-ttu-id="57ea5-172">如果您選擇 [週]，可以選擇 [On a Particular Schedule] 方塊指定工作執行的工作日。</span><span class="sxs-lookup"><span data-stu-id="57ea5-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![排定工作日][SchdWeeksOnParticular]
9. <span data-ttu-id="57ea5-174">如果您選擇 [月] 並選取 [On a Particular Schedule] 方塊，可以將工作設定為在每個月特定的 [日] 執行。</span><span class="sxs-lookup"><span data-stu-id="57ea5-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![排定每個月特定的日期][SchdMonthsOnPartDays]
10. <span data-ttu-id="57ea5-176">如果您選擇 [工作天] ，可以選擇要在哪一天或每個月的哪幾個工作天執行工作。</span><span class="sxs-lookup"><span data-stu-id="57ea5-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![排定每個月的特定工作天][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="57ea5-178">最後，您還可以使用 [發生次數] 選項，選擇讓工作在每個月哪一週 (第一、第二、第三等) 的指定工作日執行。</span><span class="sxs-lookup"><span data-stu-id="57ea5-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![排定每個月特定週的特定工作天][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="57ea5-180">在建立一或多個工作之後，這些工作的名稱會連同狀態、排程類型及其他資訊一併顯示在 [WebJobs ] 索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="57ea5-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="57ea5-181">系統會保留前 30 個 WebJob 的歷程記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="57ea5-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![工作清單][WebJobsListWithSeveralJobs]

### <span data-ttu-id="57ea5-183"><a name="Scheduler"></a>排程工作和 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="57ea5-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="57ea5-184">您可以在 [傳統入口網站](http://manage.windowsazure.com)的 Azure 排程器頁面中，進一步設定排程工作。</span><span class="sxs-lookup"><span data-stu-id="57ea5-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="57ea5-185">在 [WebJobs] 頁面中，按一下工作的 [排程]  連結以瀏覽至 Azure 排程器入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="57ea5-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![連結至 Azure 排程器][LinkToScheduler]
2. <span data-ttu-id="57ea5-187">在 [排程器] 頁面中按一下工作。</span><span class="sxs-lookup"><span data-stu-id="57ea5-187">On the Scheduler page, click the job.</span></span>
   
    ![[排程器] 入口網站頁面中的工作][SchedulerPortal]
3. <span data-ttu-id="57ea5-189">[工作動作]  頁面隨即開啟，您可以在其中進一步設定工作。</span><span class="sxs-lookup"><span data-stu-id="57ea5-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![工作動作 PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="57ea5-191"><a name="ViewJobHistory"></a>檢視工作歷程記錄</span><span class="sxs-lookup"><span data-stu-id="57ea5-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="57ea5-192">若要檢視工作的執行歷程記錄 (包括使用 WebJobs SDK 建立的工作)，請在 WebJob 刀鋒視窗的 [記錄] 資料欄下方按一下對應的連結。</span><span class="sxs-lookup"><span data-stu-id="57ea5-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="57ea5-193">(如果需要，您可以使用剪貼簿圖示將記錄檔頁面的 URL 複製到剪貼簿。)</span><span class="sxs-lookup"><span data-stu-id="57ea5-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![記錄連結](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="57ea5-195">按一下連結即可開啟 WebJob 的詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="57ea5-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="57ea5-196">此頁面能顯示執行之命令的名稱、上次執行時間及成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="57ea5-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="57ea5-197">按一下 [Recent job runs] 下的時間可查看進一步的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="57ea5-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="57ea5-199">[WebJob 執行詳細資料]  頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="57ea5-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="57ea5-200">按一下 [切換輸出]  可查看記錄的文字內容。</span><span class="sxs-lookup"><span data-stu-id="57ea5-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="57ea5-201">輸出記錄將會是文字格式。</span><span class="sxs-lookup"><span data-stu-id="57ea5-201">The output log is in text format.</span></span> 
   
    ![網站工作執行詳細資料][WebJobRunDetails]
4. <span data-ttu-id="57ea5-203">若要在個別的瀏覽器視窗中查看輸出文字，請按 [下載]  連結。</span><span class="sxs-lookup"><span data-stu-id="57ea5-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="57ea5-204">若要下載文字本身，請以滑鼠右鍵按一下連結，然後使用瀏覽器選項來儲存檔案內容。</span><span class="sxs-lookup"><span data-stu-id="57ea5-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![下載記錄輸出][DownloadLogOutput]
5. <span data-ttu-id="57ea5-206">頁面頂端的 [ **WebJob** ] 連結可讓您以便利的方法在歷程記錄儀表板中取得 WebJob 的清單。</span><span class="sxs-lookup"><span data-stu-id="57ea5-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![連結至 WebJobs 清單][WebJobsLinkToDashboardList]
   
    ![歷程記錄儀表板中的 WebJobs 清單][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="57ea5-209">按一下這些連結中的任一連結可帶您前往選取之工作的 [WebJob 詳細資料] 頁面。</span><span class="sxs-lookup"><span data-stu-id="57ea5-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="57ea5-210"><a name="WHPNotes"></a>注意</span><span class="sxs-lookup"><span data-stu-id="57ea5-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="57ea5-211">如果沒有對 scm (部署) 網站提出任何要求，則免費模式的 Web 應用程式可能會在 20 分鐘之後逾時，且 Web 應用程式在 Azure 中的入口網站也不會開啟。</span><span class="sxs-lookup"><span data-stu-id="57ea5-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="57ea5-212">對實際網站的要求將不會重設此項目。</span><span class="sxs-lookup"><span data-stu-id="57ea5-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="57ea5-213">連續工作的程式碼需經過撰寫，才能以無限迴圈的形式執行。</span><span class="sxs-lookup"><span data-stu-id="57ea5-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="57ea5-214">唯有當 Web 應用程式處於運作狀態時，連續工作才能連續執行。</span><span class="sxs-lookup"><span data-stu-id="57ea5-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="57ea5-215">[基本] 和 [標準] 模式能提供「永遠開啟」功能，此功能在啟用後能預防 Web 應用程式進入閒置狀態。</span><span class="sxs-lookup"><span data-stu-id="57ea5-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="57ea5-216">您僅可偵錯連續執行的 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="57ea5-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="57ea5-217">不支援偵錯排程或隨選的 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="57ea5-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="57ea5-218"><a name="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="57ea5-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="57ea5-219">如需詳細資訊，請參閱 [Azure WebJobs 建議資源][WebJobsRecommendedResources]。</span><span class="sxs-lookup"><span data-stu-id="57ea5-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

