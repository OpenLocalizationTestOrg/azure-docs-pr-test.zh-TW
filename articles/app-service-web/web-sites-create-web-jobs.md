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
# <a name="run-background-tasks-with-webjobs"></a>使用 WebJob 執行背景工作
## <a name="overview"></a>概觀
您可以使用下列三種方式，在 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式的 WebJob 中執行程式或指令碼：依需求、連續或根據排程。 沒有任何額外的成本 toouse WebJobs。

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

本文將說明如何使用 toodeploy WebJobs hello [Azure 入口網站](https://portal.azure.com)。 如需有關資訊 toodeploy 使用 Visual Studio 或持續傳遞程序，請參閱[如何 tooDeploy 應用程式的 Azure WebJobs tooWeb](websites-dotnet-deploy-webjobs.md)。

hello Azure WebJobs SDK 簡化了許多 WebJobs 的程式設計工作。 如需詳細資訊，請參閱[何謂 hello WebJobs SDK](websites-dotnet-webjobs-sdk.md)。

 Azure 的函式提供另一個方式 toorun 程式和指令碼從無伺服器環境，或從應用程式服務的應用程式。 如需詳細資訊，請參閱 [Azure Functions 概觀](../azure-functions/functions-overview.md)。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>指令碼或程式可接受的檔案類型
接受下列檔案類型的 hello:

* .cmd、.bat、.exe (使用 Windows 命令提示字元)
* .ps1 (使用 PowerShell)
* .sh (使用 Bash)
* .php (使用 PHP)
* .py (使用 Python)
* .js (使用 Node)
* .jar (使用 java)

## <a name="CreateOnDemand"></a>在 hello 入口網站中建立視 WebJob
1. 在 hello **Web 應用程式**刀鋒視窗中的 hello [Azure 入口網站](https://portal.azure.com)，按一下 **所有設定 > WebJobs** tooshow hello **WebJobs**刀鋒視窗。
   
    ![WebJob 刀鋒視窗](./media/web-sites-create-web-jobs/wjblade.png)
2. 按一下 [新增] 。 hello**新增 WebJob**對話方塊隨即出現。
   
    ![新增 WebJob 刀鋒視窗](./media/web-sites-create-web-jobs/addwjblade.png)
3. 在下**名稱**，提供 hello WebJob 的名稱。 hello 名稱必須以字母或數字開頭，且不得包含任何特殊字元不是"-"與"_"。
4. 在 hello**如何 tooRun**方塊中，選擇**視需要執行**。
5. 在 hello**檔案上傳**，按一下 hello 資料夾圖示，然後瀏覽 toohello zip 檔案包含您指令碼。 hello zip 檔案應包含可執行檔 (.exe.cmd.bat.sh.php.py.js) 以及任何支援的檔案需要 toorun hello 程式或指令碼。
6. 請檢查**建立**tooupload hello 指令碼 tooyour web 應用程式。 
   
    hello hello WebJob 所指定的名稱會出現在 hello 清單上 hello **WebJobs**刀鋒視窗。
7. toorun hello WebJob，請以滑鼠右鍵按一下在 hello 清單，然後按一下其名稱**執行**。
   
    ![執行 WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>建立連續執行的 WebJob
1. toocreate 持續執行的 WebJob，請遵循相同步驟為建立 WebJob 可執行一次，但在 hello hello**如何 tooRun**方塊中，選擇**連續**。
2. toostart 或停止連續的 WebJob 上按一下滑鼠右鍵在 hello 清單，然後按一下 hello WebJob**啟動**或**停止**。

> [!NOTE]
> 如果您的 Web 應用程式會執行多個執行個體，則連續執行的 WebJob 將會在您的所有執行個體上執行。 依需求和排定的 WebJob 會在 Microsoft Azure 為負載平衡而選取的單一執行個體上執行。
> 
> 持續的 Webjob toorun 可靠地及所有的執行個體上啟用 Alwayson 的 hello * hello web 應用程式則可以讓它們停止執行 hello SCM 主機站台已經閒置的時間太長的組態設定。
> 
> 

## <a name="CreateScheduledCRON"></a>使用 CRON 運算式建立排定的 WebJob
這項技術就是可用 tooWeb 應用程式在基本、 標準或進階模式下執行，而且需要 hello **Always On**設定 toobe hello 應用程式上啟用。

只需要包含 tooturn 上要求 WebJob 排程的 WebJob，到`settings.job`WebJob zip 檔案的 hello 根目錄的檔案。 此 JSON 檔案應該包含 `schedule` 屬性與 [CRON 運算式](https://en.wikipedia.org/wiki/Cron)，如以下範例所示。

hello CRON 運算式由 6 個欄位所組成： `{second} {minute} {hour} {day} {month} {day of hello week}`。

例如，tootrigger 您 WebJob 每隔 15 分鐘、 您`settings.job`必須：

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

其他的 CRON 排程範例：

* 每個小時 （也就是每當分鐘 hello 計數為 0）：`0 0 * * * *` 
* 每個小時，從上午 9 點 too5 PM:`0 0 9-17 * * *` 
* 每天上午 9:30： `0 30 9 * * *`
* 每個工作日上午 9:30： `0 30 9 * * 1-5`

**請注意**： 部署時，從 Visual Studio 的 WebJob，請確定 toomark 您`settings.job`檔案做為 '複本有更新時才' 屬性。

## <a name="CreateScheduled"></a>建立使用 hello Azure 排程器的 WebJob 排程
hello 下列替代技巧使用 hello Azure 排程器。 在此情況下，您的 web 工作沒有 hello 排程的任何直接知識。 相反地，hello Azure 排程器會取得設定的 tootrigger 您 WebJob 上排程。 

hello Azure 入口網站還沒有 hello 能力 toocreate 排程的 WebJob，但是在新增該功能之前可以執行使用 hello[傳統入口網站](http://manage.windowsazure.com)。

1. 在 hello[傳統入口網站](http://manage.windowsazure.com)移 toohello WebJob 頁面，然後按一下**新增**。
2. 在 hello**如何 tooRun**方塊中，選擇**依排程執行**。
   
    ![新增排程工作][NewScheduledJob]
3. 選擇 hello**排程器區域**適用於您的作業，然後按一下hello hello 右下方的 hello 對話方塊 tooproceed toohello 下一個畫面上的箭號。
4. 在 hello**建立作業** 對話方塊中，選擇 hello 類型**循環**想：**一次性的工作**或**週期性工作**。
   
    ![排定週期][SchdRecurrence]
5. 同時選擇 [啟動] 時間：[現在] 或 [在特定時間]。
   
    ![排定開始時間][SchdStart]
6. 如果您想在特定時間的 toostart，選擇 在您開始的時間值**啟動上**。
   
    ![排定於特定時間開始][SchdStartOn]
7. 如果您選擇週期性工作，您有 hello **Recur 每**選項 toospecify hello 頻率的發生次數與 hello**結束上**選項 toospecify 結束的時間。
   
    ![排定週期][SchdRecurEvery]
8. 如果您選擇**週**，您可以選取 hello**上特定排程**方塊並指定 hello 星期幾 hello 想 hello 作業 toorun。
   
    ![排程 hello 一週天數等][SchdWeeksOnParticular]
9. 如果您選擇**月**和選取 hello**上特定排程** 方塊中，您可以設定 hello 作業 toorun 特定編號**天**hello 月份。 
   
    ![排程 hello 月份中特定日期][SchdMonthsOnPartDays]
10. 如果您選擇**星期幾**，您可以選取一天或 hello 一周天數中您想要在 hello 作業 toorun 的 hello 月份。
    
     ![排定每個月的特定工作天][SchdMonthsOnPartWeekDays]
11. 最後，您也可以使用 hello**出現**選項 toochoose hello 月份中的哪一週 (第一次，第二個、 第三個等) 想 hello 作業 toorun hello 上的您所指定的星期幾。
    
    ![排定每個月特定週的特定工作天][SchdMonthsOnPartWeekDaysOccurences]
12. 建立一或多個工作之後，其名稱會出現其狀態、 排程類型與其他資訊的 hello WebJobs 索引標籤上。 歷程記錄資訊會保留的 hello 上次 30 WebJobs。
    
    ![工作清單][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>排程工作和 Azure 排程器
排程的工作可以進一步設定中的 hello hello Azure 排程器頁面[傳統入口網站](http://manage.windowsazure.com)。

1. 在 hello WebJobs 頁面上，按一下 hello 作業**排程**連結 toonavigate toohello Azure 排程器入口網站頁面。 
   
   ![連結 tooAzure 排程器][LinkToScheduler]
2. 在 hello 排程器 頁面上，按一下 hello 作業。
   
    ![在 hello 排程器入口網站頁面上的作業][SchedulerPortal]
3. hello**工作動作**頁面隨即開啟，可以進一步設定 hello 作業。 
   
    ![工作動作 PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>檢視 hello 作業歷程記錄
1. tooview hello 工作執行歷程記錄，包括建立 hello WebJobs SDK 按一下對應的連結下 hello**記錄**hello WebJobs 刀鋒視窗的資料行。 （您可以使用 hello 剪貼簿圖示 toocopy hello URL hello 記錄檔案頁面 toohello 剪貼簿 如果您想。）
   
    ![記錄連結](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. 按一下 hello 連結會開啟 hello WebJob 的 hello 詳細資料頁面。 Hello 名稱 hello 命令執行，此頁面顯示 hello 上次執行的時間及成功或失敗。 在下**最近執行的工作**，按一下 時間 toosee 進一步詳細資料。
   
    ![WebJobDetails][WebJobDetails]
3. hello **WebJob 執行詳細資料**頁面隨即出現。 按一下**切換輸出**toosee hello 文字 hello 記錄內容。 hello 輸出記錄檔的文字格式。 
   
    ![網站工作執行詳細資料][WebJobRunDetails]
4. toosee hello 輸出文字，在另一個瀏覽器視窗中，按一下 hello**下載**連結。 toodownload hello 文字本身，hello 連結上按一下滑鼠右鍵，並使用您的瀏覽器選項 toosave hello 的檔案內容。
   
    ![下載記錄輸出][DownloadLogOutput]
5. hello **WebJobs** hello 頁面頂端的 hello 連結 hello 記錄儀表板上提供 WebJobs 便利的方式 tooget tooa 清單。
   
    ![連結 tooWebJobs 清單][WebJobsLinkToDashboardList]
   
    ![歷程記錄儀表板中的 WebJobs 清單][WebJobsListInJobsDashboard]
   
    按一下其中一個連結，會在您選取的 hello 工作 toohello WebJob 詳細資料頁面。

## <a name="WHPNotes"></a>注意
* 在免費模式中的 web 應用程式可以經過 20 分鐘後逾時，如果不有任何要求 toohello scm （部署） 站台，而且 hello web 應用程式的入口網站不是在 Azure 中開啟。 要求 toohello 實際站台不會重設此。
* 連續工作的程式碼需要 toobe toorun 採用無止盡的迴圈。
* 連續工作持續時才執行 hello web 應用程式已啟動。
* 基本和標準模式優惠 hello 一律上的功能，當啟用時，會防止 web 應用程式變成閒置。
* 您僅可偵錯連續執行的 WebJobs。 不支援偵錯排程或隨選的 WebJobs。

## <a name="NextSteps"></a>後續步驟
如需詳細資訊，請參閱 [Azure WebJobs 建議資源][WebJobsRecommendedResources]。

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

