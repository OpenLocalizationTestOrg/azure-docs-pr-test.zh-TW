---
title: "以 WebJobs aaaRun 背景工作"
description: "了解如何在 Azure 中的 toorun 背景工作 web 應用程式。"
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
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="47bca-103">使用 WebJob 執行背景工作</span><span class="sxs-lookup"><span data-stu-id="47bca-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="47bca-104">概觀</span><span class="sxs-lookup"><span data-stu-id="47bca-104">Overview</span></span>
<span data-ttu-id="47bca-105">您可以使用下列三種方式，在 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式的 WebJob 中執行程式或指令碼：依需求、連續或根據排程。</span><span class="sxs-lookup"><span data-stu-id="47bca-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="47bca-106">沒有任何額外的成本 toouse WebJobs。</span><span class="sxs-lookup"><span data-stu-id="47bca-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="47bca-107">本文將說明如何使用 toodeploy WebJobs hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="47bca-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="47bca-108">如需有關資訊 toodeploy 使用 Visual Studio 或持續傳遞程序，請參閱[如何 tooDeploy 應用程式的 Azure WebJobs tooWeb](websites-dotnet-deploy-webjobs.md)。</span><span class="sxs-lookup"><span data-stu-id="47bca-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="47bca-109">hello Azure WebJobs SDK 簡化了許多 WebJobs 的程式設計工作。</span><span class="sxs-lookup"><span data-stu-id="47bca-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="47bca-110">如需詳細資訊，請參閱[何謂 hello WebJobs SDK](websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="47bca-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="47bca-111">Azure 的函式提供另一個方式 toorun 程式和指令碼從無伺服器環境，或從應用程式服務的應用程式。</span><span class="sxs-lookup"><span data-stu-id="47bca-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="47bca-112">如需詳細資訊，請參閱 [Azure Functions 概觀](../azure-functions/functions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="47bca-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="47bca-113"><a name="acceptablefiles"></a>指令碼或程式可接受的檔案類型</span><span class="sxs-lookup"><span data-stu-id="47bca-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="47bca-114">接受下列檔案類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="47bca-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="47bca-115">.cmd、.bat、.exe (使用 Windows 命令提示字元)</span><span class="sxs-lookup"><span data-stu-id="47bca-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="47bca-116">.ps1 (使用 PowerShell)</span><span class="sxs-lookup"><span data-stu-id="47bca-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="47bca-117">.sh (使用 Bash)</span><span class="sxs-lookup"><span data-stu-id="47bca-117">.sh (using bash)</span></span>
* <span data-ttu-id="47bca-118">.php (使用 PHP)</span><span class="sxs-lookup"><span data-stu-id="47bca-118">.php (using php)</span></span>
* <span data-ttu-id="47bca-119">.py (使用 Python)</span><span class="sxs-lookup"><span data-stu-id="47bca-119">.py (using python)</span></span>
* <span data-ttu-id="47bca-120">.js (使用 Node)</span><span class="sxs-lookup"><span data-stu-id="47bca-120">.js (using node)</span></span>
* <span data-ttu-id="47bca-121">.jar (使用 java)</span><span class="sxs-lookup"><span data-stu-id="47bca-121">.jar (using java)</span></span>

## <span data-ttu-id="47bca-122"><a name="CreateOnDemand"></a>在 hello 入口網站中建立視 WebJob</span><span class="sxs-lookup"><span data-stu-id="47bca-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="47bca-123">在 hello **Web 應用程式**刀鋒視窗中的 hello [Azure 入口網站](https://portal.azure.com)，按一下 **所有設定 > WebJobs** tooshow hello **WebJobs**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="47bca-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![WebJob 刀鋒視窗](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="47bca-125">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="47bca-125">Click **Add**.</span></span> <span data-ttu-id="47bca-126">hello**新增 WebJob**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="47bca-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![新增 WebJob 刀鋒視窗](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="47bca-128">在下**名稱**，提供 hello WebJob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="47bca-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="47bca-129">hello 名稱必須以字母或數字開頭，且不得包含任何特殊字元不是"-"與"_"。</span><span class="sxs-lookup"><span data-stu-id="47bca-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="47bca-130">在 hello**如何 tooRun**方塊中，選擇**視需要執行**。</span><span class="sxs-lookup"><span data-stu-id="47bca-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="47bca-131">在 hello**檔案上傳**，按一下 hello 資料夾圖示，然後瀏覽 toohello zip 檔案包含您指令碼。</span><span class="sxs-lookup"><span data-stu-id="47bca-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="47bca-132">hello zip 檔案應包含可執行檔 (.exe.cmd.bat.sh.php.py.js) 以及任何支援的檔案需要 toorun hello 程式或指令碼。</span><span class="sxs-lookup"><span data-stu-id="47bca-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="47bca-133">請檢查**建立**tooupload hello 指令碼 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="47bca-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="47bca-134">hello hello WebJob 所指定的名稱會出現在 hello 清單上 hello **WebJobs**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="47bca-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="47bca-135">toorun hello WebJob，請以滑鼠右鍵按一下在 hello 清單，然後按一下其名稱**執行**。</span><span class="sxs-lookup"><span data-stu-id="47bca-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![執行 WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="47bca-137"><a name="CreateContinuous"></a>建立連續執行的 WebJob</span><span class="sxs-lookup"><span data-stu-id="47bca-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="47bca-138">toocreate 持續執行的 WebJob，請遵循相同步驟為建立 WebJob 可執行一次，但在 hello hello**如何 tooRun**方塊中，選擇**連續**。</span><span class="sxs-lookup"><span data-stu-id="47bca-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="47bca-139">toostart 或停止連續的 WebJob 上按一下滑鼠右鍵在 hello 清單，然後按一下 hello WebJob**啟動**或**停止**。</span><span class="sxs-lookup"><span data-stu-id="47bca-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="47bca-140">如果您的 Web 應用程式會執行多個執行個體，則連續執行的 WebJob 將會在您的所有執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="47bca-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="47bca-141">依需求和排定的 WebJob 會在 Microsoft Azure 為負載平衡而選取的單一執行個體上執行。</span><span class="sxs-lookup"><span data-stu-id="47bca-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="47bca-142">持續的 Webjob toorun 可靠地及所有的執行個體上啟用 Alwayson 的 hello * hello web 應用程式則可以讓它們停止執行 hello SCM 主機站台已經閒置的時間太長的組態設定。</span><span class="sxs-lookup"><span data-stu-id="47bca-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="47bca-143"><a name="CreateScheduledCRON"></a>使用 CRON 運算式建立排定的 WebJob</span><span class="sxs-lookup"><span data-stu-id="47bca-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="47bca-144">這項技術就是可用 tooWeb 應用程式在基本、 標準或進階模式下執行，而且需要 hello **Always On**設定 toobe hello 應用程式上啟用。</span><span class="sxs-lookup"><span data-stu-id="47bca-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="47bca-145">只需要包含 tooturn 上要求 WebJob 排程的 WebJob，到`settings.job`WebJob zip 檔案的 hello 根目錄的檔案。</span><span class="sxs-lookup"><span data-stu-id="47bca-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="47bca-146">此 JSON 檔案應該包含 `schedule` 屬性與 [CRON 運算式](https://en.wikipedia.org/wiki/Cron)，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="47bca-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="47bca-147">hello CRON 運算式由 6 個欄位所組成： `{second} {minute} {hour} {day} {month} {day of hello week}`。</span><span class="sxs-lookup"><span data-stu-id="47bca-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="47bca-148">例如，tootrigger 您 WebJob 每隔 15 分鐘、 您`settings.job`必須：</span><span class="sxs-lookup"><span data-stu-id="47bca-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="47bca-149">其他的 CRON 排程範例：</span><span class="sxs-lookup"><span data-stu-id="47bca-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="47bca-150">每個小時 （也就是每當分鐘 hello 計數為 0）：`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="47bca-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="47bca-151">每個小時，從上午 9 點 too5 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="47bca-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="47bca-152">每天上午 9:30： `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="47bca-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="47bca-153">每個工作日上午 9:30： `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="47bca-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="47bca-154">**請注意**： 部署時，從 Visual Studio 的 WebJob，請確定 toomark 您`settings.job`檔案做為 '複本有更新時才' 屬性。</span><span class="sxs-lookup"><span data-stu-id="47bca-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="47bca-155"><a name="CreateScheduled"></a>建立使用 hello Azure 排程器的 WebJob 排程</span><span class="sxs-lookup"><span data-stu-id="47bca-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="47bca-156">hello 下列替代技巧使用 hello Azure 排程器。</span><span class="sxs-lookup"><span data-stu-id="47bca-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="47bca-157">在此情況下，您的 web 工作沒有 hello 排程的任何直接知識。</span><span class="sxs-lookup"><span data-stu-id="47bca-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="47bca-158">相反地，hello Azure 排程器會取得設定的 tootrigger 您 WebJob 上排程。</span><span class="sxs-lookup"><span data-stu-id="47bca-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="47bca-159">hello Azure 入口網站還沒有 hello 能力 toocreate 排程的 WebJob，但是在新增該功能之前可以執行使用 hello[傳統入口網站](http://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="47bca-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="47bca-160">在 hello[傳統入口網站](http://manage.windowsazure.com)移 toohello WebJob 頁面，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="47bca-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="47bca-161">在 hello**如何 tooRun**方塊中，選擇**依排程執行**。</span><span class="sxs-lookup"><span data-stu-id="47bca-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![新增排程工作][NewScheduledJob]
3. <span data-ttu-id="47bca-163">選擇 hello**排程器區域**適用於您的作業，然後按一下hello hello 右下方的 hello 對話方塊 tooproceed toohello 下一個畫面上的箭號。</span><span class="sxs-lookup"><span data-stu-id="47bca-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="47bca-164">在 hello**建立作業** 對話方塊中，選擇 hello 類型**循環**想：**一次性的工作**或**週期性工作**。</span><span class="sxs-lookup"><span data-stu-id="47bca-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![排定週期][SchdRecurrence]
5. <span data-ttu-id="47bca-166">同時選擇 [啟動] 時間：[現在] 或 [在特定時間]。</span><span class="sxs-lookup"><span data-stu-id="47bca-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![排定開始時間][SchdStart]
6. <span data-ttu-id="47bca-168">如果您想在特定時間的 toostart，選擇 在您開始的時間值**啟動上**。</span><span class="sxs-lookup"><span data-stu-id="47bca-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![排定於特定時間開始][SchdStartOn]
7. <span data-ttu-id="47bca-170">如果您選擇週期性工作，您有 hello **Recur 每**選項 toospecify hello 頻率的發生次數與 hello**結束上**選項 toospecify 結束的時間。</span><span class="sxs-lookup"><span data-stu-id="47bca-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![排定週期][SchdRecurEvery]
8. <span data-ttu-id="47bca-172">如果您選擇**週**，您可以選取 hello**上特定排程**方塊並指定 hello 星期幾 hello 想 hello 作業 toorun。</span><span class="sxs-lookup"><span data-stu-id="47bca-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![排程 hello 一週天數等][SchdWeeksOnParticular]
9. <span data-ttu-id="47bca-174">如果您選擇**月**和選取 hello**上特定排程** 方塊中，您可以設定 hello 作業 toorun 特定編號**天**hello 月份。</span><span class="sxs-lookup"><span data-stu-id="47bca-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![排程 hello 月份中特定日期][SchdMonthsOnPartDays]
10. <span data-ttu-id="47bca-176">如果您選擇**星期幾**，您可以選取一天或 hello 一周天數中您想要在 hello 作業 toorun 的 hello 月份。</span><span class="sxs-lookup"><span data-stu-id="47bca-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![排定每個月的特定工作天][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="47bca-178">最後，您也可以使用 hello**出現**選項 toochoose hello 月份中的哪一週 (第一次，第二個、 第三個等) 想 hello 作業 toorun hello 上的您所指定的星期幾。</span><span class="sxs-lookup"><span data-stu-id="47bca-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![排定每個月特定週的特定工作天][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="47bca-180">建立一或多個工作之後，其名稱會出現其狀態、 排程類型與其他資訊的 hello WebJobs 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="47bca-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="47bca-181">歷程記錄資訊會保留的 hello 上次 30 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="47bca-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![工作清單][WebJobsListWithSeveralJobs]

### <span data-ttu-id="47bca-183"><a name="Scheduler"></a>排程工作和 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="47bca-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="47bca-184">排程的工作可以進一步設定中的 hello hello Azure 排程器頁面[傳統入口網站](http://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="47bca-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="47bca-185">在 hello WebJobs 頁面上，按一下 hello 作業**排程**連結 toonavigate toohello Azure 排程器入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="47bca-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![連結 tooAzure 排程器][LinkToScheduler]
2. <span data-ttu-id="47bca-187">在 hello 排程器 頁面上，按一下 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="47bca-187">On hello Scheduler page, click hello job.</span></span>
   
    ![在 hello 排程器入口網站頁面上的作業][SchedulerPortal]
3. <span data-ttu-id="47bca-189">hello**工作動作**頁面隨即開啟，可以進一步設定 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="47bca-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![工作動作 PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="47bca-191"><a name="ViewJobHistory"></a>檢視 hello 作業歷程記錄</span><span class="sxs-lookup"><span data-stu-id="47bca-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="47bca-192">tooview hello 工作執行歷程記錄，包括建立 hello WebJobs SDK 按一下對應的連結下 hello**記錄**hello WebJobs 刀鋒視窗的資料行。</span><span class="sxs-lookup"><span data-stu-id="47bca-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="47bca-193">（您可以使用 hello 剪貼簿圖示 toocopy hello URL hello 記錄檔案頁面 toohello 剪貼簿 如果您想。）</span><span class="sxs-lookup"><span data-stu-id="47bca-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![記錄連結](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="47bca-195">按一下 hello 連結會開啟 hello WebJob 的 hello 詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="47bca-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="47bca-196">Hello 名稱 hello 命令執行，此頁面顯示 hello 上次執行的時間及成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="47bca-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="47bca-197">在下**最近執行的工作**，按一下 時間 toosee 進一步詳細資料。</span><span class="sxs-lookup"><span data-stu-id="47bca-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="47bca-199">hello **WebJob 執行詳細資料**頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="47bca-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="47bca-200">按一下**切換輸出**toosee hello 文字 hello 記錄內容。</span><span class="sxs-lookup"><span data-stu-id="47bca-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="47bca-201">hello 輸出記錄檔的文字格式。</span><span class="sxs-lookup"><span data-stu-id="47bca-201">hello output log is in text format.</span></span> 
   
    ![網站工作執行詳細資料][WebJobRunDetails]
4. <span data-ttu-id="47bca-203">toosee hello 輸出文字，在另一個瀏覽器視窗中，按一下 hello**下載**連結。</span><span class="sxs-lookup"><span data-stu-id="47bca-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="47bca-204">toodownload hello 文字本身，hello 連結上按一下滑鼠右鍵，並使用您的瀏覽器選項 toosave hello 的檔案內容。</span><span class="sxs-lookup"><span data-stu-id="47bca-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![下載記錄輸出][DownloadLogOutput]
5. <span data-ttu-id="47bca-206">hello **WebJobs** hello 頁面頂端的 hello 連結 hello 記錄儀表板上提供 WebJobs 便利的方式 tooget tooa 清單。</span><span class="sxs-lookup"><span data-stu-id="47bca-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![連結 tooWebJobs 清單][WebJobsLinkToDashboardList]
   
    ![歷程記錄儀表板中的 WebJobs 清單][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="47bca-209">按一下其中一個連結，會在您選取的 hello 工作 toohello WebJob 詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="47bca-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="47bca-210"><a name="WHPNotes"></a>注意</span><span class="sxs-lookup"><span data-stu-id="47bca-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="47bca-211">在免費模式中的 web 應用程式可以經過 20 分鐘後逾時，如果不有任何要求 toohello scm （部署） 站台，而且 hello web 應用程式的入口網站不是在 Azure 中開啟。</span><span class="sxs-lookup"><span data-stu-id="47bca-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="47bca-212">要求 toohello 實際站台不會重設此。</span><span class="sxs-lookup"><span data-stu-id="47bca-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="47bca-213">連續工作的程式碼需要 toobe toorun 採用無止盡的迴圈。</span><span class="sxs-lookup"><span data-stu-id="47bca-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="47bca-214">連續工作持續時才執行 hello web 應用程式已啟動。</span><span class="sxs-lookup"><span data-stu-id="47bca-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="47bca-215">基本和標準模式優惠 hello 一律上的功能，當啟用時，會防止 web 應用程式變成閒置。</span><span class="sxs-lookup"><span data-stu-id="47bca-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="47bca-216">您僅可偵錯連續執行的 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="47bca-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="47bca-217">不支援偵錯排程或隨選的 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="47bca-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="47bca-218"><a name="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="47bca-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="47bca-219">如需詳細資訊，請參閱 [Azure WebJobs 建議資源][WebJobsRecommendedResources]。</span><span class="sxs-lookup"><span data-stu-id="47bca-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

